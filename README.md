**Increase VM disk size**

The ansible playbook [increase_vm_disk_size.yml](increase_vm_disk_size.yml) increases the size of a virtual disk in VMware and also in the Windows OS.  

When you run the playbook you need to specify the name of the VM, the letter of the drive to expand and the percent you would like to increase it. 
```
ansible-playbook increase_vm_disk.yml -e 'vm_name=TEST_VM drive_letter=E percent_to_increase=10' --ask-vault
```
First, I get the disk serial number inside the OS based on the drive letter and then I use that serial number to identify the disk in VMware. 

The disk is finally expanded in the VM and later inside the Windows OS. 

Before running the script, update the vCenter information in the playbook (ip address, credentials and datacenter name) 

Requirements
***
* Install [pyVmomi](https://github.com/vmware/pyvmomi) 
* Install [Kerbereos Library](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html#installing-the-kerberos-library) 
* [Configure Kerberos](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html#configuring-host-kerberos)

You can create an inventory file like the one shown below. You will have to change the VM name, and the domain information.  
```
---
server_group_name:
  hosts:
    VM_NAME.contoso.corp:
  vars:
    ansible_connection: winrm
    ansible_winrm_transport: kerberos
    ansible_port: 5985
    ansible_user: admin@CONTOSO.CORP
    ansible_password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          62888888888888888888888888888888888888888888888888888888888888888888888888888888
          67777777777777777777777777777777777777777777777777777777777777777777777777777776
          34444444444444444444444444444444444444444444444444444444444444444444444444444441
          66666666666666666666666666666666666666666666666666666666666666666666666666666663
          6531
```

