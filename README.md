## Public Servers

The UVA CS Department provides servers for computing needs. See [UVA Computing Resources](https://www.cs.virginia.edu/wiki/doku.php?id=compute_resources) for more information. 

### How to access servers

1. Log in to `portal.cs.virginia.edu` through ssh first as a forward server. If you do not have credentials yet, contact the CS IT team to request access for your computing ID.

2. Check available servers. Commonly used commands:
    - `sinfo`: Servers in the state of idle and mix are potentially available (sometimes reserved servers are not displayed correctly).
    - `scontrol show reservations` : Reserved servers are only available to users on the reservation list.
3. Then you have two choices:

    - Submit a slurm script([UVA slurm information](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm)) to run a job.
    - Use the `srun` command like the one below to use the server interactively. 
        ```
        salloc -p gpu -N 1 -c 10 --mem=30G -J InteractiveJob -t 0-00:30:00 --gres=gpu:2 -C a40
        ```
        This command allocates two A40 GPUs, 10 CPUs, and 30GB of RAM for a 30-minute session. If no duration is specified, the default maximum runtime is set to four days. More explanations about the arguments can be found in [UVA slurm information](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm).
        Once the server resources are allocated, enter the following command to access the server interactively:
        ```
        srun --pty bash -i -l --
        ```
4. If we have reserved a server([slurm reservations](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm#reservations)), add `--reservation=rry4fg_7` in the `salloc` command or `#SBATCH --reservation=rry4fg_7` in the `sbatch` script. Replace `rry4fg_7` with the reservation tag provided by IT. 
Note that you cannot use the reserved servers without the tag, even if your ID is on the reservation user ID list.


### Modules
Modules are pre-installed software packages in the Slurm system that users can access without root or sudo privileges. 

To view the list of available modules, use the command `module avail`. To load a required module, such as nvtop, use `module load nvtop`. 

If a needed module is not available, contact the CS IT team for assistance with installation or alternative solutions. See [Software Modules](https://www.cs.virginia.edu/wiki/doku.php?id=linux_environment_modules) for more information. 

### Development servers
The `gpusrv[01-19]` servers([GPU servers](https://www.cs.virginia.edu/wiki/doku.php?id=compute_resources#gpu_servers)), which are low GPU memory servers, can be directly accessed via SSH for developing and debugging code. 


### Server Issues
If you encounter any hardware or software issues with the servers, send an email to cshelpdesk@virginia.edu. 

