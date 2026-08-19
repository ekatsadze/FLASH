# Installing FLASH with Docker

There are 4 steps: 
1. Install required applications: VS Code, Docker Desktop, VisIt (for visualization)
2. Get FLASH source code
3. Set up VS Code
4. Attach Docker container for FLASH to VS Code


# 1. Install required applications

* VS Code: https://code.visualstudio.com/download?_exp_download=fb315fc982
* Docker Desktop: https://docs.docker.com/desktop/setup/install/mac-install/
* VisIt (for visualization): https://visit-dav.github.io/visit-website/index.html


# 2. Get FLASH source code
Request access from: https://flash.rochester.edu/site/

<img width="1295" height="658" alt="Screenshot 2026-08-19 at 10 35 43" src="https://github.com/user-attachments/assets/c66e48e1-d366-478f-9686-d2a014311882" />

<br>

After getting access you will receive email with link from where you will be able to download the tar file of source code.

# 3. Set up VS Code

We will be working in VS Code. To setup application for running FLASH:

We will need few VS Code extensions. Open VS Code → Click Extensions icon on the left part of application, and install extensions.

## Required Extensions:
1. Remote Explorer
2. Dev Container



<img width="447" height="406" alt="Screenshot 2026-08-19 at 10 16 57" src="https://github.com/user-attachments/assets/70f1d065-1963-4144-92e6-45fbc9eb65aa" />


---

It will be also useful to install 'code' (for opening/editing files later). To install it, open Command Palette (Cmd+Shift+P) and
 type: 
```bash 
>Shell Command: install 'code' command in PATH
```
<br>

<img width="1510" height="271" alt="Screenshot 2026-08-19 at 10 48 54" src="https://github.com/user-attachments/assets/dc5b0dc7-0a7c-4020-abab-a5bd759c1b29" />

<br>

It will ask for your device password. 

---

Then download Dockerfile from: 
https://github.com/acreyes/FlashSummer/blob/main/Dockerfile

<img width="1170" height="478" alt="Screenshot 2026-08-19 at 10 21 47" src="https://github.com/user-attachments/assets/19ad126b-99e6-4a4d-9282-9a5d61b95138" />


<br>

---

## Note: for next steps we will be working in VS Code terminal

Make sure you are in home directory:
```bash
cd
```

In home directory make a new directory where you will be working with FLASH code:
```bash
mkdir FLASH
```
(you can change name of directory as preferred)

Go to new directory:
```bash
cd FLASH
```

in this new directory copy tar file of the code and downloaded Dockerfile (adjust name of tar file if you download different version of code):

```bash
cp ~/Downloads/FLASH4.8.tar.gz .
```

```bash
cp ~/Downloads/Dockerfile.txt .
```

Rename "Dockerfile.txt" to "Dockerfile":

```bash
mv Dockerfile.txt Dockerfile
```

--- 

# Additional steps for Windows users only
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

## Note: Continue next steps in WSL terminal.
--- 

# 4. Attach Docker container for FLASH to VS Code

Make sure you are in 'FLASH' directory containing tar file and Dockerfile.

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
docker container create -i -t -h gnu-mpich --name flash4 -v $(pwd):/mnt/data flashcenter/flash4-deps-dev
```
This will attach docker container in your VS Code environment. 

---

## To open container in VS Code:

Click remote explorer icon on left side of VS code and find flash container "flashcenter/flash4-deps-dev":

<img width="358" height="354" alt="Screenshot 2026-08-13 at 13 57 40" src="https://github.com/user-attachments/assets/0f0708e2-242b-44e2-a1dd-bc69ffe6b39a" />


<br>

# Sources: 
* https://github.com/acreyes/FlashSummer/blob/main/docs/IntroSciComp.md
* Presentation by Kassie Moczulski, Abigail Armstrong & Petros Tzeferacos


