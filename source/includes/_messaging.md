# Messaging

## Activate or deactivate reception of messages for a user
POST /onoff

Used to activate of deactivate the reception of messages.
When a new user is created, the message server should be
informed so that they start receving messages. The user can then opt-out of messages.
User must belong to listed ICUs to toggle message reception.

Request arguments:

{
  user_id: 212039,
  icu_ids: [123, 434] // List of ICU ids,
  on: True // True to turn on, False to turn off,
  delay: 60 // Number of seconds to delay message sending
}

## Retrieve information about scheduled messages for a user
POST /schedule

Returns information about all scheduled messages for a user, including:
icu_id: Optional[int] = None
user_id: Optional[int] = None
user_name: Optional[str] = None
icu_name: Optional[str] = None
phone: Optional[str] = None
attempts: Optional[int] = 0
first_sent: Optional[int] = None
when: Optional[int] = None
url: Optional[str] = None

TODO: format the above better
