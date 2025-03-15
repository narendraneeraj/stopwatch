---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---

<div class="container text-center">


 <div class="clock" id="digitalClock">00:00:00</div>
    
<div class="stopwatch" id="stopwatch">00:00:00</div>
  <button onclick="startStopwatch()">Start</button>
  <button onclick="splitTime()">Split</button>
  <button onclick="stopStopwatch()">Stop</button>
  <button onclick="resetStopwatch()">Reset</button>
    
  <table id="splitTable">
        <tr>
           <th>Lap</th>
           <th>Time</th>
        </tr>
    </table>
   
   <div class="timer-circle" id="timerCircle">30</div>
   <button onclick="startTimer(30)">30 Sec</button>
   <button onclick="startTimer(60)">1 Min</button>

</div>

<script>
        function updateClock() {
            const now = new Date();
            document.getElementById('digitalClock').innerText = now.toLocaleTimeString();
        }
        setInterval(updateClock, 1000);
        updateClock();
        
        let stopwatchInterval;
        let elapsedTime = 0;
        let running = false;
        let lapCount = 0;

        function startStopwatch() {
            if (!running) {
                running = true;
                const startTime = Date.now() - elapsedTime;
                stopwatchInterval = setInterval(() => {
                    elapsedTime = Date.now() - startTime;
                    updateStopwatch();
                }, 100);
            }
        }

        function stopStopwatch() {
            running = false;
            clearInterval(stopwatchInterval);
        }

        function resetStopwatch() {
            running = false;
            clearInterval(stopwatchInterval);
            elapsedTime = 0;
            lapCount = 0;
            updateStopwatch();
            document.getElementById("splitTable").innerHTML = "<tr><th>Lap</th><th>Time</th></tr>";
        }

        function splitTime() {
            if (running) {
                lapCount++;
                const totalSeconds = Math.floor(elapsedTime / 1000);
                const hours = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
                const minutes = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
                const seconds = String(totalSeconds % 60).padStart(2, '0');
                
                let table = document.getElementById("splitTable");
                let row = table.insertRow();
                row.insertCell(0).innerText = lapCount;
                row.insertCell(1).innerText = `${hours}:${minutes}:${seconds}`;
            }
        }

        function updateStopwatch() {
            const totalSeconds = Math.floor(elapsedTime / 1000);
            const hours = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
            const minutes = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
            const seconds = String(totalSeconds % 60).padStart(2, '0');
            document.getElementById('stopwatch').innerText = `${hours}:${minutes}:${seconds}`;
        }
        
        let timerInterval;
        function startTimer(duration) {
            clearInterval(timerInterval);
            let timeLeft = duration;
            document.getElementById("timerCircle").innerText = timeLeft;
            timerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById("timerCircle").innerText = timeLeft;
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                }
            }, 1000);
        }
    </script>