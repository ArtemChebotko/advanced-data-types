<div class="top">

# Tuples
### [◂](command:katapod.loadPage?step7){.steps} Step 8 of 10 [▸](command:katapod.loadPage?step9){.steps}
</div>

A *tuple* is a fixed-length list, where values can be of different types. 
To define a tuple data type, 
Cassandra Query Language provides construct `TUPLE<type1,type2,..., typeN>`, 
where `type1` , `type2` , ... , `typeN` can refer to same or different CQL data types, including 
`INT`, `DATE`, `UUID` and so forth. 

Here is an example of a `TUPLE` column:
```
ALTER TABLE users ADD full_name TUPLE<TEXT,TEXT,TEXT>;

UPDATE users 
SET full_name = ('Joe', 'The', 'Great')
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

SELECT name, full_name FROM users;
```

Unlike UDTs, individual tuple components cannot be updated without updating the whole tuple. Therefore, 
you should *always prefer UDTs to tuples*.

[continue](command:katapod.loadPage?step9){.orange_bar}
