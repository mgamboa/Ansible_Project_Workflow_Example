# workflow

This is a comprehensive Ansible project structure suitable for use with AWX workflows, including VM infrastructure setup, configuration, and destruction.

## Project Structure

```
workflow/
├── ansible.cfg
├── inventories/
│   ├── production/
│   │   ├── hosts
│   │   ├── group_vars/
│   │   └── host_vars/
│   ├── staging/
│   └── development/
├── group_vars/
├── host_vars/
├── library/
├── module_utils/
├── filter_plugins/
├── roles/
│   ├── common/
│   ├── webserver/
│   ├── database/
│   ├── loadbalancer/
│   ├── monitoring/
│   └── security/
├── playbooks/
│   ├── site.yml
│   ├── webservers.yml
│   ├── databases.yml
│   ├── loadbalancers.yml
│   ├── setup_vm_infrastructure.yml
│   └── destroy_deployment.yml
└── collections/
```

## Workflows

This project structure supports complex AWX workflows, including:

1. VM Infrastructure Setup
2. Infrastructure Configuration
3. Application Deployment
4. Deployment Destruction

Each workflow can be implemented using the playbooks in the `playbooks/` directory.

## Usage

To use this project with AWX:

1. Import this project into AWX
2. Create job templates for each playbook
3. Create workflows that chain together multiple job templates

For example, a full deployment workflow might include:

1. Run `setup_vm_infrastructure.yml` to create and configure VMs
2. Run `site.yml` to configure all servers
3. Run role-specific playbooks to deploy applications

To destroy the deployment:

1. Run `destroy_deployment.yml` to remove all created VMs

Adjust the playbooks and roles as needed for your specific infrastructure and application requirements.

### VM Infrastructure Setup

The `setup_vm_infrastructure.yml` playbook provides automated VM creation with static IP assignment. It's set to create 4 VMs by default: 1 webserver, 1 database server, 1 load balancer, and 1 monitoring server. The IP range for these VMs is set from 192.168.2.50 to 192.168.2.60.

### Deployment Destruction

The `destroy_deployment.yml` playbook allows you to tear down the entire infrastructure. Use this playbook with caution, as it will permanently delete the specified VMs.

## Configuration

Default variables are set in the common role's defaults file. You can override these in your AWX environment, inventory, or when running playbooks. Key variables include:

- vcenter_hostname: "192.168.2.101"
- vcenter_username: "Administrator@vsphere.local"
- vcenter_password: "" (set this in AWX for security)
- datacenter_name: "Datacenter"
- cluster_name: "ITMCO"
- template_name: "Client"
- vm_folder: "/vm/AAP_HOSTS"
- vm_network: "DSwitch-VM Network"
- domain_name: "itmco.local"
- ip_netmask: "255.255.255.0"
- ip_gateway: "192.168.2.1"
- dns1: "192.168.2.1"
- dns2: "192.168.2.1"

Review and adjust these settings to match your specific environment requirements.
