<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8">
  <title>System Freeze Simulation</title>
  <style>
    body {
      margin: 0;
      background: black;
      color: lime;
      font-family: monospace;
      overflow: hidden;
    }
    #screen {
      padding: 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>

<div id="screen">Initializing system...</div>

<script>
let time = 65;
const screen = document.getElementById("screen");

function fakeFreeze() {
  document.body.style.cursor = "wait";

  const interval = setInterval(() => {
    screen.innerHTML = `
      SYSTEM ERROR: CRITICAL FAILURE<br><br>
      Attempting recovery...<br>
      Time remaining: ${time}s<br><br>
      Do not turn off your computer.
    `;
    time--;

    // generowanie dużej ilości danych (lekko obciąża CPU)
    let spam = "";
    for (let i = 0; i < 50000; i++) {
      spam += Math.random();
    }

    if (time <= 0) {
      clearInterval(interval);
      screen.innerHTML = "System recovered successfully.";
      document.body.style.cursor = "default";
    }
  }, 1000);
}

// start po 1 sekundzie
setTimeout(fakeFreeze, 1000);
</script>

</body>
</html>
