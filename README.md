# Remotely Debug C++ Programs on RPI Using VS Code

# Step 1 : Download and install the following items

## 1. [Visual Studio Code](https://code.visualstudio.com/)

-   Once you've opened VS Code
-   Click `EXTENSIONS` on the menu towards the left
-   Type in the search bar the following items and click `INSTALL`
    -   Remote -SSH
    -   C/C++
    -   C/C++ Extension packs

![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/08181185-6223-4e83-8dcc-3f4c9836022e)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/dfaf99cd-9188-4c05-bc30-63eb5fc56ea2)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/b1b211ef-a6f2-4511-8d1e-c864ae1a14e0)

## 2. [VcXsrv](https://sourceforge.net/projects/vcxsrv/)

<br>

# Step 2 : Change 'DISPLAY' Envionment Variable

## 1) Open Powershell

-   Press Windows key
-   Type in search bar `Powershell`
-   Type in the following in your Powershell instance and the Notepad application should launch
    ```bash
    notepad $PROFILE
    ```
-   Enter the following in your Notepad instance
-   Save the written contents
    ```bash
    # You can pick whatever numerical value for local host
    # Example --> $env:DISPLAY = "localhost:10.0
    $env:DISPLAY = "localhost:0.0"
    ```
-   Restart Powershell
    -   You MUST close and re-open PowerShell for the changes to take effect

## 2) Add DISPLAY Variable To Enviornment Variables

-   Press Windows key
-   Type in the search bar 'ENVIRONMENT VARIABLES' then press ENTER
    -   Click on `Edit the system environment variables`
    -   Once the `Enironment Variables` window pops up, click on `NEW`
        -   For `Variable name` enter `DISPLAY`
        -   For `Variable value` enter the local host value you set earlier in your NotePad instance
            -   Which in this instance is `localhost:10.0`

![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/ab8295f5-143d-4b42-876d-a039b7bf490f)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/511515c8-0c48-4d2f-96b8-5ae97307cfe7)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/0eb77108-6957-4a95-bd83-668758a093e0)

# Step 3 : Generate SSH Key

## 1) Create .ssh 'folder'

-   Open `Powershell` press `Windows key`
-   Type in the following

```bash
mkdir .ssh
```

## 2) Generate SSH Key

-   Enter the following

```bash
ssh-keygen -t rsa
```

-   When prompted :
    -   `Enter file in which to save the key (/home/local/.ssh/id_rsa)`
        -   Choose `.ssh`
    -   `Enter passphrase (empty for no passphrase): `
        -   Just press ENTER
    -   `Enter same passphrase agian:`
        -   Just press ENTER agian
-   You'll then be promped with your `key fingerprint` and your key's `randomart image` as shown in the screenshot below
    ![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/0293f80d-ad1e-4e73-b473-93715c6ef266)

-   Find the directory where your newly generated SSH keys are stored - In my case it's in the following directory
    `bash
 C:\Users\S123456789\.ssh
` - Use the `ls` command to list the contents of the `.ssh` directory - We're going to need the `public key` that has the `.pub` ending as shown in the screenshot below - You can use either VI or VIM to view the contents of the `public key`
    ![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/d00623bc-6fb1-465d-aa29-97f43a78b550)

Take public key

-

===================================================

Outline

Link to download

-   VSCode
    -   Remote -SSH
    -   C/C++
    -   C/C++ Extension pack
-   VcXsrv Windows X Server

Change DISPLAY enviornemnt path
Set SSH key
Get IP address from Raspberry PI

-   Set IP address in VS Code
