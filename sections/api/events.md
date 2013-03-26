# Events API

The core offering of Vero is to respond to how your users interact with your software. Tracking user actions is done via our Events API. 

Vero allows you to view all events that were tracked via the API from the web interface. Furthermore you can build campaigns that are triggered by specific user actions. For example, send a 20% off coupon 2 weeks after a user performs "signed_up" but does not perform "purchase".

On top of the event name, the Event API accepts two types of data: user and event data. The difference between these two types is subtle but very important. 

User data are globally accessible properties describing the user that change very infrequently. These properties are tied to the user profile, and examples include name, age, and signup_date. 

Event data on the other hand are additional properties which describe the event and are only accessible in the scope of the event. These properties are tied to the event profile, and examples include product name, and task name.

Vero allows you to make use of user and event properties in your campaigns for either conditions (e.g. User has user property age equal to 25) or content. To sub a property into your Vero campaign, use the following format:

{{user.age}} or {{event.item_price}}

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
    <td>
      ZmIxM2NkZGZmZjY4YzFjMTI
      xYzZmMTlmNmM4NDY3ZTc5N2
      Y0NmVkYTo2MTk5YThmMDlmM
      DM5NzBkMjhkNDVjN2Y0MzI1
      ODE3YzBhZDcyMzhi
    </td>
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
    <td>a set of user attributes. This object <b>must</b> contain an "id" (a unique string for the user) field, and it is recommended that you also supply the user's "email" as well</td>
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
  "event_name": "add_to_cart",
  "data": {
    "item_name": "Blue shoes",
    "item_price": 40.00
  }
}
```
