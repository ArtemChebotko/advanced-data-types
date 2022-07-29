<div class="top">

# Let's get started ...
### [◂](command:katapod.loadPage?step1){.steps} Step 2 of 10 [▸](command:katapod.loadPage?step3){.steps}
</div>

Start the CQL shell:
```
cqlsh
```

Create the keyspace:
```
CREATE KEYSPACE killr_video
WITH replication = {
  'class': 'NetworkTopologyStrategy', 
  'DC-Houston': 1 }; 
```

Set the current working keyspace:
```
USE killr_video;
```

[continue](command:katapod.loadPage?step3){.orange_bar}