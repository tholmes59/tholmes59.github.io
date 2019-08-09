---
layout: post
title:      "Using Sinatra - Wine Journal App"
date:       2019-04-18 16:48:29 -0400
permalink:  using_sinatra_-_wine_journal_app
---


It’s easy to get lost in the day to day of learning how to program with everything there is to know and learn but looking back it’s amazing how in a few short months I have gone from having very basic coding knowledge to learning procedural and object oriented Ruby in depth, SQL, HTML/CSS and Git, completing the first Ruby CLI project, and learning Rake, ActiveRecord and now Sinatra.

For our second portfolio project, we were asked to create a web application with a MVC architectural pattern using the Sinatra framework. The framework utilizes ActiveRecord and SQL and the requirements included having authentications, validations, multiple models with at least one has_many and one belongs_to relationship, web forms and displays in .erb files and was controlled by an application controller. 

For my project I decided to create a wine journal that will let you keep track of all of the wines you drink and enjoy and would like to have again but never remember what they are after the fact. The application lets you create an account via a secure login and be able to create wine entries which include the wine’s name, varietal, year and price among other things which allows you to always remember that great wine you had at you’re cousins wedding!

This project required the use of the Ruby gem’s below:

```
gem 'sinatra'
gem 'activerecord', '~> 4.2', '>= 4.2.6', :require => 'active_record'
gem 'sinatra-activerecord', :require => 'sinatra/activerecord'
gem 'rake'
gem 'require_all'
gem 'sqlite3', '~> 1.3.6'
gem 'thin'
gem 'shotgun'
gem 'pry'
gem 'bcrypt'
gem "tux"
gem 'rack-flash3'
gem 'sinatra-flash'
```

You must use Sinatra and ActiveRecord and all of its built in functionality along with bcrypt to create salted, hashed passwords, and flash in order to use flash messages with your validations. 

This application is comprised of 2 models; a User model and a Wine model. The User model has many wines and a Wine belongs to a user. 

```
class User < ActiveRecord::Base 
  has_secure_password
  validates :username, presence: true, uniqueness: true
  validates :email, presence: true, uniqueness: true
  has_many :wines
end 
```

```
class Wine < ActiveRecord::Base 
  belongs_to :user
  self.inheritance_column = nil
end
```

The User model also includes built-in ActiveRecord helper methods for the validation of the uniqueness of usernames and emails and the authentication of passwords.

To go along with the models I ran migrations to create tables for Users and Wines. In order to use bcrypt you must use password_digest in the users table to store the passwords. The bcrypt hashing function allows us to build a password security platform that scales with computation power and always hashes every password with a salt. This is a very powerful tool that all but ensures the protection of users passwords.

```
class CreateUsersTable < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :username
      t.string :email 
      t.string :password_digest
    end 
  end
end
```

```
class CreateWinesTable < ActiveRecord::Migration
  def change
    create_table :wines do |t|
      t.string :wine_name
      t.string :type
      t.string :varietal
      t.string :region
      t.string :year 
      t.string :price 
      t.string :tasting_notes
    end 
  end
end
```

In addition to the application controller I mentioned earlier, I created a users controller and a wines controller. Each controller creates the appropriate RESTful routes and builds the methods for CRUD functionality.

I also created .erb files for Users and Wines under Views to hold the web forms to create and login users, and create, display, edit and delete wines.

I found this to be a really enjoyable project which brought together everything I had learned up until now by allowing me to take and apply this knowledge and actually put it to use in creating a web based application. After completing this I am very excited to move on to Rails and see what more features are available for the next application!

You can review my project via the links below:

[Video tutorial](https://drive.google.com/open?id=11Izh6OFqN0lCfWAXpJ5wLRwA_NA9jEes)

[Github repo](https://github.com/tholmes59/sinatra-wine-app)


Thanks for reading and Happy Coding!!

