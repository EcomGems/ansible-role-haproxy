# Ansible Role: HAProxy

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-haproxy.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-haproxy)

Installs HAProxy on RedHat/CentOS and Debian/Ubuntu Linux servers.

**Note**: This role _officially_ supports HAProxy versions 1.4 or 1.5. Future versions may require some rework.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    haproxy_socket: /var/lib/haproxy/stats

The socket through which HAProxy can communicate (for admin purposes or statistics). To disable/remove this directive, set `haproxy_socket: ''` (an empty string).

    haproxy_chroot: /var/lib/haproxy

The jail directory where chroot() will be performed before dropping privileges. To disable/remove this directive, set `haproxy_chroot: ''` (an empty string). Only change this if you know what you're doing!

    haproxy_user: haproxy
    haproxy_group: haproxy

The user and group under which HAProxy should run. Only change this if you know what you're doing!

    haproxy_frontend_name: 'hafrontend'
    haproxy_frontend_bind_address: '*'
    haproxy_frontend_port: 80
    haproxy_frontend_mode: 'http'

HAProxy frontend configuration directives.

    haproxy_backend_name: 'habackend'
    haproxy_backend_mode: 'http'
    haproxy_backend_balance_method: 'roundrobin'
    haproxy_backend_httpchk: 'HEAD / HTTP/1.1\r\nHost:localhost'

HAProxy backend configuration directives.

    haproxy_backend_servers:
      - name: app1
        address: 192.168.0.1:80
      - name: app2
        address: 192.168.0.2:80

A list of backend servers (name and address) to which HAProxy will distribute requests.

    haproxy_frontend_ssl_port: 443

The port on which to listen for SSL based traffic.

    haproxy_ssl_pem: '/path/to/pem/file'

The full path to the PEM (key + cert) file to use for SSL termination.

    haproxy_backend_hash_type: 'map-based'

The backend hashing strategy to use.  See [HAProxy hash-type](http://cbonte.github.io/haproxy-dconv/1.7/configuration.html#4.2-hash-type)

    haproxy_backend_group: false
    haproxy_backend_group_port: 9000

A list of grouped backend servers and destination ports to forward traffic to.  This can be used in addition to or in lieu of haproxy_backend_servers.

## Dependencies

None.

## Example Playbook

    - hosts: balancer
      sudo: yes
      roles:
        - { role: geerlingguy.haproxy }

## License

MIT / BSD

## Author Information

This role was created in 2015 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
