kube-user
=========

- Create kube user.
- Add user to group to obtain root throuh sudo.
- Create ssh pair key
- Add ssh pub key for auth
- Fetch priv key stores under `~/kube_keys/<fqdn>/<key_name>`

Requirements
------------

ssh access

Role Variables
--------------

- `ssh_key_type`: Key type supported, depends on client, default: ecdsa.
- `username`: Username of user to create, default: kube.
- `shell`:  Shell to use for the user, default: /bin/bash.

Dependencies
------------

none

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - { role: kube-user }
```

License
-------


Author Information
------------------

doxmx
