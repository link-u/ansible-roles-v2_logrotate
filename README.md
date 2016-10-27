Logrotate
=========

logrotateの設定用role

Requirements
------------

Ubuntu 16.04

Role Variables
--------------

```yaml
logrotate_conf_dir: "/etc/logrotate.d/"
logrotate_scripts:
  - name: nginx
    paths:
      - /var/log/nginx/*log
    options:
      - daily
      - missingok
      - rotate 52
      - compress
      - delaycompress
      - notifempty
      - create 640 nginx adm
      - sharedscripts # postrotateをローテート時に1回だけ実行
    scripts:
      postrotate: |
        if [ -f /var/run/nginx.pid ]; then
          kill -USR1 `cat /var/run/nginx.pid`
        fi
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: logrotate, tags: ["logrotate"] }

License
-------

BSD

Author Information
------------------

Link-U Inc.
