## Logrotate

![ansible ci](https://github.com/link-u/ansible-roles-v2_logrotate/workflows/ansible%20ci/badge.svg)

## 概要

logrotateの設定用role

## 動作確認バージョン

- Ubuntu 18.04 (bionic)
- ansible >= 2.8
- Jinja2 2.10.3

## 使い方 (ansible)

### Role variables

```yaml
### インストール設定 ###############################################################################
## 基本設定
logrotate_install_flag: True  # インストールフラグ
logrotate_conf_dir: "/etc/logrotate.d/"
logrotate_scripts: []  # ↓に設定例を示す.

### logrotate 設定例 ##############################################################################
## Nginxのデフォルトの設定を記述する例
#logrotate_scripts:
#  - name: nginx
#    paths:
#      - /var/log/nginx/*log
#    options:
#      - daily
#      - missingok
#      - rotate 52
#      - compress
#      - delaycompress
#      - notifempty
#      - create 640 nginx adm
#      - sharedscripts # postrotateをローテート時に1回だけ実行
#    scripts:
#      postrotate: |
#        if [ -f /var/run/nginx.pid ]; then
#          kill -USR1 `cat /var/run/nginx.pid`
#        fi
```

### Example playbook

```yaml
- hosts:
    - servers
  become: True
  roles:
    - { role: logrotate, tags: ["logrotate"] }
```

## License
MIT
