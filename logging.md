# System administration: Logging

DRIVER2.0 is composed of a number of separate services; all of these services must be operating in
order for DRIVER to work properly. In order to diagnose potential problems with the system, it may
be necessary to use log files on the system to view output from these services.

Execute the below command to get a list of the docker containers with their id’s

```sudo docker ps -a```

## Database (PostgreSQL)
Database host

`sudo docker logs {database_container_id}`

## Cache (Redis)
Database host

`sudo docker logs {redis_container_id}`

## Tile server (Windshaft)
App host

`sudo docker logs {windshaft_container_id}`

## Web proxy (Nginx)
App host

- `/var/log/nginx/driver-app.access.log` (log rotation appends `.1`, `.2`, etc.)
- `/var/log/nginx/error.log` (log rotation as above)

## Web application (Django)
App host

`sudo docker logs {django_container_id}`

## File download server (Nginx)
Celery host

Paths:
- `/var/log/nginx/driver-celery.access.log` (log rotation appends `.1`, `.2`, etc)
- `/var/log/nginx/error.log` (log rotation as above)

## Asynchronous jobs (Celery)
This includes CSV exports and other asynchronous tasks triggered by the web UI and/or Android application. Celery host.

`Sudo docker logs {celery_container_id}`
