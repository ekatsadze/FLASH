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
* VisIt (for visualization): https://visit-dav.github.io/visit-website/index.html


# 2. Get FLASH source code
Request access from: https://flash.rochester.edu/site/

and download the tar file of source code.

# 3. Set up VS Code

We will be working in VS Code. To run FLASH we need to attach Docker container for FLASH to VS Code. For that we will need few extensions inside app.

Open VS Code → Click Extensions icon on the left part of application, and install extensions:

<img width="447" height="406" alt="Screenshot 2026-08-19 at 10 16 57" src="https://github.com/user-attachments/assets/70f1d065-1963-4144-92e6-45fbc9eb65aa" />

1. Remote Explorer
2. Dev Container
3. Might also need to install python if you don’t already have it


---

It will be also useful to install 'code' (for opening/editing files later). To install it in Command Palette (Cmd+Shift+P) and
 type: 
```bash 
>Shell Command: install 'code' command in PATH
```
<img width="591" height="79" alt="Screenshot 2026-08-19 at 10 18 41" src="https://github.com/user-attachments/assets/175707e4-1b9c-4e8f-ac7f-f381776b2d50" />

It will ask for your device password. 

---

Then download Dockerfile from: 
https://github.com/acreyes/FlashSummer/blob/main/Dockerfile

<img width="1170" height="478" alt="Screenshot 2026-08-19 at 10 21 47" src="https://github.com/user-attachments/assets/19ad126b-99e6-4a4d-9282-9a5d61b95138" />

Rename "Dockerfile.txt" to "Dockerfile":
```bash
cd ~/Downloads
```

```bash
mv Dockerfile.txt Dockerfile
```

--- 

In VS Code open terminal and go to home directory:
```bash
cd
```

In home directory make new working directory where you want to install FLASH code:
```bash
mkdir WorkDirectory
```
(you can change name of directory as preferred)

in this new directory copy tar file of the code and downloaded Dockerfile (adjust names of tar file if you download different version and name of directory if you change it):

```bash
cp ~/Downloads/FLASH4.8.tar.gz ~/WorkDirectory/
```

```bash
cp ~/Downloads/Dockerfile ~/WorkDirectory/
```

--- 

# Additional steps for Windows users:
To run FLASH on Windows, you will need to install WSL. 
Open PowerShell as administrator and run: 
```bash
wsl --install
```
Restart computer if Windows asks for it.
If it does not start installing something, try the following:
```bash
wsl --install -d Ubuntu
```
Verify installation and version with: 
```bash
wsl -l -v
```
This should say version 2.

Docker requires WSL2. If it says WSL1 convert it to WSL2:
```bash
wsl --set-version Ubuntu 2
```

After that make sure Docker is integrated with WSL:
* Open Docker application
* Go to Settings
* Click resources
* Activate WSL integration: "Enable integration with my default WSL distro"
* Click Apply & Restart

Then open terminal (either VS Code terminal or command prompt) and type:
```bash
ubuntu
```
This will open WSL environment.

After this go to directory containing FLASH.

--- 

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

<img width="358" height="354" alt="Screenshot 2026-08-13 at 13 57 40" src="https://github.com/user-attachments/assets/0f0708e2-242b-44e2-a1dd-bc69ffe6b39a" />



