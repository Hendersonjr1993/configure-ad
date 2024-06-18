<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com/watch?v=lzHRxxSmQXc)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

1. Setup Resources in Azure

2. Create the Domain Controller VM (Windows Server 2022) named “DC-1”

3. Take note of the Resource Group and Virtual Network (Vnet) that get created at this time

4. Set Domain Controller’s NIC Private IP address to be static

![Resource group](https://github.com/Hendersonjr1993/configure-ad/assets/172805598/cf8cf2c8-3fbf-41a6-a902-3a10cf66b602)


5. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.a

6. Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher

7. Ensure Connectivity between the client and Domain Controller

8. Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)

9. Login to the Domain Controller and enable ICMPv4 on the local Windows firewall

10. Check back at Client-1 to see the ping succeed

11. Install Active Directory

12. Login to DC-1 and install Active Directory Domain Services

13. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)

14. Restart and then log back into DC-1 as user: mydomain.com\labuser

15. Create an Admin and Normal User Account in AD

16. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”

17. Create a new OU named “_ADMINS”

![Employees](https://github.com/Hendersonjr1993/configure-ad/assets/172805598/f15f71c5-8ca5-4a27-924f-55759279787f)


18. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”

19. Add jane_admin to the “Domain Admins” Security Group

20. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”

21. User jane_admin as your admin account from now on

22. Join Client-1 to your domain (mydomain.com)

23. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address

24. From the Azure Portal, restart Client-1

25. ![Restart Azure](https://github.com/Hendersonjr1993/configure-ad/assets/172805598/d37e21b5-911d-433d-a84b-2b6b8403b62a)


24. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)

26. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain

27. Create a new OU named “_CLIENTS” and drag Client-1 into there (Step is not really necessary, just for organizational purposes. I guess I skipped this in the lab!)

28. Setup Remote Desktop for non-administrative users on Client-1

29. Log into Client-1 as mydomain.com\jane_admin and open system properties

30. Click “Remote Desktop”

31. Allow “domain users” access to remote desktop

32. You can now log into Client-1 as a normal, non-administrative user now

33. Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)

34. Create a bunch of additional users and attempt to log into client-1 with one of the users

35. Login to DC-1 as jane_admin

36. Open PowerShell_ise as an administrator

37. ![Run powershell as Admin](https://github.com/Hendersonjr1993/configure-ad/assets/172805598/712fc84d-d70e-4760-8f56-5c0a1cfd0ec5)


38. Run the script and observe the accounts being created

39. When finished, open ADUC and observe the accounts in the appropriate OU

40. Attempt to log into Client-1 with one of the accounts (take note of the password in the script)

41. ![Accounts Created on vm](https://github.com/Hendersonjr1993/configure-ad/assets/172805598/c2c198b7-7720-4634-af00-583d43c3a404)


42. Finish.
