# PipedrivePUT

## Status
<a href="https://badge.fury.io/rb/PipedrivePUT"><img src="https://badge.fury.io/rb/PipedrivePUT.svg" alt="Gem Version" height="22"></a>

## Travis CI Build Status
<a href="https://travis-ci.org/jakepens71"><img src="https://travis-ci.org/jakepens71/RailsPipedriveGem.svg?branch=master" height="22"></a>



## Installation

Add this line to your application's Gemfile:

```ruby
gem 'PipedrivePUT'
```

#Needed for some http commands.

```ruby
gem 'httparty'
```

And then execute:

    $ bundle install

Or install it yourself as:

    $ gem install PipedrivePUT


## To install config file 
```ruby
  rails g pipedrive_p_u_t:config
```
This will install a config file in config/initializers/pipedriveput.rb
Make sure to change the value inside of this file 
```ruby 
  PipedrivePUT.key('your_api_key_goes_here')

```

## Organizations

Get all organizations from your account at Pipedrive

```ruby
  PipedrivePUT::Organizations.getAllOrgs
```

Get Organization by ID
```ruby
  PipedrivePUT::Organizations.getOrganization(< id >)
```


Add an organization

```ruby
  PipedrivePUT::Organizations.addOrganization(< Name of new Organization >)
```

You can also add various other parameters based on values in Pipedrive or custom keys when creating a organization!


```ruby
  PipedrivePUT::Organizations.addOrganization(< Name of new Organization >, < :optionArgument => "value" > )
```

NOTE: the options must be in hash format

Example:

```ruby
  PipedrivePUT::Organizations.addOrganization("Jacob Programming Test", :address => "South Jasmine Street")
```

You can aso add ANY custom key from Pipedrive to this to input values into those fields

Example:

```ruby
  PipedrivePUT::Organizations.addOrganization("Jacob Programming Test", :'3df8474115f948137b3f98a0ff651d0edbbd2f54' => "JMD", :address => "South Jasmine Street")
```

Find Organization by term

```ruby
  PipedrivePUT::Organizations.findOrganizationByName(< Term >)
```

Find Persons in an Organization
```ruby
  PipedrivePUT::Organizations.getPersonsOfOrganization(< id >)
```

Update an organization
```ruby
  PipedrivePUT::Organizations.updateOrganization(< id >, < optional params >)
```
Example
```ruby
  PipedrivePUT::Organizations.updateOrganization(1, :name => "New Organization Name")
```

## Deals

Get Specific Deal with ID

```ruby
  PipedrivePUT::Deal.getDeal(<id>)
```

Get All Deals

```ruby
PipedrivePUT::Deal.getAllDeals
```

## Deal Fields

Get All Deal Fields
```ruby
  PipedrivePUT::DealFields.getAllDealFields
```

## Search

Search entire Pipedrive (Deals, Organizations, Product, File, Person)

```ruby
  PipedrivePUT::Search.search(< Term >)
```

Search Specific Item type in Pipedrive (Deals, Organizations, Product, File, Person)

```ruby
  PipedrivePUT::Search.search(< Term >, < item_type >)
```

Example:

```ruby
  PipedrivePUT::Search.search("UPMC", "organization")
```

## Users

Get All users for your company

```ruby
  PipedrivePUT::Users.getAllUsers
```

## Persons

Get all persons from Pipedrive
```ruby
  PipedrivePUT::Persons.getAllPersons
```

Get specifi Person from Pipedrive

```ruby
  PipedrivePUT::Persons.detailsOfPerson(< id >)
```

Add a person to Pipedrive

```ruby
  PipedrivePUT::Persons.addPerson(< Name of Person >, < additional params >)
```

Example:

```ruby
  PipedrivePUT::Persons.addPerson("Programming Test Person", {:org_id => 15367, :phone => [{:value=>'555-555-3340',:label=>'work'},{:value=>'555-111-1111',:label=>'home'}]})
```

