## jQuery Interview Questions

#### Part I, The Basics

Questions

1. What does dollar sign ($) mean in jQuery?

2. How do you deal with using multiple JavaScript libraries that all use $ as their global function?

3. Is there any difference between body onload() and document.ready() function?

4. What are selectors in jQuery and how many types of selectors are there?

5. How do you select element by Id in jQuery?

6. How do you check if an element is empty?

7. What is the use of the .each() function?

8. What is the .animate() method used for?

9. What is chaining in jQuery?

10. If you get a "jquery is not defined" or "$ is not defined" error, what could be the reason?

11. What is the difference between `ajax()` and `getJSON()`?

12. How do you make an asynchronous call in jQuery?

13. What is the purpose of the `$(document).ready()` function?


Answers

1. alias for jQuery keyword

2. `jQuery.noConflict`

3. The `document.ready()` function is called as soon as the DOM is loaded whereas `body.onload()` function is called when everything gets loaded on the page including the DOM, images and all associated resources of the page.

4. There are many - some examples: element, name, id and class

5. `$('#txtName')`

6. `$('#element').is(':empty')`  OR `$.trim($('#element').html())==''`

7. Its used to iterate over any collection, either array or object.

8. Its used to create animation effects on any numeric CSS property. This method changes an element from one state to another with CSS styles. The CSS property value is changed gradually, to create an animated effect.

9. It means to connect multiple functions and/or events on selectors. Chaining gives better performance. Example:
   `$('#dvContent').addClass('dummy').css('color', 'red').fadeIn('slow');`  

10. There are multiple causes:
* You have forgotten to include a reference to the jQuery library.
* You may have included the reference to the jQuery file, but it is after your jQuery code.
* The order of the scripts is not correct. For example, if you are using any jQuery plugin and you have placed the reference for the plugin js before the jQuery library then you will see this error.

11. `ajax()` is the all-encompassing request service for jQuery with many customizable attributes. `getJSON()` is an implementation of `ajax()` that will only return data in JSON format. `getJSON()` parses the JSON string into an Object, whereas `.ajax()` returns a String that you would have to parse, as in `obj=jQuery.parseJSON(data)`. In addition, `ajax()` can also return xml.

12. Using the deferred and promise objects in jQuery Also supports chaining. Example:
  ```js
  function testAsyncDeferred() {
      var deferredObject = $.Deferred();
    setTimeout(function() {
      deferredObject.resolve(); 
    }, 1000);
    return deferredObject.promise();
  }
```
13. Its used to execute code when the document is ready for manipulation. jQuery allows you to delay execution of code until the DOM is fully loaded i.e. HTML has been parsed and DOM tree has been constructed. It works in all browsers.

Read more: http://javarevisited.blogspot.com/2015/02/top-16-jquery-interview-questions.html#ixzz49cNO2ayN

reference;  http://www.codeproject.com/Articles/618484/Latest-jQuery-interview-questions-and-answers


#### Part II, the conceptual stuff

1. What is wrong with the below code: 
 ```js
    // define the click handler for all buttons
    $( "button" ).bind( "click", function() {
      alert( "Button Clicked!" )
  });
```
    /* ... some time later ... */
```js
    // dynamically add another button to the page
    
  $( "html" ).append( "<button>Click Alert!</button>" );
  ```

The button that is added dynamically after the call to bind() will not have the click handler attached. This is because the bind() method only attaches handlers to elements that exist at the time the call to bind() is made.

2. ` $( "div#demo, div.demo, ol#items > [name$='demo']" )`

  This code performs a query to retrieve any '<div>' element with the id "demo", plus all `<div>` elements with the class "demo", plus all elements which are children of the `<ol id="items">` element and whose name attribute ends with the string "demo". This is an example of using multiple selectors at once. The function will return a jQuery object containing the results of the query.

3. Explain what the following code does:
   
`$( "div" ).css( "width", "300px" ).add( "p" ).css( "background-color", "blue" );`

This code uses method chaining to accomplish a couple of things. First, it selects all the `<div>` elements and changes their CSS width to 300px. Then, it adds all the `<p>` elements to the current selection, so it can finally change the CSS background color for both the `<div>` and `<p>` elements to blue.

4. Which of the two lines of code below is more efficient? Explain your answer.

  `document.getElementById("logo");`
    - OR -
  `$("#logo");`

The first line of code is pure JavaScript without jQuery. It is more efficient and faster. Executing the second line of code, which is jQuery, will trigger a call to the JavaScript version.

jQuery is built on top of JavaScript and uses its methods under the hood to make DOM manipulation easier, at the cost of some performance.

5. How do you make a deep copy in jQuery?

The `.clone()` method performs a deep copy of the set of matched elements, meaning that it copies the matched elements as well as their descendant elements and text nodes.

6. What is the difference between `detach()` and `remove()`?

The `.detach()` and `.remove()` methods are the same, except that `.detach()` retains all jQuery data associated with the removed elements and `.remove()` does not. `.detach()` is therefore useful when removed elements may need to be reinserted into the DOM at a later time.

7. How do you create a fade effect in jQuery?

1. There are three methods to give the fade effect to elements: fadeIn, fadeOut and fadeTo.
2. These methods change the opacity of an element with animation.

Syntax:
```js
$(selector).fadeIn(speed,callback)
$(selector).fadeOut(speed,callback)
$(selector).fadeTo(speed,opacity,callback)
```

8. What is the .siblings() method in jQuery?

Its used to fetch siblings of every elements in the set of matched elements. Example:
  `$(‘li.second_item’).siblings().css(‘color’,’blue’);`
This code selects all the li siblings of the li with id, second_item, and changes the test color to blue.


9. How do you use `jQuery.data()`?

`jQuery.data()` is used to set or get arbitrary data to / from an element. Set Example:
```js
   // Passing an object:
   $("#myDiv").data({"name":"Stevie","age":21});

   // This is the same as:
   $("#myDiv").data("name","Stevie").data("age",21);
```
  Get Example:
```js
  var theValue = $("div:first").data("name"); // Stevie

  $("div:first").click(function(){
    alert($(this).data("age"); // 21
  });
```

10. What is the difference between the prop() and attr() methods?

  1. In jQuery both prop() and attr() functiond str used to set/get the value of specified property of an element.
  2. The difference is that attr() returns the default value of the property while the prop() returns the current value of the property.

  Example:
```js
  <input value="My Value" type="text"/>
  $('input').prop('value', 'Changed Value');
```
  * `.attr('value')` will return 'My Value'
  * `.prop('value')` will return 'Changed Value'

References:   
https://www.toptal.com/jquery/interview-questions
              http://www.careerride.com/jQuery-Interview-Questions.aspx
              http://www.impressivewebs.com/jquery-tutorial-for-beginners/