# Events API

The core offering of Vero is to respond to how your users interact with your software. Tracking user actions is done via our Events API.

## Track events

### POST /api/v2/events/track

This endpoint will track an event for a user. The following parameters are accepted:

<table>
  <tr>
    <th>Attribute</th>
    <th>Required?</th>
    <th>Type</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  <tr>
    <td>auth_token</td>
    <td>Yes</td>
    <td>String</td>
    <td>your API authorisation token. This can be found by logging into your Vero account and selecting "Account" (at the top of the page)</td>
    <td>ZmIxM2NkZGZmZjY4YzFjMTIxYzZmMTlmNmM4NDY3ZTc5N2Y0NmVkYTo2MTk5YThmMDlmMDM5NzBkMjhkNDVjN2Y0MzI1ODE3YzBhZDcyMzhi</td>
  </tr>
  <tr>
    <td>event_name</td>
    <td>Yes</td>
    <td>String</td>
    <td>the name of the event</td>
    <td>signed_up</td>
  </tr>
  <tr>
    <td>identity</td>
    <td>Yes</td>
    <td>JSON object</td>
    <td>a set of user attributes. This object **must** contain an "id" (a unique string for the user) field, and it is recommended that you also supply the user's "email" as well</td>
    <td>{"id": "james@getvero.com", "email": "james@getvero.com"}</td>
  </tr>
  <tr>
    <td>data</td>
    <td>No</td>
    <td>JSON object</td>
    <td>a set of event attributes</td>
    <td>{"age": 25}</td>
  </tr>
  <tr>
    <td>development_mode</td>
    <td>No</td>
    <td>Boolean</td>
    <td>indicates whether the event is tracked in development mode. default: false</td>
    <td>true</td>
  </tr>
</table>

**Example request:**

```
# Tracking a user sign up
POST https://www.getvero.com/api/v2/events/track
{
  "auth_token": "your_auth_token",
  "identity": {
    "id": "1",
    "email": "janedoe@getvero.com"
  },
  "event_name": "user_signed_up"
}

# Tracking a user adding a product to cart
POST https://www.getvero.com/api/v2/events/track
{
  "auth_token": "your_auth_token",
  "identity": {
    "id": "1",
    "email": "janedoe@getvero.com"
  },
  "event_name": "user_signed_up",
  "data": {
    "item": "Blue shoes",
    "price": 40.00
  }
}
```
