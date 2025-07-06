# azurelab1
Create and Configure Azure Virtual Machines using Azure CLI

Step1: Create Resource Group

Bash Command: az group create --name MyResourceGroup104 --location westeurope

![Screenshot from 2025-07-06 10-55-52](https://github.com/user-attachments/assets/2f1efc1a-c463-4896-a30a-87b71809eef8)

Checked the resource group in the portal is has been made:
![Screenshot from 2025-07-06 11-01-41](https://github.com/user-attachments/assets/b29f1657-ebbf-4630-8223-755ca415282b)

A resourcegroup is required to group your resources.

Step2: Create  aVirtual Network (Vnet)

Bash command:az network vnet create --name My104VNet --resource-group MyResourceGroup104 --subnet-name Mysubnet

![Screenshot from 2025-07-06 11-07-05](https://github.com/user-attachments/assets/8cdbf434-c36d-4534-84bb-fd47dab14d93)


Step3: Create Public Ipadress

Bash command: az network public-ip create --name MyPublicIp --resource-group MyresourceGroup --allocation-method Dynamic 

![Screenshot from 2025-07-06 11-32-14](https://github.com/user-attachments/assets/4638764b-090d-4a35-afcf-6013ea5ca469)

I received an error when tryiing to create a Public Ip address. This happens bbecause Standard SKU Public IPs must be static, not dynamic.

To Resolve i had to change my command to:

Bash Command: az network public-ip create --name MyPublicIp --resource-group MyresourceGroup104 --sku Standard --allocation-method Static 

![Screenshot from 2025-07-06 11-33-38](https://github.com/user-attachments/assets/c84b0101-4255-4cd7-9dbb-7b503b94c70c)


Step4: Create Network Interface (NIC)

Bash Command:
az network nic create --resource-group MyResourceGroup104 --name MyNic --vnet-name My104VNet --subnet Mysubnet --public-ip-address MypublicIP

Step5: Create Virtual Machine

Bash Command: az vm create   --resource-group MyResourceGroup104   --name MyLinuxVM   --nics MyNIC   --image UbuntuLTS   --admin-username azureuser   --admin-password 123456

I received a few errors when i was buildng my LinuxVM, i had an invalid VM image and the Password lenght of My Vm was not compliant.

![Screenshot from 2025-07-06 11-41-57](https://github.com/user-attachments/assets/5c88ebd5-3f06-4ae7-b95d-4c0968520290)

running/:
![Screenshot from 2025-07-06 11-46-09](https://github.com/user-attachments/assets/0aa37e6a-6ddc-4ea4-b870-27a4bac08d1c)

Now i have a Running LinuxVm:

{
  "fqdns": "",
  "id": "/subscriptions/000dda75-5cc0-434a-89d4-70b097cbe53d/resourceGroups/MyResourceGroup104/providers/Microsoft.Compute/virtualMachines/MyLinuxVM",
  "location": "westeurope",
  "macAddress": "7C-ED-8D-16-0D-48",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "4.210.155.248",
  "resourceGroup": "MyResourceGroup104",
  "zones": ""




![Screenshot from 2025-07-06 11-47-57](https://github.com/user-attachments/assets/f728f228-57ad-4e67-9898-b75b7f18bb8a)


Step6: Open Port 22 for in NSG (Network Security Group) 
(I dont use port3389 RDP is for Security Reasons)
