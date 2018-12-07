---
title: 'Keycloak SSO Part 1: What is single sign on?'
date: '06-12-2018 21:48'
taxonomy:
    category:
        - blog
    tag:
        - Keycloak
hide_git_sync_repo_link: false
visible: true
---

In this series, we will take a look at Keycloak, an open-source single sign on solution similar to Microsoft's ADFS product.

In this first part, we will take a brief look at what SSO and Keycloak are, and why they are used.

===

## What is Single Sign On

Single sign-on (SSO) is a property of access control of multiple related, yet independent, software systems. [Wikipedia](https://en.m.wikipedia.org/wiki/Single_sign-on)

What this means is that we can use a single authentication service to allow users to login to other services, without providing a password to the service that is being logged into.

This is different than connecting each of these applications to LDAP, as this requires providing a username and password to every service that you want to login to.

## Benefits of SSO

1. Central location for authentication allows for easier auditing and security.

2. Central location for configuration of authorization, ie, Jane is able to access email but not the CRM suite

3. Authentication to external services such as a hosted CRM suite are made possible without sending LDAP requests over the internet

4. Tokens are wrapped in SSL/TLS as part of the HTTPS connection, but can also be both signed and/or encrypted using keys known only between the identity provider and service for increased security

## What is Keycloak

Keycloak is an open source program that allows you to setup a secure single sign on provider. It supports multiple protocols such as SAML 2.0 and OpenID Connect. It can also store user credentials locally or via an LDAP or Kerberos backend.

These features allows Keycloak to be highly configurable, but also fairly easy to install and setup.

More information about Keycloak can be found here: https://www.keycloak.org