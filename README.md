# LA Rails Learners - First App

###### Homework for each week can be found in [issues](https://github.com/LARailsLearners/_first_app_instructions/issues).

## Vanilla Rails

We are starting out this project by creating a vanilla Rails App. Once built you will have the base from which you can build any number of other applications.

#### Our Vanilla Rails Base App will include
+ An new instance of a Rails App
+ Postgres Database
+ A User Model with fields first_name, last_name, email
+ Devise
+ Bootstrap
+ Rspec 
+ README.md with clear directions to the installation and application of all the above.

## Phase One - New Rails App with Postgres and a User Model - [Issue #6](https://github.com/LARailsLearners/_first_app_instructions/issues/6)

To install vagrant see https://github.com/webapp-builders/groundwork

**Create a new rails app with a Postgres database** (change your_app_name to something like jane_doe_firstapp)

    $ rails new your_app_name --database=postgresql

**Changes directories into your new Rails app**

    $ cd your_app_name

**Create the database, load the schema and initialize it with the seed data**

    $ rake db:setup
         -- enable_extension("plpgsql")  
         -> 0.0822s  
         -- initialize_schema_migrations_table()  
         -> 0.0550s  
         -- enable_extension("plpgsql")  
         -> 0.1057s  
         -- initialize_schema_migrations_table()  
         -> 0.0290s

>[All Rails db Rake Tasks and What They Do](http://jacopretorius.net/2014/02/all-rails-db-rake-tasks-and-what-they-do.html)

>[Active Record Migrations](http://edgeguides.rubyonrails.org/active_record_migrations.html)  
>Migrations are a feature of Active Record that allows you to evolve your database schema over time. Rather than write schema modifications in pure SQL, migrations allow you to use an easy Ruby DSL to describe changes to your tables.

**Run the Migration** (Runs migrations for the current environment that have not run yet. By default it will run migrations only in the development environment.)

    $ rake db:migrate

**Create a model with the fields first_name, last_name, email**

    $ rails g scaffold User first_name:string last_name:string email:string
    
**Run the migration again**

    $ rake db:migrate
    
**Create a local git repository**

    $ git init
    
**Add your remote repositories**

    $ git remote add origin git@github.com:your_github/your_app.git
    $ git remote add rails_learner git@github.com:LARailsLearners/your_app.git
    
**Check out that your remotes were added**

    $ git remote -v
 
###### Push your app to your GitHub repository AND to this repository (github.com/LARailsLearners)

  **To push to your own repository you run this command: you run this command:**  
  
    `$ git push origin master`

  **To push to the LARailsLearners repository you run this command:**  
  
    `$ git push rails_learner master`
 
**If you previously created an ssh key, you'll need to approve it at:**     
  https://github.com/settings/ssh/audit/854149/policy

### Some useful reading:

**Rakefile**
+ http://jasonseifer.com/2010/04/06/rake-tutorial  
+ http://lukaszwrobel.pl/blog/rake-tutorial  
+ http://martinfowler.com/articles/rake.html  
+ http://railscasts.com/episodes/66-custom-rake-tasks

-----

## Phase 2 - Authentication / Devise - [Issue #2](https://github.com/LARailsLearners/_first_app_instructions/issues/2)

##### "Authentication is the process of establishing, and subsequently confirming, a site user’s identity. It is how an app recognises, who you are." ~ http://www.gotealeaf.com/blog/authentication-methods-in-rails

Most of us will use the very popular solution called Devise which is a Rails Gem. But use whatever method you want to use.

"Most Ruby on Rails applications require user registration and authentication mechanisms. Developing these from scratch requires a lot of time and effort – thankfully, there's Devise. Using the Devise gem, you can set up a full-fledged user authentication system within minutes." 
~ https://www.digitalocean.com/community/tutorials/how-to-configure-devise-and-omniauth-for-your-rails-application

Install Devise

##### Some resources:

+ https://rubygems.org/gems/devise/versions/3.4.1
+ https://www.digitalocean.com/community/tutorials/how-to-configure-devise-and-omniauth-for-your-rails-application
+ http://guides.railsgirls.com/devise/
+ https://teamtreehouse.com/library/build-a-simple-ruby-on-rails-application/creating-an-authentication-system/installing-devise-2
+ http://www.gotealeaf.com/blog/how-to-use-devise-in-rails-for-authentication

=====

These are very basic directions. The notice and alert messages can be made better with Bootstrap. The directions for installing Devise in the Rails Girls Guides by Piotr Steininger show you how to make it better. http://guides.railsgirls.com/devise/ Run these commands in your teminal / commandline.

### Add Devise Gem

##### Open up your Gemfile and add the Devise Gem by adding this line. 

Get the most current version here: https://rubygems.org/gems/devise/versions/3.4.1

    gem 'devise', '~> 3.4.1'

##### Install the Devise Gem.

    bundle install

#### Set up Devise in your App

    rails g devise:install

##### Once that runs Devise gives you a set of instructions to follow.

**Some setup you must do manually if you haven't yet:**

1. Ensure you have defined default url options in your environments files.  
   Here is an example of default_url_options appropriate for a development environment
   in `config/environments/development.rb`:
   
   `config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }`

   In production, `:host` should be set to the actual host of your application.

2. Ensure you have defined root_url to *something* in your `config/routes.rb`.  
     For example:

       `root to: "home#index"`

3. Ensure you have flash messages in app/views/layouts/application.html.erb.  
     For example:

       `<p class="notice"><%= notice %></p>`  
       `<p class="alert"><%= alert %></p>`

4. If you are deploying on Heroku with **Rails 3.2 only**, you may want to set:

    `config.assets.initialize_on_precompile = false`

   On `config/application.rb` forcing your application to not access the DB 
   or load models when precompiling your assets.

5. You can copy Devise views (for customization) to your app by running:

    `rails g devise:views`

=====

#### Rake devise setup task:

    rake devise:setup

  **This will:**
  + drop any existing database
  + create a new database
  + migrate the database
  + create a default user and admin

-----

## Phase 3 - Add Bootstrap - [Issue #3](https://github.com/LARailsLearners/_first_app_instructions/labels/HOMEWORK)

"[Bootstrap](http://getbootstrap.com/), a sleek, intuitive, and powerful mobile first front-end framework for faster and easier web development."

>Bootstrap is a framework that makes it easy for a developer to create a nice design for a website or web application. There are predefined css classes for creating common components such as widgets, typography elements, lists, forms, and more. The framework also provides Javascript which makes it easy to create things like modals, popovers, scrollspies, accordions, and more. Their documentation is very thorough, providing example code for most, if not all of the components that Bootstrap provides. ~ [Go Tea Leaf](http://www.gotealeaf.com/blog/integrating-rails-and-bootstrap-part-1)

**Some possibly helpful Links:**  
+ https://rubygems.org/gems/sass/versions/3.4.14
+ https://rubygems.org/gems/bootstrap-sass/versions/3.3.4.1
+ https://github.com/twbs/bootstrap-sass
+ https://www.youtube.com/watch?v=4zMgLzfprqo
+ http://www.gotealeaf.com/blog/integrating-rails-and-bootstrap-part-1
+ http://leveluptuts.com/tutorials/sass-tutorials
+ https://github.com/twbs/bootstrap-sass
