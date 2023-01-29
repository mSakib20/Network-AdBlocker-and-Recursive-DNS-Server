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


  




