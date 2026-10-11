# Project 02: System Info Reporter - Started 10/8/26

The goal of my second project is to write a script in Python that can tell me the general information about a system, including the
hostname, ip address, physical hardware specs, and the date and time of the report. 

## Checking to ensure Python is installed

Typically, Ubuntu Server comes with Python already installed. Regardless, to ensure it was installed, and to make sure it was up to
date, I ran the command 'python3 --version'. This command, if Python is installed, will report back the version of Python that is
installed. For me, the response I received was 3.14.4.

This means that Python is already installed. To make sure Python was fully up to date, I ran the commands 'sudo apt update' and 'sudo
apt upgrade' so that I could install the latest version of all of the packages installed on my first machine.

## Creating the script

Before creating the script, I made a new folder inside my MAIN folder called PROJECTS. Inside my new folder, I ran the command 'nano
sysinfo.py'. With this command, I created a blank '.py' file named 'sysinfo'. This is going to be the file I use for my script.

After creating the file, I ran the command 'sudo apt install python3-psutil' to install psutil, which is a module that will help me
retrieve more information about the system for my info reporter. This is only one of 5 modules I am importing, however, as I will also
be taking advantage of the modules socket, datetime, platform, and shutil.

While I was trying to install psutil, my virtual machine froze. I could not interact with it whatsoever. I did not want to shut off the
machine, because I was worried that shutting it down mid installation could damage the integrity of my files. I fixed this problem by
making my virtual machine full-screen, which fixed the frozen screen and gave me a response that my CPU had been idling for 206 seconds.

Following this error, I tried to install psutil again and the installation process went smoothly. I returned to my 'sysinfo.py' file,
where I imported all 5 of the modules I want to use for this script. Now, the real work can begin.

## Using the socket module
