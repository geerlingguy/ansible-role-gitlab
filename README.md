# Ansible Role: GitLab

Installs GitLab, a Ruby-based front-end to Git, on any RHEL/CentOS Linux system.

GitLab's default administrator account details are below; be sure to login immediately after installation and change these credentials!

    admin@local.host
    5iveL!fe

## Requirements

Requires Git 1.8.x or later (installed via `geerlingguy.git` when the variable `git_install_from_source` set to `true`.

The other main dependencies are listed in 'dependencies' below.

## Role Variables

Available variables are listed below, along with default values (see `vars/main.yml`):

    hostname: gitlab
    gitlab_url: https://gitlab/

The hostname and URL by which GitLab will be accessed.

    gitlab_database_name: gitlabhq_production
    gitlab_database_password: secret

The database name and password for gitlab (user defaults to `git`).

## Dependencies

  - geerlingguy.git
  - geerlingguy.mysql
  - geerlingguy.redis
  - geerlingguy.nginx
  - geerlingguy.ruby

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - { role: geerlingguy.gitlab }

*Inside `vars/main.yml`*:

    hostname: gitlab
    
    git_install_from_source: true
    git_version: "1.8.3"
    
    gitlab_url: https://gitlab/
    gitlab_database_name: gitlabhq_production
    gitlab_database_password: secret
    
    mysql_root_password: root
    mysql_enablerepo: epel
    mysql_packages:
      - mysql
      - mysql-server
      - mysql-devel
      - MySQL-python

## TODO

  - Break main.yml into smaller task includes.
  - Allow use of PostgreSQL instead of MySQL.
  - Allow use of Apache instead of Nginx.

## License

MIT / BSD

## Author Information

This role was created in 2014 by Jeff Geerling (@geerlingguy), author of Ansible for DevOps. You can find out more about the book at http://ansiblefordevops.com/, and learn about the author at http://jeffgeerling.com/.
