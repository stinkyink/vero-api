# Overview

When integrating with Mixpanel, Vero will simultaneously track all events recorded by Mixpanel and allow you to use them when constructing lifecycle emails. It makes setup a 30 second task.

## Setup Mixpanel integration

The only change required to configure Vero for the Mixpanel integration is to wrap the Mixpanel initialisation code in it's own method. This is required so that it is loaded only after Vero initialises.

Below is a copy of the full Mixpanel integration code, as taken from their setup guide, wrapped in it's own method.

Don't panic, we've included a failsafe that ensures Mixpanel will load even if Vero does not. This failsafe is designed so that Vero does not interfere with your Mixpanel installation.

**Note:** You must replace `TOKEN_ID` with a valid Mixpanel API token.

```html
<script type="text/javascript">
  window.mixpanel = (function (b) {

    // This snippet sets up a 'mixpanel' object to be used by Mixpanel.
    b._i=[];b.init=function(a,e,d){function f(b,h){var a=h.split(".");2==a.length&&(b=b[a[0]],h=a[1]);b[h]=function(){b.push([h].concat(Array.prototype.slice.call(arguments,0)))}}var c=b;"undefined"!==typeof d?c=b[d]=[]:d="mixpanel";c.people=c.people||[];c.toString=function(b){var a="mixpanel";"mixpanel"!==d&&(a+="."+d);b||(a+=" (stub)");return a};c.people.toString=function(){return c.toString(1)+".people (stub)"};i="disable track track_pageview track_links track_forms register register_once alias unregister identify name_tag set_config people.set people.increment people.append people.track_charge people.clear_charges people.delete_user".split(" ");for(g=0;g<i.length;g++)f(c,i[g]);b._i.push([a,e,d])};b.__SV=1.2;return b;

  })(window.mixpanel||[]);

  // Here we initialise 'mixpanel' as defined above, don't forget to include *your* Mixpanel API token.
  mixpanel.init("TOKEN_ID");

  loadMixpanel = function(e) {

    // This snippet loads Mixpanel's javascript library. This will be called either: a) after Vero successfully loads or, b) three (3) seconds after the page loads (a failsafe if Vero failed to load).
    var a,f,i,g;a=e.createElement("script");a.type="text/javascript";a.async=!0;a.src=("https:"===e.location.protocol?"https:":"http:")+'//cdn.mxpnl.com/libs/mixpanel-2.2.min.js';f=e.getElementsByTagName("script")[0];f.parentNode.insertBefore(a,f);
    
  }
</script>
```

## Load the Vero library

Once you have prepared the Mixpanel code you can load the Vero library and initialise Vero itself.

Simply copy in the code and replace your API Key to do so.

```html
<script type="text/javascript">
  var _veroq = _veroq || [];

  setTimeout(function(){if(typeof window.Semblance=="undefined"){console.log("Vero did not load in time.");for(var i=0;i<_veroq.length;i++){a=_veroq[i];if(a.length==3&&typeof a[2]=="function")a[2](null,false);}}},3000);

  _veroq.push(['init', {
      api_key: 'API_KEY'
    }, function (vero, loaded){ 
      if (loaded)
        window.mixpanel.splice(0, 0, vero.listeners.attach_to_mixpanel)
      loadMixpanel(document);
    }]
  );
  (function() {var ve = document.createElement('script'); ve.type = 'text/javascript'; ve.async = true; ve.src = '//d3qxef4rp70elm.cloudfront.net/m.js'; var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ve, s);})();
</script>
```

## Development Mode

When working in your development or test environments, you should initialise Vero in 'development_mode'. All users and events tracked in development mode are kept separate from production. Emails triggered in development mode will not be sent to your users. Instead they are forwarded to the first email you have registered under the 'Account' > 'Emails' menu in the top right menu bar.

This enables you to test Vero without any risk of accidentally emailing your customers.

Simply switch the development_mode flag to true when you initialise the library.

```js
_veroq.push(['init', {
  api_key: "fb13cddfff68c1c121c6f19f6c8467e797f46eda",
  development_mode: true
}]);
```

## Identifying a user

Because Vero records your user's identities and the events they track independently of Mixpanel, we require you to identify your user again.To do so you can either:

```js
// Identify a user with an email address
mixpanel.identify("user_email@domain.com");
```

```js
// Identify a user with a unique identifier
mixpanel.identify("user_123")
_veroq.push(["user", {"id": "user_123", "email": "user_email@domain.com"}]);
```
