# Cookie-Empire
Fun Cookie Clicker Game in Beta.
<html><head><base href="." />
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Cookie Empire - An addictive cookie clicker game where you build your cookie-based economy">
<title>Cookie Empire - Build Your Cookie Dynasty</title>
<link rel="icon" type="image/svg+xml" href="assets/favicon.svg">
<link rel="apple-touch-icon" href="assets/apple-touch-icon.png">
<style>
:root {
  --cookie-color: #cd853f;
  --primary: #8b4513;
  --secondary: #2a1b0a;
  --accent: #ffd700;
  --bg: #1a0f06;
}

body {
  font-family: 'Quicksand', sans-serif;
  background: var(--bg);
  color: #fff;
  margin: 0;
  padding: 0;
  min-height: 100vh;
  background-image: radial-gradient(circle at center, #2a1b0a 0%, #1a0f06 100%);
}

.main-nav {
  background: rgba(43, 27, 10, 0.9);
  backdrop-filter: blur(10px);
  padding: 1rem;
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 1px solid var(--accent);
}

.nav-content {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-logo {
  font-size: 1.5em;
  color: var(--accent);
  text-decoration: none;
  font-weight: bold;
}

.nav-links a {
  color: #fff;
  text-decoration: none;
  margin-left: 2rem;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: var(--accent);
}

footer {
  background: rgba(43, 27, 10, 0.9);
  padding: 1rem;
  margin-top: 3rem;
  border-top: 1px solid var(--accent);
}

.footer-content {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-right a {
  color: #fff;
  text-decoration: none;
  margin-left: 1rem;
  transition: color 0.3s;
}

.footer-right a:hover {
  color: var(--accent);
}

.game-title {
  font-size: 3.5em;
  margin: 20px;
  text-shadow: 0 0 10px var(--accent);
  background: linear-gradient(45deg, var(--primary), var(--accent));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

#cookie {
  width: 250px;
  height: 250px;
  cursor: pointer;
  filter: drop-shadow(0 0 10px var(--accent));
  transition: transform 0.1s, filter 0.3s;
}

#cookie:hover {
  transform: scale(1.1);
  filter: drop-shadow(0 0 20px var(--accent));
}

#cookie:active {
  transform: scale(0.95);
}

.stats-panel {
  background: rgba(43, 27, 10, 0.7);
  backdrop-filter: blur(10px);
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(0,0,0,0.3);
  margin: 20px auto;
  max-width: 400px;
}

#clicks, #cps {
  font-size: 1.5em;
  margin: 10px;
  text-shadow: 0 0 5px var(--accent);
}

.container {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 30px;
  max-width: 1400px;
  margin: 0 auto;
  padding: 20px;
}

.stats {
  background: rgba(43, 27, 10, 0.7);
  backdrop-filter: blur(10px);
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(0,0,0,0.3);
}

.upgrades {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.upgrade-item {
  background: linear-gradient(135deg, var(--secondary), rgba(43, 27, 10, 0.7));
  padding: 20px;
  border-radius: 15px;
  cursor: pointer;
  transition: all 0.3s;
  border: 1px solid rgba(255,255,255,0.1);
  position: relative;
  overflow: hidden;
}

.upgrade-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
  border-color: var(--accent);
}

.upgrade-item:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1), transparent);
  transform: translateX(-100%);
  transition: 0.5s;
}

.upgrade-item:hover:before {
  transform: translateX(100%);
}

.upgrade-item.locked {
  opacity: 0.7;
  cursor: not-allowed;
  filter: grayscale(1);
}

.upgrade-item .title {
  font-size: 1.2em;
  color: var(--accent);
  margin-bottom: 10px;
}

.upgrade-item .description {
  font-size: 0.9em;
  color: #ccc;
  margin-top: 10px;
  font-style: italic;
}

.cookie-rain {
  position: fixed;
  pointer-events: none;
  font-size: 24px;
  z-index: 1000;
}

.achievement {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: linear-gradient(135deg, rgba(139, 69, 19, 0.9), rgba(255, 215, 0, 0.9));
  padding: 15px 25px;
  border-radius: 10px;
  box-shadow: 0 0 20px rgba(255, 215, 0, 0.3);
  animation: slideIn 0.5s ease-out;
  z-index: 1000;
}

@keyframes slideIn {
  from { transform: translateX(100%); opacity: 0; }
  to { transform: translateX(0); opacity: 1; }
}

/* Loading animation */
.loading-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--bg);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
  animation: fadeOut 1s ease-out forwards;
}

@keyframes fadeOut {
  to { opacity: 0; visibility: hidden; }
}

