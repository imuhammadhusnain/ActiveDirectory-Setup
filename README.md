# Setting up Active Directory on Windows Server 2019

This guide offers a clear, step-by-step process for setting up a Windows Server 2019 machine, installing Active Directory Domain Services (AD DS), promoting the server to a domain controller, and configuring DNS. Furthermore, it addresses important concepts related to Active Directory, Group Policy Management (GPM), and Registry Editor, which are essential for effectively managing a Windows server environment.

 (Will add a picture to explain the whole setup)

<h3>1. Preparing the Windows Server 2019 Environment</h3>
Before beginning the installation, ensure you have the following:

- A fresh installation of Windows Server 2019 (Standard or Datacenter version).
- A static IP address (recommended for AD DS and DNS).
- Administrative credentials for the server.

Steps to Prepare the Server:
- Install Windows Server 2019: Follow the installation steps for Windows Server 2019 on your machine.
- Configure the Server: Set the machine’s hostname and ensure it has a static IP address:
- Open Network and Sharing Center → Change Adapter Settings → Right-click your network adapter → Properties → Internet Protocol Version 4 (TCP/IPv4) → Set a static IP address.

Tip: Install the Latest Windows Updates: It’s always a good idea to ensure the server is current.

<h3>2. Installing Active Directory Domain Services (AD DS)</h3>
Active Directory Domain Services is the role that provides a central directory for user authentication and resource management.

Steps to Install AD DS:
Open Server Manager: 
- After logging in to the server, click the Server Manager icon in the taskbar.
- Add Roles and Features:
- Click on Add Roles and Features.
- Click Next until you reach the Server Roles section.
- Check the box next to Active Directory Domain Services and click Next.

Install: Continue the wizard, reviewing the features, and click Install. This will install the necessary components for Active Directory.

<h3>3. Promoting the Server to Domain Controller</h3>
After installing AD DS, the next step is to promote the server to a Domain Controller.

Steps to Promote the Server:
- Open Server Manager.
- Once AD DS is installed, click on the Notification Flag at the top right and click Promote this server to a domain controller.
- And also, please make sure you do not set up AD CS before promoting a server to a domain controller, otherwise it will fail at the pre-requisites test.

?
 
Deployment Configuration:

- Choose Add a new forest if you are setting up a new domain, and provide a Root domain name (e.g., example.local).
- Select the Forest functional level (Windows Server 2016 or higher is recommended).
- Set the Domain functional level (usually the same as the forest functional level).
- Set Directory Services Restore Mode (DSRM) password: This password is important for emergency scenarios where you need to restore AD.

Review the selections and click Next. The server will now be promoted to a domain controller, and it will automatically reboot once the promotion is complete.

<h3>4. Installing and Configuring DNS</h3>
DNS (Domain Name System) is required for AD DS to function properly. It resolves domain names to IP addresses, enabling communication across the network.

Steps to Install DNS:
- Install DNS Role: You can also install the DNS server role during the promotion process. If not already installed:
- Open Server Manager → Add Roles and Features.
- Select the DNS Server and proceed with the installation.
- Configure DNS: After the installation, DNS should automatically configure itself during the domain controller promotion. However, you can verify and manage the DNS settings by opening the DNS Manager.

<h2>5. Understanding Key Concepts</h2>
<h3>Active Directory:</h3>
Active Directory (AD) is a directory service used to manage permissions and access to networked resources. It stores information about users, computers, and other network resources, allowing for centralized management.

<h3>DNS (Domain Name System):</h3>
DNS is essential for translating human-readable domain names (like example.local) into IP addresses that computers use to identify each other on the network. AD relies on DNS for locating domain controllers.

<h3>Domain Controller (DC): </h3>
A Domain Controller is a server that responds to security authentication requests (logging in, checking permissions, etc.). It stores and manages the Active Directory database.

<h3>6. Group Policy (GP) & Group Policy Objects (GPO)</h3>
Group Policy (GP):
Group Policy is a Microsoft feature that allows administrators to control user and computer settings in an Active Directory environment. This includes setting security policies, software installation, and other configurations across the entire domain.

Group Policy Objects (GPO):
GPOs are collections of settings that are applied to computers and users within a domain. A GPO can be linked to an organizational unit (OU), site, or domain.

Common GPO Configurations:
- Password Policies: Set password complexity, length, expiration, and lockout settings.
- Software Installation: Automate the installation of applications.
- User Permissions: Control which users have access to specific resources.
- To manage GPOs, use the Group Policy Management Console (GPMC).

Steps for Managing GPOs:
- Open Group Policy Management from the Server Manager.
- Right-click on Group Policy Objects and choose New to create a new GPO.
- Right-click the newly created GPO, select Edit, and configure the policies within the Group Policy Management Editor.
- Link the GPO to the appropriate domain, site, or organizational unit (OU).

<h3>7. Registry Editor Overview</h3>
What is the Registry Editor?
The Registry Editor (regedit) is a powerful tool in Windows that allows administrators to view and modify the system registry. The registry stores configuration settings for the operating system, software, hardware, and user preferences.

While the registry is essential, it should be used cautiously, as improper changes can damage the system. Always back up the registry before making any modifications.

<h3>8. Top-Level Policies in Corporate Environments</h3>
Password Policy:
A strong password policy ensures security by enforcing requirements like minimum length, complexity (uppercase, lowercase, digits, symbols), and expiration.

Account Lockout Policy:
This policy defines how many failed login attempts a user can have before their account is locked for a specified period. This helps prevent brute-force attacks.

Software Restriction Policies:
These policies are used to control which software can or cannot run on the domain-connected machines. They enhance security by preventing the execution of unauthorized software.

Audit Policy:
Audit policies allow administrators to track events such as logins, file access, and system changes. These logs are critical for monitoring the security of the network.

<h3>Final Thoughts</h3>
Setting up Active Directory on Windows Server 2019 is a fundamental skill for any IT professional managing network environments. By mastering the installation of AD DS, DNS, and Group Policy, you’ll be equipped to create a secure, scalable, and efficient infrastructure for managing users and resources. These concepts are not only critical in small to medium-sized organizations but are also essential in large enterprise environments.

By following this guide, you’ve taken the first step toward becoming proficient in the most commonly used tools in Windows server administration. With further exploration and experience, you’ll be able to optimize and secure your environment, ensuring smooth operation and better management of your network.

<p>Happy configuring!&#128640;</p>

