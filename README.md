# og_ansible

___For all Playbooks you will need to create an OpsGenie API Integration, for anything that is specfic to provisioning in OpsGenie ( Users, Teams, Integrations etc etc ) Then make sure that the API does not have "Restrict Configuration Access" ticked.___

### Variables

You can specify the vars in the playbook or in a file, if you want them in the playbook then simply in the header add a vars section like so.
```
- name: Create OpsGenie Services 
  hosts: localhost
  gather_facts: false
  vars:
    api_key: <your_api_key>
    someothervar: answer
  tasks:
    - name: Get List of all Teams
```
You can also create a file and reference that, for instance I will create a file called my_vars and in the header instead of using vars, we use vars_files and the file path needs to be relative to the playbook, 
```
- name: Create OpsGenie Services 
  hosts: localhost
  gather_facts: false
  vars_files: my_vars <or subdir/myvars>
  tasks:
    - name: Get List of all Teams
```
If you dont want to edit the playbooks then you can supply the vars file on the execution of the playbook by running the following
```
ansible-playbook <playbook_name> -e @myvars
```
# Playbooks
---
##### ANy of the vars that are marked as Bold are required where as anything else is optional and if not declared will take the API default value if it exists, this is fully documented here

https://docs.opsgenie.com/docs/api-overview

create_alerts.yml

The following vars can be specified under a var called alert.
```
alert:
  message: <Required string format>
  alias: <Not Required WIll become the Ticket ID so be carefule if Dedupe is needed>
  description: <Not Required string format>
  responders: <Not Required list format below example>
    - username: user@example.com
      type: user
    - name: teamname
      type: team
  visableTo: <Not Required list format below example>
    - username: user@example.com
      type: user
    - name: teamname
      type: team
  actions: <Not Required list format below example>
    - action1
    - action2
  tags: <Not Required list format below example>
    - tag1
    - tag2
  details: <Not Required key value pair mappings format below example>
    key1: value1
    key2: value2
  alias: <Not Required string format>
  source: <Not Required string format>
  alias: <Not Required string format>
  user: <Not Required string format>
  note: <Not Required string format>
```
