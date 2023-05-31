<html>
<head>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
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
    <button class="button" onclick="startTimer()">Start</button>
    <button class="button" onclick="stopTimer()">Stop</button>
    <button class="button" onclick="resetTimer()">Reset</button>
  </div>
  <p id="time"></p>

  <script>
var timerInterval;
var startTime;
var elapsedTime = 0;
var isRunning = false;

function startTimer() {
  if (!isRunning) {
    startTime = Date.now() - elapsedTime;
    timerInterval = setInterval(updateTimer, 10);
    isRunning = true;
  }
}

function stopTimer() {
  clearInterval(timerInterval);
  isRunning = false;
}

function resetTimer() {
  clearInterval(timerInterval);
  elapsedTime = 0;
  startTime = Date.now(); 
  isRunning = false;
  updateTimer();
}

function updateTimer() {
  var currentTime = Date.now();
  elapsedTime = currentTime - startTime;
  var formattedTime = formatTime(elapsedTime);
  document.querySelector('.timer').textContent = formattedTime;
}

function formatTime(milliseconds) {
  var hours = Math.floor(milliseconds / (1000 * 60 * 60));
  var minutes = Math.floor((milliseconds % (1000 * 60 * 60)) / (1000 * 60));
  var seconds = Math.floor((milliseconds % (1000 * 60)) / 1000);

  var formattedHours = hours.toString().padStart(2, '0');
  var formattedMinutes = minutes.toString().padStart(2, '0');
  var formattedSeconds = seconds.toString().padStart(2, '0');
  document.getElementById("time").innerHTML = formattedHours + ':' + formattedMinutes + ':' + formattedSeconds;
  return formattedHours + ':' + formattedMinutes + ':' + formattedSeconds;
}
  </script>
</body>
</html>