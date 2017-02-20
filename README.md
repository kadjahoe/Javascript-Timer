# Javascript-Timer
A javascript countdown clock or timer with beautiful HTML and CSS styling that is simple to use in any project or on any website.

```
javascript timer DEMO @ www.preview.manifestare.com/javascript%20timer/index.html


Title    : JavaScript Countdown Clock  				
Author   : Katherine Adjahoe           				  
Created  : February 18, 2017           				 
Website  : www.preview.manifestare.com/javascript%20timer
Email    : support@manifestare.com

CSS Design is influenced by the Net ninja on YouTube
```
### HTML code
```html
<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<title>Javascript Countdown Clock</title>
<meta name="Description" content="A javascript countdown clock or timer with beautiful HTML and CSS styling that is simple to use in any project or on any website .">
<meta name="Keywords" content="javascript, js, countdown, clock, timer, css, html, website, design, beautiful timer, countdown clock, countdown timer, javascript timer, javascript countdown clock, javascript countdown timer">

<link rel="stylesheet" type="text/css" href="timer.css">
</head>
	
<body>
	<div class="display">
		<div id="clock" class="clock">
			<h1 class="event_title">Live Event Starts in</h1>
			<div id="numbers">
				<span class="days"></span>
				<span class="hours"></span>
				<span class="minutes"></span>
				<span class="seconds"></span>
			</div>
			<div id="units">
				<span>Days</span>
				<span>Hours</span>
				<span>Minutes</span>
				<span>Seconds</span>
			</div>
		</div>
		<div id="door" class="hide">
			<h1 class="event_title">Event Is Live</h1>
			<p class="action_caption">Click the button below to enter Live Stream</p>
			<button class="call_to_action_button" type="button" onclick="liveStream()">Enter Live Stream!</button>
		</div>
		<div class="author">Created by Katherine Adjahoe</div>
	</div>
	<script src="timer.js"></script>
</body>
</html>
```
### JavaScript code

```javascript
let countdown;// setInterval function for countdown clock
let serviceInSession;// seTimeout function for when event is Live
const clock = document.getElementById('clock');// div that controls the clock container 
const livestreamButton = document.getElementById('door');// div that controls the button for the user to click to enter the live stream
const daysUnit = document.querySelector('.days');// span element that displays the amount of days
const hoursUnit = document.querySelector('.hours');// span element that displays the amount of hours
const minutesUnit = document.querySelector('.minutes');// span element that displays the amount of minutes
const secondsUnit = document.querySelector('.seconds');// span element that displays the amount of seconds

const startDate = new Date(2017, 1, 19, 11, 30, 00).getTime();// initial date and time the countdown clock started from (Year, Month, Day, Hours, Minutes, Seconds,)
startDate > Date.now() ? timer(startDate) : calculateFutureDate(startDate);// conditional statement that decides if the timer function should start with the start date or calculate another date
// timer function takes in a date parameter in milliseconds
function timer(date){
	// countdown holds the entire timer functionality 
	countdown = setInterval(()=>{
		const now = Date.now();// current date and time
		const differenceInTime = date - now;// distance between current time and future time of event
		// checks timer to see if the distance is zero and if zero
		if(differenceInTime < 0){
			clearInterval(countdown);// clear timer
			clock.classList.add("hide");// hide the clock div element
			livestreamButton.classList.remove("hide");// show the live stream button div element
			// keeps the live stream button div element on the screen for 2 hours or 7200000 milliseconds and then
			serviceInSession = setTimeout(()=>{
				livestreamButton.classList.add("hide");// hide live stream button div element
				calculateFutureDate(date);// pass the date that countdown was counting down to, to the calculateFutureDate function
				clock.classList.remove("hide");// show the clock again
			},7200000); // after 2 hours do what's inside the setTimeout function
			return;
		}	
		timeLeft(differenceInTime);// each iteration of setInterval send updated distance to timeLeft function
	}, 1000);// every 1 second
}
// timeLeft function takes a time as a parameter in milliseconds and displays it in Days, Hours, Minutes, and Seconds
function timeLeft(time){
		const days = Math.floor(time /(1000 * 60 * 60 * 24));// milliseconds into days
		const hours = Math.floor((time % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));// milliseconds into hours
		const minutes = Math.floor((time % (1000 * 60 * 60)) / (1000 * 60));// milliseconds into minutes
		const seconds = Math.floor((time % (1000 * 60)) / 1000);// milliseconds into seconds
		// conditional added to each portion of the time that will be displayed adds a zero to the front of numbers < 10
		const displayDays = `${days < 10 ? '0' : '' }${days}`;// days string that will be displayed 
		const displayHours = `${hours < 10 ? '0' : ''}${hours}`;// hours string that will be displayed
		const displayMinutes = `${minutes < 10 ? '0' : ''}${minutes}`;// minutes string that will be displayed
		const displaySeconds = `${seconds < 10 ? '0' : ''}${seconds}`;// seconds string that will be displayed
		//displays the time strings on the page individually
		daysUnit.textContent = displayDays;
		hoursUnit.textContent = displayHours;
		minutesUnit.textContent = displayMinutes;
		secondsUnit.textContent = displaySeconds;
		// next line is for testing purposes
		// console.log(displayDays+" : " +displayHours+" : "+displayMinutes+" : "+displaySeconds);
}
// calculateFutureDate takes a number in milliseconds as a parameter 
function calculateFutureDate (dateTochange){	
		const newDate = new Date(dateTochange);// converts it to date format
		const weeklyDate  = newDate.setDate(newDate.getDate() +07);// adds 7 days to that date
		timer(weeklyDate);// pass it to the timer function
		//console.log("new: "+dateTochange);		
}
// liveStream function changes the webpage to the webpage where the live stream is hosted
function liveStream (){
	window.location.assign("http://www.clcconthemove.org/clccLivestream.html");
}

```
### CSS code for styling

