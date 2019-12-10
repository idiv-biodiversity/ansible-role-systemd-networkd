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

None.

Role Variables
--------------

**Note:** This does not yet support the full complexity. If you are missing
something, pull requests are welcome!

```yml
systemd_networkd_networks:
  - name: wired
    match:
      name: en*
    network:
      dhcp: ipv4
      llmnr: 'no'
      domains:
        - example.com
      ntp:
        - 1.pool.example.com
        - 2.pool.example.com
        - 3.pool.example.com
        - 4.pool.example.com
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

[author]: https://www.idiv.de/groups_and_people/employees/details/eshow/krause-christian.html
[idiv]: https://www.idiv.de/
[wookietreiber]: https://github.com/wookietreiber
