# Steps for Running FLASH
1.  If you installed FLASH with Docker:
     * open VS code
     * go to remote explorer
     * open FLASH container      
     * open terminal in VS code   
     * go to your FLASH directory:
        ```bash 
        cd /mnt/data/FLASH/FLASH4.8
        ```
        FLASH container will look like this:

        <img width="358" height="354" alt="Screenshot 2026-08-13 at 13 57 40" src="https://github.com/user-attachments/assets/0f0708e2-242b-44e2-a1dd-bc69ffe6b39a" />

    <br />

2.  If you installed FLASH locally:
* Go to your FLASH directory: from terminal (either from VS Code terminal or your mac terminal) go to home directory:
     ```bash 
     cd
     ```
    then go to directory where you installed FLASH:
    ```bash 
     cd WorkDirectory/FLASH4.8
     ```
     
Note: change name of directories or version of FLASH you installed if they are different.

---

# For running FLASH simulations there are three steps:
### 1.  Setup
#### Directory: FLASH4.8

To setup problem you need to enter setup line. Example setup line for LaserSlab problem:
```bash
./setup -auto LaserSlab -2d +cylindrical -nxb=16 -nyb=16 +hdf5typeio species=cham,targ +mtmmmt +laser +uhd3t +mgd mgd_meshgroups=6 -parfile=example.par
```
Look for more detailed infromation in flash user guide:

https://flash.rochester.edu/site/flashcode/user_support/flash_ug_devel.pdf 

for LaserSlab go to chapter “Full-physics Laser Driven Simulation”.

### 2.  Compile
#### Directory: object directory (which is in FLASH4.8 directory)
```bash
make -j
```
note: 
* “make -j” uses all available processors;
* “make” uses one processor 
* “make -j4” uses four processors  

### 3.  Run
#### Directory: running directory (which can be same as object directory or different directory if you created it specifically for running)
```bash
mpirun -np 4 ./flash4
```
“-np 4” here is number of processors; “flash4” is executable which is generated after compiling; "./" specifies location of executable (in this case flash4 is in the current directory - object directory)

---

# Setting up your own simulation:
FLASH code already comes with standard test problems, which you will be able to find here:
```bash
FLASH4.8/source/Simulation/SimulationMain/
```
or for MHD problems: 
```bash
FLASH4.8/source/Simulation/SimulationMain/magnetoHD
```

### Main Simulation Files

To set up your own simulation, you will mainly need the following six files:

- #### `flash.par`
    Text file that specifies values for the runtime parameters. It specifies the values of the runtime parameters used in the simulation.

    **Note:** The parameter file can have a different name. FLASH uses CGS units for almost all physical quantities.

- #### `Config`
    Defines the physics modules and other components included in the simulation. It is also used to declare new runtime parameters.

- #### `Simulation_data.F90`
    Defines global variables and runtime parameters.

- #### `Simulation_init.F90`
    Initializes global simulation parameters and reads the runtime parameter values specified in Simulation_data.F90.

- #### `Simulation_initBlock.F90`
    Sets the initial conditions, geometry, and other problem-specific quantities.

- #### `Makefile`
    Contains the build instructions and dependencies needed to compile the simulation.


All these files should be in your simulation directory:
```bash
FLASH4.8/source/Simulation/SimulationMain/"Your_directory_name"       
```
After you setup your problem, these files will also copied in object directory (besides Config, which will only be in source/Simulation/SimulationMain/"Your_directory_name"):
```bash
FLASH4.8/object      
```

---

# Changing parameters:
* If you are changing any of these files in FLASH4.8/Simulation/SimulationMain/"Your_directory_name" directory you need to re-setup the problem then re-compile and then re-run.

* If you are changing them in your object directory you only need to re-compile and then re-run (only file you won't be able to change in object directory is Config). 

* If you are changing only flash.par you only need to re-run the problem.

---

# Organize and manage data:

### 1.  Setup

Before setting up problem, make a new directory in SimulationMain directory:
```bash
mkdir Your_directory_name
```
or copy similar test problem:
```bash
cp -r LaserSlab Your_directory_name
```
It is always useful to have new directories if you plan to change something, so if something goes wrong you can always go back to original test problem. 

In similar way we will make new object directory, instead of overwriting in one object directory.

You can do same setup line but instead of LaserSlab you use Your_directory_name and in the end you can also specify your new object directory name:
```bash
./setup -auto Your_directory_name -2d +cylindrical -nxb=16 -nyb=16 +hdf5typeio
species=cham,targ +mtmmmt +laser +uhd3t +mgd mgd_meshgroups=6 -parfile=example.par -objdir=object_directory_name
```
this will setup problem in new directory (object_directory_name), which will be your new object directory. 

### 2.  Compile

Compilation will be same way, just make sure you are in your new object directory (object_directory_name):

```bash
make -j
```

### 3.  Run

Before running, in your new object directory make new directory:
```bash
mkdir data 
```
```bash
cp flash.par data/
```
```bash
cd data
```
This is especially useful if you want to do several runs with different runtime parameters. It will be also easier to find your output files easier. 

Now you will be in ```/FLASH4.8/object_directory_name/data``` and you will run simulation here. 

note: you have to copy par file to run in data directory. For problems, where you use tabulated eos, you will also need to copy those eos files. 

For example, in LaserSlab problem we have two materials helium and aluminum, so you need to copy two ionmix files: al-imx-003.cn4 and he-imx-005.cn4 in data directory. If you are already in data directory you can use this command to copy all ionmix files:
```bash
cp ../*imx* .
```
Now you are able to run:
```bash
mpirun -np 4 ../flash4
```
Note that for running now you do two dots, because your flash4 is in object directory (previous directory).

# IMPORTANT: Make sure you are always in correct directory for each of these steps to go smooth.







