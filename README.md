<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory within Azure VMs</h1>
This project details how to configure and setup an Active Directory Lab using Azure Virtual Machines.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a Domain Controller VM with Windows Server 2022
- Create Client PC VM with Windows 10
- Install Active Directory on DC(Domain Controller)
- Create Admin and User Accounts
- Join Client VM to AD domain

<h2>Deployment and Configuration Steps</h2>

<h3>Setting up resources.</h3>

![image](https://github.com/loog4/configure-ad/assets/80493463/f6604498-9c06-466b-a615-100c27e730fe)

<p>Create the Domain Controller VM first</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/feef4f99-9508-4910-ae3d-d1724f2985ed)

![image](https://github.com/loog4/configure-ad/assets/80493463/33e90fc5-d8d8-4a4f-8f54-88240925f5c4)

<p>Next, Go to DC-1's network interface and set its private IP to static.</p>
<p>This is to make sure the Client VM will be able to use DC-1's IP as its DNS server in order to join it.</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/e67c5605-88f4-4a4e-8416-39f018fbbdf7)

![image](https://github.com/loog4/configure-ad/assets/80493463/1740623d-0076-43b4-9cee-35b37e6f2706)

<p>Create the Client-1 VM. (Make sure to set its Resource Group and Vnet is the same as DC-1's)</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/f9aa3f5e-39bf-482b-a76c-be06698d8fa8)

<p>If we login to Client-1 and ping DC-1, we can see that our requests get timed out.</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/9d40ebcb-ea69-4559-b7d0-7dc17bce025e)

<p>Go into DC-1 and allow the ICMPv4 in the firewall settings.</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/8cb58116-5246-42ab-8b00-4eca8c34fbad)

<p>This time our ping request go through now.</p>

<h3>Installing Active Directory</h3>

![image](https://github.com/loog4/configure-ad/assets/80493463/5bc18f7c-040f-47a5-8743-291a3b2776bf)
![image](https://github.com/loog4/configure-ad/assets/80493463/d240f115-3735-483c-a629-599ffea210b9)
![image](https://github.com/loog4/configure-ad/assets/80493463/6dcc8b19-c5d1-467e-bdf4-fb5f7977e6d1)

<p>Go to DC-1 and install Active Directoy Domain Services in Server Manager</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/2608d6a9-41d0-439e-9a2b-a3f552f02cb9)
![image](https://github.com/loog4/configure-ad/assets/80493463/466c5b02-9b57-481e-a8fc-a451676d5fd5)

<p>Next click the flag with the yellow exclamation point and promote the VM as a DC</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/c1ccabe4-c0ad-4b48-8dc3-c30b7216bb07)

<p>Your connection will close eventually and you will have to log back in but with the domain name in username shown</p>

<h3>Creating Accounts</h3>

![image](https://github.com/loog4/configure-ad/assets/80493463/c621fa96-b4b9-49df-bb81-6546105d9775)
![image](https://github.com/loog4/configure-ad/assets/80493463/ce4fc9f8-8f3e-415b-a58f-d39a246c3c25)

<p>Go to Active Directoy Users and Computers and create a new Organizational Unit (OU) called “_EMPLOYEES” (or any name you wish)</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/cc5e5f4d-4bff-4679-9c4c-b8689f3778fc)

<p>Create another for admin accounts</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/22f75fbb-c638-4092-882e-bf45027e54c8)
![image](https://github.com/loog4/configure-ad/assets/80493463/9dfd3acc-7ebe-469a-b311-91d71dd2712f)
![image](https://github.com/loog4/configure-ad/assets/80493463/0abf4462-502b-4024-a057-c905110a73bd)
![image](https://github.com/loog4/configure-ad/assets/80493463/b7968ca6-e626-4ef5-9061-1c12dd87698c)
![image](https://github.com/loog4/configure-ad/assets/80493463/7c51d05d-d539-43fd-bcc8-461420c904c8)


<p>Create a new Admin account inside of the _ADMINS OU</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/2c9877e4-5cd6-4aa9-9f9e-9f33b37c8adb)
![image](https://github.com/loog4/configure-ad/assets/80493463/a68cd615-d748-4c4e-b371-25f1de4392d5)


<p>Log out and log back in but this time with the admin account we created.</p>
<p>This will be the admin account we will be using from here on out.</p>

<h3>Join Client-1 to the domain (adlab.com)</h3>

![image](https://github.com/loog4/configure-ad/assets/80493463/21023988-ce01-491a-a284-f81b579c5891)

<p>In Client-1's network interface settings, change its DNS server to the private IP of DC-1</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/6dc0dc81-e29c-4c24-9578-b5aa05f06fce)

<p>Restart Client-1 and login as the original admin account</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/def78553-6171-4778-8227-cf14a521683e)
![image](https://github.com/loog4/configure-ad/assets/80493463/eb46785e-80ae-46d8-adfb-20665445f54a)
![image](https://github.com/loog4/configure-ad/assets/80493463/88513659-09b2-4f2a-a597-3c76c5d08dad)

<p>On Client-1, Join the VM to the domain</p>

![image](https://github.com/loog4/configure-ad/assets/80493463/3d887210-63c7-47c7-b796-e9a9dd52500f)

<p>Client-1 will now show up on the DC as a connected PC</p>
<p>Optional: Create an OU called _CLIENTS and drag the pc to it</p>

<h3>End of Lab</h3>
<p>That concludes this lab in which configured a barebones setup of Active Directory with a computer joined to its domain.</p>

















