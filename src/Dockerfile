# pull official base image
FROM python:3.5-alpine

# setting building arguments
ARG INSTALL_PACKAGES

# set environment varibles
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV DJANGO_STATIC /usr/src/app/staticfiles
ENV DJANGO_MEDIA /usr/src/app/mediafiles

# set work directory
WORKDIR /usr/src/app

RUN apk update && apk add postgresql-dev gcc python3-dev musl-dev

# install dependencies
RUN pip install --upgrade pip
RUN pip install pipenv
COPY ./Pipfile /usr/src/app/Pipfile
RUN pipenv lock

# installing all packages and dependencies
RUN $INSTALL_PACKAGES

# copy project
#COPY . /usr/src/app/

# Defining a healthcheck to curl the home page of Django app.
HEALTHCHECK --interval=1m --timeout=10s CMD curl -f http://localhost:8000 || exit 1

# Run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]

