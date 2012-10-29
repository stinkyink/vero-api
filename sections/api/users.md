# User API

Vero maintains a representation of each user you track with our API or CapsuleCRM integration. If you want to change any of your user's details, you can make use of our new User API. 

## Edit users

### PUT /api/v2/users/edit.json

This endpoint will update the email address and/or custom attributes for a user. The following parameters are accepted:

- id (required) - the unique string identifying the user. This could be user's email address.
- auth_token (required) - your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)
- changes - a JSON object with changes you the user
- development_mode (optional) - a boolean to indicate whether the event is tracked in development mode. default: false

**Example request:**

```
PUT https://www.getvero.com/api/v2/users/edit.json

{
  "id": "james@getvero.com",
  "auth_token": "exampleAuthToken",
  "changes": {
    "email": "new_email@getvero.com",
    "age": 25
  }
}
```

## Edit user tags

### PUT /api/v2/users/tags/edit.json

This endpoint will update the tags for an existing user. The following parameters are accepted:

- id (required) - the unique string identifying the user. This could be user's email address.
- auth_token (required) - your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)
- add (optional) - a JSON array containing the tags to add to the user
- remove (optional) - a JSON array containing the tags to remove from the user
- development_mode (optional) - a boolean to indicate whether the event is tracked in development mode. default: false

**NOTE:** Although both `add` and `remove` have been marked as optional, at least one is required or else a 400 error will be returned.

**Example request:**

```
PUT https://www.getvero.com/api/v2/users/tags/edit.json

{
  "id": "james@getvero.com",
  "auth_token": "exampleAuthToken",
  "add": ["rubyist"],
  "remove": ["warm_lead"]
}
```

## Unsubscribe user

### POST /api/v2/users/unsubscribe.json

This endpoint will unsubscribe a user from all future email communications. The following parameters are accepted:

- id (required) - the unique string identifying the user. This could be user's email address.
- auth_token (required) - your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)

**Example request:**

```
POST https://www.getvero.com/api/v2/users/unsubscribe.json

{
  "id": "james@getvero.com",
  "auth_token": "exampleAuthToken"
}
```