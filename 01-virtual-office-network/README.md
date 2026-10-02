# 01 Virtual Office Network - 10/1/26

The goal of my first project is to build a small, working "office network" out of virtual machines, which I can use in my future projects.
I aim to show that I am capable of connecting, testing, and troubleshooting these virtual machines.

## Installing VirtualBox & Ubuntu Server

I installed VirtualBox Version 7.2.20 from [virtualbox.org](https://www.virtualbox.org), and encountered no issues.

I downloaded the .iso file for Ubuntu 26.04.01 LTS from [ubuntu.com](https://ubuntu.com/download/server#manual-install-tab) and installed it in VirtualBox.

The Ubuntu VM has 2048 MB of Base Memory, 2 Processors, and a 25.0 GB disk size.

I encountered a small issue on my first installation attempt, where the installation process hung up and would not continue processing.
A quick restart fixed this, and the installation proceeded smoothly on the second attempt.

## Setting up Secondary VM

In order to set up a basic virtual office network for my future break-fix research and experiments, I need to be able to run multiple virtual machines simultaneously.

To accomplish this, I cloned the first virtual machine that I made in order to avoid having to wait for the OS to install a second time. 

After cloning was complete, I logged into the second virtual machine and gave the clone a new identity, such as a new hostname and machine id, to ensure that the two virtual machines would have no issues communicating with one another in the long run.

I ran a series of 5 commands in order to make the changes necessary:
- sudo hostnamectl set-hostname ubuntu-server-02 (This command changed the hostname of the second virtual machine.)
- sudo truncate -s 0 /etc/machine-id (This command emptied the file containing the machine id, allowing for a refresh.)
- sudo rm -f /var/lib/dbus/machine-id (This command deletes the second copy of the machine id, allowing for a refresh.)
- sudo ln -s /etc/machine-id /var/lib/dbus/machine-id (This command makes the second id copy a shortcut to the first.)
- sudo reboot (Self explanatory; reboots the machine.)

The final command, which signals the machine to reboot, will allow the operating system to refresh the second virtual machine's machine id, which will allow it to have its own unique id different than that of the first virtual machine. It does this because it notices that the machine id files are empty following the commands above. This reboot will also allow the hostname change to take effect.

One quick command, hostnamectl, allows me to see if I am successful.

<img width="407" height="273" alt="Screenshot 2026-10-02 151220" src="https://github.com/user-attachments/assets/ab06405b-1c57-4cee-ad92-b33782477305" />

Success! The second virtual machine is now completely unique, and I am ready to move on to setting up the virtual office network.
