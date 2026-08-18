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
* 1. Setup
     Directory: in FLASH4.8
     To setup problem you need to enter setup line.
     Example setup line for LaserSlab problem:
     ```bash
     ./setup -auto LaserSlab -2d +cylindrical -nxb=16 -nyb=16 +hdf5typeio species=cham,targ +mtmmmt +laser +uhd3t +mgd mgd_meshgroups=6 -parfile=example.par
     ```
     Look for more detailed infromation in flash user guide:

      https://flash.rochester.edu/site/flashcode/user_support/flash_ug_devel.pdf 

      for LaserSlab go to chapter “Full-physics Laser Driven Simulation”.
* 2. Compile
     Directory: object directory (which is in FLASH4.8 directory)
     ```bash
     make -j
     ```
* 3. Run  
