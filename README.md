Docker Mongo Server Image
=========================
A Docker image for hosting a Mongo server.

Building
--------
Same story, different repo:

    git clone https://github.com/BlueDragonX/docker-mongod.git
    docker build --rm -t bluedragonx/mongod docker-mongod

Running
-------
You can run it as normal and it will start an empty, ephemeral Mongo server:

	docker run -P bluedragonx/mongod

The databases are stored under /data/db. So if you want to keep your data
around it's a good idea to use a volume mount:

	docker run -P -v /tmp/mongod:/data bluedragonx/mongod

Environment variables can be used to change the behavior. MONGOD_REPLSET will
cause Mongo to start in replset mode with the given name. MONGOD_OPTS can be
used to pass additional options to the mongod command:

	docker run -P -e MONGOD_REPLSET=ephemeral -e MONGOD_OPTS="--auth --ipv6" bluedragonx/mongod

Inheriting
----------
The image does not use a config file for Mongo. If you'd like to use one you
can ADD a config file someplace (/etc/mongodb.conf is the default) and set
MONGOD_OPTS='--config /etc/mongodb.conf' in the new Dockerfile.

License
-------
Copyright (c) 2014 Ryan Bourgeois. Licensed under BSD-Modified. See the LICENSE
file for a copy of the license.
