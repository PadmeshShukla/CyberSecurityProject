# CyberSecurityProject
Steps to hack into the system after loading the machine onto the VirtualBox and launching Kali Linux and the Machine side by side.

Step 1: Scan all the machines which are on the network using the ip a command

This will display an lo: machine and eth0: machine . Note down the IP address (mentioned in the inet section of the eth0 machine. Include the numbers after the slash (/) as well ) of the eth0 machine somewhere. For now Let's call it <IP>.

Step 2: Use the nmap -sn -n <IP> 

This will display all the hosts currently up on the network. Since our machine is a VM , we would see the mac address of the machine and next to it we would see the words 'Oracle VirtualBox virtual NIC' (I am using VirtualBox here. You might see something else if you are using something like VMWare). This is our target machine.

Step 3: We are now going to transfer the files using the 'ftp' command. FTP - File Transfer Protocol.

use the command : ftp <IP>

We will be asked for a name.(Name ( <IP>:<kali username>):)
Enter anonymous here. It will ask us to specify a password. Just press the enter key and it will say login successful. 

Now run the ls -ltr command to see any files stored on the machine. There is a note file on my machine. 

Now type 'bin' to switch to binary mode. Then type 'get note' to get the note onto your kali machine.

In order to read the note , type 'cat note'.

In my machine , there was a machine saying : "Elly , make sure you update the payload information. Leave it on your FTP account once you are done , John. 

This implies that there are two possibilities for a user named "Elly" or "John". 



Step 4 : Now we are going to use hydra to find out the password for the users given . Try for Elly first. This might require a bit of trial and error.

First of all , download a github file called darkc0de.txt on your kali machine which contains a lot of passwords which we will use to try. We will call the path of this file be <pathdark>.

LINK : https://gitlab.com/kalilinux/packages/seclists/-/blob/kali/master/Passwords/darkc0de.txt
We will use this file.

Now run this command , hydra -l elly -P <pathdark> ftp ://<IP> -e nsr
We will get the message (login:elly password : ylle)


Step 5: we will now check ssh support for elly

run the command 'ssh elly@<IP>
It will ask us if we want to continue connecting.Enter yes there. It will ask us to enter the password.Enter 'ylle'.
It will close the connection . This implies that ssh won't work on this.


Step 6: run the ftp command again (ftp <IP>)
This time enter the name as 'elly' and password as 'ylle'
It will successfully login.

Run the ls -l to find out the files on elly. There should be a passwd file as is there on every ubuntu machine.
Transfer the passwd file onto your kali using the 'bin' command and 'get passwd'

Exit the ftp command .Open the file using cat passwd. It will give you a list of users.


Step 6: We have to use the ssh command on all the users one by one . The correct user is "SHayslett".
run the command:
hydra -l SHayslett -P <pathdark> -e nsr <IP> ssh
It will return the password of SHayslett which is "SHayslett".
Run the command ssh SHayslett@<IP>


YAY!! You have successfully gotten access to this system.
