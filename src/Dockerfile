# pull official base image
FROM python:3.5-alpine

# setting building arguments
ARG INSTALL_PACKAGES

# set environment varibles
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# set work directory
WORKDIR /usr/src/app

# install dependencies
RUN pip install --upgrade pip
RUN pip install pipenv
COPY ./Pipfile /usr/src/app/Pipfile
RUN pipenv lock

# installing all packages and dependencies
RUN $INSTALL_PACKAGES

# copy project
COPY . /usr/src/app/

# Defining a healthcheck to curl the home page of Django app.
HEALTHCHECK --interval=1m --timeout=10s CMD curl -f http://localhost:8000 || exit 1

# Run Gunicorn server to serve the project
CMD gunicorn allauth_test.wsgi:application --bind 0.0.0.0:8000

