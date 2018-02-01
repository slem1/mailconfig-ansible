Ansible Role roundcube_deploy
==============================

This role deploy a default roundcube webmail installation in nginx installation.

Requirements
------------

Nginx should be installed and php_fastcgi configured. See roles:
  - nginx_install
  - nginx_php

Role Variables
--------------

**deploy_repo**: Host directory where the roundcube installer will be downloaded

**roundcube_sha256**: sha256 checksum of the roundcube installer (see official roundcube website)

**roundcube_name**: canonical name + version of roundcube. eg: roundcubemail-1.3.3

**roundcube_archive**: roundcuble fullname installer

**roundcube_url**: roundcube download url

**roundcube_install**: Target roundcube installation directory. eg: /var/www/html or /usr/share/nginx/html/

**nginx_vhost_conf_dir**: the nginx vhost ".d" configuration directory where the php_fastcgi inclusion should be installed.

**roundcube_config_datasource**: connection string for the roundcube database. This installation use an sqlite db.

**roundcube_config_des_key**: DES key for roundcube exchange encryption


Playbook example
----------------

```
  - role: roundcube_deploy

      deploy_repo: "/home/deploy/repo/"      
      roundcube_name: "roundcubemail-1.3.3"
      roundcube_archive: "{{ roundcube_name }}-complete.tar.gz"
      roundcube_sha256: "sha256:05d9856c966c0d93accabf724e7ff2fd493bba1a57c44247ed0a2aacd617c879"      
      roundcube_url: "https://github.com/roundcube/roundcubemail/releases/download/1.3.3/{{ roundcube_archive }}"      
      roundcube_install: "/usr/share/nginx/html/webmail"      
      roundcube_config_datasource: sqlite:////usr/share/nginx/html/webmail/roundcubemail.db?mode=0646      
      roundcube_config_des_key: K0KI1FLepBiM43uituuinwC3
      nginx_vhost_conf_dir: /etc/nginx/default.d
```

License
-------

```
Copyright 2014 Google Inc. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
