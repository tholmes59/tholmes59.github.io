---
layout: post
title:      "CLI Gem Project - Boston Celtics"
date:       2019-02-19 17:41:55 -0500
permalink:  cli_gem_project_-_boston_celtics
---


After finishing the Introduction, Procedural and Object Oriented sections of Ruby in the Flatiron curriculum it is time to do the first project. Unlike all of the labs that have been completed along the way, the project is exciting because I have to create the program from scratch. This involves setting up the environment, creating a Github repository, finding a website to scrape data from, and building the objects. Also unlike the labs there is no test code to serve as a guide and you are required to come up with your own idea on what to build. Very exciting!

The general guidelines are to build a Ruby gem that provides a Command Line Interface (CLI) to an external data source with the CLI being composed of an Object Oriented Ruby application. Essentially we are to scrape a website for data and present it in the CLI. 

For my project I wanted to build a CLI gem that would scrape the roster of one of my favorite sports teams and present detailed information on each player. This proved difficult at first because to use the Nokogiri gem, a library to parse HTML in Ruby, the webpage cannot load with JavaScript, and websites built with JavaScript are commonplace today. But if you look around enough you will eventually find something. In my case I found the roster of the NBA’s Boston Celtics via the CBS Sports website that allowed me to scrape a list of their current roster an drill down for additional information.

So how did I do it? Lets take a look!

Step 1: Environment setup

•	In the terminal, run Bundle gem <filename> to create the gem. It will ask you if you would like to include rspec, a license, and a code of conduct, which you will. Some words of wisdom though, when you create the filename, use underscores and not dashes such as <file_name> and not <file-name>. This will create a better layout for the file structure and reduce issues down the line. For this project I named it celtics_roster_cli_project. 

•	You also need to create a Github repository. Go to your Github, create a new repository using the create new repository feature. You will want to use the same name you used for your gem. From here you will then run the given commands in your program file in the terminal.

•	Back in the programs bin file, you will need to create the file that will run the program. Make sure within it requires the correct libraries and has the proper command privileges. Another tip, if you create the gem using the above setup process within the learn.co IDE, you will not be able to create an environment.rb file under a config folder. You will need to rename the <file_name>.rb file that is automatically created in the lib folder and require you libraries there.

•	Lastly, in <filename>.gemspec you need to add your gem dependencies.


Step 2: Determine the scrape 

•	Before you begin coding, you will want to make sure you have found a website that you can use to pull the scraped data into you program. Try finding sites that have relatively easy to understand HTML/CSS that will allow you to find data presented in a nicely crafted list from which you can further drill down to another webpage to find additional information.

•	For this project I was able to find the roster of the of the Boston Celtics which allowed me to list out the players and drill on layer deep to their individual pages where I was able to pull additional information. 
See [Celtics Roster](https://www.cbssports.com/nba/teams/BOS/boston-celtics/roster/)

•	You will need to get very comfortable with the developer tools in Google Chrome to dig through the HTML/CSS of the data you would like to pull and find the right CSS selectors that you will need in your scrape.

Step 3: Create the classes

For this program I created three classes, the Scraper class, the Player class, and the CLI. All three classes are related to each other and I connected them using the “::” syntax.

•	The Scraper class pulls the roster data, specifically the player names and url, from the CBS Sports site and allows the creation of the individual players.

•	The Player class creates the player objects and stores them in a class array that will be called upon by the CLI. A new player is initialized with a name and a url and that url is used to pull the additional player information and statistics. 

•	The CLI class creates the user interface and pulls the requested data from the Player object. 

Step 4: Run the program

•	Once you have configured your environment, created you repository, found the data to scrape and created your classes, the moment of truth arrives! Run the program through the bin file you set up earlier. With any luck it all runs smoothly!

Conclusion:

I’ll admit when I first read the requirements of this project I panicked and wondered how I would ever be able to complete it. I think the key is to do as much research as you can to learn about setting up your environment, building objects, creating CLI’s and understanding how to scrape a website using Nokogiri. Watch tutorials, read code examples, read articles, ask questions and use your best friend Google! Don’t try to do the whole project at once. Try to build momentum by doing one step at a time. 

You can review my project via the links below:

[Video tutorial](https://drive.google.com/open?id=1w_FLmOJRxkcMyClpgJa7no9NMzDkVNPL)

[Github repo](https://github.com/tholmes59/celtics-roster-cli-project.git)

Whatever you end up doing just have fun with it! Happy coding!!




