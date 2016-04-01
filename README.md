# Ansible Role: GitLab

[![Build Status](https://travis-ci.org/cmacrae/ansible-role-gitlab.svg?branch=master)](https://travis-ci.org/cmacrae/ansible-role-gitlab)

Installs GitLab, a Ruby-based front-end to Git, on any RedHat/CentOS or Debian/Ubuntu linux system.

GitLab's default administrator account details are below; be sure to login immediately after installation and change these credentials!

    root
    5iveL!fe

## Fork details
This is a fork of [geerlingguy/ansible-role-gitlab](https://github.com/geerlingguy/ansible-role-gitlab).  
This fork simply adds the ability to define extra static configuration in the `gitlab.rb` file.  

I am making this role more generally available as [the pull request](https://github.com/geerlingguy/ansible-role-gitlab/pull/23) has been open a little while, but it'd be nice to have these features.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    gitlab_external_url: "https://gitlab/"

The URL at which the GitLab instance will be accessible. This is set as the `external_url` configuration setting in `gitlab.rb`, and if you want to run GitLab on a different port (besides 80/443), you can specify the port here (e.g. `https://gitlab:8443/` for port 8443).

    gitlab_git_data_dir: "/var/opt/gitlab/git-data"

The `gitlab_git_data_url` is the location where all the Git repositories will be stored. You can use a shared drive or any path on the system.

    # SSL Configuration.
    gitlab_redirect_http_to_https: "true"
    gitlab_ssl_certificate: "/etc/gitlab/ssl/gitlab.crt"
    gitlab_ssl_certificate_key: "/etc/gitlab/ssl/gitlab.key"

GitLab SSL configuration; tells GitLab to redirect normal http requests to https, and the path to the certificate and key (the default values will work for automatic self-signed certificate creation, if set to `true` in the variable below).

    # SSL Self-signed Certificate Configuration.
    gitlab_create_self_signed_cert: true
    gitlab_self_signed_cert_subj: "/C=US/ST=Missouri/L=Saint Louis/O=IT/CN=gitlab"

Whether to create a self-signed certificate for serving GitLab over a secure connection. Set `gitlab_self_signed_cert_subj` according to your locality and organization.

    # LDAP Configuration.
    gitlab_ldap_enabled: "false"
    gitlab_ldap_host: "example.com"
    gitlab_ldap_port: "389"
    gitlab_ldap_uid: "sAMAccountName"
    gitlab_ldap_method: "plain"
    gitlab_ldap_bind_dn: "CN=Username,CN=Users,DC=example,DC=com"
    gitlab_ldap_password: "password"
    gitlab_ldap_base: "DC=example,DC=com"

GitLab LDAP configuration; if `gitlab_ldap_enabled` is `true`, the rest of the configuration will tell GitLab how to connect to an LDAP server for centralized authentication.

    # Extra Static Configuration
    gitlab_extra_config: ~

Extra configuration to include in `gitlab.rb`. Contents of this variable will be passed statically, meaning raw configuration options should be used, like so:

    # Extra Static Configuration
    gitlab_extra_config: |
    gitlab_rails['lfs_enabled'] = true
    gitlab_rails['lfs_storage_path'] = "/mnt/storage/lfs-objects"

This defaults to a null value - if no extra configuration is defined, it will not be included in the GitLab configuration.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - { role: geerlingguy.gitlab }

*Inside `vars/main.yml`*:

    gitlab_external_url: "https://gitlab.example.com/"

## License

MIT / BSD

## Author Information

The original role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
