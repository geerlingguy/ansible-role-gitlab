# Ansible Role: GitLab

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-gitlab.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-gitlab)

Installs GitLab, a Ruby-based front-end to Git, on any RedHat/CentOS or Debian/Ubuntu linux system.

GitLab's default administrator account details are below; be sure to login immediately after installation and change these credentials!

    root
    5iveL!fe

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    gitlab_external_url: "https://gitlab/"

The URL at which the GitLab instance will be accessible. This is set as the `external_url` configuration setting in `gitlab.rb`, and if you want to run GitLab on a different port (besides 80/443), you can specify the port here (e.g. `https://gitlab:8443/` for port 8443).

    gitlab_git_data_dir: "/var/opt/gitlab/git-data"

The `gitlab_git_data_url` is the location where all the Git repositories will be stored. You can use a shared drive or any path on the system.

    gitlab_edition: "gitlab-ce"

The edition of GitLab to install. Usually either `gitlab-ce` (Community Edition) or `gitlab-ee` (Enterprise Edition).

    # SSL Configuration.
    gitlab_redirect_http_to_https: "true"
    gitlab_ssl_certificate: "/etc/gitlab/ssl/gitlab.crt"
    gitlab_ssl_certificate_key: "/etc/gitlab/ssl/gitlab.key"

GitLab SSL configuration; tells GitLab to redirect normal http requests to https, and the path to the certificate and key (the default values will work for automatic self-signed certificate creation, if set to `true` in the variable below).

    # SSL Self-signed Certificate Configuration.
    gitlab_create_self_signed_cert: "true"
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

    gitlab_time_zone: "UTC"

Gitlab timezone.

    gitlab_backup_keep_time: "604800"

How long to keep local backups (useful if you don't want backups to fill up your drive!).

    # Email configuration.
    gitlab_email_enabled: "false"
    gitlab_email_from: "gitlab@example.com"
    gitlab_email_display_name: "Gitlab"
    gitlab_email_reply_to: "gitlab@example.com"

Gitlab system mail configuration. Disabled by default; set `gitlab_email_enabled` to `true` to enable, and make sure you enter valid from/reply-to values.

    gitlab_nginx_listen_port: 8080

If you are running GitLab behind a reverse proxy, you may want to override the listen port to something else.

    gitlab_nginx_listen_https: "false"

If you are running GitLab behind a reverse proxy, you may wish to terminate SSL at another proxy server or load balancer

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

This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
