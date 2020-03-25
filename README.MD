
Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required and registered in the file `requirements.txt`

Role/Environments Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. Environments dependent variables goes to `environments/env_name`

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

The dependent roles are mentioned in `galaxy.yml` file. You can install those via ansible-galaxy,

    $ ansible-galaxy install -r galaxy.yml

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }


Example quick install & play runbook
----------------
Provide the host IPs in order to login with ansible `environments/prod/inventory`
```
[master_node]
  x.x.x.x
[data_node_1]
  x.x.x.x
  x.x.x.x
[data_node_2]
  x.x.x.x
  x.x.x.x
  x.x.x.x
```
Provide the essentials ansible vars to login  `environments/prod/group_vars/prod.yml`
```
ansible_user: ubuntu
ansible_ssh_private_key_file: ~/.ssh/your_pem_key
ansible_ssh_port: ssh port number to login default (22)
```

Fill the variables `environments/prod/group_vars/elastic.yml`
```
cluster_name: "test-cluster" # provide cluster-name
master_private_host1: "10.0.2.154:9300" # provide the master's private IP
private_hosts: "10.0.2.154:9300,10.0.2.196:9300,10.0.2.182:9300" # replace it with nodes private IPs
```

Finally, time to run the playbook as follows 

```
virtualenv ~/.virtualenvs/ansible
source ~/.virtualenvs/ansible/bin/activate
pip install -r requirements.txt
ansible-galaxy install -r galaxy.yml
ansible-playbook -i environments/prod/inventory -e "env=prod" -t "elastic_setup"  play.yml
```