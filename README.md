<img src="https://i.imgur.com/vgcZHm6.png" width="80%" height="80%" />

# Setting Up Active Directory in Microsoft Azure Using a Virtual Machine

This tutorial provides step-by-step instructions for setting up Active Directory (AD) in Microsoft Azure using a virtual machine (VM).

## Prerequisites

- An active Azure account. If you don't have one, you can create it [here](https://azure.microsoft.com/free/).
- Basic understanding of Azure and networking concepts.

## Step 1: Set Up Your Azure Account

1. **Sign in to Azure Portal**: Go to the [Azure Portal](https://portal.azure.com) and sign in with your credentials.

## Step 2: Create a Virtual Network

1. **Navigate to Virtual Networks**: In the Azure portal, search for "Virtual Networks" in the search bar and select it.
2. **Create a New Virtual Network**:
   - Click on "+ Add" or "Create".
   - Fill in the necessary details like Subscription, Resource Group (create a new one if necessary), Name, and Region.
   - In the IP Addresses section, set the IPv4 address space (e.g., `10.0.0.0/16`).
   - Configure the Subnet (e.g., Name: `default`, Address range: `10.0.0.0/24`).
   - Review and create the Virtual Network.

## Step 3: Create a Virtual Machine

1. **Navigate to Virtual Machines**: In the Azure portal, search for "Virtual Machines" and select it.
2. **Create a New Virtual Machine**:
   - Click on "+ Add" or "Create".
   - Choose your Subscription and Resource Group.
   - Enter the Virtual Machine Name, select the Region, and choose appropriate availability options.
   - Choose an image (Windows Server 2019 Datacenter is recommended).
   - Select the size of the VM based on your needs.
   - Configure the Administrator account by providing a Username and Password.
   - Inbound Port Rules: Allow RDP (port 3389) for remote access.
   - Review and create the VM.

## Step 4: Configure Networking for the VM

1. **Attach the VM to the Virtual Network**: Ensure the VM is connected to the virtual network you created.
2. **Create a Network Security Group (NSG)**:
   - Navigate to "Network Security Groups" in the Azure portal.
   - Create a new NSG if not already created, and associate it with the subnet or network interface of your VM.
   - Add inbound security rules to allow necessary traffic (e.g., allow RDP, DNS, etc.).

## Step 5: Install Active Directory Domain Services (AD DS)

1. **Connect to the VM**: Use Remote Desktop Connection (RDP) to connect to the VM using its public IP address and the credentials you created.
2. **Install AD DS**:
   - Open Server Manager on the VM.
   - Click on "Add roles and features".
   - Follow the wizard and select "Role-based or feature-based installation".
   - Select your server and click next.
   - Under Server Roles, select "Active Directory Domain Services".
   - Complete the wizard and install the role.
3. **Promote the Server to a Domain Controller**:
   - After installation, a notification will appear in Server Manager. Click on it and select "Promote this server to a domain controller".
   - In the Deployment Configuration wizard, select "Add a new forest" and provide a Root domain name (e.g., `contoso.com`).
   - Follow through the wizard, configuring DNS options, NetBIOS name, paths for the AD database, logs, and SYSVOL, and complete the installation.

## Step 6: Configure DNS

1. **Configure DNS Settings**:
   - Ensure that the VM's network interface DNS server settings are pointing to the VM’s private IP address.
   - You may need to restart the VM to apply these changes.

## Step 7: Verify the AD DS Setup

1. **Verify Active Directory Installation**:
   - Open the "Active Directory Users and Computers" tool from the Start menu.
   - Ensure your domain is listed and you can create Organizational Units (OUs), users, and other AD objects.

## Step 8: Secure and Optimize Your Setup

1. **Set Up Backups**: Use Azure Backup to create regular backups of your VM and AD DS data.
2. **Monitor and Maintain**: Regularly monitor your VM performance and update Windows and AD DS to ensure security and efficiency.

## Conclusion

By following these steps, you should have a functioning Active Directory setup in Microsoft Azure using a virtual machine. This setup can be used for managing users, groups, and computers in a centralized manner.
