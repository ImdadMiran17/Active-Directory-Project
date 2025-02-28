# Active Directory Configuration and Management in Virtualbox

In this project, I have configured an Active Directory environment with Microsoft server 2022 as domain controller. I have added a Windows 10 host and a Ubuntu server as domain users. Also Managed user accounts, groups, and organizational units (OUs), and implemented Group Policy Objects (GPOs) to enforce centralized security and resource management. Virtualbox is my goto software for creating virtual machines as always. Let's dive into the fun stuff now.

### What do we need :|
* Obviously, Virtualbox. But If you prefer Vmware or Hyper-v, that's also fine.
* Microsoft Windows server 2022. You can download it from the Official site if you're in the selected region. Or else, You can download it from here.
* Windows 10 host. You can download the ISO file from the official site via the installation media.
* Ubuntu Server 24.04 or latest version. You can download it from the official site.

First of all, let's install both the windows and ubuntu hosts which will act as the domain users. Installing windows 10 is a straight forward process which you can find here. Just remember one thing carefully. Install Windows pro version, not Home or anything.
