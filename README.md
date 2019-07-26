## vSphere Single Palo Alto Networks VM Creator ##
Skillet to deploy and bootstrap a standalone VM-Series on vSphere environment. 

The skillet is using VMware terraform provider to automate the deployment of a standalone VM-Series in vSphere environment.
The deployment will include:
- Creating bootstrapping iso file to bootstrap the VM-Series
- Uploading the bootstrapping iso file to the datastore.
- Creating a VM folder in vCenter.
- Creating a VM-Series VM from a base image template.
- Attach the bootstrapping ISO file.
- Power on the VM-Series.

After running the skillet, a standalone VM-Series will be deployed in the vSphere environment. And it will be configured with management configuration and connects to Panorama, if a Panorama Server IP is added as part of the variables.

## prerequisites ##
Before running this skillet you need to create a VM-Series VM template in your vCenter environment.

You can create the VM-Series VM Template using the following steps:

* Step 1.	Download the VM-Series base image ova file from the support portal
https://support.paloaltonetworks.com/

* Step 2.	Deploy the OVA image to vCenter. (DO NOT POWER ON THE VM)
More info can be found at:
https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vm_admin.doc/GUID-17BEDA21-43F6-41F4-8FB2-E01D275FE9B4.html

* Step 3.	Convert the VM to a Template
Right click on the VM and select Template > Convert to Template

## Usage ##

1- Import this repo into your panhandler.

2- Run the skillet and fill the following fields and click submit (Make sure to add quotes if the value will contain space):
* "user"  - description = "vSphere user name"
* "password"  - description = "vSphere password"
* "vsphere_server"  - description = "vCenter server FQDN or IP"
* "vsphere_datacenter"  - description = "In which datacenter the VM will be deployed"
* "vsphere_vm_name"  - description = "What is the name of the VM"
* "vsphere_vm_template"  - description = "Where is the VM template located"
* "vsphere_vm_folder"  - description = "In which folder the VM will be store"
* "vsphere_cluster"  - description = "In which cluster the VM will be deployed"
* "vsphere_vcpu_number"  - description = "How many vCPU will be assigned to the VM"
* "vsphere_memory_size"  - description = "How much RAM will be assigned to the VM"
* "vsphere_datastore"  - description = "What is the name of the VM datastore"
* "vsphere_port_group_mgmt"  - description = "In which port group the VM NIC will be configured for management interface (default: VM Network)"
* "vsphere_port_group_untrust"  - description = "In which port group the VM NIC will be configured for untrust interface (default: VM Network)"
* "vsphere_port_group_trust"  - description = "In which port group the VM NIC will be configured for trust interface (default: VM Network)"
* "pavm_hostname"  - description = "VM-Series hostname (Optional)"
* "pavm_ip_address"  - description = "VM-Series management IP address (Optional)"
* "pavm_netmask"  - description = "VM-Series management netmask (Optional)"
* "pavm_gateway"  - description = "VM-Series management gateway (Optional)"
* "pavm_dns_primary"  - description = "VM-Series managemenet primary DNS (Optional)"
* "pavm_dns_secondary"  - description = "VM-Series management secondary DNS (Optional)"
* "panorama_server_ip"  - description = "Panorama Server IP address (Optional)"
* "panorama_tplname"  - description = "Panorama template stack name (Optional)"
* "panorama_dgname"  - description = "Panorama device group name (Optional)"
* "panorama_vm_auth_key"  - description = "Panorama VM authentication Key (Optional)"
* "pavm_authcode"  - description = "VM-Series license auth code (Optional)" 

3- Select "Validate, init, and Apply" and then click submit.

4- After the init process finish click "Continue".

5- Wait for the Validate process to finish successfully then click "Continue".

6- Review the tasks plan and click "Continue".

7- Wait for the skillet to apply all the tasks and then click "Continue".

8- Finally, review the output and click "Continue". Before accessing the VM management URL please wait for the bootstrapping process to finish.

## Support Policy

The code and templates in the repo are released under an as-is, best effort,
support policy. These scripts should be seen as community supported and
Palo Alto Networks will contribute our expertise as and when possible.
We do not provide technical support or help in using or troubleshooting the
components of the project through our normal support options such as
Palo Alto Networks support teams, or ASC (Authorized Support Centers)
partners and backline support options. The underlying product used
(the VM-Series firewall) by the scripts or templates are still supported,
but the support is only for the product functionality and not for help in
deploying or using the template or script itself. Unless explicitly tagged,
all projects or work posted in our GitHub repository
(at https://github.com/PaloAltoNetworks) or sites other than our official
Downloads page on https://support.paloaltonetworks.com are provided under
