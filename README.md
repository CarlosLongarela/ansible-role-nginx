Ansible Role: Nginx
=========

[![Build Status](https://travis-ci.org/CarlosLongarela/ansible-role-nginx.svg?branch=master)](https://travis-ci.org/CarlosLongarela/ansible-role-nginx)
[![Percentage of issues still open](http://isitmaintained.com/badge/open/CarlosLongarela/ansible-role-nginx.svg)](http://isitmaintained.com/project/CarlosLongarela/ansible-role-nginx "Percentage of issues still open")
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/CarlosLongarela/ansible-role-nginx.svg)](http://isitmaintained.com/project/CarlosLongarela/ansible-role-nginx "Average time to resolve an issue")

Nginx installation and configuration with virtual hosts, http2 and nginx cache/purge.

Requirements
------------

None.

Role Variables
--------------

    nginx_nombre_servicio: nginx
    nginx_ejecutable: nginx
    nginx_conf_dir: "/etc/nginx"
    nginx_user: www-data
    nginx_group: www-data
    nginx_pidfile: /run/nginx.pid

    php_version: 7.1
    php_fpm_pool_listen: "/run/php/php{{ php_version }}-fpm.sock"

    # PONER IGUAL AL NÚMERO DE PROCESADORES DE LA MÁQUINA
    nginx_worker_processes: 2
    nginx_worker_connections: "1024"
    nginx_multi_accept: "off"

    nginx_sendfile: "on"
    nginx_tcp_nopush: "on"
    nginx_tcp_nodelay: "on"
    nginx_keepalive_timeout: "65"
    nginx_types_hash_max_size: "2048"
    nginx_server_tokens: "off"

    nginx_extra_http_options: ""
    # Ejemplo de opciones extra del bloque http:
    #    nginx_extra_http_options: |
    #      proxy_buffering    off;
    #      proxy_set_header   X-Real-IP $remote_addr;
    #      proxy_set_header   X-Scheme $scheme;
    #      proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    #      proxy_set_header   Host $http_host;

    nginx_vhosts_root: "/home/webs"

    nginx_vhosts: {}
    # Ejemplo de opciones de vhosts
    #  tabernawp:
    #    default_server: true # Sólo debe existir uno como default server
    #    activado: true
    #    archivo_conf: "tabernawp.com.conf"
    #    dominio: "tabernawp.com"
    #    dominio_dir_cerbot: "tabernawp.com"
    #    sin_www:  true
    #    ssl: true
    #    cache_nginx: true
    #    fcgi_cache_path: "/var/run/nginx-cache"
    #    fcgi_levels: "1:2"
    #    fcgi_keys_zone_name: "WEBWP"
    #    fcgi_keys_zone_size: "100m"
    #    fcgi_inactive: "10h"
    #    fcgi_cache_valid: "6h"
    #    cms: wordpress
    #    root: "{{ nginx_vhosts_root }}/tabernawp.com/public"
    #    index: "index.html index.htm index.php"
    #  tabernawp2:
    #    default_server: false
    #    activado: true
    #    archivo_conf: "tabernawp2.com.conf"
    #    dominio: "tabernawp2.com"
    #    dominio_dir_cerbot: "www.tabernawp2.com"
    #    sin_www:  true
    #    ssl: true
    #    cache_nginx: false
    #    cms: prestashop
    #    prestashop_admin: admin123
    #    root: "{{ nginx_vhosts_root }}/tabernawp2.com/public"
    #    index: "index.html index.htm index.php"

    nginx_vhosts_activados: []
    # Lista de hosts activados
    #  - tabernawp.com.conf
    #  - tabernawp2.com.conf

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers

      gather_facts: no
      become: true

      vars:
        nginx_vhosts_root: "/home/webs"

        nginx_vhosts:
          tabernawp:
            default_server: true # Sólo debe existir uno como default server
            activado: true
            archivo_conf: "tabernawp.com.conf"
            dominio: "tabernawp.com"
            sin_www:  true
            ssl: true
            cache_nginx: true
            fcgi_cache_path: "/var/run/nginx-cache"
            fcgi_levels: "1:2"
            fcgi_keys_zone_name: "WEBWP"
            fcgi_keys_zone_size: "100m"
            fcgi_inactive: "10h"
            fcgi_cache_valid: "6h"
            cms: wordpress
            root: "{{ nginx_vhosts_root }}/tabernawp.com/public"
            index: "index.html index.htm index.php"

        nginx_vhosts_activados:
          - tabernawp.com.conf

      roles:
         - { role: CarlosLongarela.nginx }

License
-------

GPLv2

Author Information
------------------

This role was created in 2017, May by [Carlos Longarela](mailto:carlos@longarela.eu), from [Taberna WordPress](https://tabernawp.com/).
