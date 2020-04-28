# Back Office

## User Actions

### Reset consent status for a user
`POST /reset_consent`

Reset consent status for a user.

Request arguments:

```
{
  "12345" // the user id
}
```

### Login the user from the login page
`POST /login`

Login the user from the login page form.

Query arguments:
- `next` (Optional): the URL to redirect if the user is already logged in. Can also be specified in the request body.

Request arguments:

```
{
  "email": "example@example.com",
  "password": "12345",
  "next": "/" // Can also be specified as a query param
}
```

### Log the user out
`GET /logout`

Logs the current user out.

Query/request arguments: none

### Add or update a user from the user(s) page
`POST /user`

Create a new user or update attributes of an existing user from the user form.

Request arguments:

```
{
  "password": "12345",
  "user_id": 56789,
  "name": "Dave Davidson",
  "telephone": "8888888888",
  "email": "",
  "description": "",
  "password_hash": "", // Strong hash of the password. Used for admin and manager users
  "access_salt": "", // Used for regular users for passwordless access.
  "is_active": "1", // 1 for true, 0 for false,
  "is_admin": "0", // 1 for true, 0 for false
  "locale": "", // Locale of the user for translations
  "message_type": "email", // One of {email, sms},
  "consent": true, // Consent to use ICUBAM,
  "create_date": "2020-04-27 22-56-45",
  "last_modified": "2020-04-27 22-56-45",
  "icus" = [], // ICUs that the user is assigned to
  "managed_icus" = [], // ICUs that the user manages
}
```

## Database actions

### Update an ICU from the ICU(s) page
`POST /icu`

From the ICU page form:
- Update whether an ICU is active or not
AND/OR
- Update an ICU's region id

Request arguments:

```
{
  "icu_id": 56789,
  "region_id": 56789, // Region id that the ICU belongs to
  "region": "ABC", // Name of the region that the ICU belongs to
  "name": "ABC",
  "legal_id": "ABC",
  "dept": "ABC",
  "city": "ABC",
  "country": "ABC",
  "lat": 11.752505,
  "long": 158.695720,
  "telephone": "9999999999",
  "is_active": "1", // 1 for true, 0 for false
  "create_date": "2020-04-27 22-56-45",
  "last_modified": "2020-04-27 22-56-45",
  "bed_counts" = [], // History of bed counts for the ICU
  "users" = [], // Users assigned to the ICU
  "managers" = [] // Users that can manage the ICU
}
```

### Add or update a region from the region(s) page
`POST /region`

Add a new region, or update the name of a region.

### Update a token from the access token(s) page
`POST /token`

Update access information for an external client:
- whether or not they are active
- access type
- access expiration date

### Sync data from CSV
`POST /upload`

Sync users, ICUs, or bedcounts from a CSV to the datastore.

## Page Rendering

### Render page for all bedcounts for ICUs that user is an admin for
`GET /bedcounts`

Get all bedcounts for ICUs that user is an admin for

### Render home page
`GET /``

Renders home.html, which shows a tree view of ICUs that the user manages (TODO and users they manage?)

### Render page for all ICUs
`GET /list_icus`

If the user is an admin, lists all ICUs. Otherwise, lists ICUs managed by the user.

Query/request arguments: none

### Render page for an ICU
`GET /icu`

Renders icu.html given the id for that ICU.

Query arguments:
- `id`: The id of the ICU to display.

### Render login page
`GET /login`

Renders the login.html page. If the user is already logged in, redirects to the home page.

Query arguments:
- `next` (Optional): The URL to redirect if the user is already logged in. Can also be specified in the request body.
- `error` (Optional): Whether or not an error message should be displayed. Can also be specified in the request body.

Request arguments:

```
{
  "next": "/", // Can also be specified as a query param
  "error": False // Can also be specified as a query param
}
```



### Render the map page
`GET /map`

Renders map.html

### Render page for all scheduled messages for a user
`GET /list_messages`

Lists scheduled messages for a user by calling the Message Server Client

### Render the operational dashboard page
`GET /operational-dashboard`

Serves a page with a table gathering current bedcount data with some extra information (operational-dashboard.html)

### Render page for all regions
`GET /list_regions`

Renders a page with all regions listed.

### Render page for a region
`GET /region`

Renders region.html given an id for that region.


### Render page for all tokens
`GET /list_tokens`

Lists all external clients, whether or not they are active, their access type, and their access expiration date.

### Render page for a token
`GET /token`

A token is an access token for an external client that can access ICUBAM data. Given a userid, this  page lists an external client, whether or not they are active, their access type, and their access expiration date.

### Render page that lists all users
`GET /list_users`

Render a page that lists all users, including forms to update them. If the current user is an admin, lists all users. Otherwise, lists users that the current user manages.

Query/request arguments: none

### Render page for current user
`GET /profile`

Renders /user form for current user.

Query/request arguments: none

### Render page for a user
`GET /user`

Render the form for a user given their id. User data includes:
- whether or not they are an admin
- whether or not they are active
- create date
- ICUs they have access to
- ICUs thet manage

Query arguments:
- `id` (Optional): The id of the user to display
