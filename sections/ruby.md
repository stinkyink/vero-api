# Setup

Our Rails 3.x gem is one of the fastest ways to get going with Vero. To get started add the gem to your Gemfile:

```ruby
gem 'vero'
gem 'delayed_job'
```

## Authentication

You authenticate with the Vero API by providing your API Key and API Secret. You can get these by logging in and managing your Account from the top right-hand menu. Your API keys carry many privileges, so be sure to keep them secret!

To use the API, you need only initialise the gem using your keys and the gem will automatically send your authorisation token with each request.

```ruby
# config/initializers/vero.rb
Vero::App.init do |config|
  config.api_key = "Your API key goes here"
  config.secret = "Your API secret goes here"
end
```

## Development Mode

When working in your development environment, you can flag requests with 'development_mode'. All requests flagged as such will be recorded separately in the Vero console and allow you to fully test Vero without any risk! If 'development_mode' is not explicitly set in your initializer, it will be determined by your current Rails environment.

```ruby
# config/initializers/vero.rb
Vero::App.init do |config|
  config.api_key = "Your API key goes here"
  config.secret = "Your API secret goes here"
  config.development_mode = true
end
```

***

# User identification

To use Vero you need to identify your users. This can be done by marking the model that represents a user as trackable. Identification is centered around a user's email so you must include email in the options list. Ideally your ActiveRecord will have an email field, though you may write your own method to return the user's email.

```ruby
# app/models/user.rb
class User < ActiveRecord::Base
  include Vero::Trackable
  trackable :email
  ...
end
```

## Optional data

Using customer data is an important part of building and triggering lifecycle emails. When identifying a user you can push up any extra information you want to be stored in Vero.

You can list other attributes and methods to be called when recording a user.

```ruby
# app/models/user.rb
class User < ActiveRecord::Base
  include Vero::Trackable
  trackable :email, :name, :age

  def email
    'chris.hexton@gmail.com'
  end

  def name
    'Chris Hexton'
  end

  def age
    28
  end
end
```

***

# Tracking events

All emails built and sent in Vero are based on user actions. Theoretically, the more events you capture the more complex you can make your marketing emails.

Events can be used to send an email straight away, with delay, segmented or in sequence. Much like an analytics package, tracking user events simply involves calling the 'track' method.

```ruby
# app/controllers/pages_controller.rb
class PagesController < ActionController::Base
  before_filter :authenticate_user!, :only => :documentation
  ...

  def documentation
    # Tell Vero that a user viewed the documentation
    current_user.track('viewed_documentation')
  end
end
```

## Optional data

Further to recording a user's individual details, you may want to include data specific to an event. This data can be used dynamically when building emails (e.g. a product's name could be recorded when a user 'Views a product'). Our API let's you post freeform data variables using the standard JSON format.

```ruby
# app/controllers/pages_controller.rb
class PagesController < ActionController::Base
  before_filter :authenticate_user!, :only => :documentation
  ...

  def documentation
    # Tell Vero that a user viewed the documentation
    current_user.track('viewed_documentation', {link: 'http://www.getvero.com/docs'})
  end
end
```