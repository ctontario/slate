---
title: CTO Registry API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL

toc_footers:

includes:
  - Admin
  - Committee
  - Institution
  - Security
  - Study
  - System
  - User
  - Visitor
  - errors

search: true
---

# Introduction

This documentation describes the various requests that can be made through the API, who can access them, and what they are expected to do.

## Request Categories

The requests are broken down into logical categories, which make up the menu on the right side of the screen.
These categories are just for organization. For instance, the "User" category contains all the requests that relate
to managing one existing user, like adding a new institution, or updating the user's confidentiality agreement.

## Request Parameters

Request URLs can contain parameters.  These are usually used to pass in the relevant ID for an operation.  When
requests have parameters in the URL, they will always be in the format of `:requestParam`,

i.e. for the URL `/user/:userId` a request of `/user/123` would try to access the user with the system ID of `123`

## System Security

Most of the requests contained in the CTO Registry API require authentication (logging in) and some form of authorization.

### Authentication

Authentication is simply the act of the user logging in to their account using their username and password.  To do this
simply use the <strong>Security - Authentication</strong> request.

This request will return a JSON Web Token (JWT) "token" that will be used for subsequent requests. To use this token to authenticate when performing a request,
set an HTTP Authorization header in the request with the format of "Bearer [TOKEN]".

For more information on JSON Web Tokens, visit [https://jwt.io/](https://jwt.io/)

### Authorization

After checking the users authentication, requests will generally check for further authorization.  To do this the system
uses a set of "privileges" that describe conditions that a user must meet.


### Privileges

Privileges are stored on each user's account and are maintained by the CTO Administrators and background processes in the system.
The following table describes the privileges that exist in the system:

 Scope      | Role       | Target      | Description
------------|------------|-------------|-------
self| N/A | N/A| This simply means the user can request their own data.
system| admin| N/A | A CTO system adminstrator.  This user will generally have full access to all data
institution|member|[institutionId]| Every user that is listed at an institution will have this privilege for each of their institutions
institution|admin|[institutionId]| An Institution administrator.  Similar to the CTO system administrator but with access only extending to users and data related to the specified institution
study|applicant|[studyId]| A system controlled privilege.  Instead of storing a specific privilege on the user account, the study data itself is used to determine if the user is an applicant or not.  A study applicant is any user that has any specific association to a study.
committee|member|[committeeId]| A system controlled privilege.  This privilege is granted to a user when they are listed as a member of the specific committee in the committee data.



Each request contains a table with the following format that describes what privileges a user must have on their account to access it:

 Scope      | Role       | Auth Source
------------|------------|-------------
system| admin| N/A
institution|admin|institution
study|applicant|study
committee|member|study

This table lists the different privileges that the user would need to have to access the request.  The user must have one
or more of these privileges, or the request is denied and a <strong><em>403 - UNAUTHORIZED</em></strong> response is returned. The scope and role are combined to find the
privilege in the user's account, and the auth source is used to determine how the privilege target should be resolved.

<aside class="notice">Sometimes there are extra restrictions on the data the request will return. These will be documented on the specific request
The privileges listed in the Authorization tables simply list what is required to access the request as a whole.</aside>


### Authorization Example

The way these roles work is best described using an example. Consider the following request URL and the authorization
restriction in the following table:

`GET /user/:userId`

 Scope      | Role       | Auth Source
------------|------------|-------------
institution|admin|user

This can be read as thus:

- the requesting user MUST have the <strong>institution:admin</strong> privilege

- The Auth Source tells us to look for associations based on the "user" being requested

- So the <strong>institution:admin</strong> privilege must target an institution that the user being requested is also part of




