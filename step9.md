<div class="top">

# UDTs
### [◂](command:katapod.loadPage?step8){.steps} Step 9 of 10 [▸](command:katapod.loadPage?step10){.steps}
</div>

A *user-defined type (UDT)* is a custom data type composed of one or more named and typed fields. 
UDT fields can be of simple types, collection types or even other UDTs. 
Cassandra Query Language provides statements `CREATE TYPE`, `ALTER TYPE`, `DROP TYPE` and `DESCRIBE TYPE` 
to work with UDTs.

Let's define UDT `ADDRESS` with four fields:
```
CREATE TYPE ADDRESS (
    street TEXT,
    city TEXT,
    state TEXT,
    postal_code TEXT
);
```

Alter table `users` to add column `address` of type `ADDRESS`:
```
ALTER TABLE users ADD address ADDRESS;
SELECT name, address FROM users;
```

Add an address for one of the users:
```
UPDATE users 
SET address = { street: '1100 Congress Ave',
                city: 'Austin',
                state: 'Texas',
                postal_code: '78701' }
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, address FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

UPDATE users 
SET address.state = 'TX'
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, 
       address.street      AS street, 
       address.city        AS city, 
       address.state       AS state,
       address.postal_code AS zip 
FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
```

Next, alter table `users` to add column `previous_addresses` and 
add at least two previous addresses for one of the users:
<details>
  <summary>Solution</summary> 

```
ALTER TABLE users 
ADD previous_addresses LIST<FROZEN<ADDRESS>>;

UPDATE users 
SET previous_addresses = [
              { street: '10th and L St',
                city: 'Sacramento',
                state: 'CA',
                postal_code: '95814' } ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, previous_addresses FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

UPDATE users 
SET previous_addresses = previous_addresses + [
              { street: 'State St and Washington Ave',
                city: 'Albany',
                state: 'NY',
                postal_code: '12224' } ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, address, previous_addresses FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
```

</details>

[continue](command:katapod.loadPage?step10){.orange_bar}
