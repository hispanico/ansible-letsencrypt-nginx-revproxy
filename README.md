ansible-letsencrypt-nginx-revproxy
=========
[![Build Status](https://img.shields.io/travis/hispanico/ansible-letsencrypt-nginx-revproxy.svg?style=flat-square)](https://travis-ci.org/hispanico/ansible-letsencrypt-nginx-revproxy)
[![Galaxy](https://img.shields.io/badge/galaxy-hispanico.letsencrypt--nginx--revproxy-blue.svg?style=flat-square)](https://galaxy.ansible.com/hispanico/letsencrypt-nginx-revproxy/)

Configures Nginx as reverse proxy for multiple website with Let's Encrypt certificate.

Requirements
------------

This role requires Ansible 1.9 or higher.

Role Variables
--------------

Default values:

```yaml
nginx_revproxy_sites:                                         # List of sites to reverse proxy
  example.com:                                                # Domain name
    domains:                                                  # List of server_name aliases
      - example.com
      - www.example.com
    upstreams:                                                # List of Upstreams
      - { backend_address: 192.168.0.100, backend_port: 80 }
      - { backend_address: 192.168.0.101, backend_port: 8080 }
    letsencrypt: true                                        # Set to True if you are using hispanico.letsencrypt role
    letsencrypt_email: 'contatti@ninux.org'
```

Dependencies
------------

* [hispanico.nginx-revproxy](https://galaxy.ansible.com/hispanico/nginx-revproxy)

Example Playbook
----------------

This esample configure nginx as reverse proxy for the following sites:
  * example.org with selfsign ssl certificate
  * example.com ssl certificate generate via let's encrypt ACME protocol.

```yaml
  - hosts: all
    roles:
      - ansible-nginx-revproxy
      - ansible-letsencrypt-nginx-revproxy
    vars:
      nginx_revproxy_sites:
        example.org:
          domains:
            - example.org
            - www.example.org
          upstreams:
            - { backend_address: 192.168.0.200, backend_port: 80 }
            - { backend_address: 192.168.0.201, backend_port: 80 }
          letsencrypt: false

        example.com:
          domains:
            - example.com
            - www.example.com
          upstreams:
            - { backend_address: 192.168.0.100, backend_port: 80 }
            - { backend_address: 192.168.0.101, backend_port: 80 }
          letsencrypt: true
```

License
-------

Licensed under the GPLv3 License. See the LICENSE file for details.

Author Information
------------------

Hispanico
