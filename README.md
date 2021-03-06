# Sinatra PostgreSQL Grape Template [![Dependency Status](https://gemnasium.com/badges/github.com/katgironpe/sinatra-pg-grape.svg)](https://gemnasium.com/github.com/katgironpe/sinatra-pg-grape) [![Build Status](https://secure.travis-ci.org/katgironpe/sinatra-pg-grape.png)](http://travis-ci.org/katgironpe/sinatra-pg-grape)

## What is this good for?

* Development of simple REST API for web, mobile and desktop applications
* Isolation of code for web services
* An alternative to having one big Rails application with cluttered routes
* Sanity

## Examples

* If you're writing an API implementation for various machine learning/ automation tasks, the best way is to isolate this and not make it a part of your probably bloated application
* REST API for specific mobile applications that may or may not rely another application

## Dependencies

* Ruby 2.1.2 or greater
* Grape
* PostgreSQL
* Sinatra
* ActiveRecord
* will_paginate

## Getting Started

``` bash
$ git clone --depth 1 git://github.com/katgironpe/sinatra-pg-grape.git myapp
$ rm -r myapp/.git && rm myapp/README.md
```

## PostgreSQL Configuration

Install PostgreSQL if you haven't yet.

On Mac OSX, you can use Homebrew to install PostgreSQL as

```bash
$ brew install pg
```

On Linux distros, use your package manager to install PostgreSQL. For instance, if you are on Ubuntu or Ubuntu derivative, you might use

```bash
$ apt-get install postgresql
```
You might need `sudo` privileges to run the above command. On CentOS-Fedora-Redhat, you would most likely use `yum` package manager. Similarly, on Arch, PostgreSQL can be installed with `pacman`.


## Configuration

``` bash
$ cp config/database.yml.example config/database.yml
```

Update `config/database.yml`.

## Test Data

There's a rake task for loading test data.

```bash
bundle exec rake db:populate_db
```

After loading that data, you can check `/api/v1/posts`.

Start the application:

```
bundle exec shotgun config.ru
```

Use curl or probably just your browser to view the output:

```
curl http://localhost:9393/api/v1/posts
```

## Grape Entity

With **grape-entity**, you can expose only the fields you want and format them as needed.

## Testing

We can use RSpec and Rack::Test to test the API requests.

Here's an example:

```ruby
#example.rb
class Example < Grape::API
  prefix 'api'
  version 'v1'
  format :json

  get :hello do
    { hello: 'Hello world' }
  end
end
```

We should make sure it returns correct status code and output:

```ruby
require 'spec_helper'

describe Example do
  include Rack::Test::Methods

  def app
    Example
  end

  describe 'GET /api/v1/hello' do
    it 'says hello to the world' do
      get '/api/v1/hello'
      expect(last_response.status).to eq(200)
      expect(JSON.parse(last_response.body)['hello']).to eq('Hello world')
    end
  end
end
```

Use the commands:

```bash
bundle exec rake
```

### The Golden Rule of API Design

> It’s not enough to write tests for an API you develop; you have to write unit tests for code that uses your API.

> — Michael Feathers

### Have any questions/ suggestions?

#### Katherine Pe

* <a href='https://c.kat.pe' target='_blank'>c.kat.pe</a>
