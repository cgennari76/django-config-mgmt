# pull official base image
FROM ubuntu:20.04

# install python
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip

# install postgres drivers
ARG DEBIAN_FRONTEND=noninteractive
RUN apt install -y postgresql postgresql-contrib \
    && apt install -y libpq-dev python3-dev \
    && apt install python3-psycopg2 \
    && pip3 install psycopg2

# install and start postgresql
RUN apt install -y postgresql postgresql-contrib
USER postgres
RUN /etc/init.d/postgresql start && \
    psql --command "CREATE USER hello_django WITH SUPERUSER PASSWORD 'hello_django';" && \
    createdb -O hello_django hello_django_dev

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# set firewall rule

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy project
COPY . .

