## Build AWS Infra Using Ansible
____

#### Introduction
As you all know, Ansible is a tool that is primarly intended to application deployment, updates on workstations and servers, cloud provisioning, configuration management, intra-service orchestration, and nearly anything a systems administrator does on a weekly or daily basis. In this example, we are going to find out how Ansible can be used to deploy AWS Ec2 instances and deploy website on them seamlessly.

#### Features
1. Deploy as many instances as you want, without worrying about the need for logging into your AWS console everytime you need to spin up an instance.
2. Both provisioning and management of the Ec2 instances can be controlled using single tool.
3. Since ansible is using a dynamic inventory, adding new instances or removing an existing instances will be automatically reflected in the inventory file and target nodes.

#### How to run this project
Before running this project, you must meet the following requirements
* Install python3, pip3 on your system.
* Once that has been installed, install ansible, boto3 and botocore
* Install ansible module for managing aws
```
sudo yum install python3 python3-pip
pip3 install ansible boto3 botocore
ansible-galaxy collection install amazon.aws
```
##### Using git clone, you can clone the file from git repository to your local machine
```
git clone https://github.com/sreejithsasidharan1989/ansible-aws.git
```
##### Create a file called aws_creds.yml and add your AWS IAM Access Key & Secret Key into it
```
---
access_key: "IAM Access key"
secret_key: "IAM Secret key"
```
##### Check the playbook syntax
```
ansible-playbook main.yml --syntax-check
```
##### Execute the playbook
```
ansible-playbook main.yml
```

#### Result
Upon successful completion, you would find result similar to the following:
```
PLAY [Build AWS Infra Using Ansible] ***************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************
ok: [localhost]

TASK [Create SSH Key pair] *************************************************************************************************
changed: [localhost]

TASK [Save SSH Private Key] ************************************************************************************************
changed: [localhost]

TASK [Create Securtiy Group] ***********************************************************************************************
changed: [localhost]

TASK [Creating Ec2 Instance] ***********************************************************************************************
changed: [localhost]

TASK [Hold Ansible] ********************************************************************************************************
ok: [localhost]

TASK [Fetch instance details] **********************************************************************************************
ok: [localhost]

TASK [Generate Dynamic Inventory] ****************************************************************************************************************************
ok: [localhost] => (item={'ami_launch_index': 0, 'image_id': 'ami-01a4f99c4ac11b03c', 'instance_id': 'i-02a5fbbfb1671f5bc', 'instance_type': 't2.micro', 'key_name': 'ansible-build', 'launch_time': '2023-02-28T07:23:00+00:00', 'monitoring': {'state': 'disabled'}, 'placement': {'availability_zone': 'ap-south-1a', 'group_name': '', 'tenancy': 'default'}, 'private_dns_name': 'ip-172-31-33-77.ap-south-1.compute.internal', 'private_ip_address': '172.31.33.77', 'product_codes': [], 'public_dns_name': 'ec2-13-232-212-139.ap-south-1.compute.amazonaws.com', 'public_ip_address': '13.232.212.139', 'state': {'code': 16, 'name': 'running'}, 'state_transition_reason': '', 'subnet_id': 'subnet-00cdbb7cf471dd8b5', 'vpc_id': 'vpc-072b3ccdb2cc070e3', 'architecture': 'x86_64', 'block_device_mappings': [{'device_name': '/dev/xvda', 'ebs': {'attach_time': '2023-02-28T07:23:01+00:00', 'delete_on_termination': True, 'status': 'attached', 'volume_id': 'vol-0c42b80c1f0de16d0'}}], 'client_token': '2dec45d3b57d4038ba963ca218154313', 'ebs_optimized': False, 'ena_support': True, 'hypervisor': 'xen', 'network_interfaces': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-13-232-212-139.ap-south-1.compute.amazonaws.com', 'public_ip': '13.232.212.139'}, 'attachment': {'attach_time': '2023-02-28T07:23:00+00:00', 'attachment_id': 'eni-attach-07896daec28e402c9', 'delete_on_termination': True, 'device_index': 0, 'status': 'attached', 'network_card_index': 0}, 'description': '', 'groups': [{'group_name': 'ansible-build', 'group_id': 'sg-04418b4644d7a3453'}], 'ipv6_addresses': [], 'mac_address': '02:a9:6b:b5:10:4e', 'network_interface_id': 'eni-0b499d597d0faad61', 'owner_id': '588583838275', 'private_dns_name': 'ip-172-31-33-77.ap-south-1.compute.internal', 'private_ip_address': '172.31.33.77', 'private_ip_addresses': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-13-232-212-139.ap-south-1.compute.amazonaws.com', 'public_ip': '13.232.212.139'}, 'primary': True, 'private_dns_name': 'ip-172-31-33-77.ap-south-1.compute.internal', 'private_ip_address': '172.31.33.77'}], 'source_dest_check': True, 'status': 'in-use', 'subnet_id': 'subnet-00cdbb7cf471dd8b5', 'vpc_id': 'vpc-072b3ccdb2cc070e3', 'interface_type': 'interface'}], 'root_device_name': '/dev/xvda', 'root_device_type': 'ebs', 'security_groups': [{'group_name': 'ansible-build', 'group_id': 'sg-04418b4644d7a3453'}], 'source_dest_check': True, 'tags': {'Name': 'server-ansible-build', 'Environment': 'build', 'Project': 'ansible'}, 'virtualization_type': 'hvm', 'cpu_options': {'core_count': 1, 'threads_per_core': 1}, 'capacity_reservation_specification': {'capacity_reservation_preference': 'open'}, 'hibernation_options': {'configured': False}, 'metadata_options': {'state': 'applied', 'http_tokens': 'optional', 'http_put_response_hop_limit': 1, 'http_endpoint': 'enabled', 'http_protocol_ipv6': 'disabled', 'instance_metadata_tags': 'disabled'}, 'enclave_options': {'enabled': False}, 'platform_details': 'Linux/UNIX', 'usage_operation': 'RunInstances', 'usage_operation_update_time': '2023-02-28T07:23:00+00:00', 'private_dns_name_options': {'hostname_type': 'ip-name', 'enable_resource_name_dns_a_record': False, 'enable_resource_name_dns_aaaa_record': False}, 'maintenance_options': {'auto_recovery': 'default'}})

PLAY [Deploy Website from GutHub] ****************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************
ok: [13.232.212.139]

TASK [Installing packages] *************************************************************************************************
changed: [13.232.212.139]

TASK [Create httpd.conf file] **********************************************************************************************
changed: [13.232.212.139]

TASK [Deploy Virtualhost for website.backtracker.tech] *********************************************************************************************************
changed: [13.232.212.139]

TASK [Create DocumentRoot for website.backtracker.tech] ********************************************************************************************************
changed: [13.232.212.139]

TASK [Create clone destination] ********************************************************************************************
changed: [13.232.212.139]

TASK [Clone website files from https://github.com/sreejithsasidharan1989/aws-elb-site.git] *********************************************************************
changed: [13.232.212.139]

TASK [Apply changes to website.backtracker.tech site files] ****************************************************************************************************
changed: [13.232.212.139]

RUNNING HANDLER [apache-reload] ********************************************************************************************
changed: [13.232.212.139]

RUNNING HANDLER [apache-restart] *******************************************************************************************************************************
changed: [13.232.212.139]

RUNNING HANDLER [ansible-hold] *********************************************************************************************
ok: [13.232.212.139]

PLAY RECAP *****************************************************************************************************************
13.232.212.139             : ok=11   changed=9    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```