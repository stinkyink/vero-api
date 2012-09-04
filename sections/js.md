Setup
------------

Our Javascript library is one of the fastest ways to get up and running with Vero. To get started simply setup include the Javascript library itself and assign the Vero Queue just before the `<\head>` tag of your webpage.

**Note:** You need to include this on every page of your website.

_Ensure you setup the Vero queue and include the JS library._

```html
<script type="text/javascript">
  var _veroq = _veroq || []; 
  function(){var ve = document.createElement('script');ve.type = 'text/javascript';ve.async = true;ve.src = '//getvero.com/assets/m.js';var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ve, s);})();
</script>
```

### Authentication

You authenticate to the Vero API by providing your API Key and API Secret (technically a salt, really). You can get these by logging in and selecting the 'Account' option from the top right-hand menu.

**Note:** You need to include this on every page of your website.

_Initialise the library._

```js
_veroq.push(['init', {
  api_key: "fb13cddfff68c1c121c6f19f6c8467e797f46eda", 
  secret: "6199a8f09f03970d28d45c7f4325817c0ad7238b",
}]);
```

### Development Mode

When working in your development or test environments, you should initialise Vero in 'development_mode'. All users and events tracked in development mode are kept separate from production. Emails triggered in development mode will not be sent to your users. Instead they are forwarded to the first email you have registered under the 'Account' > 'Emails' menu in the top right menu bar.

This enables you to test Vero without any risk of accidentally emailing your customers.

_Simply switch the development_mode flag to true when you initialise the library._

```js
_veroq.push(['init', {
  api_key: "fb13cddfff68c1c121c6f19f6c8467e797f46eda", 
  secret: "6199a8f09f03970d28d45c7f4325817c0ad7238b",
  development_mode: true
}]);
```

User identification
------------

To use Vero you need to identify your users. To identify a user you must record their email. By default, Vero saves a user across sessions so you should identify any user each time they subscribe, sign up or log in to your service. The Javascript API will handle the rest.

_The user command must always include an email._

```js
_veroq.push(['user', {email: 'chris@getvero.com'} ]);
```

### Optional data

Using customer data is an important part of building and triggering lifecycle emails. When identifying a user you can push up any extra information you want to be stored in Vero.

Information is passed up in the standard JSON format.

_All data is passed as standard JSON._

```js
_veroq.push(['user', {email: 'chris@getvero.com', name: 'Chris Hexton', age: 24} ]);
```

Tracking events
------------

All emails built and sent in Vero are based on user actions. Theoretically, the more events you capture the more complex you can make your marketing emails.

Events can be used to send an email straight away, with delay, segmented or in sequence. Much like an analytics package, tracking user events simply involves calling the 'track' method.

The track command must always include an event name. Events names are always lowercase with underscores representing spaces.

```js
_veroq.push(['track', 'viewed_documentation']);
```

### Optional data

Further to recording a user's individual details, you may want to include data specific to an event. This data can be used dynamically when building emails (e.g. a product's name could be recorded when a user 'Views a product'). Our API let's you post freeform data variables using the standard JSON format.

_All data is passed as standard JSON._

```js
_veroq.push(['track', 'viewed_documentation', {link: 'http://getvero.com/docs'}]);
```