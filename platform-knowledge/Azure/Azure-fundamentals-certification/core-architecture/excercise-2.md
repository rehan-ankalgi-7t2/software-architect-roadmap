# Exercise - Create an Azure resource

## 1. Create a virtual machine
In this task, you’ll create a virtual machine using the Azure portal.

1. Sign in to the Azure portal.
2. Select Create a resource > Compute > Virtual Machine > Create.
3. The Create a virtual machine pane opens to the basics tab.
4. Verify or enter the following values for each setting. If a setting isn’t specified, leave the default value.
5. Select Review and Create.
6. Select Create

## 2. Verify resources created
Once the deployment is created, you can verify that Azure created not only a VM, but all of the associated resources the VM needs.

1. Select Home.
2. Select Resource groups.
3. Select the [sandbox resource group name] resource group.

You should see a list of resources in the resource group. The storage account and virtual network are associated with the Learn sandbox. However, the rest of the resources were created when you created the virtual machine. By default, Azure gave them all a similar name to help with association and grouped them in the same resource group.
