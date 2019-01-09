# Kartoza Django Base Image

A base image for django projects.

This is a base image for django projects. It is based on the 
python base image (which in turn is based on debian). 

This image makes some other assumptions in particular:

* nodejs / npm / yuglify are installed to compress django resources
* uwsgi runs on port 8080
* uwsgi is set up to serve the django project out of /home/web/django_project
* the WORKDIR will be set to /home/web/django_project
* uwsgi will serve up static resources from /home/web/django_project/static
* uwsgi will serve up media resources from /home/web/django_project/media
* Your project is mounted into /home/web/django_project from a docker volume


**NOTE:** Django itself is not installed in this image - you must add it in your
REQUIREMENTS.txt file.

# Getting the image

There are several ways to get the image onto your system:

## Use the docker repository:

This will consume the most bandwidth for the initial build but 
will be easy to update thereafter. 

```
docker pull kartoza/django-base
```

## Build with no local checkout


to build the image without checking out the build repo do:

```
docker build -t kartoza/django-base git://github.com/timlinux/docker-django-base
```

## Build locally or with locally checked out code

```
git clone git://github.com/timlinux/docker-django-base
docker build -t kartoza/django-base .
```

# Usage

You should use the FROM directive in your Dockerfile to inherit from this file
and then install your requirements like this:

```
FROM kartoza/django-base
ADD REQUIREMENTS.txt /REQUIREMENTS.txt
RUN pip install -r /REQUIREMENTS.txt
RUN pip install uwsgi
```



## credits

Tim Sutton (tim@kartoza.com)
December 2014

