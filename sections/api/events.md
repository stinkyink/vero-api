# Events API

The core offering of Vero is to respond to how your users interact with your software. Tracking user actions is done via our Events API.

## Track events

### POST /api/v2/events/track.json

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
    <td>event_name</td>
    <td>Yes</td>
    <td>String</td>
    <td>the name of the event</td>
  </tr>
  <tr>
    <td>identity</td>
    <td>Yes</td>
    <td>JSON object</td>
    <td>a set of user attributes. This object **must** contain at least one field, 'id' (a unique string for the user)</td>
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
POST https://www.getvero.com/api/v2/events/track.json

{
  "auth_token": "exampleAuthToken",
  "identity": {
    "id": "new_email@getvero.com"
    "email": "new_email@getvero.com",
    "age": 25
  },
  "event_name": "test_event",
  "development_mode": false
}
```