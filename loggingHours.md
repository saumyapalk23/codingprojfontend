<html>
<head>
  <style>
    .timer {
      font-size: 24px;
      margin-bottom: 10px;
    }
      body{
        background-color: #01060d;
      }

    
  </style>

  <script>
   
    var timerInterval;
    var startTime;
    var elapsedTime = 0;
    var temp = 10;

    function startTimer() {
      if(temp >9){
        startTime = Date.now() - elapsedTime;
        timerInterval = setInterval(updateTimer, 10);
      }

    }

    function stopTimer() {
      temp = 9;
      clearInterval(timerInterval);
  
    }

    function resetTimer() {
      location.reload();
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
      return = formattedHours + ':' + formattedMinutes + ':' + formattedSeconds;
    }  

    </script>
</head>
<body>
  
  <button  onclick="startTimer()">Start</button>
  <button  onclick="stopTimer()">Stop</button>
  <button class="button" onclick="resetTimer()">Reset</button>
  <div class="timer">00:00:00</div>


  
</body> 
</html>
