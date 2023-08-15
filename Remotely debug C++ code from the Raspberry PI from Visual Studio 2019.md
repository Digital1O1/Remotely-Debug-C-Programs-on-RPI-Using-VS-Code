# Remotely debugg C++ code from the Raspberry PI from Visual Studio 2019

<br>

# Step 1 : Install and Enable Windows Subsystem for Linux (WSL)

Open powershell as admin

Run this command :

```shell script
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

Install Ubuntu using this command

```shell
wsl --install
```

Restart machine/computer

Open Powershell as **<u>admin</u>** after restart

Enable WSL by typing : Ubuntu

Enter a username/password

-   Username **MUST** be in lower case or you'll get an error

<br>

# Step 2 : Update WSL to WSL 2

```shell
wsl --set-default-version 2
```

<br>

# Step 3 : Install Linux development distribution for Visual Studio

Press the Windows key + R

-   Search for the 'Visual Studio Installer'
-   Click 'Modify'
    ![image](https://github.com/Digital1O1/WSL_REMOTE_Blink1/assets/39348633/7e2e1491-fec3-47a6-955a-95e320617acb)

-   Check the "Linux development with C++" - Then "Install while downloading"
    ![image](https://github.com/Digital1O1/WSL_REMOTE_Blink1/assets/39348633/225afa49-1c62-4918-9cdd-3caea7d41d6f)

## Configure VS to use WSL

Open Visual Studio.

-   Go to "Tools" > "Options."
    -   Under 'Cross Platform'
    -   Select 'Connection manager'
    -   Click "Add" to add a new connection.
        -   Hostname : IP address to the Raspberry PI
        -   Port : 22
        -   Username : Your WSL username
        -   Authentication type : Password
        -   Password : Your WSL password

## Creating a C++ project for the Raspberry PI in Visual Studio

While in Visual Studio

-   Go to File --> New --> Project
-   Make sure you chose from the drop down menus
    -   C++
    -   Linux
    -   Console
    -   Raspberry Pi Project

![image](https://github.com/Digital1O1/WSL_REMOTE_Blink1/assets/39348633/9b54e210-ceeb-4bde-93e0-4f84d0fe0b41)

From there

-   Right click on your current project
-   Select 'PROPERTIES'

![image](https://github.com/Digital1O1/WSL_REMOTE_Blink1/assets/39348633/7afedbf7-9396-4cbe-8040-2cd0c5941c41)

<br>

# IMPORTANT

-   It's worth noting that
    -   The 'build' process for the C++ code is still being done on the Raspberry PI 4
    -   ~~I'm also heavily assuming that the files used on the 'Visual Studio' side MUST be installed on the Raspberry PI 4 prior to running the code. I'll later verify if that's the case down the road (8/2/23)~~
    -   As of 8/4, I've verified that **<u>ALL</u>** header files from the Raspberry PI are copied onto your machine where you're running Visual Studio from

<br>

##

![image](https://github.com/Digital1O1/WSL_REMOTE_Blink1/assets/39348633/8d9f04f4-8b1d-40d6-99ae-0d54ffabe86b)

## To run debugger

To go Debug --> Start debugger

![image](https://github.com/Digital1O1/WSL_REMOTE_Blink1/assets/39348633/4fa46077-c47f-48b1-b347-719a3e2b800f)

<br>

# References used

https://www.howtogeek.com/426749/how-to-access-your-linux-wsl-files-in-windows-10/#:~:text=Key%20Takeaways,open%20the%20desired%20distribution%20folder.

https://www.youtube.com/watch?v=QAliMv5_DWI&t=1s&ab_channel=Dave%27sGarage
