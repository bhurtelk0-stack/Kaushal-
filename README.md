
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<title>Valentine 💖</title>

<style>
  body {
    margin: 0;
    height: 100vh;
    background: #ffe6eb;
    overflow: hidden;
    font-family: Arial, Helvetica, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  /* Floating hearts and kisses */
  .emoji {
    position: absolute;
    font-size: 24px;
    animation: floatUp 4s linear infinite;
    opacity: 0.8;
  }

  @keyframes floatUp {
    0% { transform: translateY(100vh); opacity: 10; }
    20% { opacity: 1; }
    100% { transform: translateY(-10vh); opacity: 10; }
  }

  .card {
    background: pink;
    padding: 30px;
    border-radius: 20px;
    width: 340px;
    text-align: center;
    box-shadow: 0 15px 40px rgba(0,0,0,0.25);
    position: relative;
    z-index: 10;
  }

  h1, h2 {
    color: #ff4d6d;
    font-weight: 600;
  }

  .buttons {
    position: relative;
    height: 120px;
  }

  button {
    padding: 12px 22px;
    font-size: 16px;
    border: none;
    border-radius: 30px;
    cursor: pointer;
    margin: 8px;
  }

  #yes {
    background: #ff4d6d;
    color: white;
  }

  #no {
    background: #adb5bd;
    color: white;
    position: absolute;
    right: 40px;
  }

  .hidden {
    display: none;
  }

  .option {
    width: 100%;
    background: #f1f3f5;
  }

  /* Crackers */
  .cracker {
    position: absolute;
    width: 50px;
    height: 10px;
    border-radius: 50%;
    animation: explode 5s ease-out forwards;
  }

  @keyframes explode {
    to {
      transform: translate(var(--x), var(--y)) scale(0);
      opacity: 0;
    }
  }

  /* Popup quiz invitation */
  #quizInvite {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: #ff4d6d;
    color: white;
    padding: 15px 18px;
    border-radius: 25px;
    box-shadow: 0 6px 15px rgba(255,77,109,0.4);
    font-weight: 600;
    cursor: pointer;
    display: none;
    user-select: none;
    z-index: 100;
    max-width: 280px;
  }

  #quizInvite:hover {
    background: #e84365;
  }

  /* Quiz container styling */
  #quiz {
    background: white;
    padding: 25px 20px;
    border-radius: 20px;
    width: 340px;
    text-align: center;
    box-shadow: 0 15px 40px rgba(0,0,0,0.25);
    z-index: 10;
    position: relative;
  }

  #options button {
    margin: 8px 0;
  }

  #result {
    font-weight: 600;
    color: #ff4d6d;
    margin-top: 20px;
  }
</style>
</head>
<body>

<div class="card" id="valentineCard">
  <h1 id="valentineText"> babyy will you be my valentine???? 💖</h1>
  <div class="buttons">
    <button id="yes">Yes 💕</button>
    <button id="no">No</button>
  </div>
</div>

<!-- Valentine confirmed message -->
<div class="card hidden" id="confirmedCard" style="width: 320px;">
  <h1>hehehehehe 😽💖</h1>
  <p>i knewwww ittttt!</p>
</div>

<!-- Quiz invite popup -->
<div id="quizInvite">Do you wanna play a quiz and win a gift? 👉🏻👈🏻</div>

<!-- Quiz container -->
<div class="card hidden" id="quiz">
  <h2 id="qText"></h2>
  <div id="options"></div>
  <div id="result"></div>
</div>

