openwrt-ddns
============

configure ddns aspects of your openwrt system.
compare: [http://wiki.openwrt.org/doc/uci/ddns]

Dependencies
------------

* [openwrt-uci](https://github.com/flandiGT/openwrt-uci)
* python installed (if any package is being to installed)

Role Variables
--------------

| variable name     | type             | description/structure                                | default |
|-------------------|------------------|------------------------------------------------------|---------|
| ddns_services     | array of objects | see attributes below                                 | []      |
| packages          | array of texts   | packages to install (like: 'ddns-scripts_no-ip_com') | []      |

Role Variable elements
----------------------

ddns_services attributes:

| attribute name | property type       | Mandatory? | valid values / examples                                                     |
|----------------|---------------------|------------|-----------------------------------------------------------------------------|
| name           | text                | yes        | custom service name                                                         |
| service_name   | text                | yes        | (like "ddnsprovider.com") - only use names listed in /usr/lib/ddns/services |
| domain         | interval as text    | yes        | domain of the service (like host.yourdomain.net)                            |
| username       | text                | yes        | your username                                                               |
| password       | text                | yes        | your password                                                               |
| interface      | text                | no         | interface on your router (default: 'wan')                                   |
| enabled        | boolean             | no         | enable or disable this service (default: True)                              |
| update_url     | text                | no         | the update url used with placeholders to update the ip (consider documentation of your provider) |

Example Playbook
----------------

```  
 - role: openwrt-ddns
   packages: ['ddns-scripts_no-ip_com']
   ddns_services:
     - name: myddns
       service_name: "ddnsprovider.com"
       domain: "host.yourdomain.net"
       username: "your_user_name"
       password: "p@ssw0rd"
       interface: wan
       enabled: True
```

Official documentation:
* [OpenWRT Wiki / Dynamic DNS Client configuration](http://wiki.openwrt.org/doc/uci/ddns)
* [OpenWRT Wiki / DDNS Client](https://wiki.openwrt.org/doc/howto/ddns.client)
