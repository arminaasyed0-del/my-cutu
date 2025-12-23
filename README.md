<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Kisi Chahiye?</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Quicksand:wght@500&display=swap" rel="stylesheet">

<style>
  body {
    margin: 0;
    height: 100vh;
    background: linear-gradient(135deg, #ffe6f0, #fff0f5);
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Poppins', sans-serif;
    overflow: hidden;
  }

  .card {
    background: rgba(255,255,255,0.85);
    backdrop-filter: blur(10px);
    padding: 35px 45px;
    border-radius: 25px;
    text-align: center;
    box-shadow: 0 25px 50px rgba(0,0,0,0.15);
    position: relative;
  }

  .bunny {
    width: 110px;
    margin-bottom: 15px;
  }

  .side {
    position: absolute;
    width: 70px;
  }

  .top { top: -35px; left: 50%; transform: translateX(-50%); }
  .bottom { bottom: -35px; left: 50%; transform: translateX(-50%); }
  .left { left: -35px; top: 50%; transform: translateY(-50%); }
  .right { right: -35px; top: 50%; transform: translateY(-50%); }

  h2 {
    font-family: 'Quicksand', sans-serif;
    font-size: 26px;
    margin-bottom: 15px;
  }

  p {
    min-height: 24px;
    color: #666;
  }

  button {
    padding: 12px 28px;
    font-size: 16px;
    border: none;
    border-radius: 14px;
    cursor: pointer;
    margin: 10px;
    transition: transform 0.3s ease;
  }

  #yes {
    background: #ff8fab;
    color: white;
    transform: scale(1);
  }

  #no {
    background: #ccc;
    color: #444;
    position: absolute;
    transform: scale(1);
  }

  .heart {
    position: absolute;
    color: pink;
    font-size: 20px;
    animation: float 5s linear infinite;
  }

  @keyframes float {
    from { transform: translateY(100vh); opacity: 1; }
    to { transform: translateY(-10vh); opacity: 0; }
  }
</style>
</head>

<body>

<div class="card" id="mainCard">
  <!-- DIFFERENT GIFS AROUND -->
  <img class="side top" src="https://media.giphy.com/media/3oriO0OEd9QIDdllqo/giphy.gif">
  <img class="side bottom" src="https://media.giphy.com/media/MDJ9IbxxvDUQM/giphy.gif">
  <img class="side left" src="https://media.giphy.com/media/5GoVLqeAOo6PK/giphy.gif">
  <img class="side right" src="https://media.giphy.com/media/26BRrSvJUa0crqw4E/giphy.gif">

  <!-- START GIF (cute bunny / cat, romantic, no real people) -->
  <img class="bunny" src="https://media.giphy.com/media/12HZukMBlutpoQ/giphy.gif">

  <h2>Kisi chahiye?</h2>
  <p id="msg"></p>
  <button id="yes" onclick="yesClick()">Yes</button>
  <button id="no" onclick="noClick()">No</button>
</div>

<script>
let noCount = 0;
let moveCount = 0;
let maxMoves = 7;

const messages = [
  "baby🥺🥺🥺",
  "nohhh",
  "",
  "Abee",
  "😒"
];

const noBtn = document.getElementById("no");
const yesBtn = document.getElementById("yes");
const msg = document.getElementById("msg");

const originalPos = {
  left: noBtn.offsetLeft,
  top: noBtn.offsetTop
};

function randomMove() {
  const x = Math.random() * (window.innerWidth - 120);
  const y = Math.random() * (window.innerHeight - 120);
  noBtn.style.left = x + "px";
  noBtn.style.top = y + "px";
}

function resetPosition() {
  noBtn.style.left = originalPos.left + "px";
  noBtn.style.top = originalPos.top + "px";
}

function noClick() {
  noCount++;

  if (noCount <= messages.length) {
    msg.innerText = messages[noCount - 1];
  }

  if (moveCount < maxMoves) {
    randomMove();
    moveCount++;

    if (moveCount === maxMoves) {
      setTimeout(resetPosition, 300);
    }
  } else {
    noBtn.style.transform = `scale(${Math.max(0.4, 1 - (noCount - maxMoves) * 0.08)})`;
    yesBtn.style.transform = `scale(${1 + (noCount - maxMoves) * 0.12})`;
  }
}

function yesClick() {
  document.body.style.background = "linear-gradient(135deg, #ffb6c1, #ffe4e1)";
  document.body.innerHTML = `
    <div style="text-align:center;font-family:'Quicksand',sans-serif;color:#fff;">
      <img src="https://media.giphy.com/media/MDJ9IbxxvDUQM/giphy.gif" width="180"><br><br>
      <img src="https://media.giphy.com/media/3oriO0OEd9QIDdllqo/giphy.gif" width="120">
      <img src="https://media.giphy.com/media/5GoVLqeAOo6PK/giphy.gif" width="120"><br><br>
      <h1>MYYY BABYYYYYY🥺🥺💋💋💋💋❤️❤️❤️❤️❤️❤️😘😘😘😘😘😘💋💋💋</h1>
      <h2>my shona baby my pyaara baby my cutu baby my handsome baby😘❤️😘❤️😘❤️❤️❤️😘😘😘😘💋💋😘💋😘💋😘💋😘❤️❤️💋😘💋😘💋😘😘💋😘❤️😘❤️😘❤️❤️💋💋😘</h2>
    </div>
  `;

  for (let i = 0; i < 40; i++) {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "💗";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.animationDuration = (3 + Math.random() * 3) + "s";
    document.body.appendChild(heart);
  }
}
</script>

</body>
</html>
