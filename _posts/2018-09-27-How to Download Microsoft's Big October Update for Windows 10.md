---
layout: post
current: post
navigation: True
class: post-template
author: vishnu
title: How to Download Microsoft's Big October Update for Windows 10 Right Now
cover: /assets/img/blog/w10.jpg

---

*Microsoft plans to release Windows 10 version 1809 at the beginning of October, but thanks to a little trick, you can grab the update now and take it out for an early test drive.*

To get started, you’ll need the following:
* [Microsoft’s Media Creation Tool](https://software-download.microsoft.com/download/pr/MediaCreationTool1803.exe) (version 1803)—but don’t install it yet.
* [Microsoft Windows 10 Media Creation Tool Helper](https://github.com/CHEF-KOCH/Microsoft-Windows-10-Media-Creation-Tool-Helper)

## Microsoft’s big changes with this October update include:

* A dark theme for File Explorer.

![w10d](/assets/img/blog/w10d.jpg)

* A clipboard you can synchronize between devices.

![w10c](/assets/img/blog/w10c.jpg)

* An updated Game Bar, featuring an FPS counter, as well as other details about CPU, GPU, and system RAM use.

![w10g](/assets/img/blog/w10g.jpg)

* Texting from your PC (if you have a connected Android device).
* A brand-new tab bar, or “Sets,” for almost every app.
* A new (Mac-like) screenshot capturing tool, replacing the (faithful) Snipping tool.
* A new “power usage” tab in the Task Manager to see which apps are eating up your laptop’s battery.
* More built-in emoji. Thanks, Unicode 11.

# Here is how to get the update(1809):

## Preparations
You need to download two files to a PC and place them in the same folder.

* Download the [Microsoft’s Media Creation Tool](https://software-download.microsoft.com/download/pr/MediaCreationTool1803.exe) for Windows 10 version 1803. Note that you don't want to execute the tool right away as it only offers version 1803 and not 1809, the version that you are after.
* Download [Microsoft Windows 10 Media Creation Tool Helper](https://github.com/CHEF-KOCH/Microsoft-Windows-10-Media-Creation-Tool-Helper).
* Create a new folder on the system, e.g. c:\1809.
* Place the downloaded MediaCreationTool1803.exe file in the folder.
* Now copy "products.cab", downloaded from Microsoft Windows 10 Media Creation Tool Helper and place the file products.cab in the folder as well.
* Both files, MediaCreationTool1803.exe and products.cab should now be in the same folder.(The folder which you created in "C:")

## Download Windows 10 version 1809
Once you are done with the preparations, it is time to start the download of Windows 10 version 1809.

Open an elevated command prompt to get started.

* Press the Start button.
* Type cmd.exe.
* Hold down the Shift-key and the Ctrl-key on the keyboard.
* Select cmd.exe from the list of results with the mouse, keyboard or touch. This should launch an elevated command prompt after you accept the UAC prompt. Verify that this is the case by checking that the title of the command prompt window starts with Administrator:
*Change to the directory that you created previously, e.g. cd c:\1809.*(as shown below)

![cmd](/assets/img/blog/cmd.jpg)

* Run MediaCreationTool1803.exe /Selfhost


The command starts the Media Creation Tool and forces it to use the local product.cab file overriding the default.

From there, it is just a matter of following the prompts on screen. You have the option to upgrade the current PC or create installation media.

![w1](/assets/img/blog/w1.jpg)

* I prefer to select the "create installation media" option even if my intention is to update the local PC. Doing so gives me access to the installation media so that I can reuse it, use it to install Windows 10 anew on the device, or access some of the tools that it includes.

* Selecting "upgrade this PC now" on the other hand offers none of that. The tool downloads the Windows 10 installation files and saves them either as an ISO image on the system or creates a bootable USB Flash Drive out of it.

![w2](/assets/img/blog/w2.jpg)

* Use the bootable USB Flash Drive to start the upgrade to Windows 10 version 1809, burn the ISO or create a virtual machine image using it.

* Microsoft will release an updated Media Creation Tool eventually so that you may use it directly and don't have to rely on the workaround to create Windows 10 version 1809 installation media.

---
