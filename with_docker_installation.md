# Installing FLASH with Docker
source: https://github.com/acreyes/FlashSummer/blob/main/docs/IntroSciComp.md

There are 4 steps: 
1. Install required applications: VS Code, Docker Desktop, VisIt (for visualization)
2. Get FLASH source code
3. Set up VS Code
4. Attach Docker container for FLASH to VS Code


# 1. Install applications

* VS Code: https://code.visualstudio.com/download?_exp_download=fb315fc982
* Docker Desktop: https://docs.docker.com/desktop/setup/install/mac-install/
* VisIt: https://visit-dav.github.io/visit-website/index.html
   

# 2. Get FLASH source code
Request access from: https://flash.rochester.edu/site/

# 3. Set up VS Code

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

Then download Dockerfile from: 
https://github.com/acreyes/FlashSummer/blob/main/Dockerfile

In VS Code open terminal and go to home directory:
```bash
cd
```

In home directory make new working directory where you want to install flash:
```bash
mkdir WorkDirectory
```
(you can change name of directory as preferred)

in this new directory copy tar file of the code and downloaded Dockerfile (adjust names of files or directories if needed):

```bash
cp ~/Downloads/FLASH4.8.tar.gz ~/FLASH/
```

```bash
cp ~/Downloads/Dockerfile.txt ~/FLASH/
```

Rename "Dockerfile.txt" to "Dockerfile":

```bash
mv Dockerfile.txt Dockerfile
```



# 4. Attach Docker container for FLASH to VS Code

Type: 

```bash
docker build . –t flashcenter/flash4-deps-dev:latest
```
it will take time to build. 

If you get following error:
```bash
ERROR: “docker buildx build” requires exactly 1 argument.See ‘docker buildx build --help’.
```
just type command by hand instead of copy-paste. 

Then after building is complete, type: 
```bash
make -j
docker container create -i -t -h gnu-mpich --name flash4 -v $(pwd):/mnt/data flashcenter/flash4-deps-dev
```
Now you should have attached docker container in your VS Code environment. 

To open container in VS Code:

go to remote explorer, and find flash container "flashcenter/flash4-deps-dev"

<img width="358" height="354" alt="Screenshot 2026-08-13 at 13 57 40" src="https://github.com/user-attachments/assets/0777fcda-24fb-4c23-98e0-5c7efff9166d" />


