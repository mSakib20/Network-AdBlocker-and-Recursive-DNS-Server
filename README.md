# Pi-hole-Unbound
Pi-hole setup with recursive DNS


### Install PROXMOX 

Download Link: https://www.proxmox.com/en/proxmox-ve/get-started

<img src="/piHole Setup/1.JPG">


### Create a Virtual Machine insde PROXMOX

I am using ubuntu server 22.04 for this project. 

<img src="/piHole Setup/2.JPG">

<img src="/piHole Setup/3.JPG">

<img src="/piHole Setup/4.JPG">

<img src="/piHole Setup/5.JPG">


### Setting up ubuntu server inside Virtual Machine


<img src="/piHole Setup/6.1.JPG">

<img src="/piHole Setup/6.2.JPG">

<img src="/piHole Setup/6.3.JPG">

<img src="/piHole Setup/6.4.JPG">

NOTE: IF AN ERROR OCCURS DURING REBOOT, PLEASE FOLLOW THE INSTRUCTIONS BELOW

<img src="/piHole Setup/6.5 error.JPG">

<img src="/piHole Setup/6.6.JPG">

To begin, select the virtual machine in PROXMOX. Next, navigate to the HARDWARE tab and remove the CD/DVD drive, as illustrated in the accompanying image.

NOTE: If the setup gets stuck, restart the virtual machine.

<img src="/piHole Setup/6.7 (do a restart if setup get stuck).JPG">

Now, log in with user ID and PASSWORD.

<img src="/piHole Setup/6.10.JPG">

Make a note of the IP address, as we will use it later to access the server using SSH.


### Install and configure TERMIUS 

DOWNLOAD LINK: https://termi.us/win

After downloading type in the IP address for you your ubuntu server as shown in the picture below

<img src="/termius.JPG">

### Install Pi Hole in Ubuntu server through Termius

After creating a secure connection, install lighttpd server
      
      command: sudo apt install lighttpd
      
<img src="/piHole Setup/7.1.JPG">

Then, install Pi-hole
      
      command: sudo curl -sSL https://install.pi-hole.net | bash

<img src="/piHole Setup/7.2.JPG">

SOURCE: https://www.virtualizationhowto.com/2021/12/install-pi-hole-in-ubuntu-21-04/ 

<img src="/piHole Setup/7.3.JPG">
<img src="/piHole Setup/7.4.JPG">
<img src="/piHole Setup/7.5.JPG">
<img src="/piHole Setup/7.6.JPG">
<img src="/piHole Setup/7.7.JPG">

NOTE: REMEBER THIS ADDRESS AND PASSWORD 

If you forget or want to change the password then use the following command in TERMIUS to change your password shown in the picture below.

      command: pihole -a -p

<img src="/piHole Setup/7.8.JPG">

Next, open a web browser and enter the address of your Pi-hole. For example, if your IP address is 192.168.0.9, you would enter "http://192.168.0.9/admin" into the address bar. Log in with your password.

<img src="/piHole Setup/7.9.JPG">

NOTE: Pi Hole to work properly we have to override the DNS drom our Router. 
      I am using secondary DNS address 9.9.9.9 as a backup. Once I can confirm that my setup is up and running I can comeback and remove the secondary DNS
      address. 
      
<img src="/piHole Setup/7.10.JPG">
