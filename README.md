# Rails Developer-Led Review

## Routes vs Controllers

## Plurals, Capitalization, etc. and Rails Magic

## Summarizing hashes, bcrypt, and sessions

A hash function is any function that can be used to map data of arbitrary size to data of fixed size.  A hash is one-way, meaning that while computation time to create a digest (encrypted string) is constrained, computation time to return that digest to a plaintext string is considerably harder.

bcrypt is a password hashing function designed by Niels Provos and David Mazières, based on the Blowfish cipher.  More about this in Further Resources.

Further Resources:
[bcrypt Wikipedia Page](https://en.wikipedia.org/wiki/Bcrypt)

##What does "as" do in Rails?

"as:" will create <name>_path and <name>_url as named helpers in your application. 

For example, in the below...

`get 'exit', to: 'sessions#destroy', as: :logout`

Calling logout_path will return /exit.

Further Resources:

[Rails Routing](http://guides.rubyonrails.org/routing.html)

## What does -T actually do?

In the below code:

`rails new MYAPP -T`

The -T option tells rails not to include Test::Unit

Usually, we use this because we would rather not use the default Test::Unit library included with Rails.  Rather, we want to use Rspec.  This is one of the most common customizations in Rails, as a lot of developers prefer Rspec.

Let's have a quick look at what that means in a Rails app...

## Params in Rails vs Sinatra...what about the req.body and req.body.rewind?

## 
