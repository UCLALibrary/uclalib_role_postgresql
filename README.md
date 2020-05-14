Role Name
=========

PostgreSQL Client / Server for UCLA Library

Installs PostgreSQL client, dependencies.

Optionally creates PostgreSQL user and database, adjusting `pg_hba.conf` on the server if required.

Optionally installs PostgreSQL server, setting `pg_hba.conf` to allow access when role+database name matches, from the same network.

Requirements
------------

None.

Role Variables
--------------

* `pgsql_major_version`: (string)
  * (default) If unset, will use CentOS/RHEL packaged version
  * If set, will use PGDG
* `pgsql_server`: (boolean)
  * (default) false: Install client
  * true: Install client and server
* `pgsql_host`: (string)
  * (default) localhost
  * Hostname of server client should connect to

### Client Specific

* `pgsql_user`: PostgreSQL user
  * (default) omit
* `pgsql_pass`: PostgreSQL password
  * (default) omit
* `pgsql_name`: PostgreSQL database name
  * (default) omit

### Server Specific

* `pgsql_superuser_password`: (string) PostgreSQL superuser password
  * (default) omit

Dependencies
------------

None.

Example Playbook
----------------


    - hosts: db
      roles:
         - {
              role: uclalib_role_postgresql,  
              pgsql_major_version: '12',
              pgsql_server: true,
              pgsql_superuser_password: 'changeme',
            }

    - hosts: client
      roles:
        - {
            role: uclalib_role_postgresql,
            pgsql_major_version: '12',
            pgsql_host: 'db',
            pgsql_name: 'app',
            pgsql_user: 'app',
            pgsql_pass: 'changemealso',
        }

License
-------

BSD-2-Clause

Author Information
------------------

John H. Robinson, IV <jhriv@ucla.edu>
Powell Library
University of California, Los Angeles