.loading-spinner {
  width: 100px;
  height: 100px;
  border: 5px solid var(--primary);
  border-top-color: var(--accent);
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.about-corner {
  position: fixed;
  bottom: 20px;
  left: 20px;
  background: linear-gradient(135deg, var(--secondary), rgba(43, 27, 10, 0.9));
  padding: 15px;
  border-radius: 15px;
  max-width: 250px;
  border: 1px solid rgba(255,215,0,0.2);
  box-shadow: 0 0 20px rgba(0,0,0,0.3);
  font-size: 0.9em;
  line-height: 1.4;
  z-index: 900;
  transition: all 0.3s ease;
}

.about-corner:hover {
  transform: translateY(-5px);
  border-color: var(--accent);
  box-shadow: 0 5px 25px rgba(255,215,0,0.1);
}

.about-corner h3 {
  color: var(--accent);
  margin: 0 0 10px 0;
  font-size: 1.1em;
}

.about-corner p {
  margin: 0;
  color: #ccc;
}
</style>
<link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500;600;700&display=swap" rel="stylesheet">
</head>
<body>
<header>
  <nav class="main-nav">
    <div class="nav-content">
      <a href="https://cookie-empire.com" class="nav-logo">Cookie Empire</a>
      <div class="nav-links">
        <a href="https://cookie-empire.com/about">About</a>
        <a href="https://cookie-empire.com/changelog">Changelog</a>
        <a href="https://cookie-empire.com/leaderboard">Leaderboard</a>
        <a href="https://github.com/shahenshah/cookie-empire" target="_blank">GitHub</a>
      </div>
    </div>
  </nav>
</header>
<main>
<div class="loading-overlay">
  <div class="loading-spinner"></div>
</div>

<h1 class="game-title">Cookie Empire</h1>

<div class="stats-panel">
  <div id="clicks">Cookies: 0</div>
  <div id="cps">Cookies per second: 0</div>
</div>

<svg id="cookie" viewBox="0 0 100 100" onclick="clickCookie()">
  <defs>
    <radialGradient id="cookieGradient" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
      <stop offset="0%" style="stop-color:#deb887"/>
      <stop offset="100%" style="stop-color:var(--cookie-color)"/>
    </radialGradient>
  </defs>
  <circle cx="50" cy="50" r="45" fill="url(#cookieGradient)"/>
  <circle cx="30" cy="35" r="8" fill="var(--primary)"/>
  <circle cx="60" cy="40" r="8" fill="var(--primary)"/>
  <circle cx="45" cy="60" r="8" fill="var(--primary)"/>
</svg>

<div class="container">
  <div class="stats">
    <h2>Statistics</h2>
    <div id="total-clicks">Total clicks: 0</div>
    <div id="golden-cookies">Golden cookies clicked: 0</div>
  </div>
  
  <div class="upgrades">
    <div class="upgrade-item" onclick="buyUpgrade('cursor')">
      <div class="title">Cursor (Cost: <span id="cursor-cost">15</span>)</div>
      <div>Currently owned: <span id="cursor-owned">0</span></div>
      <div class="description">Automatically clicks once per second</div>
    </div>
    <div class="upgrade-item" onclick="buyUpgrade('grandma')">
      <div class="title">Grandma (Cost: <span id="grandma-cost">100</span>)</div>
      <div>Currently owned: <span id="grandma-owned">0</span></div>
      <div class="description">A nice grandma to bake cookies for you</div>
    </div>
    <div class="upgrade-item" onclick="buyUpgrade('farm')">
      <div class="title">Cookie Farm (Cost: <span id="farm-cost">500</span>)</div>
      <div>Currently owned: <span id="farm-owned">0</span></div>
      <div class="description">Grows cookie plants</div>
    </div>
    <div class="upgrade-item" onclick="buyUpgrade('factory')">
      <div class="title">Factory (Cost: <span id="factory-cost">3000</span>)</div>
      <div>Currently owned: <span id="factory-owned">0</span></div>
      <div class="description">Mass produces cookies industrially</div>
    </div>
    <div class="upgrade-item" onclick="buyUpgrade('mine')">
      <div class="title">Cookie Mine (Cost: <span id="mine-cost">10000</span>)</div>
      <div>Currently owned: <span id="mine-owned">0</span></div>
      <div class="description">Mines cookie dough from the earth</div>
    </div>
    <div class="upgrade-item" onclick="buyUpgrade('wizard')">
      <div class="title">Cookie Wizard (Cost: <span id="wizard-cost">50000</span>)</div>
      <div>Currently owned: <span id="wizard-owned">0</span></div>
      <div class="description">Conjures cookies using ancient magic</div>
    </div>
    <div class="upgrade-item" onclick="buyUpgrade('portal')">
      <div class="title">Cookie Portal (Cost: <span id="portal-cost">200000</span>)</div>
      <div>Currently owned: <span id="portal-owned">0</span></div>
      <div class="description">Opens dimensional gates to the cookie dimension</div>
    </div>
  </div>
</div>

<div class="about-corner">
  <h3>🍪 About Cookie Empire</h3>
  <p>Created by Shahenshah as a fun little project to test my newfound skills. Hope you enjoy clicking cookies as much as I enjoyed making this!</p>
</div>
</main>
<footer>
  <div class="footer-content">
    <div class="footer-left">
      <p>© 2024 Cookie Empire by Shahenshah</p>
    </div>
    <div class="footer-right">
      <a href="https://github.com/shahenshah" target="_blank">GitHub</a>
      <a href="https://twitter.com/shahenshah" target="_blank">Twitter</a>
    </div>
  </div>
</footer>
<script>
let cookies = 0;
let totalClicks = 0;
let goldenCookiesClicked = 0;
let cps = 0;

const upgrades = {
  cursor: { cost: 15, owned: 0, cps: 0.1 },
  grandma: { cost: 100, owned: 0, cps: 1 },
  farm: { cost: 500, owned: 0, cps: 5 },
  factory: { cost: 3000, owned: 0, cps: 20 },
  mine: { cost: 10000, owned: 0, cps: 100 },
  wizard: { cost: 50000, owned: 0, cps: 500 },
  portal: { cost: 200000, owned: 0, cps: 2000 }
};

function formatNumber(num) {
  if (num >= 1e6) return (num/1e6).toFixed(1) + 'M';
  if (num >= 1e3) return (num/1e3).toFixed(1) + 'K';
  return Math.floor(num);
}

function updateDisplay() {
  document.getElementById('clicks').textContent = `Cookies: ${formatNumber(cookies)}`;
  document.getElementById('cps').textContent = `Cookies per second: ${cps.toFixed(1)}`;
  document.getElementById('total-clicks').textContent = `Total clicks: ${totalClicks}`;
  document.getElementById('golden-cookies').textContent = `Golden cookies clicked: ${goldenCookiesClicked}`;
  
  for (const [key, upgrade] of Object.entries(upgrades)) {
    document.getElementById(`${key}-cost`).textContent = formatNumber(upgrade.cost);
    document.getElementById(`${key}-owned`).textContent = upgrade.owned;
  }
}

function clickCookie() {
  cookies++;
  totalClicks++;
  createCookieParticle();
  updateDisplay();
  
  // Random chance for golden cookie
  if (Math.random() < 0.01) {
    spawnGoldenCookie();
  }
}

function buyUpgrade(type) {
  const upgrade = upgrades[type];
  if (cookies >= upgrade.cost) {
    cookies -= upgrade.cost;
    upgrade.owned++;
    upgrade.cost = Math.ceil(upgrade.cost * 1.15);
    calculateCPS();
    updateDisplay();
    showAchievement(`Bought a new ${type}!`);
  }
}

function calculateCPS() {
  cps = 0;
  for (const upgrade of Object.values(upgrades)) {
    cps += upgrade.owned * upgrade.cps;
  }
}

function createCookieParticle() {
  const particle = document.createElement('div');
  particle.className = 'cookie-rain';
  particle.style.left = `${Math.random() * window.innerWidth}px`;
  particle.style.top = '-20px';
  particle.innerHTML = '🍪';
  document.body.appendChild(particle);
  
  const animation = particle.animate([
    { transform: 'translateY(0) rotate(0deg)' },
    { transform: `translateY(${window.innerHeight}px) rotate(360deg)` }
  ], {
    duration: 2000,
    easing: 'linear'
  });
  
  animation.onfinish = () => particle.remove();
}

function spawnGoldenCookie() {
  const golden = document.createElement('div');
  golden.style.position = 'fixed';
  golden.style.left = `${Math.random() * (window.innerWidth - 50)}px`;
  golden.style.top = `${Math.random() * (window.innerHeight - 50)}px`;
  golden.style.cursor = 'pointer';
  golden.innerHTML = '🌟';
  golden.style.fontSize = '40px';
  
  golden.onclick = () => {
    const bonus = Math.ceil(cookies * 0.1);
    cookies += bonus;
    goldenCookiesClicked++;
    updateDisplay();
    showAchievement(`Golden cookie! +${formatNumber(bonus)} cookies!`);
    golden.remove();
  };
  
  document.body.appendChild(golden);
  setTimeout(() => golden.remove(), 5000);
}

function showAchievement(text) {
  const achievement = document.createElement('div');
  achievement.className = 'achievement';
  achievement.textContent = text;
  document.body.appendChild(achievement);
  setTimeout(() => achievement.remove(), 3000);
}

// Main game loop
setInterval(() => {
  cookies += cps;
  updateDisplay();
}, 1000);

// Save game every 30 seconds
setInterval(() => {
  localStorage.setItem('cookieClicker', JSON.stringify({
    cookies,
    totalClicks,
    goldenCookiesClicked,
    upgrades
  }));
}, 30000);

// Load saved game
const savedGame = localStorage.getItem('cookieClicker');
if (savedGame) {
  const data = JSON.parse(savedGame);
  cookies = data.cookies;
  totalClicks = data.totalClicks;
  goldenCookiesClicked = data.goldenCookiesClicked;
  Object.assign(upgrades, data.upgrades);
  calculateCPS();
  updateDisplay();
}
</script>
</body></html>
