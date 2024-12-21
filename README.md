# EzJwt

Simple Rails engine that implements JWT authentication for a Rails API.

The following functionality is included:

### Models:

A user model which includes username and password only

### Controllers:

login \
logout

### Concerns:

authorize_request \
authorize_resource \

### Lib / Services

jwt_encode \
jwt_decode

## Usage

The default expiration for the JWT is set to 24 hours. To change, you can pass the expiration directly to the encode function or override the engine's initializer by creating an initializer file in your main app's config/initializers/ez_jwt.rb and setting EzJwt::DEFAULT_EXPIRATION to something else (example: 48.hours.from_now)

Similarly, the default secret key for encoding JWT tokens is set by default to Rails.application.secrets.secret_key_base.to_s. This can be overridden in the same config/initializers/ez_jwt.rb file in the main application using this engine by modifying the value ExJwt::SECRET_KEY.

## Installation

Add this line to your application's Gemfile:

```ruby
gem "ez_jwt"
```

And then execute:

```bash
$ bundle
```

Or install it yourself as:

```bash
$ gem install ez_jwt
```

Since ez_jwt creates a basic user model with email and password, you need to run the migrations in your app. Simply run:

```bash
$ rails ez_jwt:install:migrations
```

and then run them:

```bash
$ rails db:migrate
```

If you need to extend the default user model (ez_jwt provides a user model with just two fields: email and password with corresponding validations), by, for instance, adding a profile or other various has_many associations, etc, simply create a new file in app/models/ez_jwt/user.rb and extend your model as follows:

```ruby
module EzJwt
  class User < ApplicationRecord
    # Add custom behavior or validations here
  end
end

```

Don't forget to add a migrations file with the extra fields you've added. For example:

```ruby
class AddColumnsToEzJwtUsers < ActiveRecord::Migration[6.0]
  def change
    add_column :ez_jwt_users, :new_column, :string
    add_column :ez_jwt_users, :another_column, :integer
  end
end

```

## Contributing

Contribution directions go here.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
