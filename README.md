ssh_hostkey_restore
=========

Manages ssh_hostkey so that you don't have to deal with complaints from the SSH tools (and ansible).
Works on SmartOS and at least Ubuntu, raspi and Debian varieties of Linux.

Requirements
------------

None

Role Variables
--------------

    ssh_key_config: which key types to handle
        - file_name: file name portion (.pub added as well)
        - algorithm: algorithm (rsa, dsa, ecdsa, ed25519)
    ssh_key_dir: directory to hold the keys
	ssh_use_existing_keys: define to use keys on host instead of from storage

	Note: the following are pairs, the _best version is our current best practices, the
    	plain version is the one that gets rendered, both are lists. 
	sshd_kex_algorithms_best: best-practice key exchange algorithms
	sshd_kex_algorithms: [sshd_kex_algorithms_best]
	sshd_ca_sig_algorithms_best:
	sshd_ca_sig_algorithms: "{{ sshd_ca_sig_algorithms_best }}"
	sshd_host_based_accepted_key_algorithms_best: [sshd_host_key_algorithms_best]
	sshd_host_based_accepted_key_algorithms: "{{ sshd_host_based_accepted_key_algorithms_best }}"
	sshd_host_key_algorithms_best: 
	sshd_host_key_algorithms: [sshd_host_key_algorithms_best]
	sshd_pubkey_accepted_key_types_best: [sshd_host_key_algorithms_best]
	sshd_pubkey_accepted_key_types: [sshd_pubkey_accepted_key_types_best]
	sshd_mac_algorithms_best: 
	sshd_mac_algorithms: [sshd_mac_algorithms_best]
	sshd_ciphers_best:
	sshd_ciphers: [sshd_ciphers_best]

Inherited Role Variables
------------------------
	vault_ssh_sign_path: secrets engine for signing host keys. If defined, all keys will be signed
	vault_ssh_key_mount: path to ssh keys storage if present


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

    - hosts: cranky_servers
      roles:
        - ssh_hostkey_restore
      vars:
        - sshd_mac_algorithms: "{{ sshd_mac_algorithms_best+['hmac-sha2-512']}}"

License
-------

MIT

