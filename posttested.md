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

# Feature step 1:test user sign-in

~~~~
@@@ruby
Given /^current user is signed in$/ do  
	@user = User.new 
end
~~~~

# Feature step 2:test creatation page

~~~~
@@@ruby
Given /^is on the post creation page$/ do
    visit new_post_path 
end
~~~~

# Feature step 3:test to publish post

~~~~
@@@ruby
When /^the user publishes a post$/ do
    @post = Post.create(title: "TODO", author: "user@example.com", date_published: "12/15/12", content:"making a test")
    click_button "Create Post"
end
~~~~

# Feature step 4: test to see the new post

~~~~
@@@ruby
Then /^the user is shown the new post$/ do
	visit post_path(@post.id)
	page.should have_content "user@example.com"   
end
~~~~

# Rspec for Post Model

`mkdir  -p spec/models`

~~~~
@@@ruby
require 'spec_helper'

describe Post do 
	it "creates a new post" do
		attr = {
			 author: "Jo",
			  title: "new post", 
			content: "how to make a rspec",
			  email: "user@example.com"
		}
		post = Post.create attr
		post.should be_valid
	end
end
~~~~

# Rspec fails

~~~~
@@@ruby
pivotal-guest-203:posttested zmontesd$ rspec spec
F

Failures:

  1) Post creates a new post
     Failure/Error: post = Post.create attr
     ActiveModel::MassAssignmentSecurity::Error:
       Can't mass-assign protected attributes: email
     # ./spec/models/post_spec.rb:11:in `block (2 levels) in <top (required)>'

Finished in 0.02623 seconds
1 example, 1 failure

Failed examples:

rspec ./spec/models/post_spec.rb:4 # Post creates a new post

Randomized with seed 24862
~~~~

