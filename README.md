# Nginx Role

An Ansible role for installing and configuring Nginx, including enabling sites and validating configurations.

## Requirements

- The role requires a Debian-based system with `apt` as the package manager.
- Ensure Ansible is installed and properly configured on your control node.

## Role Variables

The following variables can be configured to customize the role:

- `nginx_site_template_file`: Path to the Nginx site configuration template file.
  - Default: `templates/site.conf.j2`
- `nginx_site_available_dir`: Directory where the Nginx site configuration will be copied.
  - Default: `/etc/nginx/sites-available/{{ site_name }}`
- `nginx_site_enabled_dir`: Directory for symbolic links to enabled sites.
  - Default: `/etc/nginx/sites-enabled/{{ site_name }}`

## Dependencies

This role has no external dependencies.

## Example Playbook

Below is an example of how to use the role in your playbook:

```yaml
- name: Deploy and configure Nginx
  hosts: web
  become: true
  vars:
    nginx_site_template_file: "nginx.conf.j2"
    nginx_site_available_dir: "/etc/nginx/sites-available/my_site"
    nginx_site_enabled_dir: "/etc/nginx/sites-enabled/my_site"
  roles:
    - nginx
```

## Handlers

This role includes the following handler:

- Reload Nginx: Reloads the Nginx service after configuration changes.