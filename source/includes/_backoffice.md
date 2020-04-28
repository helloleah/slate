# Back Office

## Get all bedcounts
GET /bedcounts

Get all bedcounts for ICUs that user is an admin for

## Reset consent status for a user
POST /reset_consent

Reset consent status for a user

## Render home page
GET /

Renders home.html, which shows a tree view of ICUs that the user manages (TODO and users they manage?)

## Render page for all ICUs
GET /list_icus

If the user is an admin, lists all ICUs. Otherwise, lists ICUs managed by the user.

## Render page for an ICU
GET /icu

Renders icu.html given the id for that ICU.

## Update an ICU (TODO: from form it seems like?)
POST /icu

From the ICU page form:
- Update whether an ICU is active or not
AND/OR
- Update an ICU's region id

## Render login page
GET /login

Renders the login.html page. If the user is already logged in, redirects to the home page.

## Login the user from the login page
POST /login

Login the user from the login page form

## Logout the user
GET /logout

Logs the current user out

## Render the map page
GET /map

Renders map.html

## Lists scheduled messages for a user (TODO: I think this is rendering html?)
GET /list_messages

Lists scheduled messages for a user by calling the Message Server Client

## Render the operational dashboard page
GET /operational-dashboard

Serves a page with a table gathering current bedcount data with some extra information (operational-dashboard.html)

## Render page for all regions
GET /list_regions

Renders a page with all regions listed.

## Render page for a region
GET /region

Renders region.html given an id for that region.

## Add or update a region from the region page form
POST /region

Add a new region, or update the name of a region.

## Render page for all tokens
GET /list_tokens

Lists all external clients, whether or not they are active, their access type, and their access expiration date.

## Render page for a token
GET /token

A token is an access token for an external client that can access ICUBAM data. Given a userid, this  page lists an external client, whether or not they are active, their access type, and their access expiration date.

## Update a token
POST /token

Update access information for an external client:
- whether or not they are active
- access type
- access expiration date

## Sync data from CSV
POST /upload

Sync users, ICUs, or bedcounts from a CSV to the datastore.

## Render page that lists all users
GET /list_users

Render a page that lists all users, including forms to update them. If the current user is an admin, lists all users. Otherwise, lists users that the current user manages.

## Render page for current user
GET /profile

Renders /user form for current user.

## Render page for a user
GET /user

Render the form for a user given their id. User data includes:
- whether or not they are an admin
- whether or not they are active
- create date
- ICUs they have access to
- ICUs thet manage

## Create or update a user
POST /user

Create a new user or update attributes of an existing user from the user form.
