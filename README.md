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


# Extending

To add more groups based on AWS tags, you can edit the inventory.py file and add more tags to the "grouping_attrs" array:

    # Default
    grouping_attrs = [
      'availability_zone',
      'tags.Purpose',
      'tags.Type',
      'tags.Ami'
    ]


## To Do

* Implement hostvars [(see Ansible docs)](http://docs.ansible.com/ansible/latest/dev_guide/developing_inventory.html)
* Make adding more tags easier - no good reason to add code
* Support other Terraform state backends
