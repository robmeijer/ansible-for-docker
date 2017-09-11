FROM ubuntu:16.04

MAINTAINER Rob Meijer

# Add the ability to install custom repositories
RUN apt-get update \
    && apt-get install -y software-properties-common

# Install Ansible
RUN apt-add-repository ppa:ansible/ansible \
    && apt-get update \
    && apt-get install -y ansible

# Add inventory
COPY ansible/inventory/ /etc/ansible

# Run Nginx playbook
COPY ansible/nginx.yml /etc/ansible
RUN ansible-playbook etc/ansible/nginx.yml

# Tidy up
RUN apt-get remove -y --purge software-properties-common \
    && apt-get autoremove -y \
    && apt-get clean
