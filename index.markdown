---
layout: default
title: Online Stopwatch | Digital Stopwatch - Easy to Use
description: "Use our online stopwatch, Accurate and user-friendly. Track lap times with export in CSV, Digital stopwatch, and enjoy optional split intervals for your timing needs."
no_title: true
hide_meta: true
---

<div class="container text-center">
<div class="container text-center">
<h1>Stopwatch</h1>
 
 <div class="display py-4">
 <span id="hours">00</span>: <span id="minutes">00</span>: <span id="seconds">00</span>: <span id="centiseconds">00</span>
 </div>

<!-- Buttons -->
<button id="startPauseBtn" class="btn btn-outline-primary" onclick="toggleStartPause()">Start</button>
<button class="btn btn-outline-success" onclick="splitTime()">Lap</button>
<button class="btn btn-outline-warning" onclick="resetStopwatch()">Reset</button>
<button class="btn btn-outline-dark" onclick="exportCSV()">Export CSV</button>

<!-- Lap Table -->
<div class="py-4">
  <table id="splitTable" class="table table-hover">
     <tr class="table-primary">
       <th>Lap</th>
        <th>Time</th>
      </tr>
     </table>
   </div>
</div>
</div>

<h2>What is stopwatch</h2><p>A stopwatch is a device used to track the time that passes from when it starts to when it stops.</p>

<script src="{{ '/assets/js/stopwatch.js' | relative_url }}"></script>