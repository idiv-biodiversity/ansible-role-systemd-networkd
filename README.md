Ansible Role: systemd-networkd
==============================

An Ansible role that configures **systemd-networkd**.

Table of Contents
-----------------

<!-- toc -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

Requirements
------------

- Ansible 2.9

Role Variables
--------------

**Note:** This does not yet support the full complexity. If you are missing
something, pull requests are welcome!

```yml
# host_vars/my-client/vars.yml
---

systemd_networkd_networks:

  - name: 20-wired-static
    match:
      name: en*
    network:
      address: a.b.c.d/24
      gateway: a.b.c.x
      dns:
        - a.b.c.y
        - a.b.c.z
      domains:
        - example.com
      llmnr: 'no'
      multicast_dns: no
      ntp:
        - 1.ntp.example.com
        - 2.ntp.example.com
        - 3.ntp.example.com
        - 4.ntp.example.com

  - name: 50-wireless
    match:
      name: w*
    network:
      dhcp: ipv4
      link_local_addressing: ipv4
    dhcp:
      route_metric: 20

...
```

For more information, read `man 5 systemd.network`.

Dependencies
------------

None.

Example Playbook
----------------

Add to `requirements.yml`:

```yml
---

- src: idiv-biodiversity.systemd_networkd

...
```

Download:

```console
$ ansible-galaxy install -r requirements.yml
```

### Top-Level Playbook

Write a top-level playbook:

```yml
---

- name: head server
  hosts: head

  roles:
    - role: idiv-biodiversity.systemd_networkd
      tags:
        - systemd
        - systemd-networkd

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv-biodiversity.systemd_networkd
    tags:
      - systemd
      - systemd-networkd

...
```

License
-------

MIT

Author Information
------------------

This role was created in 2019 by [Christian Krause][author] aka [wookietreiber
at GitHub][wookietreiber], HPC cluster systems administrator at the [German
Centre for Integrative Biodiversity Research (iDiv)][idiv].

[author]: https://www.idiv.de/en/groups_and_people/employees/details/61.html
[idiv]: https://www.idiv.de/
[wookietreiber]: https://github.com/wookietreiber
