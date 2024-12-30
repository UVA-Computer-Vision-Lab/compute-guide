---
title: Storage
parent: CS department servers
has_children: false
nav_order: 2
---


## Storage

There are three commonly used storage directories:
- `/u/computing_id`: The home directory, which has a limit of 100GB.
- `/bigtemp/computing_id`: A temporary storage system with no maximum limits. First, you need to create a directory named after your computing id under `/bigtemp`. 
- `/p/project_name`: The project directory that could be created by requesting IT people. It can be accessed by multiple collaborators. The limit usually starts at 500GB and could be extended by requesting IT. 

Note: 
- The home directory (/u) and project directory (/p) filesystems are backed up using a ZFS snapshot each night. These snapshots are retained for one month.

- The bigtemp directory (/bigtemp) is **not backed up**, so avoid storing important files in this directory. In the past, unforeseen circumstances have led to the loss of all data and code stored in /bigtemp. To prevent such incidents, use this directory only for temporary, non-essential files.

See [UVA CS Storage](https://www.cs.virginia.edu/wiki/doku.php?id=start#storage) for more information. 