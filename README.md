# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
      I checked my rails server logs upon submission and it gave me the error: "NameError (uninitialized constant ToysController::Toys):" pointed to line 10. I knew the 'Toys' class name was written incorrectly. I replaced it with 'Toy' and the post request went through successfully.

- Update the number of likes for a toy

  - How I debugged:
      I checked the rails server logs after clicking the like button and found the following error: "Unpermitted parameter: :id". I ran byebug to check the toy_params and confirmed only the 'likes' param was permitted. I quickly went down to the private section to check the toy_params method. I added the 'id' attribute among the permitted params. I tried liking a toy on my app again, and it was updating.

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
      I clicked the 'Donate to Goodwill' button and nothing happened, so checked my server logs in which I found the error: 'ActionController::RoutingError (No route matches [DELETE] "/toys/11"):'. I checked my config/routes.rb file and indeed there wasn't any route that handled deleting from the database. I added a destroy route which handled deleting through the destroy method present in toys_controller.rb file. I now tried donating a toy, and it was successfully removed from the database, and hence disappeared from the front-end.