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

Step5: Create Virtual Machine

Step6: Open Port 22 for in NSG (Network Security Group) 
(I dont use port3389 RDP is for Security Reasons)
