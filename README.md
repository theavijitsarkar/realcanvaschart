# Real Time HTML5 Canvas Chart

## What?
A simple lightweight line chart. Uses HTML5 Canvas to draw a line chart. 

## Why?
Add real time points to the chart using the add point function. This can be used when you have huge amount of incoming data that needs to be plotted constantly without reloading the entire chart.
Google charts and most other charts cant be refreshed with new data points at such high speeds. Use this in such situations.
There is also a stroke buffer, which draws the charts after defined number of points has been added. Increase this to boost performance, especially in mobile browsers.

## How?

##### Step 1 : HTML
Inside the body add a div and give it a id.
```html

<div id="chart_div" width="200px;" height="200px;"></div>

```
On the head section include the canchart.js file 
```html
<script src="canchart.js"></script>
```

##### Step 2 : JAVASCRIPT
Initialize the chart with various parameters
```javascript

window.onload = function(){

//Parameters
var startTimestamp = 0;
var max_y=100; //Maximum horizontal points
var max_x=500; //Maximum vertical points
var color = "green"; //Color of the line
var div ="chart_div"; //Name of the ID which holds the div
var height = 200; //Height of the chart
var strokeBuffer = 1; //Number of strokes to draw at once, increase this to increase performance
var legend_x="Legend X"; //Name of the Horizontal Legend
var legend_y="Legend Y"; //Name of the Vertical Legend

/* Colored Band


Use these to create a colored band behind the chart. This is optional, just pass a blank object in its place to remove this
Ex:-  cantest.init("canTest", div , height , startTimestamp, 1 , color, max_y, max_x,{},strokeBuffer);

*/

var alarmParams={};
alarmParams.g_s=50;
alarmParams.g_e=100;
alarmParams.y_s=38;
alarmParams.y_e=50;
alarmParams.r_s=38;
alarmParams.r_e=0;
alarmParams.order="ryg";




//Create an Object of the class
 cantest = new CanvasChart();
//Initialize the object
 cantest.init("canTest", div , height , startTimestamp, 1 , color, max_y, max_x,alarmParams,strokeBuffer);


//The scale function draws the x and y axis.  

 cantest.scale(max_x,max_y,  legend_x , legend_y);



//Draw a vertical alert marker
cantest.alert_x(75,"Ver","blue");

//Draw a horizontal alert marker
cantest.alert_y(10,"Hori","red");


//Draw a line chart. Looping and adding points to the chart. Else part is optional just to show the reset method.

var i=0;

setInterval(draw,10);

function draw(){
	if(i<500){
		cantest.add_point(i,50*Math.random());
		i+=1;
	}
	else{
		cantest.reset();
		cantest.scale(max_x,max_y,  legend_x , legend_y);
		i=0;

	}
}


//Returns a canvas with the snapshot of chart in PNG format

var snapshot = cantest.snapshot();



}

```

### Thanks!!




#####Author: Avijit Sarkar & Neeraj Nagi
###### http://www.avijitsarkar.com
###### http://www.avifainfotech.com