**Increase VM disk size**

The ansible playbook (increase_vm_disk_size.yml)[increase_vm_disk_size.yml] increases the size of a Windows virtual machine in VMware. 

When you run the playbook you need to specify the name of the VM, the letter of the drive to expand and the percent you would like to increase it. 
```
ansible-playbook increase_vm_disk.yml -e 'vm_name=TEST_VM drive_letter=E percent_to_increase=10' --ask-vault
```
First, I get the disk serial number inside the OS based on the drive letter and then I use that serial number to identify the disk in VMware. 

The disk is finally expanded in the VM and later inside the Windows OS. 
