Tags
====

If you have a large playbook it may become useful to be able to run a
specific part of the configuration.  Both plays and tasks support a
"tags:" attribute for this reason.

Example::

    tasks:

        - yum: name={{ item }} state=installed
          with_items:
             - httpd
             - memcached
          tags:
             - packages

        - template: src=templates/src.j2 dest=/etc/foo.conf
          tags:
             - configuration

If you wanted to just run the "configuration" and "packages" part of a very long playbook, you could do this::

    ansible-playbook example.yml --tags "configuration,packages"

You may also apply takes to roles:

    roles:
      - { role: webserver, port: 5000, tags: [ 'web', 'foo' ] }

And you may also tag basic include statements:

    - include: foo.yml tags=web,foo

Both of these have the function of tagging every single task inside the include statement.


