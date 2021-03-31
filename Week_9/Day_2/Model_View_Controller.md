# Model-View-Controller (MVC)

## What is it?
* A common way of structuring a GUI by enforcing a **separation between the data in the application and the code** used to display it

## MVC Flow
When interacting with a Rails application:
  1. A browser sends a request
  2. Received by a webserver
  3. Passed onto a Rails *controller* - in charge of what to do next
    * Can render a *view* - template that gets converted to HTML and sent  back to browser
    * Can interact with a *model* - a Ruby object that represents an element of the site (eg. a user), and communicate with database
      * After invoking model, controller will then render the view, then
    * Return the complete web page to browser as HTML

## MVC In Action

Refer to this (image)[https://www.railstutorial.org/book/toy_app#fig-mvc_detailed]

1. The browser issues a request for the /users URL.
2. Rails routes /users to the `index` action in the Users controller.
3. The `index` action asks the User model to retrieve all users (`User.all`).
4. The User model pulls all the users from the database.
5. The User model returns the list of users to the controller.
6. The controller captures the users in the `@users` variable, which is passed to the `index` view.
7. The view uses embedded Ruby to render the page as HTML.
8. The controller passes the HTML back to the browser.

Step 2: The Rails routes, with a rule for the Users resource.
```rb
# config/routes.rb

Rails.application.routes.draw do
  resources :users
  root 'users#index'  # => adding root route for users
end

# These codes set up the table of URL/action pairs in later steps
```

### RESTful routes in Rails

| HTTP request | URL           | Action    | Purpose                       |
|---	         |---	           |---	       |---	                           |
| `GET`  	     | /users  	     | `index`   | page to list all users        |
| `GET`        | /users/1  	   | `show`  	 | page to show user with id `1` |
| `GET`  	     | /users/new    | `new` 	   | page to make a new user       |
| `POST`       | /users  	     | `create`  | create a new user             |
| `GET`        | /users/1/edit | `edit` 	 | page to e dit user with id `1`|
| `PATCH`  	   | /users/1  	   | `update`  | update user with id `1`       |
| `DELETE`     | /users/1  	   | `destroy` | delete user with id `1`       |


Step 6: The view for the users index.
```rb
# app/views/users/index.html.erb

 <p id="notice"><%= notice %></p>

<h1>Users</h1>

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Email</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <% @users.each do |user| %>
      <tr>
        <td><%= user.name %></td>
        <td><%= user.email %></td>
        <td><%= link_to 'Show', user %></td>
        <td><%= link_to 'Edit', edit_user_path(user) %></td>
        <td><%= link_to 'Destroy', user, method: :delete,
                         data: { confirm: 'Are you sure?' } %></td>
      </tr>
    <% end %>
  </tbody>
</table>

<br>

<%= link_to 'New User', new_user_path %>
```