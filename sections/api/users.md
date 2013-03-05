# User API

Vero maintains a representation of each user you track with our API or CapsuleCRM integration. If you want to change any of your user's details, you can make use of our new User API. 

## Tracking users

### POST /api/v2/events/track

This endpoint will track an event for a user. The following parameters are accepted:

<table>
  <tr>
    <th>Attribute</th>
    <th>Required?</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>auth_token</td>
    <td>Yes</td>
    <td>String</td>
    <td>your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)</td>
  </tr>
  <tr>
    <td>id</td>
    <td>Yes</td>
    <td>String</td>
    <td>the unique string identifying the user. This could be user's email address.</td>
  </tr>
  <tr>
    <td>email</td>
    <td>No</td>
    <td>String</td>
    <td>the user's email address. This must be a valid email address, and is required if you would like the user to receive your campaigns.</td>
  </tr>
  <tr>
    <td>data</td>
    <td>No</td>
    <td>JSON object</td>
    <td>a set of user attributes.</td>
  </tr>
  <tr>
    <td>development_mode</td>
    <td>No</td>
    <td>Boolean</td>
    <td>indicates whether the user is tracked in development mode. default: false</td>
  </tr>
</table>

**Example request:**

```
POST https://www.getvero.com/api/v2/users/track

{
  "auth_token": "exampleAuthToken",
  "id": "user_id",
  "email": "an_email_address@yourdomain.com",
  "data": {
    "first_name": "James",
    "age": 25
  },
  "development_mode": false
}
```

## Edit users

### PUT /api/v2/users/edit

This endpoint will update the email address and/or custom attributes for a user. The following parameters are accepted:

<table>
  <tr>
    <th>Attribute</th>
    <th>Required?</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>Yes</td>
    <td>String</td>
    <td>the unique string identifying the user. This could be user's email address.</td>
  </tr>
  <tr>
    <td>auth_token</td>
    <td>Yes</td>
    <td>String</td>
    <td>your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)</td>
  </tr>
  <tr>
    <td>changes</td>
    <td>Yes</td>
    <td>JSON object</td>
    <td>a set of changes to the user attributes.</td>
  </tr>
  <tr>
    <td>development_mode</td>
    <td>No</td>
    <td>Boolean</td>
    <td>indicates whether the event is tracked in development mode. default: false</td>
  </tr>
</table>

**Example request:**

```
PUT https://www.getvero.com/api/v2/users/edit

{
  "id": "james@getvero.com",
  "auth_token": "exampleAuthToken",
  "changes": {
    "email": "new_email@getvero.com",
    "age": 25
  }
}
```

#### Note: Changing Timezones

By default our Javascript library will detect a customer's timezone and track this as a user attribute. The timezone is stored as a numeric value relative to GMT. PST, for example, would be stored as -8. You can manually override a customers timezone by updating this attribute in the same way you would update any other.

**Example request:**

```
PUT https://www.getvero.com/api/v2/users/edit

{
  "id": "james@getvero.com",
  "auth_token": "exampleAuthToken",
  "changes": {
    "timezone": -8
  }
}
```

## Edit user tags

### PUT /api/v2/users/tags/edit

This endpoint will update the tags for an existing user. The following parameters are accepted:

<table>
  <tr>
    <th>Attribute</th>
    <th>Required?</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>Yes</td>
    <td>String</td>
    <td>the unique string identifying the user. This could be user's email address.</td>
  </tr>
  <tr>
    <td>auth_token</td>
    <td>Yes</td>
    <td>String</td>
    <td>your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)</td>
  </tr>
  <tr>
    <td>add</td>
    <td>No</td>
    <td>JSON array</td>
    <td>the tags to add to the user.</td>
  </tr>
  <tr>
    <td>remove</td>
    <td>No</td>
    <td>JSON array</td>
    <td>the tags to remove from the user.</td>
  </tr>
  <tr>
    <td>development_mode</td>
    <td>No</td>
    <td>Boolean</td>
    <td>indicates whether the event is tracked in development mode. default: false</td>
  </tr>
</table>

**NOTE:** Although both `add` and `remove` have been marked as optional, at least one is required or else a 400 error will be returned.

**Example request:**

```
PUT https://www.getvero.com/api/v2/users/tags/edit

{
  "id": "james@getvero.com",
  "auth_token": "exampleAuthToken",
  "add": ["rubyist"],
  "remove": ["warm_lead"]
}
```

## Unsubscribe user

### POST /api/v2/users/unsubscribe

This endpoint will unsubscribe a user from all future email communications. The following parameters are accepted:

<table>
  <tr>
    <th>Attribute</th>
    <th>Required?</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>Yes</td>
    <td>String</td>
    <td>the unique string identifying the user. This could be user's email address.</td>
  </tr>
  <tr>
    <td>auth_token</td>
    <td>Yes</td>
    <td>String</td>
    <td>your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)</td>
  </tr>
</table>

**Example request:**

```
POST https://www.getvero.com/api/v2/users/unsubscribe

{
  "id": "james@getvero.com",
  "auth_token": "exampleAuthToken"
}
```
