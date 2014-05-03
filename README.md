# Ansible Role: GitLab

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-gitlab.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-gitlab)

Installs GitLab, a Ruby-based front-end to Git, on any RedHat or Debian-based linux system.

GitLab's default administrator account details are below; be sure to login immediately after installation and change these credentials!

    admin@local.host
    5iveL!fe

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `vars/main.yml`):

    gitlab_package_url: ""

The package/version of GitLab to be downloaded. This is a platform-specific variable, and the defaults are defined in the platform-specific vars file inside `vars/`. You can find the latest version URLs on the [GitLab downloads page](https://www.gitlab.com/downloads/).

    # General config.
    gitlab_external_url: "https://gitlab/"
    gitlab_git_data_dir: "/var/opt/gitlab/git-data"

General GitLab configuration. The `gitlab_git_data_url` is the location where all the Git repositories will be stored. You can use a shared drive or any path on the system.

    # SSL Configuration.
    gitlab_redirect_http_to_https: "true"
    gitlab_ssl_certificate: "/etc/gitlab/ssl/gitlab.crt"
    gitlab_ssl_certificate_key: "/etc/gitlab/ssl/gitlab.key"

GitLab SSL TODO...

    # SSL Self-signed Certificate Configuration.
    gitlab_create_self_signed_cert: true
    gitlab_self_signed_cert_subj: "/C=US/ST=Missouri/L=Saint Louis/O=IT/CN=gitlab"

    # LDAP Configuration.
    gitlab_ldap_enabled: "false"
    gitlab_ldap_host: "example.com"
    gitlab_ldap_port: "389"
    gitlab_ldap_uid: "sAMAccountName"
    gitlab_ldap_method: "plain"
    gitlab_ldap_bind_dn: "CN=Username,CN=Users,DC=example,DC=com"
    gitlab_ldap_password: "password"
    gitlab_ldap_base: "DC=example,DC=com"

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
