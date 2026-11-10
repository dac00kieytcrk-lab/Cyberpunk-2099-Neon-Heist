[index.html](https://github.com/user-attachments/files/34625183/index.html)
# Cyberpunk-2099-Neon-Heist<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cyberpunk 2099: The Neon Heist</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      background-color: #05050a;
      color: #00ffcc;
      font-family: 'Courier New', Courier, monospace;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 15px;
    }
    #game-container {
      background: #0d0e15;
      border: 2px solid #ff007f;
      border-radius: 8px;
      max-width: 800px;
      width: 100%;
      padding: 25px;
      box-shadow: 0 0 30px rgba(255, 0, 127, 0.4), inset 0 0 15px rgba(0, 255, 204, 0.1);
      text-align: center;
    }
    h1 {
      color: #ff007f;
      margin-bottom: 4px;
      font-size: 1.8rem;
      letter-spacing: 2px;
      text-shadow: 0 0 10px #ff007f;
    }
    .subtitle {
      color: #00ffcc;
      font-size: 0.9rem;
      margin-bottom: 12px;
      letter-spacing: 1px;
    }
    .meta-bar {
      display: flex;
      justify-content: space-between;
      color: #ff007f;
      font-size: 0.85rem;
      margin-bottom: 12px;
      border-bottom: 1px solid #ff007f;
      padding-bottom: 6px;
    }
    .ascii-frame {
      margin: 15px 0;
      border: 1px solid #00ffcc;
      border-radius: 6px;
      background: #030307;
      padding: 15px;
      white-space: pre;
      color: #00ffcc;
      font-size: 0.8rem;
      line-height: 1.2;
      box-shadow: inset 0 0 10px rgba(0, 255, 204, 0.2);
    }
    #story-text {
      font-size: 1.0rem;
      line-height: 1.6;
      margin: 15px 0;
      min-height: 130px;
      max-height: 220px;
      overflow-y: auto;
      text-align: left;
      background: #080910;
      padding: 15px;
      border-radius: 4px;
      border-left: 4px solid #ff007f;
      white-space: pre-wrap;
    }
    .options-grid {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    button {
      background: #121420;
      color: #00ffcc;
      border: 1px solid #00ffcc;
      padding: 12px 16px;
      border-radius: 4px;
      font-family: 'Courier New', Courier, monospace;
      font-size: 0.95rem;
      cursor: pointer;
      transition: all 0.2s ease;
      text-align: left;
    }
    button:hover {
      background: #ff007f;
      color: #ffffff;
      border-color: #ff007f;
      box-shadow: 0 0 15px rgba(255, 0, 127, 0.8);
      transform: translateY(-2px);
    }
  </style>
</head>
<body>
  <div id="game-container">
    <h1>CYBERPUNK 2099</h1>
    <div class="subtitle">NEO-SHINJUKU HEIST ARCHIVES</div>

    <div class="meta-bar">
      <span id="chapter-title">LOCATION: SKYLINE SKYBRIDGE</span>
      <span id="stat-tracker">HEAT: 10% | CYBERWARE: 100% | CREDITS: 0</span>
    </div>
    
    <div class="ascii-frame" id="ascii-art">
     .----------------------------------.
    |      [ NEO-SHINJUKU SECTOR 9 ]    |
    |     |  | | |   | | |  |           |
    |    [=][=][=]   [=][=][=]          |
    |    |  | | |     | | |  |          |
    |   ~~~~~~~~~~~~~|~~~~~~~~~         |
     '----------------------------------'
    </div>

    <div id="story-text">Connecting neural link...</div>

    <div id="options" class="options-grid"></div>
  </div>

  <script>
    let state = { heat: 10, cyberware: 100, credits: 0 };

    const asciiCity = ` .----------------------------------.
|      [ NEO-SHINJUKU SECTOR 9 ]    |
|     |  | | |   | | |  |           |
|    [=][=][=]   [=][=][=]          |
|    |  | | |     | | |  |          |
|   ~~~~~~~~~~~~~|~~~~~~~~~         |
 '----------------------------------'`;

    const asciiHacker = ` .----------------------------------.
|        [ CYBER-NETRUNNER ]        |
|          _.-''''-._               |
|        .'  _     _  '.            |
|       /   (o)   (o)   \\           |
|      |     .-'-.     |            |
|       \\   '====='   /             |
 '----------------------------------'`;

    const asciiChip = ` .----------------------------------.
|        [ QUANTUM AI CHIP ]        |
|          .-------.                |
|         | [===]  |                |
|         |  0101  |                |
|          '-------'                |
|        VALUED AT 50M CREDITS      |
 '----------------------------------'`;

    const story = {
      start: {
        chapter: "ACT I: SKYLINE SKYBRIDGE",
        art: asciiCity,
        text: "Acid rain slicks the dark glass of the Arasaka-Kuro high-rise skybridge. Holographic dragons sweep through the neon fog above as automated laser turrets scan the atmospheric boundary.\n\nTarget: The 80th-floor vault. Objective: Extract the 50 Million Credit Quantum AI Chip.",
        choices: [
          { text: "[1] Cyberdeck Breach: Inject a daemon virus into the laser guard grid.", target: "act1_hack", hMod: 10, cMod: -15 },
          { text: "[2] Monowire Zip: Sling across the high-voltage sky-cable into the ventilation chute.", target: "act1_wire", hMod: 20, cMod: -10 },
          { text: "[3] Thermal Camouflage: Overclock sub-dermal optics and slip right past perimeter sensors.", target: "act1_cloak", hMod: 0, cMod: -25 }
        ]
      },

      act1_hack: {
        chapter: "ACT II: LAZARUS SECURITY STRIKES",
        art: asciiHacker,
        text: "The daemon virus executes! Turrets glitch out in turquoise sparks. You breach the vault doors just as red warning strobe lights illuminate the high-rise!\n\nA Lazarus Heavy Battle-Drone drops from the ceiling hatch, charging blue plasma in its heavy twin cannons!",
        choices: [
          { text: "[1] EMP Shockwave: Detonate an EMP grenade to short-circuit the drone core.", target: "act2_win", hMod: 15, cMod: 0 },
          { text: "[2] Sub-Dermal Reflexes: Trigger slow-mo adrenaline to dodge the plasma blasts!", target: "act2_win", hMod: 25, cMod: -20 },
          { text: "[3] Overdrive Hack: Take direct control of the drone's targeting computer!", target: "act2_win", hMod: 10, cMod: -30 }
        ]
      },

      act1_wire: {
        chapter: "ACT II: LAZARUS SECURITY STRIKES",
        art: asciiHacker,
        text: "You slice through the vent grill with glowing monowire, landing inside the vault room. Alarm horns blare across the high-rise district!\n\nA Lazarus Heavy Battle-Drone drops from the ceiling hatch, charging blue plasma in its heavy twin cannons!",
        choices: [
          { text: "[1] EMP Shockwave: Detonate an EMP grenade to short-circuit the drone core.", target: "act2_win", hMod: 15, cMod: 0 },
          { text: "[2] Sub-Dermal Reflexes: Trigger slow-mo adrenaline to dodge the plasma blasts!", target: "act2_win", hMod: 25, cMod: -20 },
          { text: "[3] Overdrive Hack: Take direct control of the drone's targeting computer!", target: "act2_win", hMod: 10, cMod: -30 }
        ]
      },

      act1_cloak: {
        chapter: "ACT II: LAZARUS SECURITY STRIKES",
        art: asciiHacker,
        text: "Invisible under thermal cloak, you ghost right past security doors. You extract the glowing Quantum AI Chip, but the sudden weight change triggers floor sensors!\n\nA Lazarus Heavy Battle-Drone drops from the ceiling hatch, charging blue plasma in its heavy twin cannons!",
        choices: [
          { text: "[1] EMP Shockwave: Detonate an EMP grenade to short-circuit the drone core.", target: "act2_win", hMod: 15, cMod: 0 },
          { text: "[2] Sub-Dermal Reflexes: Trigger slow-mo adrenaline to dodge the plasma blasts!", target: "act2_win", hMod: 25, cMod: -20 },
          { text: "[3] Overdrive Hack: Take direct control of the drone's targeting computer!", target: "act2_win", hMod: 10, cMod: -30 }
        ]
      },

      act2_win: {
        chapter: "ACT III: THE LEAP OF FAITH",
        art: asciiChip,
        text: "The battle drone sparks violently and crashes through the reinforced glass barrier, shattering it into thousands of neon-lit glass shards! High-altitude wind howls into the vault.\n\nCorporate strike teams are breaching the reinforced main doors with plasma torches. Elevators are locked down. How do you escape Sector 9?",
        choices: [
          { text: "[1] AV-4 Jump: Leap out the 80th-floor window onto your getaway team's flying vehicle!", target: "ending_av", hMod: 20, crMod: 50000000 },
          { text: "[2] Base Jump Parachute: Dive directly into the lower neon fog layers of the megacity.", target: "ending_chute", hMod: 0, crMod: 50000000 },
          { text: "[3] Cable Hack: Sever the main elevator cables with monowire and ride the car down!", target: "ending_cable", hMod: 35, crMod: 50000000 }
        ]
      },

      ending_av: {
        chapter: "EPILOGUE: SKYLINE LEGEND",
        art: asciiHacker,
        text: "You dive into open air as explosions erupt behind you! The AV-4 catches you mid-fall, swooping through neon billboard canyons. Safe in your subterranean netrunner den, 50,000,000 credits hit your encrypted wallet.\n\nHEIST SUCCESSFUL! YOU OWN THE NEON NIGHT!",
        choices: [{ text: "Reboot Cyberdeck (Play Again)", target: "start" }]
      },

      ending_chute: {
        chapter: "EPILOGUE: GHOST IN THE FOG",
        art: asciiCity,
        text: "You deploy your holo-chute, vanishing into the glowing purple smog of the low-level slums. Corporate radar loses your signature completely. 50,000,000 credits secured.\n\nHEIST SUCCESSFUL! A PERFECT GHOST RUN!",
        choices: [{ text: "Reboot Cyberdeck (Play Again)", target: "start" }]
      },

      ending_cable: {
        chapter: "EPILOGUE: HIGH-VOLTAGE SURVIVOR",
        art: asciiChip,
        text: "You ride the plummeting elevator car down 80 floors, hitting reverse thrusters at the last second! You burst out into the crowded street bazaar with the Quantum Chip in hand.\n\nHEIST SUCCESSFUL! MAXIMUM CHAOS AND VICTORY!",
        choices: [{ text: "Reboot Cyberdeck (Play Again)", target: "start" }]
      }
    };

    function renderScene(sceneKey) {
      const scene = story[sceneKey];
      if (!scene) return;

      document.getElementById('chapter-title').innerText = scene.chapter;
      document.getElementById('stat-tracker').innerText = `HEAT: ${state.heat}% | CYBERWARE: ${state.cyberware}% | CREDITS: ₡${state.credits.toLocaleString()}`;
      document.getElementById('ascii-art').innerText = scene.art;
      document.getElementById('story-text').innerText = scene.text;
      
      const optionsContainer = document.getElementById('options');
      optionsContainer.innerHTML = '';
      
      scene.choices.forEach(choice => {
        const btn = document.createElement('button');
        btn.innerText = choice.text;
        btn.onclick = () => {
          if (choice.hMod) state.heat = Math.max(0, Math.min(100, state.heat + choice.hMod));
          if (choice.cMod) state.cyberware = Math.max(0, Math.min(100, state.cyberware + choice.cMod));
          if (choice.crMod) state.credits += choice.crMod;
          renderScene(choice.target);
        };
        optionsContainer.appendChild(btn);
      });
    }

    renderScene('start');
  </script>
</body>
</html>
