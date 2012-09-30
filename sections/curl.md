# Setup

You authenticate with the Vero API by using your `auth_token`. To get your token, login to Vero and select the 'Account' option from the top right hand menu.

***


# Tracking events

All emails built and sent in Vero are based on user actions. Theoretically, the more events you capture the more complex you can make your marketing emails.

Events can be used to send an email straight away, with delay, segmented or in sequence. Much like an analytics package, tracking user events simply involves calling the 'track' method.

**EXAMPLE REQUEST**
```curl
curl http://www.getvero.com/api/v2/events/track.json \
-d auth_token=NTczNjhlNTZjYmI3NzkwNDg4ZjI5OGRjYzc4N2U2MGRhNWZkM2FkYjowYzFhZDc2OGNiZDk5OTA1MzI5YmY3YjMxM2FjZDI1NWNlMGIxMWZm \ 
-d identity['email']=chris.hexton@gmail.com \
-d event_name=viewed_documentation 
```

## Optional data

Further to recording a user's individual details, you may want to include data specific to an event. This data can be used dynamically when building emails (e.g. a product's name could be recorded when a user 'Views a product').

**EXAMPLE REQUEST**
```curl
curl http://www.getvero.com/api/v2/events/track.json \
-d auth_token=NTczNjhlNTZjYmI3NzkwNDg4ZjI5OGRjYzc4N2U2MGRhNWZkM2FkYjowYzFhZDc2OGNiZDk5OTA1MzI5YmY3YjMxM2FjZDI1NWNlMGIxMWZm \ 
-d identity['email']=chris.hexton@gmail.com \
-d event_name=viewed_documentation \
-d data['link']='http://getvero.com/docs'
```

## Development Mode

When working in your development environment, you can flag requests with 'development_mode'. All users and events tracked in development mode are kept separate from production. Emails triggered in development mode will not be sent to your users. Instead they are forwarded to the first email you have registered under the 'Account' > 'Emails' menu in the top right menu bar.

This enables you to test Vero without any risk of accidentally emailing your customers.

**EXAMPLE REQUEST**
```curl
curl http://www.getvero.com/api/v2/events/track.json \
-d auth_token=NTczNjhlNTZjYmI3NzkwNDg4ZjI5OGRjYzc4N2U2MGRhNWZkM2FkYjowYzFhZDc2OGNiZDk5OTA1MzI5YmY3YjMxM2FjZDI1NWNlMGIxMWZm \ 
-d development_mode=true
```

***

# User identification

When you track an event in Vero, we simultaneously handle user identification. At a bare minimum, you must record a user's email.

**EXAMPLE REQUEST**
```curl
curl http://www.getvero.com/api/v2/events/track.json \
-d
auth_token=NTczNjhlNTZjYmI3NzkwNDg4ZjI5OGRjYzc4N2U2MGRhNWZkM2FkYjowYzFhZDc2OGNiZDk5OTA1MzI5YmY3YjMxM2FjZDI1NWNlMGIxMWZm \
-d identity['email']=chris.hexton@gmail.com
```

## Optional data

Using customer data is an important part of building and triggering lifecycle emails. When identifying a user you can push up any extra information you want to be stored in Vero.

You do not need to pass each variable with every request, they are stored the first time they are provided to the API. You can overwrite a previous value by passing up a new value against the user's email.

**EXAMPLE REQUEST**
```curl
curl http://www.getvero.com/api/v2/events/track.json \
-d auth_token=NTczNjhlNTZjYmI3NzkwNDg4ZjI5OGRjYzc4N2U2MGRhNWZkM2FkYjowYzFhZDc2OGNiZDk5OTA1MzI5YmY3YjMxM2FjZDI1NWNlMGIxMWZm \ 
-d identity['email']=chris.hexton@gmail.com \
-d identity['name']="Chris Hexton" \
-d identity['age']=28
```