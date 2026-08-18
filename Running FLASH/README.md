# Steps for Running FLASH
If you installed FLASH with Docker, to work with FLASH code you have to:
* open vs code
* go to remote explorer
* open flash container
* open terminal in VS code
* cd to /mnt/data/FLASH/FLASH4.8


If you installed FLASH locally, to work with FLASH code you have to:
* Go to your FLASH directory: from terminal (either from VS Code terminal or your mac terminal) go to home directory:
```bash 
cd
```
then go to directory where you installed FLASH:
```bash 
cd WorkDirectory/FLASH4.8
```
Note: change name of version of FLASH you installed if it's different.

## For running FLASH there are three steps:
1. Setup
     Directory: in FLASH4.8
     To setup problem you need to enter setup line.
     Example setup line for LaserSlab problem:
     ```bash
     ./setup -auto LaserSlab -2d +cylindrical -nxb=16 -nyb=16 +hdf5typeio species=cham,targ +mtmmmt +laser +uhd3t +mgd mgd_meshgroups=6 -parfile=example.par
     ```
     Look for more detailed infromation in flash user guide:

      https://flash.rochester.edu/site/flashcode/user_support/flash_ug_devel.pdf 

      for LaserSlab go to chapter “Full-physics Laser Driven Simulation”.
2. Compile
     Directory: object directory (which is in FLASH4.8 directory)
     ```bash
     make -j
     ```
     note: “make -j” uses all available processors, just “make” uses one processor or you can specify how many processors you need with “make -j 4”. 
3. Run
     Directory: running directory (which can be same as object directory or any other directory which you will make specifically for running)
     ```bash
     mpirun -np 4 ./flash4
     ```
     “-np 4” here is number of processors; “flash4” is executable which generated after compiling; "./" specifies location of executable (in this case flash4 is in same directory where we compiled - object directory is same as running directory)

## Changing test problem/Setting up your own simulation:
If you need to change one of the test problem and doing your own simulation, you mainly will change things in:
