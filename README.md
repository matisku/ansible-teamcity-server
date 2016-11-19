# TeamCity Server
=========
[![Build Status](https://travis-ci.org/matisku/ansible-teamcity-server.svg?branch=master)](https://travis-ci.org/matisku/ansible-teamcity-server)

This role will install and configure TemCity Server - CI tool from Jetbrains.

## Requirements
----------------

1. [ansiblebit.oracle-java](https://github.com/ansiblebit/oracle-java)

## Role Variables
----------------

| Variable name                                  | Default value                                                      | Description                      |
|------------------------------------------------|--------------------------------------------------------------------|----------------------------------|
| teamcity_server_version                        | `10.0.2`                                                           | TeamCity version to install      |
| teamcity_server_sha256                         | `35abb03ed176c8326adc86cac17a93412c7248277d9aae422b89be17edff8f97` | sha256 for TeamCity package      |
| teamcity_server_su_user                        | `teamcity`                                                         | Admin user name for TeamCity     |
| teamcity_server_su_password                    | `teamcity`                                                         | Admin user password for TeamCity |
| teamcity_server_install_dir                    | `/opt`                                                             | TeamCity unpack dir              |
| teamcity_server_dir                            | `{{ teamcity_server_install_dir }}/TeamCity`                       | TeamCity install dir             |
| teamcity_server_data_dir                       | `{{ teamcity_server_dir }}/BuildServer`                            | TeamCity data/conf/plugins dir   |
| teamcity_server_plugins_dir                    | `{{ teamcity_server_data_dir }}/plugins`                           | TeamCity plugins dir             |
| teamcity_server_mysql_server_connector_version | `5.1.40`                                                           | MySQL connector version          |
| teamcity_server_mysql_connector_dir            | `/opt/mysql-connector`                                             | MySQL connector install dir      |
| teamcity_server_mysql_server_db_user           | `teamcity`                                                         | TeamCity MySQL user name         |
| teamcity_server_mysql_server_db_password       | `teamcity`                                                         | TeamCity MySQL user password     |
| teamcity_server_mysql_server_db_name           | `teamcity`                                                         | TeamCity MySQL database          |
| teamcity_server_db_type                        | `local`                                                            | Database version: local or mysql |
| teamcity_server_mysql_server_database_url      | `localhost`                                                        | MySQL database URL               |
| teamcity_server_mysql_server_database_port     | `3306`                                                             | MySQL database port              |
| teamcity_server_mysql_server_jdbc_dir          | `{{ teamcity_server_data_dir }}/lib/jdbc`                          | MySQL JDBC driver location       |

## Dependencies
----------------

This role depends on java role.

## Example Playbook
----------------

Example playbook:

```yaml
- hosts: teamcity-server
  roles:
    - teamcity-server
```

## Author Information
----------------

This role was created in 2016 by Mateusz Trojak.

This role was created for [Brainly](http://www.brainly.com) to be used for company CI automation with easy failover mechanism.
