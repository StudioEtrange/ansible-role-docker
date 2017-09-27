
docker
=========

Install and configure Docker.
Try to be minimal.

Role Variables
--------------

### `docker_config`

A dict of options that are written into docker's `daemon.json` config file. See [the docs for dockerd](https://docs.docker.com/engine/reference/commandline/dockerd/) for a full list of available options.

Default values: (set them in your `docker_config` to overwrite)

    storage-driver: devicemapper
    log-level: info

### `docker_version`

Specify the version of Docker to install, e.g. `1.12.6`, `17.05`.


### `setup_script_md5_sum`

Default value: md5 checksum of default `docker_version` setup script (see `defaults/main.yml` for exact default value)

**If you intend to install a version of Docker other than the default, you must provide an appropriate override value for this variable.**

Either:

1. Generate an md5 checksum for the desired version's install script
1. If you know what you are doing and are not worried about security, set this variable to "no" or "false" to disable checksum verification of the setup script.

### `setup_script_url`

URL pointing to a Docker setup script that will install the specified `docker_version`.

Default value: `https://releases.rancher.com/install-docker/{{ docker_version }}.sh`

The default URL utilizes [Rancher Labs' version-specific, OS-agnostic setup scripts](https://github.com/rancher/install-docker), which in turn just install the appropriate version of `docker-ce` or `docker-engine` from the official Docker `apt` and `yum` repositories.

So this role is not stuck on any particular OS other than the script can not support.

Dependencies
------------

None

Example Playbook
----------------
Install Docker
```yaml
- hosts: servers
  roles:
    - studioetrange.docker
```

Install and configure docker
```yaml
- hosts: servers
  roles:
    - role: studioetrange.docker
      docker_config:
        live-restore: true
        userland-proxy: false
```

Testing
-------
For development, we use Vagrant.

```
git clone https://github.com/StudioEtrange/ansible-role-docker studioetrange.docker
```

Bring the VM up with

```
$ vagrant up
```

This will automatically run the playbooks against the virtual machine once it's up.  
After making changes to any playbook, you can test the provisioning with

```
$ vagrant provision
```

License
-------

MIT

Author Information
------------------

This is a fork of mongrelion's work : https://github.com/mongrelion/ansible-role-docker
