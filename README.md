## Simple pagination
Generates pagination based on total number of elements and number of elements per page.

Developed with **webpack**.



### how to install:

```bash
npm install mayuska/pagination
```


### How to use it:
```javascript
var pagination = require('pagination');
var pag1 = new pagination(PagWrapper, data);
```
parameters: 
1. PagWrapper {DOM element}
2. data {object}:

data key | Type | Description 
--- | --- | ---  
currentPage		| int	 	| Sets current page.
totalItems  	| int 	 	| Number of total items in pagination.
itemsPerPage 	| int	 	| Number of how many elements will be shown on current page.
stepNum 		| int	 	| How many numbers will be shown before and after current page.
onInit 			| function 	| What will be executed on pagination init.
onPageChanged 	| function 	| What will be executed when page changes.

<br/>

### Methods:

Method | Returns | Description 
--- | --- |--- 
**.onPageChanged**(callback) 	| this 	| Callback will get only one argument **currentPage**
**.getCurrentPage**() 			| int 	| Returns current page
**.getPrevPage**() 				| int 	| Returns previous page
**.getNextPage**()				| int 	| Returns next page

 <br/>
 <br/>
 
### HTML structure

```
<a class="arrowLeft">&#9668;</a>
<span>
	<a class="pagNumber">1</a>
    <i class="pagDots">...</i>
    <a class="pagNumber">5</a>
    <a class="pagNumber current">6</a>
    <a class="pagNumber">7</a>
    <i class="pagDots">...</i>
    <a class="pagNumber">n</a>
</span>
<a class="arrowRight">&#9658;</a>
```

<br/>
<br/>

### Example: Change content when page is changed
**HTML**
```html
<div id="content"></div>
<div class="pagination"></div>
```
**JavaScript**

```javascript
 var pagination = require('pagination');

 var data = [
    {"name" : "Test 1", "description" : "1: Testing pagination"},
    {"name" : "Test 2", "description" : "2: Testing pagination"},
    {"name" : "Test 3", "description" : "3: Testing pagination"},
    {"name" : "Test 4", "description" : "4: Testing pagination"},
    {"name" : "Test 5", "description" : "5: Testing pagination"},
    {"name" : "Test 6", "description" : "6: Testing pagination"},
    {"name" : "Test 7", "description" : "7: Testing pagination"},
    {"name" : "Test 8", "description" : "8: Testing pagination"},
    {"name" : "Test 9", "description" : "9: Testing pagination"},
    {"name" : "Test 10", "description" : "10: Testing pagination"},
    {"name" : "Test 11", "description" : "11: Testing pagination"},
    {"name" : "Test 12", "description" : "12: Testing pagination"}
 ];
 var itemsPerPage = 1;

 var pag1 = new pagination(document.getElementsByClassName('pagination')[0],
     {
         currentPage: 1,		// number
         totalItems: data.length,	  // number
         itemsPerPage: itemsPerPage,    // number
         stepNum: 3,			// number
         onInit: displayContent		  // function
     });
 pag1.onPageChanged(displayContent);


 function displayContent(currentPage){
     document.getElementById('content').innerHTML = contentTemplate(currentPage);
 }

 function contentTemplate(currentPage){
     var template = "<ul>";
     for (var i = (currentPage - 1) * itemsPerPage; i < (currentPage * itemsPerPage) && i < data.length; i++) {
         template += "<li>name:" + data[i].name + "; description: " + data[i].description + "</li>";
     }
     template += "</ul>";
     return template;
 }

```
