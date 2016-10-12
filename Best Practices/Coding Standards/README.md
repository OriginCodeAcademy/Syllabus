 # Front-end Coding Standards

## By Week One

#### Code Comments:

Comments are specially marked lines of text in the code that are not evaluated. There are usually two syntactic ways to comment. The first is called a single line comment and, as implied, only applies to a single line in the "source code". The second is called a Block comment and refers usually refers to a paragraph of text. A block comment has a start symbol and an end symbol and everything between is ignored by the computer.

Add descriptive comments above all significant code sections in your HTML, JavaScript and CSS files. The goal here is to explain to the next developer looking at your code WHY you created the individual code section. Let the code itself through explain HOW you created it. In an average 400-line JavaScript file, you should expect to see at least 3-4 good comments. 

Example:

```js
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
```

#### Variable and File Naming Conventions:

Variables and files should have descriptive names that immediately identify what they are doing. The idea here is that your code should be unambiguous and self-documenting. Avoid abreviations, numbers and special characters. Variables and function names should be camel cased, i.e., "camelCasedExample". File names should be all lower-cased and should describe the application features they define. Use consistent names for all component files following a pattern that describes the component's feature then (optionally) its type. The recommended pattern is 'feature.type.js'. An example of this would be:  avengers.controller.js.

## By Week Two

#### Folder Naming Conventions

The top level folder below the root of your applications by convention is named 'app'. Below the app folder, all folder names should be lower-cased and describe the feature managed within that folder. Here are some examples: 'customers', 'admin', 'products'. There are exceptions. Certain folders can be named for the types of files and components that they contain, usually if they are used globally within the application. Here are some examples: 'images', 'styles', 'logging'.

#### Separation of Concerns

Conceptually, this means that each coded component or module of an application should be responsible for only one specific feature or functionality. Separation of concerns is achieved by the establishment of boundaries. A boundary is any logical or physical constraint which delineates a given set of responsibilities. For the purpose of this course, examples of boundaries leading to separation of concerns would include the use of functions and objects to simplify code routines and maximize reuse. Angular controllers, factories, services and custom directives and components will be defined in seperate files and injected as needed.

## By Week Three

#### Error Handling and Reporting

The idea behind error handling and reporting is to enable our software to anticipate and gracefully handle any errors that can occur in any logical path of the application. The situation where an application error is thrown and the software fails mysteriously to the end user is to be avoided.

This means wrapping all calls to internal and external services that could return an application generated error in conditional logic that anticipates and handles these errors. During development, these errors can be logged to the console for identification. Reporting errors to the end user should be handled by the display of error messages either directly on the view page or in pop-up notifications such as Toastr.

Form validation needs to be added for html inputs that receive user-entered data to ensure that values entered are present, if required, and are the correct data type. This can be accomplished using a combination of HTML5 and Angular ngMessages.

## By Week Four

#### Unit Testing

Unit tests are created by developers to ensure that their code is bug free. Coverage in unit testing refers to the percentage of logical paths in an application that are actually handled in unit testing. For this course, we strive for 85% code coverage as a standard in our unit testing.  Unit tests need to be created for all controllers and services in Angular using Jasmine and Karma. 


For an exhaustive reference and discussion of these topics, please see John Papa's Style Guide:  https://github.com/johnpapa/angular-styleguide/tree/master/a1

## By Week Five

#### C# Naming Conventions

Every language has it's own conventions that developers should adhere to so that other developers can easily read and recognize what your code is doing. In C#, the naming conventions are relatively straightforward and well documented across the web. You can find our collection of conventions in this repository under `Best Practices > Coding Standards > Backend > C#`.

#### Visual Studio Solution Conventions

Building on the concept of [Separation of Concerns](#separation-of-concerns) and sticking to good [Folder Naming Conventions](#folder-naming-conventions) as mentioned in earlier weeks, a good Visual Studio solution is built such that the components you write to build your application are well organized and clearly separated/organized. For the purpose of this course, the goal is to build solutions that are seperated into three projects. 

- A `.Core` project that contains all of your *Business Logic*.
- A `.Data` project that contains all of your *Data Access Logic*.
- A `.API` project that contains all of your *Controller Logic*.

## By Week Six

#### The 5 Principles of Object Oriented Programming (S.O.L.I.D)

*S.O.L.I.D* is an acronym describing the "first five principles" named by Robert C. Martin in the early 2000s. Each letter in the acronym stands for one of the 5 best practice principles of object-oriented programming and design. Adhering to these design patterns makes it more likely that you will create systems/applications that are easy to maintain and extend over time - which is a very valuable skill to have. 

To read more about the S.O.L.I.D principles - check out this [Scotch.io](https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design) article.

## By Week Seven / Eight

Note - in week seven, the class will be split into two groups of 6-8 developers to complete a relatively large project with around 5-6 different modules. 

#### GitHub Flow

GitHub Flow is more of a mindset than a specific tool. It is a lightweight, branch-based workflow that supports teams and projects where deployments are made regularly. It suggests ways for developers to use the `git` tool to streamline sharing a codebase with a team.

To read more about GitHub Flow - check out this [interactive guide](https://guides.github.com/introduction/flow/) provided by GitHub.

#### Project Management

When presented with a new project, steps are followed in a certain order to ensure that a project is delivered on time and to a high standard.

These steps vary from company to company, but typically in an Agile environment a project from start to finish looks something like this.

<img src="http://ambysoft.com/artwork/agileLifecycleDetailed.jpg" />

It begins with an initial iteration that mostly involves planning the work that needs to be accomplished, followed by a variable number of construction iterations (or sprints) to accomplish the work laid out during the initial iteration. After a working system has been achieved, it is transitioned over a period of time into a production environment where it is maintained until eventual retirement.

## By Week Nine

#### Deployment Best Practices



