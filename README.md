# Ansible-network_snmp

Ansible role that configures snmp settings on network devices.  

The configuration of the role is done so that it shouldn't be necessary to modify the role for any configuration.
All settings can be configured by changing role parameters or by declaring new config as variable.

Please report any issues or send PR.

nxos specific: if password strength-check is enabled on device and you use a password that doesn't meet the reqs the task fails silently.  

## Examples

```yaml
---
- name: Example of how to configure snmp location and contact
  hosts: sw1
  vars:
    snmp:
      location: 
        state: present
        name: colo at 2 network street
      contact:
        name: IT support
        state: present          
  roles:
    - Ansible-network_snmp

- name: Example of how to configure snmp server
  hosts: sw1
  vars:
    snmp:
      notifications:
        state: present
        user: sw_test
        host: 1.1.1.1
        type: inform                        # can be 'trap' or 'inform'
        source_int: loopback0
        port: 162
        v3_security: auth 
        version: v3
        vrf: prod
  roles:
    - Ansible-network_snmp

- name: Example of how to configure snmp users
  hosts: sw1
  vars:
    snmp:
      user:
        state: present
        user: snmp_test
        auth: sha                           # 'md5' or 'sha'
        pwd: testPA18                        # auth pass when using md5 or sha. not idempotent
        group: network-operator
        encrypt: yes                        # enables AES-128 encryption when using privacy password.    
        privacy: testPass1
  roles:
    - Ansible-network_snmp

```

## Role variables

```yaml
---
# Define the snmp settings to be configured (see README for examples)
snmp: { }
```


## License

Apache


## Author

Dan Murarasu