!SLIDE 
# Mongoid #

Nguyen Vu Nguyen

github.com/yetanothernguyen

says.com

!SLIDE bullets incremental highlight-rb
# What is Mongoid? #

* Object Document Mapper for MongoDB
* Written in Ruby
* Agnostic (Rails, Sinatra or Padrino)

!SLIDE bullets incremental transition=fade 
# Why Mongoid #

* Solid documentation (mongoid.org)
* ActiveRecord-like API
* Active development
* Compatible with other popular gems
* Includes a better implementation of the MongoDB Ruby Driver (Moped)

!SLIDE
# Mongoid Document #

!SLIDE
.notes Demo creating a Person in Rails console Person.new

 	@@@ ruby
 	class Person
		include Mongoid::Document
	end

!SLIDE
.notes Demo creating a Person in Rails console Person.new and getting and setting field values
# Field Definition #

!SLIDE

	@@@ ruby
	class Person
		include Mongoid::Document
		field :first_name,  type: String
		field :middle_name, type: String
		field :last_name,   type: String
		field :location,    type: String, 
		                 default: 'KL'
		field :dob,         type: Time, 
		                 default: Time.now
	end

!SLIDE big-spacing small-list

* Array
* BigDecimal
* Boolean
* Date
* DateTime
* Float
* Hash
* Integer
* Moped::BSON::ObjectId
* Moped::BSON::Binary
* Range
* Regexp
* String
* Symbol
* Time
* TimeWithZone

!SLIDE bullets incremental small-header
.notes Demonstrate create and save on Person
# Persistence #

* Model.create
* Model.create!
* Model#save
* Model#delete
* Model#destroy
* Model#upsert

!SLIDE
.notes Mongoid supports all expected CRUD operations for those familiar with other Ruby mappers like Active Record . A big difference between Mongoid and other ODM is that Mongoid performs atomic updates on only the fields that have changed instead of writing the entire document to the database each time.

Most persistence operations are atomic updates.

!SLIDE
.notes MongdDB dynamic query is wrapped with Criteria. It only touches the database when they need to, for example on iteration of results. Demonstrate
# Querying #

!SLIDE
# Criteria #
Criteria is a chainable and lazily evaluated

!SLIDE bullets incremental

* Criteria#where
* Criteria#find
* Criteria#exists?
* Criteria#count

!SLIDE bullets incremental
.notes Relations are associations between one model and another in the domain and in the database. Embedded relations describe documents who are stored inside other documents in the database. Referenced relations describe documents that reference documents in another collection by storing foreign key data (usually an id) about the other document in itself.
# Relations #

* embeds_many
* embeds_one
* embedded_in
* has_many
* has_one
* belongs_to

!SLIDE

	@@@ ruby
	class Band
	  include Mongoid::Document
	  embeds_many :albums
	end

	class Album
	  include Mongoid::Document
	  field :name, type: String
	  embedded_in :band
	end

!SLIDE
# Rails integration #

!SLIDE

	@@@ shell
	rails new mongoid_demo \
	            --skip-active-record
	
!SLIDE

Include in Gemfile

	@@@ shell
	gem 'mongoid'

!SLIDE

		@@@ shell
		rails generate mongoid:config

!SLIDE

	@@@ shell
	rails generate model Person \ 
						 first_name:string \
						 last_name:string \
						 location:string

!SLIDE
# Replication #

!SLIDE bullets
# Other features #

* Validations
* Dirty tracking
* Dynamic fields
* Inheritance
* Scopes
* Callbacks

!SLIDE bullets
# More information #

* http://mongoid.org
* http://github.com/mongoid/mongoid
* http://groups.google.com/group/mongoid