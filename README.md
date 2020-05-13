# Ansible Role: Patroni from Zalando

[![Build Status](https://travis-ci.com/yanehi/ansible-role-patroni.svg?branch=master)](https://travis-ci.org/yanehi/ansible-role-patroni)

An Ansible Role that installs Patroni based Postgres with Python on CentOS.

## Requirements

No requirements.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yml
pg_major_version: 12
pg_repo_url: "https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm"
pg_enablerepo: "pgdg12"
```
Set PostgreSQL major version. Patroni works with Open Source PostgreSQL binaries for bootstrapping clusters.

```yml
patroni_data_dir: "/data/patroni"
patroni_home: "/etc/patroni"
patroni_log_dir: "/var/log/pgsql/{{ pg_major_version }}"
pg_bin_path: "/usr/pgsql-{{ pg_major_version }}/bin"
patroni_bin_path: /usr/local/bin/patroni
pg_pass: /var/lib/pgsql/{{ pg_major_version }}
```
Set some directories Patroni will be used for bootstrapping new clusters.

```yml
pg_user: postgres
pg_user_password: postgres
pg_group: postgres
```
Set postgres user. He owns the Patroni based directories and files. 

```yml
pg_patroni_scope: postgres-ha
pg_patroni_namespace: patroni-postgres
```
Set the scope and namespace that all PostgreSQL instances from one Patroni cluster.

```yml
etcd0_ip: 192.168.56.150
etcd1_ip: 192.168.56.151
etcd2_ip: 192.168.56.152
```
Patroni uses etcd `key-value` store for PostgreSQL leader election. Use 3, 5 or 7 etcd instances for `RAFT`.

```yml
pg_port: 5432
etcd_port: 2379
patroni_port: 8008
```
Specify PostgreSQL, etcd connection and Patroni port. Patroni port will be used for health checks of the instances. 

```yml
pg_packages:
  - postgresql{{ pg_major_version }}-server
  - postgresql{{ pg_major_version }}-contrib
  - postgresql{{ pg_major_version }}-libs
```
Required Open Source PostgreSQL packages with binaries for Patroni.

```yml
os_python_packages:
  - net-tools
  - firewalld
  - gcc
  - python3
  - python3-devel
  - python3-pip
```
Install some operating system packages that Patroni needs for Python setup.

```yml
patroni_python_packages:
  - urllib3>=1.24.2
  - boto
  - PyYAML
  - six>=1.7
  - kazoo>=1.3.1
  - python-etcd>=0.4.3,<0.5
  - click>=4.1
  - prettytable>=0.7
  - python-dateutil
  - psutil>=2.0.0
  - cdiff
  - psycopg2-binary>=2.8.4
```
Required Python packages for Patroni.

## License

MIT

## Author Information

This role was created in 2020 by Yannic Nevado.