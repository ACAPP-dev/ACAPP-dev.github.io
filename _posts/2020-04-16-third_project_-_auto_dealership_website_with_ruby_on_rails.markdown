---
layout: post
title:      "Third Project - Auto Dealership Website with Ruby on Rails"
date:       2020-04-16 17:53:44 +0000
permalink:  third_project_-_auto_dealership_website_with_ruby_on_rails
---


Hi everyone!  It is the 4th week of the pandemic lockdown and I’m finishing my 3rd class with two more to go.  Fortunately there is minimal disruption to our classes as we are 100% online.  I’m grateful for that because learning about Ruby on Rails has been fun and challenging.  Plus it helps keep me busy during this crazy time.

My project is an auto dealership with features for customers as well as features specific to employees or owners.  Customers can view the vehicle inventory, create a customer account, and make sales or service appointments.  Employees have administrative functions including adding vehicles to inventory,  managing employees, and viewing appointments that customers created.

My goal with the project was to make the website as usable as possible – similar to how a real world auto dealership website would work.  Some of my challenges included designing and structuring the website, adding search and filter functionality, and providing the administrative functionality.

As with many things in life, planning and design were a challenging (and important) aspect of my project.  I spent quite a bit of time planning out the tables and features and found that the actual development definitely went smoother in the areas where my planning was better.

A challenge I faced was how to implement searching and filtering the vehicle inventory (index view).  I wanted to keep the logic out of the controller by using class methods in the vehicle model.  It was tough to figure out how to do this, but the actual implementation was relatively simple:

Step 1: Create a custom form in a view that submits a GET request (rather than the default POST or PATCH request): 

```
<%= form_tag vehicles_path, method: ‘get’ do %>
   <%= text_field_tag :’search’ %>
   …
```

Step 2: Structure the vehicles_controller to call a Vehicle class search method: 

```
if !params[:search].blank?
   @vehicles = Vehicle.search_vehicle(params[:search])
	 …
```

Step 3: Create the class method .search_vehicle in the model (vehicle.rb) that will return all vehicles that meet this criteria:

```
def self.search_vehicle(search)
    where(“vehicle_search LIKE ?”, “%#{search}%”)
end
```

This is a database query that returns all objects that contain the search term.  The LIKE keyword means only a partial match is needed.  The % is needed to insure text before and after any matching text is ignored.

Note that the field ‘vehicle_search’ is a combination of the vehicle year, make, and model (i.e. "2017 Porsche 911") to enable easier searching.  I could have just as easily used the vehicle description field if I made sure it always contained this information.

No other change to the index view is needed as the @vehicles instance variable contains just the matching vehicles instead of all vehicles in inventory.

I was also able to set up similar functionality to sort the vehicle inventory by price, make, or year.  For example, to sort by price I used the following:

Step 1: Make a custom link in the view that adds a param[:order_by] to the get request:

`<%= link_to “Order by Price”, vehicles_path(order_by: ‘price’) %>`

Step 2: Set up a method call in the vehicles_controller:

`@vehicles = Vehicle.order_by_price`

Step 3: Create a class method in the model vehicle.rb to return the vehicle inventory in the specified order:

```
def self.order_by_price
		order(price: :asc)
end
```

Another challenge with my project was namespacing all the admin functions.  To accomplish this I followed these steps:

Step 1: Set up namespaced routes in routes.rb like the following:

```
namespace :admin do
		resources :vehicles
		…
end
```

This created routes like the following:

`new_admin_vehicle --> to create a new vehicle`
`edit_admin_vehicle -->  to edit a vehicle`

Step 2: Create controllers and views under the admin folder:

The vehicles controller for example would be in: app/controllers/admin/vehicles_controller.rb

The vehicle admin show view would be in: app/views/admin/vehicles/show.html.erb

This enabled me to follow RESTful conventions while keeping admin functions separate.

One advantage of this structure was the ability to use a different layout for admin views.  Rails provides a default layout that can contain a navigation bar or other formatting that will stay consistent on all views.  I set up the customer navigation bar and formatting on the default application.html.erb layout.  For the admin navigation bar and formatting, I set up a second layout called admin.html.erb.  Then all I had to do is add the statement “layout ‘admin’” to the admin controllers.  The application layout would then be replaced with admin in all the views called by this controller.

I learned a lot in my Ruby on Rails class and making this project.  I love being able to put together full featured web apps.  So far we’ve concentrated mostly on the ‘back end’ / server side development.  I’m looking forward to our next class on Javascript which will focus more on ‘front end’ / user side interactive functionality. And hopefully getting out of lockdown mode soon!

