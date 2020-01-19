ldap-users
=========

Create users and groups in an LDAP directory

Requirements
------------

 A working openLDAP installation is required for this role

Role Variables
--------------

  - home_dir:    base directory that contains the users home directories; defaults to
                 /home
  - domain_dn:   DN of the base domain in the directory
  - ldap_groups: Array of dicts of groups with the following keys:
     name:      Name of the group
     gidNumber: Group ID number
  - ldap_users:  Array of dicts of users with the following keys:
      name:          User Name
      uidNumber:     User ID number
      sn:            Surname
      gidNumber:     Main group ID number
      homeDirectory: Home directory of the user. Optional, defaults to /home/{{ username}}
      givenName:     First / christian name
      cn:            Full Name. Will appear in the GECOS field
      mail:          email address
      userPassword:  SSHA hashed password for user.
  - ldap_auth: Dictionary with the following keys:
      bind_dn: Full dn of the bind user
      bind_pass: password for the user.


Dependencies
------------

 There are no external dependencies for this role.

Example Playbook
----------------


    - hosts: servers
      vars:
        domain_dn: dc=example,dc=com
        ldap_groups:
          name: admins:
          gidNumber: 666
          members:
            - user1
        ldap_users:
          - name: user1
            sn: One
            uidNumber: 10000
            gidNumber: 10000
            givenName: User
            cn: User One
            mail: user1@example.com

      roles:
         - { role: ldap-users}

License
-------

GPLv3

Author Information
------------------

Iain M Conochie <iain@thargoid.co.uk>
