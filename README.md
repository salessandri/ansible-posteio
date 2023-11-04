# poste.io

This role sets up a mailserver using the dockerized free version of [poste.io](https://poste.io/).

This only takes care of setting up the service, its configuration is done through the web interface once the service is running.

## Requirements

This role relies on `docker` being available on the host and the [`docker_container` ansible module](https://docs.ansible.com/ansible/latest/modules/docker_container_module.html) in ansible.

To cover the first one, the [`geerlingguy.docker` role](https://galaxy.ansible.com/geerlingguy/docker) can be used.

To cover the dependencies for the `docker_container` module the [`geerlingguy.pip` role](https://galaxy.ansible.com/geerlingguy/pip) can be used to install Python's [`docker` package](https://pypi.org/project/docker/).

Only the _host_ networking mode is supported for the time being, thus the following ports needs to be available on the host machine and will be used by the mailserver: **_25, 80, 110, 143, 443, 465, 587, 993, 995_** and **_4190_**.

## Role Variables

 - **`posteio__version`** (optional, default: _2.3.14_): Image version tag to use.
 - **`posteio__container_name`** (optional, default: _posteio-mailserver_): Name to use for the container created by the role.
 - **`posteio__timezone`** (optional, default: _UTC_): Timezone to configure on the mailserver. Valid options can be found in [this Wikipedia article](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).
 - **`posteio__data_dir`** (optional, default _/var/posteio/_): Folder to use for storing the persistent files.
 - **`posteio__clamav`** (optional, default: _yes_): Enable/disable ClamAV.
 - **`posteio__rspamd`** (optional, default: _yes_): Enable/disable Rspamd.
 - **`posteio__roundcube`** (optional, default: _yes_): Enable/disable Roundcube webmail.

## Example Playbook

The following would be a fairly common role usage example:

```yaml
- host: mail.my-domain.com
  roles:
    - role: salessandri.posteio
```

## License

MIT

## Author Information

This role was created in 2020 by [Santiago Alessandri](https://rambling-ideas.salessandri.name).
