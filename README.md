# Ansible Role: rclone_docker_plugin

[![Build Status][build_badge]][build_link]
[![Ansible Galaxy][galaxy_badge]][galaxy_link]

Ansible role to install & configure the [rclone Docker Volume Plugin](https://rclone.org/docker).

Install the role: `ansible-galaxy role install tigattack.rclone_docker_plugin`

See the [rclone Docker Volume Plugin documentation](https://rclone.org/docker) for further information. It's very useful for a deeper understanding of how this works.

## Role Variables

The most commonly useful variables are documented below. More variables and their default values can be seen in [default/main.yml](defaults/main.yml).

> [!IMPORTANT]  
> Changing any of these variables after initial installation is likely to cause an error, as volume plugins cannot be updated while they are still enabled and in-use by existing volumes.  
> If you need to change any of the plugin options, volumes using the plugin must be removed and the plugin must be disabled.

#### `rclone_docker_plugin_version`

Rclone volume plugin version. By default the latest available version will be installed.

#### `rclone_docker_plugin_args`

Rclone arguments. Both [rclone serve docker flags](https://rclone.org/commands/rclone_serve_docker/#options) and [generic rclone flags](https://rclone.org/flags/) are supported, including backend parameters that will be used as defaults for volume creation.

#### `rclone_docker_plugin_cache_dir`

Cache directory for rclone. There is no need to change this from the role's default value unless you have a specific reason to do so.

#### `rclone_docker_plugin_config_dir`

Config directory for rclone. The plugin will look for `rclone.conf` in this directory. There is no need to change this from the role's default value unless you have a specific reason to do so.

## Example Playbook

Simple, only install plugin:

```yml
- hosts: all
  roles:
    - role: tigattack.rclone_docker_plugin
```

Advanced, install specific plugin version with custom args and a custom cache directory:

```yml
- hosts: all
  roles:
    - role: tigattack.rclone_docker_plugin
      vars:
        rclone_docker_plugin_version: '1.65.2'
        rclone_docker_plugin_args: >-
          --allow-other
          --vfs-cache-mode=full
          --vfs-cache-max-size=5G
        rclone_docker_plugin_cache_dir: /home/user/.cache/rclone
```

# Attribution

Thanks to [cycneuramus](https://github.com/cycneuramus) for the foundations of this role's functionality ([cycneuramus/ansible-hybrid-cloud](https://github.com/cycneuramus/ansible-hybrid-cloud/blob/master/roles/rclone-docker-plugin/tasks/main.yml)).

[build_badge]:  https://img.shields.io/github/actions/workflow/status/tigattack/ansible-rclone-rc-remotes/ci.yml?branch=main&label=Ansible%20Lint
[build_link]:   https://github.com/tigattack/ansible-rclone-rc-remotes/actions?query=workflow:CI
[galaxy_badge]: https://img.shields.io/ansible/role/d/tigattack/rclone_docker_plugin
[galaxy_link]:  https://galaxy.ansible.com/tigattack/rclone_docker_plugin
