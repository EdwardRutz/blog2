# Ruby on Rails 
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
- To exit Rails Console type ```exit```

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
- After retrieving a model object from the database, we can modify its data and update the database record. 
- This is much the same as working with a new model object; we assign new values to the existing object's attributes, and call "save" on it.

To update a field such as the posts's title:
- Get a collection of all the Post objects by calling ```Post.all```
- Find the "id" attribute of the record we want to update, and retrieve it with the "find" method. 
- Assign the object we get back to a variable: ```post = Post.find(4)```
- Change the title: ```post.title = "I've been updated!"```
- These changes only exist in your computer's memory, not in the database. Call the "save" method on the object to save it to the database: ```post.save```
    
    ```
    Post.all
    Post.find(4)
    post = Post.find(4)
    post.title - "I've been updated!"
    post.save
    ```

#### Deleting Model Objects
- Users need to be able to delete data and remove records from the database. 
- Load up a particular instance of the model and call the "destroy" method on it.
- Load instance using its ID, and assign it to a variable: ```post = Post.find(7)```
- Call the "destroy" method on that object: ```post.destroy```
- Observe the SQL query that deletes the record from the database.
- Use the ```.destroy``` method and not the ```.delete``` method

    ```
    Post.all
    post = Post.find(4)
    post.destroy
    Post.all
    ```
### Updating the Model: Adding a Model Attribute
- Add a field for post body to the database.
  ```rails generate migration AddBodyToPosts body:text```

- A migration is used to update the Rails database. 
- Generating the migration doesn't actually update the database. To do that, run bin/rails db:migrate.
- The migration to create the "posts" table was set up as part of the scaffold we used earlier. 
- Create the migration separately by running the "migration" generator instead of scaffold.
- The migration name is CamelCase (with each word capitalized), since it will be used as a class name.
- Using the syntax "Add<attribute name>To<table name>", the generator will set up a command to add a column to that table for us. Name it "AddBodyToPosts".
- Next specify one or more columns we want to add
  - Create "body:text" to create a "body" attribute of type "text".
- For the title, we used a type of "string". But the post body needs to be longer, so we use a type of "text" here, so that the resulting database column can hold more text.

```
rails generate migration AddBodyToPosts body:text
rails db:migrate
```
In Rails console, add body text
```
bin/rails console
post = Post.first
post.body = "This is my first post. Oh what a wonderful world it is."
post.save
Post.all
```
#### Updating Views
- Update the view to show the body field in posts.
- Open app/views/posts/index.html.erb
  - Add ```<th>Body</th>``` under the ```<th>Title</th>``` header
  - In the table body, under table data for post.title add ```<td><%= post.body %></td>```
- Add the body field to the page for the individual posts
  - Open app/views/posts/show.html.erb
  - Under the title code, add 

      ```ruby
        <p id="notice"><%= notice %></p>

        <p>
          <strong>Title:</strong>
          <%= @post.title %>
        </p>

        <p>
          <strong>Body:</strong>
          <%= @post.title %>
        </p>

        <%= link_to 'Edit', edit_post_path(@post) %> |
        <%= link_to 'Back', posts_path %>
    ```

#### Updating Partials
- "Partial" is short for "partial view". A partial contains the HTML code for the form.
- ```<%= render 'form', post: @post```
  - A call to the Render method with the arguement of 'form.' 
  - This looks up the partial 
- Partials are allow multiple pages to use the same identical element for all the pages.
- To make a partial, take any code that is identical between two pages and move it to a partial.
- Partials allow convenient consistency across the pages. Any changes to the partials will apply to all pages that use it. No more re-coding the same element on mutiple pages.
- Both the "edit post" page and the "new post" page use the partial called "form"
- An underscore at the beginning of a file name means the file contains a partial template.
- When calling render, the underscore and "html.erb" can be left off. Use only the partial name.
- Following the partial is a hatch, ```post: @post```,that sets up local variables to be used within the partial.
    ```<%= render 'form', post: @post```
- In ```<%= form_with(model: post, local: true) do |form| %> ``` the ```|form|``` holds the Ruby object representing the html form.



#### Updating Strong Parameters





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















