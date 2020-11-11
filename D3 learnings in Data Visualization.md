# D3 learnings
### This page includes all my learnings while working with D3, javascript, html and css.
#### This page is under progress. 

1. When you face any problem and are trying to google for answers, first identify whether the problem lies with javascript synatx, html or D3 functions. This will make the process much faster.

2. ***Windows*** When trying to open your webpage in chrome: 
Your html and css elements will load, but you may have problems with javascript and loading the data, especially if your data is stored as a separate file.
> eg: d3.v3.min.js:1 XMLHttpRequest cannot load file:///C:/../dataset.csv. Cross origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, https.

Solution:
- Open in firefox browser.
- If you still want to open in chrome, ... 

3. ***Javascript*** Referencing an object's property.
If your object looks something like this:  
my_object = [{value:"Ruchita", 123:"USA"},
 			 {value:"Robert",  123:"India"}]

Mentioning the property name with a 'dot' after the oject name will access that column of data.
> eg: my_object.value -> ("Ruchita","Robert")

To access specific row of data
> eg: my_object[0] -> ("Ruchita", "USA")

But problem arises when my_object.123 gives you an error.
I replaced '123' with 'a123' in my original dataset, just so that javascript treats it as a string.

4. ***Javascript*** Tips
  - To print something on the inspect element console:        
  `console.log("Enter stuff here")`
  - To get the type of a variable with a basic datatype (String/Number/Boolean)        
  `typeof(your_variable)`
  - To get the type of an object        
  `Object.prototype.toString.call(pass_the_object_here)`        
  - To get the number of elements present inside an object        
  `var temp = {};         
  Object.keys(temp).length;`

5. ***D3*** When trying to access multiple files in the same d3.js file, yo can simply do something like:     
`d3.csv("csv1.csv", function(error1, data1) {                                                            
   d3.csv("csv2.csv", function(error2, data2) {                                                      
      // code requiring data access                                                                                        
    });                                                                                                 
});`                                                                                                                   

6. ***D3*** D3 requires a numeric source and target     
We need this:
> {"nodes":[ 
	 	{"name":"node1"}, 
		{"name":"node2"}, 
		{"name":"node3"}, 
		{"name":"node4"} 
	],       
	"links":[
		{"source":3,"target":1}, 
		{"source":0,"target":2} 
	] 
   } 

   And not this:
> {"nodes":[ 
	 	{"name":"node1"}, 
		{"name":"node2"}, 
		{"name":"node3"}, 
		{"name":"node4"} 
	],         
	"links":[ 
		{"source":node4,"target":node2}, 
		{"source":node1,"target":node3} 
	] 
   }      

We need to get index of each node using indexOf to achieve this.

7. ***D3 & HTML*** Appending one html element vs appending one element for each data item.
If you want to append a single html element, use the append method:

`d3.select('.classname').append('div').text("This is a title").attr("id", "title");`                                         
This will append a div to the element having class:"classname", and give an id to this element.

If you have your data in an array, and would like to append an html element for each item in the array:                          
`var array_numbers = ["1","2","3"];                                                           
d3.select('.classname').selectAll('div').data(array_numbers).enter().append('div').text(function(array_numbers) { return array_numbers; }).attr("id", function(array_numbers) { return array_numbers;});`                                                       
This will append 3 div elements, each with its own id and text.

8. ***CSS*** Defining variables in CSS.                                                            
Add your variables inside a root class. Supported in chrome, firefox, safari.                                            
`:root {
  --peach: #ffe0cc;
}
body {
	background-color:var(--peach); 
}`

9. ***D3*** Fetching multiple values from a scrolling select list.
`list_of_selections=d3.select("#id_of_select_element").selectAll("option").filter(function (d, i) {return this.selected;});`
> list_of_selections --> Array[Array[<option text="option1">,<option text="option2">,<option text="option3">]]

10. ***HTML*** HTML encoding
>To add '<', '>' or other such characters as text inside your HTML file, you need to use HTML encoding
Eg: If you want to say something like "For amount >$10", you will have to use the HTML code:
`<p>"For amount &gt;$10</p>



