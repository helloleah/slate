# Admin

## User Actions

### Reset consent status for a user

> Request body

```
{
  "12345" // the user id
}
```

`POST /reset_consent`

Reset consent status for a user.

### Login the user from the login page

> Request body

```
{
  "email": "example@example.com",
  "password": "12345",
  "next": "/" // Can also be specified as a query param
}
```

`POST /login`

Login the user from the login page form.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`next` | string | The URL to redirect if the user is already logged in. Can also be specified in the request body.

### Log the user out
`GET /logout`

Logs the current user out.

Query/request arguments: none

### Add or update a user from the user(s) page

> Request body

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

`POST /user`

Create a new user or update attributes of an existing user from the user form.

## Database actions

### Update an ICU from the ICU(s) page

> Request body

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

`POST /icu`

From the ICU page form:

- Update whether an ICU is active or not
AND/OR
- Update an ICU's region id

### Add or update a region from the region(s) page

> Request body

```
{
  "region_id": 12345,
  "name": "ABCD",
  "create_date": "2020-04-27 22-56-45",
  "last_modified": "2020-04-27 22-56-45",
  "icus": [] // ICUs in the region
}
```

`POST /region`

Add a new region, or update the name of a region.

### Update a token from the access token(s) page

> Request body

```
{
  "external_client_id": 12345,
  "name": "ABCD",
  "email": "example@example.com",
  "telephone": "1234567890",
  "access_key_hash": "ABCD", // Strong hash of the access key. It should be unique.
  "access_key": "ABCD", // Be aware this will be removed at some point in the future.
  "expiration_date": "2021-04-27 22-56-45", // If set, denotes the date that the access key expires.
  "is_active": "1", // 1 for true, 0 for false.
  "access_type": "1", // 1 for map access, 2 for database retrieve access, 3 for database upload access, 4 for all access
  "create_date": "2020-04-27 22-56-45",
  "last_modified": "2020-04-27 22-56-45",
  "regions": [] // Regions that an external client can access.
}
```

`POST /token`

Update access information for an external client:

- whether or not they are active
- access type
- access expiration date

### Sync data from CSV

> Request body

```
{
  "data": "", // CSV content
  "objtype": "ICUs" // One of: {"ICUs", "Bed Counts", "Scheduled Messages", "Regions", "Users", "Access Tokens"}
}
```

`POST /upload`

Sync users, ICUs, or bedcounts from a CSV to the datastore.

## Page Rendering

### Render page for all bedcounts for ICUs that user is an admin for
`GET /bedcounts`

Renders a page with all bedcounts for ICUs that user is an admin for.

### Render home page
`GET /`

Renders home.html, which shows a tree view of ICUs that the user manages.

### Render page for all ICUs
`GET /list_icus`

If the user is an admin, lists all ICUs. Otherwise, lists ICUs managed by the user.

### Render page for an ICU
`GET /icu`

Renders icu.html given the id for that ICU.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`id` | integer | The id of the ICU to display.

### Render login page

> Request body

```
{
  "next": "/", // Can also be specified as a query param
  "error": False // Can also be specified as a query param
}
```

`GET /login`

Renders the login.html page. If the user is already logged in, redirects to the home page.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`next` | string | The URL to redirect if the user is already logged in. Can also be specified in the request body.
`error` | boolean  | Whether or not an error message should be displayed. Can also be specified in the request body.

### Render the map page
`GET /map`

Renders map.html.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`level` | integer | The level to display data at. Must be one of {"country", "region", "dept", "city", "icu"}. Default is "dept."

### Render page for all scheduled messages for current user
`GET /list_messages`

Lists scheduled messages for the current user.

### Render the operational dashboard page
`GET /operational-dashboard`

Serves a page with a table gathering current bedcount data with some extra information (operational-dashboard.html).

**Querystring parameters**

Name | Type | Description
-----|------|------------
`region` | integer | The id of the region to limit the data to.

### Render page for all regions
`GET /list_regions`

Renders a page with all regions listed.

### Render page for a region
`GET /region`

Renders region.html given an id for that region.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`id` | integer | The id of the region to display.

### Render page for all tokens
`GET /list_tokens`

Lists all external clients, whether or not they are active, their access type, and their access expiration date.

### Render page for a token
`GET /token`

A token is an access token for an external client that can access ICUBAM data. Given a userid, this  page lists an external client, whether or not they are active, their access type, and their access expiration date.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`id` | integer | The id of the token to display.

### Render page that lists all users
`GET /list_users`

Render a page that lists all users, including forms to update them. If the current user is an admin, lists all users. Otherwise, lists users that the current user manages.

### Render page for current user
`GET /profile`

Renders /user form for current user.

### Render page for a user
`GET /user`

Render the form for a user given their id. User data includes:

- whether or not they are an admin
- whether or not they are active
- create date
- ICUs they have access to
- ICUs they manage

**Querystring parameters**

Name | Type | Description
-----|------|------------
`id` | integer | The id of the user to display.