<script>
  // Floating hearts & kisses emojis
  const emojis = ["❤️","supriyeee","😘","💕","chuchundrii","mayaluuuy","kissyyyy","iloveyouuuu","kanchiiii","padhna jauuu"];
  setInterval(() => {
    const e = document.createElement("div");
    e.className = "emoji";
    e.innerText = emojis[Math.floor(Math.random()*emojis.length)];
    e.style.left = Math.random() * 100 + "vw";
    document.body.appendChild(e);
    setTimeout(() => e.remove(), 6000);
  }, 300);

  // NO button dodge loop
  const noBtn = document.getElementById("no");
  const noTexts = [
    "No",
    "Are you sure?",
    "kutaii khaneyyy??😐",
    "Still no?",
    "achiiiiii 😤",
    "Try Yes 😌",
    "yess in cha tyaa",
    "chocolate didinaaa",
    "parkhaa naa timlaii",
    "jauuu haiiii"
  ];
  let n = 0;
  function dodgeNo() {
    const x = Math.random() * 200;
    const y = Math.random() * 70;
    noBtn.style.left = x + "px";
    noBtn.style.top = y + "px";
    noBtn.innerText = noTexts[n++ % noTexts.length];
  }
  noBtn.onclick = dodgeNo;
  noBtn.ontouchstart = dodgeNo;

  // YES click — show confirmed + crackers + invite quiz popup
  const yesBtn = document.getElementById("yes");
  const valCard = document.getElementById("valentineCard");
  const confCard = document.getElementById("confirmedCard");
  const quizInvite = document.getElementById("quizInvite");
  const quizCard = document.getElementById("quiz");
  const valText = document.getElementById("valentineText");

  yesBtn.onclick = () => {
    // Hide initial valentine card
    valCard.classList.add("hidden");
    // Show confirmed card
    confCard.classList.remove("hidden");
    // Fire crackers
    fireCrackers();
    // Show quiz invite popup after short delay
    setTimeout(() => {
      quizInvite.style.display = "block";
    }, 1500);
  };

  // Firecracker animation
  function fireCrackers() {
    for (let i = 0; i < 50; i++) {
      const c = document.createElement("div");
      c.className = "cracker";
      c.style.left = "50%";
      c.style.top = "50%";
      c.style.background = `hsl(${Math.random()*360},100%,60%)`;
      c.style.setProperty("--x", (Math.random()*400 - 200) + "px");
      c.style.setProperty("--y", (Math.random()*400 - 200) + "px");
      document.body.appendChild(c);
      setTimeout(() => c.remove(), 1000);
    }
  }

  // Quiz questions
  const quiz = [
    { q: "whats my fav food???", a: ["masuu bhat", "mee"], c: 1 },
    { q: "T20 game vanekoo kasto???", a: ["50", "20"], c: 1 },
    { q: "what was my first gift????", a: ["clip", "kinder joy"], c: 0 },
    { q: "what was the time when i text youu?", a: ["9 or near that", "8:45 or something"], c: 1 },
    { q: "how old was im when i texted you?", a: ["16.1", "15.10"], c: 1 },
    { q: "am i jealous bf or clam?", a: [" both", " only one "], c: 0 },
    { q: "Jealous type???", a: ["less", "alottt"], c: 1 },
    { q: "Love language?", a: [" spending time talkingg,touchyy", " video call or text, touchyy  "], c: 0 },
    { q: "Romantic or funny??", a: ["funny", "romantic"], c: 1 },
    { q: "Forever?", a: ["Yes", "Obviously"], c: 1 }
  ];

  let index = 0, score = 0;
  const qText = document.getElementById("qText");
  const optionsBox = document.getElementById("options");
  const resultBox = document.getElementById("result");

  // Click on quiz invite popup → start quiz
  quizInvite.onclick = () => {
    quizInvite.style.display = "none";
    confCard.classList.add("hidden");
    document.getElementById("quiz").classList.remove("hidden");
    showQuestion();
  };

  function showQuestion() {
    if (index >= quiz.length) {
      showResult();
      return;
    }
    qText.innerText = quiz[index].q;
    optionsBox.innerHTML = "";

    quiz[index].a.forEach((opt, i) => {
      const btn = document.createElement("button");
      btn.className = "option";
      btn.innerText = opt;
      btn.onclick = () => {
        if (i === quiz[index].c) score++;
        index++;
        showQuestion();
      };
      optionsBox.appendChild(btn);
    });
  }

  function showResult() {
    qText.innerText = "Your result:";
    optionsBox.innerHTML = "";
    if (score >= 6) {
      resultBox.innerHTML = `🎁 You scored ${score}/10<br><br>jityeuuu , gift paunaa chaiii ekk kisyyy haiiii ! 😌💖`;
      fireCrackers();
    } else {
      resultBox.innerHTML = `You scored ${score}/10 😅<br><br>Close! Maybe next time 😉`;
    }
  }
</script>

</body>
</html>
