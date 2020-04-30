# Messaging

### Activate or deactivate reception of messages for a user

> Request body

```
{
  user_id: 212039,
  icu_ids: [123, 434] // List of ICU ids,
  on: True // True to turn on, False to turn off,
  delay: 60 // Number of seconds to delay message sending
}
```

`POST /onoff`

Used to activate of deactivate the reception of messages.
When a new user is created, the message server should be
informed so that they start receving messages. The user can then opt-out of messages.
User must belong to listed ICUs to toggle message reception.

### Retrieve information about scheduled messages for a user

> Request body

```
{
  user_id: 12345
}
```

`POST /schedule`

Returns information about all scheduled messages for a user, including:
- icu_id
- user_id
- user_name
- icu_name
- phone
- attempts
- first_sent
- when
- url
