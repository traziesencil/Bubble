<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>XIV. It's still you</title>
    <style>
        :root {
            --bg-color: #0c0c0e;
            --card-bg: rgba(255, 255, 255, 0.03);
            --card-border: rgba(255, 255, 255, 0.08);
            --text-main: #ffffff;
            --text-muted: #a1a1aa;
            --accent: #e5c158; 
            --error: #ff453a;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
            padding: 20px;
        }

        /* --- LOCK SCREEN INTERFACE --- */
        #lock-screen {
            display: flex;
            flex-direction: column;
            align-items: center;
            max-width: 360px;
            width: 100%;
            text-align: center;
            transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .lock-icon {
            font-size: 28px;
            margin-bottom: 20px;
            color: var(--accent);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 0.6; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.05); }
            100% { opacity: 0.6; transform: scale(1); }
        }

        .title-preview {
            font-size: 1.8rem;
            font-weight: 600;
            letter-spacing: -0.5px;
            margin-bottom: 8px;
        }

        .subtitle-preview {
            font-size: 0.9rem;
            color: var(--text-muted);
            margin-bottom: 35px;
        }

        .pin-dots {
            display: flex;
            gap: 18px;
            margin-bottom: 40px;
        }

        .dot {
            width: 14px;
            height: 14px;
            border: 2px solid var(--text-muted);
            border-radius: 50%;
            transition: all 0.2s ease;
        }

        .dot.active {
            background-color: var(--accent);
            border-color: var(--accent);
            box-shadow: 0 0 10px var(--accent);
            transform: scale(1.1);
        }

        .dot.error {
            background-color: var(--error);
            border-color: var(--error);
            box-shadow: 0 0 10px var(--error);
        }

        .keypad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            width: 100%;
        }

        .key {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            color: var(--text-main);
            font-size: 1.6rem;
            font-weight: 400;
            height: 75px;
            width: 75px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            justify-self: center;
            user-select: none;
            transition: all 0.1s ease;
        }

        .key:active {
            background: rgba(229, 193, 88, 0.2);
            border-color: var(--accent);
            transform: scale(0.92);
        }

        .key.utility {
            font-size: 0.95rem;
            background: transparent;
            border-color: transparent;
            color: var(--text-muted);
        }

        /* --- LETTER CONTENT INTERFACE --- */
        #letter-screen {
            display: none;
            max-width: 600px;
            width: 100%;
            background: rgba(20, 20, 25, 0.7);
            border: 1px solid var(--card-border);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            padding: 45px 30px;
            border-radius: 28px;
            box-shadow: 0 30px 60px rgba(0,0,0,0.6);
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .letter-header {
            border-bottom: 1px solid var(--card-border);
            padding-bottom: 25px;
            margin-bottom: 35px;
            text-align: center;
        }

        .letter-title {
            font-size: 2.4rem;
            font-weight: 700;
            margin-bottom: 10px;
            letter-spacing: -0.5px;
        }

        .letter-timeframe {
            font-size: 0.95rem;
            color: var(--accent);
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 600;
        }

        .letter-body {
            font-size: 1.1rem;
            line-height: 1.85;
            color: rgba(255, 255, 255, 0.9);
        }

        .letter-body p {
            margin-bottom: 24px;
        }

        .letter-body p em {
            color: var(--accent);
            font-style: italic;
            font-weight: 500;
        }

        /* --- GALLERY --- */
        .photo-gallery {
            margin-top: 40px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .photo-card {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid var(--card-border);
            border-radius: 16px;
            padding: 12px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }

        .photo-img {
            width: 100%;
            height: auto;
            border-radius: 10px;
            display: block;
            object-fit: cover;
        }

        .photo-caption {
            font-size: 0.85rem;
            color: var(--text-muted);
            text-align: center;
            margin-top: 10px;
            font-style: italic;
        }

        .shake { animation: shake 0.4s ease-in-out; }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-10px); }
            40%, 80% { transform: translateX(10px); }
        }
        .fade-out { opacity: 0; transform: scale(0.95); pointer-events: none; }
    </style>
