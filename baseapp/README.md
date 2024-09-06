# Base App

## Generating a Controller (replace CONTROLLER_NAME with your controller)
`docker compose run baeapp rails g controller CONTROLLER_NAME home`

If you wanted to generate a model or run a migration, you would run them in the same way.

## Modify the Routes File
Remove the get 'CONTROLLER_NAME/home' line near the top of config/routes.rb and replace it with the following:

`root 'CONTROLLER_NAME#home'`

If you go back to your browser, you should see the new home page we have set up.

## Adding a New Job (replace JOB_NAME with your job)
`docker compose run baseapp rails g job JOB_NAME`

## Modifying the JOB_NAME Job
Next, replace the perform function in app/job/JOB_NAME_job.rb to look like this:
```
def perform(*args)
  21 + 21
end
```

## Modifying the CONTROLLER_NAME Controller
Replace the home action in app/controllers/CONTROLLER_NAME_controller.rb to look like this:

```
def home
  @meaning_of_life = JOB_NAMEJob.perform_now
end
```

## Modifying the Home View
The next step is to replace the app/views/CONTROLLER_NAME/home.html.erb file to look as follows:

`<h1>The meaning of life is <%= @meaning_of_life %></h1>`

## Restart the Rails Application
You need to restart the Rails server to pick up new jobs, so hit CTRL+C to stop everything, and then run docker compose up again.

If you reload the website you should see the changes we made.

## Adding Some Tests
Create a test for the JOB_NAMEJob job. Create a file called test/job/JOB_NAME_test.rb:
```
require 'test_helper'

class JOB_NAMETest < ActiveJob::TestCase
  test "returns 42" do
     assert_equal 42, JOB_NAME.perform_now
  end
end
```
Let’s add a second test for the CONTROLLER_NAME controller. Create a file called test/controllers/CONTROLLER_NAME_controller_test.rb:

```
require 'test_helper'

class CONTROLLER_NAMETest < ActionDispatch::IntegrationTest
  test "should get home" do
    get "/"
    assert_response :success
  end
end
```

Before running the tests, create a test database:

`docker compose run drkiq rake db:test:prepare`

To run the tests, execute:

`docker compose run drkiq rails test`

### More Info
https://semaphoreci.com/community/tutorials/dockerizing-a-ruby-on-rails-application
