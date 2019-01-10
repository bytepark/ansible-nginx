[![Build Status](https://travis-ci.org/bytepark/ansible-nginx.svg?branch=master)](https://travis-ci.org/bytepark/ansible-nginx)

ansible-nginx
=========

Ansible role to install and configure NGINX

Requirements
------------

No further requirements besides bash.

Role Variables
--------------
Variable defaults

```
# repo url - either deb or ppa (e.g "ppa:bytepark/nginx-mainline")
nginx_repo: "deb https://nginx.org/packages/ubuntu/ bionic nginx"
# repo key - when repo needs signing key (e.g. http://nginx.org/keys/nginx_signing.key) 
nginx_repo_key: ""
# package name to install (can allso be nginx-full e.g)
nginx_package: "nginx"

# optional config in nginx.conf
nginx_extra_conf_options: ""
# optional config in nginx.conf http block
nginx_extra_http_options: ""

# list of vhosts with following keys
#   type                        - static/fastcgi/proxy - which type to use
#   hostname                    - main server name
#   additional_server_names     - alias domains
#   is_default                  - whether this vhost is the default listener
#   docroot                     - document root for vhost
#   logfile_separate            - true/false - for separate log file for this vhost
#   logfile_format              - name of a different logfile format defined in nginx.conf 
#   enable_ssl                  - true/false - whether to enable SSL
#   cache_enable                - true/false - whether to enable caching (fastcgi/proxy only)
#   cache_time                  - e.g. 30s - how long to cache valid responses
#   enable_websocket            - true/false - for proxy setups, enable websocket listening
#   naxsi_enable                - true/false - whether to include NAXSI WAF
#   naxsi_mode_learning         - true/false - whether to enable learningmode
#   naxsi_denied_url            - url for cases of denied requests
#   extra_server_options        - extra nginx server conf options
#                                 Example:
#                                   extra_server_options: |
#                                     include /etc/nginx/y.conf;
#                                     include /etc/nginx/x.conf;
nginx_vhosts: []

#   nginx_ssl_type              - modern/intermediate - cipher config from mozilla server configurator
nginx_ssl_type: "modern"
#   nginx_enable_hsts           - whether to enable HSTS
nginx_enable_hsts: false        

nginx_dhparam_path: "/etc/ssl/dhparam.pem"
nginx_dhparam_encryption_size: 2048

nginx_naxsi_enable:             - true/false
nginx_naxsi_rules_file: "https://raw.githubusercontent.com/nbs-system/naxsi/master/naxsi_config/naxsi_core.rules"
```

Dependencies
------------

No dependencies.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: bytepark.nginx }

License
-------

MIT

Author Information
------------------

bytepark / 2018.
