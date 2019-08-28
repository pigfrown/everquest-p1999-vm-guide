# everquest-p1999-vm-guide

A guide for running Everquest Titanium (EQEmu/Project1999) in VirtualBox with a Windows XP guest.

## Motivations

1) For Running on linux/whatever without using Wine.

2) Portable EQ installation that can be ran on linux/windows/osx.

3) Classic windows XP experience (if you don't want XP you can just use Windows 10 instead, but performance is worse for me).
 
4) Protect the privacy of your host machine from dsetup.dll.

## Requirements

Download Windows XP ISO from wherever you got Everquest Titanium.

Download VirtualBox ( https://www.virtualbox.org/wiki/Downloads )

Install VirtualBox.

## Create new VirtualBox

Open VirtualBox.

Click "Machine"->"New".

Name as you like, Version "Windows XP (32bit)".., click "Next".

Memory Size.. I selected roughly 2GB (2000MB).. click "Next".

Hard Disk... Select "Create a virtual hard disk now". click "Next".

Hard Disk file type... Select "VDI (VirtualBox Disk Image)". click "Next".

Storage on physical hard disk... Select dynamically allocated (saves space). click "Next".

File Location and size... Defaults here should be sufficient. You can change the location the virtualbox is saved by clicking the folder icon. You can select the hard disk size. Leave it at 10GB default. Click "Create".

## Configuring the new VirtualBox

The VirtualBox now needs configuring to use 3D acceleration and to boot from the Windows XP ISO.

Select your new VirtualBox in the left hand window.

Click Machine->Settings.

### In the settings window:


Click "Display" in left pane. In the "Graphics Controller" dropdown, select "VBoxVGA" (NOT the default "VBoxSVGA", XP does not work with this controller. If you are using Windows 10 either should work). Increase "Video Memory" slider to maximum. Click the "Enable 3D Acceleration" and "Enable 2D Acceleration" check boxes.


Click "Storage" in left pane. In the middle pane click the CD icon with "Empty" label. In the right hand pane click the CD icon drop down (next to "Optical Drive: IDE Secondary Master). Click "Choose Virtual Optical Disk File". In the new window navigate to the Windows XP iso you acquired earlier and select it.

Click Ok to save settings.

## Installing Windows XP in the VirtualBox

Select your new VirtualBox in the left hand window. Click the large arrow labeled "Start".

The VirtualBox should boot up and load the Windows XP installation. Click through prompts/requests for information.

Oncethe installation is complete you should be looking at a fresh Windows XP installation.

## Installing VirtualBox guest additions in Windows XP

This enables many nice features like resizing, shared folders, and 3D acceleration. It needs to be done in safe mode in XP. 

Shutdown the windows XP VirtualBox if it is on.

Remove the installation CD from the VirtualBox by right clicking it in Settings-Storage-Storage Devices and clicking "remove".

Start the VirtualBox... as it boots spam F8 and select "Safe Mode".


When windows has booted, select "Devices->Insert Guest Additions CD" (this is on the VirtualBox window containing the running Windows VM, not in windows itself.)

The CD will autorun. Click through it until you reach the "Choose Components" page. Make sure you check "Direct3D Support (Experimental)" before installing.

Windows will now reboot. You should now be able to resize the VirtualBox properly.


## Install Everquest Titanium

When the VirtualBox is running, click "Devices->Optical Drives->Choose Disk Image". Browse to and select the Everquest Titanium CD 1 ISO and click "Open".

Everquest installation should now start. Repeat the above procedure for every CD requested until installation complete.


If you want to copy across any files from existing installations (the P99 zip, character UI files etc) you can do this by adding a shared folder. Otherwise, you can skip this step.

### Adding a shared folder

A shared folder is used to copy all required files (DUXA Installer, P99 zip, any UI files/extras you want) to the VirtualBox (XP Internet Explorer is unusable on modern sites and insecure).

When the VirtualBox is running, click "Devices->Shared Folders->Shared Folder Settings"

Click the "folder with +" icon. Browse to the directory you want to share (either your Everquest directory, or the directory containing the Everquest ISOs). Select AutoMount. Click OK.

Back in the VirtualBox, In "My Computer", you should see the shared folder mounted as a network drive.

You can now copy DUXA Installer, P99 zip, and any UI files into the shared location on the host and access them in the VirtualBox.

## Tweaks to get EQ working correctly.


- Use DUXAS All in one Installer (https://www.project1999.com/forums/showthread.php?t=28335) with option 1. Make sure you select "Windowed Mode" and your resolution of choice. (see notes below about fullscreen).

- Extract the current "Project1999 Files" zip into the Everquest folder (download from https://www.project1999.com/forums/showthread.php?t=2651)

- Open eqclient.ini in your Everquest folder and set the all Vertex and Pixel shaders to FALSE.

e.g. change:

```
VertexShaders=TRUE
20PixelShaders=TRUE
14PixelShaders=TRUE
1xPixelShaders=TRUE
```

to 

```
VertexShaders=FALSE
20PixelShaders=FALSE
14PixelShaders=FALSE
1xPixelShaders=FALSE
```

This is neccesary for character models to display correctly and general stability.

## Launch EQ

Use the "Everquest (p99) - bypass EQemu" desktop shortcut created by DUXA installer, or the "Launch Titanium" file in the everquest folder. 


## Notes/Issues

Fullscreen mode will crash if the VirtualBox has a non-standard resolution, e.g. because the window has been resized by the host. To work around this manually set the resolution in Windows XP (and don't resize the VirtualBox?).

Everytime you use DUXA to change resolutions you need to disable Shaders in your eqclient.ini (see above).

Mouse sensitivity is way too high when using mouse look. You can disable mouse integration to fix this, but then you can't see the cursor. Seems this is a known issue with VirtualBox (https://www.virtualbox.org/ticket/7945). Still looking for workarounds for this, but no luck so far :(






