---
layout: post
title: "Common Rails Developer Interview Questions and Topics"
description: ""
category: 
tags: [RoR, Interviews, OOP]
---
{% include JB/setup %}

In the last few weeks I've had several interviews, mostly for mid-level full-stack dev positions, where I was quizzed on technical topics and terms that I couldn't articulate as well as I wanted. Well alright, some I just has absolutely no idea about. Now I knew for most of these interviews I was in over my head, but Jr. Dev positions in my neck of the woods (San Diego, CA) are harder to find here than an uncrowded surf break. I wrote out some basic definitions for the topics and terms I've been asked about multiple times. I'll clean this up eventually, but maybe it will be helpful to someone on their way into the gauntlet:

**OOP**

* code reuse, inheritance - any time you take a block of code and make it callable from anywhere else in the code is promote reuse
* accessibility - can choose whether to make code accessible by just the class itself (private), class and subclasses (protected), or by any of the code (public)
* variable accessibility or scope - [a-z] or _ (like x = 0) local, ($) global, (@) instance, and @@ class 
* segregation - ability to keep code modular and prevent dependencies
* extensibility - taking into account the future ability of code to be built upon. using a code class as a base, and building on top of it. pluggable can also be extensible but mainly means that it is modular and can be dropped in and work
* programs are composed of self-sufficient modules (classes) each instances of which (objects) contains all the information to manipulate its own data structure (members)

**Rails Concerns**

* in models, concerns are used to extract common and / or context specific chunks of code for reuse
cleans up the models so they don’t get too fat
* place in the app/models/concerns and called a module
* add ‘include module taggable.rb' or w/e name is to the top of model
this way you can in this case add the taggable module to any class and share it’s functionality
* extend ActiveSupport::Concern at top of module as well
* concerns directory is auto loaded in rails 4
* may be hard to find which module a method is being called from

**Service Objects**

* a service defines system interactions, usually involving one or more business models
for the MVC of a user requesting a forgotten pw, the controller is the service - responsible for locating the user, sending the reset pw email, then reporting back to the originator (in this case, controller)
* service objects implement individual services, providing modularity and easier testing on the controllers and models
* the forgotten pw service would become its own class, and it’s own controller with a single method
* tests on the controllers will be simple and you don’t run the risk of turning them into integration tests
* add directory ‘services’ under app dir
* simply create the class here as for example an authentication.rb class
* other examples: invitation, pw reset, user format, user search
* call from controller with class name in capitalized . method ( UserSearch.new(params[:query]).users for example
* complex controller + complex model operations is a good time to use SO's

**Fat model, skinny controller**

* non-response related logic should go in the model
* promotes code reuse and also can test code outside the context of a request
* @published_posts = Post.all :conditions => {[‘published_at <= ?’, Time.now]}
would become:
* in controller - @published_posts = Post.all_published 
* in model, it would become the method:
{% highlight ruby %}
def self.all_published
  all :conditions => {[‘published_at <= ?’, Time.now]}
end
{% endhighlight %}

**Associations**

* has_many :orders
* belongs_to :customers
* streamlines common operations by declaratively telling rails that their is an association between two models
* six types: belongs_to, has_one, has_many, has_many :through, has_one :through, has_and_belongs_to_many

**Polymorphic Associations**

* this way, a model can belong to more than one model on a single association
* for example, class picture belongs_to :imageable, polymorphic: true
* employee has_many pictures, as: :imageable
* product has_many pictures, as: :imageable
* must declare foreign key and type columns in the polymorphic model

**RESTful API**

* representational state transfer
* doesn’t require the client to know anything about the structure of the API - it’s completely disconnected and modular
* server provides whatever information requested or needed to interact with the page
* POST is used to create
* PUT is used to create or update
* PUT is idempotent

**Soft Questions**

* What part of coding do you enjoy the most?
* What sites or apps do you admire?
* Why did you decide to get into programming?
* What technologies or what aspects of coding are you strongest with?
* Weakest points technology wise?
* What is your greatest strength?
* Greatest weakness?

**Questions I tend to ask the interviewer:**

* What is your vision for your company?
* Where do you feel like you could use the most help currently?
* What do you generally see being the biggest challenges for jr. developers coming in?
* What do you find to be the most valuable characteristics among successful developers?
* Where did you learn most of your coding languages?
* What do you do for fun?
* How many devs are you looking to hire?
* What skill level are you aiming for?
* Why?
*What technologies do you use?
