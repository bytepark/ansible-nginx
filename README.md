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

# number of nginx worker connections
nginx_worker_connections: 1024
# number of nginx worker processes 
nginx_worker_processes: 2
# hash bucket size
nginx_server_names_hash_bucket_size: 64

# upload custom files to reference later. files can be in "files/" directory in your project
nginx_extra_files: []

# list of vhosts with following keys
#   type                        - static/fastcgi/proxy - which type to use
#   hostname                    - main server name
#   additional_server_names     - alias domains
#   is_default                  - whether this vhost is the default listener
#   default_redirect_to         - where to redirect all requests to
#   docroot                     - document root for vhost
#   docroot_fastcgi             - optional document root for fastcgi php location
#   logfile_separate            - true/false - for separate log file for this vhost
#   logfile_format              - name of a different logfile format defined in nginx.conf 
#   enable_ssl                  - true/false - whether to enable SSL
#   ssl_certificate             - location of SSL cert
#   ssl_certificate_key         - location of SSL key
#   ssl_trusted_certificate     - location of SSL trusted chain certs
#   disable_try_files           - don't add a predefined try_files directive to location
#   auth                        - passwort used for htpasswd
#   auth_basic_file             - path of the basic auth file
#   auth_satisfy                - satisfy mode used for authentication (any/all)
#   auth_allowed_ips            - list of allowed ips
#   cache_enable                - true/false - whether to enable caching (fastcgi/proxy only)
#   cache_time                  - e.g. 30s - how long to cache valid responses
#   cache_types                 - dicts with entries code and time for individual caching times
#   proxy_headers               - dicts with entries key and value for individual proxy_headers
#   enable_websocket            - true/false - for proxy setups, enable websocket listening
#   naxsi_enable                - true/false - whether to include NAXSI WAF
#   naxsi_mode_learning         - true/false - whether to enable learningmode
#   naxsi_denied_url            - url for cases of denied requests
#   naxsi_whitelist_file        - path for a naxsi whitelist file
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
