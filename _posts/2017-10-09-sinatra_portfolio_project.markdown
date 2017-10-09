---
layout: post
title:      "Sinatra Portfolio Project "
date:       2017-10-09 15:31:46 -0400
permalink:  sinatra_portfolio_project
---


The weather's cooling down, sweaters are coming out, and I’m at that point where things are finally coming together with my coding. Ah, how I love Autumn. Making my way through the Sinatra module over these past few weeks has been quite a challenge, but I have to say my favorite part was the code names and puns that came with using Sinatra and Shotgun. Besides constantly hanging with Gob Bluth, I learned a lot about MVC and CRUD structuring, and can’t wait to see how Rails will take it to the next level. 

**Coming up with a Topic**

This project's requirements were to create a MVC Sinatra application with associating models, user accounts, and user input validation. At first my idea was for a user to login and input a list of tasks to complete, but because I am a novice and didn’t realize how much more complex it could get in code, I decided to step it up a notch. What if I could have two types of users, say an Employer and an Employee, and each user account interacts with it's associating account. 

The employer user could login to an account and post tasks for their employee, and then the employee user could then login into their account to view these assigned tasks and check them off as complete. The completed task list would then be updated in both the employer's and employee's account. And just like that, TaskiT, a virtual micromanagement application, was born. 


**Models**

After setting up all my files to configure my environment, gems, and rake, I was ready to create my database tables and models. I created three tables for my three class Models of Employer, Employee, and Task, and then used rake to autogenerate migrations for each table in my database. 

 `rake db: create_migrations NAME=create_employers `
 
 `rake db: create_migrations NAME=create_employees `
 
 `rake db: create_migrations NAME=create_tasks `
 
I then set up each model to have associations with each other: 
* An employer has many employees, and an employee belongs to an employer.
* An employee has many tasks, and a task belongs to an employee. 


**Password Authentication with bcrypt**

Each user would sign up with a username, email, and password. These three items would get stored in the database, in their associating columns. But it is important to encrypt each password for security purposes, and a great tool for this is bcrypt. All you need to do is install the bcrypt gem, set the password column in the database to `:password_digest`, and add `has_secure_password` in the class model. Now both the employee and employer can create passwords securely.  


**ApplicationController**

This rendered the homepage for my application. Here, the user can choose to continue as an employer or an employee.
	

**EmployerController and Views**

This controller holds the routes to allow the employer to do the following:
1. Signup/Login
2. View list of employees
3. Click on an individual employee to access their show page
4. Create a new task that would be saved with an employee_id 
5. Click on an individual task and either update or delete it
6. Logout

**EmployeeController and Views** 

This controller holds the routes to allow the employee to do the following:
1. Signup/Login--user sees a list of employers and can select their employer. This would set the employer_id to that employee.
2. View a list of tasks that was created by the employer. 
3. Check the tasks that they completed, and submit the form. The tasks that were checked would be deleted.
3. The list of tasks would be updated for both the employer and employee.
4. Logout
 

**App in Action**

Once everything was set up correctly, it was really cool to see it in action. Tasks were being created, read, updated and deleted by two different users, and I can officially check building a Sinatra application off of my task list. 


