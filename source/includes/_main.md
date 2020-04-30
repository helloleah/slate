# Main

## Get Requests

### Get all ICU bedcounts
**`GET /db/all_bedcounts`**

Retrieve all bedcount data. User must have GET access to the ICUBAM stats.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`format` | string | File format of output. Can be 'csv' or 'hdf' for CSV and HDF files. Otherwise, the output will be written in HTML.
`max_ts` | integer | Restricts the time of the bedcounts returned to this date. Time is in seconds since epoch.
`should_preprocess` | string | Whether preprocessing should be applied to the data. The raw data of ICUBAM contains inputs errors and this preprocessing will attempt to fix them. It should be used cautiously because it alters the data in ways that are useful for analysis purposes but not necessarily reflect the exact/real bed count values. Whenever a query argument named 'preprocess' is present, we enable this preprocessing (it can be 'preprocess=<anything>' or simply 'preprocess').
`id` | integer | The user's access token.

### Get all ICUs
**`GET /db/get_icus`**

Retrieve a list of all ICUs. User must have GET access to the ICUBAM stats.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`format` | string | File format of output. Can be 'csv' or 'hdf' for CSV and HDF files. Otherwise, the output will be written in HTML.
`id` | integer | The user's access token.

### Get all regions
**`GET /db/get_regions`**

Retrieve a list of all regions. User must have GET access to the ICUBAM stats.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`format` | string | File format of output. Can be 'csv' or 'hdf' for CSV and HDF files. Otherwise, the output will be written in HTML.
`id` | integer | The user's access token.

### Get visible bedcounts for current user
**`GET /db/bedcounts`**

Retrieve the latest bed counts of ICS that are visible to the user.
Admin users can view all ICUs. For other users, only ICUs that are in the
same regions as the ICUs that they are assigned to will be visible.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`format` | string | File format of output. Can be 'csv' or 'hdf' for CSV and HDF files. Otherwise, the output will be written in HTML.
`max_ts` | integer | Restricts the time of the bedcounts returned to this date. Time is in seconds since epoch.
`id` | integer | The user's access token.

## Update Requests

### Sync bedcount CSVs to the database

> Request body

```
{
  files:
    {
      file: {
        body: // file body
      }
    }
  ]
}
```

**`POST /db/bedcounts`**

Sync bedcount CSVs from IdF RoR uplink. User must have POST access to the ICUBAM stats.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`format` | string | File format of input. Only 'ror_idf' is supported at this time.
`id` | integer | The user's access token.

### Update bedcounts from the update form page
**`POST /update_counts`**

Register new bedcounts coming from the form by reading the form and saving to the DB. The form data is encoded in the request body.

## Settings/Info

### Consent to ICUBAM terms

> Request body

```
{
  agree: "0" // can be "0" for disagree or "1" for agree
}
```

**`POST /consent`**

Depending on which button the user has clicked, we decide to set the
consent field of the user to True or False.
If False, the user has no access to ICUBAM and it is considered as
inactive. Otherwise we won't ask again and acces is granted.

### Get version information
**`GET /version`**

Retrieve ICUBAM version, git hash of most recent commit, and last modified date of bedcounts data.

## Page Rendering

### Render operational dashboard page
**`GET /dashboard`**

Render a page with a table gathering current bedcount data with some extra information. Must have an API key with GET database access.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`region` | integer | The id of the region to limit the data to.

### Render the home page
**`GET /`**

Render the home page of ICUBAM (index.html).

### Render the home page with an API key
**`GET /map`**

Render the home page of ICUBAM (index.html), but accessed with an API key. Must have an API key with MAP access.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`id` | integer | The user's access token.

### Render the update form page
**`GET /update`**

Render the form for doctors to update their bed count data (update_form.html). User will be prompted to consent if they haven't already.

**Querystring parameters**

Name | Type | Description
-----|------|------------
`id` | integer | The user's access token.

### Render unauthorized error page
**`GET /error`**

Render a page for a 401 unauthorized error (error.html).
