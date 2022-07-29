<div class="top">

# Lists
### [◂](command:katapod.loadPage?step4){.steps} Step 5 of 10 [▸](command:katapod.loadPage?step6){.steps}
</div>

A *list* is an ordered collection of values, where the same value may occur more than once. 
In Cassandra, lists are intended for 
storing a small number of values of the same type. To define a list data type, 
Cassandra Query Language provides construct `LIST<type>`, where `type` can refer to a CQL data type like 
`INT`, `DATE`, `UUID` and so forth.

As an example, alter table `users` to add column `searches` of type `LIST<TEXT>`:
```
ALTER TABLE users ADD searches LIST<TEXT>;
SELECT id, name, searches FROM users;
```

Add three latest search leterals for one of the users:
```
UPDATE users 
SET searches = [ 'Alice in Wonderland' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
UPDATE users 
SET searches = searches + [ 'Comedy movies' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
UPDATE users 
SET searches = searches + [ 'Alice in Wonderland' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT id, name, searches FROM users;
```

Delete the oldest search literal and add a new one:
```
DELETE searches[0] FROM users 
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
UPDATE users 
SET searches = searches + [ 'New releases' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT id, name, searches FROM users;
```

Next, alter table `users` to add column `emails` and 
add two email addresses for one of the users:
<details>
  <summary>Solution</summary> 

```
ALTER TABLE users ADD emails LIST<TEXT>;

UPDATE users 
SET emails = [ 'joe@datastax.com', 
               'joseph@datastax.com' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

SELECT id, name, emails FROM users;
```

</details>

[continue](command:katapod.loadPage?step6){.orange_bar}