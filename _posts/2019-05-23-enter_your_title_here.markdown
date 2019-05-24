---
layout: post
title:      "Enter your title here"
date:       2019-05-23 20:56:38 -0400
permalink:  enter_your_title_here
---


For our third portfolio project, we were asked to create a second web application with a MVC architectural pattern but this time use Ruby on Rails. Rails is a powerful framework that allows users to build very comprehensive web applications. 

The requirements for the project were more extensive requiring at least one has_many relationship, at least one belongs_to relationship, at least two has_many through relationships, at least one many-to-many relationship that includes at least one user submittable attribute other than its foreign keys that can be submitted by the app's user, ActiveRecord scope methods and validations, and the ability to be able to sign in via a third party like Facebook or Github. 

For this project I built an application for creating custom workouts that can been seen and reviewed by other users. This required creating classes for users, workouts, exercises and reviews as well as a join table to join workouts with exercises. Below are the classes and associations that were created. 

```
class User < ApplicationRecord
    has_many :workouts
    has_many :reviews

end

class Workout < ApplicationRecord
    belongs_to :user
    has_many :workout_exercises
    has_many :exercises, through: :workout_exercises
    has_many :reviews

 end
 
 class Exercise < ApplicationRecord
    has_many :workout_exercises
    has_many :workouts, through: :workout_exercises
		
	end
	
	class Review < ApplicationRecord
    belongs_to :user
    belongs_to :workout
		
	end
	
	class WorkoutExercise < ApplicationRecord
    belongs_to :workout 
    belongs_to :exercise 
		
	end
	```
	
![Domain Model](https://drive.google.com/open?id=1XYNEOsfAMe5Uo1pCMwsVEXWR5axOCmD4)
	
	


