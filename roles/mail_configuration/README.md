Ansible Role mail_configuration
=============================

Requirements
------------
Tested on Centos 7. Should be ok with any redhat based distribution.

Role Variables
--------------

mail_user : The linux system account for retrieving mail
dovecot_mail_user_password : The imap password to access the mail_user inbox

postfix_myhostname: postfix's main.cf myhostname value
postfix_mydomain: postfix's main.cf mydomain value

virtual_alias_domains: virtual domain for which postfix should handle email eg gmail.com mycompany.com
virtual_alias_domains_mappings: mapping from email addresses to user (usually the mail_user account)

Playbook example
----------------

The following playbook does:
- the creation of the mail_user system account.
- the postfix and dovecot localhost configuration.

```
  roles:
    - role: mail_configuration
      mail_user: mailuser
      dovecot_mail_user_password: mailuser
      postfix_myhostname: localhost
      postfix_mydomain: localdomain
      virtual_alias_domains: mycompany.com gmail.com
      virtual_alias_domains_mappings: ['@mycompany.com', '@gmail.com']
```

Verify installation
----------------

#### postfix

on the host,

```shell
echo "hello" | mail -s "postfix alias mapping test" bruce.wayne@mycompany.com
```

```shell
sudo tail /var/log/maillog
```

You should found the kind of following log line:

```shell
Jan 29 13:14:51 XXXX postfix/local[10663]: DEA8B108A405: to=<mailuser@localhost.localdomain>, orig_to=<bruce.wayne@mycompany.com>, relay=local, delay=0.04, delays=0.02/0.01/0/0
, dsn=2.0.0, status=sent (delivered to mailbox)
```

and mail content could be read from :

```shell
sudo less /var/mail/mailuser
```

#### dovecot

on the host,

Open a telnet on localhost:143

```
telnet localhost 143
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
* OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE STARTTLS AUTH=PLAIN] Dovecot ready.
```

Check login:
```
a login mailuser mailuser
a OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHI
LDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS SPECIAL-USE BINARY MOVE] Logged in
```

Check Inbox access for logged user:
```
b select INBOX
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 852 EXISTS
* 0 RECENT
* OK [UNSEEN 400] First unseen.
* OK [UIDVALIDITY 1513786247] UIDs valid
* OK [UIDNEXT 1048] Predicted next UID
b OK [READ-WRITE] Select completed (0.000 secs).
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
