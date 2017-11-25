# Creating a Blog App

Exercise, creating a variation of the basic blog Rails app.

See notes in [DOCS-BLOG2/Rails-Notes.md](https://github.com/EdwardRutz/blog2/blob/master/DOCS-BLOG2/Rails-Notes.md)

## Intentional Practice & Concepts
- Create a new Rails app
- Add resources using scaffold
- Add resources indepenedently and editing views/controller as needed
- Understand how the controller loads model objecs from the database and populates a view with them
- Database: Use a migration to add additional parameters to the Model/fields to the database.
  - Update the controller and necessary views to support the new attribute
- Rails Console: Use the Rails Console to create, read, update and delete model objects
- Security: Understanding of how Strong Parameters protect database from unauthorized changes.

=====================================================

## Installing the App on Your Local Machine

### Dependencies
- Ruby version: 2.4.2
- SQLite 3.19.3

### Getting Started
- Clone repository: ```git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY```
- Install gems ```bundle install --without production```
  - "--without production" skips the PostgreSQL gem (pg) in development and use SQLite for development and testing.
- Migrate database ```rails db:migrate```
- Verify app is working correctly by running tests written duing TDD ```rails test```
- If tests pass, run rails server ```rails server```
- Use browser to open ```127.0.0.1:3000/hello```


## REFERENCES
- Exercise from https://teamtreehouse.com/library/ruby-on-rails-5-basics
- [Routing](http://guides.rubyonrails.org/routing.html)








