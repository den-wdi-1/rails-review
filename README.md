# Rails Developer-Led Review

## Routes vs Controllers

The concept of a **controller** is incredibly nebulous.  There are some programmers who believe we need to stop using the word altogether, as it no longer has any consistent meaning.  Fun, right?

My definition in Rails is two-part "a **controller** is the thing that drives your main functionality" and "a **controller** is the thing that connects your **model** to your **view**".

DHH does not agree, and as we all know, DHH is quite opinionated.  And he, unlike Matz, is quite vocal and loud-spoken about those opinions.  

>The heuristics I use to drive that is: whenever I have the inclination that I want to add a method on a controller that’s not part of the default five or whatever REST actions that we have by default, make a new controller! And just call it that.

In other words, inside your controller, you should have at most the following methods we have been learning:

* `index`
* `show`
* `new`
* `edit`
* `create`
* `update`
* `destroy`
 
You are welcome to choose from those, but you should not have methods named anything else.  Rails...is Omakase.

OK, now what is a **route**?  Well, quite simply a **route** is a combination of a **path** (like "/home") and an **action** (like "GET", "POST", "PUT", or "DELETE").  As its name implies, it is the middle-man that directs traffic between the front-end and the back-end.  It takes the **path** and **action** given by the end-user and matches with a **path** and **action** combination on the server side.

A great part (or horrible part, depending on your opinion) about Rails is it leaves us no doubt as to where this logic lies.

All your routes will be found in `app_name/config/routes.rb`.

All your controllers will be found in `app_name/app/controllers`.

Further Resources:

* [A More Precise Definition from StackExchange](http://programmers.stackexchange.com/questions/135495/in-mvc-what-is-the-difference-between-controller-and-router)

## Plurals, Capitalization, etc. and Rails Magic

Rails can be frustrating at first, because it demands a very strict syntax, but does not, like JavaScript, stick almost entirely to the rule of "what you just told me".  That is, while JavaScript expects consistency in variable naming from function to function and file to file, Rails adds things like **C**apitalization, pluralization**s**, and **_**underscores, in addition to other special characters to make sure all your Models, Views, and Controllers line up with no work from you.

Further Resources:

* [Ruby and Rails Naming Conventions](http://itsignals.cascadia.com.au/?p=7)

## Summarizing hashes, bcrypt, and sessions

A **hash** function is any function that can be used to map data of arbitrary size to data of fixed size.  A hash is one-way, meaning that while computation time to create a digest (encrypted string) from a plaintext string is constrained, computation time to return that digest to a plaintext string is considerably harder.  This differs from encryption functions which are two-way, meaning that converting to an encrypted string is as easy as converting back to a plaintext string.

**bcrypt** is a password hashing function designed by Niels Provos and David Mazières, based on the Blowfish cipher.  More about this in Further Resources.

The **session** hash is a way for Rails to keep track of user states.  A session usually consists of a hash of values and a session id, usually a 32-character string, to identify the hash. Every cookie sent to the client's browser includes the session id. And the other way round: the browser will send it to the server on every request from the client. In Rails you can save and retrieve values using the session method:

session[:user_id] = @current_user.id

User.find(session[:user_id])

This allows two things.  First, it allows us to authenticate a user after logging in without requiring username and password every time, or even having to pass anything to do with the password at all.  The server knows the user logged in before, and what it is passing is that knowledge that "you are you".  Second, it allows us to handle authorization by checking if the session is up (again with no sending of passwords).  If not, we can redirect the user to log in.  If so, we can direct them to the proper resource.

Further Resources:

* [bcrypt Wikipedia Page](https://en.wikipedia.org/wiki/Bcrypt)
* [More on Sessions - Rails Guides](http://guides.rubyonrails.org/security.html)

##What does "as" do in Rails?

"as:" will create <name>_path and <name>_url as named helpers in your application. 

For example, in the below...

`get 'exit', to: 'sessions#destroy', as: :logout`

Calling logout_path will return /exit.

Further Resources:

*[Rails Routing](http://guides.rubyonrails.org/routing.html)

## What does -T actually do?

In the below code:

`rails new MYAPP -T`

The -T option tells rails not to include Test::Unit

Usually, we use this because we would rather not use the default Test::Unit library included with Rails.  Rather, we want to use Rspec.  This is one of the most common customizations in Rails, as a lot of developers prefer Rspec.

Let's have a quick look at what that means in a Rails app...

## Params in Rails vs Sinatra...what about the req.body and req.body.rewind?

`params[]` is actually a Rack hash, which is the web server for both Sinatra and Rails.  It works in both Sinatra and Rails, but slightly differently.

The main difference we have experienced is the handling of JSON.  While Rails does this automatically for us (helping out yet again, huh, Rails?), Sinatra is bare-bones so uses the default Rack functionality, which does not have this parsing ability.

So basically, if you're sending **form data**, there's almost no difference between `params` in Rails and Sinatra.  If, however, you're sending JSON, Sinatra requires you to bring in a `json` library and use `req.body`.
