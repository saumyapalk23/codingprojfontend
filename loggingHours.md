<html>
<head>
  <style>
    body {
      /* display: flex; */
      /* display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      margin: 0; */
      background-color: #01060d;
    }
    .button {
      font-size: 18px;
      padding: 10px 20px;
      background-color: #161666;
      color: white;
      border: none;
      border-radius: 5px;
      margin: 0 10px;
    }
    .timer {
      font-size: 24px;
      margin-bottom: 10px;
      color: white;
    }
  </style>
</head>
<body>
  <h1 class="text-center m-5">Hours</h1>
  <div class="text-center m-5 timer">00:00:00</div>
  <div class="button-container">
    <center> <button class="button" onclick="startTimer()">Start</button></center>
    <br>
    <center><button class="button" onclick="stopTimer()">Stop</button></center>
    <br>
    <center><button class="button" onclick="resetTimer()">Reset</button></center>
  </div>
  
  <script>
// Declare global variables
var timerInterval; // Holds the interval ID for the timer
var startTime; // Holds the starting time of the timer
var elapsedTime = 0; // Holds the elapsed time in milliseconds
var isRunning = false; // Indicates whether the timer is currently running or not

// Function to start the timer
function startTimer() {
  if (!isRunning) { // Only start the timer if it's not already running
    startTime = Date.now() - elapsedTime; // Calculate the starting time by subtracting the elapsed time from the current time
    timerInterval = setInterval(updateTimer, 10); // Set an interval to update the timer every 10 milliseconds
    isRunning = true; // Set the running flag to true
  }
}

// Function to stop the timer
function stopTimer() {
  clearInterval(timerInterval); // Clear the interval to stop the timer
  isRunning = false; // Set the running flag to false
}

// Function to reset the timer
function resetTimer() {
  clearInterval(timerInterval); // Clear the interval to stop the timer
  elapsedTime = 0; // Reset the elapsed time to 0
  startTime = Date.now(); // Update the starting time to the current time
  isRunning = false; // Set the running flag to false
  updateTimer(); // Update the timer display immediately
}

// Function to update the timer display
function updateTimer() {
  var currentTime = Date.now(); // Get the current time
  elapsedTime = currentTime - startTime; // Calculate the elapsed time by subtracting the starting time from the current time
  var formattedTime = formatTime(elapsedTime); // Format the elapsed time in HH:MM:SS format
  document.querySelector('.timer').textContent = formattedTime; // Update the timer display on the webpage
}

// Function to format the elapsed time in HH:MM:SS format
function formatTime(milliseconds) {
  var hours = Math.floor(milliseconds / (1000 * 60 * 60)); // Calculate the number of hours
  var minutes = Math.floor((milliseconds % (1000 * 60 * 60)) / (1000 * 60)); // Calculate the number of minutes
  var seconds = Math.floor((milliseconds % (1000 * 60)) / 1000); // Calculate the number of seconds
  var formattedHours = hours.toString().padStart(2, '0'); // Format the hours with leading zeros if necessary
  var formattedMinutes = minutes.toString().padStart(2, '0'); // Format the minutes with leading zeros if necessary
  var formattedSeconds = seconds.toString().padStart(2, '0'); // Format the seconds with leading zeros if necessary
  
  return formattedHours + ':' + formattedMinutes + ':' + formattedSeconds; // Return the formatted time as a string
}
  </script>
</body>
</html>
