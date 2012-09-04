# Overview

When integrating with Mixpanel, Vero will simultaneously track all events recorded by Mixpanel and allow you to use them when constructing lifecycle emails. It makes setup a 30 second task.

## Setup Mixpanel integration

The only change required to configure Vero for the Mixpanel integration is to wrap the Mixpanel initialisation code in it's own method. This is required so that it is loaded only after Vero initialises.

To the right is a copy of the full Mixpanel integration code, as taken from their setup guide, wrapped in it's own method.

Don't panic, we've included a failsafe below that ensures Mixpanel will load even if Vero does not. This failsafe is designed to ensure Vero does not interfere with your Mixpanel installation.

```html
<script type="text/javascript">
  window.mixpanel = (function (a) {

    // This snippet sets up a 'mixpanel' object to be used by Mixpanel.
    a._i=[];a.init=function(b,c,f){function d(a,b){var c=b.split(".");2==c.length&&(a=a[c[0]],b=c[1]);a[b]=function(){a.push([b].concat(Array.prototype.slice.call(arguments,0)))}}var g=a;"undefined"!==typeof f?g=
    a[f]=[]:f="mixpanel";g.people=g.people||[];h="disable track track_pageview track_links track_forms register register_once unregister identify name_tag set_config people.set people.increment".split(" ");for(e=0;e<h.length;e++)d(g,h[e]);a._i.push([b,c,f])};a.__SV=1.1;return a;

  })(window.mixpanel||[]);

  // Here we initialise 'mixpanel' as defined above, don't forget to include *your* Mixpanel API token.
  mixpanel.init("TOKEN_ID");

  loadMixpanel = function(c) {

    // This snippet loads Mixpanels javascript library. This will be called either: a) after Vero successfully loads or, b) three (3) seconds after the page loads (a failsafe if Vero failed to load).
    var b,d,h,e;b=c.createElement("script");b.type="text/javascript";b.async=!0;b.src=("https:"===c.location.protocol?"https:":"http:")+'//api.mixpanel.com/site_media/js/api/mixpanel.2.js';d=c.getElementsByTagName("script")[0];d.parentNode.insertBefore(b,d);

  };
</script>
```

## Load the Vero library

Once you have prepared the Mixpanel code you can load the Vero library and initialise Vero itself.

Simply copy in the code to the right and replace your API Key and API Secret to do so.

```html
<script type="text/javascript">
  var _veroq = _veroq || [];

  setTimeout(function(){if(typeof window.Semblance=="undefined"){console.log("Vero did not load in time.");for(var i=0;i<_veroq.length;i++){a=_veroq[i];if(a.length==3&&typeof a[2]=="function")a[2](null,false);}}},3000);

  _veroq.push(['init', {
      api_key: 'API_KEY', 
      secret: 'API_SECRET'
    }, function (vero, loaded){ 
      if (loaded)
        window.mixpanel.splice(0, 0, vero.listeners.attach_to_mixpanel)
      loadMixpanel(document);
    }]
  );
  (function() {var ve = document.createElement('script'); ve.type = 'text/javascript'; ve.async = true; ve.src = '//getvero.com/assets/m.js'; var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ve, s);})();
</script>
```

## Development Mode

When working in your development or test environments, you should initialise Vero in 'development_mode'. All users and events tracked in development mode are kept separate from production. Emails triggered in development mode will not be sent to your users. Instead they are forwarded to the first email you have registered under the 'Account' > 'Emails' menu in the top right menu bar.

This enables you to test Vero without any risk of accidentally emailing your customers.

Simply switch the development_mode flag to true when you initialise the library.

```js
_veroq.push(['init', {
  api_key: "fb13cddfff68c1c121c6f19f6c8467e797f46eda", 
  secret: "6199a8f09f03970d28d45c7f4325817c0ad7238b",
  development_mode: true
}]);
```