<div class="top">

# Sets
### [◂](command:katapod.loadPage?step3){.steps} Step 4 of 10 [▸](command:katapod.loadPage?step5){.steps}
</div>

A *set* is an unordered collection of distinct values. In Cassandra, sets are intended for 
storing a small number of values of the same type. To define a set data type, 
Cassandra Query Language provides construct `SET<type>`, where `type` can refer to a CQL data type like 
`INT`, `DATE`, `UUID` and so forth.

As an example, alter table `movies` to add column `production` of type `SET<TEXT>`:
```
ALTER TABLE movies ADD production SET<TEXT>;
SELECT title, year, production FROM movies;
```

Add three production companies for one of the movies:
```
UPDATE movies 
SET production = { 'Walt Disney Pictures', 
                   'Roth Films' }
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
UPDATE movies 
SET production = production + { 'Team Todd' } 
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
SELECT title, year, production FROM movies;
```

Next, alter table `movies` to add column `genres` and 
add values *Adventure*, *Family* and *Fantasy* for one of the movies:
<details>
  <summary>Solution</summary>

```
ALTER TABLE movies ADD genres SET<TEXT>;

UPDATE movies 
SET genres = { 'Adventure', 'Family', 'Fantasy' }
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;

SELECT title, year, genres FROM movies;
```

</details>

[continue](command:katapod.loadPage?step5){.orange_bar}