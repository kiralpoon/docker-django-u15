# docker-django
A simple Django application using my own memcached and ubunutu 15 images


RUN
------
	$ docker-compose up
	or
	$ docker-compose up -d #deattach mode
	$ docker-compose ps
	# To SEE LOG
	$ docker-compose log
	# TO STOP
	$ docker-compose down

TO MAKE LOGIN WORKS WHILE IT IS RUNNING
-------------------
	# Either in detach mode or new terminal
	$ docker-compose run django python django-example/manage.py migrate

	OR

	$ docker ps
	CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                    NAMES
	8d6b0db2b7ed        dockerdjangou15_django       "gunicorn -c gunicorn"   40 seconds ago      Up 39 seconds       0.0.0.0:8000->8000/tcp   dockerdjangou15_django_1
	a40c671ec54e        postgres:9.3                 "/docker-entrypoint.s"   41 seconds ago      Up 40 seconds       5432/tcp                 dockerdjangou15_postgres_1
	9a5ad85fb6fd        kiralpoon/memcached:latest   "/usr/bin/memcached -"   42 seconds ago      Up 41 seconds       11211/tcp                dockerdjangou15_memcached_1

	$ docker exec -i -t dockerdjangou15_django_1 /bin/bash

	root@8d6b0db2b7ed:/usr/src/app# ls  
	CONTRIBUTORS.txt  Dockerfile  Gruntfile.js  LICENSE  Procfile  README.md  django-example  docker-compose.yml  docs  gunicorn_conf.py  package.json  requirements.txt  setup.cfg  setup.py
	root@8d6b0db2b7ed:/usr/src/app# cd django-example/
	root@8d6b0db2b7ed:/usr/src/app/django-example# ls 
	__init__.py  config  contrib  manage.py  static  templates  urls.py  urls.pyc  users  wsgi.py  wsgi.pyc
	root@8d6b0db2b7ed:/usr/src/app/django-example# python manage.py migrate
	Operations to perform:
	  Synchronize unmigrated apps: account, allauth, debug_toolbar, avatar, crispy_forms, socialaccount
	  Apply all migrations: users, sessions, admin, sites, auth, contenttypes
	Synchronizing apps without migrations:
	  Creating tables...
	    Creating table avatar_avatar
	    Creating table account_emailaddress
	    Creating table account_emailconfirmation
	    Creating table socialaccount_socialapp_sites
	    Creating table socialaccount_socialapp
	    Creating table socialaccount_socialaccount
	    Creating table socialaccount_socialtoken
	  Installing custom SQL...
	  Installing indexes...
	Running migrations:
	  Applying contenttypes.0001_initial... OK
	  Applying auth.0001_initial... OK
	  Applying users.0001_initial... OK
	  Applying admin.0001_initial... OK
	  Applying sessions.0001_initial... OK
	  Applying sites.0001_initial... OK
	  Applying sites.0002_set_site_domain_and_name... OK

