---
title: CS department servers
has_children: true
nav_order: 1
---

## CS department servers

The UVA CS Department provides servers for computing needs. See [UVA Computing Resources](https://www.cs.virginia.edu/wiki/doku.php?id=compute_resources) for more information. 

### How to access servers

1. Log in to `portal.cs.virginia.edu` through ssh first as a forward server. If you do not have credentials yet, contact the CS IT team to request access for your computing ID.

2. Check available servers. Commonly used commands:
    - `sinfo`: Servers in the state of idle and mix are potentially available (sometimes reserved servers are not displayed correctly).
    - `squeue -p gpu`: Check the queue of the gpu partition to see if there are any jobs waiting to be run.
    - `scontrol show job <jobid>`: Check the status of a specific job. This could be used to check if a job is waiting for a server that you are also waiting for. 
    - `scontrol show node <node>`: Check the status of a specific node. This could be used to check the available resources on a node. 
    - `scontrol show res` : List all reservations including the server, users, and time. Reserved servers are only available to users on the reservation list.
3. Then you have two choices:

    - Submit a slurm script([UVA slurm information](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm)) to run a job. An example is below:
        ```bash
        #!/bin/bash

        #SBATCH --job-name=your_job_name
        #SBATCH --output=%x_%j.out
        #SBATCH --error=%x_%j.err
        #SBATCH --partition=gpu
        #SBATCH --nodes=1
        #SBATCH --ntasks-per-node=1
        #SBATCH --cpus-per-task=10
        #SBATCH --gres=gpu:4
        #SBATCH --mem=50G
        #SBATCH --time=D-HH:MM:SS
        #SBATCH --constraint="a40|a100_80gb|a100_40gb|h100_80gb"   # The requested gpu type could be either a40, a100_80gb, a100_40gb or h100_80gb
        #SBATCH --reservation=<reservation name>                   # If you have a reservation on the targeted node
        #SBATCH --mail-type=begin,end,fail
        #SBATCH --mail-user=<computingID>@virginia.edu

        module load cuda-toolkit-11.8.0                            # Optional, according to your project

        python your_script.py --your_arguments xxx
        ```
        Use `sbatch mysbatchscript.sh` to submit the slurm script.
    - Use the `salloc` command like the one below to use the server interactively. 
        ```
        salloc -p gpu -N 1 -c 10 --mem=30G -J InteractiveJob -t 0-00:30:00 --gres=gpu:2 -C a100_80gb
        ```
        This command allocates two A100 80GB GPUs, 10 CPUs, and 30GB of RAM for a 30-minute session. If no duration is specified, the default maximum runtime is set to four days. More explanations about the arguments can be found in [UVA slurm information](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm).
        Once the server resources are allocated, enter the following command to access the server interactively:
        ```
        srun --pty bash -i -l --
        ```
4. After a job is started, you could use `srun --pty --overlap --jobid=<jobid> <command>` to run a command on the server. This is useful when you want to run a command on a server that is already running a job. For example, the `<command>` could be `nvtop` to check the GPU usage of the running job. The `<command>` could also be `bash` to open a new terminal on the server. 
5. If we have reserved a server([slurm reservations](https://www.cs.virginia.edu/wiki/doku.php?id=compute_slurm#reservations)), add `--reservation=rry4fg_7` in the `salloc` command or `#SBATCH --reservation=rry4fg_7` in the `sbatch` script. Replace `rry4fg_7` with the reservation tag provided by IT. 
Note that you cannot use the reserved servers without the tag, even if your ID is on the reservation user ID list.

### Public server owned by our group

Node `cheetah06` contains 8 80GB A100 GPUs and is owned by our group. It is open to the public and on the slurm queues. To prevent others from using the machine, you need to put a reservation. Actually, anyone can reserve the server, so for upcoming submission deadlines, it is better to reserve the server in advance. Remember to put all the group members on the list of who can access the reserved server.

### Modules
Modules are pre-installed software packages in the Slurm system that users can access without root or sudo privileges. 

To view the list of available modules, use the command `module avail`. To load a required module, such as nvtop, use `module load nvtop`. 

If a needed module is not available, contact the CS IT team for assistance with installation or alternative solutions. See [Software Modules](https://www.cs.virginia.edu/wiki/doku.php?id=linux_environment_modules) for more information. 

### Development servers
The `gpusrv[01-19]` servers([GPU servers](https://www.cs.virginia.edu/wiki/doku.php?id=compute_resources#gpu_servers)), which are low GPU memory servers, can be directly accessed via SSH for developing and debugging code. 


### Server Issues
If you encounter any hardware or software issues with the servers, send an email to cshelpdesk@virginia.edu. 

