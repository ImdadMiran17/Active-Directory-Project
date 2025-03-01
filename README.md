# Active Directory Configuration and Management in Virtualbox

In this project, I have configured an Active Directory environment with Microsoft server 2022 as domain controller. I have added a Windows 10 host and a Ubuntu server as domain users. Also Managed user accounts, groups, and organizational units (OUs), and implemented Group Policy Objects (GPOs) to enforce centralized security and resource management. Virtualbox is my goto software for creating virtual machines as always. Let's dive into the fun stuff now.

### What do we need :|
* Obviously, Virtualbox. But If you prefer Vmware or Hyper-v, that's also fine.
* Microsoft Windows server 2022. You can download it from the Official site if you're in the selected region. Or else, You can download it from here.
* Windows 10 host. You can download the ISO file from the official site via the installation media.
* Ubuntu Server 24.04 or latest version. You can download it from the official site.

First of all, we have to configure the network in Virtualbox. Set it to NAT Network. Create a NAT network and give it a IP range. Let's say, `192.168.10.0/24`. While configuring system, we have to set the network as NAT network as the hosts will be connected internally as well as to the internet.

Now, let's install both the windows and ubuntu hosts which will act as the domain users. 

## Configuring Windows 10 Target PC

Installing windows 10 is a straight forward process which you can find here. Just remember one thing carefully. Install Windows pro version, not Home or anything. Only in Windows 10 pro, you are allowed to join as Domain users.

After installing Windows 10, Let's change the name of our PC to `Target-PC`. Search for `This PC` with windows search functionality. Right click on `This PC` and choose `Properties`. Here, you will find a button that says `Rename this PC`. Change the name from here. 

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20000406.png)

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20001655.png)

In Windows 10, IP address is set automatically by default. Let's set a static IP address. First, right click on the ethernet icon in the taskbar and choose `Open Network & Internet settings`. 
Scroll down a bit and choose `Change adapter options`. 
There is only ethernet adapter. Right click on Ethernet option and choose properties. Then select `Internet Protocol Version 4 (TCP/IPv4) Properties` and click on properties. It is set to automatic by default. Change it to manual and set IP address, subnet mask, default gateway and DNS server.

# Configuring Ubuntu Server

We can say the same thing about the Ubuntu server. For system configuration, you can follow this. Other than that, it's only a matter of clicking some 'Done's and 'Continue's. You will face this screen surely. Complete it according to your preferences.

![Profile Configuration](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20205733.png)


