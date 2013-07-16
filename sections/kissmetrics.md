# Overview

When integrating with KISSMetrics, Vero will simultaneously track all events recorded by KISSMetrics and allow you to use them when constructing lifecycle emails. It makes setup a 30 second task.

## Setup KISSMetrics integration

The only change required to configure Vero for the KISSMetrics integration is to wrap the KISSMetrics initialisation code in it's own method. This is required so that it is loaded only after Vero initialises.

To the right is a copy of the full KISSMetrics integration code, as taken from their setup guide, wrapped in it's own method.

Don't panic, we've included a failsafe below that ensures KISSMetrics will load even if Vero does not. This failsafe is designed to ensure Vero does not interfere with your KISSMetrics installation.

```html
<script type="text/javascript">
  // Define the KISSMetrics queue as normal
  var _kmq = _kmq || [];

  function _kms(u){setTimeout(function(){var s=document.createElement('script');var f=document.getElementsByTagName('script')[0];s.type='text/javascript';s.async=true;s.src=u;f.parentNode.insertBefore(s,f);},1);}

  loadKissmetrics = function () {
    // Include your KISSMetrics token
    var _kmk = _kmk || 'API_TOKEN';

    // Load the KISSMetrics script
    _kms('//i.kissmetrics.com/i.js');_kms('//doug1izaerwt3.cloudfront.net/' + _kmk + '.1.js');
  };
</script>
```

## Load the Vero library

Once you have prepared the KISSMetrics code you can load the Vero library and initialise Vero itself.

Simply copy in the code to the right and replace your API Key to do so.

```html
<script type="text/javascript">
  var _veroq = _veroq || [];

  setTimeout(function(){if(typeof window.Semblance=="undefined"){console.log("Vero did not load in time.");for(var i=0;i<_veroq.length;i++){a=_veroq[i];if(a.length==3&&typeof a[2]=="function")a[2](null,false);}}},3000);

  _veroq.push(['init', {
    api_key: 'API_KEY'
  }, function(vero, loaded) {
    if (loaded)
      window._kmq.splice(0, 0, vero.listeners.attach_to_kissmetrics);
    loadKissmetrics();
  }]);
  (function() {var ve = document.createElement('script'); ve.type = 'text/javascript'; ve.async = true; ve.src = '//d3qxef4rp70elm.cloudfront.net/m.js'; var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ve, s);})();
</script>
```

## Development Mode

When working in your development or test environments, you should initialise Vero in `development_mode`. All users and events tracked in development mode are kept separate from production. Emails triggered in development mode will not be sent to your users. Instead they are forwarded to the first email you have registered under the 'Account' > 'Emails' menu in the top right menu bar.

This enables you to test Vero without any risk of accidentally emailing your customers.

Simply switch the development_mode flag to true when you initialise the library.

```js
_veroq.push(['init', {
  api_key: 'API_KEY',
  development_mode: true
}]);
```
