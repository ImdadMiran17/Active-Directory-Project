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

After installing Windows 10, Let's change the name of our PC to `Target-PC`. Search for `This PC` with windows search functionality. Right click on `This PC` and choose `Properties`. Here, you will find a button that says `Rename this PC`. Change the name of the PC from here. 

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20000406.png)

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20001655.png)

In Windows 10, IP address is set automatically by default. Let's set a static IP address. First, right click on the ethernet icon in the taskbar and choose `Open Network & Internet settings`. 
Scroll down a bit and choose `Change adapter options`. 

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-03-01%20174301.png)

There is only ethernet adapter. Right click on Ethernet option and choose properties.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-03-01%20174342.png)

Then select `Internet Protocol Version 4 (TCP/IPv4)` and click on properties. It is set to automatic by default. Change it to manual and set IP address, subnet mask, default gateway and DNS server. For DNS server, we can set `8.8.8.8` which is Google's DNS server.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20214526.png)

Now we should check if the IP settings are applied. Open cmd and run `ipconfig` command. Check if it's the same IP address that you have set earlier. Also, check if the DNS server is working. Run `ping` command on `google.com`.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20214744.png)

# Configuring Ubuntu Server

We can say the same thing about the Ubuntu server. For system configuration, you can follow this. Other than that, it's only a matter of clicking some 'Done's and 'Continue's. You will face this screen surely. Complete it according to your preferences.

![Profile Configuration](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20205733.png)

After the installation is done, we should upgrade the machine first. So we can run these two commands:

```
Sudo apt update
Sudo apt upgrade
```

Now, let's check the network settings of the machine. we can run:

```
ip a
```

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20212514.png)

It's set to the Windows 10 machine's IP address. So we have to set a static IP and configure DNS server of this machine. Let's edit out the networking file to add a static ip and DNS server to our linux machine.

```
sudo nano /etc/netplan/50-cloud-init.yaml
```

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20220212.png)

Here, I have set up DHCP to `no`, set a static IP and set DNS server to google's DNS server. But this won't work. The IP is set perfectly as you can see but I didn't get any connectivity. You can always check with `ping` command.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-26%20220240.png)

But why did that happen? Because we have to add the gateway IP (eg. `192.168.10.1`) to the nameservers addresses.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-27%20005247.png)

Now we are all set up. You can check connectivity and IP address settings by `ping` and `ip a` commands.

## Configuring Windows Server 2022 and Active Directory

Installing windows server is no different from installing windows 10 OS. But, while installing windows server, choose desktop version. After the installation is complete, we can follow the same procedure to set static IP address.

Now let's open server manager. In the navbar, click on **Manager** and choose **Add Roles and Features**.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20215929.png)

This wizard box will be opened.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220013.png)

Click **Next**

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220500.png)

Select **Role-based or feature-based installation** and click **Next**.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220548.png)

With the server selected, click **Next**.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220628.png)

Select **Active Directory Domain Services** and click **Next**.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220647.png)

Click **Add Features**.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220751.png)

Click **Next**.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220812.png)

Click **Next**.

![](https://raw.githubusercontent.com/ImdadMiran17/Active-Directory-Project/refs/heads/main/screenshots%20ad%20project/Screenshot%202025-02-25%20220831.png)

Click **Next**.

