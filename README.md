<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Happy Birthday!</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>🎉 Happy Birthday! 🎂</h1>
    <p>Wishing you a day filled with joy, love, and laughter!</p>
    <button onclick="playMusic()">🎵 Play Music</button>
    <canvas id="confetti"></canvas>
  </div>

  <audio id="birthdaySong" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"></audio>
  <script src="script.js"></script>
</body>
</html>
body {
  margin: 0;
  padding: 0;
  font-family: 'Comic Sans MS', cursive, sans-serif;
  background: linear-gradient(to right, #ff9a9e, #fad0c4);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  overflow: hidden;
}

.container {
  text-align: center;
  color: #fff;
  z-index: 10;
  position: relative;
}

h1 {
  font-size: 3em;
  margin-bottom: 0.5em;
  animation: pop 1s ease-out forwards;
}

p {
  font-size: 1.5em;
  margin-bottom: 1em;
}

button {
  padding: 10px 20px;
  font-size: 1em;
  border: none;
  border-radius: 20px;
  background-color: #ff6f91;
  color: white;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  background-color: #ff3e6c;
}

@keyframes pop {
  0% { transform: scale(0); opacity: 0; }
  100% { transform: scale(1); opacity: 1; }
}

canvas#confetti {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}
function playMusic() {
  const audio = document.getElementById("birthdaySong");
  audio.play();
}

// 🎉 Simple confetti
const canvas = document.getElementById('confetti');
const ctx = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let confetti = [];

function createConfetti() {
  for (let i = 0; i < 150; i++) {
    confetti.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      r: Math.random() * 6 + 2,
      d: Math.random() * 10 + 2,
      color: `hsl(${Math.random() * 360}, 100%, 50%)`,
      tilt: Math.floor(Math.random() * 10) - 5
    });
  }
}

function drawConfetti() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  confetti.forEach((c, i) => {
    ctx.beginPath();
    ctx.lineWidth = c.r;
    ctx.strokeStyle = c.color;
    ctx.moveTo(c.x + c.tilt + c.r / 2, c.y);
    ctx.lineTo(c.x + c.tilt, c.y + c.tilt + c.r / 2);
    ctx.stroke();
  });

  updateConfetti();
}

function updateConfetti() {
  confetti.forEach((c, i) => {
    c.y += Math.cos(c.d) + 1 + c.r / 2;
    c.x += Math.sin(0.5);

    if (c.y > canvas.height) {
      confetti[i].y = -10;
      confetti[i].x = Math.random() * canvas.width;
    }
  });
}

function animate() {
  drawConfetti();
  requestAnimationFrame(animate);
}

createConfetti();
animate();
