 # Front-end Coding Standards

## By Week One

#### Code Comments:

Comments are specially marked lines of text in the code that are not evaluated. There are usually two syntactic ways to comment. The first is called a single line comment and, as implied, only applies to a single line in the "source code". The second is called a Block comment and refers usually refers to a paragraph of text. A block comment has a start symbol and an end symbol and everything between is ignored by the computer.

Add descriptive comments above all significant code sections in your HTML, JavaScript and CSS files. The goal here is to explain to the next developer looking at your code WHY you created the individual code section. Let the code itself through explain HOW you created it. In an average 400-line JavaScript file, you should expect to see at least 3-4 good comments. 

Example:

  /* verify we can actually access the method 
  we are needing to test */
  it("should have a getWeather method", function() {
    expect(angular.isFunction(WeatherFactory.getWeather)).toBe(true);
  });

  // verify successful access and expected response
  it("should work", function () {

    // setup http backend
    httpBackend
        .whenGET("http://api.openweathermap.org/data/2.5/weather?APPID=9df2180a41f8a77f7f435abb28cafd81&id=524901")
        .respond({name:"Moscow"});

    // fake the call to the service
    WeatherFactory.getWeather({APPID:"9df2180a41f8a77f7f435abb28cafd81",id:524901})

        // test the response
        .then(function(response) {
            expect(response.data.name).toBe("Moscow");
            expect(response.status).toEqual(200);
        });


#### Variable and File Naming Conventions:

Variables and files should have descriptive names that immediately identify what they are doing. The idea here is that your code should be unambiguous and self-documenting. Avoid abreviations, numbers and special characters. Variables and function names should be camel cased, i.e., "camelCasedExample". File names should be all lower-cased and should describe the application features they define. Use consistent names for all component files following a pattern that describes the component's feature then (optionally) its type. The recommended pattern is 'feature.type.js'. An example of this would be:  avengers.controller.js.

## By Week Two

#### Folder Naming Conventions

The top level folder below the root of your applications by convention is named 'app'. Below the app folder, all folder names should be lower-cased and describe the feature managed within that folder. Here are some examples: 'customers', 'admin', 'products'. There are exceptions. Certain folders can be named for the types of files and components that they contain, usually if they are used globally within the application. Here are some examples: 'images', 'styles', 'logging'.

#### Separation of Concerns

Conceptually, this means that each coded component or module of an application should be responsible for only one specific feature or functionality. Separation of concerns is achieved by the establishment of boundaries. A boundary is any logical or physical constraint which delineates a given set of responsibilities. For the purpose of this course, examples of boundaries leading to separation of concerns would include the use of functions and objects to simplify code routines and maximize reuse. Angular controllers, factories, services and custom directives and components will be defined in seperate files and injected as needed.

## By Week Three

#### Error Handling and Reporting

The idea behind error handling and reporting is to enable our software to anticipate and gracefully handle any errors that can occur in any logical path of the application. The situation where an application error is thrown and the software fails mysteriously to the end user is to be avoided. This means wrapping all calls to internal and external services that could return an application generated error in conditional logic that anticipates and handles these errors. During development, these errors can be logged to the console for identification. Reporting errors to the end user should be handled by the display of error messages either directly on the view page or in pop-up notifications such as Toastr. 

## By Week Four

#### Unit Testing

Unit tests are created by developers to ensure that their code is bug free. Coverage in unit testing refers to the percentage of logical paths in an application that are actually handled in unit testing. For this course, we strive for 85% code coverage as a standard in our unit testing.  Unit tests need to be created for all controllers and services in Angular using Jasmine and Karma. 


For an exhaustive reference and discussion of these topics, please see John Papa's Style Guide:  https://github.com/johnpapa/angular-styleguide/tree/master/a1