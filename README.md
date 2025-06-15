<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mushroom Snail Clicker</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            background: linear-gradient(135deg, #2d5016, #4a7c24, #2d5016);
            color: #fff;
            overflow-x: hidden;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 20px;
            min-height: 100vh;
        }

        .main-game {
            text-align: center;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 20px;
            padding: 30px;
            backdrop-filter: blur(10px);
            height: fit-content;
        }

        .sidebar {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 20px;
            padding: 20px;
            backdrop-filter: blur(10px);
            height: fit-content;
            max-height: 90vh;
            overflow-y: auto;
        }

        .title {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            background: linear-gradient(45deg, #ff6b6b, #ffd93d, #6bcf7f);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .stats {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
            flex-wrap: wrap;
        }

        .stat {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 15px;
            margin: 5px;
            min-width: 120px;
            backdrop-filter: blur(5px);
        }

        .stat-value {
            font-size: 1.5em;
            font-weight: bold;
            color: #ffd93d;
        }

        .mushroom-snail {
            width: 200px;
            height: 200px;
            margin: 20px auto;
            cursor: pointer;
            transition: all 0.1s ease;
            position: relative;
            background: linear-gradient(135deg, #8b4513, #d2691e);
            border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .mushroom-cap {
            width: 120px;
            height: 80px;
            background: linear-gradient(135deg, #cc4444, #ff6666);
            border-radius: 50% 50% 50% 50% / 100% 100% 0% 0%;
            position: relative;
            margin-bottom: 20px;
        }

        .mushroom-spots {
            position: absolute;
            width: 15px;
            height: 15px;
            background: #ffeeaa;
            border-radius: 50%;
        }

        .spot1 { top: 20px; left: 20px; }
        .spot2 { top: 30px; right: 25px; }
        .spot3 { top: 45px; left: 40px; }

        .snail-eyes {
            display: flex;
            gap: 30px;
            margin-top: -10px;
        }

        .eye {
            width: 20px;
            height: 25px;
            background: #f4e4bc;
            border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
            position: relative;
        }

        .pupil {
            width: 12px;
            height: 12px;
            background: #000;
            border-radius: 50%;
            position: absolute;
            top: 2px;
            left: 4px;
        }

        .mushroom-snail:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 40px rgba(255, 215, 61, 0.3);
        }

        .mushroom-snail:active {
            transform: scale(0.95);
        }

        .click-effect {
            position: absolute;
            color: #ffd93d;
            font-size: 2em;
            font-weight: bold;
            pointer-events: none;
            animation: floatUp 1s ease-out forwards;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
        }

        @keyframes floatUp {
            from {
                opacity: 1;
                transform: translateY(0);
            }
            to {
                opacity: 0;
                transform: translateY(-100px);
            }
        }

        .upgrade-section {
            margin-top: 20px;
            margin-bottom: 25px;
        }

        .upgrade-section h3 {
            color: #ffd93d;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.2em;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
        }

        .upgrade {
            background: rgba(255, 255, 255, 0.15);
            border: 2px solid rgba(255, 255, 255, 0.2);
            color: white;
            padding: 12px;
            margin: 8px 0;
            border-radius: 12px;
            cursor: pointer;
            width: 100%;
            text-align: left;
            transition: all 0.3s ease;
            backdrop-filter: blur(5px);
            display: block;
            font-size: 0.9em;
        }

        .upgrade:hover {
            background: rgba(255, 255, 255, 0.25);
            border-color: rgba(255, 215, 61, 0.5);
            transform: translateX(3px);
            box-shadow: 0 4px 15px rgba(255, 215, 61, 0.2);
        }

        .upgrade:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
            background: rgba(255, 255, 255, 0.05);
        }

        .upgrade-name {
            font-weight: bold;
            color: #ffd93d;
        }

        .upgrade-cost {
            color: #ff6b6b;
            font-size: 0.9em;
        }

        .upgrade-effect {
            color: #6bcf7f;
            font-size: 0.8em;
        }

        .prestige-section {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 2px solid rgba(255, 255, 255, 0.2);
        }

        .prestige-btn {
            background: linear-gradient(45deg, #ff6b6b, #ffd93d);
            border: none;
            color: white;
            padding: 15px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1.1em;
            font-weight: bold;
            width: 100%;
            transition: all 0.3s ease;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
        }

        .prestige-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 20px rgba(255, 107, 107, 0.4);
        }

        .prestige-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .achievements {
            margin-top: 20px;
        }

        .achievement {
            background: rgba(255, 215, 61, 0.15);
            padding: 12px;
            margin: 8px 0;
            border-radius: 10px;
            border-left: 4px solid #ffd93d;
            font-size: 0.85em;
            transition: all 0.3s ease;
        }

        .achievement.unlocked {
            background: rgba(107, 207, 127, 0.2);
            border-left-color: #6bcf7f;
            color: #6bcf7f;
            box-shadow: 0 2px 10px rgba(107, 207, 127, 0.3);
        }

        .particle {
            position: absolute;
            width: 6px;
            height: 6px;
            background: #ffd93d;
            border-radius: 50%;
            pointer-events: none;
            animation: particle 2s ease-out forwards;
        }

        @keyframes particle {
            from {
                opacity: 1;
                transform: scale(1);
            }
            to {
                opacity: 0;
                transform: scale(0) translateY(-200px);
            }
        }

        @media (max-width: 768px) {
            .container {
                grid-template-columns: 1fr;
                gap: 10px;
            }
            
            .sidebar {
                order: 2;
                max-height: none;
            }
            
            .main-game {
                order: 1;
            }
            
            .mushroom-snail {
                width: 150px;
                height: 150px;
            }
            
            .title {
                font-size: 1.8em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="main-game">
            <h1 class="title">🐌🍄 Mushroom Snail Empire 🍄🐌</h1>
            
            <div class="stats">
                <div class="stat">
                    <div>Slime Points</div>
                    <div class="stat-value" id="slimePoints">0</div>
                </div>
                <div class="stat">
                    <div>Per Click</div>
                    <div class="stat-value" id="clickPower">1</div>
                </div>
                <div class="stat">
                    <div>Per Second</div>
                    <div class="stat-value" id="slimePerSecond">0</div>
                </div>
                <div class="stat">
                    <div>Prestige Level</div>
                    <div class="stat-value" id="prestigeLevel">0</div>
                </div>
            </div>

            <div class="mushroom-snail" id="mushroomSnail">
                <div>
                    <div class="mushroom-cap">
                        <div class="mushroom-spots spot1"></div>
                        <div class="mushroom-spots spot2"></div>
                        <div class="mushroom-spots spot3"></div>
                    </div>
                    <div class="snail-eyes">
                        <div class="eye">
                            <div class="pupil"></div>
                        </div>
                        <div class="eye">
                            <div class="pupil"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="sidebar">
            <div class="upgrade-section">
                <h3>🏪 Slime Producers</h3>
                <div id="producers">
                    <button class="upgrade" onclick="buyProducer('slugs')">
                        <div class="upgrade-name">Baby Slugs</div>
                        <div class="upgrade-cost">Cost: 15 slime</div>
                        <div class="upgrade-effect">+0.1/sec | Owned: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyProducer('snails')">
                        <div class="upgrade-name">Garden Snails</div>
                        <div class="upgrade-cost">Cost: 100 slime</div>
                        <div class="upgrade-effect">+1/sec | Owned: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyProducer('mushroomSnails')">
                        <div class="upgrade-name">Mushroom Snails</div>
                        <div class="upgrade-cost">Cost: 1.1K slime</div>
                        <div class="upgrade-effect">+8/sec | Owned: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyProducer('glowSnails')">
                        <div class="upgrade-name">Glow Snails</div>
                        <div class="upgrade-cost">Cost: 12K slime</div>
                        <div class="upgrade-effect">+47/sec | Owned: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyProducer('kingSnails')">
                        <div class="upgrade-name">King Snails</div>
                        <div class="upgrade-cost">Cost: 130K slime</div>
                        <div class="upgrade-effect">+260/sec | Owned: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyProducer('ancientSnails')">
                        <div class="upgrade-name">Ancient Snails</div>
                        <div class="upgrade-cost">Cost: 1.4M slime</div>
                        <div class="upgrade-effect">+1.4K/sec | Owned: 0</div>
                    </button>
                </div>
            </div>

            <div class="upgrade-section">
                <h3>⚡ Click Upgrades</h3>
                <div id="clickUpgrades">
                    <button class="upgrade" onclick="buyClickUpgrade('betterSlime')">
                        <div class="upgrade-name">Better Slime</div>
                        <div class="upgrade-cost">Cost: 100 slime</div>
                        <div class="upgrade-effect">+2 click power | Level: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyClickUpgrade('magicMushroom')">
                        <div class="upgrade-name">Magic Mushroom</div>
                        <div class="upgrade-cost">Cost: 1K slime</div>
                        <div class="upgrade-effect">+5 click power | Level: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyClickUpgrade('slimeBooster')">
                        <div class="upgrade-name">Slime Booster</div>
                        <div class="upgrade-cost">Cost: 10K slime</div>
                        <div class="upgrade-effect">+10 click power | Level: 0</div>
                    </button>
                    <button class="upgrade" onclick="buyClickUpgrade('goldenTouch')">
                        <div class="upgrade-name">Golden Touch</div>
                        <div class="upgrade-cost">Cost: 100K slime</div>
                        <div class="upgrade-effect">+25 click power | Level: 0</div>
                    </button>
                </div>
            </div>

            <div class="prestige-section">
                <h3>✨ Prestige</h3>
                <p>Reset progress for permanent bonuses!</p>
                <p>Next prestige gives: <span id="prestigeGain">0</span> Golden Slime</p>
                <p>Golden Slime: <span id="goldenSlime">0</span> (+<span id="prestigeBonus">0</span>% all production)</p>
                <button class="prestige-btn" id="prestigeBtn" onclick="prestige()" disabled>Prestige (Need 1M slime)</button>
            </div>

            <div class="achievements">
                <h3>🏆 Achievements</h3>
                <div id="achievementsList">
                    <div class="achievement">
                        <strong>First Click!</strong><br>
                        Click the mushroom snail
                    </div>
                    <div class="achievement">
                        <strong>Click Master</strong><br>
                        Click 1000 times
                    </div>
                    <div class="achievement">
                        <strong>Slime Collector</strong><br>
                        Collect 10,000 slime
                    </div>
                    <div class="achievement">
                        <strong>Producer</strong><br>
                        Buy your first producer
                    </div>
                    <div class="achievement">
                        <strong>Slime Factory</strong><br>
                        Own 100 total producers
                    </div>
                    <div class="achievement">
                        <strong>Millionaire</strong><br>
                        Have 1 million slime
                    </div>
                    <div class="achievement">
                        <strong>Prestige!</strong><br>
                        Perform your first prestige
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Game state
        let gameState = {
            slimePoints: 0,
            clickPower: 1,
            goldenSlime: 0,
            prestigeLevel: 0,
            producers: {
                slugs: 0,
                snails: 0,
                mushroomSnails: 0,
                glowSnails: 0,
                kingSnails: 0,
                ancientSnails: 0
            },
            clickUpgrades: {
                betterSlime: 0,
                magicMushroom: 0,
                slimeBooster: 0,
                goldenTouch: 0
            },
            achievements: {
                firstClick: false,
                clickMaster: false,
                slimeCollector: false,
                producer: false,
                factory: false,
                millionaire: false,
                firstPrestige: false
            },
            totalClicks: 0,
            totalSlimeEarned: 0
        };

        // Producer definitions
        const producers = {
            slugs: { name: "Baby Slugs", baseCost: 15, baseProduction: 0.1, multiplier: 1.07 },
            snails: { name: "Garden Snails", baseCost: 100, baseProduction: 1, multiplier: 1.07 },
            mushroomSnails: { name: "Mushroom Snails", baseCost: 1100, baseProduction: 8, multiplier: 1.07 },
            glowSnails: { name: "Glow Snails", baseCost: 12000, baseProduction: 47, multiplier: 1.07 },
            kingSnails: { name: "King Snails", baseCost: 130000, baseProduction: 260, multiplier: 1.07 },
            ancientSnails: { name: "Ancient Snails", baseCost: 1400000, baseProduction: 1400, multiplier: 1.07 }
        };

        // Click upgrade definitions
        const clickUpgrades = {
            betterSlime: { name: "Better Slime", baseCost: 100, effect: 2, maxLevel: 50 },
            magicMushroom: { name: "Magic Mushroom", baseCost: 1000, effect: 5, maxLevel: 25 },
            slimeBooster: { name: "Slime Booster", baseCost: 10000, effect: 10, maxLevel: 20 },
            goldenTouch: { name: "Golden Touch", baseCost: 100000, effect: 25, maxLevel: 15 }
        };

        // Click handler
        function clickSnail(event) {
            let clickValue = gameState.clickPower * (1 + gameState.goldenSlime * 0.1);
            gameState.slimePoints += clickValue;
            gameState.totalSlimeEarned += clickValue;
            gameState.totalClicks++;

            // Create click effect
            const clickEffect = document.createElement('div');
            clickEffect.className = 'click-effect';
            clickEffect.textContent = '+' + Math.floor(clickValue);
            clickEffect.style.left = (event.offsetX || 100) + 'px';
            clickEffect.style.top = (event.offsetY || 100) + 'px';
            event.currentTarget.appendChild(clickEffect);

            // Create particles
            for (let i = 0; i < 5; i++) {
                createParticle(event.offsetX || 100, event.offsetY || 100, event.currentTarget);
            }

            setTimeout(() => clickEffect.remove(), 1000);
            
            updateDisplay();
            updateAchievements();
        }

        function createParticle(x, y, container) {
            const particle = document.createElement('div');
            particle.className = 'particle';
            particle.style.left = x + (Math.random() - 0.5) * 50 + 'px';
            particle.style.top = y + (Math.random() - 0.5) * 50 + 'px';
            container.appendChild(particle);
            setTimeout(() => particle.remove(), 2000);
        }

        // Calculate slime per second
        function calculateSlimePerSecond() {
            let total = 0;
            for (let key in producers) {
                let producer = producers[key];
                let owned = gameState.producers[key] || 0;
                total += producer.baseProduction * owned;
            }
            return total * (1 + gameState.goldenSlime * 0.1);
        }

        // Update display
        function updateDisplay() {
            document.getElementById('slimePoints').textContent = formatNumber(Math.floor(gameState.slimePoints));
            document.getElementById('clickPower').textContent = formatNumber(gameState.clickPower * (1 + gameState.goldenSlime * 0.1));
            document.getElementById('slimePerSecond').textContent = formatNumber(calculateSlimePerSecond());
            document.getElementById('prestigeLevel').textContent = gameState.prestigeLevel;
            document.getElementById('goldenSlime').textContent = gameState.goldenSlime;
            document.getElementById('prestigeBonus').textContent = (gameState.goldenSlime * 10).toFixed(1);
            
            // Update prestige button
            const prestigeBtn = document.getElementById('prestigeBtn');
            const prestigeGain = Math.floor(Math.sqrt(gameState.totalSlimeEarned) / 1000);
            document.getElementById('prestigeGain').textContent = prestigeGain;
            
            if (gameState.slimePoints >= 1000000) {
                prestigeBtn.disabled = false;
                prestigeBtn.textContent = `Prestige (+${prestigeGain} Golden Slime)`;
            } else {
                prestigeBtn.disabled = true;
                prestigeBtn.textContent = 'Prestige (Need 1M slime)';
            }

            updateUpgradeButtons();
        }

        // Format numbers
        function formatNumber(num) {
            if (num < 1000) return Math.floor(num).toString();
            if (num < 1000000) return (num / 1000).toFixed(1) + 'K';
            if (num < 1000000000) return (num / 1000000).toFixed(1) + 'M';
            if (num < 1000000000000) return (num / 1000000000).toFixed(1) + 'B';
            return (num / 1000000000000).toFixed(1) + 'T';
        }

        // Update upgrade buttons
        function updateUpgradeButtons() {
            // Update producer buttons
            const producerButtons = document.querySelectorAll('#producers .upgrade');
            const producerKeys = Object.keys(producers);
            
            producerButtons.forEach((button, index) => {
                const key = producerKeys[index];
                if (key && producers[key]) {
                    const producer = producers[key];
                    const cost = Math.floor(producer.baseCost * Math.pow(producer.multiplier, gameState.producers[key]));
                    const owned = gameState.producers[key];
                    
                    button.innerHTML = `
                        <div class="upgrade-name">${producer.name}</div>
                        <div class="upgrade-cost">Cost: ${formatNumber(cost)} slime</div>
                        <div class="upgrade-effect">+${formatNumber(producer.baseProduction)}/sec | Owned: ${owned}</div>
                    `;
                    
                    button.disabled = gameState.slimePoints < cost;
                }
            });

            // Update click upgrade buttons
            const clickButtons = document.querySelectorAll('#clickUpgrades .upgrade');
            const upgradeKeys = Object.keys(clickUpgrades);
            
            clickButtons.forEach((button, index) => {
                const key = upgradeKeys[index];
                if (key && clickUpgrades[key]) {
                    const upgrade = clickUpgrades[key];
                    const level = gameState.clickUpgrades[key];
                    const cost = Math.floor(upgrade.baseCost * Math.pow(2, level));
                    
                    if (level >= upgrade.maxLevel) {
                        button.innerHTML = `
                            <div class="upgrade-name">${upgrade.name}</div>
                            <div class="upgrade-effect">MAX LEVEL</div>
                        `;
                        button.disabled = true;
                    } else {
                        button.innerHTML = `
                            <div class="upgrade-name">${upgrade.name}</div>
                            <div class="upgrade-cost">Cost: ${formatNumber(cost)} slime</div>
                            <div class="upgrade-effect">+${upgrade.effect} click power | Level: ${level}</div>
                        `;
                        button.disabled = gameState.slimePoints < cost;
                    }
                }
            });
        }

        // Buy producer
        function buyProducer(key) {
            const producer = producers[key];
            if (!producer) return;
            
            const cost = Math.floor(producer.baseCost * Math.pow(producer.multiplier, gameState.producers[key]));
            
            if (gameState.slimePoints >= cost) {
                gameState.slimePoints -= cost;
                gameState.producers[key]++;
                updateDisplay();
            }
        }

        // Buy click upgrade
        function buyClickUpgrade(key) {
            const upgrade = clickUpgrades[key];
            if (!upgrade) return;
            
            const level = gameState.clickUpgrades[key];
            const cost = Math.floor(upgrade.baseCost * Math.pow(2, level));
            
            if (gameState.slimePoints >= cost && level < upgrade.maxLevel) {
                gameState.slimePoints -= cost;
                gameState.clickUpgrades[key]++;
                gameState.clickPower += upgrade.effect;
                updateDisplay();
            }
        }

        // Prestige
        function prestige() {
            if (gameState.slimePoints >= 1000000) {
                const prestigeGain = Math.floor(Math.sqrt(gameState.totalSlimeEarned) / 1000);
                
                // Reset game state but keep prestige bonuses
                gameState.slimePoints = 0;
                gameState.clickPower = 1;
                gameState.totalSlimeEarned = 0;
                gameState.goldenSlime += prestigeGain;
                gameState.prestigeLevel++;
                
                // Reset producers and upgrades
                for (let key in gameState.producers) {
                    gameState.producers[key] = 0;
                }
                for (let key in gameState.clickUpgrades) {
                    gameState.clickUpgrades[key] = 0;
                }
                
                updateDisplay();
            }
        }

        // Update achievements
        function updateAchievements() {
            const achievements = [
                { id: "firstClick", condition: () => gameState.totalClicks >= 1 },
                { id: "clickMaster", condition: () => gameState.totalClicks >= 1000 },
                { id: "slimeCollector", condition: () => gameState.totalSlimeEarned >= 10000 },
                { id: "producer", condition: () => Object.values(gameState.producers).some(p => p > 0) },
                { id: "factory", condition: () => Object.values(gameState.producers).reduce((a, b) => a + b, 0) >= 100 },
                { id: "millionaire", condition: () => gameState.slimePoints >= 1000000 },
                { id: "firstPrestige", condition: () => gameState.prestigeLevel >= 1 }
            ];

            const achievementElements = document.querySelectorAll('#achievementsList .achievement');
            
            achievements.forEach((achievement, index) => {
                if (!gameState.achievements[achievement.id] && achievement.condition()) {
                    gameState.achievements[achievement.id] = true;
                    if (achievementElements[index]) {
                        achievementElements[index].classList.add('unlocked');
                    }
                }
                
                if (gameState.achievements[achievement.id] && achievementElements[index]) {
                    achievementElements[index].classList.add('unlocked');
                }
            });
        }

        // Game loop
        function gameLoop() {
            let slimePerSecond = calculateSlimePerSecond();
            gameState.slimePoints += slimePerSecond / 10; // Divide by 10 because loop runs 10 times per second
            gameState.totalSlimeEarned += slimePerSecond / 10;
            
            updateDisplay();
            updateAchievements();
        }

        // Initialize game
        function initGame() {
            updateDisplay();
            updateAchievements();
            
            // Add click event listener
            document.getElementById('mushroomSnail').addEventListener('click', clickSnail);
            
            // Start game loop
            setInterval(gameLoop, 100);
        }

        // Start the game when page loads
        window.addEventListener('load', initGame);
    </script>
</body>
</html>
