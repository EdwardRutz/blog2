# Ruby on Rails 
[Treehouse Exercise](https://teamtreehouse.com/tracks/rails-development)

##  RUBY ON RAILS 5 BASICS

### Intentional Practice & Concepts
- Create a new Rails app
- Add resources using scaffold
- Add resources indepenedently and editing views/controller as needed
- Understand how the controller loads model objecs from the database and populates a view with them
- Database: Use a migration to add additional parameters to the Model/fields to the database.
  - Update the controller and necessary views to support the new attribute
- Rails Console: Use the Rails Console to create, read, update and delete model objects
- Security: Understanding of how Strong Parameters protect database from unauthorized changes.

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
- Strong Parameters prevent unauthorized changes
- Strong parameters is a list of parameters in every controller which the controller will accept.
- This prevents users from adding parameters that give them too many permission on the site.
- Rails Strong Parameters prevents the body parameter from writing to the database. We need to add the body field to the list of approved parameters.
- The create method in post_controller.rb calls the post_params method. We need to add the body parameter to this method.

```ruby
def create
    @post = Post.new(post_params)
    ...
end
```

- Add the body parameter to post_param method in the post_controller.rb

```ruby
    # Never trust parameters from the scary internet, only allow the white list through.
    def post_params
      params.require(:post).permit(:title :body)
    end
```



================================



## RAILS ROUTES AND RESOURCES

### Intentional Practice & Concepts
- Create resources from scratch: Models, Views, Controllers
- Modify routes as needed


###  A Route to an Index Action 
- Rails lets you set up "routes" for requests, so that you can send a particular request to a controller that can handle it.
- Set up a route, a controller, a view, and a model for our Pages from scratch without using scaffold
- Use ```bin/rails routes``` to view all routes used by the application

#### Creating a Route
- Set up a route to the pages controller, then create a pages controller.
- To set up a route to the index of all Page objects, add this in config/routes.rb:

```get '/pages', to: 'pages#index'```

- GET, a request to view a page uses ```GET```
- As an arguement to the get method, provide a path this route shoud match as a string: ```/pages```
- The next GET arguement is a hash giving keys and values: ```to: 'pages#index'```
  - The to: key specifies which controller and action the request is sent to  
- Instance methods of a class are marked with a hashmark(#)
- Results: The request for pages is routed correctly but no Pages controller exists.

#### Creating a Controller
- Use the controller generator to create a pages controller to handle request for pages
- Controller names are plural
- Don't put "controller" in the name because rails automatically adds it.
- To delete, type ```rails destroy ControllerName```
- Generate Controller:  ```bin/rails generate controller Pages```
- Results:  Pages controller is found but there is no index action

##### Add an Index Action
- In pages_controller.rb add a method

```
def index
end
```

#### Creating a View
- Create an index View for the pages controller
- In app/views/pages create the file index.html.erb
- Add basic html to the page
- Git Log shows all commits ```git log```

#### Creating a Model
- The /pages path needs to show a list of blog pages. Set the controller up to load Page data to be include in the template.

- Run the model generator from the terminal:  ```bin/rails generate model ModelName attr1:type attr2:type```
- ...where ModelName is the name of the model class to create (like Post), attr1, attr2, etc. are the names of attributes (like title or body), and each type entry is the type of the attribute (like string or integer).
- Create a list of the blog pages on the pages view.
- In the pages_controller load page data to include in a template
- Create a method to load all page data and store it in an instance variable 
- In pages_controller.rb, add:

```ruby
def index
  @pages = "Page.all"
end
```
- Results: Receive an error because the model class is not created yet.

##### Create a Model Class
- Use the rails model generator to create a model class, source files and migration file to create records to hold the data.

```ruby
  bin/rails generate model Page title:string body:text slug:text
```

- The slug attribute is used to make human readable urls
- Results: migration is created but database isn't updated until we run ```rails db:migrate```

#### Add Records Via Rails Console
- We created a Page model class, but the list of pages is still blank. Part of the problem is that no "Page" records exist now. Go to the Rails console and fix that...
- Start rails console:  ```bin/rails c```
  - both ```rails console``` or ```rails c``` work.

- ```Page.all``` is empty because there are no records.
- Create records to go in model
- Create a new variable to hold the Page object and create a new empty page object to go in it.

```page = Page.new```

- Next, assign attributes...
```ruby
page.title = "About this Blog"
page.body = "Here I will share my notes about Rails."
page.slug = "about"
page.save
```
- Create two more page objects...

```ruby
page2 = Page.new
page2.title = "My Resume"
page2.body = "Edward Rutz\n \n Ruby Developer \n \n Likes hiking up mountains."
page2.slug = "resume"
page2.save

page3 = Page.new
page3.title = "My Robots"
page3.body =  "Zorgbot\nMoon Explorer\An old robot"
page3.slug = "robots"
page3.save

Page.all
```

#### Populating the View
- We set up our controller's "index" method to load all "Page" objects into the "@pages" instance variable. 
- We created "Page" records for it to load. 
- We still don't see any page data. That's because we haven't set up the our view template to display the pages we've loaded. To do that, we're going to use ERB to embed some Ruby code into our HTML.

##### Notes...
- Most text in an ERB template is copied to the output verbatim.

  ```<p>I'll appear in the output exactly as I do here.</p>```

- But Ruby code within ERB tags gets evaluated instead of being copied directly to the output.
- Code within output ERB tags (<%= %>) is evaluated, and the result is embedded into the output. This code will output the current time:

    ```<p>The current time is: <%= Time.now %></p>```

- Code within regular ERB tags (<% %>, without an equals sign) is also evaluated, but is not included directly in the output. It can be used to influence the result of output tags.

- If you place a conditional within regular tags, text within the conditional will only be output if the condition is true. This code will include You passed! in the output:

```ruby
    <% grade = 97 %>
    <% if grade > 60 %>
      You passed!
    <% end %>
```

- This code will not:

```ruby
    <% grade = 54 %>
    <% if grade > 60 %>
      You passed!
    <% end %>
```

- If you place a loop in regular ERB tags, text within the loop will be output repeatedly.
- This code will output 4 <p> elements with the text 0 fish, 1 fish, 2 fish, and 3 fish:

```ruby
  <% 4.times do |index| %>
    <p><%= index %> fish</p>
  <% end %>
```
##### Add Page Content to the Site
Add page content to index.html.erb:

- Using ```<%= @pages.first.title %>``` only shows first title.  A loop is needed:

- Assuming @pages contains a collection of Page objects, this code will output the title of each Page:

```ruby
  <% @pages.each do |page| %>
    <p>
      <%= page.title %>
    </p>
  <% end %>
```
##### Summary of the Process
- Here is how the request gets processed from beginning to end
- A route receives the http GET request and directs it to the proper controller and action.
- The route directs the "/pages" path to the pages_controller's "pages#index" action

    ```get 'pages/', to: 'pages#index'```

- The "index" method loads the collection of page model objects from the database and assigns the collection to an instance variable, @pages...

```ruby
  def index
    @pages = Page.all
  end
```

- By default, the pages_controller looks for the app/views/index.html.erb 
- Within the index template, we loop over each of the page objects and output an html paragraph with the page.title

```ruby
  <h1>Blog Pages</h1>

  <% @pages.each do |page| %>
    <p><%= page.title %></p>
  <% end %>
```



###  A Route to a Read Action 
###  Routes to Create Actions 
###  Routes to Update Actions 
###  A Route to a Delete Action 















