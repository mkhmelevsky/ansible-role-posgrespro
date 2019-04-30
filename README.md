# Ansible Role: PostgreSQL or Postgres Pro

## Summary

This role installs and configures patched version of PostgreSQL or Postgres Pro server on RHEL/CentOS machine
for use with 1C: Enterprise products

## Role tasks

  - Installs PostgreSQL / Postgres Pro
  - Install extensions
  - Configures PostgreSQL / Postgres Pro
  - Create DB and users
  - Add privileges to users

## Requirements
------------

  - Minimal Version of the Ansible for installation: 2.5.14
  - Supported versions:
      - PostgreSQL
          - 9.6
      - Postgres Pro Standard
          - 11
  - Supported OS:
      - RHEL
          - 6
          - 7
      - CentOS
          - 6
          - 7


## Role Variables
--------------

Available variables are listed in following files, along with their default values:

  - `defaults/main.yml`
  - `vars/{{ postgresql_daemon }}-{{ ansible_os_family }}.yml`


## Dependencies
------------

This role have no external dependencies

## Example Playbook
----------------

### Installing Postgres Pro Standard version 11:

```yaml
- name: Applying role ansible-role-postgrespro to every host in group 'dbservers'
  hosts: dbservers
  become: True
  roles:
    - role: ansible-role-postgrespro
      postgresql_daemon: postgrespro
      postgresql_version: 11
      postgresql_databases:
        - name: example_db
          owner: example_user
          encoding: UTF-8
          collation: ru_RU.UTF-8
          ctype: ru_RU.UTF-8
          hstore: False
          uuid_ossp: False
          citext: False
      postgresql_users:
        - name: example_user
          password: Sime32_U$er_p@ssw0rd
      postgresql_user_privileges:
        - name: example_user
          db: example_db
          priv: "ALL"
          role_attr_flags: "CREATEDB"
      postgresql_port: 5432
      postgresql_listen_addresses:
        - '127.0.0.1'
``` 

## License
-------

Apache

## Author Information
------------------

Author:
  - Max Khmelevsky <max.khmelevsky@yandex.ru>

