# Azure_Routing
how create a routing tabele to route bettwen 2 difrent subnet using virtual appliance 

check this : https://learn.microsoft.com/en-us/azure/virtual-network/tutorial-create-route-table-portal

## Overview
This lab demonstrates how to connect two different subnets in Azure using a virtual appliance and routing tables. By configuring routing between the subnets via a virtual appliance, you can control and manage the traffic flow between them.

## Prerequisites
Before starting the lab, make sure you have the following:

An Azure subscription
Access to the Azure portal
Basic understanding of Azure networking concepts such as subnets, virtual networks, and routing
A virtual appliance (NVA - Network Virtual Appliance) deployed in your Azure environment

### Create a Resource Group:
Create a resource group named "cisco-vnet".
```bash
az group create --name cisco-vnet --location <your_location>
```

### Create 3 Subnets:
Create three subnets: 
- usa-zone, 
- jpan-zone, 
- nva-zone.

Assign IP ranges for each subnet:
- usa-zone: 10.10.0.0/24
- jpan-zone: 10.20.0.0/24
- nva-zone: 10.30.0.0/24


### Create 3 Virtual Machines and Assign to Subnets:
Create three virtual machines, one for each subnet, and assign each virtual machine to its corresponding subnet.


### Enabel ip forwding in the vna machine 
"![image](https://github.com/Mouhamed-dridi/Azure_Routing/assets/53900924/522fa715-cd7b-4875-949c-7ecd6c309332)
"
In this section, turn on IP forwarding for the operating system of the vm-nva virtual machine to forward network traffic. 
```bash
sudo vim /etc/sysctl.conf
```

In the Vim editor, remove the # from the line net.ipv4.ip_forward=1
```bash
Uncomment the next line to enable packet forwarding for IPv4
net.ipv4.ip_forward=1
```

## Create a route table : 
create a simple routing tabel called highway 59  and create a route called usa_to_jpan
![image](https://github.com/Mouhamed-dridi/Azure_Routing/assets/53900924/5128be8a-a273-44ed-a304-9b3fa60c893b)

- add name
- destaion
- nextope address "ip nva"
- type virtual appliance

  #### add source route address

- Select Subnets in Settings.
- Select + Associate.
- Enter or select the following information in Associate subnet:

## Testing Connectivity Between VMs

To trace the routing of network traffic from `vm-usa` to `vm-jpan`, execute the following command:

```bash
tracepath 10.20.0.4
```
After executing the above command, please reboot the VMs and verify the connectivity
