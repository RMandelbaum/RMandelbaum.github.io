---
layout: post
title:  "CLI Data Gem Project"
date:   2017-08-28 17:15:31 -0400
---


I'm almost done with Object Oriented Ruby and SLOWLY making my way through the final projects. Everything I have learned so far is coming together in these last few projects, and it's CLI Data Gem Project time. 

**Starting a Project**

I'm sitting at a blank screen trying to decide where to begin. Usually, each project is extremely structured, but now I've got all this freedom, with too many options. I have to write a CLI Gem application from scratch, and that cursor just keeps blinking. I need to start somewhere, so I go with what is most familiar to me: English. Let's write out what I need to do and then "simply" change it into code. I know I need to create a cli that prompts a user with some sort of list, and let's them choose to view more information based on their input. I also know that I'm basing my project off a CLI Gem, so I'll probably need to figure out how to install that once I have my topic.  

**Choosing a Topic**

After creating and deleting at least three repositories, somehow I managed to stick with a project for a job I just quit. I worked way too many weekends at Smorgasburg (a food festival), where I repeatedly told customers the same information, so why not create a program that does the work for me.  

**Installing the CLI Gem**

I checked out the example projects to see the format for the gem, and had no idea how I was suppose to create one for my project until I watched the walkthrough video. Something that seemed so complex to create, turned out to be typing three words into my terminal. 

`bundle gem Smorgasburg `

And just like that, I was cooking with gas. I pushed this all up to Github, refreshed my page and my project was starting to look very official. Bless all those programmers who made this so simple. Well done. 

**Creating the CLI**

Next up was setting up my project and connecting all the files so they actually respond to each other. Thankfully, the walkthrough video explained where to require each file and that set everything up to work smoothly. Well, maybe not at first. I tried coding my CLI and nothing was working, and I kept hearing Avi say in the video to go slowly. Test each line of code, and you'll know exactly where it breaks. 
> TImes like these, going slower is always faster.

Now with my CLI class and CLI controller connected, I was ready to code. I wanted the application to begin with a welcome message and a list of the three locations. Then I would ask the user to choose one location to learn more information, and then list the time and address. The user would then have the option to view the other locations, or exit the program. I also wanted to make sure that the user's input would only work if it was valid so I included some code to ensure this.


```
 def list_locations
    #first hard code to make sure it works, then use scrape to create objects
    puts "Please enter the number to see more info of the location."
    puts "1. Smorgasburg Prospect Park"
    puts "2. Smorgasburg Williamsburg"
    puts "3. Smorgasburg Square"
 
    input = gets.strip
    index = input.to_i - 1
 
   if !index.between?(0,2)
    puts "Invalid input"
    list_locations
 
   else
     puts "Smorgasburg Prospect Park - Sunday - 11am - 6pm - address,
          Smorgasburg Prospect Park - Sunday - 11am - 6pm - address,
          Smorgasburg Square - Saturday and Sunday - 11am-6pm - address"
 
   end
```

**Scraping the Information**

My CLI seemed to be working, but it was getting information from a method that I hard coded with the list of locations.
I needed to be able to scrape the name of the location, time, and address, and each location had a separate webpage. I coded three separate methods that used nokogiri and open uri to scrape this info, and set them as objects that could be used in the CLI. Luckily whoever wrote these webpages, was a very organized coder and the html and css were nearly identical, so scraping from three different webpages was a breeze. 

```
[4] pry(Smorgasburg::Scraper)> name = doc.css("div .project-slide-description-text p").first.text
=> "Smorg Square"
```
Each method instantiated a new object that had a name, address, and time. I then pushed all three objects into an array that could be accessed in the CLI. 

```
def self.scrape_info
  locations = []
  locations << self.scrape_williamsburg
  locations << self.scrape_prospect_park
  locations << self.scrape_square
  locations
end
```

So everytime the user input a number that correlated with the specific location object, it knew to return the object's name, address, and time. 

```
  smorg = @locations[index]
    puts "#{smorg.name} - #{smorg.time} - #{smorg.address}"
   end
```
**Run Time!**

My scraper class was all set up, and now I had to test the CLI to make sure it was working properly. I ran my program and the list of locations appeared!

I entered a number of the locations, and saw all the information listed. Success! 

```
// ♥ ruby bin/smorgasburg
Welcome to your resource for Smorgasburg locations!
 1. Smorgasburg Williamsburg
 2. Smorgasburg Prospect Park
 3. Smorg Square
Please enter the number to see more info of the location.
1
Smorgasburg Williamsburg - 11am-6pm • Saturdays - 90 Kent Ave. Brooklyn NY 11211
To see more info of another location enter 'see more'. Otherwise enter 'exit.'
see more
 1. Smorgasburg Williamsburg
 2. Smorgasburg Prospect Park
 3. Smorg Square
Please enter the number to see more info of the location.
2
Smorgasburg Prospect Park - 11am-6pm • Sundays - Prospect Park – Breeze Hill (East Drive at Lincoln Rd.)
To see more info of another location enter 'see more'. Otherwise enter 'exit.'
exit
Goodbye!
```




