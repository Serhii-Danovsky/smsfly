# Smsfly

Welcome! 
 This Ruby gem  helps You to send SMS using API https://sms-fly.com/

TODO: 

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'smsfly', '~> 0.4.6'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install smsfly


Then run:

    $ rails g smsfly:config

which will generate default settings files:

    config/initializers/smsfly.rb

Then configurate smsfly.rb file:

```ruby
Smsfly.configuration do |config|
  config.login = 'You login' # Like this 380675807873
  config.password = 'You password' # Like this  ZhHtgj4Z
end
```
Or another method

```ruby
#/YouApp/config/application.rb
    module YouApp
      class Application < Rails::Application
      ENV['SMS_FLY_USER'] = 'You login' # Like this 380675807873
      ENV['SMS_FLY_PASS'] = 'Your password' # Your password at  https://sms-fly.com/
      end
    end
#and  config/initializers/smsfly.rb
    Smsfly.configuration do |config|
      config.login = ENV['SMS_FLY_USER'] 
      config.password = ENV['SMS_FLY_PASS']
    end
```



Test connection to API:

```ruby
Smsfly.authentication?
#this return
true #- If authentication is successful 
false #- If authentication failed
```

Get your balance:

```ruby
Smsfly.balance
#this return
Float object(like "6.177" ,"5.655")#- If authentication is successful 
false #- If authentication failed
```

## Usage

TODO: 

For show you login and password run:

    $ rails c
    $ Smsfly.connect_info

If the file *smsfly.rb* is set up correctly 
You can send a test message to your own login/phone

```ruby
Smsfly.test_sms('You random text')
```


To send a message to other numbers, use

```ruby
Smsfly.send_sms(text, recipient , description , source)  #  For example Smsfly.send_sms('Hello Word', '380675807873' , 'Name for Sms' , 'Alfaname')
```


Add campaignID

```ruby
  log_obj  -  object where we write campaignID
  log_filed - campaignID  field
  
  # for example 
  history  = HistoryItem.new()
  history.save
  Smsfly.send_sms(text, recipient , description , source  , {:log_obj => history, :log_filed => 'campaign_id'} ) 
  # This write campaignID from API TO history.campaign_id
```

To send a message without getting campaignID

```ruby
Smsfly.send_sms(text, recipient , description , source  , options = {} )  #  For example Smsfly.send_sms('Hello Word', '380675807873' , 'Name for Sms' , 'Alfaname'   , {:log_obj => 'Model', :log_filed => 'campaign_id'})
```


Get Sms Status

```ruby
Smsfly.get_status(campaignID)  # Smsfly.get_status(43545345) 
# It return {"STOPFLAG"=>"0", "ALFANAMELIMITED"=>"0", "ERROR"=>"0", "USERSTOPED"=>"0", "STOPED"=>"0", "UNDELIV"=>"1", "EXPIRED"=>"0", "DELIVERED"=>"0", "SENT"=>"0", "PENDING"=>"0", "NEW"=>"0"} if  campaignID   valid
# Or returrn false if campaignID = no valid


```


## Development

After checking out the repo, run `bin/setup` to install dependencies. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/Serhii-Danovsky/smsfly. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

