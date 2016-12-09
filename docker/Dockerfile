#
FROM ubuntu:trusty

MAINTAINER seandavi@gmail.com

RUN apt-get update
RUN apt-get install -y wget lsb-release apt-transport-https sudo

RUN wget -qO - https://packages.irods.org/irods-signing-key.asc | sudo apt-key add -
RUN echo "deb https://packages.irods.org/apt/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/renci-irods.list
RUN apt-get update


RUN apt-get install -y postgresql


COPY irods_db_setup.sql /tmp/irods_db_setup.sql
RUN chown postgres:postgres /tmp/irods_db_setup.sql

USER postgres

# Note: here we use ``&&\`` to run commands one after the other - the ``\``
#       allows the RUN command to span multiple lines.
RUN    /etc/init.d/postgresql start &&\
    psql -f /tmp/irods_db_setup.sql

USER root

RUN sudo apt-get install -y irods-server irods-database-plugin-postgres


