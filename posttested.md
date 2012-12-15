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
 

