---
title: authentication
tags:
  - authentication
  - assignment
---

### Assignment based class
- using a authentication based website.
- Assignment 
	- Admin should be able to sign up
	- Admin should be able to create courses
		- Courses has a title, description ,price and image link 
		- Course should be able to be published
	- Admins should be able to edit courses 
	- Users should be able to sign up
	- Users should be able to purchase courses
	- Users should be able to view purchased courses
	- Users should be able to view all courses
- Every course selling website has a backend without authentication and a dashboard with authentication and details for the same.
- Client side and user side frontend that will be present and everything else.
- 

### soln1 :
- making i-memory stuff and a array of items that will hold that stuff 
- ADMINS , USERS and COURSES 
- and add methods to add items to it and add a middleware by passing next , that will cause the middleware to authenticate.
- userAuthentication method will check if the item exists in the array , then update else it will call the method to call the middleware for the next method.
- s