---
layout: post
title:      "Rails Fitness App"
date:       2019-05-23 20:56:38 -0400
permalink:  enter_your_title_here
---


For our third portfolio project, we were asked to create a second web application with a MVC architectural pattern but this time use Ruby on Rails. Rails is a powerful framework that allows users to build very comprehensive web applications. 

The requirements for the project were more extensive requiring at least one has_many relationship, at least one belongs_to relationship, at least two has_many through relationships, at least one many-to-many relationship that includes at least one user submittable attribute other than its foreign keys that can be submitted by the app's user, ActiveRecord scope methods and validations, and the ability to be able to sign in via a third party like Facebook or Github. 

For this project I built an application for creating custom workouts that can be seen and reviewed by other users. This required creating classes for users, workouts, exercises and reviews as well as a join table to join workouts with exercises. Below are the classes and associations that were created. 

```
class User < ApplicationRecord
    has_many :workouts
    has_many :reviews

class Workout < ApplicationRecord
    belongs_to :user
    has_many :workout_exercises
    has_many :exercises, through: :workout_exercises
    has_many :reviews
 
class Exercise < ApplicationRecord
    has_many :workout_exercises
    has_many :workouts, through: :workout_exercises
	
class Review < ApplicationRecord
    belongs_to :user
    belongs_to :workout
	
class WorkoutExercise < ApplicationRecord
    belongs_to :workout 
    belongs_to :exercise 
```
	
Another requirement was to use nested routes for for index, show, and new.  For this requirment I had nested the reviews under workouts. this would display an example URL as user/1/reviews/new. Below are the routes for this app.

```
get '/signup', to: 'users#new'
  post '/signup', to: 'users#create'

  get '/login', to: 'sessions#new'
  post '/login', to: 'sessions#create'
  delete 'logout', to: 'sessions#destroy'

  get '/auth/github/callback', to: 'sessions#github'

  resources :users
  resources :workouts

  resources :users, only: [:show] do
    resources :workouts, only: [:index]
  end

  resources :workouts, only: [:show] do 
    resources :reviews, only: [:new, :create, :index]
  end

  root 'static#home'
  get '/home', to: 'welcome#home'
```

Controllers created for this application include users, sessions, workouts, reviews, and a welcome/static for the home page depending on being logged in or not. 

This was a difficult but enjoyable project utilizing a lot of what we have learned so far in the Flatiron program including Ruby, Rails, HTML, CSS, Bootstrap, MySQL and Git/Github.

If you would like to see the code please take a peek [Rails Fitness App](https://github.com/tholmes59/fitness-app)

With this complete it's on to the front end with Javascript and React/Redux which I am excited about.

Thanks again for reading and Happy Coding!!


