## Public Servers

The UVA CS Department provides servers for computing needs. See [UVA Computing Resources](https://www.cs.virginia.edu/wiki/doku.php?id=compute_resources) for more information. 

### How to use

1. Log in to `portal.cs.virginia.edu` through ssh first as a forward server. If you do not have credentials yet, contact the CS IT team to request access for your computing ID.

2. You have two choices:

    - Submit a slurm script([UVA slurm information](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm)) to run a job.
    - Use the `srun` command like the one below to use the server interactively. Explanations about the arguments can be found in [UVA slurm information](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm). 
        ```
        srun -w puma02 -p gpu --pty bash -i -l -
        ```
3. If we have reserved a server like `puma02` ([slurm reservations](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm_reservations)), use the command below instead.  Replace `rry4fg_7` with the reservation tag provided by IT. Note that you cannot use the reserved servers without the tag, even if your ID is on the reservation user ID list.
    ```
    srun --reservation=rry4fg_7  -w puma02 -p gpu --pty bash -i -l - 
    ```

### Server Issues
If you encounter any hardware or software issues with the servers, send an email to cshelpdesk@virginia.edu. 

