docker_install_fedora
=========

This Ansible role installs and configures Docker Engine on Fedora hosts. It ensures any previous Docker installations and data are safely removed, sets up the official Docker repository, installs the required packages, and manages user group membership for Docker access.


Requirements
------------

- Target host must be running Fedora server (v41 or 42).
- Ansible 2.9+ recommended.


Role Variables
--------------

Variables can be set in `defaults/main.yml`, `vars/main.yml`, or passed as parameters.

- `docker_users`: List of users to be added to the `docker` group. Default value is `user`

Example:
```yaml
docker_users:
  - user1
  - user2
```

Dependencies
------------

No external role dependencies.

Warning
------------

The task responsible for starting the Docker service (`systemctl enable docker`) is not automatically tested within the Molecule environment. In production environments, you might need to manually enable and start the Docker service using `systemctl enable docker` and `systemctl start docker` to ensure it starts on boot.


Tags
----------------

- `cleanup_docker`:  
  Use this tag to safely remove old Docker data (`/var/lib/docker`).  
  Example usage:
  ```sh
  ansible-playbook playbook.yml --tags cleanup_docker
  ```
  By default, this block is skipped unless explicitly tagged.

Example Playbook
----------------


```yaml
- hosts: fedora_hosts
  roles:
    - role: docker_install_fedora
      docker_users:
        - alice
        - bob
```

License
-------

BSD

Author Information
------------------

Role maintained by tomhn0808
