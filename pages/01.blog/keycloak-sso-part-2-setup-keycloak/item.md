---
title: 'Keycloak SSO Part 2: Setting up Keycloak'
published: false
date: '06-12-2018 21:00'
taxonomy:
    category:
        - blog
    tag:
        - Keycloak
visible: true
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

### Relational Database Setup

The next thing we have to do is setup Keycloak to use a database, since we are going to be creating a deployment with multiple servers, we are going to need a shared database. Setting up a centrally accessible database is beyond the scope of this article. Just know that we are going to be using a PostgreSQL database that is hosted outside of both of the Keycloak servers.

#### Download a JDBC driver

The first step in setting up a database for Keycloak is to download a JDBC driver for the database. This allows Java to interact with the database. You can usually find these on the main site of your chosen database. For example, PostgreSQL's JDBC driver can be found here: https://jdbc.postgresql.org/download.html

#### Package the driver JAR and install

The official documentation is a good resource for how to package the driver for use with Keycloak, and there is no point in duplicating efforts. It can be found here: https://www.keycloak.org/docs/latest/server_installation/index.html#package-the-jdbc-driver

This boils down to adding a folder structure, copying the .jar file, and adding an .xml file like the following:

```
<?xml version="1.0" ?>
<module xmlns="urn:jboss:module:1.3" name="org.postgresql">

    <resources>
        <resource-root path="postgresql-9.4.1212.jar"/> <!-- update the filename to match your PostgreSQL JDBC driver file name -->
    </resources>

    <dependencies>
        <module name="javax.api"/>
        <module name="javax.transaction.api"/>
    </dependencies>
</module>
```

Making sure to update the path with the correct file name.

#### Declare and load the driver

This part, as well as modifying the datasource are a bit more advanced, so I will go over them in a bit more detail here, however the documentation is still very helpful.

We are going to look at the standalone-ha.xml file we were working on earlier, specifically the `drivers` XML block. In this block, we will be adding an additional driver. We can mostly copy the existing format of the h2 driver, and update the information for PostgreSQL.