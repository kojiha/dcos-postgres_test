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

At least you must modify docker.image for your image location.



(4) deploy the image to DC/OS via marathon
```
dcos marathon app add marathon.json
```
or put the marathon.json content into JSON CONFIGUFATION text area of DC/OS 'Run a Service' UI.


(5) verify if the service is running with a volume attached