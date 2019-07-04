---
title: CTO Registry API Reference v1.4

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
  - dictionaries
  - Sample Request
  - errors

search: true
---

# CTO Registry API Reference

<aside class="notice"><strong>Version: 1.4.0, Published: Thu Jul 04 2019 14:29:50 GMT-0400 (Eastern Daylight Time)</strong></aside>

The CTO Registry is a project by Clinical Trials Ontario that builds on the functionality provided by the CTO Stream system.
The backbone of the CTO Registry is a set of REST APIs. This documentation describes the various requests that can be made
through the API, who can access them, and what they are expected to do.


## Request Categories

The requests are broken down into logical categories.
These categories are just for organization. For instance, the **_User_** category contains all the requests that relate
to managing one existing user, like adding a new institution, or updating the user's profile information.


## JSON Schemas

Each request where applicable will include a **_Request Schema_** and a **_Response Schema_**.  These schemas are JSON schema
objects that are used to validate the data being sent and retrieved through the API.  These schemas indicate which fields
are required and describe the possible values for dictionary type fields.

For more information on JSON Schema, please review the documenation: [http://json-schema.org/](http://json-schema.org/)


## Request Schemas

Where applicable each request will list a **_Request Schema_** which describes what data can be sent to the API along with
the request.  The Request Schema will be a JSON Schema with up to 3 top level objects, **_query_**, **_params_** and **_body_**.


### Request Query

Request query fields are appended to the end of the URI as regular HTML query variables.


### Request Parameters

Request URLs can contain parameters.  These are usually used to pass in the relevant ID for an operation.  When
requests have parameters in the URI, they will always be in the format of `:requestParam`.  In addition to being listed
in the Request Schema, the request parameters are also displayed in the URI itself.

i.e. for the URL `/user/:userId` a request of `/user/123` would try to access the user with the system ID of `123`


### Request Body

The request body describes the format of the data that needs to be send as the HTML POST body portion of the request.


## Response Schemas

Each Request where applicable will list the schema that describes the format the response data will be retured in.


## System Security

Most of the requests contained in the CTO Registry API require authentication (logging in) and some form of authorization.


### Authentication

Authentication is simply the act of the user logging in to their account using their username and password.  To do this
simply use the **_Security - Authentication_** request.

This request will return a JSON Web Token (JWT) "token" that will be used for subsequent requests. To use this token to authenticate when performing a request,
set an HTTP Authorization header in the request with the format of `Bearer [TOKEN]``.

For more information on JSON Web Tokens, visit [https://jwt.io/](https://jwt.io/)


### Authorization

After checking the users authentication, requests will generally check for further authorization.  To do this the system
uses a set of **_privileges_** that describe conditions that a user must meet.


### Privileges

Privileges are stored in each user's account and are maintained by the CTO Administrators and background processes in the system.
The following table describes the privileges that exist in the system:

 Scope      | Role       | Target      | Description
------------|------------|-------------|-------
self| N/A | N/A| This simply means the user can request their own data.
system| admin| N/A | A CTO system adminstrator.  This user will generally have full access to all data
institution|member|[institutionId]| Every user that is listed at an institution will have this privilege for each of their institutions
institution|admin|[institutionId]| An Institution administrator.  Similar to the CTO system administrator but with access only extending to users and data related to the specified institution
study|applicant|[studyId]| A system controlled privilege.  Instead of storing a specific privilege on the user account, the study data itself is used to determine if the user is an applicant or not.  A study applicant is any user that has any specific association to a study.
committee|member|[committeeId]| A system controlled privilege.  This privilege is granted to a user when they are listed as an REB Chair or REB Member of the specific committee in the CTO Stream.
committee|admin|[committeeId]| A system controlled privilege.  This privilege is granted to a user when they are listed as an REB Staff or REB Director/Manager of the specific committee in CTO Stream.


Each request contains a table with the following format that describes what privileges a user must have on their account to access it:

Scope | Role | Auth Source | Restrictions
------|------|------------|-------------------
Scope from the Privileges table|Role from the Privileges table|What part of the request is used to determine if the user has the privilege.|Any Restrictions that will be put on the response data if this role is authorized.

This table lists the different privileges that the user would need to have to access the request.  The user must have one
or more of these privileges, or the request is denied and a <strong><em>403 - UNAUTHORIZED</em></strong> response is returned. The scope and role are combined to find the
privilege in the user's account, and the auth source is used to determine how the privilege target should be resolved.

<aside class="notice">Sometimes there are extra restrictions on the data the request will return. These will be documented in the Restrictions column.  If a user authorizes with multiple
privileges, the least restricted version of the data will be returned.
</aside>


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




