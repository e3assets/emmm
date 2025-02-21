<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Eeny Meeny Miny Moe - Ultimate Elimination Game</title>
  <!-- SEO Meta Tags -->
  <meta name="description" content="Play the ultimate Eeny Meeny Miny Moe elimination game with fun animations, sound effects, and clear instructions on how to use it. Enjoy and subscribe for more updates." />
  <meta name="keywords" content="Eeny Meeny Miny Moe, elimination game, decision making, party game, fun game, SEO friendly game" />
  <!-- Canvas Confetti Library -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.4.0/dist/confetti.browser.min.js"></script>
  <style>
    /* Smooth scrolling */
    html {
      scroll-behavior: smooth;
    }
    /* Global Styles */
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #74ABE2, #5563DE);
      color: #fff;
      margin: 0;
      padding: 10px; /* Reduced padding */
      text-align: center;
      overflow-x: hidden;
    }
    /* Headings in Comic Sans */
    h1, h2, h3 {
      font-family: "Comic Sans MS", cursive, sans-serif;
      margin-bottom: 10px;
    }
    /* Responsive Container */
    .container {
      max-width: 1200px;
      margin: 0 auto;
    }
    /* Sections with fade-in effect */
    .section {
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 1s ease-out, transform 1s ease-out;
    }
    .section.visible {
      opacity: 1;
      transform: translateY(0);
    }
    /* Input Section */
    #inputSection {
      margin-bottom: 10px;
    }
    #playersInput {
      width: 60ch;
      max-width: 90%;
      height: 80px;
      padding: 5px;
      font-size: 16px;
      border-radius: 5px;
      border: none;
    }
    button {
      padding: 8px 16px;
      font-size: 16px;
      margin-top: 10px;
      cursor: pointer;
      border: none;
      border-radius: 5px;
      background-color: #00cc00; /* Green background */
      color: #fff;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #00aa00;
    }
    /* Game Grid */
    #grid {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      max-width: 800px;
      margin: 10px auto;
      gap: 10px;
    }
    .tile {
      width: 100px;
      height: 100px;
      background: #fff;
      color: #333;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 18px;
      border: 2px solid #333;
      border-radius: 5px;
      transition: transform 0.3s, background 0.3s;
    }
    .highlight {
      background: #ffcc00;
      transform: scale(1.1);
    }
    /* Fade-out effect for eliminated players */
    .fade-out {
      animation: fadeOut 1s forwards;
    }
    @keyframes fadeOut {
      to { opacity: 0; transform: scale(0.5); }
    }
    /* Notification */
    #notification {
      position: fixed;
      bottom: 10px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(255, 204, 0, 0.9);
      color: #333;
      padding: 8px 16px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
      display: none;
    }
    /* Winner Message */
    #winnerMessage {
      font-size: 28px;
      font-weight: bold;
      margin-top: 10px;
      animation: winnerAnimation 1s infinite alternate;
    }
    @keyframes winnerAnimation {
      from { transform: scale(1); }
      to { transform: scale(1.1); }
    }
    /* Balloon Styling */
    .balloon {
      position: fixed;
      bottom: -150px;
      width: 40px;
      height: 55px;
      background-color: red;
      border-radius: 50%;
      opacity: 0.9;
      z-index: 1000;
      animation: balloonUp 5s ease-in forwards;
    }
    @keyframes balloonUp {
      0% {
        transform: translateX(0) translateY(0) scale(1);
        opacity: 0.9;
      }
      100% {
        transform: translateX(0) translateY(-120vh) scale(1.2);
        opacity: 0.3;
      }
    }
    /* What is This Game For Section */
    #howToPlaySection {
      margin: 20px auto;
      max-width: 800px;
      background: #fff;
      color: #333;
      padding: 10px;
      border-radius: 5px;
    }
    #howToPlaySection table {
      width: 100%;
      border-collapse: collapse;
    }
    #howToPlaySection th, #howToPlaySection td {
      padding: 8px;
      border: 1px solid #ccc;
      text-align: left;
    }
    #howToPlaySection th {
      background-color: #f4f4f4;
    }
    /* Stats Section */
    #statsSection {
      margin: 20px auto;
      max-width: 600px;
      background: #fff;
      color: #333;
      padding: 10px;
      border-radius: 5px;
    }
    #statsSection table {
      width: 100%;
      border-collapse: collapse;
    }
    #statsSection th, #statsSection td {
      padding: 8px;
      border: 1px solid #ccc;
      text-align: center;
    }
    #statsSection th {
      background-color: #f4f4f4;
    }
    /* FAQ Section */
    #faqSection {
      margin: 20px auto;
      max-width: 600px;
      background: #fff;
      color: #333;
      padding: 10px;
      border-radius: 5px;
    }
    #faqSection table {
      width: 100%;
      border-collapse: collapse;
    }
    #faqSection th, #faqSection td {
      padding: 8px;
      border: 1px solid #ccc;
      text-align: left;
    }
    #faqSection th {
      background-color: #f4f4f4;
    }
    /* Newsletter Section */
    #newsletter {
      background: #fff;
      color: #333;
      padding: 10px;
      margin-top: 20px;
      border-radius: 5px;
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
    }
    #newsletter input[type="email"] {
      width: 80%;
      padding: 8px;
      margin: 8px 0;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    #newsletter input[type="submit"] {
      padding: 8px 16px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      background: #5563DE;
      color: #fff;
      cursor: pointer;
    }
    /* Advertisement Section */
    #adSection {
      background: #fff;
      color: #333;
      padding: 10px;
      margin-top: 20px;
      border-radius: 5px;
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
      font-size: 16px;
    }
    /* Responsive Adjustments */
    @media (max-width: 600px) {
      .tile {
        width: 80px;
        height: 80px;
        font-size: 16px;
      }
      #playersInput {
        width: 90%;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <header class="section">
      <h1>Eeny Meeny Miny Moe</h1>
      <p>Play our fun elimination game!</p>
    </header>
    
    <!-- Input Section -->
    <section id="inputSection" class="section">
      <textarea id="playersInput" placeholder="Enter names, one per line..."></textarea><br>
      <button onclick="startGame()">Start Game</button>
    </section>
    
    <!-- Game Grid -->
    <section id="gameSection" class="section">
      <div id="grid"></div>
      <div id="winnerMessage"></div>
      <div id="notification"></div>
    </section>
    
    <!-- What is This Game For Section -->
    <section id="howToPlaySection" class="section">
      <h2>What is This Game For?</h2>
      <table>
        <tr>
          <th>Example</th>
          <th>Description</th>
        </tr>
        <tr>
          <td>Decision Making</td>
          <td>Use the game to make fun decisions or resolve group choices.</td>
        </tr>
        <tr>
          <td>Party Entertainment</td>
          <td>A great icebreaker and party game to engage guests.</td>
        </tr>
        <tr>
          <td>Team Building</td>
          <td>Encourage teamwork and laughter in corporate or school settings.</td>
        </tr>
        <tr>
          <td>Random Selections</td>
          <td>Let chance decide winners for contests, giveaways, or everyday fun.</td>
        </tr>
      </table>
    </section>
    
    <!-- Stats Section -->
    <section id="statsSection" class="section">
      <h2>Game Stats</h2>
      <table>
        <tr>
          <th>Games Played</th>
          <th>Hours Played</th>
        </tr>
        <tr>
          <td id="gamesPlayedCounter">0</td>
          <td id="hoursPlayedCounter">0.00</td>
        </tr>
      </table>
    </section>
    
    <!-- FAQ Section -->
    <section id="faqSection" class="section">
      <h2>Frequently Asked Questions</h2>
      <table>
        <tr>
          <th>Question</th>
          <th>Answer</th>
        </tr>
        <tr>
          <td>Is my information safe?</td>
          <td>Yes! We do not store any personal data from the game. All inputs remain local to your device.</td>
        </tr>
        <tr>
          <td>Can the game be manipulated?</td>
          <td>The game runs entirely on the client side. While someone with technical knowledge might modify their local copy, it does not affect other players.</td>
        </tr>
      </table>
    </section>
    
    <!-- Newsletter Subscription Section -->
    <section id="newsletter" class="section">
      <h2>Subscribe to Our Newsletter</h2>
      <p>Get the latest updates, news, and fun games delivered straight to your inbox!</p>
      <form action="https://YOUR-MAILCHIMP-URL-HERE" method="post" target="_blank" novalidate>
        <input type="email" name="EMAIL" placeholder="Your email address" required />
        <input type="submit" value="Subscribe" />
      </form>
    </section>
    
    <!-- Advertisement Section -->
    <section id="adSection" class="section">
      <!-- Insert your ad code here -->
      <p>Advertisement</p>
    </section>
  </div>
  
  <!-- Audio Elements -->
  <audio id="rhymeAudio" src="https://www.soundjay.com/button/sounds/button-10.mp3"></audio>
  <audio id="buzzSound" src="https://www.soundjay.com/misc/sounds/buzzer-1.mp3"></audio>
  <audio id="winnerSound" src="https://www.soundjay.com/misc/sounds/bell-ringing-05.mp3"></audio>
  
  <!-- Game Script -->
  <script>
    let names = [];
    let currentHighlight = 0;
    let highlightInterval;
    let startTime = 0;
    let gamesPlayed = 0;
    let hoursPlayed = 0;
    
    const rhymeAudio = document.getElementById('rhymeAudio');
    const buzzSound = document.getElementById('buzzSound');
    const winnerSound = document.getElementById('winnerSound');

    function startGame() {
      document.getElementById('winnerMessage').innerText = "";
      clearInterval(highlightInterval);
      startTime = Date.now();
      names = shuffle(document.getElementById('playersInput').value.trim().split("\n").filter(n => n));
      if (names.length < 2) {
        alert("Please enter at least 2 names.");
        return;
      }
      const grid = document.getElementById('grid');
      grid.innerHTML = "";
      names.forEach((name, index) => {
        const tile = document.createElement('div');
        tile.classList.add('tile');
        tile.id = 'tile-' + index;
        tile.innerText = name;
        grid.appendChild(tile);
      });
      currentHighlight = Math.floor(Math.random() * document.querySelectorAll('.tile').length);
      runEliminationCycle();
    }

    // Fisher-Yates shuffle algorithm
    function shuffle(array) {
      let currentIndex = array.length, randomIndex;
      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;
        [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
      }
      return array;
    }

    function runEliminationCycle() {
      highlightInterval = setInterval(() => {
        document.querySelectorAll('.tile').forEach(tile => tile.classList.remove('highlight'));
        const gridTiles = document.querySelectorAll('.tile');
        if (gridTiles.length === 0) return;
        let indexToHighlight = currentHighlight % gridTiles.length;
        gridTiles[indexToHighlight].classList.add('highlight');
        currentHighlight++;
      }, 400);

      setTimeout(() => {
        clearInterval(highlightInterval);
        eliminatePlayer();
      }, 400 * 10);
    }

    function eliminatePlayer() {
      const gridTiles = Array.from(document.querySelectorAll('.tile'));
      const highlightedTile = document.querySelector('.tile.highlight');
      const eliminatedTile = highlightedTile ? highlightedTile : gridTiles[Math.floor(Math.random() * gridTiles.length)];
      rhymeAudio.currentTime = 0;
      rhymeAudio.play();
      buzzSound.currentTime = 0;
      buzzSound.play();
      const eliminatedName = eliminatedTile.innerText;
      notify(`${eliminatedName} is out of the game!`);
      eliminatedTile.classList.add('fade-out');
      setTimeout(() => { eliminatedTile.remove(); }, 1000);
      names = names.filter(name => name !== eliminatedName);
      if (names.length === 1) {
        setTimeout(() => { declareWinner(); }, 1500);
      } else {
        currentHighlight = Math.floor(Math.random() * document.querySelectorAll('.tile').length);
        setTimeout(() => { runEliminationCycle(); }, 1000);
      }
    }

    function declareWinner() {
      document.querySelectorAll('.tile').forEach(tile => tile.classList.remove('highlight'));
      const winnerTile = document.querySelector('.tile');
      if (winnerTile) {
        document.getElementById('winnerMessage').innerText = `Winner: ${winnerTile.innerText}`;
        winnerSound.currentTime = 0;
        winnerSound.play();
        confetti({
          particleCount: 150,
          spread: 70,
          origin: { y: 0.6 }
        });
        launchBalloons(15);
        const gameDurationHours = (Date.now() - startTime) / 3600000;
        gamesPlayed++;
        hoursPlayed += gameDurationHours;
        updateStats();
      }
    }

    function notify(message) {
      const notification = document.getElementById('notification');
      notification.innerText = message;
      notification.style.display = 'block';
      setTimeout(() => { notification.style.display = 'none'; }, 2000);
    }

    function launchBalloons(count) {
      for (let i = 0; i < count; i++) {
        const balloon = document.createElement('div');
        balloon.classList.add('balloon');
        balloon.style.backgroundColor = getRandomColor();
        balloon.style.left = Math.random() * 100 + "vw";
        document.body.appendChild(balloon);
        balloon.addEventListener('animationend', () => { balloon.remove(); });
      }
    }

    function getRandomColor() {
      const colors = ['#FF5733', '#FFBD33', '#75FF33', '#33FFBD', '#3375FF', '#BD33FF'];
      return colors[Math.floor(Math.random() * colors.length)];
    }
    
    function updateStats() {
      document.getElementById("gamesPlayedCounter").innerText = gamesPlayed;
      document.getElementById("hoursPlayedCounter").innerText = hoursPlayed.toFixed(2);
    }
    
    // IntersectionObserver for scroll animations
    document.addEventListener("DOMContentLoaded", () => {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add("visible");
          }
        });
      }, { threshold: 0.2 });
      
      document.querySelectorAll(".section").forEach(section => {
        observer.observe(section);
      });
    });
  </script>
</body>
</html>
