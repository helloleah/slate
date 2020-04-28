# Back Office

## User Actions

### Reset consent status for a user
POST /reset_consent

Reset consent status for a user

### Login the user from the login page
POST /login

Login the user from the login page form

### Log the user out
GET /logout

Logs the current user out

### Add or update a user from the user(s) page
POST /user

Create a new user or update attributes of an existing user from the user form.

## Database actions

### Update an ICU from the ICU(s) page
POST /icu

From the ICU page form:
- Update whether an ICU is active or not
AND/OR
- Update an ICU's region id

### Add or update a region from the region(s) page
POST /region

Add a new region, or update the name of a region.

### Update a token from the access token(s) page
POST /token

Update access information for an external client:
- whether or not they are active
- access type
- access expiration date

### Sync data from CSV
POST /upload

Sync users, ICUs, or bedcounts from a CSV to the datastore.

## Page Rendering

### Render page for all bedcounts for ICUs that user is an admin for
GET /bedcounts

Get all bedcounts for ICUs that user is an admin for

### Render home page
GET /

Renders home.html, which shows a tree view of ICUs that the user manages (TODO and users they manage?)

### Render page for all ICUs
GET /list_icus

If the user is an admin, lists all ICUs. Otherwise, lists ICUs managed by the user.

### Render page for an ICU
GET /icu

Renders icu.html given the id for that ICU.

### Render login page
GET /login

Renders the login.html page. If the user is already logged in, redirects to the home page.

### Render the map page
GET /map

Renders map.html

### Render page for all scheduled messages for a user
GET /list_messages

Lists scheduled messages for a user by calling the Message Server Client

### Render the operational dashboard page
GET /operational-dashboard

Serves a page with a table gathering current bedcount data with some extra information (operational-dashboard.html)

### Render page for all regions
GET /list_regions

Renders a page with all regions listed.

### Render page for a region
GET /region

Renders region.html given an id for that region.


### Render page for all tokens
GET /list_tokens

Lists all external clients, whether or not they are active, their access type, and their access expiration date.

### Render page for a token
GET /token

A token is an access token for an external client that can access ICUBAM data. Given a userid, this  page lists an external client, whether or not they are active, their access type, and their access expiration date.

### Render page that lists all users
GET /list_users

Render a page that lists all users, including forms to update them. If the current user is an admin, lists all users. Otherwise, lists users that the current user manages.

### Render page for current user
GET /profile

Renders /user form for current user.

### Render page for a user
GET /user

Render the form for a user given their id. User data includes:
- whether or not they are an admin
- whether or not they are active
- create date
- ICUs they have access to
- ICUs thet manage
