# Setup Hyper-V Core as a Server Host


This post provides instruction on how to deploy a Windows Hyper-V Core host and suggested configuration during setup to provide remote access.

First we need to get our Microsoft Hyper-V Server 2019 ISO file.  Here is a direct link to Microsoft's ISO file: https://software-download.microsoft.com/download/pr/17763.737.190906-2324.rs5_release_svc_refresh_SERVERHYPERCORE_OEM_x64FRE_en-us_1.iso

*if you are interested in earlier or future versions you can find other download links here: https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019.*

In order to install Windows Hyper-V Core using the ISO file you will need a utility that can create a bootable drive to facilitate the installation.  Rufus https://rufus.ie/
is a commonly used open source tool that can assist with this process (another options is Etcher - https://www.balena.io/etcher/).

Run the program of your choosing (Rufus is displayed below) and for each field:

- **Boot selection =** your ISO file<br>
- **Device =** the external drive you want to make a bootable drive (this will erase all data)<br>
- **Image option =** leave as default<br>
- **Partition scheme =** GPT if your device supports UEFI, MBR if not<br>
- **Target system =** leave as default<br>
- **Volume label =** provides your drive with a friendly name<br>

*All other settings can be left with defaults.*

![alt text](https://github.com/jakden/Hyper-V_Core_Setup/blob/main/images/P0002_IMG01.png)

Click START to begin the image creation process.  Once this process has completed the word READY will re-appear and the status bar will be green end to end.  Properly eject this drive from your PC by right clicking the drive in File Explorer and clicking Eject.  This will help avoid any data corruption if the drive was still in use.

Insert the drive into the machine you plan to transform into a Hyper-V Core host and boot the device.  You may need to access your device's BIOS settings and alter the boot options in order to have it boot to this drive.  Once you have booted to your flash drive you will be provided with the typical Windows installation prompts.  Select the drive you would like to install this OS on and start the installation process by clicking on Next:

![alt text](https://github.com/jakden/Hyper-V_Core_Setup/blob/main/images/P0002_IMG02.png)

![alt text](https://github.com/jakden/Hyper-V_Core_Setup/blob/main/images/P0002_IMG03.png)

After a few reboots the installation will complete and you will be presented with the prompt below where you will be required to create and confirm the local administrative password for the Administrator account.

![alt text](https://github.com/jakden/Hyper-V_Core_Setup/blob/main/images/P0002_IMG04.png)

After you are logged into the system you will be presented with blue command prompt called sconfig.  This prompt will help with configuring some basic settings.  Powershell commands can be used for some more advanced options like noc binding for your network ports but we will stick to the prompt for this tutorial.  If for some reason you loose your prompts you can utilize the CTRL+ALT++END key combination to bring up the task manager which allows you to run another task - cmd.exe and once in the prompt you can type the command below to enter the blue configuration prompt again.
```bat
sconfig
```
<br>
![alt text](https://github.com/jakden/Hyper-V_Core_Setup/blob/main/images/P0002_IMG05.png)

**Some of the suggested settings to quickly get connected remotely and continue the reset of your configuration from you PC:** <br>
- Set your static IP (#8) <br>
- Turn on Remote Desktop (#7) <br>
- Change the device name (#2) <br>
- Allow the device to be pinged (#4 and then #3) <br>

Now you have a working Hyper-V Core that can host your VMs.  For production environments Windows Standard licensing provides you with rights for one Core host and two additional VMs that meet the core count requirements.
