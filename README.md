# Ansible Role: GitLab

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-gitlab.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-gitlab)

Installs GitLab, a Ruby-based front-end to Git, on any RHEL/CentOS Linux system.

GitLab's default administrator account details are below; be sure to login immediately after installation and change these credentials!

    admin@local.host
    5iveL!fe

## Requirements

Requires Git 1.8.x or later (installed via `geerlingguy.git` when the variable `git_install_from_source` is `true`). Git and other dependencies are listed below.

## Role Variables

Available variables are listed below, along with default values (see `vars/main.yml`):

    hostname: gitlab
    gitlab_url: https://gitlab/

The hostname and URL by which GitLab will be accessed.

    gitlab_user_home: /home/git

The home folder path for the `git` user (created for GitLab's use).

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

This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
