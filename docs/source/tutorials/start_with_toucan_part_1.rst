Start With Toucan part 1
------

In this tutorial, you will learn to mount a Toucan Toco stack (front-end and backend) using Docker in.a dev environment. 

As dev environment we mean local or local server.

Download and install Docker
++++++
Before starting to install Toucan Toco you only need to install Docker. Please refer to the docker `official documentation <https://docs.docker.com/get-docker/>`_

Access requirements
+++++++

All the Toucan Toco Docker images are hosted on the  `official Quay.io registry <https://quay.io/>`_, we don’t use any other registry.

To be able to retrieve and pull the Toucan Toco Docker images, you will need to have access to this registry.

We will hence need your `Quay.io <https:://quay.io>`_ ID to grant you the privileges to do it.

Moreover please give us an email address we could use to inform you about latest releases or security issues.

Launch docker-compose
+++++++
Below is an example of a ``docker-compose.yml`` file - Downloadable `here <link>`_ -::

   version: '3'

   services:
     mongo:
       image: mongo:5.0.3
       expose:
         - "27017"
     redis:
       image: redis:6.2.1-alpine
       expose:
         - "6379"
     backend:
       image: quay.io/toucantoco/backend:latest-monthly
       environment:
         TOUCAN_DB_ENCRYPTION_SECRET: "mySecretTopSecret3"
       depends_on:
         - mongo
         - redis
       ports:
         - "5000:80"
     frontend:
       image: quay.io/toucantoco/frontend:latest-monthly
       environment:
         API_BASEROUTE: http://localhost:5000
       ports:
         - "8000:80"


- Open a terminal

- Run ``docker-compose up`` in the same folder as this file

- Now visit on your frontend url which should be ``localhost:8000``

On the frontend you will have a login page, 

- Log using usermane: ``toucantoco``, password: ``hakunamapikata``

- You will be redirected to the Toucan Toco App Store

Conclusion
+++++
You have built a Toucan Toco stack with a single node mongo and a redis associated in a dev environment using docker-compose with no persistence. 
