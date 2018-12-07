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