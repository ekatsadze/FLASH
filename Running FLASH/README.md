# Steps for Running FLASH
1.  If you installed FLASH with Docker:
     * open VS code
     * go to remote explorer
     * open flash container
       <img width="358" height="354" alt="Screenshot 2026-08-13 at 13 57 40" src="https://github.com/user-attachments/assets/0f0708e2-242b-44e2-a1dd-bc69ffe6b39a" />
       
     * open terminal in VS code
     * ```bash 
       cd /mnt/data/FLASH/FLASH4.8
       ```


2.  If you installed FLASH locally:
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

## Setting up your own simulation:
FLASH code already comes with standard test problems, which you will be able to find here:
     ```bash
     FLASH4.8/source/Simulation/SimulationMain/
     ```
or for MHD probelems: 
     ```bash
     FLASH4.8/source/Simulation/SimulationMain/magnetoHD
     ```

To do your own simulation, you mainly will need these 6 files:
     * flash.par (par file can be named differently): text file that specifies values for the runtime parameters.
     note: FLASH uses CGS units for all parameters (almost).
     * Config: for choosing physics modules for problem, adding new runtime parameters and so on.
     * Simulation_data.F90: where you define global runtime parameters
     * Simulation_init.F90: where you initialize global simulation parameters (reads runtime parameters)
     * Simulation_initBlock.F90: where we set initial conditions, geometry and so on.
     * Makefile

All these files should be in your simulation directory:
     ```bash
     FLASH4.8/source/Simulation/SimulationMain/"Your_directory_name"       
     ```
After you setup your problem these files (besides Config, which will only be in source/Simulation/SimulationMain/"Your_directory_name") will also copied in object directory:
     ```bash
     FLASH4.8/object      
     ```
## Changing parameters:
If you are changing any of these files in FLASH4.8/Simulation/SimulationMain/"Your_directory_name" directory you need to re-setup the problem then re-compile and then re-run.

If you are changing them in your object directory you need to only re-compile and then re-run (only file you won't be able to change in object directory is Config). 

If you are changing only flash.par you need to only to re-run the problem.





