﻿<a name="title" />
# Connecting Cloud Services #

---

<a name="Overview" />
## Overview ##
This demonstration will show how to connect a traditional Windows Azure web role to a virtual machine running SQL server using a virtual network. 

> **Note:** In order to run through this complete demo, you must have network connectivity and a Microsoft account.

<a id="goals" />
### Goals ###
In this demo, you will see three things:

1.	Configuring a simple virtual network. 
1.	Configure a SQL server VM 
1.	Connecting a web role to the Windows Azure Virtual Network.
1.	Taking advantage of full SQL server from a web role.
1.	This configuration is low latency and highly secure as the web role and the VM are on the same virtual network.

<a name="technologies" />
### Key Technologies ###

This demo uses the following technologies:

- [Windows Azure Management Portal] [1]
- [Visual Studio 2012] [2]

[1]: https://manage.windowsazure.com/
[2]: http://www.microsoft.com/visualstudio/11

<a name="setup" />
### Setup and Configuration ###
To configure this demonstration you will need to walk through the hands on lab:

[Connecting a PaaS application to an IaaS Application with a Virtual Network](https://github.com/WindowsAzure-TrainingKit/HOL-WindowsAzureVMandWebRoleVNet)

---

<a name="Demo" />
## Demo ##

This demo is composed of the following segments:

1. [Configure a virtual network](#segment1)
1. [Deploy a SQL server into the VNET](#segment2)
1. [Configure Windows Azure Cloud Service Project to join the VNET and connect to existing SQL Server](#segment3)

<a name="segment1" />
### Configure a Virtual Network  ###


> **Speaking Point:** In the next 7 minutes, I will configure a simple Windows Azure virtual network and deploy Windows Azure application to connect directly to a SQL Server running on a virtual machine. The application we are going to deploy has a dependency on SQL Server Full Text Search. To solve this problem we will create a virtual network, deploy a SQL Server and configure the Windows Azure Web Role to connect directly through the VNET.

1. Follow the steps to configure the virtual network in the Windows Azure Management portal:

	> **Note:** _HOL_: Windows Azure Virtual Machines and Web Role with VNET.
	> _Section_: Getting Started - Configuring Virtual Networking

	> **Important** - Name the VNET **MyVNET-1** because MyVNET will already exist.

	![Creating a Virtual Network](Images/creating-a-virtual-network.png?raw=true "Creating a Virtual Network")

	_Creating a Virtual Network_

	> **Speaking Point:** Creating a virtual network allows multiple cloud services to connect and communicate with each other. The advantages are the connection is secure because public endpoints like SQL Server 1433 are never exposed and very low latency because the applications are on the same network and do not require additional hops through the load balancer. 


<a name="segment2" />
### SQL Server Deployment ###

1. Provision a new virtual machine using the SQL Server evaluation edition into the VNET to demonstrate how VMs get into the VNET. 

	> **Note:** Use the initial steps from **Exercise 1** of the "**Windows Azure Virtual Machines and Web Role with VNET**" HOL to walk through the VM creation gallery experience. 
	>
	> Do not configure data disks and deploy the VM - just walk through the wizard to show connectivity to the VNET. Note that you have already done this in another SQL VM. 

	![Provisioning a new VM](Images/provisioning-a-new-vm.png?raw=true "Provisioning a new VM")
	
	_Provisioning a new VM_


	> **Speaking Point:** Explain that in order to connect you will select the VNET to join the VM to the virtual network you just created.

1. Select the **AppSubnet** Subnet.

	![VM Options](Images/vm-options.png?raw=true "VM Options")
	
	_VM Options_


<a name="segment3" />
### Configure Windows Azure Cloud Service Project ###

> **Speaking Point:** I have previously configured this SQL Server with the database for the application, enabled full text search and have configured the data disks and firewall rules. 

1. Log into the already configured SQL Server.

	> **Speaking Point:** To have the application connect to the SQL Server I need the IP address. VNET solutions do not have out of the box name resolution. 

1. Run **IPConfig** to retrieve the SQL Server IP address.

	![IPConfig](Images/ipconfig.png?raw=true "IPConfig")
	
	_Getting the IP of the SQL Server VM_

1. Open the **Windows Azure Project** from the "**Windows Azure Virtual Machines and Web Role with VNET**" hands on lab. 

1. In Visual Studio, Open the **Web.config** and modify the connection strings to use the new IP Address for the SQL Server. 

	> **Note:** Refer to Exercise 2: Step 9 of the HOL

1. Open the **ServiceConfiguration.cscfg** file and add the network configuration to connect to the virtual network.

	> **Note:** Refer to Exercise 2: Step 10 of the HOL

1. Walk through the steps to deploy the application to the same cloud service but do not actually finish the deployment (not enough time to actually deploy).

1. Browse to running site - demonstrate search.

	![Browsing the Application](Images/browsing-the-web-site.png?raw=true "Browsing the Application")

	_Browsing the Application_

---

<a name="summary" />
## Summary ##

In this demonstration you saw how to provision a simple cloud only virtual network that allows you to directly connect a cloud service with a traditional Windows Azure PaaS webrole directly to a cloud service hosting full SQL Server. 