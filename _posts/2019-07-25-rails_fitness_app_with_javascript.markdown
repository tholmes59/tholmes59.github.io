---
layout: post
title:      "Rails Fitness App with JavaScript"
date:       2019-07-25 20:36:04 -0400
permalink:  rails_fitness_app_with_javascript
---


The JavaScript section has been really enjoyable and its a language I'm really enjoying which may make me a little strange! After learning the basics of JS syntax, principles, data structures, looping and iteration, scope, functions JS objects, and consuming and building API's, it is time for the fourth project which is to take our existing Rails application and add dynamic features using JavaScript and the JSON API. 

The first step is to create a bare clone of the Rails app repo and rename it. From there I needed to create the JavaScript manifest in the application.js file as per the below.

```
//= require rails-ujs
//= require activestorage
//= require jquery
//= require_ujs
//= require_tree .
```

This will create an asset pipeline for all of the .js files in order to keep the code organized in different files but allows Rails to keep track of them all. 

Then I needed to add the below gems to the gemfile to allow the use of JQuery and to create Active Model Serializers which provides a convention-based approach to serializing resources in a Rails.

```
gem 'jquery-rails'
gem 'active_model_serializers'
```

After running `bundle install` I used the serializer generator to create serializers for each of the existing models and copied over the table names from the database as attributes. An example of one of my serializers is below.

```
class UserSerializer < ActiveModel::Serializer
  attributes :id, :username, :email

  has_many :workouts
  has_many :reviews
  
end
```

The specifications for this project require rendering an index and show page via JavaScript and an Active Model Serialization JSON Backend. To start I had to update the index and show controller methods to allow the rendering of JSON by adding the `respond_to` method below.

```
respond_to do |f|
            f.html
            f.json {render json: @workouts}
end
```

This project also required the use of  object oriented JavaScript by creating constructor functions like the one below.

```
function Workout(workout) {
    this.id = workout.id;
    this.workout_name = workout.workout_name;
    this.workout_description = workout.workout_description;
    this.workout_instructions = workout.workout_instructions;
    this.exercise = workout.exercises.map(json => new Exercise(json));
    this.workout_exercise = workout.workout_exercises.map(json => new WorkoutExercise(json));
    this.createdAt = new Date(workout.created_at);
    this.user = new User(workout.user);
    this.review = workout.reviews.map(json => new Review(json));
}
```

Lastly, the specifications required the use of an Object.prototype function and the creation of event listeners for the Index and Show pages and the submission of a form. Below are my examples for the Index page.

Object.prototype function:
```
Workout.prototype.formatIndex = function() {
    let workoutHtml = `
    <a href="/workouts/${this.id}" data-id="${this.id}" class="show-link">${this.workout_name}</a><br>
    ${this.workout_description}<br>
    by: <a href="/users/${this.user.id}">${this.user.username}</a> on ${this.createdAt.toLocaleDateString()}<br><br>
    `
    return workoutHtml;
}
```

Event handler function:
```
const bindClickHandlers = () => {
    $('#all-workouts').on('click', (e) => {
        e.preventDefault()
        fetch('/workouts.json')
        .then(res => res.json())
        .then(workouts => {
            $('#app-container').html('<h1>Pick a Workout!</h1>')
            workouts.forEach((workout) => {
                let newWorkout = new Workout(workout)
                let workoutHtml = newWorkout.formatIndex()
                // console.log(workoutHtml)
                $('#app-container').append(workoutHtml).addClass('container workouts-index')
            })
        })
    })
```
		
Similar functionality was created for the Show pages and for a form submission. 
		
This was another very challenging but also very rewarding project and my first taste of the exciting world of front end development. I'm really excited to continue more advanced learning of JavaScript as well as diving into React/Redux. 

You can view the full repo of this project here [fitness-app-js](https://github.com/tholmes59/fitness-app-js)

Thanks again for reading and Happy Coding!!
		
