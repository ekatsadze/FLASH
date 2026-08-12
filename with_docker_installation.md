# Installing FLASH with Docker
source: https://github.com/acreyes/FlashSummer/blob/main/docs/IntroSciComp.md

There are 3 steps: 
1. Install applications: VS Code, Docker Desktop, VisIt (for visualization)
2. Get FLASH source code
3. Set up and attach to the FLASH Docker container

# 1. Install applications

* VS Code: https://code.visualstudio.com/download?_exp_download=fb315fc982
* Docker Desktop: https://docs.docker.com/desktop/setup/install/mac-install/
* VisIt: https://visit-dav.github.io/visit-website/index.html
   

# 2. Get FLASH source code
Request access from: https://flash.rochester.edu/site/

# 3. Set up and attach to the FLASH Docker container

We will be working in VS Code. To run FLASH we need to attach Docker container for FLASH to VS Code. For that we will need few extensions inside app.

Open VS Code → Click Extensions icon on the left part of application, and install extensions:

1. Remote Explorer
2. Dev Container
3. Might also need to install python if you don’t have already

Another useful thing to install is code (for opening/editing files later). To install it in Command Palette type: 
```bash 
>Shell Command: install 'code' command in PATH
```
will ask your device password. 

Download Dockerfile from: 
https://github.com/acreyes/FlashSummer/blob/main/Dockerfile
