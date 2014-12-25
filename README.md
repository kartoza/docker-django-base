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

## Build with no package caching


to build the image without apt-cacher do:

```
docker build -t kartoza/django-base git://github.com/kartoza/docker-django-base
```

## Build locally or with apt-cacher-ng caching locally

**Note:** we recommend using ``apt-cacher-ng`` to speed up package fetching -
you should configure the host for it in the provided 71-apt-cacher-ng file.

To build with apt-cacher-ng do you need to clone this repo locally first and 
modify the contents of 71-apt-cacher-ng to match your cacher host. then 
build using a local url instead of directly from github.

```
git clone git://github.com/kartoza/docker-django-base
```

now edit ``71-apt-cacher-ng`` then do:

```
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

