<div class="top">

# Maps
### [◂](command:katapod.loadPage?step5){.steps} Step 6 of 10 [▸](command:katapod.loadPage?step7){.steps}
</div>

A *map* is a collection of key-value pairs, where each pair has a unique key. 
In Cassandra, maps are intended for 
storing a small number of key-value pairs of the same type. To define a map data type, 
Cassandra Query Language provides construct `MAP<type1,type2>`, where `type1` and `type2` can refer to same or different CQL data types, including 
`INT`, `DATE`, `UUID` and so forth.

As an example, alter table `users` to add column `sessions` of type `MAP<TIMEUUID,INT>`:
```
ALTER TABLE users ADD sessions MAP<TIMEUUID,INT>;
SELECT name, sessions FROM users;
```

Add two sessions with `TIMEUUID` keys and `INT` duration values for one of the users:
```
UPDATE users 
SET sessions = { now(): 32, 
    e22deb70-b65f-11ea-9aac-99396fc4f757: 7 }
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, sessions FROM users;
```

Update a duration value for one of the sessions:
```
UPDATE users 
SET sessions[e22deb70-b65f-11ea-9aac-99396fc4f757] = 9 
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, sessions FROM users;
```

Next, alter table `users` to add column `preferences` and 
add key-value pairs (*color-scheme*: *dark*) and (*quality*: *auto*) for one of the users:
<details>
  <summary>Solution</summary> 

```
ALTER TABLE users ADD preferences MAP<TEXT,TEXT>;

UPDATE users 
SET preferences['color-scheme'] = 'dark'
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
UPDATE users 
SET preferences['quality'] = 'auto' 
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

SELECT name, preferences FROM users;
```

</details>

[continue](command:katapod.loadPage?step7){.orange_bar}