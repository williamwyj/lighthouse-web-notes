# W10D01 - Rails Review

### To Do
- [ ] "Rails Week" Conversation
- [ ] MVC Review
- [ ] Rails Libraries
- [ ] Quickly build simple Rails App
- [ ] Nested Resources
- [ ] Scaffold generator

### Rails Week Convo
* Like the way Ruby looks (very clean)
* Automation of Rails (so many steps) maybe too auto-magical?
* AR is great!

### MVC - Model View Controller
* Model = database interaction layer
* View = UI, erb
* Constroller = connect the model with the view
* Routing = directs incoming requests (MVCR)

Browser > Webserver > routes > dispatcher > controller > model > controller > view > controller > browser

### Rails
* A collection of different libraries
* Active Record - querying the database, migrations, seeding
* Action View - templating engine, helpers (form_for, link_to)
* Action controller - controllers
* Action Dispatch - dispatcher, communicates between router and the controller
* Action Cable - web sockets for Rails

## Example Rails App
hitchhikers to twin peaks
* rails s - start rails server, rails new my-app --database=postgres < create new rails app with postgres db
* Gem file - add dependency gems add in development gem < bundle install to install dependencies
  - gem 'faker'
* rails c < rails console
  - starts up everything except the rails server
  - eg, Faker will output Faker
  - Faker::Movies::HitchhikersGuideToTheGalaxy.character() < generate a random name from the gem library
* rails g < list commands for rails generator

### create database model
* rails g model Location
  - generate a migration file, test files, Model
* rails g model Planets
  - create planet need to be before create location, the one in the one to many relationship also need to be created first
  - rename migrate file so it is run first, migration files are run in alphabetical order
``` planets migration file
class CreatePlanets < ActiveRecord::Migration[6.1]
  def change
    create_table :planets do |t|  #symbols are objects as close to primitive as possible string comes with many overhead functions attached
      t.string :planet_name
      t.string :species
    
      t.timestampes
    end
  end
end

# locations
class CreateLocations < ActiveRecord::Migration[6.1]
  def change
    create_table :locations do |t|  
      t.string :character
      t.string :location
      t.string :quote
      
      t.references :planet, index: true, foreign_key: true # want to index foreign keys, improves speed of queries, slow down inserts
      
      t.timestampes
    end
  end
end
```
* rails db:migrate - generate db

* seeds of fake data

```
puts "Starting seeding..."

# create the planets
puts "creating planets
10.times do
  Planet.create(
    planet_name: Faker::Movies::HitchhikersGuideToTheGalaxy.planet,
    species: Faker::Movies::HitchhikersGuideToTheGalaxy.specie
  )
end

#fetch the planets
puts "fetching planets"
planets = Planet.all

#create the locations
puts "creating locations"

50.times do
  Location.create(
    character: Faker:TvShows::TwinPeaks.character,
    location: Faker:TvShows::TwinPeaks.character,
    quote: Faker:TvShows::TwinPeaks.quote,
    planet_id: planets.sample # grab a random element from the array
  )
end


puts "All done!!!"
```
* models

```
class Planet < ApplicationRecord
  has_many :locations #plural, this enables active record to recognize the relationship between the 2 tables, eg planet=Planet.all, planet.locations return the locations of all planets in an array of arrays
end

class Location < ApplicationRecord
  belongs_to : planet #singular
end

```

* routes

```
Rails.application.routes.draw do
  resources :planets 
  
  resources :locations, only: [:show, :index]
  
  resources :planets do  #embed the locations routes in the planets
    resources :locations
  end
end
```

* controller
  - rails g controller planets

```
class PlanetsController < ApplicationController
  def index
    @planets = Planet.all #instance variable, will be available inside views
  end
end

class LocationsController < ApplicationController
  def index
    @planet = Planet.find(params[:planet_id])
    @locations = @planet.locations
  end
end
```

* views

- planets view
``` index.html.erb



<% @planets.each do |planet| %>
  <div class="planet">
  <h2> Planet name:<%= planet.planet_name %></h2>
  <h2> Species: <%= planet.species %></h2>
  <%= link_to "Locations for this planet", planet_locations_path(planet) %>
<% end %>

```
- locations view
```

<h1>All the locations for <%= @planet.planet_name %>
<%= link_to "Planets", planets_path %> #can also use '/plants' but need to update if name space changes, planets_path is a helper method that point to this page

<% @locations.each do |location| %>
  <div class="location">
    <h2>Character: <%=location.character%></h2>
    <h2>Planet: <%= location.planet.planet_name %></h2>
<% end %>
```
### Scaffold Generator

* rails g scaffold ice_cream
  - creates all rails feature such as controllers, views with html pages already implemented, routes, 

# W10D2


