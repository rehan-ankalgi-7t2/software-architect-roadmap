# Exercise - Create an Azure virtual machine
In this exercise, you create an Azure virtual machine (VM) and install Nginx, a popular web server.

You could use the Azure portal, the Azure CLI, Azure PowerShell, or an Azure Resource Manager (ARM) template.

In this instance, you're going to use the Azure CLI.

## Task 1: Create a Linux virtual machine and install Nginx
1. From Cloud Shell, run the following az vm create command to create a Linux VM:
```Bash
az vm create \
  --resource-group "learn-38311a6c-f07f-4431-8869-9010a18bc23d" \
  --name my-vm \
  --public-ip-sku Standard \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys    


output:
/usr/lib64/az/lib/python3.9/site-packages/paramiko/pkey.py:100: CryptographyDeprecationWarning: TripleDES has been moved to cryptography.hazmat.decrepit.ciphers.algorithms.TripleDES and will be removed from this module in 48.0.0.
  "cipher": algorithms.TripleDES,
/usr/lib64/az/lib/python3.9/site-packages/paramiko/transport.py:259: CryptographyDeprecationWarning: TripleDES has been moved to cryptography.hazmat.decrepit.ciphers.algorithms.TripleDES and will be removed from this module in 48.0.0.
  "class": algorithms.TripleDES,
SSH key files '/home/rehanankalgi7t2/.ssh/id_rsa' and '/home/rehanankalgi7t2/.ssh/id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. If using machines without permanent storage, back up your keys to a safe location.
{
  "fqdns": "",
  "id": "/subscriptions/66934742-a2f4-4f94-ad7b-07a47d83d2bc/resourceGroups/learn-38311a6c-f07f-4431-8869-9010a18bc23d/providers/Microsoft.Compute/virtualMachines/my-vm",
  "location": "westus",
  "macAddress": "60-45-BD-04-67-B1",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.174.108",
  "resourceGroup": "learn-38311a6c-f07f-4431-8869-9010a18bc23d",
  "zones": ""
}
```

Your VM takes a few moments to come up. You named the VM my-vm. You use this name to refer to the VM in later steps.

2. Run the following az vm extension set command to configure Nginx on your VM:

```Bash
az vm extension set \
  --resource-group "learn-38311a6c-f07f-4431-8869-9010a18bc23d" \
  --vm-name my-vm \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --version 2.1 \
  --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
  --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'  

output:
{
  "autoUpgradeMinorVersion": true,
  "enableAutomaticUpgrade": null,
  "forceUpdateTag": null,
  "id": "/subscriptions/66934742-a2f4-4f94-ad7b-07a47d83d2bc/resourceGroups/learn-38311a6c-f07f-4431-8869-9010a18bc23d/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/customScript",
  "instanceView": null,
  "location": "westus",
  "name": "customScript",
  "protectedSettings": null,
  "protectedSettingsFromKeyVault": null,
  "provisionAfterExtensions": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.Extensions",
  "resourceGroup": "learn-38311a6c-f07f-4431-8869-9010a18bc23d",
  "settings": {
    "fileUris": [
      "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
    ]
  },
  "suppressFailures": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "2.1",
  "typePropertiesType": "customScript"
}
```

This command uses the Custom Script Extension to run a Bash script on your VM. The script is stored on GitHub. While the command runs, you can choose to examine the Bash script from a separate browser tab. To summarize, the script:

1. Runs `apt-get update` to download the latest package information from the internet. This step helps ensure that the next command can locate the latest version of the Nginx package.
2. Installs Nginx.
3. Sets the home page, */var/www/html/index.html*, to print a welcome message that includes your VM's host name.

