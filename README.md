# azurelab1
Create and Configure Azure Virtual Machines using Azure CLI

Step1: Create Resource Group

Bash Command: az group create --name MyResourceGroup104 --location westeurope
![Screenshot from 2025-07-06 12-43-48](https://github.com/user-attachments/assets/85d343f0-0f64-4433-84a5-90059b9414f3)

![Screenshot from 2025-07-06 12-46-36](https://github.com/user-attachments/assets/af8ee937-1b61-484b-a373-2e444678a04a)

Checked the resource group in the portal is has been made:


A resourcegroup is required to group your resources.

Step2: Create  aVirtual Network (Vnet)

Bash command:az network vnet create --name My104VNet --resource-group MyResourceGroup104 --subnet-name Mysubnet

![Screenshot from 2025-07-06 12-58-41](https://github.com/user-attachments/assets/9f57c996-d878-406c-85f9-30b33b2c7083)


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

Bash Command: az vm create   --resource-group MyResourceGroup104   --name MyLinuxVM   --nics MyNIC   --image UbuntuLTS   --admin-username azureuser   --admin-password #givenpassword

I received a few errors when i was buildng my LinuxVM, i had an invalid VM image and the Password lenght of My Vm was not compliant.

![Screenshot from 2025-07-06 11-41-57](https://github.com/user-attachments/assets/5c88ebd5-3f06-4ae7-b95d-4c0968520290)

running/:
![Screenshot from 2025-07-06 11-46-09](https://github.com/user-attachments/assets/0aa37e6a-6ddc-4ea4-b870-27a4bac08d1c)

Now i have a Running LinuxVm:


![Screenshot from 2025-07-06 11-47-57](https://github.com/user-attachments/assets/f728f228-57ad-4e67-9898-b75b7f18bb8a)

Step6: Create a Networksecurity group (NSG)
az network nsg create --resource-group MyResourceGroup104 --name MyNSG


![Screenshot from 2025-07-06 12-16-43](https://github.com/user-attachments/assets/53137968-7cd3-4ef5-bc24-b5039e649924)


Step7: Create a NSG rule to Open Port 22  
(I dont use a Windows VM + port3389 RDP is not secure)

Bash Command:
az network nsg rule create --resource-group MyResourceGroup104 --nsg-name MyNSG --name AllowSSH --protocol tcp --direction inbound --priority 100 --source-address-prefixes '*' --source-port-ranges '*' --destination-port-ranges 22 --access allow

![Screenshot from 2025-07-06 12-16-54](https://github.com/user-attachments/assets/a820a15c-e50f-417a-b5e6-46d2844ff240)


Step 8: associate NSG with NIC

Bash command:
az network nic update --resource-group MyResourceGroup104 --name MyLinuxVMVMNic --network-security-group MyNSG

Step 9: Open Port 22 

az vm open-port --port 22 --resource-group MyResourceGroup104 --name MyLinuxVM
![Screenshot from 2025-07-06 12-23-17](https://github.com/user-attachments/assets/839f53cd-35dd-407e-9833-049ec0bfa211)

Step 10: 

Bash Command: 
Connect to the VM with SSH protocol:

ssh azureuser@4.210.155.248
![Screenshot from 2025-07-06 12-25-49](https://github.com/user-attachments/assets/e8d5cf25-fc9e-4c3c-8349-ebde05702348)

Im in!!!

![Screenshot from 2025-07-06 12-26-35](https://github.com/user-attachments/assets/5fba24bb-2407-49f2-b62f-5fdc080d7e2c)

