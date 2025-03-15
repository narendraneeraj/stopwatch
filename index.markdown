---
layout: page
title: Hello World1
description: "India 123dee4e"
no_title: true
hide_meta: true
---

<div class="container text-center">


<p><div class="clock" id="digitalClock">00:00:00</div></p>
    
<!-- <div class="clock" id="digitalClock">00:00:00</div> -->
    
 <div class="stopwatch" id="stopwatch">00:00:00.00</div>
   <button type="button" class="btn btn-outline-primary" onclick="startStopwatch()">Start</button>
   <button type="button" class="btn btn-outline-success" onclick="splitTime()">Split</button>
   <button type="button" class="btn btn-outline-warning" onclick="stopStopwatch()">Stop</button>
   <button type="button" class="btn btn-outline-danger" onclick="resetStopwatch()">Reset</button>
   <button type="button" class="btn btn-outline-dark" onclick="exportCSV()">Export CSV</button>
  
<div class="py-4"> 
  <table id="splitTable" class="table table-hover py-4">
      <tr class="table-primary">
          <th>Lap</th>
           <th>Time</th>
       </tr>
   </table>
</div>
</div>

<h1>What is stopwatch</h1><p>A stopwatch is a device used to track the time that passes from when it starts to when it stops.</p>

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
                }, 10);
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
                const totalMilliseconds = elapsedTime;
                const totalSeconds = Math.floor(totalMilliseconds / 1000);
                const hours = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
                const minutes = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
                const seconds = String(totalSeconds % 60).padStart(2, '0');
                const milliseconds = String(totalMilliseconds % 1000).padStart(3, '0');
                
                let table = document.getElementById("splitTable");
                let row = table.insertRow();
                row.insertCell(0).innerText = lapCount;
                row.insertCell(1).innerText = `${hours}:${minutes}:${seconds}.${milliseconds}`;
            }
        }

        function updateStopwatch() {
            const totalMilliseconds = elapsedTime;
            const totalSeconds = Math.floor(totalMilliseconds / 1000);
            const hours = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
            const minutes = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
            const seconds = String(totalSeconds % 60).padStart(2, '0');
            const milliseconds = String(totalMilliseconds % 1000).padStart(3, '0');
            document.getElementById('stopwatch').innerText = `${hours}:${minutes}:${seconds}.${milliseconds}`;
        }

        function exportCSV() {
            let csvContent = "Lap,Time\n";
            const rows = document.querySelectorAll("#splitTable tr");
            rows.forEach((row, index) => {
                if (index > 0) {
                    let cols = row.querySelectorAll("td");
                    if (cols.length > 0) {
                        csvContent += cols[0].innerText + "," + cols[1].innerText + "\n";
                    }
                }
            });
            let blob = new Blob([csvContent], { type: "text/csv" });
            let a = document.createElement("a");
            a.href = URL.createObjectURL(blob);
            a.download = "stopwatch_times.csv";
            a.click();
        }

       
    </script>