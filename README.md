ssh_hostkey_restore
=========

Manages ssh_hostkey so that you don't have to deal with complaints from the SSH tools (and ansible).

Requirements
------------

None

Role Variables
--------------

    ssh_key_config: which key types to handle
        - file_name: file name portion (.pub added as well)
        - algorithm: algorithm (rsa, dsa, ecdsa, ed25519)
    ssh_key_dir: directory to hold the keys


Dependencies
------------

In order for this to function correctly, `control_path` must be `control_path=%(directory)s/%%C` in the ansible.cfg.
As of Ansible 2.2, the `control_path` default was changed to something that I couldn't easily replicate in jinja2, 
thus, I switched to using the `%C` from OpenSSH 6.7+ [GBP]

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - ssh_hostkey_restore

License
-------

Proprietary

