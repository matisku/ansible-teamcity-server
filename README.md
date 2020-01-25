TeamCity Server
=========

[![Build Status](https://travis-ci.org/matisku/ansible-teamcity-server.svg?branch=master)](https://travis-ci.org/matisku/ansible-teamcity-server)

This role will install and configure TemCity Server - CI tool from JetBrains.
I created this role because I needed to have a fully automated TeamCity setup.

This role will:
1. Install TeamCity
2. Setup database connection (local/mysql)
3. Setup TeamCity default admin user - `teamcity`
4. Accept license

As a result, this role will setup fully working TeamCity Server.
Feel free to use it along with my TeamCity Agent role - [matisku.teamcity-agent](https://github.com/matisku/ansible-teamcity-agent).

## Compatibility
This role is compatible with Ubuntu 14.04 and Ubuntu 16.04

## Requirements
1. [lean_delivery.java](https://github.com/lean-delivery/ansible-role-java) - Java is required on TeamCity Server

## Role Variables
| Variable name                           | Default value                                                      | Description                      |
|-----------------------------------------|--------------------------------------------------------------------|----------------------------------|
| teamcity_server_version                 | `2019.2.1`                                                         | TeamCity version to install      |
| teamcity_server_sha256                  | `ab74aa6caa6ea0eebbc02af28521474cf610a7b43d502125c5469240325cdf42` | sha256 for TeamCity package      |
| teamcity_server_su_user                 | `teamcity`                                                         | Admin user name for TeamCity     |
| teamcity_server_su_password             | `teamcity`                                                         | Admin user password for TeamCity |
| teamcity_server_install_dir             | `/opt`                                                             | TeamCity unpack dir              |
| teamcity_server_dir                     | `{{ teamcity_server_install_dir }}/TeamCity`                       | TeamCity install dir             |
| teamcity_server_data_dir                | `{{ teamcity_server_dir }}/BuildServer`                            | TeamCity data/conf/plugins dir   |
| teamcity_server_plugins_dir             | `{{ teamcity_server_data_dir }}/plugins`                           | TeamCity plugins dir             |
| teamcity_server_license_keys            | `[]`                                                               | List of TeamCity Licenses        |
| teamcity_server_mysql_connector_version | `5.1.40`                                                           | MySQL connector version          |
| teamcity_server_mysql_connector_dir     | `/opt/mysql-connector`                                             | MySQL connector install dir      |
| teamcity_server_mysql_db_user           | `teamcity`                                                         | TeamCity MySQL user name         |
| teamcity_server_mysql_db_password       | `teamcity`                                                         | TeamCity MySQL user password     |
| teamcity_server_mysql_db_name           | `teamcity`                                                         | TeamCity MySQL database          |
| teamcity_server_db_type                 | `local`                                                            | Database version: local, mysql or postgresql |
| teamcity_server_mysql_database_url      | `localhost`                                                        | MySQL database URL               |
| teamcity_server_mysql_database_port     | `3306`                                                             | MySQL database port              |
| teamcity_server_jdbc_dir                | `{{ teamcity_server_data_dir }}/lib/jdbc`                          | MySQL JDBC driver location       |

## Setting up for Postgres
Set the variable `teamcity_server_db_type` to `postgres`.

Make sure that you set the correct variables for Postgres

```yaml
teamcity_db:
  - host: "localhost"
  - name: "teamcity"
  - user: "teamcity"
  - pass: "teamcity"
  - port: 5432
```

## nginx Proxy
Set the following variables. If `teamcity_nginx.proxy` is set to false, nginx will not be configured.
```yaml
teamcity_hostname: teamcity.example.org

teamcity_nginx:
  - proxy: false
  - config_path: /etc/nginx/conf.d/teamcity.conf
  - hostname: "{{ teamcity_hostname }}"
  - ssl:
      - configure: false
      - cert: /etc/letsencrypt/live/{{ teamcity_hostname }}/fullchain.pem
      - key:  /etc/letsencrypt/live/{{ teamcity_hostname }}/privkey.pem
  - port: 443
```

## Dependencies
This role depends on `java` role. 

## Example Playbook
Example playbook:

```yaml
- hosts: teamcity-servers
  become: yes 
  roles:
    - matisku.teamcity-server
```

## Author Information
This role was created by Mateusz Trojak for [Brainly](http://www.brainly.com).
We are using this role for company CI automation with easy failover mechanism.

## License
Copyright © 2016-2018 Mateusz Trojak. See LICENSE for details.
