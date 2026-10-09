# Side Project 01: New Login Messages - Started 10/3/26

While working on my first project, I came up with the idea of making my virtual machines display a custom message at login.
I decided to move forward with this idea as a side project, because I did not like the login message that came packaged with
the operating system.

My goal is simple: replace the original login message with my own custom text.

## Writing my custom message on VM1

I wanted to make sure that when I replaced the login message, I had a backup of both my custom message as well as the original.
Because of this, I decided that I would make a new directory on VM1 called MAIN, that I can use to store all of my files separate.
After making the folder, I used the command 'cd MAIN' in order to move to it. Then, I used the 'nano' command in order to make a new
text file inside the folder. 

Since these projects of mine are not only to strengthen my resume, but also for my own enjoyment, I decided to take inspiration for
my login message from one of the games I have been enjoying recently. Once I finished writing my message, I saved it as
'newloginmessage.txt'.  

## Replacing VM1's login message

Once I had my new login message written, it was time for me to turn my attention towards the original. The login message for Ubuntu
Server 26.04 is saved in /etc/issue. I needed to make sure that I saved a backup of the original file, just in case something went
wrong during my experimentation.

I accomplished this by running the command 'sudo cp /etc/issue /etc/issue.bak'. This command copied the content of the original login
message and pasted it into a new file understandably named 'issue.bak'.

From there, I ran the command 'sudo cp ~/MAIN/newloginmessage.txt /etc/issue'. This is the same command that I used to make a backup
of the original login message. However, this time I used the command to copy the contents of my new login message and paste them
into the original message's file. This is also useful for preserving my new message as well, because the file remains unaffected by
the command.

## Copying my message to VM2

## Replacing VM2's login message

## Replacing OpenSSH login messages
