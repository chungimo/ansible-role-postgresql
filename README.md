# Ansible Role: PostgreSQL

Installs and configures PostgreSQL server on RHEL/CentOS or Debian/Ubuntu servers.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    postgresql_enablerepo: ""

Global configuration options that will be set in `postgresql.conf`. Note that for RHEL/CentOS 6 (or very old versions of PostgreSQL), you need to at least override this variable and set the `option` to `unix_socket_directory`.

    postgresql_hba_entries:
      - { type: local, database: all, user: postgres, auth_method: peer }
      - { type: local, database: all, user: all, auth_method: peer }
      - { type: host, database: all, user: all, address: '127.0.0.1/32', auth_method: md5 }
      - { type: host, database: all, user: all, address: '::1/128', auth_method: md5 }

Configure [host based authentication](https://www.postgresql.org/docs/current/static/auth-pg-hba-conf.html) entries to be set in the `pg_hba.conf`. Options for entries include:

  - `type` (required)
  - `database` (required)
  - `user` (required)
  - `address` (one of this or the following two are required)
  - `ip_address`
  - `ip_mask`
  - `auth_method` (required)
  - `auth_options` (optional)

## Example Playbook

    - hosts: database
      become: yes
      vars_files:
        - vars/main.yml
      roles:
        - ansible-role-postgresql
