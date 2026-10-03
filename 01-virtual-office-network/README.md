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

One quick command, 'hostnamectl', allows me to see if I am successful.

<img width="407" height="273" alt="Screenshot 2026-10-02 151220" src="https://github.com/user-attachments/assets/ab06405b-1c57-4cee-ad92-b33782477305" />

Success! The second virtual machine is now completely unique, and I am ready to move on to setting up the virtual office network.

## Creating the Virtual Office Network

In order to turn my two virtual machines into an actual testing environment, my virtual machines need to be connected to their own network.

Since I am using Oracle VirtualBox for my research and testing, I can easily create a virtual network by using the sidebar to navigate to the Network tab.

Under NAT Networks, I created a new virtual network named OfficeNet.
I then gave this network an IPv4 Prefix, and enabled DHCP for automatic IP assignments.

I did not enable IPv6.

I clicked apply, and my virtual network was complete. 

<img width="1046" height="129" alt="Screenshot 2026-10-03 184631" src="https://github.com/user-attachments/assets/b39a1131-ed44-4da5-802a-6052507936c3" />

## Connecting VMs to OfficeNet & testing their connection

To connect my virtual machines to my virtual network, OfficeNet, I navigated back to the Machines tab and right clicked on my primary VM to access its Settings menu.

From here, I opened the Network settings for the machine, and enabled the first Network Adapter.
I attached the adapter to a NAT Network, and selected OfficeNet as the network.

After clicking ok, the connection was made and I repeated these steps for my secondary virtual machine.

Once each machine was connected to my virtual network, I started both of them and ran several commands to test if my
network was correctly configured.

First, I made sure to run the 'ip a' command on both machines to get their IPv4 addresses, and then performed a connection test using the 'ping' command.

A 'ping' command from primary VM to secondary VM:
<img width="526" height="279" alt="Screenshot 2026-10-02 152348" src="https://github.com/user-attachments/assets/483cefa4-4eb3-4ed0-91a8-fb53e83f872e" />

A 'ping' command from secondary VM to primary VM:
<img width="547" height="381" alt="Screenshot 2026-10-02 152330" src="https://github.com/user-attachments/assets/54b303bb-df4d-4ef3-bfc1-6ca33e5e1b37" />

A 'ping' command from primary VM to 8.8.8.8:
<img width="523" height="182" alt="Screenshot 2026-10-02 152440" src="https://github.com/user-attachments/assets/77894003-7be0-49db-acf7-70a6a0c1933a" />

With my first two pings, I ensured that each machine could see each other and communicate with each other over OfficeNet.
With my final ping, I made sure that the two machines could actually connect to the internet.
The IP address '8.8.8.8' belongs to Google's public DNS server, and is almost always online. Great for testing.

Once I confirmed that both machines could see and communicate with one another as well as the internet itself,
my introductory Virtual Office Network project was complete.
