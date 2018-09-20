TeamCity Server
=========

[![Build Status](https://travis-ci.org/matisku/ansible-teamcity-server.svg?branch=master)](https://travis-ci.org/matisku/ansible-teamcity-server)

This role will install and configure TemCity Server - CI tool from JetBrains.
I created this role because I needed to have a fully automated TeamCity setup.

This role will:
1. Install TeamCity
2. Setup database connection (local/mysql)
3. Setup TeamCity default admin user - `teamcity`
4. Accept license automatically
5. Start Teamcity Server at port 8111

As a result, this role will setup fully working TeamCity Server.
Feel free to use it along with my TeamCity Agent role - [matisku.teamcity-agent](https://github.com/matisku/ansible-teamcity-agent).

## Compatibility
This role is compatible with Ubuntu 16.04 and Ubuntu 18.04

## Requirements
1. [ansiblebit.oracle-java](https://github.com/ansiblebit/oracle-java) - Java is required on TeamCity Server

## Role Variables
| Variable name                           | Default value                                                      | Description                      |
|-----------------------------------------|--------------------------------------------------------------------|----------------------------------|
| teamcity_server_version                 | `2018.1.2`                                                         | TeamCity version to install      |
| teamcity_server_sha256                  | `cd441b28c7603f9ad2dbd27ae5e35b035dfb90b7a77b7d327c278d71289af942` | sha256 for TeamCity package      |
| teamcity_server_su_user                 | `teamcity`                                                         | Admin user name for TeamCity     |
| teamcity_server_su_password             | `teamcity`                                                         | Admin user password for TeamCity |
| teamcity_server_install_dir             | `/opt`                                                             | TeamCity unpack dir              |
| teamcity_server_dir                     | `{{ teamcity_server_install_dir }}/TeamCity`                       | TeamCity install dir             |
| teamcity_server_data_dir                | `{{ teamcity_server_dir }}/BuildServer`                            | TeamCity data/conf/plugins dir   |
| teamcity_server_plugins_dir             | `{{ teamcity_server_data_dir }}/plugins`                           | TeamCity plugins dir             |
| teamcity_server_license_keys            | `[]`                                                               | List of TeamCity Licenses        |
| teamcity_server_mysql_connector_version | `8.0.12`                                                           | MySQL connector version          |
| teamcity_server_mysql_connector_dir     | `/opt/mysql-connector`                                             | MySQL connector install dir      |
| teamcity_server_mysql_db_user           | `teamcity`                                                         | TeamCity MySQL user name         |
| teamcity_server_mysql_db_password       | `teamcity`                                                         | TeamCity MySQL user password     |
| teamcity_server_mysql_db_name           | `teamcity`                                                         | TeamCity MySQL database          |
| teamcity_server_db_type                 | `local`                                                            | Database version: local or mysql |
| teamcity_server_mysql_database_url      | `localhost`                                                        | MySQL database URL               |
| teamcity_server_mysql_database_port     | `3306`                                                             | MySQL database port              |
| teamcity_server_mysql_jdbc_dir          | `{{ teamcity_server_data_dir }}/lib/jdbc`                          | MySQL JDBC driver location       |

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
