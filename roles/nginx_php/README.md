Ansible Role nginx_php
=============================

This role deploys all the required php dependencies and php_fastcgi configuration for nginx.

The php_fastcgi configuration will be deployed in /etc/nginx/php_fastcgi so it could be included by any of server blocks definition in /etc/nginx/conf.d/

Requirements
------------
Tested on Centos 7. Should be ok with any redhat based distribution.

Role Variables
--------------

Playbook example
----------------

```
  roles:
    - role: nginx_php
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