```css
/* CSS Design is influenced by the Net ninja on YouTube */

.display {
	flex: 1;
	display: flex;
	flex-direction : column;
	align-items : center;
	justify-content : center;
	background: #001f3f;
	font-family: tahoma !important;
	padding-bottom: 60px;
}
.event_title {
	color: #fff;	
	text-align: center;
	font-size: 74px;
	letter-spacing: 10px;
}
p.action_caption{
	color: #fff;	
	text-align: center;
	font-size: 16px;
	letter-spacing: 5px;
	font-weight: 100;
}
#door{
	text-align: center;
}
.call_to_action_button{
	margin-top: 40px;
	border-radius: 20px;
}
button.call_to_action_button {
	letter-spacing: 2px;
	text-align: center;
	font-size: 16px;
	top: 50%;
	left: 50%;
	color: #fff;
	padding: 20px;
	width: 0 auto;
	border-radius: 20px;
	box-sizing: border-box;
	background: #0074D9;
	border-style: none;
}
button:hover{
	background: #fff;
	color: #0074D9;
	font-weight: bold;
}
button:active{
	background: #fff;
	color: #0074D9;
	font-weight: bold;
}
button:focus{
	background: #fff;
	color: #0074D9;
	font-weight: bold;
}
.clock{
	width: auto;
}
#numbers{
	width: auto;
}
#numbers span{
	float: left;
	text-align: center;
	font-size: 60px;
	margin: 0 2.5%;
	color: #fff;
	padding: 20px;
	width: 20%;
	border-radius: 20px;
	box-sizing: border-box;
}
#numbers span:nth-child(1){
  background: #fa5559;
}
#numbers span:nth-child(2){
  background: #26c2b9;
}
#numbers span:nth-child(3){
  background: #f6bc58;
}
#numbers span:nth-child(4){
  background: #2dcb74;
}

#numbers:after{
	content: "";
	display: block;
	clear: both;
}

#units span{
	float: left;
	width: 25%;
	text-align: center;
	margin-top: 30px;
	color: #ddd;
	text-transform: uppercase;
	font-size: 16px;
	letter-spacing: 2px;
	text-shadow: 1px 1px 1px rgba(10,10,10, 0.7);
}

span.turn{
  	animation: turn 0.7s ease forwards;
}

@keyframes turn{
	0%{transform: rotateX(0deg)}
	100%{transform: rotateX(360deg)}
}

.hide{
	display: none;
}

.author{
	padding-top: 60px;
	color: #fff;	
	text-align: center;
	font-size: 13px;
	letter-spacing: 2px;
	font-weight: 100;
}
```
