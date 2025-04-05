# Setting up Active Directory on Windows Server 2019

This guide offers a clear, step-by-step process for setting up a Windows Server 2019 machine, installing Active Directory Domain Services (AD DS), promoting the server to a domain controller, and configuring DNS. Furthermore, it addresses important concepts related to Active Directory, Group Policy Management (GPM), and Registry Editor, which are essential for effectively managing a Windows server environment.

*(Will add a picture to explain the whole setup)*

### 1. Preparing the Windows Server 2019 Environment

Before beginning the installation, ensure you have the following:

- A fresh installation of Windows Server 2019 (Standard or Datacenter version).
- A static IP address (recommended for AD DS and DNS).
- Administrative credentials for the server.

#### Steps to Prepare the Server:
- **Install Windows Server 2019**: Follow the installation steps for Windows Server 2019 on your machine.
- **Configure the Server**: Set the machine’s hostname and ensure it has a static IP address:
    - Open **Network and Sharing Center** → **Change Adapter Settings** → Right-click your network adapter → **Properties** → **Internet Protocol Version 4 (TCP/IPv4)** → Set a static IP address.

> **Tip**: *Install the Latest Windows Updates*: It’s always a good idea to ensure the server is current.

---

### 2. Installing Active Directory Domain Services (AD DS)

Active Directory Domain Services is the role that provides a central directory for user authentication and resource management.

#### Steps to Install AD DS:
- **Open Server Manager**: After logging in to the server, click the **Server Manager** icon in the taskbar.
- **Add Roles and Features**:
    - Click on **Add Roles and Features**.
    - Click **Next** until you reach the **Server Roles** section.
    - Check the box next to **Active Directory Domain Services** and click **Next**.
- **Install**: Continue the wizard, reviewing the features, and click **Install**. This will install the necessary components for Active Directory.

---

### 3. Promoting the Server to Domain Controller

After installing AD DS, the next step is to promote the server to a Domain Controller.

#### Steps to Promote the Server:
- **Open Server Manager**.
- Once AD DS is installed, click on the **Notification Flag** at the top right and click **Promote this server to a domain controller**.
- **Important Note**: Ensure that **AD CS** is not set up before promoting the server to a domain controller. If it is, the promotion will fail at the pre-requisite test.

<tb>![Error](https://github.com/imuhammadhusnain/ActiveDirectory-Setup/blob/main/AD%20DS%20error%20prerequisite.png)</tb>

**Please note**: *I resolved the error by going to Tools at the top right in Server Manager, removing the AD CS service, completing the promotion of the server to a Domain Controller, and then reinstalling the AD CS from Tools.*

#### Deployment Configuration:
<tb>![snip](https://github.com/imuhammadhusnain/ActiveDirectory-Setup/blob/main/AD%20DS%201.png)</tb>
- Choose **Add a new forest** if you are setting up a new domain, and provide a **Root domain name** (e.g., example.local).
- Select the **Forest functional level** (Windows Server 2016 or higher is recommended).
- Set the **Domain functional level** (usually the same as the forest functional level).
<tb>![snip](https://github.com/imuhammadhusnain/ActiveDirectory-Setup/blob/main/AD%20DS%202.png)</tb>
- Set the **Directory Services Restore Mode (DSRM)** password: This password is important for emergency scenarios where you need to restore AD.

Review the selections and click **Next**. The server will now be promoted to a domain controller, and it will automatically reboot once the promotion is complete.

---

### 4. Installing and Configuring DNS

DNS (Domain Name System) is required for AD DS to function properly. It resolves domain names to IP addresses, enabling communication across the network.

#### Steps to Install DNS:
- **Install DNS Role**: You can also install the DNS server role during the promotion process. If not already installed:
    - Open **Server Manager** → **Add Roles and Features**.
    - Select the **DNS Server** and proceed with the installation.
- **Configure DNS**: After the installation, DNS should automatically configure itself during the domain controller promotion. However, you can verify and manage the DNS settings by opening the **DNS Manager**.

---

## 5. Understanding Key Concepts

### Active Directory:
Active Directory (AD) is a directory service used to manage permissions and access to networked resources. It stores information about users, computers, and other network resources, allowing for centralized management.

(Will add picture here for (DNS))
### DNS (Domain Name System):
DNS is essential for translating human-readable domain names (like example.local) into IP addresses that computers use to identify each other on the network. AD relies on DNS for locating domain controllers.

(Will add picture here for (AD DS DC))
### Domain Controller (DC):
A Domain Controller is a server that responds to security authentication requests (logging in, checking permissions, etc.). It stores and manages the Active Directory database.

---

## 6. Group Policy (GP) & Group Policy Objects (GPO)

### Group Policy (GP):
Group Policy is a Microsoft feature that allows administrators to control user and computer settings in an Active Directory environment. This includes setting security policies, software installation, and other configurations across the entire domain.

### Group Policy Objects (GPO):
GPOs are collections of settings that are applied to computers and users within a domain. A GPO can be linked to an organizational unit (OU), site, or domain.

<tb>![snip](https://github.com/imuhammadhusnain/ActiveDirectory-Setup/blob/main/GPO.png)</tb>

#### Common GPO Configurations:
- **Password Policies**: Set password complexity, length, expiration, and lockout settings.
- **Software Installation**: Automate the installation of applications.
- **User Permissions**: Control which users have access to specific resources.

#### To manage GPOs:
- Open **Group Policy Management** from the Server Manager.
- Right-click on **Group Policy Objects** and choose **New** to create a new GPO.
- Right-click the newly created GPO, select **Edit**, and configure the policies within the **Group Policy Management Editor**.
- Link the GPO to the appropriate domain, site, or organizational unit (OU).

#### Applying the GPO Changes:
Once you have configured and linked the GPOs, you can force the changes to take effect immediately using the following command on the affected machine:

```bash
gpupdate /force
```

### 7. Top-Level Policies in Corporate Environments

- **Password Policy**:  
A strong password policy ensures security by enforcing requirements like minimum length, complexity (uppercase, lowercase, digits, symbols), and expiration.

- **Account Lockout Policy**:  
This policy defines how many failed login attempts a user can have before their account is locked for a specified period. This helps prevent brute-force attacks.

- **Software Restriction Policies**:  
These policies are used to control which software can or cannot run on domain-connected machines. They enhance security by preventing the execution of unauthorized software.

- **Audit Policy**:  
Audit policies allow administrators to track events such as logins, file access, and system changes. These logs are critical for monitoring the security of the network.

These are the most useful policies in the organization that can be easily deployed and are well understood in how they work. Additionally, many others can be configured based on requirements.

---

### Final Thoughts

Setting up Active Directory on Windows Server 2019 is a fundamental skill for any IT professional managing network environments. By mastering the installation of AD DS, DNS, and Group Policy, you’ll be equipped to create a secure, scalable, and efficient infrastructure for managing users and resources. These concepts are not only critical in small to medium-sized organizations but are also essential in large enterprise environments.

By following this guide, you're not just setting up a server—you're enhancing your understanding of organizational infrastructure, which is crucial for any IT professional. Trying this setup will expand your knowledge and help you see the bigger picture of how a network should operate, securing and optimising it for smooth management. This experience will undoubtedly sharpen your skills and give you the confidence to handle more complex IT challenges.

**Happy configuring! 🚀**
---
