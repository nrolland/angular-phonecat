# &lt;angular/&gt; Phone Catalog Tutorial Application

# Overview

This application takes the developer thought the process of building a web-application using
angular. The application is loosely based on
[Google phone gallery](http://www.google.com/phone/). Each commit is a separate lesson
teaching a single aspect of angular.


# Prerequisites

- `git`: A good place to learn about setting up git is [here][git]
- `node.js`: Generic [installation instructions][node-generic].
  - Mac DMG [here][node-mac]
  - Windows download from [here][node-windows]. (You will also need
    [7 Zip] to unzip the node archive)
    (and don't forget to add `node.exe` to  your executable path)


# Workings of the application

- The application filesystem layout structure is based on the [angular-seed] project.
- There is no backend (no server) for this application. Instead we fake the XHRs by fetching
  static json files.
- Read the Development section at the end to familiarize yourself with running and developing
  an angular application.

# Commits / Tutorial Outline

You can check out any point of the tutorial using
    git co step-?

To see the changes which between any two lessons use the git diff command.
    git diff step-?..step-?

## step-0

- Initial [angular-seed] project layout


## step-1

- We have converted the seed application by removing all of the boiler-plate code.
- We have added single static HTML file which shows a static list of phones. (we will convert this
  static page into dynamic one with the help of angular)


## step-2

- Converted static page into dynamic one by:
  - create a root controller for the application
  - extracting the data from HTML into a the controller as a mock dataset
  - convert the static document into a template with the use of `ng:` [directive] (iterate over
    mock data using [ng:repeat] and render it into a view)
- Added unit test, which mostly shows how one goes about writing a unit test, rather then test
  something of value on our mock dataset.


## step-3

- added a search box to demonstrate how:
  - the data-binding works on input fields
  - to use [$filter] function
  - [ng:repeat] automatically shrinks and grows the number of phones in the view
- added an end-to-end test to:
  - show how end-to-end tests are written and used
  - to prove that the search box and the repeater are correctly wired together


## step-4

- replaced the mock data with data loaded from the server (in our case the JSON return is just a
  static file)
  - The JSON is loaded using the [$xhr] service
- Demonstrate the use of [services][service] and [dependency injection][DI]
  - The [$xhr] is injected into the controller through [dependency injection][DI]


## step-5

- adding phone image and links to phone pages
- css to style the page just a notch


## step-6

- making the order predicate for catalog dynamic
  - adding 'predicates' section to the view with links that control the order
  - ordering defaults to 'age' property
- css sugar


## step-7

- Introduce the [$route] service which allows binding URLs for deep-linking with views
  - Replace content of root controller PhonesCtrl with [$route] configuration
  - Map `/phones' to PhoneListCtrl and partails/phones-list.html
  - Map `/phones/phone-id' to PhoneDetailCtrl and partails/phones-detail.html
  - Copy deep linking parameters to root controller `params` property for access in sub controllers
  - Replace content of index.html with [ng:view]
- Create PhoneListCtrl view
  - Move code which fetches phones data into PhoneListCtrl
  - Move existing HTML from index.html to partials/phone-list.html
- Create PhoneDetailsCtrl view
  - Wire [$route] service to map `/phanes/phone-id` to map to this controller.
  - Empty PhoneDetailsCtrl
  - Place holder partials/phane-details.html

## step-8

- Fetch data for and render phone detail view
  - [$xhr] to fetch details for a specific phone
  - template for the phone detailed view
- CSS to make it look pretty
- Detail data for phones in JSON format

## step-9

- replace [$xhr] with [$resource]
  - demonstrate how a resource can be created using a [service]

# Development

## Running the app during development

1. run `./scripts/web-server.js`
2. navigate your browser to `http://localhost:8000/app/index.html` to see the app running in your
   browser.

## Running unit tests

Requires java.

1. start `./scripts/test-server.sh`
2. navigate your browser to `http://localhost:9876/`
3. click on: capture strict link
4. run `scripts/test.sh`
5. edit files in `app/` or `src/` and save them
6. go to step 4.


## Continuous unit testing

Requires ruby and [watchr](https://github.com/mynyml/watchr) gem.

1. start JSTD server and capture a browser as described above
2. start watchr as `watchr scripts/watchr.rb`
3. in a different window/tab/editor `tail -f logs/jstd.log`
4. edit files in `app/` or `src/` and save them
5. watch the log to see updates


## End to end testing

1. open `http://localhost:8000/test/e2e/runner.html` in your browser


## Application Directory Layout

    app/                --> all of the files to be used in production
      css/              --> css files
        app.css         --> default stylesheet
      img/              --> image files
      js/               --> javascript files
        controllers.js  --> application controllers
        filters.js      --> custom angular filters
        services.js     --> custom angular services
        widgets.js      --> custom angular widgets
      lib/              --> angular and 3rd party javascript libraries
        angular/
          angular.js            --> the latest angular js
          angular.min.js        --> the latest minified angular js
          angular-ie-compat.js  --> angular patch for IE 6&7 compatibility
          version.txt           --> version number
      partials/         --> angular view partials (partial html templates)

    config/jsTestDriver.conf    --> config file for JsTestDriver

    logs/               --> JSTD and other logs go here (git-ignored)

    scripts/            --> handy shell/js/ruby scripts
      test-server.sh    --> starts JSTD server
      test.sh           --> runs all unit tests
      watchr.rb         --> config script for continuous testing with watchr
      web-server.js     --> simple development webserver based on node.js

    test/               --> test source files and libraries
      e2e/              -->
        runner.html     --> end-to-end test runner (open in your browser to run)
        scenarios.js    --> end-to-end specs
      lib/
        angular/                --> angular testing libraries
          angular-mocks.js      --> mocks that replace certain angular services in tests
          angular-scenario.js   --> angular's scenario (end-to-end) test runner library
          version.txt           --> version file
        jasmine/                --> Pivotal's Jasmine - an elegant BDD-style testing framework
        jasmine-jstd-adapter/   --> bridge between JSTD and Jasmine
        jstestdriver/           --> JSTD - JavaScript test runner
      unit/                     --> unit level specs/tests
        controllersSpec.js      --> specs for controllers

## Contact

For more information on angular please check out http://angularjs.org/

[7 Zip]: http://www.7-zip.org/
[angular-seed]: https://github.com/angular/angular-seed
[DI]: http://docs.angularjs.org/#!guide.di
[directive]: http://docs.angularjs.org/#!angular.directive
[$filter]: http://docs.angularjs.org/#!angular.Array.filter
[git]: http://help.github.com/set-up-git-redirect
[ng:repeat]: http://docs.angularjs.org/#!angular.widget.@ng:repeat
[ng:view]: http://docs.angularjs.org/#!angular.widget.ng:view
[node-mac]: http://code.google.com/p/rudix/downloads/detail?name=node-0.4.0-0.dmg&can=2&q=
[node-windows]: http://node-js.prcn.co.cc/
[node-generic]: https://github.com/joyent/node/wiki/Installation
[$resource]: http://docs.angularjs.org/#!angular.service.$resource
[$rouet]: http://docs.angularjs.org/#!angular.service.$route
[service]: http://docs.angularjs.org/#!angular.service
[$xhr]: http://docs.angularjs.org/#!angular.service.$xhr
