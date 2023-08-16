# Remotely Debug C++ Programs on RPI Using VS Code

<br>

# Step 1 : Download and install the following items

## 1) [Visual Studio Code](https://code.visualstudio.com/)

-   Once you've opened VS Code
-   Click `EXTENSIONS` on the menu towards the left
-   Type in the search bar the following items and click `INSTALL`
    -   Remote -SSH
    -   C/C++
    -   C/C++ Extension packs

![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/08181185-6223-4e83-8dcc-3f4c9836022e)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/dfaf99cd-9188-4c05-bc30-63eb5fc56ea2)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/b1b211ef-a6f2-4511-8d1e-c864ae1a14e0)

## 2) [VcXsrv](https://sourceforge.net/projects/vcxsrv/)

<br>

# Step 2 : Change The `DISPLAY` Envionment Variable

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
    $env:DISPLAY = "localhost:10.0"
    ```
-   Restart Powershell
    -   You MUST close and re-open PowerShell for the changes to take effect
    -   To double check if the `DISPLAY` variable was saved, copy/paste the following
    ```bash
    $env:DISPLAY
    ```

## 2) Add DISPLAY Variable To Enviornment Variables

-   Press Windows key
-   Type in the search bar 'ENVIRONMENT VARIABLES' then press ENTER
    -   Click on `Edit the system environment variables`
    -   Once the `Enironment Variables` window pops up, click on `new`
        -   For `Variable name` enter `DISPLAY`
        -   For `Variable value` enter the local host value you set earlier in your NotePad instance
            -   Which in this instance is `localhost:10.0`

![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/ab8295f5-143d-4b42-876d-a039b7bf490f)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/511515c8-0c48-4d2f-96b8-5ae97307cfe7)
![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/0eb77108-6957-4a95-bd83-668758a093e0)

<br>

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

```bash
 C:\Users\S123456789\.ssh
```

-   Use the `ls` command to list the contents of the `.ssh` directory
-   We're going to need the `public key` that has the `.pub` ending as shown in the screenshot below
-   You can use either `VI` or `VIM` to view the contents of your `public key`
    ![image](https://github.com/Digital1O1/4_DOF_Robotic_Arm/assets/39348633/d00623bc-6fb1-465d-aa29-97f43a78b550)

## 3) Save SSH Key on Raspberry PI

-   Type in the following commands in your Raspberry PI terminal

```bash
cd ~
sudo nano ~/.ssh/authorized_keys
```

-   If the `.ssh` folder DOESN'T exist, use the following commands

```bash
cd ~
mkdir authorized_keys
sudo nano ~/.ssh/authorized_keys
```

-   Then :
    -   Paste your `.pub` SSH key into the `authorized_keys` file
    -   Press `Control + X` --> `Y` --> `ENTER` to save and exit out of the file

## 4) Obtain your Raspberry PI IP address

-   Open a terminal on the Raspberry PI
-   Type in the following and take note of the value that's displayed under the `wlan0` section
    ```bash
    ifconfig
    ```
    ![image](https://github.com/Digital1O1/Remotely-Debug-C-Programs-on-RPI-Using-VS-Code/assets/39348633/5094e115-1d6a-4775-b6e3-224ddad1cc65)

## 5) Enable X11 Port Fowarding

-   On your host machine
    -   Open a Powershell instance
    -   Use the :
        -   `cd` command to return back to the `.ssh` folder
        -   `-ls -a` command to list everything stored in the `.ssh` folder
            -   You should see a `config` file
            -   Use either `vim` or `nano` to edit the `config` file and enter the following WITHOUT THE BRACKETS
            ```bash
                Host [YOUR RASPBERRY PI IP ADDRESS]
                    HostName [YOUR RASPBERRY PI IP ADDRESS]
                    User [YOUR RASPBERRY PI USER NAME]
                    ForwardAgent yes
                    ForwardX11 yes
                    ForwardX11Trusted yes
            ```

<br>

# Step 4 : Configuring VS Code for remote development

-   Open VS Code - Right click on `Remote-SSH` - Click on `Extension Settings` - Ensure the following boxes are checked: - Remote.SSH: Enable Agent Forwarding - Remote.SSH: Enable Dynamic Forwarding - Remote.SSH: Enable X11 Forwarding
    ![image](https://github.com/Digital1O1/Remotely-Debug-C-Programs-on-RPI-Using-VS-Code/assets/39348633/28e62abd-0267-4eba-b8f2-7ac6be5c3d1e)

<br>

-   Establish connection to host
    -   Press `Control + Shift + P`
    -   Type in the following : `connect to host` and choose either option
    -   Click on `Add New SSH Host`
    -   To verify that you're connected to the Raspberry PI you can :
        -   Check the lower left corner and you should see the Raspberry PI IP address
            ![image](https://github.com/Digital1O1/Remotely-Debug-C-Programs-on-RPI-Using-VS-Code/assets/39348633/ab9e3ef0-2a4c-4739-a223-259bc104bca7)
            ![image](https://github.com/Digital1O1/Remotely-Debug-C-Programs-on-RPI-Using-VS-Code/assets/39348633/609af753-9a70-40cb-adf2-df4efb71ff68)
        -   Both a bash terminal and the IP address should show up as indicated in the screenshot below
            ![image](https://github.com/Digital1O1/Remotely-Debug-C-Programs-on-RPI-Using-VS-Code/assets/39348633/dbc7e89a-8005-4e03-9830-d74ac7eda989)

-   To open a project that's saved on the Raspberry PI
    -   Click the first icon on the left side menu
    -   Click on `Open Folder`
        -   Then you can navagate to whatever folder your project is stored in
            ![image](https://github.com/Digital1O1/Remotely-Debug-C-Programs-on-RPI-Using-VS-Code/assets/39348633/39dee248-9492-41bc-aa46-68ed690abb24)
