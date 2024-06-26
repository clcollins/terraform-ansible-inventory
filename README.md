#This repository is archived and will no longer receive updates.

terraform-ansible-inventory
===========================

An [Ansible dynamic inventory](http://docs.ansible.com/ansible/latest/intro_dynamic_inventory.html) script for generating an inventory from a [Terraform terraform.tfstate](https://www.terraform.io/docs/state/) file.

## Features

Creates inventory groups by:

* Tags
* Availability Zone (location)


## Usage

Make sure you are in the directory that contains the terraform.tfstate file, then specifiy the inventory script in your `ansible` or `ansible-playbook` commands:

    ansible-playbook -i path.to.inventory.py site.yml webservers
    ansible -i path.to.inventory.py -m ping all


## Extending

To add more groups based on AWS tags, you can edit the inventory.py file and add more tags to the "grouping_attrs"  and "attributes" arrays.  The "grouping_attrs" array is what is used to create the actual Ansible inventory groups.

    # Default
    attributes = [
       'ami',
       'availability_zone',
       'instance_type',
       'private_dns',
       'private_ip',
       'public_dns',
       'public_ip',
       'tags.Name',
       'tags.Purpose',
       'tags.Role',
       'tags.Type',
       'tags.Ami'
     ]

    grouping_attrs = [
      'availability_zone',
      'tags.Name',
      'tags.Purpose',
      'tags.Role',
      'tags.Type',
      'tags.Ami'
    ]


## To Do

* Implement hostvars [(see Ansible docs)](http://docs.ansible.com/ansible/latest/dev_guide/developing_inventory.html)
* Make adding more tags easier - no good reason to add code
* Support other Terraform state backends
