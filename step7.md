<div class="top">

# Nested collections
### [◂](command:katapod.loadPage?step6){.steps} Step 7 of 10 [▸](command:katapod.loadPage?step8){.steps}
</div>

It is also possible to define collection data types that contain nested collections, such as *list of maps* or 
*set of sets of sets*. A nested collection definition has to be designated as `FROZEN`, which means that a nested collection 
is stored as a single blob value and manipulated as a whole. In other words, when an individual element 
of a frozen collection needs to be updated, the entire collection must be overwritten. As a result, nested collections 
are generally less efficient unless they hold immutable or rarely changing data. 

Let's alter table `movies` again to be able to store movie casts and crews in column `crew` of type `MAP<TEXT,FROZEN<LIST<TEXT>>>`:
```
ALTER TABLE movies 
ADD crew MAP<TEXT,FROZEN<LIST<TEXT>>>;
SELECT title, year, crew FROM movies;
```

Add a movie crew:
```
UPDATE movies 
SET crew = { 
  'cast': ['Johnny Depp', 'Mia Wasikowska'], 
  'directed by': ['Tim Burton']
 }
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
SELECT title, year, crew FROM movies;
```

[continue](command:katapod.loadPage?step8){.orange_bar}