NOTE: The option arguments do not be put in as strings. As of right now that is not working in irb console. I will attempt to see if that plays a factor in rails its self.

Delete a persons from Pipedrive

```ruby
  PipedrivePUT::Persons.deletePerson(< id >)
```

Update a persons from Pipedrive

```ruby
  PipedrivePUT::Persons.updatePerson(< id >, < additional params >)
```

Example

```ruby
  PipedrivePUT::Persons.updatePerson(10, :email => "test@test.com")
```

## Activities

Get all Activites per user 
```ruby 
  PipedrivePUT::Activity.getActivity(< user_id >)
```

Get all Activites for a specific organization 

```ruby 
   PipedrivePUT::Activity.getOrgActivities(< org_id >)
```

Add an Activity 

```ruby 
   PipedrivePUT::Activity.addActivity(<subject>, <type>, <:options => "value">)
```

## Activity Types

Get all Activity Types
```ruby
  PipedrivePUT::Activity.getActivity_type
```

## Filters 

Get all filters 
```ruby
  PipedrivePUT::Filters.getFilters
```

## Files 
Get all files
```ruby 
  PipedrivePUT::Files.getAllFiles
```

Download a specific file 
```ruby 
  PipedrivePUT::Files.downloadFile(< file_id >)
```
# ^This will download the specific file and place it in the root dir of your current dir

## Currencies

Get all Currencies
```ruby 
  PipedrivePUT::Currencies.getAllCurr
```

Search for Currencies based off currency name 
```ruby
  PipedrivePUT::Currencies.getCurr(< currency_name >)
```

If you want to get fancy and calculate exchange rates I added method in for that as well :)
```ruby 
   PipedrivePUT::Currencies.getExchangeRate(< currency_name >, < options = {} >)
   #this uses the gem 'money' and 'google_currency'
   #The options for this method are :amount and :ex_code
   # :amount needs to look like this wholenumber_change so $100.80 would look like 100_80 
   # :ex_code will be the currency code you want to calculate the exchange rate for
   #Ex: 
   PipedrivePUT::Currencies.getExchangeRate('Australian Dollar', :amount => "100_80", :ex_code => "USD")
   #=> "$72.72"

```


## Pipelines

Get all Pipelines
```ruby
  PipedrivePUT::Pipelines.getAllPipelines
```

Get one Pipeline
```ruby
  PipedrivePUT::Pipelines.getOnePipeline(< id >)
```

## Recents

Get all Recent changes from Pipedrive based on a specific time
```ruby
  PipedrivePUT::Recents.getRecent(< Time.now >)
```

## Organization Fields

Get all fields that are able to be used in an organization
```ruby
  PipedrivePUT::OrganizationFields.getAllOrganizationFields
```

NOTE: This searches for everything in Pipedrive (deal, organization, user, state, product, etc.) 

I hope to add additional support to break this down at a later time.

Add Organization Field
```ruby
  PipedrivePUT::OrganizationFields.addOrganizationField(< Field Name>, <Field Type>, { <options> } )
```

Field types: " ", varchar, varchar_auto, text, double, monetary, date, set, enum, user, org, people, phone, time, timerange, daterange

NOTE: The field type for Pipedrive is required. However, it can also be left as empty.

Example:
```ruby
  PipedrivePUT::OrganizationFields.addOrganizationField("Total Ordered in September", "monetary", {:important_flag => 'true'})
```

Data is returned in JSON format.

This can be easily customized. I needed something quickly and easily for my own personal project.

This is my first attempt at a ruby gem so I appoligize if things are unorthodox.

The Pipedrive API can be found at:
https://developers.pipedrive.com/v1

## To do List


1. Add support for additional arguments when creating a deal

2. Add ability to search for recent changes by specific types onle (deal, organization, user, state, etc.)

3. Many other Pipedrive API Calls


## Contributing

1. Fork it ( https://github.com/jakepens71/RailsPipedriveGem/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
