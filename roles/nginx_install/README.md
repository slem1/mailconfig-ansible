Ansible Role nginx_install
=============================

This role install nginx.

The default server blocks for both ssl and non ssl secured server in /etc/nginx/nginx.conf
are deployed as two separate configuration files in /etc/nginx/conf.d.

ssl server configuration is disabled by default.

Requirements
------------
Tested on Centos 7. Should be ok with any redhat based distribution.

Role Variables
--------------

Playbook example
----------------

```
  roles:
    - role: nginx_install
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
