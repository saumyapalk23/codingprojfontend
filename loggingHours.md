<html>
<head>
  <style>
    .timer {
      font-size: 24px;
      margin-bottom: 10px;
    }

    .button {
      font-size: 18px;
      padding: 10px 20px;
      background-color: green;
      color: white;
      border: none;
      border-radius: 5px;
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <div class="timer">00:00:00</div>
  <button class="button" onclick="startTimer()">Start</button>
  <button class="button" onclick="stopTimer()">Stop</button>
  <button class="button" onclick="resetTimer()">Reset</button>

  <script>
    '''
  var timerInterval;
    var startTime;
    var elapsedTime = 0;

    function startTimer() {
      startTime = Date.now() - elapsedTime;
      timerInterval = setInterval(updateTimer, 10);
    }

    function stopTimer() {
      clearInterval(timerInterval);
    }

    function resetTimer() {
      clearInterval(timerInterval);
      elapsedTime = 0;
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

      return formattedHours + ':' + formattedMinutes + ':' + formattedSeconds;
    }  
    '''
    </script>
</body> 
</html>