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
      algorithm: algorithm (rsa, dsa, ecdsa, ed25519)


Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - ssh_hostkey_restore

License
-------

Proprietary

