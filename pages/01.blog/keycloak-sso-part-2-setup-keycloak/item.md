---
title: 'Keycloak SSO Part 2: Setting up Keycloak'
published: false
date: '06-12-2018 21:00'
taxonomy:
    category:
        - blog
    tag:
        - Keycloak
visible: false
hide_git_sync_repo_link: false
---

In part two of this series, we are going to look at setting up a standalone-ha deployment of Keycloak on two CentOS 7 servers.

There are three different deployment types for Keycloak, Standalone, Standalone-HA, and Domain Clustered. Standalone deployments are single servers, this is good for a dev or test environment, but not very useful for production use. Standalone-HA are one or more servers which can both be used to serve authentication requests. This method requires a shared database, and each server is configured manually. In a Domain deployment, there is a master server known as the domain controller, and one or more host controllers which serve authentication requests. This mode allows the host controllers to all have an updated configuration when it is changed on the domain controller, greatly reducing administration overhead with multiple servers.

## Installation

Hardware requirements, as well as distribution directory structure and operation mode information can be found at https://www.keycloak.org/docs/latest/server_installation/index.html#installation

I use Ansible to deploy the folder structure for Keycloak and make sure all dependencies are setup correctly. This allows me to easily update and ensure that all my Keycloak servers are deployed correctly. My playbook calls https://github.com/andrewrothstein/ansible-keycloak with some configuration file changes.

## Configuration

Reading and understanding the official documentation is essential to installing Keycloak in a secure manner, I highly recommend you follow the information there and use my configuration as a guide.

### Operation Mode

The first thing to think about when deploying Keycloak is what operation mode you want to use. This will mostly come down to your environment, and the configuration of most modes is the same, just within different files. I am most experienced with Standalone-HA mode, so that is what we are going to work with in this series.

Configuration for this mode is done in the standalone-ha.xml configuration file found at `$keycloak_home/standalone/configuration/standalone-ha.xml`