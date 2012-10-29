# Events API

The core offering of Vero is to respond to how your users interact with your software. Tracking user actions is done via our Events API.

## Track events

### POST /api/v2/events/track.json

This endpoint will track an event for a user. The following parameters are accepted:

- auth_token (required) - your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)
- event_name (required) - the name of the event
- identity (required) - a JSON object which contains a set of user attributes. This object **must** contain at least one field, 'id' (a unique string for the user)
- development_mode (optional) - a boolean to indicate whether the event is tracked in development mode. default: false

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