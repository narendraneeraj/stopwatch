---
layout: default
title: World Clock
permalink: /world-clock/
---

<h1 class="text-center my-4">World Clock</h1>

<div class="container">
    <div class="row">
        <div class="col-md-4">
            <h3>New York (USA)</h3>
            <p id="new-york-time" class="fs-5"></p>
        </div>
        <div class="col-md-4">
            <h3>London (UK)</h3>
            <p id="london-time" class="fs-5"></p>
        </div>
        <div class="col-md-4">
            <h3>Tokyo (Japan)</h3>
            <p id="tokyo-time" class="fs-5"></p>
        </div>
    </div>
</div>

<script>
    function updateWorldClock() {
        const options = { timeZoneName: "short", hour: "2-digit", minute: "2-digit", second: "2-digit" };

        document.getElementById("new-york-time").innerText = new Date().toLocaleTimeString("en-US", { timeZone: "America/New_York", ...options });
        document.getElementById("london-time").innerText = new Date().toLocaleTimeString("en-GB", { timeZone: "Europe/London", ...options });
        document.getElementById("tokyo-time").innerText = new Date().toLocaleTimeString("ja-JP", { timeZone: "Asia/Tokyo", ...options });
    }

    setInterval(updateWorldClock, 1000);
    updateWorldClock(); // Run initially
</script>