</head>
<body>

    <div id="lock-screen">
        <div class="lock-icon">🔒</div>
        <div class="title-preview">XIV. It's still you.</div>
        <div class="subtitle-preview">Enter our secret 4-digit PIN</div>

        <div class="pin-dots" id="pin-dots">
            <div class="dot"></div>
            <div class="dot"></div>
            <div class="dot"></div>
            <div class="dot"></div>
        </div>

        <div class="keypad">
            <div class="key" onclick="pressNum('1')">1</div>
            <div class="key" onclick="pressNum('2')">2</div>
            <div class="key" onclick="pressNum('3')">3</div>
            <div class="key" onclick="pressNum('4')">4</div>
            <div class="key" onclick="pressNum('5')">5</div>
            <div class="key" onclick="pressNum('6')">6</div>
            <div class="key" onclick="pressNum('7')">7</div>
            <div class="key" onclick="pressNum('8')">8</div>
            <div class="key" onclick="pressNum('9')">9</div>
            <div class="key utility" onclick="clearPin()">Clear</div>
            <div class="key" onclick="pressNum('0')">0</div>
            <div class="key utility" onclick="backspace()">⌫</div>
        </div>
    </div>

    <div id="letter-screen">
        <div class="letter-header">
            <div class="letter-title">XIV. It's still you.</div>
            <div class="letter-timeframe">14 years &bull; 5,113 days</div>
        </div>
        
        <div class="letter-body">
            <p>And through it all, it is still always you.</p>
            
            <p>Sin-o man abi maka isip, 'di bala? It all started from a simple game—from you being curious about what was behind the name "Tracy." But guess what? We made it this far.</p>
            
            <p>For more than a decade, damo ta na pang-agyan nga problems that challenged us and pushed us apart. But despite everything, we proved that <em>"iiyak, pero di susuko ang mga fersons."</em></p>
            
            <p>As we celebrate another season of away-bati, I love looking back at our relapse moments—manghagad ma-one bot to a place somewhere only we know, talking about the life and dreams we continue to fight for.</p>
            
            <p>As we take one step closer to our XV year, basi paman lang ma fulfill na naton ang dream that we always had.</p>
            
            <div class="photo-gallery">
                <div class="photo-card"><img class="photo-img" src="FB_IMG_1775360529420.jpg"><div class="photo-caption">Our beautiful moments together</div></div>
                <div class="photo-card"><img class="photo-img" src="IMG_20260315_134408_8.jpg"><div class="photo-caption">Through every journey and adventure</div></div>
                <div class="photo-card"><img class="photo-img" src="IMG_20260315_213019.jpg"><div class="photo-caption">Blessed with the life we continue to build</div></div>
                <div class="photo-card"><img class="photo-img" src="IMG_20260124_081613 (1).jpg"><div class="photo-caption">Side by side, hand in hand</div></div>
                <div class="photo-card"><img class="photo-img" src="IMG_20250724_153532.jpg"><div class="photo-caption">Making every milestone count</div></div>
                <div class="photo-card"><img class="photo-img" src="1704777670597.jpg"><div class="photo-caption">Always and forever, it's still you</div></div>
            </div>

            <p style="margin-top: 50px; text-align: center; font-weight: 600; color: var(--accent); font-size: 1.2rem;">
                Thank you for staying. Happy 14th Anniversary! ❤️
            </p>
        </div>
    </div>

    <script>
        // Set to your requested lock pin 
        const CORRECT_PIN = "0724"; 
        
        let currentInput = "";
        const dots = document.querySelectorAll('.dot');
        const lockScreen = document.getElementById('lock-screen');
        const letterScreen = document.getElementById('letter-screen');

        function updateDots() {
            dots.forEach((dot, index) => {
                if (index < currentInput.length) { dot.classList.add('active'); } 
                else { dot.classList.remove('active'); }
            });
        }

        function pressNum(num) {
            if (currentInput.length < 4) {
                currentInput += num;
                updateDots();
                if (currentInput.length === 4) { setTimeout(checkPin, 250); }
            }
        }

        function clearPin() { currentInput = ""; updateDots(); }
        function backspace() { currentInput = currentInput.slice(0, -1); updateDots(); }

        function checkPin() {
            if (currentInput === CORRECT_PIN) {
                lockScreen.classList.add
