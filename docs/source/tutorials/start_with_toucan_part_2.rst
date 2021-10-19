In this tutorial, you will learn to mount a Toucan Toco stack (front-end and backend) using Docker in.a dev environment.

As dev environment we mean local or local server.

in a previous tutorial you have learned to deploy a Toucan Toco stack locally with no persistence. 

Here, you will learn how to add persistence on your mongo node and on your backend. 

Without mounting volumes, you will not be able to retrieve your data when doing update or reboot your stack.

Add volumes to your backend
+++++

Start by runing ``docker-compose down`` to stop your docker stack.

Modify your ``docker-compose.yml`` file by adding ``volumes: "path_volume:"``::

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
         TOUCAN_DB_ENCRYPTION_SECRET: "ChangeItForProductionContext"
       depends_on:
         - mongo
         - redis
       ports:
         - "5000:80"
       volumes:
         - "/mnt/data/apps/your_toucan_app:/app/storage"
     frontend:
       image: quay.io/toucantoco/frontend:latest-monthly
       environment:
         API_BASEROUTE: http://localhost:5000
       ports:
         - "8000:80"
         
         
