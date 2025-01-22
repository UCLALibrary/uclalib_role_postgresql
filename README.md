uclalib_role_postgresql
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
  * (default) dnf's default posrgresql stream
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
* `pgsql_encoding`: (string) Encoding for template0
  * (default) UTF8
* `pgsql_locale`: (string) Locale for template0
  * (default) `en_US.UTF-8`

Dependencies
------------

None.

Example Playbook
----------------

    ---
    - hosts: db
      roles:
        - role: uclalib_role_postgresql
          vars:
            pgsql_major_version: '16'
            pgsql_server: true
            pgsql_superuser_password: 'changeme'
          become: true

    - hosts: client
      vars:
        pgsql_host: 'db',
        pgsql_major_version: '16',
        pgsql_name: 'app',
        pgsql_pass: 'changemealso',
        pgsql_user: 'app',

      roles:
        - role: uclalib_role_postgresql
          delegate_to: '{{ pgsql_host }}'
          become: true

License
-------

BSD-2-Clause

Author Information
------------------

John H. Robinson, IV <jhriv@ucla.edu>    
Powell Library    
University of California, Los Angeles
