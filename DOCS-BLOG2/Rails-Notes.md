# Rails Track
[Treehouse](https://teamtreehouse.com/tracks/rails-development)

##  RUBY ON RAILS 5 BASICS

### Creating an App

#### The MVC Pattern
- The models write Ruby objects to the database, and read them out again later.
- The views show data to users, most often in the form of HTML webpages.
- Controllers respond to requests from users, usually by coordinating the model and the view.

#### Create a new app
```rails new blog2```


#### Running a Server
- Make a habit of running ```bin/rails``` to make sure you are running the same version of rails. 
  - This runs rails from the ```bin``` in the directory
  - Running just ```rails``` could run anyversion that is on the system.

#### Our First Resource
- A resource is a type of object users to 
  - Create instances of it
  - Read data for
  - Update data for
  - Delete Instances of it 

#### Creating a Resource with Scaffold
- Create a resource, generate a Model named "Post" with an attribute called "title"....
   ```bin/rails generate scaffold Post title:string```
- The ```scaffold``` command creates the model, view and controller for a resource at the same time.
- The attribute creates the fields in the model and view automatically

#### Handling Requests
Here's an overview of how Rails handles a request.
- Rails looks at the request, to figure out which code should handle it.
- The request gets routed to an action method on a "controller".
- The controller loads the resource in from database using a "model class".
- The controller renders a "view" using the model data, to generate the response content.

#### The Controller
- Methods that respond to requests are called actions
- The controller is responsible for handling the browser request. It CONTROLS the model and the view to generate a response.

#### The Model
- The model is responsible for storing and retrieving data from users of your app.
- When you call the "all" method on a model class, each database record is converted to an instance of the model class

#### The View
- The view is responsible for displaying data to your users.
- Views are usually html templates with embedded ruby.
- ERB tags begin and end with ```<% %>```

### Using the Rails Console
- Create new model objects from the terminal using Rails console
- Launch the Rails Console ```bin/rails console```
- Show all entries in the post model:  ```Post.all```
- Show the most recent record in the m ```Post.last```

#### Reading Model Objects
Methods
```
Post.all
.last
.find(id)
  Post.find(3) #shows the record with id of 3.
```

#### Creating Model Objects
- We can create new records in the database by creating new Model objects
- Create a new  post and assign it to a variable: ```post = Post.new``` 
  - Class Name, Post, is captialized.
  - The variable name is all lowercase
- Assign a title to the title attribute, ```post.title = "Hello, console!"```
- This object is in memory but not saved to database.
- Save new object to database, ```post.save```
  - The post object is saved to the database and given an ID
- View the new post database recored, ```Post.find(4)```
      ```
      post = Post.new
      post.title = "Hello, console!"
      post.save
      Post.last
      ```


#### Updating Model Objects
#### Deleting Model Objects

### Adding a Model Attribute






================================
## RAILS ROUTES AND RESOURCES
CONCEPTS: Routes, Models, Views, Controllers


###  A Route to an Index Action 
Set up a route, a controller, a view, and a model for our Pages from scratch without using scaffold
- 





###  A Route to a Read Action 



###  Routes to Create Actions 



###  Routes to Update Actions 


###  A Route to a Delete Action 















