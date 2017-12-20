# Overview
Sample scripts to deploy PostgreSQL to Mesosphere DC/OS with Local Persistent Storage enabled.

# Steps
** Replace kojiha/postgres_test with your own tag.


(1) build a container image
```
docker build -t kojiha/postgres_test .
```


(2) push the image to your container registry
```
docker login
docker push kojiha/postgres_test
```


(3) modify marathon.json for your environment

Customization points are:

- `docker.image`
- `container.volumes.containerPath` and `env.PGDATA`
- `container.volumes.persistent.size`
- `container.volumes.persistent.type`
- add `POSTGRES_USER`, `POSTGRES_PASSWORD` in `env` as you need

At least you must modify `docker.image` for your image location.  


(4) deploy the image to DC/OS via marathon
```
dcos marathon app add marathon.json
```
or put the marathon.json content into JSON CONFIGUFATION text area of DC/OS 'Run a Service' UI.


(5) verify if the service is running with a volume attached


# Comments

* `container.volumes.containerPath` may not contain any slashes

* The environment variable `PGDATA` must have a path `/mnt/mesos/sandbox/` + the value set in `container.volumes.containerPath`

