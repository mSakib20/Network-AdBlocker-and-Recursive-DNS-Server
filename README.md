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

##### NOTE: IF AN ERROR OCCURS DURING REBOOT, PLEASE FOLLOW THE INSTRUCTIONS BELOW

<img src="/piHole Setup/6.5 error.JPG">

<img src="/piHole Setup/6.6.JPG">

To begin, select the virtual machine in PROXMOX. Next, navigate to the HARDWARE tab and remove the CD/DVD drive, as illustrated in the accompanying image.

##### NOTE: If the setup gets stuck, restart the virtual machine.

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

##### NOTE: REMEBER THIS ADDRESS AND PASSWORD 

If you forget or want to change the password then use the following command in TERMIUS to change your password shown in the picture below.

      command: pihole -a -p

<img src="/piHole Setup/7.8.JPG">

Next, open a web browser and enter the address of your Pi-hole. For example, if your IP address is 192.168.0.9, you would enter "http://192.168.0.9/admin" into the address bar. Log in with your password.

<img src="/piHole Setup/7.9.JPG">

##### NOTE: Pi Hole to work properly we have to override the DNS from our Router. 
      I am using secondary DNS address 9.9.9.9 as a backup. Once I can confirm that my setup is up and running I can comeback and remove the secondary DNS
      address. 
      
<img src="/piHole Setup/7.10.JPG">

<img src="/piHole Setup/9.JPG">

### OPTIONAL Recurssive DNS / Unbound Pi Hole

I will use TERMIUS to establish an SSH connection to my Pi-Hole in order to install Recursive DNS

To create an SSH connection using TERMIUS, simply enter your Pi-hole IP address in the designated field.

<img src="/piHole Setup/7.1.JPG">

INSTALL Unbound: 
      
      command: sudo apt install unbound   

<img src="/piHole Setup/8.1.JPG">

Configure Unbound: 
      
      command: sudo nano /etc/unbound/unbound.conf.d/pi-hole.conf
      
      then copy paste the following lines and save the file.
      
      ===============================================================================================================================================
      
      server:
          # If no logfile is specified, syslog is used
          # logfile: "/var/log/unbound/unbound.log"
          verbosity: 0

          interface: 127.0.0.1
          port: 5335
          do-ip4: yes
          do-udp: yes
          do-tcp: yes

          # May be set to yes if you have IPv6 connectivity
          do-ip6: no

          # You want to leave this to no unless you have *native* IPv6. With 6to4 and
          # Terredo tunnels your web browser should favor IPv4 for the same reasons
          prefer-ip6: no

          # Use this only when you downloaded the list of primary root servers!
          # If you use the default dns-root-data package, unbound will find it automatically
          #root-hints: "/var/lib/unbound/root.hints"

          # Trust glue only if it is within the server's authority
          harden-glue: yes

          # Require DNSSEC data for trust-anchored zones, if such data is absent, the zone becomes BOGUS
          harden-dnssec-stripped: yes

          # Don't use Capitalization randomization as it known to cause DNSSEC issues sometimes
          # see https://discourse.pi-hole.net/t/unbound-stubby-or-dnscrypt-proxy/9378 for further details
          use-caps-for-id: no

          # Reduce EDNS reassembly buffer size.
          # IP fragmentation is unreliable on the Internet today, and can cause
          # transmission failures when large DNS messages are sent via UDP. Even
          # when fragmentation does work, it may not be secure; it is theoretically
          # possible to spoof parts of a fragmented DNS message, without easy
          # detection at the receiving end. Recently, there was an excellent study
          # >>> Defragmenting DNS - Determining the optimal maximum UDP response size for DNS <<<
          # by Axel Koolhaas, and Tjeerd Slokker (https://indico.dns-oarc.net/event/36/contributions/776/)
          # in collaboration with NLnet Labs explored DNS using real world data from the
          # the RIPE Atlas probes and the researchers suggested different values for
          # IPv4 and IPv6 and in different scenarios. They advise that servers should
          # be configured to limit DNS messages sent over UDP to a size that will not
          # trigger fragmentation on typical network links. DNS servers can switch
          # from UDP to TCP when a DNS response is too big to fit in this limited
          # buffer size. This value has also been suggested in DNS Flag Day 2020.
          edns-buffer-size: 1232

          # Perform prefetching of close to expired message cache entries
          # This only applies to domains that have been frequently queried
          prefetch: yes

          # One thread should be sufficient, can be increased on beefy machines. In reality for most users running on small networks or on a single machine,           it should be unnecessary to seek performance enhancement by increasing num-threads above 1.
          num-threads: 1

          # Ensure kernel buffer is large enough to not lose messages in traffic spikes
          so-rcvbuf: 1m

          # Ensure privacy of local IP ranges
          private-address: 192.168.0.0/16
          private-address: 169.254.0.0/16
          private-address: 172.16.0.0/12
          private-address: 10.0.0.0/8
          private-address: fd00::/8
          private-address: fe80::/10
          
 Source: https://docs.pi-hole.net/guides/dns/unbound/
 
 Now we have to change Pi Hole settings. 
 
 First, navigate to the settings within Pi-hole. Then select the DNS option and uncheck the box for IPv4, as shown in the picture below.
 
 <img src="/piHole Setup/8.5.JPG">
 
 Then, scroll down to Upstream DNS Server select Custom 1 (IPv4) and then type in following address:
      
      127.0.0.1#5335
 
 <img src="/piHole Setup/8.6.JPG">
 
 #### With that, the setup of a Pi-hole with a Recursive DNS Server is complete. 
 
 <img src="/piHole Setup/9.JPG">
 
  
 
 
