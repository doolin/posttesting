# Post tested BDD/TDD

# Simple testing for Railsbridge intermediate curriculum

Use cucumber and rspec to implement simple acceptance and
model testing for posts.code

# Add cucumber to Gemfile

~~~~
@@@ruby 

gem 'rails'
gem 'sqlite3'
gem 'jquery-rails'

group :assets do
  gem 'sass-rails'
  gem 'coffee-rails'
  gem 'uglifier'
end


group :test do
  gem 'cucumber-rails'
  gem 'database_cleaner'
end
~~~~



# Install cucumber

~~~~
@@@ bash
bundle install
rails generate cucumber:install
~~~~ 


# Acceptance tests

Our application needs to support the following capabilities:

* The user should be able to create a post with a title, author, date published, and content. The author should be the current user.
* The complete post should appear on its own page (aka its show page).
* If the user doesn’t submit all required fields, they should see some error messaging, but shouldn’t lose any of their work.
 
# Features

~~~~
@@@ ruby
Feature: Add pages to create and look at posts

  Users want to write blog posts and suchlike then
  look at them later.

  Scenario: The current user creates a post with title, date, content, author
    Given current user is signed in
      And is on the post creation page
    When the user publishes a post
    Then the user is shown the new post
~~~~

### Run cucumber

# Create step files

~~~~
@@@ ruby 

Given /^current user is signed in$/ do
  pending # express the regexp above with the code you wish you had
end

Given /^is on the post creation page$/ do
  pending # express the regexp above with the code you wish you had
end

When /^the user publishes a post$/ do
  pending # express the regexp above with the code you wish you had
end

Then /^the user is shown the new post$/ do
  pending # express the regexp above with the code you wish you had
end
~~~~

# Create User model

~~~~
@@@ ruby
rails generate model User email:string password:string
~~~~

### Migration

* `rake db:migrate`
* `rake db:test:prepare`

But we don't have users authentication implemented, so...
we make a dummy user:


