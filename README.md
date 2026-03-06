<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="theme-color" content="#050505">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    
    <title>Maa Nirmala DJ | Premium Event App</title>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600;800;900&family=Orbitron:wght@400;700;900&family=Outfit:wght@300;400;600;800&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            /* MND Master Color Palette */
            --app-bg: #030305;
            --app-surface: #0a0a10;
            --gold-primary: #D4AF37;
            --gold-glow: #FFDF00;
            --cyan-neon: #00e5ff;
            --red-alert: #ff3333;
            
            /* Typography */
            --font-head: 'Cinzel', serif;
            --font-tech: 'Orbitron', sans-serif;
            --font-body: 'Outfit', sans-serif;
            --font-data: 'Rajdhani', sans-serif;

            /* App Dimensions */
            --nav-top-height: 60px;
            --nav-bot-height: 70px;
            
            /* Glassmorphism */
            --glass-bg: rgba(10, 10, 15, 0.7);
            --glass-border: rgba(255, 255, 255, 0.05);
        }

        /* Hard Reset for App Consistency */
        * {
            margin: 0; padding: 0; box-sizing: border-box;
            -webkit-tap-highlight-color: transparent; /* Removes blue tap flash on mobile */
            user-select: none; /* Prevents accidental text selection like a real app */
        }
        
        html, body {
            width: 100%;
            height: 100%;
            background-color: var(--app-bg);
            color: #ffffff;
            font-family: var(--font-body);
            overflow: hidden; /* We handle scrolling inside the main container */
            overscroll-behavior-y: none; /* Stops pull-to-refresh bounce */
        }

        /* Let users copy text only where we allow it */
        .allow-select { user-select: text; }

        /* ========================================= */
        /* THE APP SHELL (Top Nav, Main, Bottom Nav) */
        /* ========================================= */

        /* Top Navigation Bar */
        .app-top-bar {
            position: fixed;
            top: 0; left: 0; width: 100%; height: var(--nav-top-height);
            background: var(--glass-bg);
            backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--glass-border);
            display: flex; justify-content: space-between; align-items: center;
            padding: 0 20px;
            z-index: 1000;
        }

        .app-logo-area { display: flex; align-items: center; gap: 10px; }
        .app-logo-img { width: 35px; height: 35px; border-radius: 50%; border: 1px solid var(--gold-primary); box-shadow: 0 0 10px rgba(212,175,55,0.3); }
        .app-brand-name { font-family: var(--font-head); font-size: 16px; font-weight: 900; letter-spacing: 1px; color: #fff; }
        .app-brand-sub { font-family: var(--font-tech); font-size: 8px; color: var(--gold-primary); display: block; margin-top: -3px; }

        .app-top-actions i { font-size: 20px; color: #fff; margin-left: 15px; cursor: pointer; transition: 0.2s; }
        .app-top-actions i:active { color: var(--gold-primary); transform: scale(0.9); }

        /* Main Scrollable Content Area */
        .app-main-content {
            position: absolute;
            top: var(--nav-top-height);
            bottom: var(--nav-bot-height);
            left: 0; right: 0;
            overflow-y: auto;
            overflow-x: hidden;
            scroll-behavior: smooth;
            background: radial-gradient(circle at top right, #0a0a1a 0%, var(--app-bg) 100%);
            padding: 20px;
        }
        /* Hide scrollbar for a cleaner app look */
        .app-main-content::-webkit-scrollbar { display: none; }

        /* Bottom Tab Navigation */
        .app-bottom-bar {
            position: fixed;
            bottom: 0; left: 0; width: 100%; height: var(--nav-bot-height);
            background: var(--glass-bg);
            backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
            border-top: 1px solid var(--glass-border);
            display: flex; justify-content: space-around; align-items: center;
            padding: 0 10px;
            z-index: 1000;
            padding-bottom: env(safe-area-inset-bottom); /* Fix for iPhones with home indicator */
        }

        .tab-item {
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            width: 60px; height: 100%; cursor: pointer; color: #666; transition: 0.3s;
        }
        .tab-item i { font-size: 20px; margin-bottom: 4px; transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .tab-item span { font-family: var(--font-data); font-size: 10px; font-weight: bold; }
        
        /* Active Tab Styling */
        .tab-item.active { color: var(--gold-primary); }
        .tab-item.active i { transform: translateY(-3px) scale(1.2); text-shadow: 0 5px 15px rgba(212,175,55,0.5); }

        /* ========================================= */
        /* SYSTEM BOOT SCREEN (Prevents White Flashes)*/
        /* ========================================= */
        .sys-boot-screen {
            position: fixed; inset: 0; background: #000; z-index: 99999;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            transition: opacity 0.8s ease-out;
        }
        .boot-logo { width: 100px; height: 100px; border-radius: 50%; border: 2px solid var(--gold-primary); animation: pulseGlow 2s infinite alternate; }
        .boot-text { font-family: var(--font-tech); color: var(--cyan-neon); margin-top: 20px; font-size: 14px; letter-spacing: 5px; animation: blink 1s infinite; }
        .boot-progress { width: 200px; height: 2px; background: #222; margin-top: 20px; position: relative; overflow: hidden; }
        .boot-bar { position: absolute; top: 0; left: 0; height: 100%; background: var(--gold-primary); width: 0%; animation: loadBar 2s ease-in-out forwards; }

        @keyframes pulseGlow { 0% { box-shadow: 0 0 10px rgba(212,175,55,0.2); } 100% { box-shadow: 0 0 40px rgba(212,175,55,0.8); } }
        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
        @keyframes loadBar { 0% { width: 0%; } 100% { width: 100%; } }

    </style>
</head>
<body>

    <div class="sys-boot-screen" id="bootScreen">
        <img src="https://i.postimg.cc/76mz1v2j/file-0000000090a471fa84cbecd48a774885.png" alt="MND Logo" class="boot-logo">
        <div class="boot-text">INITIALIZING MND OS</div>
        <div class="boot-progress"><div class="boot-bar"></div></div>
    </div>

    <header class="app-top-bar">
        <div class="app-logo-area">
            <img src="https://i.postimg.cc/76mz1v2j/file-0000000090a471fa84cbecd48a774885.png" class="app-logo-img" alt="Logo">
            <div>
                <div class="app-brand-name">MND V3 PRO</div>
                <div class="app-brand-sub">BELTIKRI HQ ONLINE</div>
            </div>
        </div>
        <div class="app-top-actions">
            <i class="fas fa-bell"></i>
            <i class="fas fa-cog"></i>
        </div>
    </header>

    <main class="app-main-content" id="mainScroller">
        
        <div style="padding: 40px 10px; text-align: center; border: 1px dashed #333; border-radius: 12px; margin-top: 20px;">
            <i class="fas fa-check-circle" style="font-size: 40px; color: #00ff00; margin-bottom: 15px;"></i>
            <h2 style="font-family: var(--font-head); color: var(--gold-primary); margin-bottom: 10px;">APP CORE INSTALLED</h2>
            <p style="font-family: var(--font-body); color: #888; font-size: 14px;">The progressive web app skeleton is running perfectly. No scrolling issues. No white screens.</p>
        </div>
        <style>
            /* Deep App Buttons */
            .app-btn-primary {
                background: linear-gradient(135deg, var(--gold-primary), var(--gold-glow));
                color: #000;
                border: none;
                border-radius: 8px;
                padding: 15px 24px;
                font-family: var(--font-tech);
                font-weight: 900;
                font-size: 14px;
                letter-spacing: 1px;
                display: flex;
                align-items: center;
                justify-content: center;
                gap: 10px;
                width: 100%;
                box-shadow: 0 10px 20px rgba(212,175,55,0.4), inset 0 2px 5px rgba(255,255,255,0.5);
                cursor: pointer;
                transition: transform 0.1s, box-shadow 0.1s;
            }
            .app-btn-primary:active {
                transform: scale(0.96);
                box-shadow: 0 5px 10px rgba(212,175,55,0.4), inset 0 2px 5px rgba(0,0,0,0.2);
            }

            .app-btn-outline {
                background: rgba(0,0,0,0.5);
                color: var(--cyan-neon);
                border: 1px solid var(--cyan-neon);
                border-radius: 8px;
                padding: 12px 20px;
                font-family: var(--font-data);
                font-weight: bold;
                font-size: 13px;
                text-transform: uppercase;
                display: flex;
                align-items: center;
                justify-content: center;
                gap: 8px;
                cursor: pointer;
                transition: 0.2s;
                box-shadow: inset 0 0 10px rgba(0,229,255,0.1);
            }
            .app-btn-outline:active { background: var(--cyan-neon); color: #000; }

            /* Global Toast Notification System */
            #appToast {
                visibility: hidden;
                min-width: 250px;
                background-color: rgba(20, 20, 25, 0.95);
                color: #fff;
                text-align: center;
                border-radius: 30px;
                padding: 15px 20px;
                position: fixed;
                z-index: 999999;
                left: 50%;
                transform: translateX(-50%);
                bottom: 90px; /* Above bottom nav */
                font-family: var(--font-body);
                font-size: 12px;
                border: 1px solid var(--gold-primary);
                box-shadow: 0 10px 30px rgba(0,0,0,0.8), 0 0 15px rgba(212,175,55,0.3);
                opacity: 0;
                transition: opacity 0.3s, bottom 0.3s;
            }
            #appToast.show { visibility: visible; opacity: 1; bottom: 100px; }
            #appToast i { color: var(--gold-primary); margin-right: 8px; font-size: 14px; }

            /* App Section Containers */
            .app-section {
                background: var(--app-surface);
                border: 1px solid var(--glass-border);
                border-radius: 16px;
                padding: 20px;
                margin-top: 20px;
                box-shadow: 0 15px 35px rgba(0,0,0,0.5);
                position: relative;
                overflow: hidden;
            }
            .section-header {
                display: flex; justify-content: space-between; align-items: center;
                margin-bottom: 20px; border-bottom: 1px solid rgba(255,255,255,0.05); padding-bottom: 10px;
            }
            .section-title { font-family: var(--font-head); font-size: 16px; color: var(--gold-primary); margin: 0; }
            .section-icon { background: rgba(212,175,55,0.1); width: 30px; height: 30px; border-radius: 8px; display: flex; justify-content: center; align-items: center; color: var(--gold-primary); }
        </style>

        <style>
            .hero-card {
                background: linear-gradient(145deg, #111520, #05050a);
                border: 1px solid #1a2a3a;
                border-radius: 20px;
                padding: 25px;
                position: relative;
                overflow: hidden;
            }
            /* Deep Animated Radar Background */
            .hero-card::before {
                content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%;
                background: conic-gradient(from 0deg, transparent 70%, rgba(0,229,255,0.1) 100%);
                animation: spinRadar 6s linear infinite; pointer-events: none; z-index: 1;
            }
            @keyframes spinRadar { 100% { transform: rotate(360deg); } }

            .hero-content { position: relative; z-index: 2; }
            .hero-greeting { font-family: var(--font-data); color: #888; font-size: 12px; letter-spacing: 2px; text-transform: uppercase; }
            .hero-main-text { font-family: var(--font-tech); font-size: 24px; color: #fff; margin: 5px 0 15px 0; line-height: 1.2; text-shadow: 0 0 20px rgba(0,229,255,0.3); }
            .hero-main-text span { color: var(--cyan-neon); }

            .hero-stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px; }
            .h-stat { background: rgba(0,0,0,0.6); border: 1px solid #222; border-radius: 10px; padding: 15px; border-left: 2px solid var(--gold-primary); }
            .h-stat-lbl { font-family: var(--font-body); font-size: 10px; color: #aaa; display: block; margin-bottom: 5px; }
            .h-stat-val { font-family: var(--font-tech); font-size: 18px; color: #fff; font-weight: bold; }
        </style>

        <div class="hero-card">
            <div class="hero-content">
                <div class="hero-greeting" id="liveGreeting">Initializing...</div>
                <h1 class="hero-main-text">WELCOME TO <span>MND</span><br>EVENT COMMAND</h1>
                
                <div class="hero-stats-grid">
                    <div class="h-stat" onclick="triggerToast('Server Ping: 12ms. All systems operational.')">
                        <span class="h-stat-lbl">SYSTEM STATUS</span>
                        <span class="h-stat-val" style="color: #00ff00; font-size: 14px;"><i class="fas fa-circle" style="font-size: 8px; vertical-align: middle; animation: blink 1s infinite;"></i> ONLINE</span>
                    </div>
                    <div class="h-stat" onclick="triggerToast('Tractor Fleet dispatched from Katoria.')">
                        <span class="h-stat-lbl">FLEET UNITS</span>
                        <span class="h-stat-val">4 ACTIVE</span>
                    </div>
                </div>

                <div style="display: flex; gap: 10px;">
                    <button class="app-btn-primary" onclick="triggerToast('Accessing Deep Booking Matrix...')">
                        <i class="fas fa-calendar-check"></i> NEW BOOKING
                    </button>
                    <button class="app-btn-outline" style="width: 50px;" onclick="triggerToast('Opening Support Uplink...')">
                        <i class="fas fa-headset"></i>
                    </button>
                </div>
            </div>
        </div>

        <style>
            .pricing-engine { padding: 5px; }
            
            /* Custom Range Sliders */
            .app-slider-container { margin-bottom: 25px; }
            .app-slider-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
            .app-slider-lbl { font-family: var(--font-data); color: #fff; font-size: 12px; font-weight: bold; letter-spacing: 1px;}
            .app-slider-val { font-family: var(--font-tech); color: var(--gold-primary); font-size: 16px; background: #000; padding: 4px 10px; border-radius: 6px; border: 1px solid #333;}
            
            .app-slider {
                -webkit-appearance: none; width: 100%; height: 8px; border-radius: 4px;
                background: #1a1a24; outline: none; border: 1px solid #333; box-shadow: inset 0 2px 5px rgba(0,0,0,0.8);
            }
            .app-slider::-webkit-slider-thumb {
                -webkit-appearance: none; appearance: none; width: 24px; height: 24px; border-radius: 50%;
                background: radial-gradient(circle, var(--gold-primary), #8a7322); cursor: grab;
                box-shadow: 0 0 15px rgba(212,175,55,0.6), inset 0 2px 4px rgba(255,255,255,0.4);
                border: 2px solid #000;
            }
            .app-slider::-webkit-slider-thumb:active { cursor: grabbing; transform: scale(1.1); }

            /* Setup Type Selectors */
            .setup-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-bottom: 30px; }
            .setup-card {
                background: #000; border: 1px solid #333; border-radius: 10px; padding: 15px 5px;
                text-align: center; cursor: pointer; transition: 0.2s; position: relative;
            }
            .setup-card i { font-size: 20px; color: #666; margin-bottom: 8px; transition: 0.2s; }
            .setup-card span { display: block; font-family: var(--font-data); font-size: 10px; font-weight: bold; color: #888; }
            
            /* Active State for Setup Cards */
            .setup-card.active { background: rgba(0,229,255,0.1); border-color: var(--cyan-neon); box-shadow: 0 5px 15px rgba(0,229,255,0.2); }
            .setup-card.active i { color: var(--cyan-neon); transform: scale(1.2); }
            .setup-card.active span { color: #fff; }

            /* Final Output Display */
            .price-output-box {
                background: linear-gradient(180deg, #111, #000); border: 2px dashed var(--gold-primary);
                border-radius: 12px; padding: 20px; text-align: center; margin-top: 10px;
                box-shadow: inset 0 0 30px rgba(212,175,55,0.1);
            }
            .price-lbl { font-family: var(--font-head); font-size: 12px; color: #aaa; display: block; margin-bottom: 5px; }
            .price-val { font-family: var(--font-tech); font-size: 36px; color: #00ff00; font-weight: 900; text-shadow: 0 0 20px rgba(0,255,0,0.4); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">AI PRICING ENGINE</h2>
                <div class="section-icon"><i class="fas fa-calculator"></i></div>
            </div>
            
            <div class="pricing-engine">
                <div class="app-slider-container">
                    <div class="app-slider-header">
                        <span class="app-slider-lbl">EXPECTED CROWD (PA REQUIRED)</span>
                        <span class="app-slider-val" id="valCrowd">500</span>
                    </div>
                    <input type="range" class="app-slider" id="slideCrowd" min="100" max="5000" step="100" value="500" oninput="calculateLivePrice()">
                </div>

                <div class="app-slider-container">
                    <div class="app-slider-header">
                        <span class="app-slider-lbl">DURATION (DG FUEL LOAD)</span>
                        <span class="app-slider-val" id="valHours">6 Hrs</span>
                    </div>
                    <input type="range" class="app-slider" id="slideHours" min="2" max="24" step="1" value="6" oninput="calculateLivePrice()">
                </div>

                <span style="font-family: var(--font-data); font-size: 12px; color: #fff; font-weight: bold; margin-bottom: 10px; display: block;">MND SETUP TIER</span>
                <div class="setup-grid">
                    <div class="setup-card" data-tier="1" data-multiplier="1.0" onclick="selectTier(this)">
                        <i class="fas fa-speaker"></i><span>STANDARD<br>BASS</span>
                    </div>
                    <div class="setup-card active" data-tier="2" data-multiplier="1.8" onclick="selectTier(this)">
                        <i class="fas fa-compact-disc"></i><span>PRO CLUB<br>DMX RIG</span>
                    </div>
                    <div class="setup-card" data-tier="3" data-multiplier="3.5" onclick="selectTier(this)">
                        <i class="fas fa-chess-king"></i><span>MAHARAJA<br>TENT + DJ</span>
                    </div>
                </div>

                <div class="price-output-box">
                    <span class="price-lbl">ESTIMATED SYSTEM COST</span>
                    <div class="price-val" id="livePriceOutput">₹ 0</div>
                    <span style="font-family: var(--font-body); font-size: 9px; color: #666; margin-top: 10px; display: block;">*Excludes transport beyond Banka district. Subject to availability.</span>
                </div>
            </div>
        </div>

        <style>
            .topo-widget { display: flex; align-items: center; gap: 15px; background: #000; border: 1px solid #222; border-radius: 12px; padding: 15px; margin-top: 20px; }
            .topo-radar { width: 50px; height: 50px; border-radius: 50%; border: 2px solid #00e5ff; position: relative; overflow: hidden; display: flex; justify-content: center; align-items: center;}
            .topo-radar::after { content:''; position:absolute; top:50%; left:50%; width:50%; height:2px; background:#00e5ff; transform-origin: left center; animation: radarScan 2s linear infinite; box-shadow: 0 0 10px #00e5ff;}
            @keyframes radarScan { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
            
            .topo-data { flex: 1; }
            .topo-title { font-family: var(--font-tech); font-size: 12px; color: var(--cyan-neon); margin-bottom: 5px; }
            .topo-line { display: flex; justify-content: space-between; font-family: var(--font-data); font-size: 11px; color: #aaa; border-bottom: 1px dashed #333; padding-bottom: 3px; margin-bottom: 3px;}
        </style>
        
        <div class="topo-widget" onclick="triggerToast('Running geographic scan for Laxmikant Transport routing...')">
            <div class="topo-radar"><i class="fas fa-satellite-dish" style="color: rgba(0,229,255,0.5); font-size: 20px;"></i></div>
            <div class="topo-data">
                <div class="topo-title">LOGISTICS SENSOR ACTIVE</div>
                <div class="topo-line"><span>Terrain:</span><span style="color:#fff;">Hard Soil (Safe)</span></div>
                <div class="topo-line"><span>Weather:</span><span style="color:#00ff00;">Clear (No Tent Cover Req.)</span></div>
            </div>
        </div>

        <div style="height: 80px; width: 100%;"></div>

    </main> <nav class="app-bottom-bar" id="bottomNav">
        <div class="tab-item active" onclick="switchTab(this, 'home')">
            <i class="fas fa-home"></i><span>HOME</span>
        </div>
        <div class="tab-item" onclick="switchTab(this, 'studio')">
            <i class="fas fa-sliders-h"></i><span>STUDIO</span>
        </div>
        <div class="tab-item" onclick="switchTab(this, 'vault')">
            <i class="fas fa-fingerprint"></i><span>VAULT</span>
        </div>
        <div class="tab-item" onclick="switchTab(this, 'profile')">
            <i class="fas fa-user-circle"></i><span>LALU</span>
        </div>
    </nav>

    <div id="appToast"><i class="fas fa-info-circle"></i> <span id="toastMsg">Notification</span></div>


    <script>
        // --- 1. SYSTEM BOOT SEQUENCE ---
        // This ensures the user sees a smooth loading screen while the browser renders the heavy DOM.
        document.addEventListener("DOMContentLoaded", () => {
            const bootScreen = document.getElementById('bootScreen');
            
            // Set dynamic greeting based on time of day
            const hour = new Date().getHours();
            const greetingEl = document.getElementById('liveGreeting');
            if(hour < 12) greetingEl.innerText = "Good Morning, Commander";
            else if (hour < 18) greetingEl.innerText = "Good Afternoon, Commander";
            else greetingEl.innerText = "Good Evening, Commander";

            // Fake loading delay for premium feel, then fade out
            setTimeout(() => {
                bootScreen.style.opacity = '0';
                setTimeout(() => {
                    bootScreen.style.display = 'none';
                    triggerToast("MND Neural Net Online.");
                    
                    // Initial calculation of the pricing engine
                    calculateLivePrice(); 
                }, 800); // Wait for CSS opacity transition
            }, 2000); // 2 seconds boot time
        });

        // --- 2. GLOBAL TOAST NOTIFICATION SYSTEM ---
        // A reusable function to trigger on-screen popups for any button press
        let toastTimeout;
        function triggerToast(message) {
            const toast = document.getElementById("appToast");
            const msgSpan = document.getElementById("toastMsg");
            
            msgSpan.innerText = message;
            toast.className = "show";
            
            // Haptic feedback (vibrates phone if supported)
            if (navigator.vibrate) {
                navigator.vibrate(50); // short 50ms buzz
            }

            // Clear existing timeout if spamming buttons
            clearTimeout(toastTimeout);
            
            // Hide after 3 seconds
            toastTimeout = setTimeout(function(){ 
                toast.className = toast.className.replace("show", ""); 
            }, 3000);
        }

        // --- 3. BOTTOM NAVIGATION LOGIC ---
        // Switches the active state color of the bottom icons
        function switchTab(element, tabName) {
            // Remove active class from all tabs
            const tabs = document.querySelectorAll('.tab-item');
            tabs.forEach(tab => tab.classList.remove('active'));
            
            // Add active class to clicked tab
            element.classList.add('active');
            
            // In a full app, this would hide/show different <section> tags.
            // For now, we trigger a toast to prove it works.
            triggerToast(`Routing to ${tabName.toUpperCase()} matrix...`);
            
            // Heavy haptic for tab switch
            if (navigator.vibrate) navigator.vibrate([30, 50, 30]);
        }

        // --- 4. AI DYNAMIC PRICING ENGINE LOGIC ---
        // Variables to hold state
        let currentMultiplier = 1.8; // Default is PRO CLUB (Tier 2)

        function selectTier(element) {
            // Remove active class from all cards
            const cards = document.querySelectorAll('.setup-card');
            cards.forEach(card => card.classList.remove('active'));
            
            // Add to clicked
            element.classList.add('active');
            
            // Update math multiplier
            currentMultiplier = parseFloat(element.getAttribute('data-multiplier'));
            
            // Haptic & Recalculate
            if (navigator.vibrate) navigator.vibrate(20);
            calculateLivePrice();
        }

        function calculateLivePrice() {
            // Get values from sliders
            const crowdSlider = document.getElementById('slideCrowd');
            const hoursSlider = document.getElementById('slideHours');
            
            const crowdVal = parseInt(crowdSlider.value);
            const hoursVal = parseInt(hoursSlider.value);
            
            // Update Text Displays above sliders
            document.getElementById('valCrowd').innerText = crowdVal.toLocaleString();
            document.getElementById('valHours').innerText = hoursVal + " Hrs";

            // THE MND PRICING ALGORITHM (Proprietary Math)
            // Base setup fee
            let baseFee = 5000;
            
            // Cost per person (sound scaling) - larger crowd = exponentially more expensive PA system
            let crowdCost = crowdVal * 15; 
            
            // Cost per hour (generator fuel + crew time)
            let timeCost = hoursVal * 800; 

            // Calculate Raw Total
            let rawTotal = baseFee + crowdCost + timeCost;
            
            // Apply Setup Tier Multiplier (Standard x1, Pro x1.8, Maharaja x3.5)
            let finalPrice = Math.round(rawTotal * currentMultiplier);

            // Animate the number counting up
            animateValue("livePriceOutput", finalPrice, 500); // 500ms duration
        }

        // --- 5. NUMBER COUNTUP ANIMATION ---
        // Makes the price display roll up smoothly instead of snapping instantly
        function animateValue(id, end, duration) {
            const obj = document.getElementById(id);
            
            // Get current number displayed, remove commas and ₹ symbol
            let startStr = obj.innerText.replace(/[^0-9]/g, '');
            let start = parseInt(startStr) || 0;
            
            // If it's the exact same number, do nothing to save CPU
            if (start === end) return;

            let startTimestamp = null;
            const step = (timestamp) => {
                if (!startTimestamp) startTimestamp = timestamp;
                const progress = Math.min((timestamp - startTimestamp) / duration, 1);
                
                // Easing function (easeOutQuad)
                const easeProgress = progress * (2 - progress);
                
                const currentVal = Math.floor(easeProgress * (end - start) + start);
                
                // Format with Indian Rupee formatting
                obj.innerText = "₹ " + currentVal.toLocaleString('en-IN');
                
                if (progress < 1) {
                    window.requestAnimationFrame(step);
                } else {
                    // Ensure final exact value is set
                    obj.innerText = "₹ " + end.toLocaleString('en-IN');
                    // Flash text green on finish
                    obj.style.color = "#fff";
                    setTimeout(()=> obj.style.color = "#00ff00", 100);
                }
            };
            window.requestAnimationFrame(step);
        }
    </script>
    <style>
            .studio-wrapper {
                background: linear-gradient(135deg, #111116 0%, #08080a 100%);
                border: 2px solid #2a2a35;
                border-radius: 16px;
                padding: 20px 15px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 -5px 15px rgba(0,0,0,0.8);
            }

            /* Carbon Fiber Faceplate Texture */
            .studio-wrapper::before {
                content: ''; position: absolute; top: 0; left: 0; right: 0; bottom: 0;
                background: 
                    linear-gradient(27deg, #151515 5px, transparent 5px) 0 5px,
                    linear-gradient(207deg, #151515 5px, transparent 5px) 10px 0px,
                    linear-gradient(27deg, #222 5px, transparent 5px) 0px 10px,
                    linear-gradient(207deg, #222 5px, transparent 5px) 10px 5px;
                background-size: 20px 20px; opacity: 0.2; pointer-events: none; z-index: 0;
            }

            .studio-content { position: relative; z-index: 2; }

            /* Engine Power Button */
            .engine-pwr-box {
                display: flex; justify-content: space-between; align-items: center;
                background: #000; padding: 15px; border-radius: 12px; border: 1px solid #333; margin-bottom: 20px;
            }
            .engine-led { width: 15px; height: 15px; border-radius: 50%; background: #333; border: 2px solid #111; box-shadow: inset 0 0 5px #000; transition: 0.3s; }
            .engine-led.active { background: #00ff00; box-shadow: 0 0 15px #00ff00, inset 0 0 5px #fff; }

            /* Launchpad 16-Grid */
            .launchpad-grid {
                display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px;
                background: #0a0a0a; padding: 15px; border-radius: 12px; border: 1px solid #222;
                box-shadow: inset 0 10px 25px rgba(0,0,0,0.8); margin-bottom: 25px;
            }

            .pad-btn {
                aspect-ratio: 1 / 1;
                background: linear-gradient(180deg, #333 0%, #1a1a1a 100%);
                border: none; border-radius: 8px;
                box-shadow: 0 6px 0 #0f0f0f, 0 8px 10px rgba(0,0,0,0.9), inset 0 2px 5px rgba(255,255,255,0.2);
                position: relative; cursor: pointer; transition: transform 0.05s, box-shadow 0.05s;
                overflow: hidden;
                /* Disable zoom on double tap for pads */
                touch-action: manipulation; 
            }
            .pad-btn::before { content: ''; position: absolute; inset: 4px; border-radius: 4px; border: 2px solid rgba(255,255,255,0.05); transition: 0.05s; }

            /* 3D Physical Push Effect */
            .pad-btn:active, .pad-btn.active-state {
                transform: translateY(6px);
                box-shadow: 0 0px 0 #0f0f0f, 0 2px 5px rgba(0,0,0,0.9), inset 0 2px 5px rgba(255,255,255,0.1);
            }

            /* Pad Color Coding */
            .pad-red:active::before, .pad-red.active-state::before { border-color: #ff3333; background: rgba(255,51,51,0.3); box-shadow: 0 0 20px #ff3333; }
            .pad-cyan:active::before, .pad-cyan.active-state::before { border-color: #00e5ff; background: rgba(0,229,255,0.3); box-shadow: 0 0 20px #00e5ff; }
            .pad-gold:active::before, .pad-gold.active-state::before { border-color: var(--gold-primary); background: rgba(212,175,55,0.3); box-shadow: 0 0 20px var(--gold-primary); }
            .pad-purp:active::before, .pad-purp.active-state::before { border-color: #b829ff; background: rgba(184,41,255,0.3); box-shadow: 0 0 20px #b829ff; }

            /* Dual Decks Layout */
            .dj-decks { display: flex; justify-content: space-between; gap: 10px; }
            
            .deck {
                flex: 1; background: #111; border: 1px solid #333; border-radius: 12px;
                padding: 10px; display: flex; flex-direction: column; align-items: center; position: relative;
            }
            
            .platter {
                width: 100px; height: 100px; border-radius: 50%;
                background: repeating-radial-gradient(#222 0, #222 2px, #111 3px, #111 4px);
                border: 3px solid #444; display: flex; justify-content: center; align-items: center;
                box-shadow: 0 10px 20px rgba(0,0,0,0.8); position: relative;
                transition: transform 0.1s linear;
            }
            .platter.spin { animation: spinPlatter 2s linear infinite; }
            @keyframes spinPlatter { 100% { transform: rotate(360deg); } }

            .platter-label {
                width: 30px; height: 30px; border-radius: 50%; display: flex; justify-content: center; align-items: center; border: 2px solid #000;
            }
            .platter-label::after { content: ''; width: 4px; height: 4px; background: #000; border-radius: 50%; }
            .marker { position: absolute; top: 5px; width: 4px; height: 15px; background: #fff; border-radius: 2px; }

            .tonearm {
                position: absolute; top: 10px; right: 5px; width: 10px; height: 60px;
                background: linear-gradient(90deg, #888, #ccc, #888); transform-origin: top center;
                transform: rotate(-15deg); transition: 0.5s cubic-bezier(0.25, 1, 0.5, 1);
                border-radius: 5px; box-shadow: 2px 5px 10px rgba(0,0,0,0.8); z-index: 5;
            }
            .deck.playing .tonearm { transform: rotate(20deg); }

            /* Crossfader */
            .cf-box { background: #0a0a0f; border: 1px solid #222; border-radius: 8px; padding: 15px; margin-top: 15px; }
            .cf-track { width: 100%; height: 8px; background: #000; border-radius: 4px; position: relative; box-shadow: inset 0 2px 5px rgba(0,0,0,0.8); }
            .cf-knob {
                width: 24px; height: 36px; background: linear-gradient(180deg, #555, #222);
                border: 2px solid #111; border-radius: 4px; position: absolute; top: -14px; left: 50%; transform: translateX(-50%);
                cursor: grab; box-shadow: 0 5px 10px rgba(0,0,0,0.8);
            }
            .cf-knob::after { content: ''; position: absolute; top: 50%; left: 10%; right: 10%; height: 2px; background: #fff; transform: translateY(-50%); }
            .cf-knob:active { cursor: grabbing; background: linear-gradient(180deg, #777, #333); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">MND VIRTUAL STUDIO</h2>
                <div class="section-icon"><i class="fas fa-headphones"></i></div>
            </div>

            <div class="studio-wrapper">
                <div class="studio-content">
                    
                    <div class="engine-pwr-box">
                        <div>
                            <span style="font-family: var(--font-tech); font-size: 14px; color: #fff; font-weight: bold;">AUDIO ENGINE</span>
                            <span style="font-family: var(--font-data); font-size: 10px; color: #888; display: block;">WEB AUDIO API SYNTHESIS</span>
                        </div>
                        <div style="display: flex; align-items: center; gap: 15px;">
                            <div class="engine-led" id="synthLed"></div>
                            <button class="app-btn-outline" style="padding: 8px 15px; font-size: 10px;" id="btnBootAudio" onclick="bootAudioEngine()">BOOT SYS</button>
                        </div>
                    </div>

                    <span style="font-family: var(--font-tech); font-size: 10px; color: var(--gold-primary); letter-spacing: 2px; margin-bottom: 10px; display: block;">LIVE SAMPLER PADS</span>
                    <div class="launchpad-grid">
                        <button class="pad-btn pad-red" onpointerdown="playSynth('kick', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-red" onpointerdown="playSynth('punch', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-red" onpointerdown="playSynth('sub808', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-red" onpointerdown="playSynth('subDrop', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        
                        <button class="pad-btn pad-cyan" onpointerdown="playSynth('snare1', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-cyan" onpointerdown="playSynth('clap', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-cyan" onpointerdown="playSynth('hihatC', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-cyan" onpointerdown="playSynth('hihatO', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>

                        <button class="pad-btn pad-gold" onpointerdown="playSynth('laserA', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-gold" onpointerdown="playSynth('laserB', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-gold" onpointerdown="playSynth('chordMin', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-gold" onpointerdown="playSynth('chordMaj', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>

                        <button class="pad-btn pad-purp" onpointerdown="playSynth('djHorn', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-purp" onpointerdown="playSynth('siren', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-purp" onpointerdown="playSynth('sweepUp', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                        <button class="pad-btn pad-purp" onpointerdown="playSynth('impact', this)" onpointerup="releaseSynth(this)" onpointerleave="releaseSynth(this)"></button>
                    </div>

                    <span style="font-family: var(--font-tech); font-size: 10px; color: var(--gold-primary); letter-spacing: 2px; margin-bottom: 10px; display: block;">AUTO-MIXER DECKS</span>
                    <div class="dj-decks">
                        <div class="deck" id="deckA">
                            <div class="tonearm"></div>
                            <div class="platter" id="platA" onpointerdown="scratchDeck('A', event)">
                                <div class="marker"></div>
                                <div class="platter-label" style="background: var(--cyan-neon);"></div>
                            </div>
                            <button class="app-btn-outline" style="margin-top: 15px; width: 100%; padding: 8px; font-size: 10px;" onclick="toggleDeckPlay('A')">CH A: PLAY</button>
                        </div>

                        <div class="deck" id="deckB">
                            <div class="tonearm"></div>
                            <div class="platter" id="platB" onpointerdown="scratchDeck('B', event)">
                                <div class="marker"></div>
                                <div class="platter-label" style="background: var(--red-alert);"></div>
                            </div>
                            <button class="app-btn-outline" style="margin-top: 15px; width: 100%; padding: 8px; font-size: 10px;" onclick="toggleDeckPlay('B')">CH B: PLAY</button>
                        </div>
                    </div>

                    <div class="cf-box">
                        <div style="display: flex; justify-content: space-between; font-family: var(--font-tech); font-size: 9px; color: #666; margin-bottom: 10px;">
                            <span>DECK A</span><span>X-FADER</span><span>DECK B</span>
                        </div>
                        <div class="cf-track" id="cfTrack">
                            <div class="cf-knob" id="cfKnob"></div>
                        </div>
                    </div>

                </div>
            </div>
        </div>

        <script>
            // --- GLOBAL AUDIO CONTEXT ---
            let actx = null;
            let masterGain = null;
            let distortionNode = null;
            let isEngineOn = false;

            // --- 1. BOOT ENGINE ---
            // Browsers require a user interaction (click) to start the AudioContext
            function bootAudioEngine() {
                const btn = document.getElementById('btnBootAudio');
                const led = document.getElementById('synthLed');

                if (!isEngineOn) {
                    try {
                        const AudioContext = window.AudioContext || window.webkitAudioContext;
                        actx = new AudioContext();
                        
                        // Setup Master Routing
                        masterGain = actx.createGain();
                        masterGain.gain.value = 0.8; // 80% volume default
                        
                        distortionNode = actx.createWaveShaper();
                        distortionNode.curve = makeDistCurve(0); // 0 distortion to start
                        distortionNode.oversample = '4x';

                        // Route: Distortion -> Master -> Speakers
                        distortionNode.connect(masterGain);
                        masterGain.connect(actx.destination);

                        isEngineOn = true;
                        led.classList.add('active');
                        btn.innerText = "SHUTDOWN";
                        btn.style.color = "#ff3333";
                        btn.style.borderColor = "#ff3333";
                        
                        triggerToast("Web Audio API Synthesizer Booted Successfully.");
                        
                        // Play a startup chord
                        playSynth('chordMaj', null);

                    } catch(e) {
                        triggerToast("Audio Error: Browser does not support Web Audio API.");
                    }
                } else {
                    // Shut down
                    if(actx) actx.close();
                    isEngineOn = false;
                    led.classList.remove('active');
                    btn.innerText = "BOOT SYS";
                    btn.style.color = "var(--cyan-neon)";
                    btn.style.borderColor = "var(--cyan-neon)";
                    triggerToast("Audio Engine Offline.");
                }
            }

            // Math function for heavy distortion
            function makeDistCurve(amount) {
                const k = typeof amount === 'number' ? amount : 50;
                const n_samples = 44100;
                const curve = new Float32Array(n_samples);
                const deg = Math.PI / 180;
                for (let i = 0; i < n_samples; ++i) {
                    const x = i * 2 / n_samples - 1;
                    curve[i] = (3 + k) * x * 20 * deg / (Math.PI + k * Math.abs(x));
                }
                return curve;
            }

            // --- 2. PAD INTERACTION VISUALS ---
            function releaseSynth(element) {
                if(element) element.classList.remove('active-state');
            }

            // --- 3. SYNTHESIS ENGINE (Generating the sounds) ---
            function playSynth(soundType, element) {
                if(!isEngineOn) {
                    triggerToast("System Offline. Boot Audio Engine First.");
                    // Shake the boot button to direct attention
                    const btn = document.getElementById('btnBootAudio');
                    btn.style.transform = 'translateX(5px)';
                    setTimeout(()=> btn.style.transform = 'translateX(-5px)', 50);
                    setTimeout(()=> btn.style.transform = 'translateX(0)', 100);
                    return;
                }

                if(element) {
                    element.classList.add('active-state');
                    if(navigator.vibrate) navigator.vibrate(15); // Light haptic tap
                }

                const t = actx.currentTime;
                const osc = actx.createOscillator();
                const gain = actx.createGain();

                // Route oscillator to its own gain, then to master distortion
                osc.connect(gain);
                gain.connect(distortionNode);

                switch(soundType) {
                    case 'kick':
                        // Standard Punchy Kick
                        osc.type = 'sine';
                        osc.frequency.setValueAtTime(150, t);
                        osc.frequency.exponentialRampToValueAtTime(0.01, t + 0.5);
                        gain.gain.setValueAtTime(1, t);
                        gain.gain.exponentialRampToValueAtTime(0.01, t + 0.5);
                        osc.start(t); osc.stop(t + 0.5);
                        break;
                        
                    case 'sub808':
                        // Deep MND Bass
                        osc.type = 'sine';
                        osc.frequency.setValueAtTime(50, t);
                        osc.frequency.exponentialRampToValueAtTime(30, t + 1.5); // Pitch drops slightly
                        gain.gain.setValueAtTime(1, t);
                        gain.gain.linearRampToValueAtTime(0.8, t + 0.2); // Hold
                        gain.gain.exponentialRampToValueAtTime(0.01, t + 1.5); // Fade
                        osc.start(t); osc.stop(t + 1.5);
                        // Heavy haptic for bass
                        if(navigator.vibrate) navigator.vibrate([50, 30, 50]); 
                        break;

                    case 'snare1':
                        // Noise Burst Snare
                        const noiseBuf = actx.createBuffer(1, actx.sampleRate * 0.2, actx.sampleRate);
                        const output = noiseBuf.getChannelData(0);
                        for (let i = 0; i < noiseBuf.length; i++) output[i] = Math.random() * 2 - 1;
                        
                        const noiseSrc = actx.createBufferSource();
                        noiseSrc.buffer = noiseBuf;
                        const noiseFilter = actx.createBiquadFilter();
                        noiseFilter.type = 'highpass';
                        noiseFilter.frequency.value = 1000;
                        
                        const noiseGain = actx.createGain();
                        noiseGain.gain.setValueAtTime(1, t);
                        noiseGain.gain.exponentialRampToValueAtTime(0.01, t + 0.2);
                        
                        noiseSrc.connect(noiseFilter);
                        noiseFilter.connect(noiseGain);
                        noiseGain.connect(distortionNode);
                        noiseSrc.start(t);
                        break;

                    case 'laserA':
                        // High Pitch Pew
                        osc.type = 'sawtooth';
                        osc.frequency.setValueAtTime(1500, t);
                        osc.frequency.exponentialRampToValueAtTime(100, t + 0.2);
                        gain.gain.setValueAtTime(0.5, t);
                        gain.gain.exponentialRampToValueAtTime(0.01, t + 0.2);
                        osc.start(t); osc.stop(t + 0.2);
                        break;

                    case 'djHorn':
                        // Air Horn (Multiple dissonant oscillators)
                        const freqs = [300, 340, 380];
                        freqs.forEach(f => {
                            const o = actx.createOscillator();
                            const g = actx.createGain();
                            o.type = 'square';
                            o.frequency.setValueAtTime(f, t);
                            // Wobbly pitch
                            o.frequency.linearRampToValueAtTime(f + 20, t + 0.1);
                            o.frequency.linearRampToValueAtTime(f, t + 0.4);
                            o.connect(g); g.connect(distortionNode);
                            g.gain.setValueAtTime(0, t);
                            g.gain.linearRampToValueAtTime(0.3, t + 0.05); // Attack
                            g.gain.exponentialRampToValueAtTime(0.01, t + 0.6); // Decay
                            o.start(t); o.stop(t + 0.6);
                        });
                        break;

                    case 'chordMaj':
                        // Happy Chord
                        [261.63, 329.63, 392.00].forEach(f => { // C4, E4, G4
                            const o = actx.createOscillator();
                            const g = actx.createGain();
                            o.type = 'triangle'; o.frequency.value = f;
                            o.connect(g); g.connect(distortionNode);
                            g.gain.setValueAtTime(0, t);
                            g.gain.linearRampToValueAtTime(0.2, t + 0.1);
                            g.gain.exponentialRampToValueAtTime(0.01, t + 1.0);
                            o.start(t); o.stop(t + 1.0);
                        });
                        break;

                    default:
                        // Fallback beep
                        osc.type = 'sine'; osc.frequency.value = 440;
                        gain.gain.setValueAtTime(0.5, t); gain.gain.exponentialRampToValueAtTime(0.01, t + 0.1);
                        osc.start(t); osc.stop(t + 0.1);
                }
            }

            // --- 4. DUAL DECK MECHANICS ---
            let deckAState = false;
            let deckBState = false;

            function toggleDeckPlay(deckId) {
                if(typeof playTap === 'function') playTap();
                const deckWrap = document.getElementById('deck' + deckId);
                const platter = document.getElementById('plat' + deckId);
                const btn = deckWrap.querySelector('button');

                if(deckId === 'A') {
                    deckAState = !deckAState;
                    if(deckAState) {
                        deckWrap.classList.add('playing');
                        platter.classList.add('spin');
                        btn.innerText = "CH A: PAUSE";
                        btn.style.color = "var(--gold-primary)";
                        btn.style.borderColor = "var(--gold-primary)";
                        if(isEngineOn) playSynth('hihatC', null); // Tick sound
                    } else {
                        deckWrap.classList.remove('playing');
                        platter.classList.remove('spin');
                        btn.innerText = "CH A: PLAY";
                        btn.style.color = "var(--cyan-neon)";
                        btn.style.borderColor = "var(--cyan-neon)";
                    }
                } else {
                    deckBState = !deckBState;
                    if(deckBState) {
                        deckWrap.classList.add('playing');
                        platter.classList.add('spin');
                        btn.innerText = "CH B: PAUSE";
                        btn.style.color = "var(--gold-primary)";
                        btn.style.borderColor = "var(--gold-primary)";
                    } else {
                        deckWrap.classList.remove('playing');
                        platter.classList.remove('spin');
                        btn.innerText = "CH B: PLAY";
                        btn.style.color = "var(--cyan-neon)";
                        btn.style.borderColor = "var(--cyan-neon)";
                    }
                }
            }

            // --- 5. RECORD SCRATCHING LOGIC (Touch & Drag) ---
            let isScratching = false;
            let scratchStartX = 0;
            let activePlatter = null;

            function scratchDeck(deckId, e) {
                e.preventDefault(); // Stop page scrolling
                isScratching = true;
                activePlatter = document.getElementById('plat' + deckId);
                scratchStartX = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                
                // Pause CSS animation if it was playing
                activePlatter.style.animationPlayState = 'paused';
                
                // Play synth scratch sound
                if(isEngineOn) playSynth('snare1', null); 
            }

            function handleScratchMove(e) {
                if(!isScratching || !activePlatter) return;
                e.preventDefault();
                
                const currentX = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                const deltaX = currentX - scratchStartX;
                
                // Manually rotate the platter based on drag distance
                activePlatter.style.transform = `rotate(${deltaX * 3}deg)`;
            }

            function endScratch() {
                if(!isScratching) return;
                isScratching = false;
                if(activePlatter) {
                    activePlatter.style.transform = ''; // Clear manual transform
                    activePlatter.style.animationPlayState = 'running'; // Resume if playing
                    activePlatter = null;
                }
            }

            // Attach global listeners for smooth dragging outside the div bounds
            window.addEventListener('mousemove', handleScratchMove);
            window.addEventListener('touchmove', handleScratchMove, {passive: false});
            window.addEventListener('mouseup', endScratch);
            window.addEventListener('touchend', endScratch);

            // --- 6. CROSSFADER LOGIC ---
            const cfTrack = document.getElementById('cfTrack');
            const cfKnob = document.getElementById('cfKnob');
            let isFading = false;

            cfKnob.addEventListener('mousedown', (e) => { isFading = true; e.preventDefault(); });
            cfKnob.addEventListener('touchstart', (e) => { isFading = true; }, {passive: true});

            window.addEventListener('mousemove', (e) => {
                if(!isFading) return;
                const rect = cfTrack.getBoundingClientRect();
                let x = e.clientX - rect.left;
                if(x < 0) x = 0;
                if(x > rect.width) x = rect.width;
                cfKnob.style.left = `${x}px`;
            });
            window.addEventListener('touchmove', (e) => {
                if(!isFading) return;
                const rect = cfTrack.getBoundingClientRect();
                let x = e.touches[0].clientX - rect.left;
                if(x < 0) x = 0;
                if(x > rect.width) x = rect.width;
                cfKnob.style.left = `${x}px`;
            }, {passive: true});

            window.addEventListener('mouseup', () => isFading = false);
            window.addEventListener('touchend', () => isFading = false);
        </script>
        <style>
            .dream-crafter-wrapper {
                background: linear-gradient(180deg, var(--app-surface), #05080f);
                border: 1px solid var(--glass-border);
                border-radius: 16px;
                padding: 20px 10px;
                box-shadow: 0 20px 40px rgba(0,0,0,0.8), inset 0 0 20px rgba(0,229,255,0.05);
                display: flex;
                flex-direction: column;
                gap: 15px;
            }

            /* Live HUD for Budget & Status */
            .builder-hud {
                display: flex;
                justify-content: space-between;
                align-items: center;
                background: rgba(0,0,0,0.6);
                padding: 12px 15px;
                border-radius: 12px;
                border: 1px solid #222;
            }
            .hud-title { display: flex; flex-direction: column; }
            .hud-title span:first-child { font-family: var(--font-head); font-size: 14px; font-weight: bold; color: #fff; }
            .hud-title span:last-child { font-family: var(--font-tech); font-size: 9px; color: var(--cyan-neon); }
            .hud-budget { font-family: var(--font-tech); font-size: 20px; font-weight: 900; color: #00ff00; text-shadow: 0 0 10px rgba(0,255,0,0.4); transition: 0.3s; }

            /* Blueprint Canvas Area */
            .blueprint-canvas {
                width: 100%;
                height: 320px;
                background-color: #020a14;
                background-image: 
                    linear-gradient(rgba(0, 229, 255, 0.15) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(0, 229, 255, 0.15) 1px, transparent 1px);
                background-size: 25px 25px;
                border: 2px solid #004466;
                border-radius: 12px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 30px rgba(0,0,0,1);
                /* Prevent scroll when dragging inside */
                touch-action: none;
            }
            .blueprint-canvas::after {
                content: ''; position: absolute; inset: 0;
                background: radial-gradient(circle at center, transparent 40%, rgba(2,10,20,0.9) 100%);
                pointer-events: none; z-index: 1;
            }
            .zone-label {
                position: absolute; bottom: 10px; left: 50%; transform: translateX(-50%);
                color: rgba(0, 229, 255, 0.3); font-family: var(--font-tech); font-size: 12px; font-weight: bold; letter-spacing: 4px; pointer-events: none; z-index: 1;
            }

            /* Inventory Palette (Scrollable) */
            .inventory-palette {
                display: flex;
                gap: 12px;
                overflow-x: auto;
                padding: 10px 5px;
                scrollbar-width: none; /* Firefox */
                background: #000;
                border-radius: 12px;
                border: 1px solid #222;
            }
            .inventory-palette::-webkit-scrollbar { display: none; } /* Chrome/Safari */

            /* Draggable Items */
            .drag-source-item {
                flex: 0 0 60px;
                width: 60px; height: 60px;
                background: linear-gradient(135deg, #111, #222);
                border: 1px solid var(--gold-primary);
                border-radius: 10px;
                display: flex; flex-direction: column; justify-content: center; align-items: center;
                cursor: grab; position: relative; z-index: 10;
                box-shadow: 0 4px 10px rgba(0,0,0,0.5);
                touch-action: none; /* CRITICAL for custom mobile drag */
            }
            .drag-source-item i { font-size: 24px; color: var(--gold-primary); pointer-events: none; }
            .drag-source-item span { font-family: var(--font-data); font-size: 8px; color: #fff; margin-top: 4px; font-weight: bold; pointer-events: none; text-align: center; line-height: 1;}
            .drag-source-item:active { background: var(--gold-primary); transform: scale(1.05); }
            .drag-source-item:active i, .drag-source-item:active span { color: #000; }

            /* Placed Items on the Blueprint */
            .placed-item {
                position: absolute;
                width: 50px; height: 50px;
                background: rgba(0, 229, 255, 0.1);
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                display: flex; justify-content: center; align-items: center;
                color: var(--cyan-neon); font-size: 20px;
                box-shadow: 0 0 15px rgba(0, 229, 255, 0.3);
                cursor: grab; z-index: 5;
                transform: translate(-50%, -50%); /* Center on finger */
                animation: dropIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
                touch-action: none;
            }
            .placed-item:active { cursor: grabbing; border-color: var(--red-alert); color: var(--red-alert); box-shadow: 0 0 20px rgba(255,51,51,0.5); z-index: 100;}
            
            @keyframes dropIn { 0% { transform: translate(-50%, -50%) scale(0); } 100% { transform: translate(-50%, -50%) scale(1); } }

            /* Trash Can for deleting placed items */
            .trash-zone {
                position: absolute; top: 10px; right: 10px;
                width: 40px; height: 40px; background: rgba(255,51,51,0.2);
                border: 1px dashed var(--red-alert); border-radius: 8px;
                display: flex; justify-content: center; align-items: center;
                color: var(--red-alert); font-size: 16px; z-index: 2; opacity: 0.5; transition: 0.3s;
            }
            .trash-zone.active-trash { opacity: 1; background: var(--red-alert); color: #fff; transform: scale(1.1); }
        </style>

        <style>
            .holo-section-wrapper {
                background: #000;
                border: 1px solid #1a1a24;
                border-radius: 16px;
                margin-top: 20px;
                padding: 30px 0;
                overflow: hidden;
            }

            .holo-scene {
                width: 100%;
                height: 350px;
                perspective: 1200px; /* Gives the 3D depth */
                display: flex;
                justify-content: center;
                align-items: center;
                position: relative;
            }
            
            /* Ambient Floor Lighting */
            .holo-scene::after {
                content: ''; position: absolute; bottom: 10px; left: 50%; transform: translateX(-50%);
                width: 70%; height: 20px; background: radial-gradient(ellipse, rgba(212,175,55,0.4) 0%, transparent 70%);
                filter: blur(15px); pointer-events: none; z-index: 0;
            }

            .holo-carousel {
                width: 220px; /* Width of front facing panel */
                height: 280px;
                position: relative;
                transform-style: preserve-3d;
                transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);
                z-index: 2;
            }

            .holo-panel {
                position: absolute;
                width: 100%;
                height: 100%;
                left: 0; top: 0;
                border: 2px solid var(--gold-primary);
                border-radius: 12px;
                overflow: hidden;
                box-shadow: 0 0 20px rgba(0,0,0,0.9), inset 0 0 15px rgba(212,175,55,0.3);
                background: #111;
                /* Backface hidden prevents seeing reverse images */
                backface-visibility: hidden;
                /* Floor reflection */
                -webkit-box-reflect: below 5px linear-gradient(transparent 60%, rgba(0,0,0,0.5)); 
            }
            .holo-panel img { width: 100%; height: 100%; object-fit: cover; filter: contrast(1.1) brightness(0.8); transition: 0.3s; }
            .holo-panel:hover img { filter: contrast(1.2) brightness(1.1); }

            /* HUD Controls for 3D */
            .holo-controls {
                display: flex; justify-content: center; gap: 20px; margin-top: 20px; z-index: 10; position: relative;
            }
            .h-btn {
                width: 50px; height: 50px; border-radius: 50%; background: rgba(20,20,25,0.8);
                border: 1px solid var(--gold-primary); color: var(--gold-primary); font-size: 20px;
                display: flex; justify-content: center; align-items: center; cursor: pointer;
                box-shadow: 0 5px 15px rgba(0,0,0,0.5); backdrop-filter: blur(10px); transition: 0.2s;
            }
            .h-btn:active { background: var(--gold-primary); color: #000; transform: scale(0.9); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">VIRTUAL STAGE BUILDER</h2>
                <div class="section-icon"><i class="fas fa-drafting-compass"></i></div>
            </div>

            <div class="dream-crafter-wrapper">
                <div class="builder-hud">
                    <div class="hud-title">
                        <span>PROJECT BLUEPRINT</span>
                        <span>GRID ACCURACY: 1m x 1m</span>
                    </div>
                    <div class="hud-budget" id="blueprintBudget">₹0</div>
                </div>

                <div class="blueprint-canvas" id="bpCanvas">
                    <div class="zone-label">VIP DANCE FLOOR</div>
                    <div class="trash-zone" id="bpTrash"><i class="fas fa-trash"></i></div>
                    </div>

                <span style="font-family: var(--font-data); font-size: 10px; color: #888; text-transform: uppercase;">DRAG EQUIPMENT TO CANVAS</span>
                
                <div class="inventory-palette" id="bpPalette">
                    <div class="drag-source-item" data-type="dj" data-icon="fa-compact-disc" data-price="8000">
                        <i class="fas fa-compact-disc"></i><span>DJ RIG</span>
                    </div>
                    <div class="drag-source-item" data-type="sub" data-icon="fa-speaker" data-price="3500">
                        <i class="fas fa-volume-up"></i><span>SUB 21"</span>
                    </div>
                    <div class="drag-source-item" data-type="laser" data-icon="fa-bolt" data-price="1500">
                        <i class="fas fa-bolt"></i><span>LASER</span>
                    </div>
                    <div class="drag-source-item" data-type="truss" data-icon="fa-campground" data-price="15000">
                        <i class="fas fa-campground"></i><span>TENT</span>
                    </div>
                    <div class="drag-source-item" data-type="sofa" data-icon="fa-couch" data-price="2500">
                        <i class="fas fa-couch"></i><span>VIP SOFA</span>
                    </div>
                    <div class="drag-source-item" data-type="gen" data-icon="fa-charging-station" data-price="5000">
                        <i class="fas fa-charging-station"></i><span>DG SET</span>
                    </div>
                </div>

                <button class="app-btn-outline" style="border-color: var(--red-alert); color: var(--red-alert);" onclick="clearBlueprint()">
                    <i class="fas fa-eraser"></i> WIPE BLUEPRINT
                </button>
            </div>
        </div>

        <div class="app-section" style="padding: 0; background: transparent; border: none; box-shadow: none;">
            <div style="padding: 0 20px;">
                <div class="section-header" style="margin-bottom: 0;">
                    <h2 class="section-title">3D EVENT MATRIX</h2>
                    <div class="section-icon"><i class="fas fa-cube"></i></div>
                </div>
            </div>

            <div class="holo-section-wrapper">
                <div class="holo-scene">
                    <div class="holo-carousel" id="holoCarousel">
                        <div class="holo-panel"><img src="https://i.postimg.cc/pXx5fqGQ/image_fac9be10.png" alt="Royal Setup"></div>
                        <div class="holo-panel"><img src="https://i.postimg.cc/g20XqtDW/IMG_20260303_121446.png" alt="DJ Rig"></div>
                        <div class="holo-panel"><img src="https://i.postimg.cc/cLJgMkmJ/maxresdefault.jpg" alt="Lighting"></div>
                        <div class="holo-panel"><img src="https://i.postimg.cc/76mz1v2j/file-0000000090a471fa84cbecd48a774885.png" alt="Logo"></div>
                        <div class="holo-panel"><img src="https://i.postimg.cc/5yRdctZh/1771529133710.jpg" alt="Truss"></div>
                        <div class="holo-panel"><img src="https://i.postimg.cc/hPgQLpyz/image_b73be3f2_1.png" alt="Floral"></div>
                    </div>
                </div>

                <div class="holo-controls">
                    <div class="h-btn" onclick="rotateHolo(-1)"><i class="fas fa-chevron-left"></i></div>
                    <div class="h-btn" id="btnHoloAuto" onclick="toggleHoloAuto()"><i class="fas fa-pause"></i></div>
                    <div class="h-btn" onclick="rotateHolo(1)"><i class="fas fa-chevron-right"></i></div>
                </div>
            </div>
        </div>


        <script>
            // --- 1. VIRTUAL STAGE BUILDER LOGIC (Native Touch Drag Engine) ---
            const bpCanvas = document.getElementById('bpCanvas');
            const sourceItems = document.querySelectorAll('.drag-source-item');
            const bpTrash = document.getElementById('bpTrash');
            const budgetDisplay = document.getElementById('blueprintBudget');
            
            let activeDragObj = null;
            let currentBlueprintTotal = 0;
            let isNewSpawn = false; // Flag to check if we are pulling from palette or moving an existing item

            // Attach listeners to inventory palette items
            sourceItems.forEach(item => {
                item.addEventListener('mousedown', bpDragStart);
                item.addEventListener('touchstart', bpDragStart, {passive: false});
            });

            function bpDragStart(e) {
                // Prevent scrolling while dragging
                if(e.type === 'touchstart') e.preventDefault(); 
                if(typeof playTap === 'function') playTap(); // External haptic if available

                const touch = e.type.includes('touch') ? e.touches[0] : e;
                const target = e.currentTarget;

                // Create the element that follows the finger
                activeDragObj = document.createElement('div');
                activeDragObj.className = 'placed-item';
                activeDragObj.innerHTML = target.querySelector('i').outerHTML;
                activeDragObj.dataset.price = target.dataset.price;
                
                // Allow this new item to be dragged again later
                activeDragObj.addEventListener('mousedown', bpMoveExisting);
                activeDragObj.addEventListener('touchstart', bpMoveExisting, {passive: false});

                // Append temporarily to body so it floats above absolutely everything during drag
                document.body.appendChild(activeDragObj);
                
                // Center on finger
                activeDragObj.style.left = touch.pageX + 'px';
                activeDragObj.style.top = touch.pageY + 'px';

                isNewSpawn = true;
            }

            // Function for when an item ALREADY on the canvas is clicked
            function bpMoveExisting(e) {
                if(e.type === 'touchstart') e.preventDefault();
                if(typeof playTap === 'function') playTap();
                
                activeDragObj = e.currentTarget;
                isNewSpawn = false;

                // Move from canvas back to body temporarily for unbounded drag
                const rect = activeDragObj.getBoundingClientRect();
                activeDragObj.style.left = rect.left + (rect.width/2) + 'px';
                activeDragObj.style.top = rect.top + (rect.height/2) + 'px';
                document.body.appendChild(activeDragObj);
            }

            // Global Move Event
            document.addEventListener('mousemove', bpDragMove);
            document.addEventListener('touchmove', bpDragMove, {passive: false});

            function bpDragMove(e) {
                if (!activeDragObj) return;
                e.preventDefault(); // Stop screen scroll
                
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                
                // Follow finger
                activeDragObj.style.left = touch.pageX + 'px';
                activeDragObj.style.top = touch.pageY + 'px';

                // Check if hovering over trash can (Collision Detection)
                const trashRect = bpTrash.getBoundingClientRect();
                if (
                    touch.clientX > trashRect.left && touch.clientX < trashRect.right &&
                    touch.clientY > trashRect.top && touch.clientY < trashRect.bottom
                ) {
                    bpTrash.classList.add('active-trash');
                } else {
                    bpTrash.classList.remove('active-trash');
                }
            }

            // Global End Event
            document.addEventListener('mouseup', bpDragEnd);
            document.addEventListener('touchend', bpDragEnd);

            function bpDragEnd(e) {
                if (!activeDragObj) return;

                const touch = e.type.includes('touch') ? e.changedTouches[0] : e;
                const canvasRect = bpCanvas.getBoundingClientRect();
                const trashRect = bpTrash.getBoundingClientRect();

                // 1. Check if dropped in TRASH
                if (
                    touch.clientX > trashRect.left && touch.clientX < trashRect.right &&
                    touch.clientY > trashRect.top && touch.clientY < trashRect.bottom
                ) {
                    // Destroy item
                    if(!isNewSpawn) {
                        // If it was an existing item, deduct price
                        currentBlueprintTotal -= parseInt(activeDragObj.dataset.price);
                        updateBpBudget();
                    }
                    activeDragObj.remove();
                    bpTrash.classList.remove('active-trash');
                    if(navigator.vibrate) navigator.vibrate(50);
                    activeDragObj = null;
                    return;
                }

                // 2. Check if dropped inside CANVAS bounds
                if (
                    touch.clientX > canvasRect.left && touch.clientX < canvasRect.right &&
                    touch.clientY > canvasRect.top && touch.clientY < canvasRect.bottom
                ) {
                    // Calculate position relative to the canvas itself
                    // We use clientX/Y (viewport) minus canvas bounding box
                    // Snap to grid (Optional math: round to nearest 25px)
                    let newX = touch.clientX - canvasRect.left;
                    let newY = touch.clientY - canvasRect.top;

                    // Append into canvas
                    bpCanvas.appendChild(activeDragObj);
                    activeDragObj.style.left = newX + 'px';
                    activeDragObj.style.top = newY + 'px';

                    // If it was a new spawn, ADD to budget
                    if(isNewSpawn) {
                        currentBlueprintTotal += parseInt(activeDragObj.dataset.price);
                        updateBpBudget();
                        if(navigator.vibrate) navigator.vibrate(20);
                    }
                } else {
                    // Dropped completely outside, destroy it
                    if(!isNewSpawn) {
                        // Deduct if it was dragged off canvas
                        currentBlueprintTotal -= parseInt(activeDragObj.dataset.price);
                        updateBpBudget();
                    }
                    activeDragObj.remove();
                }

                activeDragObj = null;
            }

            function updateBpBudget() {
                // Re-use the animateValue function from Part 2 if available, else simple update
                if(typeof animateValue === 'function') {
                    animateValue('blueprintBudget', currentBlueprintTotal, 300);
                } else {
                    budgetDisplay.innerText = `₹${currentBlueprintTotal.toLocaleString('en-IN')}`;
                }
            }

            function clearBlueprint() {
                if(typeof triggerToast === 'function') triggerToast("Blueprint Erased.");
                const items = bpCanvas.querySelectorAll('.placed-item');
                items.forEach(item => {
                    item.style.transform = 'translate(-50%, -50%) scale(0)';
                    setTimeout(()=> item.remove(), 300); // Wait for shrink animation
                });
                currentBlueprintTotal = 0;
                updateBpBudget();
            }

            // --- 2. 3D HOLOGRAPHIC CAROUSEL MATH ENGINE ---
            const carousel = document.getElementById('holoCarousel');
            const panels = document.querySelectorAll('.holo-panel');
            const numPanels = panels.length; // Currently 6
            const thetaHolo = 360 / numPanels; // 60 degrees per panel
            
            // Radius formula: r = (width / 2) / tan(PI / n)
            // Panel width is 220px in CSS
            const radiusHolo = Math.round((220 / 2) / Math.tan(Math.PI / numPanels));
            
            let currHoloIndex = 0;
            let holoAutoTimer = null;

            // Position each panel in 3D space permanently
            function setupHolo() {
                panels.forEach((panel, i) => {
                    const angle = thetaHolo * i;
                    panel.style.transform = `rotateY(${angle}deg) translateZ(${radiusHolo}px)`;
                });
                updateHoloView();
                startHoloAuto();
            }

            function updateHoloView() {
                // Rotate the entire container in the opposite direction
                const angle = thetaHolo * currHoloIndex * -1;
                carousel.style.transform = `translateZ(${-radiusHolo}px) rotateY(${angle}deg)`;
            }

            function rotateHolo(direction) {
                currHoloIndex += direction;
                updateHoloView();
                if(navigator.vibrate) navigator.vibrate(15);
                
                // Reset auto-timer if user interacts
                if(holoAutoTimer) {
                    clearInterval(holoAutoTimer);
                    startHoloAuto();
                }
            }

            function startHoloAuto() {
                holoAutoTimer = setInterval(() => {
                    currHoloIndex++;
                    updateHoloView();
                }, 3000);
                document.getElementById('btnHoloAuto').innerHTML = '<i class="fas fa-pause"></i>';
            }

            function toggleHoloAuto() {
                if(holoAutoTimer) {
                    clearInterval(holoAutoTimer);
                    holoAutoTimer = null;
                    document.getElementById('btnHoloAuto').innerHTML = '<i class="fas fa-play"></i>';
                    if(typeof triggerToast === 'function') triggerToast("Hologram Rotation Paused");
                } else {
                    startHoloAuto();
                }
            }

            // 3D Touch/Swipe Support
            let hStartX = 0;
            let hDragging = false;

            carousel.addEventListener('touchstart', (e) => {
                hDragging = true;
                hStartX = e.touches[0].clientX;
                clearInterval(holoAutoTimer); // Stop auto rotate while dragging
                carousel.style.transition = 'none'; // Instant follow finger
            }, {passive: true});

            carousel.addEventListener('touchmove', (e) => {
                if(!hDragging) return;
                const deltaX = e.touches[0].clientX - hStartX;
                const baseAngle = thetaHolo * currHoloIndex * -1;
                // Add fraction of drag to rotation
                const dragAngle = baseAngle + (deltaX * 0.4); 
                carousel.style.transform = `translateZ(${-radiusHolo}px) rotateY(${dragAngle}deg)`;
            }, {passive: true});

            carousel.addEventListener('touchend', (e) => {
                if(!hDragging) return;
                hDragging = false;
                carousel.style.transition = 'transform 0.6s cubic-bezier(0.25, 1, 0.5, 1)';
                
                const deltaX = e.changedTouches[0].clientX - hStartX;
                // Snap to next/prev face if dragged far enough
                if(deltaX > 50) currHoloIndex--;
                else if (deltaX < -50) currHoloIndex++;
                
                updateHoloView();
                // Resume auto if it wasn't paused manually
                if(document.getElementById('btnHoloAuto').innerHTML.includes('pause')) {
                    startHoloAuto();
                }
            });

            // Initialize 3D Engine on load
            setTimeout(setupHolo, 500);

        </script>
        <style>
            .vibe-grid {
                display: grid;
                grid-template-columns: repeat(2, 1fr);
                gap: 15px;
            }
            .vibe-card {
                background: rgba(0,0,0,0.4);
                border: 2px solid transparent;
                border-radius: 12px;
                padding: 20px 10px;
                text-align: center;
                cursor: pointer;
                transition: 0.3s cubic-bezier(0.25, 1, 0.5, 1);
                position: relative;
                overflow: hidden;
            }
            .vibe-card i { font-size: 28px; margin-bottom: 10px; transition: 0.3s; }
            .vibe-card span { display: block; font-family: var(--font-data); font-weight: 800; font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: #fff; }
            .vibe-card:active { transform: scale(0.95); }

            /* Default Vibe Colors for Cards */
            .vc-royal i { color: #D4AF37; }
            .vc-neon i { color: #b829ff; }
            .vc-bass i { color: #ff3333; }
            .vc-corp i { color: #00e5ff; }

            .vibe-card.active { box-shadow: inset 0 0 20px currentColor; border-color: currentColor; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">SYSTEM VIBE OVERRIDE</h2>
                <div class="section-icon"><i class="fas fa-heartbeat"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Select an aesthetic protocol to shift the entire OS interface.</p>
            
            <div class="vibe-grid">
                <div class="vibe-card vc-royal active" style="color: #D4AF37;" onclick="applyVibe('royal', this)">
                    <i class="fas fa-chess-king"></i><span>Royal Wedding</span>
                </div>
                <div class="vibe-card vc-neon" style="color: #b829ff;" onclick="applyVibe('neon', this)">
                    <i class="fas fa-compact-disc"></i><span>Neon Club</span>
                </div>
                <div class="vibe-card vc-bass" style="color: #ff3333;" onclick="applyVibe('bass', this)">
                    <i class="fas fa-fire"></i><span>Baaraat Bass</span>
                </div>
                <div class="vibe-card vc-corp" style="color: #00e5ff;" onclick="applyVibe('corp', this)">
                    <i class="fas fa-briefcase"></i><span>Corporate Elite</span>
                </div>
            </div>
        </div>

        <style>
            .dmx-virtual-stage {
                width: 100%;
                height: 220px;
                background: #000;
                border-radius: 12px;
                border: 2px solid #222;
                position: relative;
                overflow: hidden;
                perspective: 800px;
                box-shadow: inset 0 0 50px rgba(0,0,0,1);
                margin-bottom: 20px;
            }
            
            .dmx-stage-wall {
                position: absolute;
                inset: 0;
                /* Dynamic background driven by CSS variables from JS */
                background: radial-gradient(circle at center, rgb(var(--dmx-r, 0), var(--dmx-g, 229), var(--dmx-b, 255)) 0%, #000 80%);
                opacity: var(--dmx-intensity, 0.8);
                transition: opacity 0.1s;
                z-index: 1;
            }

            .dmx-beam-container {
                position: absolute;
                bottom: -20px;
                left: 50%;
                width: 100%;
                display: flex;
                justify-content: space-around;
                transform: translateX(-50%);
                z-index: 2;
                transform-style: preserve-3d;
            }
            
            .dmx-beam {
                width: 50px;
                height: 300px;
                background: linear-gradient(to top, rgba(var(--dmx-r, 0), var(--dmx-g, 229), var(--dmx-b, 255), 0.9), transparent);
                clip-path: polygon(40% 100%, 60% 100%, 100% 0, 0 0);
                transform-origin: bottom center;
                /* Dynamic Pan and Tilt driven by CSS variables */
                transform: rotateZ(var(--dmx-pan, 0deg)) rotateX(var(--dmx-tilt, 45deg));
                filter: blur(2px);
                mix-blend-mode: screen;
                opacity: var(--dmx-intensity, 0.8);
            }

            .dmx-fader-board {
                display: flex;
                justify-content: space-between;
                background: #050505;
                padding: 15px 10px;
                border-radius: 12px;
                border: 1px solid #222;
                overflow-x: auto;
                scrollbar-width: none;
            }
            
            .fader-channel {
                display: flex;
                flex-direction: column;
                align-items: center;
                min-width: 40px;
                gap: 15px;
            }
            .fader-lbl { font-family: var(--font-tech); font-size: 9px; font-weight: 900; text-transform: uppercase; }
            .fader-val { font-family: var(--font-data); font-size: 10px; color: #fff; background: #000; padding: 2px 5px; border: 1px solid #333; border-radius: 3px; width: 35px; text-align: center; }

            /* Vertical Slider Hack */
            .fader-input {
                -webkit-appearance: none;
                width: 100px; 
                height: 6px; 
                background: #111;
                border: 1px solid #222;
                border-radius: 3px;
                outline: none;
                transform: rotate(-90deg); 
                margin: 45px 0; 
                box-shadow: inset 0 2px 5px rgba(0,0,0,1);
            }
            .fader-input::-webkit-slider-thumb {
                -webkit-appearance: none;
                appearance: none;
                width: 18px;
                height: 30px;
                background: linear-gradient(90deg, #444, #222);
                border: 2px solid #555;
                border-radius: 4px;
                cursor: grab;
                box-shadow: -2px 0 5px rgba(0,0,0,0.8);
            }
            .fader-input::-webkit-slider-thumb:active { background: linear-gradient(90deg, #666, #333); }
            
            /* Custom Fader Colors */
            .f-red::-webkit-slider-thumb { border-color: #ff3333; box-shadow: 0 0 10px rgba(255,51,51,0.5); }
            .f-grn::-webkit-slider-thumb { border-color: #00ff00; box-shadow: 0 0 10px rgba(0,255,0,0.5); }
            .f-blu::-webkit-slider-thumb { border-color: #00e5ff; box-shadow: 0 0 10px rgba(0,229,255,0.5); }
        </style>

        <div class="app-section" id="dmxConsoleEnv">
            <div class="section-header">
                <h2 class="section-title">DMX LIGHTING MATRIX</h2>
                <div class="section-icon"><i class="fas fa-lightbulb"></i></div>
            </div>

            <div class="dmx-virtual-stage">
                <div class="dmx-stage-wall"></div>
                <div class="dmx-beam-container">
                    <div class="dmx-beam" style="--dmx-pan: calc(var(--base-pan, 0deg) - 25deg);"></div>
                    <div class="dmx-beam" style="--dmx-pan: calc(var(--base-pan, 0deg) - 10deg);"></div>
                    <div class="dmx-beam" style="--dmx-pan: calc(var(--base-pan, 0deg) + 10deg);"></div>
                    <div class="dmx-beam" style="--dmx-pan: calc(var(--base-pan, 0deg) + 25deg);"></div>
                </div>
                <div style="position:absolute; top:10px; left:10px; color:#fff; font-family:var(--font-tech); font-size:9px; opacity:0.5;">CH: 01-05 // MODE: MANUAL</div>
            </div>

            <div class="dmx-fader-board">
                <div class="fader-channel">
                    <span class="fader-lbl" style="color:#ff3333;">RED</span>
                    <input type="range" class="fader-input f-red" min="0" max="255" value="0" oninput="updateDMX('r', this.value)">
                    <span class="fader-val" id="dmx-val-r">0</span>
                </div>
                <div class="fader-channel">
                    <span class="fader-lbl" style="color:#00ff00;">GRN</span>
                    <input type="range" class="fader-input f-grn" min="0" max="255" value="229" oninput="updateDMX('g', this.value)">
                    <span class="fader-val" id="dmx-val-g">229</span>
                </div>
                <div class="fader-channel">
                    <span class="fader-lbl" style="color:#00e5ff;">BLU</span>
                    <input type="range" class="fader-input f-blu" min="0" max="255" value="255" oninput="updateDMX('b', this.value)">
                    <span class="fader-val" id="dmx-val-b">255</span>
                </div>
                <div style="width: 1px; background: #333; margin: 0 5px;"></div>
                <div class="fader-channel">
                    <span class="fader-lbl" style="color:#888;">PAN</span>
                    <input type="range" class="fader-input" min="-60" max="60" value="0" oninput="updateDMX('pan', this.value)">
                    <span class="fader-val" id="dmx-val-pan">0</span>
                </div>
                <div class="fader-channel">
                    <span class="fader-lbl" style="color:#888;">TILT</span>
                    <input type="range" class="fader-input" min="0" max="80" value="45" oninput="updateDMX('tilt', this.value)">
                    <span class="fader-val" id="dmx-val-tilt">45</span>
                </div>
                <div class="fader-channel">
                    <span class="fader-lbl" style="color:#fff;">INTEN</span>
                    <input type="range" class="fader-input" min="0" max="100" value="80" oninput="updateDMX('intensity', this.value)">
                    <span class="fader-val" id="dmx-val-intensity">80</span>
                </div>
            </div>
            
            <button class="app-btn-outline" style="margin-top: 15px; width: 100%;" onclick="toggleStrobe()" id="btnStrobe">
                <i class="fas fa-bolt"></i> ENGAGE STROBE
            </button>
        </div>

        <style>
            .topo-canvas-container {
                width: 100%;
                height: 280px;
                background: #000;
                border: 2px solid var(--gold-primary);
                border-radius: 12px;
                position: relative;
                overflow: hidden;
                /* Prevent scrolling while tapping canvas */
                touch-action: none; 
            }

            #topoCanvas {
                width: 100%; height: 100%; display: block; z-index: 2; position: relative;
                mix-blend-mode: screen; /* Crucial for heatmap overlapping effect */
            }

            /* Blueprint Grid beneath heatmap */
            .topo-grid {
                position: absolute; inset: 0;
                background-image: 
                    linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px);
                background-size: 20px 20px; z-index: 1; pointer-events: none;
            }

            .topo-legend {
                display: flex; align-items: center; gap: 15px; margin-top: 15px;
                background: rgba(0,0,0,0.5); padding: 10px; border-radius: 8px; border: 1px solid #222;
            }
            .legend-bar { flex-grow: 1; height: 8px; border-radius: 4px; background: linear-gradient(90deg, #00e5ff, #00ff00, #ffff00, #ff3333); }
            .legend-text { color: #888; font-family: var(--font-data); font-size: 10px; font-weight: bold; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">ACOUSTIC TOPOGRAPHY</h2>
                <div class="section-icon"><i class="fas fa-wave-square"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Tap the blueprint to deploy virtual subwoofers and simulate SPL coverage.</p>

            <div class="topo-canvas-container" id="topoWrap">
                <div class="topo-grid"></div>
                <canvas id="topoCanvas"></canvas>
                <div style="position: absolute; top:10px; left:10px; color:#fff; font-family:var(--font-tech); font-size:9px; z-index:10; pointer-events:none;">SPL HEATMAP // LIVE</div>
            </div>

            <div class="topo-legend">
                <span class="legend-text">LOW DB</span>
                <div class="legend-bar"></div>
                <span class="legend-text">MAX DB</span>
            </div>

            <div style="display: flex; gap: 10px; margin-top: 15px;">
                <button class="app-btn-outline" style="flex: 1;" onclick="clearTopo()">
                    <i class="fas fa-eraser"></i> CLEAR
                </button>
                <button class="app-btn-primary" style="flex: 2; background: linear-gradient(135deg, #ff3333, #990000); color: #fff;" onclick="simulateBassHit()">
                    <i class="fas fa-bomb"></i> BASS DROP
                </button>
            </div>
        </div>

        <script>
            // --- 1. GLOBAL VIBE MATCHER LOGIC ---
            function applyVibe(vibeId, element) {
                if(typeof triggerToast === 'function') triggerToast("System Protocol Updated.");
                if(navigator.vibrate) navigator.vibrate(20);

                // Update UI selection
                document.querySelectorAll('.vibe-card').forEach(c => c.classList.remove('active'));
                element.classList.add('active');

                // The Root element where CSS variables live
                const root = document.documentElement;

                switch(vibeId) {
                    case 'royal':
                        root.style.setProperty('--gold-primary', '#D4AF37');
                        root.style.setProperty('--gold-glow', '#FFDF00');
                        root.style.setProperty('--cyan-neon', '#00e5ff');
                        root.style.setProperty('--app-bg', '#030305');
                        break;
                    case 'neon':
                        root.style.setProperty('--gold-primary', '#b829ff'); // Override gold with purple
                        root.style.setProperty('--gold-glow', '#ff00ff');
                        root.style.setProperty('--cyan-neon', '#00e5ff');
                        root.style.setProperty('--app-bg', '#050010');
                        break;
                    case 'bass':
                        root.style.setProperty('--gold-primary', '#ff3333'); // Override with aggressive red
                        root.style.setProperty('--gold-glow', '#ff6666');
                        root.style.setProperty('--cyan-neon', '#ffcc00');
                        root.style.setProperty('--app-bg', '#100000');
                        break;
                    case 'corp':
                        root.style.setProperty('--gold-primary', '#ffffff'); // Clean white/blue
                        root.style.setProperty('--gold-glow', '#cccccc');
                        root.style.setProperty('--cyan-neon', '#0055ff');
                        root.style.setProperty('--app-bg', '#000510');
                        break;
                }
            }

            // --- 2. DMX LIGHTING CONSOLE LOGIC ---
            let strobeInterval = null;
            let dmxIsOn = true;

            function updateDMX(channel, val) {
                const env = document.getElementById('dmxConsoleEnv');
                document.getElementById(`dmx-val-${channel}`).innerText = val;
                
                // Update CSS Custom Properties that drive the stage colors and transforms
                if(['r', 'g', 'b'].includes(channel)) {
                    env.style.setProperty(`--dmx-${channel}`, val);
                } else if (channel === 'pan') {
                    env.style.setProperty('--base-pan', `${val}deg`);
                } else if (channel === 'tilt') {
                    env.style.setProperty('--dmx-tilt', `${val}deg`);
                } else if (channel === 'intensity') {
                    env.style.setProperty('--dmx-intensity', val / 100);
                }
            }

            function toggleStrobe() {
                if(typeof triggerToast === 'function') triggerToast("Strobe Override Engaged.");
                if(navigator.vibrate) navigator.vibrate(30);
                
                const env = document.getElementById('dmxConsoleEnv');
                const btn = document.getElementById('btnStrobe');
                
                if(strobeInterval) {
                    // Turn off
                    clearInterval(strobeInterval);
                    strobeInterval = null;
                    const inten = document.querySelector('.f-input[oninput*="intensity"]');
                    const val = inten ? inten.value : 80;
                    env.style.setProperty('--dmx-intensity', val / 100);
                    btn.innerHTML = '<i class="fas fa-bolt"></i> ENGAGE STROBE';
                    btn.style.color = "var(--cyan-neon)";
                    btn.style.borderColor = "var(--cyan-neon)";
                } else {
                    // Turn on rapid flicker
                    btn.innerHTML = '<i class="fas fa-stop"></i> HALT STROBE';
                    btn.style.color = "var(--red-alert)";
                    btn.style.borderColor = "var(--red-alert)";
                    
                    strobeInterval = setInterval(() => {
                        dmxIsOn = !dmxIsOn;
                        env.style.setProperty('--dmx-intensity', dmxIsOn ? '1' : '0');
                    }, 50); // 50ms pulse
                }
            }

            // --- 3. ACOUSTIC TOPOGRAPHY HEATMAP LOGIC ---
            const topoCanvas = document.getElementById('topoCanvas');
            const topoWrap = document.getElementById('topoWrap');
            let tCtx = null;
            let subwoofers = []; // Array to store placed speakers
            let topoAnimFrame = null;
            let topoPhase = 0; // For pulse animation

            function initTopo() {
                // Set true internal resolution
                topoCanvas.width = topoWrap.clientWidth;
                topoCanvas.height = topoWrap.clientHeight;
                tCtx = topoCanvas.getContext('2d');
            }
            window.addEventListener('resize', initTopo);
            setTimeout(initTopo, 500);

            // Handle Tap to Place Subwoofer
            topoCanvas.addEventListener('mousedown', placeSub);
            topoCanvas.addEventListener('touchstart', (e) => { e.preventDefault(); placeSub(e); }, {passive: false});

            function placeSub(e) {
                if(typeof triggerToast === 'function') triggerToast("Subwoofer Deployed.");
                if(navigator.vibrate) navigator.vibrate(20);

                const rect = topoCanvas.getBoundingClientRect();
                const clientX = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                const clientY = e.type.includes('touch') ? e.touches[0].clientY : e.clientY;

                const x = clientX - rect.left;
                const y = clientY - rect.top;
                
                // Add to array with base power
                subwoofers.push({x: x, y: y, power: 80}); 
                
                if(!topoAnimFrame) animateTopo();
            }

            function clearTopo() {
                if(typeof triggerToast === 'function') triggerToast("Topography Cleared.");
                subwoofers = [];
                if(tCtx) tCtx.clearRect(0, 0, topoCanvas.width, topoCanvas.height);
                if(topoAnimFrame) { cancelAnimationFrame(topoAnimFrame); topoAnimFrame = null; }
            }

            function simulateBassHit() {
                if(subwoofers.length === 0) {
                    if(typeof triggerToast === 'function') triggerToast("Deploy a subwoofer first.");
                    return;
                }
                
                if(typeof triggerToast === 'function') triggerToast("Maximum Excursion Reached.");
                if(navigator.vibrate) navigator.vibrate([100, 50, 200]);
                
                // Temporarily boost power massively
                subwoofers.forEach(sub => sub.power = 200);
                
                // Screen shake effect on canvas wrapper
                topoWrap.style.transform = 'translate(5px, 5px)';
                setTimeout(()=> topoWrap.style.transform = 'translate(-5px, -5px)', 50);
                setTimeout(()=> topoWrap.style.transform = 'translate(0, 0)', 100);

                // If audio engine from Part 3 is running, trigger a bass drop sound
                if(typeof playSynth === 'function') playSynth('subDrop', null);

                // Recover to normal power slowly
                setTimeout(() => {
                    subwoofers.forEach(sub => sub.power = 80);
                }, 500);
                
                if(!topoAnimFrame) animateTopo();
            }

            function animateTopo() {
                if(subwoofers.length === 0) return;
                topoAnimFrame = requestAnimationFrame(animateTopo);
                
                // Clear with black for clean additive blending
                tCtx.fillStyle = '#000';
                tCtx.fillRect(0, 0, topoCanvas.width, topoCanvas.height);
                
                // Lighter blending means overlapping areas get brighter/hotter
                tCtx.globalCompositeOperation = 'lighter';
                
                topoPhase += 0.1; // Pulse speed

                subwoofers.forEach(sub => {
                    // Radius pulses slightly using sine wave
                    const currentRadius = sub.power + (Math.sin(topoPhase) * 10);
                    
                    if(currentRadius > 0) {
                        const gradient = tCtx.createRadialGradient(sub.x, sub.y, 0, sub.x, sub.y, currentRadius);
                        
                        // Thermal mapping: Center Red -> Yellow -> Green -> Blue edges
                        gradient.addColorStop(0, 'rgba(255, 0, 0, 1)');      // Center
                        gradient.addColorStop(0.3, 'rgba(255, 255, 0, 0.8)');// Mid
                        gradient.addColorStop(0.6, 'rgba(0, 255, 0, 0.5)');  // Far
                        gradient.addColorStop(1, 'rgba(0, 0, 255, 0)');      // Edge
                        
                        tCtx.fillStyle = gradient;
                        tCtx.beginPath();
                        tCtx.arc(sub.x, sub.y, currentRadius, 0, Math.PI * 2);
                        tCtx.fill();
                        
                        // Draw physical box icon
                        tCtx.globalCompositeOperation = 'source-over';
                        tCtx.fillStyle = '#fff';
                        tCtx.fillRect(sub.x - 4, sub.y - 4, 8, 8);
                        tCtx.globalCompositeOperation = 'lighter';
                    }
                });
                tCtx.globalCompositeOperation = 'source-over';
            }
        </script>
        <style>
            .phase-aligner-wrapper {
                background: #02050a;
                border: 2px solid #112233;
                border-radius: 16px;
                padding: 20px;
                box-shadow: 0 15px 35px rgba(0,0,0,0.8), inset 0 0 40px rgba(0, 229, 255, 0.05);
            }

            .oscilloscope-screen {
                width: 100%;
                height: 200px;
                background: #000;
                border: 2px solid #005577;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 30px rgba(0,229,255,0.2);
            }
            
            /* Radar/Oscilloscope Grid */
            .oscilloscope-screen::before {
                content: ''; position: absolute; inset: 0;
                background-image: 
                    linear-gradient(rgba(0, 229, 255, 0.15) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(0, 229, 255, 0.15) 1px, transparent 1px);
                background-size: 20px 20px;
                background-position: center;
                pointer-events: none; z-index: 1;
            }
            /* Center Zero Line */
            .oscilloscope-screen::after {
                content: ''; position: absolute; top: 50%; left: 0; width: 100%; height: 1px;
                background: rgba(0, 229, 255, 0.6); pointer-events: none; z-index: 1;
            }

            #phaseCanvas {
                width: 100%; height: 100%; display: block; position: relative; z-index: 2; mix-blend-mode: screen;
            }

            .phase-hud {
                display: flex; justify-content: space-between; align-items: center; margin-top: 15px;
            }
            .p-stat-box { text-align: center; background: rgba(0,0,0,0.5); padding: 10px; border-radius: 8px; border: 1px solid #222; flex: 1; margin: 0 5px; }
            .p-lbl { font-family: var(--font-data); font-size: 9px; color: #888; text-transform: uppercase; letter-spacing: 1px; display: block; margin-bottom: 5px;}
            .p-val { font-family: var(--font-tech); font-size: 16px; font-weight: 900; }

            .phase-slider-container { margin-top: 20px; text-align: center; }
            
            .phase-verdict {
                margin-top: 15px; padding: 12px; border-radius: 6px; font-family: var(--font-body); font-size: 11px;
                font-weight: bold; text-align: center; transition: 0.3s; border-left: 4px solid transparent;
            }
            .verdict-bad { background: rgba(255,51,51,0.1); color: var(--red-alert); border-color: var(--red-alert); }
            .verdict-good { background: rgba(0,255,0,0.1); color: #00ff00; border-color: #00ff00; text-shadow: 0 0 10px rgba(0,255,0,0.4); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">ACOUSTIC PHASE ALIGNER</h2>
                <div class="section-icon"><i class="fas fa-wave-square"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Tune the Digital Delay (ms) to synchronize Subwoofer B with Subwoofer A. Avoid destructive cancellation.</p>

            <div class="phase-aligner-wrapper">
                <div class="oscilloscope-screen" id="phaseWrap">
                    <div style="position:absolute; top:10px; left:10px; font-family:var(--font-tech); font-size:9px; color:#00e5ff; z-index:5; text-shadow: 0 0 5px #00e5ff;">SUMMATION WAVEFORM</div>
                    <canvas id="phaseCanvas"></canvas>
                </div>

                <div class="phase-hud">
                    <div class="p-stat-box">
                        <span class="p-lbl">SUB A (FIXED)</span>
                        <span class="p-val" style="color:var(--cyan-neon);">0.0ms</span>
                    </div>
                    <div class="p-stat-box">
                        <span class="p-lbl">SUB B (DELAYED)</span>
                        <span class="p-val" id="delayMsVal" style="color:var(--gold-primary);">0.0ms</span>
                    </div>
                    <div class="p-stat-box">
                        <span class="p-lbl">OUTPUT SPL</span>
                        <span class="p-val" id="ampVal" style="color:#fff;">100%</span>
                    </div>
                </div>

                <div class="phase-slider-container">
                    <span style="font-family:var(--font-data); font-size:11px; color:#fff; font-weight:bold; letter-spacing:2px; display:block; margin-bottom:10px;">DIGITAL DELAY ADJUSTMENT</span>
                    <input type="range" class="app-slider" id="phaseSlider" min="0" max="360" value="180" oninput="updatePhase(this.value)">
                </div>

                <div class="phase-verdict verdict-bad" id="phaseVerdict">
                    <i class="fas fa-exclamation-triangle"></i> DESTRUCTIVE INTERFERENCE: BASS CANCELLATION
                </div>
            </div>
        </div>

        <style>
            .crew-dispatch-wrapper {
                background: #050505;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .crew-roster {
                display: flex; gap: 12px; overflow-x: auto; padding-bottom: 10px; scrollbar-width: none;
            }
            .crew-roster::-webkit-scrollbar { display: none; }

            .crew-card {
                flex: 0 0 75px;
                background: linear-gradient(180deg, #1a1a24, #0a0a10); border: 1px solid #333; border-radius: 10px;
                padding: 12px 5px; display: flex; flex-direction: column; align-items: center; gap: 8px;
                cursor: pointer; transition: 0.2s; position: relative;
            }
            .crew-card:active, .crew-card.selected { border-color: var(--gold-primary); background: rgba(212,175,55,0.15); transform: translateY(-3px); box-shadow: 0 5px 15px rgba(212,175,55,0.2); }
            
            .crew-avatar {
                width: 36px; height: 36px; border-radius: 50%; background: #000; border: 2px solid var(--gold-primary);
                display: flex; justify-content: center; align-items: center; font-size: 16px; color: var(--gold-primary);
            }
            .crew-name { font-family: var(--font-data); font-size: 11px; font-weight: bold; color: #fff; text-transform: uppercase; }
            .crew-role { font-family: var(--font-body); font-size: 8px; color: #888; text-align: center; line-height: 1.1; }
            
            .crew-card::after { content:''; position:absolute; top:5px; right:5px; width:6px; height:6px; background:#00ff00; border-radius:50%; box-shadow:0 0 5px #00ff00; }
            .crew-card.assigned::after { background: var(--red-alert); box-shadow: 0 0 5px var(--red-alert); }
            .crew-card.assigned { opacity: 0.4; pointer-events: none; filter: grayscale(1); }

            .task-matrix { margin-top: 20px; display: flex; flex-direction: column; gap: 15px; }

            .task-row {
                background: #0a0a0f; border: 1px solid #222; border-radius: 8px; padding: 15px;
                position: relative; overflow: hidden;
            }
            .task-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px; }
            .task-title { font-family: var(--font-head); font-size: 13px; color: #fff; font-weight: bold; }
            .task-eta { font-family: var(--font-tech); font-size: 12px; color: var(--cyan-neon); font-weight: bold; }
            
            .gantt-bar-bg { width: 100%; height: 6px; background: #111; border-radius: 3px; overflow: hidden; }
            .gantt-bar-fill { height: 100%; width: 100%; background: linear-gradient(90deg, #005588, var(--cyan-neon)); transition: width 0.5s cubic-bezier(0.25, 1, 0.5, 1); }

            .task-dropzone {
                margin-top: 10px; min-height: 35px; border: 1px dashed #444; border-radius: 6px;
                display: flex; align-items: center; padding: 5px; gap: 5px; background: rgba(0,0,0,0.3);
            }
            .task-dropzone.empty::before { content: 'Tap here to assign selected operative'; color: #555; font-family: var(--font-body); font-size: 9px; margin-left: 5px; }

            .assigned-badge {
                background: var(--gold-primary); color: #000; font-family: var(--font-data); font-size: 9px; font-weight: bold;
                padding: 4px 10px; border-radius: 12px; display: flex; align-items: center; gap: 5px; box-shadow: 0 2px 5px rgba(212,175,55,0.4);
            }

            .total-eta-display {
                margin-top: 20px; padding: 20px; background: rgba(0,255,0,0.05); border: 1px solid #00ff00; border-radius: 10px;
                text-align: center; box-shadow: inset 0 0 20px rgba(0,255,0,0.05);
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">TACTICAL DISPATCH MATRIX</h2>
                <div class="section-icon"><i class="fas fa-users-cog"></i></div>
            </div>
            
            <div class="crew-dispatch-wrapper">
                <span style="font-family:var(--font-tech); font-size:9px; color:var(--gold-primary); letter-spacing:1px; margin-bottom:10px; display:block;">1. SELECT OPERATIVE</span>
                
                <div class="crew-roster">
                    <div class="crew-card" onclick="selectOperative('lalu', this)" data-id="lalu" data-skill="sound">
                        <div class="crew-avatar"><i class="fas fa-headphones"></i></div>
                        <span class="crew-name">Lalu</span><span class="crew-role">Audio Engineer</span>
                    </div>
                    <div class="crew-card" onclick="selectOperative('sildhar', this)" data-id="sildhar" data-skill="light">
                        <div class="crew-avatar"><i class="fas fa-lightbulb"></i></div>
                        <span class="crew-name">Sildhar</span><span class="crew-role">DMX Master</span>
                    </div>
                    <div class="crew-card" onclick="selectOperative('sanjay', this)" data-id="sanjay" data-skill="tent">
                        <div class="crew-avatar"><i class="fas fa-campground"></i></div>
                        <span class="crew-name">Sanjay</span><span class="crew-role">Rigging Lead</span>
                    </div>
                    <div class="crew-card" onclick="selectOperative('anil', this)" data-id="anil" data-skill="power">
                        <div class="crew-avatar"><i class="fas fa-bolt"></i></div>
                        <span class="crew-name">Anil</span><span class="crew-role">Power & Fleet</span>
                    </div>
                </div>

                <span style="font-family:var(--font-tech); font-size:9px; color:var(--gold-primary); letter-spacing:1px; margin-top:20px; margin-bottom:10px; display:block;">2. ASSIGN TO DEPLOYMENT PHASE</span>
                
                <div class="task-matrix">
                    <div class="task-row" onclick="assignOperative('tent')">
                        <div class="task-header">
                            <span class="task-title">Structural Pandal Rigging</span>
                            <span class="task-eta" id="eta-tent">8.0 Hrs</span>
                        </div>
                        <div class="gantt-bar-bg"><div class="gantt-bar-fill" id="bar-tent" style="width: 100%;"></div></div>
                        <div class="task-dropzone empty" id="zone-tent"></div>
                    </div>
                    <div class="task-row" onclick="assignOperative('sound')">
                        <div class="task-header">
                            <span class="task-title">Line-Array Deployment</span>
                            <span class="task-eta" id="eta-sound">5.0 Hrs</span>
                        </div>
                        <div class="gantt-bar-bg"><div class="gantt-bar-fill" id="bar-sound" style="width: 100%;"></div></div>
                        <div class="task-dropzone empty" id="zone-sound"></div>
                    </div>
                    <div class="task-row" onclick="assignOperative('light')">
                        <div class="task-header">
                            <span class="task-title">Laser Matrix Calibration</span>
                            <span class="task-eta" id="eta-light">4.0 Hrs</span>
                        </div>
                        <div class="gantt-bar-bg"><div class="gantt-bar-fill" id="bar-light" style="width: 100%;"></div></div>
                        <div class="task-dropzone empty" id="zone-light"></div>
                    </div>
                </div>

                <div class="total-eta-display">
                    <span style="font-family:var(--font-data); font-size:11px; color:#aaa; font-weight:bold; letter-spacing:1px;">ESTIMATED SYSTEM READINESS</span>
                    <div style="font-family:var(--font-tech); font-size:32px; color:#00ff00; font-weight:900; margin:5px 0; text-shadow:0 0 15px rgba(0,255,0,0.5);" id="masterEtaVal">17.0 HRS</div>
                    <button class="app-btn-primary" style="margin-top:10px;" onclick="triggerToast('Logistics Data synced with Beltikri HQ.')">
                        <i class="fas fa-satellite-transmit"></i> LOCK LOGISTICS PLAN
                    </button>
                </div>
            </div>
        </div>

        <style>
            .poster-builder-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .poster-canvas-box {
                width: 100%;
                aspect-ratio: 4 / 5; /* Standard Instagram Portrait size */
                background: #111;
                border: 2px solid var(--gold-primary);
                border-radius: 8px;
                margin-bottom: 20px;
                position: relative;
                overflow: hidden;
                box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            }
            #posterCanvas { width: 100%; height: 100%; display: block; }
            
            .poster-inputs { display: flex; flex-direction: column; gap: 12px; }
            
            .p-input-field {
                width: 100%; background: #111; border: 1px solid #333; border-radius: 6px;
                padding: 12px; color: #fff; font-family: var(--font-body); font-size: 13px;
                outline: none; transition: 0.2s;
            }
            .p-input-field:focus { border-color: var(--cyan-neon); box-shadow: inset 0 0 10px rgba(0,229,255,0.1); }
            
            .poster-theme-row { display: flex; gap: 10px; margin-top: 5px; }
            .p-theme-btn {
                flex: 1; padding: 10px 0; text-align: center; font-family: var(--font-data); font-size: 11px;
                font-weight: bold; background: #0a0a0f; border: 1px solid #333; border-radius: 6px; cursor: pointer; color: #888;
            }
            .p-theme-btn.active { background: var(--gold-primary); color: #000; border-color: var(--gold-primary); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">GENERATIVE POSTER AI</h2>
                <div class="section-icon"><i class="fas fa-paint-brush"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Generate and download a high-resolution MND event invitation.</p>

            <div class="poster-builder-wrapper">
                <div class="poster-canvas-box">
                    <canvas id="posterCanvas" width="800" height="1000"></canvas>
                </div>

                <div class="poster-inputs">
                    <input type="text" class="p-input-field" id="postTitle" placeholder="Main Event Title (e.g. Rahul Weds Anjali)" value="The Grand Celebration" oninput="renderPoster()">
                    <input type="text" class="p-input-field" id="postSub" placeholder="Subtitle" value="Powered by MND Sound" oninput="renderPoster()">
                    <div style="display: flex; gap: 10px;">
                        <input type="date" class="p-input-field" id="postDate" onchange="renderPoster()" style="color:#aaa;">
                        <input type="text" class="p-input-field" id="postLoc" placeholder="Location" value="Beltikri" oninput="renderPoster()">
                    </div>
                    
                    <span style="font-family:var(--font-data); font-size:10px; color:#888; margin-top:10px; display:block;">SELECT AESTHETIC</span>
                    <div class="poster-theme-row">
                        <div class="p-theme-btn active" onclick="setPosterTheme('royal', this)">ROYAL GOLD</div>
                        <div class="p-theme-btn" onclick="setPosterTheme('neon', this)">CYBER NEON</div>
                        <div class="p-theme-btn" onclick="setPosterTheme('dark', this)">MINIMAL</div>
                    </div>

                    <button class="app-btn-outline" style="margin-top: 15px; border-color: var(--gold-primary); color: var(--gold-primary);" onclick="downloadPoster()">
                        <i class="fas fa-download"></i> SAVE HIGH-RES POSTER
                    </button>
                </div>
            </div>
        </div>

        <script>
            // --- 1. ACOUSTIC PHASE ALIGNER LOGIC ---
            const phCanvas = document.getElementById('phaseCanvas');
            const phWrap = document.getElementById('phaseWrap');
            let phCtx = null;
            let phAnimFrame = null;
            let phaseOffsetDeg = 180; // 180 degrees out of phase initially (destructive)
            let phaseTime = 0;

            function initPhaseAligner() {
                phCanvas.width = phWrap.clientWidth;
                phCanvas.height = phWrap.clientHeight;
                phCtx = phCanvas.getContext('2d');
                animatePhase();
            }
            window.addEventListener('resize', () => {
                if(phWrap) { phCanvas.width = phWrap.clientWidth; phCanvas.height = phWrap.clientHeight; }
            });

            function updatePhase(val) {
                phaseOffsetDeg = parseInt(val);
                
                // Map 0-360 degrees to roughly 0-20ms of digital delay
                const delayMs = ((phaseOffsetDeg / 360) * 20).toFixed(1);
                document.getElementById('delayMsVal').innerText = `${delayMs}ms`;
            }

            function animatePhase() {
                phAnimFrame = requestAnimationFrame(animatePhase);
                
                // Slight fade for oscilloscope tail effect
                phCtx.fillStyle = 'rgba(0, 0, 0, 0.4)';
                phCtx.fillRect(0, 0, phCanvas.width, phCanvas.height);

                phaseTime += 0.05; // Speed of the wave
                
                const w = phCanvas.width;
                const h = phCanvas.height;
                const midY = h / 2;
                const amplitude = h * 0.2; // Height of individual waves
                const freq = 0.03; // Number of waves on screen

                phCtx.lineWidth = 2;

                // 1. Draw Sub A (Fixed Reference Wave) - Cyan
                phCtx.beginPath();
                phCtx.strokeStyle = 'rgba(0, 229, 255, 0.4)';
                for(let x=0; x<w; x+=3) {
                    const y = midY + Math.sin(x * freq + phaseTime) * amplitude;
                    if(x===0) phCtx.moveTo(x,y); else phCtx.lineTo(x,y);
                }
                phCtx.stroke();

                // 2. Draw Sub B (Delayed/Phase Shifted Wave) - Gold
                const offsetRad = phaseOffsetDeg * (Math.PI / 180); // Convert deg to radians
                phCtx.beginPath();
                phCtx.strokeStyle = 'rgba(212, 175, 55, 0.4)';
                for(let x=0; x<w; x+=3) {
                    const y = midY + Math.sin(x * freq + phaseTime + offsetRad) * amplitude;
                    if(x===0) phCtx.moveTo(x,y); else phCtx.lineTo(x,y);
                }
                phCtx.stroke();

                // 3. Draw SUMMATION WAVE (The actual physical sound produced) - White
                phCtx.beginPath();
                phCtx.lineWidth = 3;
                phCtx.strokeStyle = '#fff';
                phCtx.shadowBlur = 10;
                phCtx.shadowColor = '#fff';
                
                let maxSumAmplitude = 0;
                
                for(let x=0; x<w; x+=3) {
                    const y1 = Math.sin(x * freq + phaseTime) * amplitude;
                    const y2 = Math.sin(x * freq + phaseTime + offsetRad) * amplitude;
                    const ySum = y1 + y2;
                    
                    if(Math.abs(ySum) > maxSumAmplitude) maxSumAmplitude = Math.abs(ySum);

                    if(x===0) phCtx.moveTo(x, midY + ySum); else phCtx.lineTo(x, midY + ySum);
                }
                phCtx.stroke();
                phCtx.shadowBlur = 0; // Reset

                // Update Logic & UI based on Max Sum Amplitude
                // Max possible theoretical sum is (amplitude * 2)
                const efficiencyPct = Math.round((maxSumAmplitude / (amplitude * 2)) * 100);
                document.getElementById('ampVal').innerText = `${efficiencyPct}%`;

                const verdict = document.getElementById('phaseVerdict');
                if(efficiencyPct < 20) {
                    verdict.className = 'phase-verdict verdict-bad';
                    verdict.innerHTML = '<i class="fas fa-times-circle"></i> DESTRUCTIVE CANCELLATION';
                } else if(efficiencyPct > 95) {
                    verdict.className = 'phase-verdict verdict-good';
                    verdict.innerHTML = '<i class="fas fa-check-double"></i> PERFECT PHASE ALIGNMENT (+6dB)';
                } else {
                    verdict.className = 'phase-verdict';
                    verdict.style.borderColor = 'var(--gold-primary)';
                    verdict.style.color = 'var(--gold-primary)';
                    verdict.style.background = 'rgba(212,175,55,0.1)';
                    verdict.innerHTML = '<i class="fas fa-exclamation-circle"></i> PARTIAL ALIGNMENT (COMB FILTERING)';
                }
            }
            // Initialize with slight delay to ensure DOM is rendered
            setTimeout(initPhaseAligner, 500);

            // --- 2. TACTICAL CREW DISPATCH LOGIC ---
            let selectedCrewId = null;
            let selectedCrewName = null;
            let selectedCrewSkill = null;

            // Base Times (Hours)
            const masterTasks = {
                tent: { base: 8.0, current: 8.0, elTime: 'eta-tent', elBar: 'bar-tent', elZone: 'zone-tent' },
                sound: { base: 5.0, current: 5.0, elTime: 'eta-sound', elBar: 'bar-sound', elZone: 'zone-sound' },
                light: { base: 4.0, current: 4.0, elTime: 'eta-light', elBar: 'bar-light', elZone: 'zone-light' }
            };

            function selectOperative(id, el) {
                if(typeof playTap === 'function') playTap();
                if(el.classList.contains('assigned')) {
                    if(typeof triggerToast === 'function') triggerToast("Operative already deployed.");
                    return;
                }

                document.querySelectorAll('.crew-card').forEach(c => c.classList.remove('selected'));
                el.classList.add('selected');

                selectedCrewId = id;
                selectedCrewName = el.querySelector('.crew-name').innerText;
                selectedCrewSkill = el.getAttribute('data-skill');
                
                if(navigator.vibrate) navigator.vibrate(10);
            }

            function assignOperative(taskId) {
                if(!selectedCrewId) {
                    if(typeof triggerToast === 'function') triggerToast("Select an operative from the roster first.");
                    return;
                }
                if(typeof playTap === 'function') playTap();

                const task = masterTasks[taskId];
                
                // Logic: Does the crew skill match the task?
                let timeReduction = 1.0; // Everyone helps reduce time by 1 hour
                if(selectedCrewSkill === taskId) timeReduction = 3.0; // Specialist bonus
                if(selectedCrewId === 'anil') timeReduction = 2.0; // Owner multi-task bonus
                
                task.current -= timeReduction;
                if(task.current < 1.0) task.current = 1.0; // Cap minimum time
                
                // Update UI DOM
                document.getElementById(task.elTime).innerText = `${task.current.toFixed(1)} Hrs`;
                document.getElementById(task.elBar).style.width = `${(task.current / task.base) * 100}%`;
                
                const dropzone = document.getElementById(task.elZone);
                dropzone.classList.remove('empty');
                dropzone.innerHTML += `<div class="assigned-badge"><i class="fas fa-check"></i> ${selectedCrewName}</div>`;
                
                // Disable the crew card
                const cCard = document.querySelector(`.crew-card[data-id="${selectedCrewId}"]`);
                cCard.classList.remove('selected');
                cCard.classList.add('assigned');
                
                // Reset selection
                selectedCrewId = null;
                selectedCrewName = null;
                selectedCrewSkill = null;
                
                calculateMasterEta();
            }

            function calculateMasterEta() {
                // Tasks are executed in parallel (at the same time), so total ETA is the longest task
                const totalEta = Math.max(masterTasks.tent.current, masterTasks.sound.current, masterTasks.light.current);
                
                const masterEtaEl = document.getElementById('masterEtaVal');
                masterEtaEl.innerText = `${totalEta.toFixed(1)} HRS`;
                
                // UI Pop animation
                masterEtaEl.style.transform = 'scale(1.1)';
                setTimeout(() => masterEtaEl.style.transform = 'scale(1)', 200);
            }

            // --- 3. GENERATIVE AI POSTER BUILDER ---
            const pCanvas = document.getElementById('posterCanvas');
            const pCtx = pCanvas.getContext('2d');
            let activeTheme = 'royal';

            // Theme Definitions
            const pThemes = {
                royal: { bg: '#111', prim: '#D4AF37', sec: '#fff', fontHead: 'Cinzel', fontSub: 'Rajdhani' },
                neon: { bg: '#050010', prim: '#00e5ff', sec: '#b829ff', fontHead: 'Orbitron', fontSub: 'Outfit' },
                dark: { bg: '#000', prim: '#fff', sec: '#888', fontHead: 'Outfit', fontSub: 'Outfit' }
            };

            function setPosterTheme(themeName, btnEl) {
                if(typeof playTap === 'function') playTap();
                document.querySelectorAll('.p-theme-btn').forEach(b => b.classList.remove('active'));
                btnEl.classList.add('active');
                activeTheme = themeName;
                renderPoster();
            }

            function renderPoster() {
                // Wait for fonts to load before drawing to canvas (important for first load)
                document.fonts.ready.then(() => {
                    const title = document.getElementById('postTitle').value || 'MND EVENT';
                    const sub = document.getElementById('postSub').value || 'Premium Setup';
                    const loc = document.getElementById('postLoc').value || 'Location TBD';
                    const rawDate = document.getElementById('postDate').value;
                    
                    let dateStr = 'DATE NOT SET';
                    if(rawDate) {
                        const d = new Date(rawDate);
                        dateStr = d.toLocaleDateString('en-IN', { day:'2-digit', month:'long', year:'numeric'}).toUpperCase();
                    }

                    const t = pThemes[activeTheme];
                    const w = pCanvas.width;  // 800
                    const h = pCanvas.height; // 1000
                    const cx = w / 2;

                    // 1. Draw Background
                    pCtx.fillStyle = t.bg;
                    pCtx.fillRect(0, 0, w, h);

                    // 2. Draw Theme Specific Graphics
                    pCtx.strokeStyle = t.prim;
                    pCtx.lineWidth = 4;
                    
                    if(activeTheme === 'royal') {
                        // Elegant double border
                        pCtx.strokeRect(40, 40, w - 80, h - 80);
                        pCtx.lineWidth = 1;
                        pCtx.strokeRect(50, 50, w - 100, h - 100);
                        
                        // Corner ornaments
                        pCtx.beginPath(); pCtx.arc(50, 50, 20, 0, Math.PI*2); pCtx.stroke();
                        pCtx.beginPath(); pCtx.arc(w-50, 50, 20, 0, Math.PI*2); pCtx.stroke();
                        pCtx.beginPath(); pCtx.arc(50, h-50, 20, 0, Math.PI*2); pCtx.stroke();
                        pCtx.beginPath(); pCtx.arc(w-50, h-50, 20, 0, Math.PI*2); pCtx.stroke();
                    } 
                    else if (activeTheme === 'neon') {
                        // Cyber grid
                        pCtx.strokeStyle = 'rgba(0, 229, 255, 0.2)';
                        pCtx.lineWidth = 2;
                        for(let i=0; i<w; i+=50) { pCtx.beginPath(); pCtx.moveTo(i,0); pCtx.lineTo(i,h); pCtx.stroke(); }
                        for(let i=0; i<h; i+=50) { pCtx.beginPath(); pCtx.moveTo(0,i); pCtx.lineTo(w,i); pCtx.stroke(); }
                        
                        // Center Neon Triangle
                        pCtx.strokeStyle = t.sec;
                        pCtx.lineWidth = 8;
                        pCtx.shadowBlur = 30; pCtx.shadowColor = t.sec;
                        pCtx.beginPath(); pCtx.moveTo(cx, 200); pCtx.lineTo(w-200, h-300); pCtx.lineTo(200, h-300); pCtx.closePath(); pCtx.stroke();
                        pCtx.shadowBlur = 0; // reset
                    } 
                    else if (activeTheme === 'dark') {
                        // Minimalist stark lines
                        pCtx.beginPath(); pCtx.moveTo(cx, 100); pCtx.lineTo(cx, 300); pCtx.stroke();
                        pCtx.beginPath(); pCtx.moveTo(cx, h-300); pCtx.lineTo(cx, h-100); pCtx.stroke();
                    }

                    // 3. Draw Typography
                    pCtx.textAlign = 'center';
                    
                    // Top Branding
                    pCtx.font = `bold 24px ${t.fontSub}`;
                    pCtx.fillStyle = t.sec;
                    pCtx.fillText('MAA NIRMALA DJ PRESENTS', cx, 150);

                    // Main Title
                    pCtx.font = `bold 70px ${t.fontHead}`;
                    pCtx.fillStyle = t.prim;
                    
                    // Simple word wrap for long titles
                    if(title.length > 15) {
                        const words = title.split(' ');
                        const half = Math.ceil(words.length / 2);
                        pCtx.fillText(words.slice(0, half).join(' '), cx, h/2 - 40);
                        pCtx.fillText(words.slice(half).join(' '), cx, h/2 + 40);
                    } else {
                        pCtx.fillText(title, cx, h/2);
                    }

                    // Subtitle
                    pCtx.font = `35px ${t.fontSub}`;
                    pCtx.fillStyle = t.sec;
                    pCtx.fillText(sub, cx, h/2 + 120);

                    // Footer Details (Date & Loc)
                    pCtx.font = `bold 40px ${t.fontHead}`;
                    pCtx.fillStyle = t.prim;
                    pCtx.fillText(dateStr, cx, h - 200);

                    pCtx.font = `30px ${t.fontSub}`;
                    pCtx.fillStyle = t.sec;
                    pCtx.fillText(loc, cx, h - 140);
                });
            }
            
            // Initial render call
            setTimeout(renderPoster, 800);

            function downloadPoster() {
                if(typeof triggerToast === 'function') triggerToast("Rendering High-Resolution File...");
                if(navigator.vibrate) navigator.vibrate([100, 50, 100]);
                
                setTimeout(() => {
                    const link = document.createElement('a');
                    link.download = 'MND_Event_Poster_HQ.png';
                    // Convert canvas to Data URL
                    link.href = pCanvas.toDataURL('image/png', 1.0);
                    link.click();
                    if(typeof triggerToast === 'function') triggerToast("Download Complete.");
                }, 1000); // Artificial delay to simulate processing
            }
        </script>
        <style>
            .truss-load-wrapper {
                background: #050505;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 20px 15px;
                box-shadow: inset 0 0 30px rgba(212, 175, 55, 0.05);
                position: relative;
            }

            .truss-display-area {
                width: 100%;
                height: 160px;
                background: linear-gradient(180deg, #0a0a0f, #000);
                border: 1px solid #333;
                border-radius: 8px;
                position: relative;
                margin-bottom: 20px;
                overflow: visible; /* Important so the SVG can bend downward outside the box if overloaded */
            }

            /* SVG Truss Beam Engine */
            #trussEngineSvg {
                position: absolute;
                top: 20px; left: 0;
                width: 100%; height: 120px;
                pointer-events: none;
            }

            /* Support Pillars (Left & Right) */
            .truss-pillar {
                position: absolute; top: 20px; width: 16px; height: 140px;
                background: repeating-linear-gradient(0deg, #333, #333 4px, #111 4px, #111 8px);
                border: 2px solid #555; border-radius: 2px; box-shadow: 0 0 10px rgba(0,0,0,0.8);
            }
            .tp-left { left: 10%; }
            .tp-right { right: 10%; }

            /* Hanging Load Icons */
            .hanging-load-item {
                position: absolute;
                transform: translateX(-50%);
                display: flex; flex-direction: column; align-items: center;
                transition: top 0.3s cubic-bezier(0.25, 1, 0.5, 1);
            }
            .load-chain { width: 2px; height: 15px; background: #888; }
            .load-box { 
                background: #111; border: 1px solid #555; border-radius: 4px; padding: 4px; 
                color: var(--gold-primary); font-size: 10px; box-shadow: 0 5px 10px rgba(0,0,0,0.8); 
                text-align: center; line-height: 1.2;
            }

            .truss-stats-grid {
                display: flex; justify-content: space-between;
                background: #0a0a0a; padding: 15px; border-radius: 8px; border: 1px solid #222;
            }
            .t-stat-block { display: flex; flex-direction: column; align-items: center; gap: 4px; }
            .ts-val { font-family: var(--font-tech); font-size: 18px; font-weight: 900; color: #00ff00; transition: color 0.3s; }
            .ts-lbl { font-family: var(--font-data); font-size: 9px; color: #888; letter-spacing: 1px; text-transform: uppercase; }

            .truss-controls {
                display: flex; gap: 10px; margin-top: 15px;
            }
            
            /* Warning State (Critical Overload) */
            .truss-warning .ts-val { color: var(--red-alert) !important; animation: blink 0.5s infinite; text-shadow: 0 0 10px rgba(255,51,51,0.8); }
            .truss-warning #tPathMain { stroke: var(--red-alert) !important; filter: drop-shadow(0 0 5px var(--red-alert)); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">KINETIC TRUSS MATRIX</h2>
                <div class="section-icon"><i class="fas fa-weight-hanging"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Monitor structural integrity. Add equipment to calculate physics-based bending moments.</p>

            <div class="truss-load-wrapper" id="trussEnvironment">
                <div class="truss-display-area">
                    <div class="truss-pillar tp-left"></div>
                    <div class="truss-pillar tp-right"></div>
                    
                    <svg id="trussEngineSvg" viewBox="0 0 400 120" preserveAspectRatio="none">
                        <path id="tPathMain" d="M 40 10 Q 200 10 360 10" fill="none" stroke="#888" stroke-width="4" stroke-dasharray="8,4"/>
                        <path id="tPathTop" d="M 40 2 Q 200 2 360 2" fill="none" stroke="#555" stroke-width="2"/>
                        <path id="tPathBot" d="M 40 18 Q 200 18 360 18" fill="none" stroke="#555" stroke-width="2"/>
                    </svg>

                    <div id="hangingLoadsContainer"></div>
                </div>

                <div class="truss-stats-grid">
                    <div class="t-stat-block">
                        <span class="ts-val" id="tWeightVal">0</span>
                        <span class="ts-lbl">TOTAL LOAD (KG)</span>
                    </div>
                    <div class="t-stat-block">
                        <span class="ts-val" id="tDeflectVal">0.0</span>
                        <span class="ts-lbl">DEFLECTION (MM)</span>
                    </div>
                    <div class="t-stat-block">
                        <span class="ts-val" id="tStatusVal" style="color: #888;">SAFE</span>
                        <span class="ts-lbl">INTEGRITY</span>
                    </div>
                </div>

                <div class="truss-controls">
                    <button class="app-btn-outline" style="flex: 1; border-color: var(--cyan-neon); color: var(--cyan-neon);" onclick="addTrussLoad('audio', 120)">
                        <i class="fas fa-speaker"></i> + AUDIO (120kg)
                    </button>
                    <button class="app-btn-outline" style="flex: 1; border-color: var(--gold-primary); color: var(--gold-primary);" onclick="addTrussLoad('light', 45)">
                        <i class="fas fa-lightbulb"></i> + LIGHT (45kg)
                    </button>
                    <button class="app-btn-outline" style="flex: 0.3; border-color: var(--red-alert); color: var(--red-alert);" onclick="resetTrussPhysics()">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>
            </div>
        </div>

        <style>
            .fog-sim-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .fog-canvas-container {
                width: 100%;
                height: 250px;
                background: #050505;
                border-radius: 8px;
                border: 1px solid #1a1a1a;
                position: relative;
                overflow: hidden;
            }
            /* Mix-blend screen allows the lasers to visually 'illuminate' the smoke */
            #fogCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Virtual Laser Emitters on the ground */
            .laser-emitter {
                position: absolute; bottom: 0; width: 12px; height: 8px; background: #333; border-radius: 4px 4px 0 0; z-index: 5;
            }
            .le-1 { left: 20%; } .le-2 { left: 50%; transform: translateX(-50%); } .le-3 { right: 20%; }

            .fog-controls {
                display: flex; flex-direction: column; gap: 15px; margin-top: 15px;
                background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #222;
            }
            .fc-row { display: flex; align-items: center; gap: 10px; }
            .fc-lbl { font-family: var(--font-tech); font-size: 9px; color: #aaa; letter-spacing: 1px; width: 70px; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">VOLUMETRIC FOG ENGINE</h2>
                <div class="section-icon"><i class="fas fa-smog"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Control atmospheric fluid dynamics. Watch lasers physically interact with dense smoke particles.</p>

            <div class="fog-sim-wrapper">
                <div class="fog-canvas-container" id="fogWrap">
                    <canvas id="fogCanvas"></canvas>
                    <div class="laser-emitter le-1"></div>
                    <div class="laser-emitter le-2"></div>
                    <div class="laser-emitter le-3"></div>
                </div>

                <div class="fog-controls">
                    <div class="fc-row">
                        <span class="fc-lbl">DENSITY</span>
                        <input type="range" class="app-slider" id="fogDensityVal" min="5" max="80" value="40" oninput="updateFogSystem()">
                    </div>
                    <div class="fc-row">
                        <span class="fc-lbl">WIND (X)</span>
                        <input type="range" class="app-slider" id="fogWindVal" min="-3" max="3" value="0" step="0.1" oninput="updateFogSystem()">
                    </div>
                </div>
            </div>
        </div>

        <style>
            .strobe-sequencer-wrapper {
                background: #0a0a0f;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .strobe-grid {
                display: grid;
                /* 1 col for label, 8 cols for steps */
                grid-template-columns: 30px repeat(8, 1fr);
                gap: 4px;
                margin-top: 15px;
                position: relative;
            }

            /* The moving vertical playhead line */
            .seq-playhead {
                position: absolute;
                top: -5px; bottom: -5px; width: 2px;
                background: var(--cyan-neon);
                box-shadow: 0 0 10px var(--cyan-neon);
                z-index: 10;
                left: calc(30px + 4px); /* Starts after label col */
                transition: left 0.1s linear;
                display: none;
            }

            .seq-row-label {
                display: flex; justify-content: center; align-items: center;
                background: #111; color: #888; font-family: var(--font-tech); font-size: 10px; font-weight: bold; border-radius: 4px;
            }
            .sr-r { color: var(--red-alert); } 
            .sr-g { color: #00ff00; } 
            .sr-b { color: var(--cyan-neon); } 
            .sr-w { color: #ffffff; }

            .seq-step-pad {
                background: #1a1a1a;
                border: 1px solid #333;
                border-radius: 4px;
                height: 35px;
                cursor: pointer;
                transition: 0.1s;
                touch-action: manipulation;
            }
            
            /* Active Colors for Pads */
            .seq-step-pad[data-color="red"].active { background: var(--red-alert); box-shadow: 0 0 10px rgba(255,51,51,0.5); border-color: #fff; }
            .seq-step-pad[data-color="grn"].active { background: #00ff00; box-shadow: 0 0 10px rgba(0,255,0,0.5); border-color: #fff; }
            .seq-step-pad[data-color="blu"].active { background: var(--cyan-neon); box-shadow: 0 0 10px rgba(0,229,255,0.5); border-color: #fff; }
            .seq-step-pad[data-color="wht"].active { background: #ffffff; box-shadow: 0 0 10px rgba(255,255,255,0.5); border-color: #fff; }

            .seq-controls {
                display: flex; justify-content: space-between; align-items: center; margin-top: 20px;
            }
            .bpm-input-box {
                background: #000; border: 1px solid var(--gold-primary); color: var(--gold-primary);
                font-family: var(--font-tech); font-size: 14px; text-align: center; padding: 8px; border-radius: 6px; width: 70px; outline: none;
            }

            /* Physical Screen Flashes applied to the body via JS */
            body.strobe-flash-red { background-color: rgba(255,0,0,0.4) !important; filter: contrast(1.2); }
            body.strobe-flash-grn { background-color: rgba(0,255,0,0.4) !important; filter: contrast(1.2); }
            body.strobe-flash-blu { background-color: rgba(0,229,255,0.4) !important; filter: contrast(1.2); }
            body.strobe-flash-wht { background-color: rgba(255,255,255,0.6) !important; filter: contrast(1.5); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">STROBE SEQUENCER</h2>
                <div class="section-icon"><i class="fas fa-th"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Program the DMX lighting grid. Press play to execute physical screen strobes synced to BPM.</p>

            <div class="strobe-sequencer-wrapper">
                <div class="strobe-grid" id="strobeGridContainer">
                    <div class="seq-playhead" id="strobePlayhead"></div>
                    
                    <div class="seq-row-label sr-r">R</div>
                    <div class="seq-step-pad" data-color="red" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad active" data-color="red" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="red" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="red" onclick="toggleStrobeStep(this)"></div>
                    <div class="seq-step-pad active" data-color="red" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="red" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="red" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="red" onclick="toggleStrobeStep(this)"></div>
                    
                    <div class="seq-row-label sr-g">G</div>
                    <div class="seq-step-pad" data-color="grn" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="grn" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad active" data-color="grn" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="grn" onclick="toggleStrobeStep(this)"></div>
                    <div class="seq-step-pad" data-color="grn" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="grn" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad active" data-color="grn" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="grn" onclick="toggleStrobeStep(this)"></div>

                    <div class="seq-row-label sr-b">B</div>
                    <div class="seq-step-pad active" data-color="blu" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="blu" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="blu" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="blu" onclick="toggleStrobeStep(this)"></div>
                    <div class="seq-step-pad" data-color="blu" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad active" data-color="blu" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="blu" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="blu" onclick="toggleStrobeStep(this)"></div>

                    <div class="seq-row-label sr-w">W</div>
                    <div class="seq-step-pad" data-color="wht" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="wht" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="wht" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad active" data-color="wht" onclick="toggleStrobeStep(this)"></div>
                    <div class="seq-step-pad" data-color="wht" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="wht" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad" data-color="wht" onclick="toggleStrobeStep(this)"></div><div class="seq-step-pad active" data-color="wht" onclick="toggleStrobeStep(this)"></div>
                </div>

                <div class="seq-controls">
                    <div style="display:flex; align-items:center; gap:10px;">
                        <span style="font-family:var(--font-data); color:#888; font-size:12px; font-weight:bold;">TEMPO (BPM)</span>
                        <input type="number" id="sequencerBpm" class="bpm-input-box" value="128">
                    </div>
                    <button class="app-btn-primary" id="btnPlaySequencer" style="width: auto;" onclick="toggleStrobeSequence()">
                        <i class="fas fa-play"></i> RUN SEQUENCE
                    </button>
                </div>
            </div>
        </div>

        <script>
            // --- 1. KINETIC TRUSS PHYSICS ENGINE ---
            let trussWeight = 0;
            const TRUSS_MAX_SAFE = 600; // kg
            let loadElements = 0;
            const maxLoads = 6; // Max visual items

            function addTrussLoad(type, weight) {
                if(typeof playTap === 'function') playTap();
                
                if(loadElements >= maxLoads) {
                    if(typeof triggerToast === 'function') triggerToast("Truss full. Max rigging points reached.");
                    return;
                }

                trussWeight += weight;
                loadElements++;

                // Visual Representation
                const container = document.getElementById('hangingLoadsContainer');
                const el = document.createElement('div');
                el.className = 'hanging-load-item';
                
                // Distribute evenly along the middle 60% of the truss (20% to 80%)
                const leftPercent = 20 + ((80 - 20) / (maxLoads + 1)) * loadElements;
                el.style.left = `${leftPercent}%`;
                el.style.top = `10px`; // Default, will be overridden by physics math

                const icon = type === 'audio' ? '<i class="fas fa-speaker" style="color:var(--cyan-neon);"></i>' : '<i class="fas fa-lightbulb" style="color:var(--gold-primary);"></i>';
                el.innerHTML = `<div class="load-chain"></div><div class="load-box">${icon}<br>${weight}kg</div>`;
                
                container.appendChild(el);
                
                if(navigator.vibrate) navigator.vibrate(15);
                calculateTrussSag();
            }

            function resetTrussPhysics() {
                if(typeof playTap === 'function') playTap();
                trussWeight = 0;
                loadElements = 0;
                document.getElementById('hangingLoadsContainer').innerHTML = '';
                calculateTrussSag();
            }

            function calculateTrussSag() {
                const env = document.getElementById('trussEnvironment');
                const pathMain = document.getElementById('tPathMain');
                const pathTop = document.getElementById('tPathTop');
                const pathBot = document.getElementById('tPathBot');
                
                const wDisplay = document.getElementById('tWeightVal');
                const dDisplay = document.getElementById('tDeflectVal');
                const sDisplay = document.getElementById('tStatusVal');

                wDisplay.innerText = trussWeight;

                // Physics Math: Bending Moment (Sag) is proportional to weight
                // Let's say max safe sag visually is 40 pixels
                let maxVisualSag = 40; 
                let sagPx = (trussWeight / TRUSS_MAX_SAFE) * maxVisualSag;
                
                // Exaggerate bend if overloaded (breaking point)
                if(trussWeight > TRUSS_MAX_SAFE) sagPx *= 1.5;

                // Update SVG Bezier Curves (The Q control point dictates the bend)
                // ViewBox is 400x120. Start is X:40, End is X:360. Center is X:200.
                const baseMidY = 10;
                const baseTopY = 2;
                const baseBotY = 18;

                // Multiply sagPx by 2 for the control point to ensure the actual line reaches the desired sag
                pathMain.setAttribute('d', `M 40 ${baseMidY} Q 200 ${baseMidY + sagPx * 2} 360 ${baseMidY}`);
                pathTop.setAttribute('d', `M 40 ${baseTopY} Q 200 ${baseTopY + sagPx * 2} 360 ${baseTopY}`);
                pathBot.setAttribute('d', `M 40 ${baseBotY} Q 200 ${baseBotY + sagPx * 2} 360 ${baseBotY}`);

                // Move the physical HTML items hanging on the curve
                const loads = document.querySelectorAll('.hanging-load-item');
                loads.forEach(load => {
                    const leftPct = parseFloat(load.style.left);
                    // Sine wave approximation for the parabolic curve drop based on horizontal position
                    // Map 20%-80% to 0-PI. Center (50%) gets max multiplier of 1.
                    const mappedX = (leftPct - 20) / 60; 
                    const sagMultiplier = Math.sin(mappedX * Math.PI);
                    
                    const newTop = baseMidY + (sagPx * sagMultiplier);
                    load.style.top = `${newTop}px`;
                });

                // Fake millimeter deflection calculation for UI
                const mmDeflection = (trussWeight * 0.12).toFixed(1);
                dDisplay.innerText = mmDeflection;

                // Warning States
                if(trussWeight > TRUSS_MAX_SAFE) {
                    env.classList.add('truss-warning');
                    sDisplay.innerText = "CRITICAL FAIL";
                    if(navigator.vibrate) navigator.vibrate([200, 100, 400, 100, 200]);
                    if(typeof triggerToast === 'function') triggerToast("WARNING: Structural limits exceeded!");
                } else if(trussWeight > TRUSS_MAX_SAFE * 0.75) {
                    env.classList.remove('truss-warning');
                    sDisplay.innerText = "HEAVY LOAD";
                    sDisplay.style.color = "var(--gold-primary)";
                    wDisplay.style.color = "var(--gold-primary)";
                } else {
                    env.classList.remove('truss-warning');
                    sDisplay.innerText = "SAFE";
                    sDisplay.style.color = "#888";
                    wDisplay.style.color = "#00ff00";
                }
            }

            // --- 2. VOLUMETRIC FOG & LASER FLUID DYNAMICS ENGINE ---
            const fogCanvas = document.getElementById('fogCanvas');
            let fogCtx = null;
            let smokeParticles = [];
            let fogAnimFrame = null;
            let currentDensity = 40;
            let currentWindX = 0;

            function initFogSim() {
                const wrap = document.getElementById('fogWrap');
                if(!wrap) return;
                fogCanvas.width = wrap.clientWidth;
                fogCanvas.height = wrap.clientHeight;
                fogCtx = fogCanvas.getContext('2d');
                
                spawnFogParticles();
                animateFogSim();
            }
            window.addEventListener('resize', initFogSim);

            function updateFogSystem() {
                currentDensity = parseInt(document.getElementById('fogDensityVal').value);
                currentWindX = parseFloat(document.getElementById('fogWindVal').value);
                spawnFogParticles();
            }

            class SmokeParticle {
                constructor() {
                    this.reset();
                    // Initial spawn randomize Y so it starts full
                    this.y = Math.random() * fogCanvas.height;
                }
                reset() {
                    this.x = Math.random() * fogCanvas.width;
                    this.y = fogCanvas.height + (Math.random() * 50); // Start below floor
                    this.vx = Math.random() * 0.4 - 0.2; // Tiny random horizontal drift
                    this.vy = -(Math.random() * 0.8 + 0.2); // Float up slowly
                    this.radius = Math.random() * 30 + 30; // Large soft circles
                    this.opacity = Math.random() * 0.15 + 0.05; // Very transparent
                }
                update() {
                    // Add global wind
                    this.x += this.vx + currentWindX;
                    this.y += this.vy;
                    
                    // Screen wrap
                    if(this.y < -this.radius) this.reset();
                    if(this.x > fogCanvas.width + this.radius) this.x = -this.radius;
                    if(this.x < -this.radius) this.x = fogCanvas.width + this.radius;
                }
                draw(ctx) {
                    const grad = ctx.createRadialGradient(this.x, this.y, 0, this.x, this.y, this.radius);
                    grad.addColorStop(0, `rgba(200, 200, 200, ${this.opacity})`);
                    grad.addColorStop(1, 'rgba(200, 200, 200, 0)');
                    ctx.fillStyle = grad;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                    ctx.fill();
                }
            }

            function spawnFogParticles() {
                // Map density slider (5-80) to actual particle count (roughly same)
                if(smokeParticles.length < currentDensity) {
                    const toAdd = currentDensity - smokeParticles.length;
                    for(let i=0; i<toAdd; i++) smokeParticles.push(new SmokeParticle());
                } else if (smokeParticles.length > currentDensity) {
                    smokeParticles.splice(0, smokeParticles.length - currentDensity);
                }
            }

            function animateFogSim() {
                fogAnimFrame = requestAnimationFrame(animateFogSim);
                
                // Clear background
                fogCtx.fillStyle = '#050505';
                fogCtx.fillRect(0, 0, fogCanvas.width, fogCanvas.height);
                
                // 1. Draw Smoke
                fogCtx.globalCompositeOperation = 'screen';
                smokeParticles.forEach(p => { p.update(); p.draw(fogCtx); });
                
                // 2. Draw Lasers & Volumetric Intersections
                fogCtx.globalCompositeOperation = 'lighter';
                
                // Laser origins (matches CSS .laser-emitter classes)
                const cw = fogCanvas.width;
                const ch = fogCanvas.height;
                const lasers = [
                    { x: cw * 0.2, color: 'rgba(0, 229, 255, 0.5)' }, // Cyan
                    { x: cw * 0.5, color: 'rgba(255, 51, 51, 0.5)' }, // Red
                    { x: cw * 0.8, color: 'rgba(212, 175, 55, 0.5)' } // Gold
                ];

                lasers.forEach(laser => {
                    // Draw base beam line (Straight up)
                    fogCtx.beginPath();
                    fogCtx.moveTo(laser.x, ch);
                    fogCtx.lineTo(laser.x, 0);
                    fogCtx.lineWidth = 2;
                    fogCtx.strokeStyle = laser.color;
                    fogCtx.stroke();

                    // Complex Physics: Light Scattering
                    // If a smoke particle is touching the laser line, make it glow the laser's color
                    smokeParticles.forEach(p => {
                        // Check horizontal distance between particle center and laser line
                        if(Math.abs(p.x - laser.x) < p.radius * 0.8) {
                            // Extract RGB from the rgba string to build a custom gradient
                            const rgbMatch = laser.color.match(/\d+, \d+, \d+/);
                            if(rgbMatch) {
                                const rgb = rgbMatch[0];
                                const glowGrad = fogCtx.createRadialGradient(laser.x, p.y, 0, laser.x, p.y, p.radius);
                                // The glow intensity is tied to the smoke particle's base opacity
                                glowGrad.addColorStop(0, `rgba(${rgb}, ${p.opacity * 2.5})`);
                                glowGrad.addColorStop(1, `rgba(${rgb}, 0)`);
                                
                                fogCtx.fillStyle = glowGrad;
                                fogCtx.beginPath();
                                fogCtx.arc(laser.x, p.y, p.radius, 0, Math.PI*2);
                                fogCtx.fill();
                            }
                        }
                    });
                });
                
                fogCtx.globalCompositeOperation = 'source-over'; // Reset for next frame
            }
            // Delay start to ensure DOM sizing
            setTimeout(initFogSim, 800);

            // --- 3. HYPER-SYNC STROBE SEQUENCER LOGIC ---
            let seqIsPlaying = false;
            let seqCurrentStep = 0;
            let seqIntervalTimer = null;

            function toggleStrobeStep(el) {
                if(typeof playTap === 'function') playTap();
                el.classList.toggle('active');
            }

            function toggleStrobeSequence() {
                if(typeof playTap === 'function') playTap();
                const btn = document.getElementById('btnPlaySequencer');
                const playhead = document.getElementById('strobePlayhead');
                
                if(!seqIsPlaying) {
                    seqIsPlaying = true;
                    btn.innerHTML = '<i class="fas fa-stop"></i> STOP SEQUENCE';
                    btn.style.background = 'linear-gradient(135deg, var(--red-alert), #990000)';
                    btn.style.color = '#fff';
                    playhead.style.display = 'block';
                    seqCurrentStep = 0;
                    
                    // Math for BPM -> MS
                    // 60,000 ms in a minute. We are doing 8th notes, so divide beat by 2.
                    const bpm = parseInt(document.getElementById('sequencerBpm').value) || 128;
                    const msPerStep = (60000 / bpm) / 2; 
                    
                    seqIntervalTimer = setInterval(processSequencerStep, msPerStep);
                    
                } else {
                    seqIsPlaying = false;
                    btn.innerHTML = '<i class="fas fa-play"></i> RUN SEQUENCE';
                    btn.style.background = 'linear-gradient(135deg, var(--gold-primary), var(--gold-glow))';
                    btn.style.color = '#000';
                    playhead.style.display = 'none';
                    clearInterval(seqIntervalTimer);
                    document.body.className = ''; // Wipe all flash classes
                }
            }

            function processSequencerStep() {
                // Keep step between 0 and 7 (8 columns)
                seqCurrentStep = seqCurrentStep % 8;
                
                // UI: Move Playhead
                const playhead = document.getElementById('strobePlayhead');
                const grid = document.getElementById('strobeGridContainer');
                
                // Grid calculation: Total width minus the 30px label column and gap
                const usableWidth = grid.clientWidth - 34; 
                const colWidth = usableWidth / 8;
                
                // Position playhead in center of current column
                playhead.style.left = `calc(34px + ${seqCurrentStep * colWidth}px + ${colWidth/2}px)`;

                // LOGIC: Check which pads are active in the current column
                const pads = document.querySelectorAll('.seq-step-pad');
                
                let r=false, g=false, b=false, w=false;
                
                // Row 1 (Red) is indices 0-7
                if(pads[seqCurrentStep].classList.contains('active')) r = true;
                // Row 2 (Grn) is indices 8-15
                if(pads[seqCurrentStep + 8].classList.contains('active')) g = true;
                // Row 3 (Blu) is indices 16-23
                if(pads[seqCurrentStep + 16].classList.contains('active')) b = true;
                // Row 4 (Wht) is indices 24-31
                if(pads[seqCurrentStep + 24].classList.contains('active')) w = true;

                // EXECUTION: Apply CSS classes to the global body to flash the screen
                document.body.className = ''; // Clear previous flash
                
                // Priority logic (White overrides colors)
                if(w) { 
                    document.body.classList.add('strobe-flash-wht'); 
                    if(navigator.vibrate) navigator.vibrate(20); // Hard tap for white
                }
                else if(r) document.body.classList.add('strobe-flash-red');
                else if(b) document.body.classList.add('strobe-flash-blu');
                else if(g) document.body.classList.add('strobe-flash-grn');

                // Clear the flash rapidly to create the strobe effect (50ms duration)
                setTimeout(() => {
                    if(seqIsPlaying) document.body.className = '';
                }, 50);

                seqCurrentStep++;
            }
        </script>
        <style>
            .telemetry-map-container {
                width: 100%;
                height: 220px;
                background: #050a10;
                border: 1px solid #1a3344;
                border-radius: 12px;
                position: relative;
                overflow: hidden;
                margin-bottom: 15px;
            }

            /* Topographic Map Background */
            .telemetry-map-container::before {
                content: ''; position: absolute; inset: 0;
                background-image: 
                    radial-gradient(circle at 20% 30%, transparent 20%, rgba(0, 229, 255, 0.05) 21%, transparent 22%),
                    radial-gradient(circle at 80% 70%, transparent 30%, rgba(0, 229, 255, 0.05) 31%, transparent 32%);
                background-size: 150px 150px; opacity: 0.8;
            }

            #routeSvg { position: absolute; inset: 0; width: 100%; height: 100%; z-index: 2; pointer-events: none; }
            
            /* Map Nodes */
            .map-node {
                position: absolute; width: 10px; height: 10px; border-radius: 50%;
                transform: translate(-50%, -50%); z-index: 3; box-shadow: 0 0 10px currentColor;
            }
            .map-lbl {
                position: absolute; color: #fff; font-family: var(--font-data); font-size: 9px;
                font-weight: bold; transform: translateX(-50%); margin-top: 8px; z-index: 4; text-shadow: 0 2px 4px #000;
            }

            /* The Moving Tractor Blip */
            .tractor-blip {
                position: absolute; width: 24px; height: 24px;
                background: rgba(255, 204, 0, 0.2); border: 2px solid #ffcc00; border-radius: 50%;
                transform: translate(-50%, -50%); display: flex; justify-content: center; align-items: center;
                color: #ffcc00; font-size: 10px; z-index: 5;
                box-shadow: 0 0 15px rgba(255,204,0,0.6); transition: left 0.1s linear, top 0.1s linear;
            }
            .tractor-blip::after {
                content:''; position:absolute; width:34px; height:34px;
                border:1px solid #ffcc00; border-radius:50%; animation: radarPulse 1.5s infinite;
            }

            .telemetry-stats {
                display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px;
            }
            .t-stat-box { background: rgba(0,0,0,0.5); border: 1px solid #222; border-radius: 8px; padding: 10px; text-align: center; }
            .t-lbl { display: block; font-family: var(--font-tech); font-size: 8px; color: var(--cyan-neon); letter-spacing: 1px; margin-bottom: 3px; }
            .t-val { font-family: var(--font-body); font-size: 14px; color: #fff; font-weight: 900; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">FLEET TELEMETRY</h2>
                <div class="section-icon"><i class="fas fa-truck-moving"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Live GPS tracking of Laxmikant Heavy Transport.</p>

            <div class="telemetry-map-container" id="mapEnvironment">
                <svg id="routeSvg">
                    <path id="deliveryRoute" fill="none" stroke="rgba(0, 229, 255, 0.3)" stroke-width="3" stroke-dasharray="6,6"/>
                </svg>
                
                <div class="map-node" id="nodeHQ" style="background: var(--gold-primary); color: var(--gold-primary);"></div>
                <div class="map-lbl" id="lblHQ">BELTIKRI HQ</div>
                
                <div class="map-node" id="nodeDest" style="background: var(--cyan-neon); color: var(--cyan-neon);"></div>
                <div class="map-lbl" id="lblDest">VENUE DROP</div>

                <div class="tractor-blip" id="tractorIcon"><i class="fas fa-tractor"></i></div>
            </div>

            <div class="telemetry-stats">
                <div class="t-stat-box">
                    <span class="t-lbl">PAYLOAD</span>
                    <span class="t-val">8.5 TON</span>
                </div>
                <div class="t-stat-box">
                    <span class="t-lbl">TERRAIN</span>
                    <span class="t-val" style="color: var(--gold-primary);">OFF-ROAD</span>
                </div>
                <div class="t-stat-box">
                    <span class="t-lbl">SYS ETA</span>
                    <span class="t-val" id="etaTracker" style="color: #00ff00;">STANDBY</span>
                </div>
            </div>

            <button class="app-btn-outline" style="margin-top: 15px; width: 100%; border-color: var(--gold-primary); color: var(--gold-primary);" onclick="startFleetDelivery()" id="btnDispatchFleet">
                <i class="fas fa-satellite"></i> DISPATCH HEAVY TRACTOR
            </button>
        </div>

        <style>
            .stress-test-wrapper {
                background: #000;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 20px;
                text-align: center;
                position: relative;
                overflow: hidden;
            }

            .virtual-glass-pane {
                width: 100%;
                height: 180px;
                background: linear-gradient(135deg, rgba(255,255,255,0.05), rgba(255,255,255,0.01));
                border: 1px solid rgba(255,255,255,0.1);
                border-radius: 8px;
                margin: 0 auto 20px auto;
                position: relative;
                backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px);
                display: flex; flex-direction: column; justify-content: center; align-items: center;
                overflow: hidden;
                box-shadow: inset 0 0 20px rgba(255,255,255,0.05);
            }

            /* Animated shine crossing the glass */
            .glass-shine {
                position: absolute; top: 0; left: -100%; width: 50%; height: 100%;
                background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
                transform: skewX(-20deg); animation: glassShineAnim 4s infinite;
            }
            @keyframes glassShineAnim { 0% { left: -100%; } 20% { left: 200%; } 100% { left: 200%; } }

            .spl-readout { font-family: var(--font-tech); font-size: 32px; font-weight: 900; color: #fff; z-index: 2; transition: 0.1s; }
            .spl-label { font-family: var(--font-data); font-size: 10px; color: #aaa; letter-spacing: 2px; z-index: 2; }

            /* Hidden crack SVG */
            .glass-crack-svg {
                position: absolute; inset: 0; width: 100%; height: 100%; pointer-events: none; z-index: 3; display: none;
            }

            .shatter-slider {
                -webkit-appearance: none; width: 100%; height: 12px; border-radius: 6px;
                background: linear-gradient(90deg, #00ff00, #ffff00, var(--red-alert));
                outline: none; border: 2px solid #333; margin-top: 10px;
            }
            .shatter-slider::-webkit-slider-thumb {
                -webkit-appearance: none; appearance: none; width: 28px; height: 28px; border-radius: 50%;
                background: #111; border: 3px solid #fff; cursor: grab; box-shadow: 0 0 10px rgba(0,0,0,0.8);
            }

            /* Broken State Classes */
            .stress-test-wrapper.broken .virtual-glass-pane { background: rgba(255,0,0,0.05); border-color: var(--red-alert); }
            .stress-test-wrapper.broken .glass-crack-svg { display: block; }
            .stress-test-wrapper.broken .spl-readout { color: var(--red-alert); animation: blink 0.2s infinite; }
            
            /* Physical App Shake */
            @keyframes apocalypseShake {
                0% { transform: translate(5px, 5px); } 20% { transform: translate(-5px, -5px); }
                40% { transform: translate(5px, -5px); } 60% { transform: translate(-5px, 5px); }
                80% { transform: translate(5px, 0); } 100% { transform: translate(0, 5px); }
            }
            body.apocalypse-shake { animation: apocalypseShake 0.1s infinite; filter: contrast(1.2); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">SPL STRESS TEST</h2>
                <div class="section-icon"><i class="fas fa-volume-up"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Push the 21-inch subwoofers to maximum excursion. Warning: Structural damage likely.</p>

            <div class="stress-test-wrapper" id="shatterEnvironment">
                <div class="virtual-glass-pane" id="glassPane">
                    <div class="glass-shine"></div>
                    <svg class="glass-crack-svg" viewBox="0 0 100 100" preserveAspectRatio="none">
                        <path d="M50 50 L10 10 M50 50 L85 20 M50 50 L15 80 M50 50 L90 85 M50 50 L40 95 M35 30 L50 50 L70 45" stroke="rgba(255,255,255,0.9)" stroke-width="0.8" fill="none"/>
                        <path d="M50 50 L30 40 L45 20" stroke="rgba(255,255,255,0.4)" stroke-width="0.3" fill="none"/>
                    </svg>
                    <div class="spl-readout" id="splLevelDisplay">60 dB</div>
                    <span class="spl-label">ACOUSTIC CABIN PRESSURE</span>
                </div>

                <span style="font-family:var(--font-data); font-size:11px; color:#fff; font-weight:bold; display:block; margin-bottom:5px;">MASTER FADER</span>
                <input type="range" class="shatter-slider" id="splStressSlider" min="60" max="145" value="60" oninput="checkSplStress(this.value)">
                
                <button class="app-btn-outline" id="btnRepairGlass" style="margin-top: 15px; display: none; width: 100%; border-color: #00ff00; color: #00ff00;" onclick="repairVirtualGlass()">
                    <i class="fas fa-tools"></i> REPAIR STRUCTURAL GLASS
                </button>
            </div>
        </div>

        <style>
            .drone-swarm-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .swarm-canvas-container {
                width: 100%;
                height: 280px;
                background: radial-gradient(circle at bottom center, #001a33 0%, #000 100%);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                border: 1px solid #112233;
            }
            #swarmCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .swarm-hud {
                position: absolute; top: 10px; left: 10px; pointer-events: none;
            }
            .sw-title { font-family: var(--font-tech); font-size: 10px; font-weight: 900; color: var(--cyan-neon); letter-spacing: 1px; }
            .sw-stats { font-family: var(--font-data); font-size: 9px; color: #fff; margin-top: 3px; }

            .swarm-controls {
                display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-top: 15px;
            }
            .sw-btn {
                background: rgba(0,0,0,0.5); border: 1px solid #333; border-radius: 6px;
                color: #888; font-family: var(--font-data); font-weight: bold; font-size: 11px; padding: 10px 0;
                cursor: pointer; transition: 0.2s; text-align: center;
            }
            .sw-btn:active { transform: scale(0.95); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DRONE SWARM AI</h2>
                <div class="section-icon"><i class="fas fa-helicopter"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Command the autonomous aerial LED fleet to form dynamic sky constellations.</p>

            <div class="drone-swarm-wrapper">
                <div class="swarm-canvas-container" id="swarmWrap">
                    <canvas id="swarmCanvas"></canvas>
                    <div class="swarm-hud">
                        <div class="sw-title">AERIAL FLEET // ONLINE</div>
                        <div class="sw-stats">ACTIVE UNITS: 120</div>
                    </div>
                </div>

                <div class="swarm-controls">
                    <button class="sw-btn" onclick="commandSwarm('scatter')" style="color: var(--cyan-neon); border-color: var(--cyan-neon);">SCATTER</button>
                    <button class="sw-btn" onclick="commandSwarm('heart')" style="color: var(--red-alert); border-color: var(--red-alert);">HEART</button>
                    <button class="sw-btn" onclick="commandSwarm('star')" style="color: var(--gold-primary); border-color: var(--gold-primary);">STAR</button>
                </div>
            </div>
        </div>

        <script>
            // --- 1. LAXMIKANT FLEET TELEMETRY LOGIC ---
            const mapEnv = document.getElementById('mapEnvironment');
            const routeSvg = document.getElementById('routeSvg');
            const deliveryRoute = document.getElementById('deliveryRoute');
            const nodeHQ = document.getElementById('nodeHQ');
            const nodeDest = document.getElementById('nodeDest');
            const lblHQ = document.getElementById('lblHQ');
            const lblDest = document.getElementById('lblDest');
            const tractor = document.getElementById('tractorIcon');
            const etaDisplay = document.getElementById('etaTracker');
            const btnDispatch = document.getElementById('btnDispatchFleet');
            
            let isFleetDelivering = false;
            let fleetProgress = 0;
            let fleetTimer = null;

            function setupTelemetryMap() {
                if(!mapEnv) return;
                const w = mapEnv.clientWidth;
                const h = mapEnv.clientHeight;
                
                // Set fixed points (HQ bottom left, Dest top right)
                const hqX = 40; const hqY = h - 40;
                const destX = w - 40; const destY = 40;
                
                // Position DOM elements
                nodeHQ.style.left = `${hqX}px`; nodeHQ.style.top = `${hqY}px`;
                lblHQ.style.left = `${hqX}px`; lblHQ.style.top = `${hqY}px`;
                
                nodeDest.style.left = `${destX}px`; nodeDest.style.top = `${destY}px`;
                lblDest.style.left = `${destX}px`; lblDest.style.top = `${destY}px`;

                // Draw SVG Bezier curve
                const cp1X = w * 0.3; const cp1Y = h * 0.2; // Control point 1
                const cp2X = w * 0.7; const cp2Y = h * 0.8; // Control point 2
                
                const pathStr = `M ${hqX} ${hqY} C ${cp1X} ${cp1Y}, ${cp2X} ${cp2Y}, ${destX} ${destY}`;
                deliveryRoute.setAttribute('d', pathStr);
                
                // Set initial tractor position if not moving
                if(!isFleetDelivering) {
                    tractor.style.left = `${hqX}px`;
                    tractor.style.top = `${hqY}px`;
                }
            }
            window.addEventListener('resize', setupTelemetryMap);
            setTimeout(setupTelemetryMap, 500);

            function startFleetDelivery() {
                if(isFleetDelivering) return;
                if(typeof playTap === 'function') playTap();
                
                isFleetDelivering = true;
                fleetProgress = 0;
                
                btnDispatch.innerHTML = '<i class="fas fa-spinner fa-spin"></i> EN ROUTE...';
                btnDispatch.style.color = '#888'; btnDispatch.style.borderColor = '#333';
                
                if(navigator.vibrate) navigator.vibrate([200, 100, 200]);
                if(typeof triggerToast === 'function') triggerToast("Laxmikant Heavy Transport Dispatched.");

                const pathLength = deliveryRoute.getTotalLength();

                fleetTimer = setInterval(() => {
                    fleetProgress += 0.005; // Adjust speed here
                    
                    if(fleetProgress >= 1) {
                        clearInterval(fleetTimer);
                        isFleetDelivering = false;
                        if(typeof triggerToast === 'function') triggerToast("Equipment safely delivered to Venue.");
                        etaDisplay.innerText = "ARRIVED";
                        etaDisplay.style.color = "var(--gold-primary)";
                        
                        btnDispatch.innerHTML = '<i class="fas fa-check"></i> DELIVERY COMPLETE';
                        btnDispatch.style.color = '#00ff00'; btnDispatch.style.borderColor = '#00ff00';
                        
                        // Play horn sound from Part 3 if available
                        if(typeof playSynth === 'function') playSynth('djHorn', null);
                        return;
                    }
                    
                    // Get coordinates along the curved SVG path
                    const point = deliveryRoute.getPointAtLength(fleetProgress * pathLength);
                    tractor.style.left = `${point.x}px`;
                    tractor.style.top = `${point.y}px`;
                    
                    // Update Fake ETA (Starts at 45 mins)
                    const minsLeft = Math.floor((1 - fleetProgress) * 45); 
                    etaDisplay.innerText = `T-MINUS ${minsLeft}m`;
                    etaDisplay.style.color = "var(--cyan-neon)";
                    
                }, 50); // 50ms update interval for smooth animation
            }

            // --- 2. ACOUSTIC GLASS-SHATTER PHYSICS LOGIC ---
            let isGlassShattered = false;

            function checkSplStress(val) {
                if(isGlassShattered) {
                    // Lock slider at max if broken
                    document.getElementById('splStressSlider').value = 145;
                    return; 
                }

                const display = document.getElementById('splLevelDisplay');
                const env = document.getElementById('shatterEnvironment');
                const pane = document.getElementById('glassPane');
                
                display.innerText = `${val} dB`;

                // Calculate Physical Shake (Starts getting intense past 100dB)
                if(val > 100) {
                    display.style.color = 'var(--gold-glow)';
                    const shakeAmt = (val - 100) / 8; // Max shake ~5.6px
                    // Apply random translation
                    pane.style.transform = `translate(${(Math.random()-0.5)*shakeAmt}px, ${(Math.random()-0.5)*shakeAmt}px)`;
                    
                    // Minor haptic rumble
                    if(navigator.vibrate && val % 3 === 0) navigator.vibrate(10);
                } else {
                    display.style.color = '#fff';
                    pane.style.transform = 'translate(0, 0)';
                }

                // BREAKING POINT (140 dB)
                if(val >= 140) {
                    isGlassShattered = true;
                    env.classList.add('broken');
                    display.innerText = "STRUCTURAL FAIL";
                    pane.style.transform = 'translate(0, 0)'; // Stop smooth shake
                    
                    // Heavy Haptic Shock
                    if(navigator.vibrate) navigator.vibrate([300, 100, 500]);
                    
                    // Global screen shake via body class
                    document.body.classList.add('apocalypse-shake');
                    setTimeout(() => document.body.classList.remove('apocalypse-shake'), 300);
                    
                    // Trigger Bass Drop sound if audio engine is running
                    if(typeof playSynth === 'function') playSynth('subDrop', null);
                    
                    // Show repair button
                    document.getElementById('btnRepairGlass').style.display = 'block';
                }
            }

            function repairVirtualGlass() {
                if(typeof playTap === 'function') playTap();
                isGlassShattered = false;
                
                const env = document.getElementById('shatterEnvironment');
                env.classList.remove('broken');
                
                const slider = document.getElementById('splStressSlider');
                slider.value = 60;
                
                document.getElementById('splLevelDisplay').innerText = "60 dB";
                document.getElementById('splLevelDisplay').style.color = "#fff";
                document.getElementById('btnRepairGlass').style.display = 'none';
                
                if(typeof triggerToast === 'function') triggerToast("Structural Glass Repaired.");
            }

            // --- 3. DRONE SWARM CHOREOGRAPHY AI LOGIC ---
            const swCanvas = document.getElementById('swarmCanvas');
            let swCtx = null;
            const swWrap = document.getElementById('swarmWrap');
            let dronesArray = [];
            let swarmAnimFrame = null;
            const totalDrones = 120;

            function initSwarmEngine() {
                if(!swWrap) return;
                swCanvas.width = swWrap.clientWidth;
                swCanvas.height = swWrap.clientHeight;
                swCtx = swCanvas.getContext('2d');
                
                // Initialize drones in random positions
                for(let i=0; i<totalDrones; i++) {
                    dronesArray.push(new SmartDrone(Math.random() * swCanvas.width, Math.random() * swCanvas.height));
                }
                
                commandSwarm('scatter'); // Default formation
                animateDroneSwarm();
            }
            window.addEventListener('resize', () => {
                if(swWrap) { swCanvas.width = swWrap.clientWidth; swCanvas.height = swWrap.clientHeight; commandSwarm('scatter');}
            });

            class SmartDrone {
                constructor(x, y) {
                    this.x = x; this.y = y;
                    this.targetX = x; this.targetY = y;
                    this.color = 'var(--cyan-neon)';
                    this.speed = Math.random() * 0.05 + 0.03; // Lerp factor
                    this.offset = Math.random() * Math.PI * 2; // For hover effect
                }
                update() {
                    // Linear interpolation (Lerp) towards target
                    this.x += (this.targetX - this.x) * this.speed;
                    this.y += (this.targetY - this.y) * this.speed;
                    
                    // Add natural hovering motion
                    const time = Date.now() * 0.002;
                    this.x += Math.sin(time + this.offset) * 0.5;
                    this.y += Math.cos(time + this.offset) * 0.5;
                }
                draw(ctx) {
                    ctx.fillStyle = this.color;
                    ctx.shadowBlur = 8;
                    ctx.shadowColor = this.color;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, 2, 0, Math.PI*2);
                    ctx.fill();
                    ctx.shadowBlur = 0;
                }
            }

            function commandSwarm(shape) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(15);
                
                const w = swCanvas.width;
                const h = swCanvas.height;
                const cx = w / 2;
                const cy = h / 2;

                // Determine color based on shape
                let hue = 'var(--cyan-neon)';
                if(shape === 'heart') hue = 'var(--red-alert)';
                if(shape === 'star') hue = 'var(--gold-primary)';

                dronesArray.forEach((drone, i) => {
                    drone.color = hue;
                    
                    if(shape === 'scatter') {
                        drone.targetX = Math.random() * w;
                        drone.targetY = Math.random() * h;
                    } 
                    else if (shape === 'heart') {
                        // Parametric equation for a heart
                        const t = (i / totalDrones) * Math.PI * 2;
                        const scale = 6;
                        // 16sin^3(t)
                        const hx = 16 * Math.pow(Math.sin(t), 3);
                        // 13cos(t) - 5cos(2t) - 2cos(3t) - cos(4t)
                        const hy = -(13 * Math.cos(t) - 5 * Math.cos(2*t) - 2 * Math.cos(3*t) - Math.cos(4*t));
                        
                        drone.targetX = cx + hx * scale;
                        drone.targetY = cy + hy * scale;
                    }
                    else if (shape === 'star') {
                        // 5-pointed star math
                        const t = (i / totalDrones) * Math.PI * 2;
                        const radius = (i % 2 === 0) ? 90 : 40; // Alternate between outer and inner radius
                        
                        drone.targetX = cx + Math.cos(t) * radius;
                        drone.targetY = cy + Math.sin(t) * radius;
                    }
                });
            }

            function animateDroneSwarm() {
                swarmAnimFrame = requestAnimationFrame(animateDroneSwarm);
                
                // Draw semi-transparent black background to create motion trails
                swCtx.fillStyle = 'rgba(0, 0, 0, 0.4)';
                swCtx.fillRect(0, 0, swCanvas.width, swCanvas.height);
                
                swCtx.globalCompositeOperation = 'lighter';
                dronesArray.forEach(drone => {
                    drone.update();
                    drone.draw(swCtx);
                });
                swCtx.globalCompositeOperation = 'source-over';
            }
            
            setTimeout(initSwarmEngine, 800);
        </script>
        <style>
            .interference-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 15px 40px rgba(0,0,0,0.9);
            }

            .wave-canvas-container {
                width: 100%;
                height: 280px;
                background: linear-gradient(180deg, #050505, #0a0a0f);
                border: 1px solid #333;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #waveCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Virtual Subwoofers over Canvas */
            .wave-sub-icon {
                position: absolute; bottom: 20px;
                width: 24px; height: 24px;
                background: #111; border: 2px solid var(--red-alert);
                border-radius: 4px; box-shadow: 0 0 15px rgba(255,51,51,0.4);
                transform: translateX(-50%); z-index: 5;
                display: flex; justify-content: center; align-items: center;
                transition: left 0.1s linear;
            }
            .wave-sub-icon::after { content:''; width:12px; height:12px; background:#000; border-radius:50%; border:1px solid #444; }
            #subLeft { left: 35%; }
            #subRight { left: 65%; }

            .wave-controls {
                display: flex; flex-direction: column; align-items: center; margin-top: 20px; gap: 10px;
                background: #0a0a0a; padding: 15px; border-radius: 8px; border: 1px solid #111;
            }
            .wave-ctrl-header {
                display: flex; justify-content: space-between; width: 100%; 
                font-family: var(--font-data); font-size: 10px; color: var(--gold-primary); font-weight: bold; letter-spacing: 1px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">ACOUSTIC INTERFERENCE AI</h2>
                <div class="section-icon"><i class="fas fa-water"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Adjust subwoofer distance to visualize constructive interference and the resulting "Power Alley" effect of low frequencies.</p>

            <div class="interference-wrapper">
                <div class="wave-canvas-container" id="waveWrap">
                    <canvas id="waveCanvas"></canvas>
                    <div class="wave-sub-icon" id="subLeft"></div>
                    <div class="wave-sub-icon" id="subRight"></div>
                    <div style="position:absolute; top:10px; left:50%; transform:translateX(-50%); color:rgba(255,51,51,0.8); font-family:var(--font-tech); font-size:9px; text-shadow: 0 0 5px rgba(255,0,0,0.5); font-weight:bold; pointer-events: none;">CONSTRUCTIVE SUMMATION ZONE</div>
                </div>

                <div class="wave-controls">
                    <div class="wave-ctrl-header">
                        <span>CLOSER (COMB FILTERING)</span>
                        <span>SUBWOOFER SPACING</span>
                        <span>WIDER (POWER ALLEY)</span>
                    </div>
                    <input type="range" class="app-slider" id="subDistSlider" min="5" max="40" value="15" style="width: 100%;" oninput="updateSubSpacing(this.value)">
                </div>
            </div>
        </div>

        <style>
            .journey-mapper-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .journey-graph-container {
                width: 100%;
                height: 220px;
                background: #050508;
                border-radius: 8px;
                border: 1px solid #112233;
                margin-top: 15px;
                position: relative;
                overflow-x: auto;
                overflow-y: hidden;
                white-space: nowrap;
                scrollbar-width: none; /* Hide scrollbar */
                padding: 20px 30px;
                display: flex;
                align-items: flex-end;
                box-shadow: inset 0 0 30px rgba(0,0,0,0.8);
            }
            .journey-graph-container::-webkit-scrollbar { display: none; }

            /* SVG Line connection between nodes */
            #journeyLineSvg {
                position: absolute; top: 0; left: 0; width: 1000px; height: 100%; pointer-events: none; z-index: 1;
            }

            .journey-node {
                display: inline-flex;
                flex-direction: column;
                align-items: center;
                position: relative;
                z-index: 2;
                margin-right: 50px;
                transition: transform 0.3s;
                cursor: pointer;
            }
            .journey-node:hover { transform: translateY(-5px); }
            
            .j-bar { width: 8px; border-radius: 4px 4px 0 0; position: relative; transition: height 0.5s ease-out;}
            .j-lbl { font-family: var(--font-data); font-size: 10px; color: #fff; font-weight: bold; position: absolute; bottom: -20px; text-transform: uppercase; white-space: nowrap;}
            .j-time { font-family: var(--font-tech); font-size: 8px; color: var(--gold-primary); position: absolute; top: -15px;}
            
            /* Dynamic heights and colors based on "energy level" */
            .e-low { height: 30px; background: linear-gradient(to top, var(--cyan-neon), #fff); box-shadow: 0 0 10px rgba(0,229,255,0.5);}
            .e-mid { height: 80px; background: linear-gradient(to top, var(--gold-primary), #fff); box-shadow: 0 0 10px rgba(212,175,55,0.5);}
            .e-high { height: 140px; background: linear-gradient(to top, var(--red-alert), #fff); box-shadow: 0 0 15px rgba(255,51,51,0.5);}

            .journey-controls {
                display: flex; justify-content: center; gap: 10px; margin-top: 10px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">AI EVENT JOURNEY MAPPER</h2>
                <div class="section-icon"><i class="fas fa-route"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Visualize the acoustic energy flow and emotional trajectory of your event timeline.</p>

            <div class="journey-mapper-wrapper">
                <div class="journey-controls">
                    <button class="app-btn-outline" style="width: auto; border-radius: 20px;" onclick="renderJourney('wedding')">WEDDING PROFILE</button>
                    <button class="app-btn-outline" style="width: auto; border-radius: 20px; border-color: var(--gold-primary); color: var(--gold-primary);" onclick="renderJourney('club')">CLUB PROFILE</button>
                </div>

                <div class="journey-graph-container" id="journeyGraphBox">
                    <svg id="journeyLineSvg">
                        <path id="journeyPath" fill="none" stroke="rgba(255,255,255,0.3)" stroke-width="2" stroke-dasharray="4,4"/>
                    </svg>
                    </div>
            </div>
        </div>

        <style>
            .neural-review-wrapper {
                background: #000;
                border: 1px solid #1a1a24;
                border-radius: 12px;
                padding: 10px;
                position: relative;
            }

            .neural-review-box {
                width: 100%;
                height: 350px;
                background: radial-gradient(circle at center, #050a10 0%, #000 100%);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #reviewCanvas { width: 100%; height: 100%; position: absolute; inset: 0; z-index: 1; pointer-events: none;}
            
            /* Physical DOM Nodes that float over the canvas */
            .review-node {
                position: absolute; width: 12px; height: 12px; border-radius: 50%;
                background: var(--gold-primary); box-shadow: 0 0 15px var(--gold-primary);
                cursor: pointer; z-index: 5; transform: translate(-50%, -50%);
                transition: background 0.3s, box-shadow 0.3s, transform 0.1s;
            }
            .review-node:active { transform: translate(-50%, -50%) scale(1.5); }
            .review-node.active { background: var(--cyan-neon); box-shadow: 0 0 20px var(--cyan-neon); }

            /* Floating review card when node is clicked */
            .review-popup-card {
                position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%) scale(0.9);
                width: 85%; max-width: 320px; background: var(--glass-bg);
                backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
                border: 1px solid var(--gold-primary); border-radius: 16px; padding: 25px; z-index: 10;
                opacity: 0; pointer-events: none; transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
                box-shadow: 0 20px 50px rgba(0,0,0,0.9), inset 0 0 20px rgba(212,175,55,0.1);
            }
            .review-popup-card.show { opacity: 1; pointer-events: auto; transform: translate(-50%, -50%) scale(1); }
            
            .rp-close { position: absolute; top: 15px; right: 15px; color: #888; cursor: pointer; font-size: 18px; padding: 5px;}
            .rp-close:active { color: var(--red-alert); }
            .rp-client { font-family: var(--font-head); font-size: 18px; color: var(--gold-primary); font-weight: bold; margin: 0; }
            .rp-loc { font-family: var(--font-tech); font-size: 9px; color: var(--cyan-neon); text-transform: uppercase; letter-spacing: 2px; }
            .rp-stars { color: var(--gold-glow); margin: 12px 0; font-size: 12px; letter-spacing: 2px; }
            .rp-text { font-family: var(--font-body); font-size: 13px; color: #ddd; line-height: 1.6; font-style: italic; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">CLIENT NEURAL NETWORK</h2>
                <div class="section-icon"><i class="fas fa-network-wired"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Tap the drifting data nodes to decrypt verified client testimonies and performance metrics.</p>

            <div class="neural-review-wrapper">
                <div class="neural-review-box" id="neuralBox">
                    <canvas id="reviewCanvas"></canvas>
                    <div style="position:absolute; bottom:10px; left:10px; color:#444; font-family:var(--font-tech); font-size:9px; z-index:2;">DECRYPTING REGIONAL DATABASES...</div>
                    
                    <div class="review-popup-card" id="reviewPopupCard">
                        <i class="fas fa-times rp-close" onclick="closeReviewNode()"></i>
                        <h4 class="rp-client" id="rpClientName">Client Name</h4>
                        <div class="rp-loc" id="rpClientLoc">Location</div>
                        <div class="rp-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                        <div class="rp-text" id="rpClientText">Review text goes here.</div>
                    </div>
                </div>
            </div>
        </div>

        <script>
            // --- 1. ACOUSTIC INTERFERENCE WAVE ENGINE ---
            const wCanvas = document.getElementById('waveCanvas');
            const wCtx = wCanvas ? wCanvas.getContext('2d') : null;
            const wWrap = document.getElementById('waveWrap');
            const subL = document.getElementById('subLeft');
            const subR = document.getElementById('subRight');
            
            let waveAnimFrame = null;
            let waveTime = 0;
            let subSpacingPct = 15; // Represents distance from center (5 to 40)

            function resizeWaveCanvas() {
                if(!wWrap || !wCanvas) return;
                wCanvas.width = wWrap.clientWidth;
                wCanvas.height = wWrap.clientHeight;
            }
            window.addEventListener('resize', resizeWaveCanvas);

            function updateSubSpacing(val) {
                subSpacingPct = parseInt(val);
                // Center is 50%. Left sub goes left, Right sub goes right.
                if(subL && subR) {
                    subL.style.left = `${50 - subSpacingPct}%`;
                    subR.style.left = `${50 + subSpacingPct}%`;
                }
                if(navigator.vibrate) navigator.vibrate(10);
            }

            function animateAcousticWaves() {
                if(!wCtx) return;
                waveAnimFrame = requestAnimationFrame(animateAcousticWaves);
                
                // Clear canvas with deep black
                wCtx.fillStyle = '#050505';
                wCtx.fillRect(0, 0, wCanvas.width, wCanvas.height);
                
                wCtx.globalCompositeOperation = 'screen'; // Additive blending for light overlap
                
                waveTime += 1.0; // Speed of expanding rings
                
                // Physical Pixel Coordinates of Subwoofers
                const pxLeft = wCanvas.width * ((50 - subSpacingPct) / 100);
                const pxRight = wCanvas.width * ((50 + subSpacingPct) / 100);
                const py = wCanvas.height - 20; // Match CSS bottom: 20px

                wCtx.lineWidth = 2;

                // Draw expanding rings for both subs (12 rings total)
                for(let i=0; i<12; i++) {
                    // Loop radius from 0 to 400px
                    let r = (waveTime + (i * 35)) % 400; 
                    
                    if(r > 0) {
                        // Fade out as it gets bigger
                        const opacity = 1 - (r / 400);
                        wCtx.strokeStyle = `rgba(255, 51, 51, ${opacity * 0.8})`;
                        
                        // Left Sub Wave
                        wCtx.beginPath();
                        wCtx.arc(pxLeft, py, r, Math.PI, Math.PI * 2); // Top half circle
                        wCtx.stroke();
                        
                        // Right Sub Wave
                        wCtx.beginPath();
                        wCtx.arc(pxRight, py, r, Math.PI, Math.PI * 2);
                        wCtx.stroke();
                    }
                }
                
                wCtx.globalCompositeOperation = 'source-over';
                
                // Draw a faint yellow center line to emphasize the "Power Alley"
                wCtx.strokeStyle = 'rgba(255, 255, 0, 0.3)';
                wCtx.lineWidth = 1;
                wCtx.setLineDash([5, 5]);
                wCtx.beginPath();
                wCtx.moveTo(wCanvas.width/2, 0);
                wCtx.lineTo(wCanvas.width/2, wCanvas.height);
                wCtx.stroke();
                wCtx.setLineDash([]);
            }
            
            setTimeout(() => {
                resizeWaveCanvas();
                animateAcousticWaves();
            }, 800);

            // --- 2. AI SETLIST JOURNEY MAPPER LOGIC ---
            const jGraphBox = document.getElementById('journeyGraphBox');
            const jPath = document.getElementById('journeyPath');

            const journeyDataProfiles = {
                wedding: [
                    { time: '18:00', lbl: 'Warmup', class: 'e-low' },
                    { time: '19:30', lbl: 'Baraat', class: 'e-high' },
                    { time: '21:00', lbl: 'Varmala', class: 'e-mid' },
                    { time: '22:30', lbl: 'Dinner', class: 'e-low' },
                    { time: '00:00', lbl: 'Dance', class: 'e-high' }
                ],
                club: [
                    { time: '20:00', lbl: 'Doors', class: 'e-low' },
                    { time: '22:00', lbl: 'Groove', class: 'e-mid' },
                    { time: '00:00', lbl: 'Peak', class: 'e-high' },
                    { time: '02:00', lbl: 'Drop', class: 'e-high' },
                    { time: '04:00', lbl: 'Close', class: 'e-mid' }
                ]
            };

            function renderJourney(profileType) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(15);
                
                if(!jGraphBox) return;

                // Clear existing nodes (except the SVG background)
                const existingNodes = jGraphBox.querySelectorAll('.journey-node');
                existingNodes.forEach(n => n.remove());

                const data = journeyDataProfiles[profileType];
                let svgPathData = "";
                let xOffset = 40; // Start padding

                data.forEach((item, index) => {
                    const node = document.createElement('div');
                    node.className = 'journey-node';
                    
                    // Simple staggered fade in
                    node.style.opacity = '0';
                    node.style.transform = 'translateY(10px)';
                    node.style.transition = 'opacity 0.4s, transform 0.4s';
                    setTimeout(() => {
                        node.style.opacity = '1';
                        node.style.transform = 'translateY(0)';
                    }, index * 100);
                    
                    node.innerHTML = `
                        <span class="j-time">${item.time}</span>
                        <div class="j-bar ${item.class}"></div>
                        <span class="j-lbl">${item.lbl}</span>
                    `;
                    
                    jGraphBox.appendChild(node);

                    // Calculate path for SVG line connecting the tops of the bars
                    // Container inner height is 220px minus padding (20px top, 30px bottom)
                    // Bar heights: low=30, mid=80, high=140
                    let h = item.class === 'e-low' ? 30 : item.class === 'e-mid' ? 80 : 140;
                    // Y position from top of container: 220 - 30(bottom pad) - h
                    let yPos = 220 - 30 - h; 
                    
                    if(index === 0) svgPathData += `M ${xOffset} ${yPos} `;
                    else svgPathData += `L ${xOffset} ${yPos} `;
                    
                    xOffset += 58; // Bar width (8) + margin-right (50)
                });

                // Update SVG Line
                if(jPath) {
                    jPath.setAttribute('d', svgPathData);
                    // Animate line draw
                    const length = jPath.getTotalLength();
                    jPath.style.strokeDasharray = length;
                    jPath.style.strokeDashoffset = length;
                    // Force reflow
                    jPath.getBoundingClientRect();
                    jPath.style.transition = 'stroke-dashoffset 1.5s ease-in-out';
                    jPath.style.strokeDashoffset = '0';
                }
            }

            // Init default journey
            setTimeout(() => renderJourney('wedding'), 1000);


            // --- 3. NEURAL-NET CLIENT FEEDBACK MATRIX LOGIC ---
            const nrBox = document.getElementById('neuralBox');
            const revCanvas = document.getElementById('reviewCanvas');
            const rCtx = revCanvas ? revCanvas.getContext('2d') : null;
            
            const realReviews = [
                { name: 'Rohan Sharma', loc: 'Deoghar', text: 'The bass from MND is unbelievable. The whole ground was physically shaking during my Baraat!' },
                { name: 'Priya Singh', loc: 'Banka', text: 'They built a completely waterproof VIP pandal overnight. Extremely professional crew.' },
                { name: 'Amit Verma', loc: 'Katoria', text: 'The DMX laser show turned our reception into a high-end club. Simply amazing.' },
                { name: 'Suresh Das', loc: 'Beltikri', text: 'Laxmikant tractors navigated the worst off-road conditions to get the heavy DJ setup to our village on time.' },
                { name: 'Neha Gupta', loc: 'Jamui', text: 'Audio quality was crystal clear. No feedback during speeches, and massive energy during the dance.' }
            ];

            let reviewNodesArray = [];
            let nrAnimFrame = null;

            class ReviewNodeObj {
                constructor(data) {
                    this.data = data;
                    // Start in bounds
                    this.x = Math.random() * (nrBox.clientWidth - 40) + 20;
                    this.y = Math.random() * (nrBox.clientHeight - 40) + 20;
                    this.vx = (Math.random() - 0.5) * 1.0; // Slower, elegant speed
                    this.vy = (Math.random() - 0.5) * 1.0;
                    
                    // Create HTML element to overlay on canvas for easy click handling
                    this.el = document.createElement('div');
                    this.el.className = 'review-node';
                    
                    // Attach touch/click event
                    this.el.addEventListener('mousedown', () => openReviewNode(this));
                    this.el.addEventListener('touchstart', (e) => { e.preventDefault(); openReviewNode(this); }, {passive: false});
                    
                    nrBox.appendChild(this.el);
                }
                update() {
                    this.x += this.vx; 
                    this.y += this.vy;
                    
                    // Soft wall bounce
                    if(this.x <= 10 || this.x >= nrBox.clientWidth - 10) this.vx *= -1;
                    if(this.y <= 10 || this.y >= nrBox.clientHeight - 10) this.vy *= -1;
                    
                    // Sync DOM element position
                    this.el.style.left = `${this.x}px`;
                    this.el.style.top = `${this.y}px`;
                }
            }

            function initNeuralReviews() {
                if(!nrBox || !revCanvas) return;
                revCanvas.width = nrBox.clientWidth;
                revCanvas.height = nrBox.clientHeight;
                
                // Spawn nodes
                realReviews.forEach(d => reviewNodesArray.push(new ReviewNodeObj(d)));
                animateNeuralNet();
            }

            function animateNeuralNet() {
                if(!rCtx) return;
                nrAnimFrame = requestAnimationFrame(animateNeuralNet);
                
                rCtx.clearRect(0,0, revCanvas.width, revCanvas.height);
                
                // Update Physics
                reviewNodesArray.forEach(n => n.update());
                
                // Draw connecting laser lines between nodes that are close to each other
                rCtx.lineWidth = 1;
                
                for(let i=0; i<reviewNodesArray.length; i++) {
                    for(let j=i+1; j<reviewNodesArray.length; j++) {
                        const dx = reviewNodesArray[i].x - reviewNodesArray[j].x;
                        const dy = reviewNodesArray[i].y - reviewNodesArray[j].y;
                        const dist = Math.hypot(dx, dy);
                        
                        // If close enough, draw a line. Closer = more opaque.
                        if(dist < 120) {
                            const opacity = 1 - (dist / 120);
                            rCtx.strokeStyle = `rgba(212, 175, 55, ${opacity * 0.5})`;
                            rCtx.beginPath();
                            rCtx.moveTo(reviewNodesArray[i].x, reviewNodesArray[i].y);
                            rCtx.lineTo(reviewNodesArray[j].x, reviewNodesArray[j].y);
                            rCtx.stroke();
                        }
                    }
                }
            }
            
            function openReviewNode(nodeObj) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                
                // Reset other nodes
                document.querySelectorAll('.review-node').forEach(n => n.classList.remove('active'));
                nodeObj.el.classList.add('active');
                
                // Populate popup data
                document.getElementById('rpClientName').innerText = nodeObj.data.name;
                document.getElementById('rpClientLoc').innerText = nodeObj.data.loc;
                document.getElementById('rpClientText').innerText = nodeObj.data.text;
                
                // Show popup
                document.getElementById('reviewPopupCard').classList.add('show');
                
                // Play tech sound if engine is running
                if(typeof playSynth === 'function') playSynth('laserB', null);
            }

            function closeReviewNode() {
                if(typeof playTap === 'function') playTap();
                document.getElementById('reviewPopupCard').classList.remove('show');
                document.querySelectorAll('.review-node').forEach(n => n.classList.remove('active'));
            }

            window.addEventListener('resize', () => {
                if(nrBox && revCanvas) {
                    revCanvas.width = nrBox.clientWidth;
                    revCanvas.height = nrBox.clientHeight;
                }
            });
            setTimeout(initNeuralReviews, 1000);
        </script>
        <style>
            .power-grid-wrapper {
                background: linear-gradient(180deg, #111, #050505);
                border: 2px solid #333;
                border-radius: 12px;
                padding: 20px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 40px rgba(0,0,0,1);
                transition: background 0.2s, border-color 0.2s;
            }

            /* Blackout State */
            .power-grid-wrapper.blackout-state {
                background: #000 !important;
                border-color: #111 !important;
            }
            .power-grid-wrapper.blackout-state * {
                color: #222 !important;
                border-color: #111 !important;
                box-shadow: none !important;
                text-shadow: none !important;
                background-color: #050505 !important;
            }
            .power-grid-wrapper.blackout-state .blackout-overlay {
                display: flex !important;
                background: rgba(0,0,0,0.9) !important;
            }

            .blackout-overlay {
                position: absolute; inset: 0; z-index: 20;
                display: none; flex-direction: column; justify-content: center; align-items: center;
                backdrop-filter: blur(5px); -webkit-backdrop-filter: blur(5px);
            }
            .bo-text { font-family: var(--font-tech); font-size: 28px; font-weight: 900; color: var(--red-alert) !important; text-shadow: 0 0 20px var(--red-alert) !important; animation: blink 0.5s infinite; }
            .bo-sub { font-family: var(--font-body); font-size: 11px; color: #fff !important; margin-top: 10px; text-transform: uppercase; letter-spacing: 1px; }

            .pg-hud { display: flex; justify-content: space-between; align-items: flex-end; margin-bottom: 20px; border-bottom: 2px dashed #333; padding-bottom: 15px; }
            .pg-title { font-family: var(--font-head); font-size: 16px; color: var(--gold-primary); font-weight: 900; }
            .pg-capacity { font-family: var(--font-tech); font-size: 24px; color: #00ff00; font-weight: 900; text-shadow: 0 0 10px rgba(0,255,0,0.5); transition: 0.3s; }
            
            .load-bar-box { width: 100%; height: 16px; background: #000; border: 1px solid #444; border-radius: 8px; overflow: hidden; position: relative; margin-bottom: 25px; box-shadow: inset 0 2px 5px rgba(0,0,0,0.8); }
            .load-bar-fill { height: 100%; width: 0%; background: linear-gradient(90deg, #00e5ff, #00ff00, #ffff00, var(--red-alert)); transition: width 0.3s ease-out; }
            .load-limit-marker { position: absolute; top: 0; bottom: 0; width: 2px; background: var(--red-alert); z-index: 2; box-shadow: 0 0 10px var(--red-alert); }

            .load-sliders { display: flex; flex-direction: column; gap: 15px; }
            .load-row { display: flex; align-items: center; gap: 10px; }
            .load-lbl { width: 70px; font-family: var(--font-data); font-size: 10px; color: #aaa; font-weight: bold; }
            .load-val { width: 45px; font-family: var(--font-tech); font-size: 11px; color: #fff; text-align: right; }

            .breaker-reset-btn {
                margin-top: 20px; width: 100%; padding: 15px;
                background: linear-gradient(180deg, var(--red-alert), #990000);
                border: 2px solid #550000; border-radius: 8px;
                color: #fff; font-family: var(--font-tech); font-weight: 900; font-size: 14px;
                box-shadow: 0 5px 15px rgba(255,0,0,0.4), inset 0 2px 5px rgba(255,255,255,0.4);
                cursor: pointer; transition: 0.1s; letter-spacing: 2px;
            }
            .breaker-reset-btn:active { transform: translateY(4px); box-shadow: 0 0px 0px rgba(255,0,0,0.4), inset 0 5px 10px rgba(0,0,0,0.6); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DG SET LOAD BALANCER</h2>
                <div class="section-icon"><i class="fas fa-bolt"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Manage the electrical draw of the equipment. Exceeding 60kW will trip the generator breaker.</p>

            <div class="power-grid-wrapper" id="powerGridEnv">
                <div class="blackout-overlay" id="blackoutScreen">
                    <i class="fas fa-plug" style="font-size: 40px; color: var(--red-alert); margin-bottom: 15px;"></i>
                    <span class="bo-text">SYSTEM OVERLOAD</span>
                    <span class="bo-sub">Breaker Tripped. Reset Required.</span>
                    <button class="breaker-reset-btn" style="width: 80%; margin-top: 20px;" onclick="resetGeneratorBreaker()">RESET BREAKER</button>
                </div>

                <div class="pg-hud">
                    <div>
                        <div class="pg-title">SILENT DG SET A</div>
                        <span style="font-family:var(--font-body); font-size:9px; color:#666;">62.5 kVA Kirloskar Core</span>
                    </div>
                    <div style="text-align:right;">
                        <span style="font-family:var(--font-data); font-size:9px; color:#aaa; display:block;">CURRENT LOAD</span>
                        <span class="pg-capacity" id="currentKwDisplay">0 kW</span>
                    </div>
                </div>

                <div style="position: relative;">
                    <div class="load-bar-box">
                        <div class="load-bar-fill" id="kwBarFill"></div>
                        <div class="load-limit-marker" style="left: 75%;"></div> </div>
                    <span style="position:absolute; top:20px; left:75%; transform:translateX(-50%); font-size:8px; color:var(--red-alert); font-family:var(--font-tech); font-weight:bold;">TRIP POINT (60kW)</span>
                </div>

                <div class="load-sliders">
                    <div class="load-row">
                        <span class="load-lbl"><i class="fas fa-volume-up" style="color:var(--cyan-neon);"></i> AUDIO</span>
                        <input type="range" class="app-slider" id="kwAudio" min="0" max="30" value="0" oninput="calculateGridLoad()">
                        <span class="load-val"><span id="valKwAudio">0</span>kW</span>
                    </div>
                    <div class="load-row">
                        <span class="load-lbl"><i class="fas fa-lightbulb" style="color:var(--gold-primary);"></i> LIGHTS</span>
                        <input type="range" class="app-slider" id="kwLights" min="0" max="30" value="0" oninput="calculateGridLoad()">
                        <span class="load-val"><span id="valKwLights">0</span>kW</span>
                    </div>
                    <div class="load-row">
                        <span class="load-lbl"><i class="fas fa-tv" style="color:#b829ff;"></i> LED WALL</span>
                        <input type="range" class="app-slider" id="kwLed" min="0" max="25" value="0" oninput="calculateGridLoad()">
                        <span class="load-val"><span id="valKwLed">0</span>kW</span>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .mapping-wrapper {
                background: #030305;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .mapper-canvas-box {
                width: 100%;
                height: 250px;
                background: #000;
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                touch-action: none; /* Crucial for drawing */
                box-shadow: 0 0 20px rgba(0, 229, 255, 0.1);
            }
            
            /* Virtual Structure Background */
            .mapper-canvas-box::before {
                content: ''; position: absolute; inset: 0;
                background: url('https://i.postimg.cc/pXx5fqGQ/image_fac9be10.png') center/cover;
                opacity: 0.2; filter: grayscale(100%) contrast(1.5);
                pointer-events: none; z-index: 1;
            }

            #mapperCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2; mix-blend-mode: screen; }

            .mapper-hud {
                position: absolute; top: 10px; left: 10px; z-index: 5; pointer-events: none;
                color: var(--cyan-neon); font-family: var(--font-tech); font-size: 9px; font-weight: 900; letter-spacing: 1px;
                text-shadow: 0 0 5px var(--cyan-neon);
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">PROJECTION MAPPING AI</h2>
                <div class="section-icon"><i class="fas fa-draw-polygon"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Trace architectural geometry with your finger. The AI laser will continuously map the outline.</p>

            <div class="mapping-wrapper">
                <div class="mapper-canvas-box" id="mapperWrap">
                    <div class="mapper-hud">LASER MAPPER // NODES: <span id="pmNodeCount">0</span></div>
                    <canvas id="mapperCanvas"></canvas>
                </div>
                
                <div style="display: flex; gap: 10px; margin-top: 15px;">
                    <button class="app-btn-outline" style="flex: 1;" onclick="clearProjectionMap()">
                        <i class="fas fa-trash"></i> CLEAR MESH
                    </button>
                    <div style="flex: 2; display: flex; flex-direction: column; justify-content: center;">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888; margin-bottom:5px;">LASER VELOCITY</span>
                        <input type="range" class="app-slider" id="pmSpeed" min="2" max="25" value="8">
                    </div>
                </div>
            </div>
        </div>

        <style>
            .nuke-wrapper {
                background: #000;
                border: 1px dashed #333;
                border-radius: 12px;
                padding: 40px 20px;
                display: flex;
                flex-direction: column;
                align-items: center;
                position: relative;
            }

            /* The physical button design */
            .nuke-button {
                width: 140px; height: 140px;
                border-radius: 50%;
                background: radial-gradient(circle at 30% 30%, #ff4d4d, #880000);
                border: 6px solid #1a1a1a;
                box-shadow: 
                    0 10px 30px rgba(255,0,0,0.4),
                    inset 0 10px 20px rgba(255,255,255,0.3),
                    inset 0 -10px 20px rgba(0,0,0,0.8),
                    0 0 0 12px #0a0a0a,
                    0 0 0 14px #333;
                cursor: pointer;
                display: flex; justify-content: center; align-items: center;
                color: #fff; font-family: var(--font-tech); font-size: 20px; font-weight: 900; letter-spacing: 2px;
                text-shadow: 0 2px 5px rgba(0,0,0,0.8);
                transition: transform 0.1s, box-shadow 0.1s;
                z-index: 5;
                /* Disable text selection and mobile context menu */
                -webkit-user-select: none; user-select: none; -webkit-touch-callout: none;
            }
            
            .nuke-button:active {
                transform: scale(0.95);
                box-shadow: 
                    0 5px 15px rgba(255,0,0,0.5),
                    inset 0 2px 5px rgba(255,255,255,0.1),
                    inset 0 -5px 10px rgba(0,0,0,0.8),
                    0 0 0 12px #0a0a0a,
                    0 0 0 14px #333;
            }

            /* Cinematic Overlay activated during countdown */
            #bassDropOverlay {
                position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 99998;
                display: none; justify-content: center; align-items: center; flex-direction: column;
                opacity: 0; transition: opacity 0.5s ease-in;
                backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
            }
            .drop-timer {
                font-family: var(--font-tech); font-size: 160px; font-weight: 900; color: var(--red-alert);
                text-shadow: 0 0 50px var(--red-alert); line-height: 1;
            }
            .drop-text { color: #fff; font-family: var(--font-data); font-size: 18px; letter-spacing: 12px; margin-top: 20px; font-weight: bold; text-align: center; }

            /* Extreme shake for the actual drop */
            @keyframes nukeShake {
                0% { transform: translate(15px, 15px) rotate(1deg); filter: contrast(2) saturate(2) hue-rotate(90deg); }
                20% { transform: translate(-15px, -20px) rotate(-1deg); filter: contrast(2) saturate(2) hue-rotate(-90deg); }
                40% { transform: translate(-30px, 0px) rotate(2deg); filter: contrast(3) saturate(3) invert(1); }
                60% { transform: translate(30px, 20px) rotate(0deg); filter: contrast(2) saturate(2) hue-rotate(180deg); }
                80% { transform: translate(15px, -15px) rotate(-2deg); filter: contrast(2) saturate(2) hue-rotate(45deg); }
                100% { transform: translate(0, 0) rotate(0deg); filter: none; }
            }
            body.nuke-mode { animation: nukeShake 0.1s infinite; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">MAXIMUM OVERDRIVE</h2>
                <div class="section-icon" style="color: var(--red-alert); background: rgba(255,51,51,0.1);"><i class="fas fa-radiation"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 25px; text-align: center;">Warning: Initiates the Zero-Gravity Bass Drop Protocol.</p>

            <div class="nuke-wrapper">
                <div style="position:absolute; top:15px; left:15px; color:var(--red-alert); font-family:var(--font-tech); font-size:10px; animation:blink 1s infinite;">ARMED & READY</div>
                <div class="nuke-button" onclick="initiateNukeDrop()">DROP</div>
            </div>
        </div>

        <div id="bassDropOverlay">
            <div class="drop-timer" id="bdCountdown">3</div>
            <div class="drop-text" id="bdText">SYSTEM OVERLOAD IMMINENT</div>
        </div>


        <script>
            // --- 1. DG SET POWER GRID BALANCER LOGIC ---
            let isBlackout = false;
            const MAX_KW = 60; // Generator trip limit

            function calculateGridLoad() {
                if(isBlackout) return; // Prevent adjustment during blackout

                const audioKw = parseInt(document.getElementById('kwAudio').value);
                const lightsKw = parseInt(document.getElementById('kwLights').value);
                const ledKw = parseInt(document.getElementById('kwLed').value);
                
                // Update specific values
                document.getElementById('valKwAudio').innerText = audioKw;
                document.getElementById('valKwLights').innerText = lightsKw;
                document.getElementById('valKwLed').innerText = ledKw;

                const totalKw = audioKw + lightsKw + ledKw;
                const kwDisp = document.getElementById('currentKwDisplay');
                const barFill = document.getElementById('kwBarFill');

                kwDisp.innerText = `${totalKw} kW`;
                
                // Max slider limit combined is 30+30+25 = 85. Set bar max to 80 for visual padding.
                let pct = (totalKw / 80) * 100;
                if(pct > 100) pct = 100;
                barFill.style.width = `${pct}%`;

                // Color warning updates
                if(totalKw > MAX_KW * 0.85) {
                    kwDisp.style.color = '#ffff00'; // Warning yellow
                } else {
                    kwDisp.style.color = '#00ff00'; // Safe green
                }

                // TRIP BREAKER LOGIC
                if(totalKw > MAX_KW) {
                    triggerBlackout();
                }
            }

            function triggerBlackout() {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate([500, 200, 500]); // Heavy haptic alarm
                
                isBlackout = true;
                const env = document.getElementById('powerGridEnv');
                env.classList.add('blackout-state');
                
                // Reset physical sliders immediately to 0
                document.getElementById('kwAudio').value = 0;
                document.getElementById('kwLights').value = 0;
                document.getElementById('kwLed').value = 0;
                
                // If Web Audio Engine is running, shut it down to simulate power loss
                if(typeof isEngineOn !== 'undefined' && isEngineOn) {
                    if(typeof bootAudioEngine === 'function') bootAudioEngine(); 
                }
            }

            function resetGeneratorBreaker() {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(50);
                
                isBlackout = false;
                const env = document.getElementById('powerGridEnv');
                env.classList.remove('blackout-state');
                
                // Recalculate to reset UI text since sliders are now at 0
                calculateGridLoad(); 
                
                if(typeof triggerToast === 'function') triggerToast("DG Set Restarted. Power Restored.");
            }


            // --- 2. PROJECTION MAPPING LASER TRACER LOGIC ---
            const pmCanvas = document.getElementById('mapperCanvas');
            let pmCtx = null;
            const pmWrap = document.getElementById('mapperWrap');
            
            let pmPoints = [];
            let isPmDrawing = false;
            let laserHeadPos = {x: 0, y: 0};
            let currentTargetIdx = 0;
            let pmAnimFrame = null;

            function initProjectionMapper() {
                if(!pmWrap) return;
                pmCanvas.width = pmWrap.clientWidth;
                pmCanvas.height = pmWrap.clientHeight;
                pmCtx = pmCanvas.getContext('2d');
            }
            window.addEventListener('resize', initProjectionMapper);
            setTimeout(initProjectionMapper, 800);

            // Capture touch/mouse coordinates relative to canvas
            function getPmCoords(e) {
                const rect = pmCanvas.getBoundingClientRect();
                const x = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                const y = e.type.includes('touch') ? e.touches[0].clientY : e.clientY;
                return { x: x - rect.left, y: y - rect.top };
            }

            pmCanvas.addEventListener('mousedown', pmStartDraw);
            pmCanvas.addEventListener('touchstart', (e) => { e.preventDefault(); pmStartDraw(e); }, {passive: false});

            function pmStartDraw(e) {
                isPmDrawing = true;
                const pos = getPmCoords(e);
                pmPoints.push(pos);
                document.getElementById('pmNodeCount').innerText = pmPoints.length;
                
                // If this is the very first point, snap the laser head to it
                if(pmPoints.length === 1) {
                    laserHeadPos.x = pos.x; 
                    laserHeadPos.y = pos.y;
                    if(!pmAnimFrame) animateProjectionLaser();
                }
            }

            pmCanvas.addEventListener('mousemove', pmMoveDraw);
            pmCanvas.addEventListener('touchmove', pmMoveDraw, {passive: false});

            function pmMoveDraw(e) {
                if(!isPmDrawing) return;
                e.preventDefault();
                const pos = getPmCoords(e);
                
                // Optimization: Only save point if dragged far enough (e.g., 10px) to prevent array explosion
                const lastPt = pmPoints[pmPoints.length - 1];
                const dist = Math.hypot(pos.x - lastPt.x, pos.y - lastPt.y);
                
                if(dist > 15) {
                    pmPoints.push(pos);
                    document.getElementById('pmNodeCount').innerText = pmPoints.length;
                }
            }

            window.addEventListener('mouseup', () => isPmDrawing = false);
            window.addEventListener('touchend', () => isPmDrawing = false);

            function clearProjectionMap() {
                if(typeof playTap === 'function') playTap();
                pmPoints = [];
                currentTargetIdx = 0;
                if(pmCtx) pmCtx.clearRect(0, 0, pmCanvas.width, pmCanvas.height);
                document.getElementById('pmNodeCount').innerText = '0';
            }

            function animateProjectionLaser() {
                if(pmPoints.length === 0) {
                    pmAnimFrame = null;
                    return;
                }
                pmAnimFrame = requestAnimationFrame(animateProjectionLaser);

                // Constant fade for motion blur / laser trail effect
                pmCtx.fillStyle = 'rgba(0, 0, 0, 0.1)';
                pmCtx.fillRect(0, 0, pmCanvas.width, pmCanvas.height);

                // Draw the static skeleton path faintly
                if(pmPoints.length > 1) {
                    pmCtx.beginPath();
                    pmCtx.strokeStyle = 'rgba(0, 229, 255, 0.1)';
                    pmCtx.lineWidth = 1;
                    pmCtx.moveTo(pmPoints[0].x, pmPoints[0].y);
                    for(let i=1; i<pmPoints.length; i++) {
                        pmCtx.lineTo(pmPoints[i].x, pmPoints[i].y);
                    }
                    // Connect end to start
                    pmCtx.lineTo(pmPoints[0].x, pmPoints[0].y);
                    pmCtx.stroke();
                }

                // AI Autonomous Laser Head Movement
                if(pmPoints.length > 1) {
                    const target = pmPoints[currentTargetIdx];
                    const speed = parseInt(document.getElementById('pmSpeed').value) || 8;
                    
                    const dx = target.x - laserHeadPos.x;
                    const dy = target.y - laserHeadPos.y;
                    const dist = Math.hypot(dx, dy);

                    if(dist < speed) {
                        // Snap to target and queue next point
                        laserHeadPos.x = target.x;
                        laserHeadPos.y = target.y;
                        currentTargetIdx = (currentTargetIdx + 1) % pmPoints.length; // Infinite loop
                    } else {
                        // Move towards target
                        laserHeadPos.x += (dx / dist) * speed;
                        laserHeadPos.y += (dy / dist) * speed;
                    }

                    // Render Glowing Laser Head
                    pmCtx.globalCompositeOperation = 'lighter';
                    pmCtx.beginPath();
                    pmCtx.arc(laserHeadPos.x, laserHeadPos.y, 4, 0, Math.PI * 2);
                    pmCtx.fillStyle = '#fff';
                    pmCtx.shadowBlur = 15;
                    pmCtx.shadowColor = 'var(--cyan-neon)';
                    pmCtx.fill();
                    pmCtx.globalCompositeOperation = 'source-over';
                    pmCtx.shadowBlur = 0; // reset
                }
            }


            // --- 3. ZERO-GRAVITY BASS DROP PROTOCOL ---
            let isNukeActive = false;
            let nukeAudioCtx = null;

            function initiateNukeDrop() {
                if(isNukeActive) return;
                isNukeActive = true;
                
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(100); // Startup thump

                const overlay = document.getElementById('bassDropOverlay');
                const timerEl = document.getElementById('bdCountdown');
                const textEl = document.getElementById('bdText');
                
                // Reset UI
                timerEl.innerText = "3";
                timerEl.style.color = "var(--red-alert)";
                timerEl.style.fontSize = "160px";
                textEl.style.display = "block";
                
                overlay.style.display = 'flex';
                // Trigger layout reflow for fade in
                void overlay.offsetWidth; 
                overlay.style.opacity = '1';

                // Attempt to generate synthetic riser audio securely
                try {
                    const AudioContext = window.AudioContext || window.webkitAudioContext;
                    nukeAudioCtx = new AudioContext();
                    
                    // Riser (Pitch going up)
                    const rOsc = nukeAudioCtx.createOscillator();
                    const rGain = nukeAudioCtx.createGain();
                    rOsc.type = 'sawtooth';
                    rOsc.frequency.setValueAtTime(50, nukeAudioCtx.currentTime);
                    rOsc.frequency.exponentialRampToValueAtTime(1000, nukeAudioCtx.currentTime + 3);
                    
                    rOsc.connect(rGain);
                    rGain.connect(nukeAudioCtx.destination);
                    
                    rGain.gain.setValueAtTime(0.1, nukeAudioCtx.currentTime);
                    rGain.gain.exponentialRampToValueAtTime(1.0, nukeAudioCtx.currentTime + 3);
                    
                    rOsc.start();
                    rOsc.stop(nukeAudioCtx.currentTime + 3);
                } catch(e) { console.log("Audio blocked or unsupported."); }

                // Countdown Loop
                let count = 3;
                const interval = setInterval(() => {
                    count--;
                    if(count > 0) {
                        timerEl.innerText = count;
                        if(navigator.vibrate) navigator.vibrate(100);
                    } else {
                        clearInterval(interval);
                        executePhysicalDrop(timerEl, textEl);
                    }
                }, 1000);
            }

            function executePhysicalDrop(timerEl, textEl) {
                // UI Explosion
                timerEl.innerText = "BOOM";
                timerEl.style.color = "#fff";
                timerEl.style.fontSize = "100px";
                textEl.style.display = "none";

                // Physical Screen Shake CSS Class
                document.body.classList.add('nuke-mode');
                
                // Massive Haptic Pattern
                if(navigator.vibrate) navigator.vibrate([500, 100, 500, 100, 800]);

                // The Deep Sub-Bass Audio Hit
                if(nukeAudioCtx) {
                    const bOsc = nukeAudioCtx.createOscillator();
                    const bGain = nukeAudioCtx.createGain();
                    bOsc.type = 'sine';
                    // Punchy drop from 120hz to 20hz
                    bOsc.frequency.setValueAtTime(150, nukeAudioCtx.currentTime);
                    bOsc.frequency.exponentialRampToValueAtTime(20, nukeAudioCtx.currentTime + 2.5);
                    
                    // Add massive distortion using the math function from Part 3 if available
                    // If not, we just play loud clean bass
                    if(typeof makeDistCurve === 'function') {
                        const dist = nukeAudioCtx.createWaveShaper();
                        dist.curve = makeDistCurve(100); 
                        bOsc.connect(dist);
                        dist.connect(bGain);
                    } else {
                        bOsc.connect(bGain);
                    }
                    
                    bGain.connect(nukeAudioCtx.destination);
                    bGain.gain.setValueAtTime(2.0, nukeAudioCtx.currentTime);
                    bGain.gain.exponentialRampToValueAtTime(0.01, nukeAudioCtx.currentTime + 2.5);
                    
                    bOsc.start();
                    bOsc.stop(nukeAudioCtx.currentTime + 2.5);
                }

                // Cleanup and Return to Normal after 3 seconds
                setTimeout(() => {
                    document.body.classList.remove('nuke-mode');
                    const overlay = document.getElementById('bassDropOverlay');
                    overlay.style.opacity = '0'; // Fade out
                    
                    setTimeout(() => { 
                        overlay.style.display = 'none'; 
                        isNukeActive = false;
                    }, 500); // Wait for fade out
                }, 2800);
            }
        </script>
        <style>
            .vault-wrapper {
                background: linear-gradient(180deg, #050508, #111);
                border: 1px solid #222;
                border-radius: 12px;
                padding: 30px 20px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 30px rgba(0, 229, 255, 0.05);
                display: flex;
                flex-direction: column;
                align-items: center;
                text-align: center;
            }

            /* Fingerprint Scanner UI */
            .scanner-container {
                position: relative;
                width: 140px;
                height: 140px;
                margin: 20px auto;
                display: flex;
                justify-content: center;
                align-items: center;
                cursor: pointer;
                /* Crucial to prevent magnifier glass or selection on mobile long-press */
                user-select: none; -webkit-user-select: none; touch-action: none;
            }

            .scanner-ring {
                position: absolute; inset: 0; border-radius: 50%;
                border: 2px dashed rgba(0, 229, 255, 0.3); transition: 0.3s; pointer-events: none;
            }
            .sr-1 { inset: 5px; border-style: solid; border-color: rgba(0, 229, 255, 0.1); border-top-color: var(--cyan-neon); animation: spin 4s linear infinite; }
            .sr-2 { inset: 15px; border-style: dotted; border-color: rgba(212, 175, 55, 0.5); animation: spin 6s linear infinite reverse; }

            .fp-icon {
                font-size: 50px; color: rgba(0, 229, 255, 0.4);
                position: relative; z-index: 2; transition: 0.3s; text-shadow: 0 0 10px rgba(0, 229, 255, 0.1);
            }

            /* SVG Progress Ring */
            .scan-svg {
                position: absolute; inset: -10px; width: calc(100% + 20px); height: calc(100% + 20px);
                transform: rotate(-90deg); pointer-events: none; z-index: 3;
            }
            .scan-circle {
                fill: none; stroke: #00ff00; stroke-width: 4;
                stroke-dasharray: 471; /* 2 * PI * r (r=75) */
                stroke-dashoffset: 471; transition: stroke-dashoffset 0.1s linear;
                stroke-linecap: round; filter: drop-shadow(0 0 5px #00ff00);
            }

            .vault-status-txt { font-family: 'Courier New', monospace; color: var(--gold-primary); font-size: 11px; height: 15px; font-weight: bold;}

            /* Hidden Content */
            .vault-content { display: none; width: 100%; animation: fadeIn 0.5s ease-out; margin-top: 20px; }
            .vault-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-top: 20px; }
            .v-doc {
                background: rgba(255,255,255,0.05); border: 1px solid #333; border-radius: 8px; padding: 15px 5px;
                display: flex; flex-direction: column; align-items: center; gap: 8px; transition: 0.2s; cursor: pointer;
            }
            .v-doc:active { background: rgba(212,175,55,0.15); border-color: var(--gold-primary); transform: scale(0.95); }
            .v-doc i { font-size: 20px; color: var(--gold-primary); }
            .v-doc span { font-size: 9px; font-family: var(--font-tech); color: #fff; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">SECURE CLIENT VAULT</h2>
                <div class="section-icon"><i class="fas fa-fingerprint"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 10px; text-align: center;">Biometric authorization required to access premium booking contracts.</p>

            <div class="vault-wrapper">
                <div id="vaultAuthView">
                    <h3 style="font-family:var(--font-tech); color:var(--cyan-neon); font-size:14px; letter-spacing:2px;">IDENTITY VERIFICATION</h3>
                    <p style="font-family:var(--font-data); color:#666; font-size:10px;">PRESS AND HOLD TO DECRYPT</p>

                    <div class="scanner-container" id="fpScannerPad" onmousedown="startVaultScan(event)" onmouseup="stopVaultScan(event)" onmouseleave="stopVaultScan(event)" ontouchstart="startVaultScan(event)" ontouchend="stopVaultScan(event)">
                        <div class="scanner-ring sr-1"></div>
                        <div class="scanner-ring sr-2"></div>
                        <i class="fas fa-fingerprint fp-icon" id="fpIconElement"></i>
                        <svg class="scan-svg"><circle class="scan-circle" id="scanProgressCircle" cx="80" cy="80" r="75"></circle></svg>
                    </div>
                    <div class="vault-status-txt" id="vaultStatusText">AWAITING INPUT...</div>
                </div>

                <div class="vault-content" id="vaultDataView">
                    <i class="fas fa-unlock-alt" style="font-size: 30px; color: #00ff00; margin-bottom: 10px; text-shadow: 0 0 15px rgba(0,255,0,0.5);"></i>
                    <h3 style="font-family:var(--font-head); color:#fff; font-size:18px;">ACCESS GRANTED</h3>
                    
                    <div class="vault-grid">
                        <div class="v-doc" onclick="triggerToast('Downloading Master Price List PDF...')"><i class="fas fa-file-invoice-dollar"></i><span>Master Pricing</span></div>
                        <div class="v-doc" onclick="triggerToast('Opening NDA & Terms...')"><i class="fas fa-file-signature"></i><span>Legal Terms</span></div>
                        <div class="v-doc" onclick="triggerToast('Downloading Setup Blueprints...')"><i class="fas fa-file-image"></i><span>Setup Blueprints</span></div>
                        <div class="v-doc" onclick="lockClientVault()" style="border-color: var(--red-alert);"><i class="fas fa-lock" style="color:var(--red-alert);"></i><span style="color:var(--red-alert);">Lock Vault</span></div>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .analyzer-wrapper {
                background: #0a0a0f;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: inset 0 0 20px rgba(0,0,0,0.8);
            }

            .mic-hud {
                display: flex; justify-content: space-between; align-items: center;
                background: #050505; border: 1px solid #111; padding: 15px; border-radius: 8px; margin-bottom: 15px;
            }
            .db-meter { text-align: center; }
            .db-val { font-family: var(--font-tech); font-size: 28px; font-weight: 900; color: #00ff00; text-shadow: 0 0 10px rgba(0,255,0,0.4); transition: 0.2s;}
            .db-lbl { font-family: var(--font-data); font-size: 9px; color: #888; letter-spacing: 1px; }

            .mic-canvas-box {
                width: 100%; height: 150px; background: #000; border: 1px solid #222; border-radius: 6px;
                position: relative; overflow: hidden; margin-bottom: 15px;
            }
            #micCanvas { width: 100%; height: 100%; display: block; }
            .mic-grid {
                position: absolute; inset: 0; pointer-events: none;
                background: linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px);
                background-size: 10px 10px;
            }

            .mic-verdict {
                padding: 12px; background: rgba(255,255,255,0.05); border-left: 3px solid var(--gold-primary);
                font-family: var(--font-body); font-size: 10px; color: #ccc; border-radius: 4px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">ENVIRONMENT ANALYZER</h2>
                <div class="section-icon"><i class="fas fa-microphone-alt"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Analyze your physical room's ambient noise to determine the necessary audio payload.</p>

            <div class="analyzer-wrapper">
                <div class="mic-hud">
                    <div class="db-meter">
                        <div class="db-val" id="dbReadout">--</div>
                        <div class="db-lbl">DECIBELS (dB)</div>
                    </div>
                    <div>
                        <button class="app-btn-outline" id="btnInitMic" onclick="toggleRoomAnalyzer()">
                            <i class="fas fa-rss"></i> INIT MIC
                        </button>
                    </div>
                </div>

                <div class="mic-canvas-box" id="micWrap">
                    <div class="mic-grid"></div>
                    <canvas id="micCanvas"></canvas>
                    <div style="position:absolute; top:5px; right:5px; color:#fff; font-family:var(--font-tech); font-size:8px; opacity:0.5;">REAL-TIME FFT</div>
                </div>

                <div class="mic-verdict" id="micVerdictTxt">
                    <strong>AWAITING SENSOR DATA...</strong> Please initialize the microphone to scan the room's acoustic profile.
                </div>
            </div>
        </div>

        <style>
            .hex-wrapper {
                background: #000;
                border: 1px solid #1a1a24;
                border-radius: 12px;
                padding: 20px;
                display: flex; flex-direction: column; align-items: center;
            }

            .hex-canvas-container {
                width: 260px; height: 260px; position: relative; margin: 20px auto;
            }
            #hexCanvas { width: 100%; height: 100%; display: block; }
            
            /* Absolute positioned labels around the radar */
            .hl { position: absolute; font-family: var(--font-tech); font-size: 9px; font-weight: bold; color: #aaa; transform: translate(-50%, -50%); white-space: nowrap; text-shadow: 0 2px 4px #000;}
            .hl-top { top: -5px; left: 50%; color: var(--gold-primary); }
            .hl-tr { top: 25%; left: 95%; }
            .hl-br { top: 75%; left: 95%; }
            .hl-bot { top: 105%; left: 50%; }
            .hl-bl { top: 75%; left: 5%; }
            .hl-tl { top: 25%; left: 5%; }

            .hex-legend { display: flex; gap: 15px; margin-top: 15px; }
            .h-leg-item { display: flex; align-items: center; gap: 5px; font-family: var(--font-data); font-size: 10px; color: #fff; }
            .h-leg-dot { width: 10px; height: 10px; border-radius: 50%; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">COMPETITIVE METRICS</h2>
                <div class="section-icon"><i class="fas fa-spider"></i></div>
            </div>

            <div class="hex-wrapper">
                <div class="hex-canvas-container" id="hexWrap">
                    <canvas id="hexCanvas"></canvas>
                    <span class="hl hl-top">SPL (BASS)</span>
                    <span class="hl hl-tr">LASER DENSITY</span>
                    <span class="hl hl-br">STRUCTURAL INT.</span>
                    <span class="hl hl-bot">POWER RELIABILITY</span>
                    <span class="hl hl-bl">CREW SPEED</span>
                    <span class="hl hl-tl">AESTHETICS</span>
                </div>
                
                <div class="hex-legend">
                    <div class="h-leg-item"><div class="h-leg-dot" style="background:var(--gold-primary); box-shadow:0 0 10px var(--gold-primary);"></div> MND PRESTIGE</div>
                    <div class="h-leg-item"><div class="h-leg-dot" style="background:rgba(100,100,100,0.5);"></div> STANDARD DJ</div>
                </div>
            </div>
        </div>

        <script>
            // --- 1. BIOMETRIC CLIENT VAULT LOGIC ---
            let vaultScanTimer = null;
            let vaultProgress = 0;
            const maxScanOffset = 471; // Match stroke-dasharray in CSS
            let isVaultUnlocked = false;

            function startVaultScan(e) {
                if(isVaultUnlocked) return;
                e.preventDefault(); // Stop mobile highlight
                
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                
                const statusTxt = document.getElementById('vaultStatusText');
                const fpIcon = document.getElementById('fpIconElement');
                const scanCircle = document.getElementById('scanProgressCircle');
                
                statusTxt.innerText = "ANALYZING BIOMETRICS...";
                statusTxt.style.color = "var(--cyan-neon)";
                fpIcon.style.color = "var(--cyan-neon)";
                fpIcon.style.textShadow = "0 0 20px var(--cyan-neon)";
                
                vaultScanTimer = setInterval(() => {
                    vaultProgress += 2.5; // Unlock speed
                    const offset = maxScanOffset - ((vaultProgress / 100) * maxScanOffset);
                    scanCircle.style.strokeDashoffset = offset;
                    
                    if(vaultProgress >= 100) {
                        unlockClientVault();
                    }
                }, 30); // 30ms interval
            }

            function stopVaultScan(e) {
                if(isVaultUnlocked) return;
                e.preventDefault();
                clearInterval(vaultScanTimer);
                vaultProgress = 0;
                
                const scanCircle = document.getElementById('scanProgressCircle');
                const statusTxt = document.getElementById('vaultStatusText');
                const fpIcon = document.getElementById('fpIconElement');
                
                scanCircle.style.strokeDashoffset = maxScanOffset; // Reset
                statusTxt.innerText = "SCAN ABORTED.";
                statusTxt.style.color = "var(--red-alert)";
                fpIcon.style.color = "rgba(0, 229, 255, 0.4)";
                fpIcon.style.textShadow = "none";
                
                setTimeout(() => { 
                    if(!isVaultUnlocked) { 
                        statusTxt.innerText = "AWAITING INPUT..."; 
                        statusTxt.style.color = "var(--gold-primary)"; 
                    }
                }, 1000);
            }

            function unlockClientVault() {
                clearInterval(vaultScanTimer);
                isVaultUnlocked = true;
                
                if(navigator.vibrate) navigator.vibrate([100, 50, 200]);
                if(typeof playSynth === 'function') playSynth('chordMaj', null); // Success sound from Part 3
                
                document.getElementById('vaultAuthView').style.display = 'none';
                document.getElementById('vaultDataView').style.display = 'block';
                if(typeof triggerToast === 'function') triggerToast("Security clearance accepted.");
            }

            function lockClientVault() {
                if(typeof playTap === 'function') playTap();
                isVaultUnlocked = false;
                vaultProgress = 0;
                
                document.getElementById('scanProgressCircle').style.strokeDashoffset = maxScanOffset;
                document.getElementById('vaultAuthView').style.display = 'block';
                document.getElementById('vaultDataView').style.display = 'none';
                
                const statusTxt = document.getElementById('vaultStatusText');
                statusTxt.innerText = "VAULT SECURED.";
                setTimeout(() => { statusTxt.innerText = "AWAITING INPUT..."; }, 2000);
            }

            // --- 2. ACOUSTIC ROOM ANALYZER (Mic API) ---
            let audioStream = null;
            let micAudioCtx = null;
            let micAnalyser = null;
            let micDataArray = null;
            const mCanvas = document.getElementById('micCanvas');
            let mCtx = null;
            let micAnimFrame = null;
            let isMicOn = false;

            function initMicCanvas() {
                const wrap = document.getElementById('micWrap');
                if(wrap && mCanvas) {
                    mCanvas.width = wrap.clientWidth;
                    mCanvas.height = wrap.clientHeight;
                    mCtx = mCanvas.getContext('2d');
                }
            }
            window.addEventListener('resize', initMicCanvas);
            setTimeout(initMicCanvas, 500);

            async function toggleRoomAnalyzer() {
                if(typeof playTap === 'function') playTap();
                const btn = document.getElementById('btnInitMic');
                const verdict = document.getElementById('micVerdictTxt');
                
                if(!isMicOn) {
                    try {
                        btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> CONNECTING...';
                        
                        // Request Hardware Access
                        audioStream = await navigator.mediaDevices.getUserMedia({ audio: true, video: false });
                        
                        const AudioContext = window.AudioContext || window.webkitAudioContext;
                        micAudioCtx = new AudioContext();
                        const source = micAudioCtx.createMediaStreamSource(audioStream);
                        
                        micAnalyser = micAudioCtx.createAnalyser();
                        micAnalyser.fftSize = 256;
                        source.connect(micAnalyser); 
                        // IMPORTANT: DO NOT connect to destination to avoid horrible feedback loop!
                        
                        micDataArray = new Uint8Array(micAnalyser.frequencyBinCount);
                        
                        isMicOn = true;
                        btn.innerHTML = '<i class="fas fa-stop"></i> HALT SCAN';
                        btn.style.color = 'var(--red-alert)'; btn.style.borderColor = 'var(--red-alert)';
                        
                        processMicAudio();
                        if(typeof triggerToast === 'function') triggerToast("Acoustic Sensors Online.");
                        
                    } catch(err) {
                        console.error(err);
                        btn.innerHTML = '<i class="fas fa-exclamation-triangle"></i> ACCESS DENIED';
                        verdict.innerHTML = "<strong style='color:var(--red-alert);'>ERROR:</strong> Microphone permission denied. Cannot analyze room acoustics.";
                        setTimeout(() => { btn.innerHTML = '<i class="fas fa-rss"></i> INIT MIC'; }, 3000);
                    }
                } else {
                    // Shutdown
                    isMicOn = false;
                    if(audioStream) audioStream.getTracks().forEach(track => track.stop());
                    if(micAudioCtx) micAudioCtx.close();
                    if(micAnimFrame) cancelAnimationFrame(micAnimFrame);
                    
                    if(mCtx) mCtx.clearRect(0, 0, mCanvas.width, mCanvas.height);
                    
                    document.getElementById('dbReadout').innerText = '--';
                    document.getElementById('dbReadout').style.color = '#00ff00';
                    btn.innerHTML = '<i class="fas fa-rss"></i> INIT MIC';
                    btn.style.color = 'var(--cyan-neon)'; btn.style.borderColor = 'var(--cyan-neon)';
                    verdict.innerHTML = "<strong>SCAN HALTED.</strong>";
                }
            }

            function processMicAudio() {
                if(!isMicOn || !mCtx) return;
                micAnimFrame = requestAnimationFrame(processMicAudio);
                
                micAnalyser.getByteFrequencyData(micDataArray);
                
                // Calculate average volume
                let sum = 0;
                for(let i=0; i<micDataArray.length; i++) { sum += micDataArray[i]; }
                const average = sum / micDataArray.length;
                
                // Map raw average (0-255) to a fake dB scale (30-120) for visual representation
                const db = Math.floor(30 + (average / 255) * 90); 
                const dbDisplay = document.getElementById('dbReadout');
                dbDisplay.innerText = db;
                
                const verdict = document.getElementById('micVerdictTxt');

                // Intelligent Feedback based on noise level
                if(db < 50) {
                    dbDisplay.style.color = 'var(--cyan-neon)';
                    verdict.innerHTML = "<strong>VERDICT: TOO QUIET.</strong> Absolute silence detected. Venue desperately requires MND heavy deployment to generate atmosphere.";
                } else if(db < 85) {
                    dbDisplay.style.color = '#00ff00';
                    verdict.innerHTML = "<strong>VERDICT: AMBIENT LEVEL.</strong> Normal conversation detected. Line-Array speakers recommended to overpower crowd noise.";
                } else {
                    dbDisplay.style.color = 'var(--red-alert)';
                    verdict.innerHTML = "<strong>VERDICT: ACOUSTIC SATURATION.</strong> Environment is loud. Maximum 21-inch Subwoofers required to penetrate the noise floor.";
                }

                // Draw FFT Spectrum
                mCtx.fillStyle = 'rgba(0, 0, 0, 0.3)'; // Motion fade
                mCtx.fillRect(0, 0, mCanvas.width, mCanvas.height);
                
                const barWidth = (mCanvas.width / micDataArray.length) * 2.5;
                let x = 0;
                
                for(let i = 0; i < micDataArray.length; i++) {
                    const barHeight = (micDataArray[i] / 255) * mCanvas.height;
                    
                    // Color maps from Cyan to Purple based on frequency
                    const r = barHeight + (25 * (i/micDataArray.length));
                    const g = 200 * (1 - i/micDataArray.length);
                    const b = 255;
                    
                    mCtx.fillStyle = `rgb(${r},${g},${b})`;
                    mCtx.fillRect(x, mCanvas.height - barHeight, barWidth, barHeight);
                    x += barWidth + 1;
                }
            }

            // --- 3. HEX-GRID PERFORMANCE ANALYTICS LOGIC ---
            const hCanvas = document.getElementById('hexCanvas');
            let hCtx = null;
            let hexAnimOffset = 0;

            function initHexChart() {
                const wrap = document.getElementById('hexWrap');
                if(!wrap || !hCanvas) return;
                
                // Fix DPI for sharp canvas rendering on mobile
                const dpr = window.devicePixelRatio || 1;
                const size = wrap.clientWidth;
                
                hCanvas.width = size * dpr;
                hCanvas.height = size * dpr;
                hCtx = hCanvas.getContext('2d');
                hCtx.scale(dpr, dpr);
                
                if(!window.hexIsRunning) {
                    window.hexIsRunning = true;
                    drawHexFrame();
                }
            }
            window.addEventListener('resize', initHexChart);
            setTimeout(initHexChart, 500);

            // Metric Data (0 to 100)
            const metricStandard = [50, 40, 60, 50, 70, 40]; // Normal DJ
            const metricMND = [95, 90, 100, 95, 85, 95];     // MND Pro

            // Helper to draw a regular polygon (the background web)
            function drawWebPolygon(cx, cy, radius, sides, ctx) {
                ctx.beginPath();
                for (let i = 0; i < sides; i++) {
                    const angle = (Math.PI * 2 * i) / sides - Math.PI / 2; // Start at top
                    const x = cx + radius * Math.cos(angle);
                    const y = cy + radius * Math.sin(angle);
                    if (i === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);
                }
                ctx.closePath();
                ctx.strokeStyle = 'rgba(255,255,255,0.1)';
                ctx.lineWidth = 1;
                ctx.stroke();
            }

            // Helper to draw the actual data shape
            function drawDataPolygon(cx, cy, maxRadius, dataArr, ctx, color, isGlowing) {
                ctx.beginPath();
                for (let i = 0; i < 6; i++) {
                    const angle = (Math.PI * 2 * i) / 6 - Math.PI / 2;
                    
                    // Add slight sine wave animation to the MND data points to make it "breathe"
                    const animVariance = isGlowing ? Math.sin(hexAnimOffset + i) * 3 : 0;
                    let val = dataArr[i] + animVariance;
                    if(val > 100) val = 100;
                    
                    const r = (val / 100) * maxRadius;
                    const x = cx + r * Math.cos(angle);
                    const y = cy + r * Math.sin(angle);
                    
                    if (i === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);
                }
                ctx.closePath();
                
                if(isGlowing) {
                    ctx.fillStyle = 'rgba(212,175,55,0.3)';
                    ctx.shadowBlur = 15; 
                    ctx.shadowColor = color;
                } else {
                    ctx.fillStyle = 'rgba(100,100,100,0.3)';
                    ctx.shadowBlur = 0;
                }
                
                ctx.fill();
                ctx.lineWidth = 2;
                ctx.strokeStyle = color;
                ctx.stroke();
                ctx.shadowBlur = 0; // reset
            }

            function drawHexFrame() {
                requestAnimationFrame(drawHexFrame);
                if(!hCtx) return;
                
                hexAnimOffset += 0.05;

                // Canvas CSS size is 260x260, so center is 130
                const cx = 130; 
                const cy = 130; 
                const maxR = 100; // Max radius fits inside 260
                
                hCtx.clearRect(0,0, 260, 260);

                // 1. Draw 5 Background Web Rings
                for(let i=1; i<=5; i++) {
                    drawWebPolygon(cx, cy, maxR * (i/5), 6, hCtx);
                }
                
                // 2. Draw Spokes connecting center to corners
                hCtx.strokeStyle = 'rgba(255,255,255,0.1)';
                for (let i = 0; i < 6; i++) {
                    const angle = (Math.PI * 2 * i) / 6 - Math.PI / 2;
                    hCtx.beginPath(); 
                    hCtx.moveTo(cx, cy);
                    hCtx.lineTo(cx + maxR * Math.cos(angle), cy + maxR * Math.sin(angle));
                    hCtx.stroke();
                }

                // 3. Draw Data
                drawDataPolygon(cx, cy, maxR, metricStandard, hCtx, '#888', false);
                
                // Read CSS variable for gold primary in case vibe was changed
                const rootStyles = getComputedStyle(document.documentElement);
                const currentGold = rootStyles.getPropertyValue('--gold-primary').trim() || '#D4AF37';
                
                drawDataPolygon(cx, cy, maxR, metricMND, hCtx, currentGold, true);
            }
        </script>
        <style>
            .spatial-audio-wrapper {
                background: #020408;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            }

            .spatial-room {
                width: 100%;
                height: 260px;
                background: linear-gradient(180deg, #050a15, #000);
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                /* Prevent scrolling while dragging nodes */
                touch-action: none;
                box-shadow: inset 0 0 40px rgba(0, 229, 255, 0.1);
            }
            
            /* Virtual Floor Grid */
            .spatial-room::before {
                content: ''; position: absolute; inset: 0;
                background-image: 
                    linear-gradient(rgba(0, 229, 255, 0.1) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(0, 229, 255, 0.1) 1px, transparent 1px);
                background-size: 20px 20px; pointer-events: none;
            }

            /* Draggable Nodes */
            .spatial-node {
                position: absolute;
                width: 34px; height: 34px;
                border-radius: 50%;
                display: flex; justify-content: center; align-items: center;
                font-size: 14px; cursor: grab; z-index: 10;
                transform: translate(-50%, -50%);
                transition: box-shadow 0.2s;
            }
            .spatial-node:active { cursor: grabbing; transform: translate(-50%, -50%) scale(1.1); }
            
            .node-speaker { background: #111; border: 2px solid var(--gold-primary); color: var(--gold-primary); box-shadow: 0 0 15px rgba(212,175,55,0.4); }
            .node-listener { background: #111; border: 2px solid #00ff00; color: #00ff00; box-shadow: 0 0 15px rgba(0,255,0,0.4); }

            /* Acoustic Waves Overlay */
            #spatialCanvas { position: absolute; inset: 0; width: 100%; height: 100%; pointer-events: none; z-index: 5; mix-blend-mode: screen; }

            .spatial-hud {
                display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-top: 15px;
            }
            .sp-stat { background: #0a0a10; border: 1px solid #222; border-radius: 6px; padding: 10px; text-align: center; }
            .sp-lbl { font-family: var(--font-tech); font-size: 8px; color: #888; display: block; margin-bottom: 5px; letter-spacing: 1px;}
            .sp-val { font-family: var(--font-data); font-size: 16px; color: #fff; font-weight: bold; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">SPATIAL AUDIO MAPPER</h2>
                <div class="section-icon"><i class="fas fa-headphones-alt"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Drag the Listener and Line-Arrays to calculate distance, panning, and SPL loss.</p>

            <div class="spatial-audio-wrapper">
                <div class="spatial-room" id="spatialRoom">
                    <canvas id="spatialCanvas"></canvas>
                    <div class="spatial-node node-speaker" id="spkLeft" style="left: 20%; top: 20%;"><i class="fas fa-speaker"></i></div>
                    <div class="spatial-node node-speaker" id="spkRight" style="left: 80%; top: 20%;"><i class="fas fa-speaker"></i></div>
                    <div class="spatial-node node-listener" id="spkListener" style="left: 50%; top: 80%;"><i class="fas fa-user"></i></div>
                </div>

                <div class="spatial-hud">
                    <div class="sp-stat">
                        <span class="sp-lbl">DISTANCE (L/R)</span>
                        <span class="sp-val" id="spDistVal">0.0m / 0.0m</span>
                    </div>
                    <div class="sp-stat">
                        <span class="sp-lbl">PANNING</span>
                        <span class="sp-val" id="spPanVal" style="color: var(--cyan-neon);">CENTER</span>
                    </div>
                    <div class="sp-stat">
                        <span class="sp-lbl">EST. SPL DROP</span>
                        <span class="sp-val" id="spSplVal" style="color: var(--red-alert);">-0 dB</span>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .spectrum-wrapper {
                background: #000;
                border: 1px solid #1a1a24;
                border-radius: 12px;
                padding: 15px;
                position: relative;
            }

            .spectrum-canvas-box {
                width: 100%;
                height: 180px;
                background: linear-gradient(180deg, #050505, #111);
                border: 1px solid #333;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 30px rgba(0,0,0,0.9);
            }
            #specCanvas { width: 100%; height: 100%; display: block; }
            
            .spec-hud {
                position: absolute; top: 10px; left: 10px; display: flex; flex-direction: column;
                pointer-events: none; z-index: 5;
            }
            .spec-title { font-family: var(--font-tech); font-size: 10px; font-weight: 900; color: var(--gold-primary); letter-spacing: 2px; text-shadow: 0 0 5px var(--gold-primary); }
            .spec-sub { font-family: var(--font-data); font-size: 9px; color: #aaa; margin-top: 2px; }

            .freq-labels {
                display: flex; justify-content: space-between; padding: 5px 10px;
                font-family: var(--font-tech); font-size: 8px; color: #555; border-top: 1px solid #222; margin-top: 5px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">MASTER SPECTRUM ANALYZER</h2>
                <div class="section-icon"><i class="fas fa-chart-bar"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Live 64-Band FFT Audio Visualizer. Hooks directly into the Web Audio Synth Engine.</p>

            <div class="spectrum-wrapper">
                <div class="spectrum-canvas-box" id="specWrap">
                    <div class="spec-hud">
                        <span class="spec-title">MASTER OUT (POST-FX)</span>
                        <span class="spec-sub" id="specStatusTxt">AWAITING ENGINE BOOT...</span>
                    </div>
                    <canvas id="specCanvas"></canvas>
                </div>
                <div class="freq-labels">
                    <span>20Hz</span><span>SUB</span><span>LOW</span><span>MID</span><span>HIGH</span><span>AIR</span><span>20kHz</span>
                </div>
            </div>
        </div>

        <style>
            .plotter-wrapper {
                background: #020202;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .plotter-inputs {
                display: flex; gap: 10px; margin-bottom: 15px;
            }
            .plot-input-group {
                flex: 1; background: #0a0a0f; border: 1px solid #333; border-radius: 8px; padding: 10px;
            }
            .plot-lbl { font-family: var(--font-data); font-size: 9px; color: #888; display: block; margin-bottom: 5px; text-transform: uppercase;}
            .plot-input {
                width: 100%; background: transparent; border: none; border-bottom: 1px solid var(--cyan-neon);
                color: #fff; font-family: var(--font-tech); font-size: 16px; outline: none; text-align: center; padding-bottom: 5px;
            }

            .plotter-canvas-container {
                width: 100%;
                height: 300px;
                background: #001122; /* Blueprint Blue */
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            /* Blueprint Grid */
            .plotter-canvas-container::before {
                content: ''; position: absolute; inset: 0;
                background-image: 
                    linear-gradient(rgba(255, 255, 255, 0.1) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(255, 255, 255, 0.1) 1px, transparent 1px);
                background-size: 25px 25px; pointer-events: none; z-index: 1;
            }
            #plotCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2; }

            .plot-stats {
                display: flex; justify-content: space-between; margin-top: 15px; padding: 10px;
                background: rgba(0,229,255,0.05); border-radius: 6px; border: 1px dashed var(--cyan-neon);
            }
            .pst-item { font-family: var(--font-data); font-size: 10px; color: var(--cyan-neon); font-weight: bold;}
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">AI LIGHTING PLOTTER</h2>
                <div class="section-icon"><i class="fas fa-project-diagram"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Enter venue dimensions to procedurally generate a top-down DMX rigging schematic.</p>

            <div class="plotter-wrapper">
                <div class="plotter-inputs">
                    <div class="plot-input-group">
                        <span class="plot-lbl">VENUE LENGTH (M)</span>
                        <input type="number" class="plot-input" id="venueL" value="30" onchange="generatePlot()">
                    </div>
                    <div class="plot-input-group">
                        <span class="plot-lbl">VENUE WIDTH (M)</span>
                        <input type="number" class="plot-input" id="venueW" value="20" onchange="generatePlot()">
                    </div>
                </div>

                <button class="app-btn-primary" style="margin-bottom: 15px;" onclick="generatePlot()">
                    <i class="fas fa-cogs"></i> GENERATE BLUEPRINT
                </button>

                <div class="plotter-canvas-container" id="plotWrap">
                    <div style="position:absolute; bottom:10px; right:10px; font-family:var(--font-tech); font-size:8px; color:rgba(255,255,255,0.5); z-index:5;">TOP-DOWN VIEW</div>
                    <canvas id="plotCanvas"></canvas>
                </div>

                <div class="plot-stats">
                    <span class="pst-item" id="pstTruss">TRUSS: 0m</span>
                    <span class="pst-item" id="pstMovers">MOVING HEADS: 0</span>
                    <span class="pst-item" id="pstPars">LED PARS: 0</span>
                </div>
            </div>
        </div>

        <script>
            // --- 1. 3D SPATIAL AUDIO MAPPER LOGIC ---
            const spRoom = document.getElementById('spatialRoom');
            const spCanvas = document.getElementById('spatialCanvas');
            let spCtx = null;
            const nodes = document.querySelectorAll('.spatial-node');
            
            let activeSpatialNode = null;
            let spAnimFrame = null;
            let spWaveTime = 0;

            function initSpatialEngine() {
                if(!spRoom || !spCanvas) return;
                spCanvas.width = spRoom.clientWidth;
                spCanvas.height = spRoom.clientHeight;
                spCtx = spCanvas.getContext('2d');
                animateSpatialWaves();
                calculateAcoustics();
            }
            window.addEventListener('resize', initSpatialEngine);
            setTimeout(initSpatialEngine, 800);

            // Drag Logic for Nodes
            nodes.forEach(node => {
                node.addEventListener('mousedown', spDragStart);
                node.addEventListener('touchstart', (e) => { e.preventDefault(); spDragStart(e); }, {passive: false});
            });

            function spDragStart(e) {
                if(typeof playTap === 'function') playTap();
                activeSpatialNode = e.currentTarget;
            }

            document.addEventListener('mousemove', spDragMove);
            document.addEventListener('touchmove', spDragMove, {passive: false});

            function spDragMove(e) {
                if (!activeSpatialNode) return;
                e.preventDefault();
                
                const rect = spRoom.getBoundingClientRect();
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                
                let x = touch.clientX - rect.left;
                let y = touch.clientY - rect.top;
                
                // Clamp to box bounds
                if(x < 17) x = 17; if(x > rect.width - 17) x = rect.width - 17;
                if(y < 17) y = 17; if(y > rect.height - 17) y = rect.height - 17;

                activeSpatialNode.style.left = `${x}px`;
                activeSpatialNode.style.top = `${y}px`;
                
                calculateAcoustics();
            }

            document.addEventListener('mouseup', () => activeSpatialNode = null);
            document.addEventListener('touchend', () => activeSpatialNode = null);

            function calculateAcoustics() {
                const sl = document.getElementById('spkLeft');
                const sr = document.getElementById('spkRight');
                const list = document.getElementById('spkListener');
                
                if(!sl || !sr || !list) return;

                // Get pixel coordinates
                const getCoords = (el) => {
                    return { x: parseFloat(el.style.left), y: parseFloat(el.style.top) };
                };
                
                const pl = getCoords(sl);
                const pr = getCoords(sr);
                const pList = getCoords(list);

                // Assuming 10 pixels = 1 meter
                const pxToMeters = 0.1; 
                
                const distL = Math.hypot(pList.x - pl.x, pList.y - pl.y) * pxToMeters;
                const distR = Math.hypot(pList.x - pr.x, pList.y - pr.y) * pxToMeters;
                
                document.getElementById('spDistVal').innerText = `${distL.toFixed(1)}m / ${distR.toFixed(1)}m`;

                // Panning Calculation (-1.0 to 1.0)
                // If listener is perfectly between them on X axis, pan is 0.
                const centerX = (pl.x + pr.x) / 2;
                const panRaw = (pList.x - centerX) / (Math.abs(pr.x - pl.x) || 1); // Avoid div by zero
                let panClamp = Math.max(-1, Math.min(1, panRaw * 2)); // Amplify pan effect
                
                let panText = "CENTER";
                if(panClamp < -0.1) panText = `L ${Math.round(Math.abs(panClamp)*100)}%`;
                else if(panClamp > 0.1) panText = `R ${Math.round(panClamp*100)}%`;
                
                const panEl = document.getElementById('spPanVal');
                panEl.innerText = panText;
                
                // Color code panning
                if(panClamp < -0.5 || panClamp > 0.5) panEl.style.color = "var(--red-alert)";
                else panEl.style.color = "var(--cyan-neon)";

                // SPL Drop Law: -6dB for every doubling of distance. 
                // Assume 1m is reference (0dB loss).
                const avgDist = (distL + distR) / 2;
                let splLoss = 0;
                if(avgDist > 1) {
                    splLoss = 20 * Math.log10(avgDist); // Acoustic physics formula
                }
                document.getElementById('spSplVal').innerText = `-${splLoss.toFixed(1)} dB`;
            }

            function animateSpatialWaves() {
                if(!spCtx) return;
                spAnimFrame = requestAnimationFrame(animateSpatialWaves);
                spCtx.clearRect(0,0, spCanvas.width, spCanvas.height);
                
                spWaveTime += 0.5;

                const sl = document.getElementById('spkLeft');
                const sr = document.getElementById('spkRight');
                if(!sl || !sr) return;

                const drawWaves = (x, y, color) => {
                    spCtx.strokeStyle = color;
                    spCtx.lineWidth = 1;
                    for(let i=0; i<4; i++) {
                        let r = (spWaveTime + (i * 40)) % 200;
                        if(r > 0) {
                            spCtx.globalAlpha = 1 - (r / 200);
                            spCtx.beginPath();
                            spCtx.arc(x, y, r, 0, Math.PI*2);
                            spCtx.stroke();
                        }
                    }
                    spCtx.globalAlpha = 1.0;
                };

                drawWaves(parseFloat(sl.style.left), parseFloat(sl.style.top), 'var(--gold-primary)');
                drawWaves(parseFloat(sr.style.left), parseFloat(sr.style.top), 'var(--cyan-neon)');
                
                // Draw line of sight
                const list = document.getElementById('spkListener');
                spCtx.strokeStyle = 'rgba(255,255,255,0.1)';
                spCtx.setLineDash([5, 5]);
                spCtx.beginPath();
                spCtx.moveTo(parseFloat(sl.style.left), parseFloat(sl.style.top));
                spCtx.lineTo(parseFloat(list.style.left), parseFloat(list.style.top));
                spCtx.lineTo(parseFloat(sr.style.left), parseFloat(sr.style.top));
                spCtx.stroke();
                spCtx.setLineDash([]);
            }

            // --- 2. MASTER OUTPUT SPECTRUM ANALYZER LOGIC ---
            const specCanvas = document.getElementById('specCanvas');
            let specCtx = null;
            let specAnimFrame = null;
            let specAnalyser = null;
            let specDataArray = null;
            let simTime = 0; // For simulated noise

            function initSpectrum() {
                const wrap = document.getElementById('specWrap');
                if(!wrap || !specCanvas) return;
                specCanvas.width = wrap.clientWidth;
                specCanvas.height = wrap.clientHeight;
                specCtx = specCanvas.getContext('2d');
                
                // Check if audio engine from Part 3 is active and attach analyser
                if(typeof actx !== 'undefined' && actx && typeof masterGain !== 'undefined') {
                    if(!specAnalyser) {
                        specAnalyser = actx.createAnalyser();
                        specAnalyser.fftSize = 128; // 64 bins
                        specDataArray = new Uint8Array(specAnalyser.frequencyBinCount);
                        masterGain.connect(specAnalyser);
                        document.getElementById('specStatusTxt').innerText = "ENGINE SYNCED // LIVE FFT";
                        document.getElementById('specStatusTxt').style.color = "#00ff00";
                    }
                }
                
                if(!specAnimFrame) animateSpectrum();
            }
            window.addEventListener('resize', initSpectrum);
            
            // Poll for engine connection if booted later
            setInterval(() => {
                if(!specAnalyser && typeof actx !== 'undefined' && actx && actx.state === 'running') {
                    initSpectrum();
                }
            }, 2000);

            function animateSpectrum() {
                specAnimFrame = requestAnimationFrame(animateSpectrum);
                if(!specCtx) return;

                specCtx.fillStyle = '#050505';
                specCtx.fillRect(0, 0, specCanvas.width, specCanvas.height);

                const bins = 64;
                const barWidth = specCanvas.width / bins;
                
                if(specAnalyser && typeof isEngineOn !== 'undefined' && isEngineOn) {
                    // LIVE DATA from Web Audio API
                    specAnalyser.getByteFrequencyData(specDataArray);
                    
                    for(let i=0; i<bins; i++) {
                        const val = specDataArray[i]; // 0 to 255
                        const percent = val / 255;
                        const barHeight = percent * specCanvas.height;
                        
                        drawSpecBar(i, barWidth, barHeight, percent);
                    }
                } else {
                    // SIMULATED DATA (Idle Animation)
                    simTime += 0.05;
                    for(let i=0; i<bins; i++) {
                        // Create a pleasing ambient wave using Perlin-like math
                        let noise = Math.sin(i * 0.1 + simTime) * Math.cos(i * 0.05 - simTime*1.5);
                        noise = (noise + 1) / 2; // Normalize 0 to 1
                        // Keep it low
                        noise *= 0.3; 
                        
                        // Add some random flicker
                        if(Math.random() > 0.95) noise += 0.2;
                        
                        const barHeight = noise * specCanvas.height;
                        drawSpecBar(i, barWidth, barHeight, noise);
                    }
                }
            }

            function drawSpecBar(i, barWidth, barHeight, percent) {
                const x = i * barWidth;
                const y = specCanvas.height - barHeight;
                
                // Gradient based on frequency (Low = Red, Mid = Gold, High = Cyan)
                let r = 255, g = 0, b = 0;
                if(i < 20) { r=255; g=51; b=51; } // Bass
                else if (i < 40) { r=212; g=175; b=55; } // Mids
                else { r=0; g=229; b=255; } // Highs
                
                specCtx.fillStyle = `rgba(${r},${g},${b}, 0.8)`;
                
                // Add a glow cap at the top
                specCtx.fillRect(x + 1, y, barWidth - 2, barHeight);
                
                specCtx.fillStyle = '#fff';
                specCtx.fillRect(x + 1, y, barWidth - 2, 2);
            }
            setTimeout(initSpectrum, 1000);


            // --- 3. GENERATIVE AI LIGHTING PLOTTER LOGIC ---
            const pCanvas = document.getElementById('plotCanvas');
            let pCtx = null;

            function initPlotter() {
                const wrap = document.getElementById('plotWrap');
                if(!wrap || !pCanvas) return;
                pCanvas.width = wrap.clientWidth;
                pCanvas.height = wrap.clientHeight;
                pCtx = pCanvas.getContext('2d');
                generatePlot();
            }
            window.addEventListener('resize', initPlotter);
            setTimeout(initPlotter, 1200);

            function generatePlot() {
                if(!pCtx) return;
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);

                const L = parseFloat(document.getElementById('venueL').value);
                const W = parseFloat(document.getElementById('venueW').value);
                
                if(isNaN(L) || isNaN(W) || L < 5 || W < 5) return;

                pCtx.clearRect(0,0, pCanvas.width, pCanvas.height);

                // Math to scale real-world meters to canvas pixels
                // We want to fit the whole room inside the canvas with padding
                const padding = 20;
                const usableW = pCanvas.width - (padding*2);
                const usableH = pCanvas.height - (padding*2);
                
                // Find scaling factor (pixels per meter)
                const scaleX = usableW / W;
                const scaleY = usableH / L;
                const scale = Math.min(scaleX, scaleY);
                
                // Center the drawing
                const drawW = W * scale;
                const drawH = L * scale;
                const offsetX = (pCanvas.width - drawW) / 2;
                const offsetY = (pCanvas.height - drawH) / 2;

                // 1. Draw Venue Boundary
                pCtx.strokeStyle = 'var(--cyan-neon)';
                pCtx.lineWidth = 2;
                pCtx.strokeRect(offsetX, offsetY, drawW, drawH);

                // Procedural Logic based on size
                // Stage is usually at the back (top of our drawing)
                const stageDepth = 5 * scale; // 5 meters deep
                const stageWidth = (W * 0.6) * scale; // 60% of room width
                const stageX = offsetX + (drawW - stageWidth) / 2;
                const stageY = offsetY;

                // Draw Stage
                pCtx.fillStyle = 'rgba(0, 229, 255, 0.1)';
                pCtx.fillRect(stageX, stageY, stageWidth, stageDepth);
                pCtx.strokeStyle = 'var(--gold-primary)';
                pCtx.strokeRect(stageX, stageY, stageWidth, stageDepth);

                // GENERATE TRUSS (Box over stage)
                pCtx.strokeStyle = '#888';
                pCtx.lineWidth = 3;
                pCtx.setLineDash([2, 2]); // Simulate scaffold look
                
                // Front truss, back truss, left, right
                pCtx.strokeRect(stageX - (1*scale), stageY - (1*scale), stageWidth + (2*scale), stageDepth + (2*scale));
                pCtx.setLineDash([]);

                let moverCount = 0;
                let parCount = 0;
                let trussMeters = (W*0.6 + 2) * 2 + (5 + 2) * 2; // perimeter

                // Helper to draw lights
                const drawMover = (x,y) => {
                    pCtx.fillStyle = '#fff';
                    pCtx.beginPath(); pCtx.arc(x,y, 4, 0, Math.PI*2); pCtx.fill();
                    // Draw tiny beam
                    pCtx.fillStyle = 'rgba(255,255,255,0.2)';
                    pCtx.beginPath(); pCtx.moveTo(x,y); pCtx.lineTo(x-10, y+20); pCtx.lineTo(x+10, y+20); pCtx.fill();
                    moverCount++;
                };

                const drawPar = (x,y) => {
                    pCtx.fillStyle = 'var(--red-alert)';
                    pCtx.fillRect(x-3, y-3, 6, 6);
                    parCount++;
                };

                // Space lights evenly on front truss
                const frontTrussY = stageY + stageDepth + (1*scale);
                const frontTrussStartX = stageX - (1*scale);
                const frontTrussW = stageWidth + (2*scale);
                
                // 1 mover every 3 meters
                const numFrontMovers = Math.floor((frontTrussW / scale) / 3);
                const spacing = frontTrussW / (numFrontMovers + 1);

                for(let i=1; i<=numFrontMovers; i++) {
                    let lx = frontTrussStartX + (spacing * i);
                    drawMover(lx, frontTrussY);
                    // Add pars between movers
                    drawPar(lx - (spacing/2), frontTrussY);
                }
                drawPar(frontTrussStartX + frontTrussW - (spacing/2), frontTrussY);

                // Draw Back Truss Wash Lights
                const backTrussY = stageY - (1*scale);
                for(let i=1; i<=numFrontMovers + 2; i++) {
                    drawPar(frontTrussStartX + (frontTrussW / (numFrontMovers+3)) * i, backTrussY);
                }

                // Update UI Stats
                document.getElementById('pstTruss').innerText = `TRUSS: ${Math.round(trussMeters)}m`;
                document.getElementById('pstMovers').innerText = `SHARPY/MOVERS: ${moverCount}`;
                document.getElementById('pstPars').innerText = `LED PARS: ${parCount}`;
            }
        </script>
        <style>
            .raytrace-wrapper {
                background: #020202;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .ray-canvas-box {
                width: 100%;
                height: 250px;
                background: #000;
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 40px rgba(0, 229, 255, 0.1);
            }
            #rayCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Virtual Speaker Box */
            .ray-speaker {
                position: absolute;
                top: 50%; left: 50%; transform: translate(-50%, -50%);
                width: 20px; height: 30px; background: #111; border: 2px solid #555; border-radius: 2px;
                z-index: 5; display: flex; flex-direction: column; justify-content: space-evenly; align-items: center;
            }
            .ray-speaker::before, .ray-speaker::after {
                content: ''; width: 10px; height: 10px; background: #000; border-radius: 50%; border: 1px solid #333;
            }

            .ray-controls {
                margin-top: 15px; background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #222;
            }
            
            .ray-hud { display: flex; justify-content: space-between; margin-bottom: 10px; }
            .rh-item { font-family: var(--font-tech); font-size: 10px; color: var(--gold-primary); letter-spacing: 1px; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">ACOUSTIC RAY-TRACING AI</h2>
                <div class="section-icon"><i class="fas fa-satellite-dish"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate sound wave reflections (Reverb). Adjust wall absorption to see the effect of MND acoustic dampening.</p>

            <div class="raytrace-wrapper">
                <div class="ray-canvas-box" id="rayWrap">
                    <canvas id="rayCanvas"></canvas>
                    <div class="ray-speaker"></div>
                    <div style="position:absolute; top:10px; left:10px; color:#fff; font-family:var(--font-tech); font-size:8px; opacity:0.5;">TOP-DOWN BOUNCE PHYSICS</div>
                </div>

                <div class="ray-controls">
                    <div class="ray-hud">
                        <span class="rh-item">WALL ABSORPTION COEFFICIENT</span>
                        <span class="rh-item" style="color:var(--cyan-neon);" id="absorbValDisplay">10%</span>
                    </div>
                    <input type="range" class="app-slider" id="wallAbsorption" min="1" max="50" value="5" oninput="updateAbsorption(this.value)">
                    
                    <button class="app-btn-primary" style="margin-top: 15px; padding: 10px;" onclick="fireAcousticPulse()">
                        <i class="fas fa-bullhorn"></i> FIRE ACOUSTIC PULSE
                    </button>
                </div>
            </div>
        </div>

        <style>
            .cable-matrix-wrapper {
                background: linear-gradient(135deg, #050508, #111);
                border: 1px dashed #333;
                border-radius: 12px;
                padding: 15px;
            }

            .cable-input-grid {
                display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px;
            }
            .cab-group { display: flex; flex-direction: column; gap: 5px; }
            .cab-lbl { font-family: var(--font-data); font-size: 10px; color: #aaa; font-weight: bold; letter-spacing: 1px;}
            .cab-input {
                background: #000; border: 1px solid #444; border-radius: 6px; padding: 10px;
                color: #fff; font-family: var(--font-tech); font-size: 16px; text-align: center; outline: none;
            }
            .cab-input:focus { border-color: var(--gold-primary); box-shadow: 0 0 10px rgba(212,175,55,0.2); }

            .cable-results {
                background: #000; border-radius: 8px; border: 1px solid #222; overflow: hidden;
            }
            .cr-row {
                display: flex; justify-content: space-between; align-items: center;
                padding: 12px 15px; border-bottom: 1px solid #111;
            }
            .cr-row:last-child { border-bottom: none; }
            .cr-title { font-family: var(--font-body); font-size: 12px; color: #ccc; display: flex; align-items: center; gap: 10px; }
            .cr-val { font-family: var(--font-tech); font-size: 14px; font-weight: bold; color: var(--cyan-neon); }
            
            /* Specific cable colors */
            .cr-power { color: var(--red-alert); }
            .cr-signal { color: #00ff00; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">CABLE ROUTING MATRIX</h2>
                <div class="section-icon"><i class="fas fa-plug"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Calculate required wiring lengths and voltage drops from FOH (Front of House) to Main Stage.</p>

            <div class="cable-matrix-wrapper">
                <div class="cable-input-grid">
                    <div class="cab-group">
                        <span class="cab-lbl">FOH TO STAGE (M)</span>
                        <input type="number" class="cab-input" id="cabDist" value="45" oninput="calcCables()">
                    </div>
                    <div class="cab-group">
                        <span class="cab-lbl">LINE-ARRAY BOXES</span>
                        <input type="number" class="cab-input" id="cabBoxes" value="8" oninput="calcCables()">
                    </div>
                </div>

                <div class="cable-results">
                    <div class="cr-row">
                        <span class="cr-title"><i class="fas fa-bolt cr-power"></i> 6sqmm Power Core</span>
                        <span class="cr-val cr-power" id="resPower">0 m</span>
                    </div>
                    <div class="cr-row">
                        <span class="cr-title"><i class="fas fa-wave-square cr-signal"></i> XLR Audio Signal</span>
                        <span class="cr-val cr-signal" id="resXlr">0 m</span>
                    </div>
                    <div class="cr-row">
                        <span class="cr-title"><i class="fas fa-network-wired" style="color:var(--gold-primary);"></i> DMX Data Link</span>
                        <span class="cr-val" id="resDmx" style="color:var(--gold-primary);">0 m</span>
                    </div>
                    <div class="cr-row" style="background: rgba(255,255,255,0.05);">
                        <span class="cr-title">Est. Voltage Drop</span>
                        <span class="cr-val" id="resVdrop" style="color:#fff;">0.0 V</span>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .terrain-wrapper {
                background: #000;
                border: 2px solid #1a1a1a;
                border-radius: 12px;
                padding: 10px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.9);
            }

            .terrain-canvas-box {
                width: 100%;
                height: 200px;
                background: radial-gradient(circle at top center, #0a1122 0%, #000 100%);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #terrainCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .terrain-hud {
                position: absolute; bottom: 10px; left: 10px;
                font-family: var(--font-tech); font-size: 9px; color: #00e5ff; opacity: 0.7;
            }

            .terrain-controls { display: flex; gap: 10px; margin-top: 15px; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">3D FREQUENCY TERRAIN</h2>
                <div class="section-icon"><i class="fas fa-layer-group"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">A topological mapping of low-frequency oscillations passing through physical space.</p>

            <div class="terrain-wrapper">
                <div class="terrain-canvas-box" id="terrainWrap">
                    <canvas id="terrainCanvas"></canvas>
                    <div class="terrain-hud">Z-AXIS: OSCILLATING<br>GRID: 20x20 METERS</div>
                </div>

                <div class="terrain-controls">
                    <button class="app-btn-outline" style="flex:1; border-color:var(--gold-primary); color:var(--gold-primary);" onclick="adjustTerrainSpeed(0.02)">SLOW GROOVE</button>
                    <button class="app-btn-outline" style="flex:1; border-color:var(--red-alert); color:var(--red-alert);" onclick="adjustTerrainSpeed(0.1)">HEAVY BASS</button>
                </div>
            </div>
        </div>

        <script>
            // --- 1. ACOUSTIC RAY-TRACING AI LOGIC ---
            const rCanvas = document.getElementById('rayCanvas');
            let rCtx = null;
            const rWrap = document.getElementById('rayWrap');
            
            let acousticRays = [];
            let rayAnimFrame = null;
            let absorptionCoef = 0.05; // 5% energy lost per bounce

            function initRayTracer() {
                if(!rWrap || !rCanvas) return;
                rCanvas.width = rWrap.clientWidth;
                rCanvas.height = rWrap.clientHeight;
                rCtx = rCanvas.getContext('2d');
            }
            window.addEventListener('resize', initRayTracer);
            setTimeout(initRayTracer, 500);

            function updateAbsorption(val) {
                // Map slider (1-50) to a percentage multiplier (0.01 to 0.5)
                absorptionCoef = parseInt(val) / 100;
                document.getElementById('absorbValDisplay').innerText = `${val}%`;
            }

            class AcousticRay {
                constructor(cx, cy) {
                    this.x = cx;
                    this.y = cy;
                    // Random angle 0 to 360
                    const angle = Math.random() * Math.PI * 2;
                    const speed = Math.random() * 4 + 4; // High speed
                    this.vx = Math.cos(angle) * speed;
                    this.vy = Math.sin(angle) * speed;
                    this.energy = 1.0; // 100% life
                    this.history = [{x: cx, y: cy}]; // Trail for drawing
                }

                update(width, height) {
                    this.x += this.vx;
                    this.y += this.vy;

                    let bounced = false;

                    // Wall Collision (Bounce)
                    if (this.x <= 0 || this.x >= width) {
                        this.vx *= -1;
                        this.x = this.x <= 0 ? 0 : width; // Clamp
                        bounced = true;
                    }
                    if (this.y <= 0 || this.y >= height) {
                        this.vy *= -1;
                        this.y = this.y <= 0 ? 0 : height; // Clamp
                        bounced = true;
                    }

                    if (bounced) {
                        // Lose energy hitting the wall based on absorption slider
                        this.energy -= absorptionCoef;
                    }

                    // Keep a short history for the glowing trail
                    this.history.push({x: this.x, y: this.y});
                    if (this.history.length > 15) {
                        this.history.shift(); // Remove oldest
                    }
                }

                draw(ctx) {
                    if (this.energy <= 0) return;

                    ctx.beginPath();
                    for (let i = 0; i < this.history.length; i++) {
                        const pt = this.history[i];
                        if (i === 0) ctx.moveTo(pt.x, pt.y);
                        else ctx.lineTo(pt.x, pt.y);
                    }
                    
                    // Fades from cyan to dark blue as it loses energy
                    const alpha = Math.max(0, this.energy);
                    ctx.strokeStyle = `rgba(0, 229, 255, ${alpha})`;
                    ctx.lineWidth = 2;
                    ctx.stroke();
                }
            }

            function fireAcousticPulse() {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                
                // Clear existing
                acousticRays = [];
                
                // Start from center (virtual speaker)
                const cx = rCanvas.width / 2;
                const cy = rCanvas.height / 2;

                // Fire 60 rays in all directions
                for(let i=0; i<60; i++) {
                    acousticRays.push(new AcousticRay(cx, cy));
                }

                if(!rayAnimFrame) animateRays();
                
                // Play synth hit if audio engine active
                if(typeof playSynth === 'function') playSynth('kick', null);
            }

            function animateRays() {
                // Stop loop if all rays are dead to save CPU
                let activeRays = acousticRays.filter(r => r.energy > 0);
                if(activeRays.length === 0) {
                    rayAnimFrame = null;
                    // Final clear to fade out
                    rCtx.fillStyle = 'rgba(0,0,0,0.1)';
                    rCtx.fillRect(0, 0, rCanvas.width, rCanvas.height);
                    return;
                }

                rayAnimFrame = requestAnimationFrame(animateRays);

                // Heavy motion blur background
                rCtx.fillStyle = 'rgba(0, 0, 0, 0.3)';
                rCtx.fillRect(0, 0, rCanvas.width, rCanvas.height);

                rCtx.globalCompositeOperation = 'lighter';
                activeRays.forEach(ray => {
                    ray.update(rCanvas.width, rCanvas.height);
                    ray.draw(rCtx);
                });
                rCtx.globalCompositeOperation = 'source-over';
            }


            // --- 2. INDUSTRIAL CABLE ROUTING LOGIC ---
            function calcCables() {
                const distStr = document.getElementById('cabDist').value;
                const boxStr = document.getElementById('cabBoxes').value;
                
                let dist = parseFloat(distStr);
                let boxes = parseInt(boxStr);
                
                if(isNaN(dist)) dist = 0;
                if(isNaN(boxes)) boxes = 0;

                // Math Model:
                // Cable requires slack. Usually +20% for routing over/under truss and ground.
                const safeDistance = dist * 1.2;

                // 1. Power (Assuming 1 main heavy line to the stage distro, plus linking cables)
                const mainPower = safeDistance;
                const linkPower = boxes * 1.5; // 1.5m jumper between each box
                const totalPower = mainPower + linkPower;

                // 2. XLR Signal (Main L/R from FOH to Stage)
                const mainXlr = safeDistance * 2; // Need Left and Right lines
                const linkXlr = boxes * 1.5;
                const totalXlr = mainXlr + linkXlr;

                // 3. DMX (Single line daisy chained)
                const totalDmx = safeDistance + (boxes * 1.5);

                // 4. Voltage Drop Estimate (Physics)
                // V_drop = (2 * L * R * I) / 1000
                // Fake values: 6sqmm resistance is ~3 ohms/km. Assume 30 Amp load.
                const resistancePerM = 0.003; 
                const currentAmps = 30;
                const vDrop = 2 * dist * resistancePerM * currentAmps;

                // Update UI
                document.getElementById('resPower').innerText = `${Math.ceil(totalPower)} m`;
                document.getElementById('resXlr').innerText = `${Math.ceil(totalXlr)} m`;
                document.getElementById('resDmx').innerText = `${Math.ceil(totalDmx)} m`;
                
                const dropEl = document.getElementById('resVdrop');
                dropEl.innerText = `${vDrop.toFixed(1)} V`;
                
                // Color warn if voltage drop is too high (> 10V)
                if(vDrop > 10) dropEl.style.color = "var(--red-alert)";
                else if(vDrop > 5) dropEl.style.color = "var(--gold-primary)";
                else dropEl.style.color = "#00ff00";
            }
            
            // Init calc
            setTimeout(calcCables, 500);


            // --- 3. 3D FREQUENCY TERRAIN VISUALIZER LOGIC ---
            const tCanvas = document.getElementById('terrainCanvas');
            let tCtx = null;
            const tWrap = document.getElementById('terrainWrap');
            
            let terrAnimFrame = null;
            let terrainTime = 0;
            let terrainSpeed = 0.02;

            const cols = 20;
            const rows = 15;
            const scl = 25; // Scale of grid squares

            function initTerrain() {
                if(!tWrap || !tCanvas) return;
                tCanvas.width = tWrap.clientWidth;
                tCanvas.height = tWrap.clientHeight;
                tCtx = tCanvas.getContext('2d');
                if(!terrAnimFrame) animateTerrain();
            }
            window.addEventListener('resize', initTerrain);
            setTimeout(initTerrain, 800);

            function adjustTerrainSpeed(spd) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                terrainSpeed = spd;
                
                // If heavy bass is selected, spike the graph momentarily
                if(spd > 0.05 && typeof playSynth === 'function') {
                    playSynth('sub808', null);
                }
            }

            function animateTerrain() {
                terrAnimFrame = requestAnimationFrame(animateTerrain);
                if(!tCtx) return;

                tCtx.fillStyle = '#020205';
                tCtx.fillRect(0, 0, tCanvas.width, tCanvas.height);

                terrainTime += terrainSpeed;

                const w = tCanvas.width;
                const h = tCanvas.height;
                const cx = w / 2;
                
                // We want to project a 3D grid onto a 2D canvas manually.
                // Grid total width is cols * scl. Center it.
                const gridWidth = cols * scl;
                const offsetX = cx - (gridWidth / 2);
                
                // Y offset pushes the grid down into view
                const offsetY = h * 0.3; 

                tCtx.strokeStyle = 'rgba(0, 229, 255, 0.4)';
                tCtx.lineWidth = 1;

                // We generate a 2D array of Z-heights (elevation)
                let zValues = [];
                for (let y = 0; y < rows; y++) {
                    zValues[y] = [];
                    for (let x = 0; x < cols; x++) {
                        // The magic math: Combine two sine waves moving over time to create hills
                        // x * 0.3 creates horizontal ripples, y * 0.3 creates depth ripples
                        // terrainTime offsets it so it "moves" forward
                        let noise = Math.sin((x * 0.3) + terrainTime) * Math.cos((y * 0.3) - terrainTime);
                        // Increase height multiplier based on speed (heavy bass = taller waves)
                        let heightMult = terrainSpeed > 0.05 ? 40 : 15;
                        zValues[y][x] = noise * heightMult;
                    }
                }

                // Function to project 3D coordinate (x,y,z) to 2D screen
                function project(x, y, z) {
                    // Simple perspective math
                    const focalLength = 300;
                    // Y represents depth into the screen.
                    const depth = y * scl + 50; 
                    const scale = focalLength / depth;
                    
                    // Project X and Z
                    // x is horizontal, z is vertical (height)
                    const px = cx + ((x * scl) - (gridWidth / 2)) * scale;
                    const py = offsetY + (depth * 0.4) - (z * scale); // 0.4 tilts the floor
                    
                    return {px, py};
                }

                // Draw horizontal lines (Left to right)
                for (let y = 0; y < rows; y++) {
                    tCtx.beginPath();
                    for (let x = 0; x < cols; x++) {
                        const pt = project(x, y, zValues[y][x]);
                        if (x === 0) tCtx.moveTo(pt.px, pt.py);
                        else tCtx.lineTo(pt.px, pt.py);
                    }
                    tCtx.stroke();
                }

                // Draw vertical lines (Front to back)
                for (let x = 0; x < cols; x++) {
                    tCtx.beginPath();
                    for (let y = 0; y < rows; y++) {
                        const pt = project(x, y, zValues[y][x]);
                        if (y === 0) tCtx.moveTo(pt.px, pt.py);
                        else tCtx.lineTo(pt.px, pt.py);
                    }
                    tCtx.stroke();
                }
            }
        </script>
        <style>
            .cryo-wrapper {
                background: #05080c;
                border: 2px solid #111;
                border-radius: 12px;
                padding: 15px;
                box-shadow: inset 0 0 40px rgba(0, 229, 255, 0.05);
                position: relative;
            }

            .cryo-canvas-box {
                width: 100%;
                height: 250px;
                background: linear-gradient(180deg, #001122, #000);
                border-radius: 8px;
                border: 1px solid #1a3344;
                position: relative;
                overflow: hidden;
            }
            #cryoCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }
            
            /* Virtual Stage Box for Cannon Nozzle */
            .cryo-cannon-base {
                position: absolute; bottom: 0; left: 50%; transform: translateX(-50%);
                width: 60px; height: 20px; background: #222; border-top: 2px solid #555;
                border-radius: 4px 4px 0 0; z-index: 5; display: flex; justify-content: center;
            }
            .cryo-cannon-nozzle {
                width: 18px; height: 15px; background: #000; border: 1px solid #444; margin-top: -10px; border-radius: 2px;
            }

            .cryo-trigger-btn {
                width: 100%; height: 70px; margin-top: 20px;
                background: linear-gradient(180deg, #ffffff, #cccccc);
                border: 4px solid #fff; border-radius: 12px;
                color: #000; font-family: var(--font-tech); font-size: 24px; font-weight: 900; letter-spacing: 5px;
                cursor: pointer; box-shadow: 0 10px 20px rgba(255,255,255,0.2), inset 0 -5px 15px rgba(0,0,0,0.3);
                display: flex; justify-content: center; align-items: center; gap: 10px;
                user-select: none; touch-action: none; transition: 0.1s;
            }
            .cryo-trigger-btn:active {
                transform: translateY(5px);
                box-shadow: 0 2px 5px rgba(255,255,255,0.2), inset 0 5px 15px rgba(0,0,0,0.3);
                background: linear-gradient(180deg, #dddddd, #aaaaaa);
            }
            
            /* Global Freezing Screen Effect */
            body.frozen-screen::after {
                content: ''; position: fixed; inset: 0; z-index: 99999;
                background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><path d="M0,0 L10,10 L20,0 Z" fill="rgba(255,255,255,0.1)"/></svg>');
                box-shadow: inset 0 0 150px rgba(0,229,255,0.5);
                pointer-events: none; opacity: 1; animation: freezeIn 0.1s;
            }
            @keyframes freezeIn { from {opacity: 0;} to {opacity: 1;} }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">CRYO-JET CO2 CANNON</h2>
                <div class="section-icon"><i class="fas fa-wind" style="color: #fff;"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Hold to detonate heavy atmospheric CO2 blasts and drop the venue temperature.</p>

            <div class="cryo-wrapper" id="cryoEnv">
                <div class="cryo-canvas-box" id="cryoWrap">
                    <canvas id="cryoCanvas"></canvas>
                    <div class="cryo-cannon-base"><div class="cryo-cannon-nozzle"></div></div>
                </div>

                <div class="cryo-trigger-btn" id="btnCryo" onmousedown="startCryoBlast()" onmouseup="stopCryoBlast()" onmouseleave="stopCryoBlast()" ontouchstart="startCryoBlast()" ontouchend="stopCryoBlast()">
                    <i class="fas fa-snowflake" style="color: var(--cyan-neon);"></i> BLAST
                </div>
            </div>
        </div>

        <style>
            .pixel-mapper-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .pixel-canvas-box {
                width: 100%;
                aspect-ratio: 16 / 9; /* Standard widescreen LED ratio */
                background: #050505;
                border: 2px solid #333;
                position: relative;
                touch-action: none; /* Prevent scroll while drawing */
                cursor: crosshair;
                box-shadow: 0 0 20px rgba(0,0,0,0.9);
            }
            #pixelCanvas { width: 100%; height: 100%; display: block; image-rendering: pixelated; }

            .pixel-controls {
                display: flex; flex-direction: column; gap: 15px; margin-top: 15px;
                background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #111;
            }
            
            .color-picker-row { display: flex; justify-content: space-around; align-items: center; }
            .pix-color-btn {
                width: 35px; height: 35px; border-radius: 4px; border: 2px solid transparent;
                cursor: pointer; transition: 0.2s; box-shadow: inset 0 0 10px rgba(0,0,0,0.5);
            }
            .pix-color-btn.active { border-color: #fff; transform: scale(1.1); box-shadow: 0 0 15px currentColor; }

            .pix-hud { display: flex; justify-content: space-between; font-family: var(--font-data); font-size: 10px; color: #888; font-weight: bold; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">LED WALL PIXEL MAPPER</h2>
                <div class="section-icon"><i class="fas fa-tv"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Draw custom visuals directly onto the virtual P3 LED screen matrix.</p>

            <div class="pixel-mapper-wrapper">
                <div class="pixel-canvas-box" id="pixelWrap">
                    <canvas id="pixelCanvas"></canvas>
                </div>

                <div class="pixel-controls">
                    <div class="color-picker-row">
                        <div class="pix-color-btn active" style="background: var(--cyan-neon); color: var(--cyan-neon);" onclick="setPixelColor('var(--cyan-neon)', this)"></div>
                        <div class="pix-color-btn" style="background: var(--red-alert); color: var(--red-alert);" onclick="setPixelColor('var(--red-alert)', this)"></div>
                        <div class="pix-color-btn" style="background: var(--gold-primary); color: var(--gold-primary);" onclick="setPixelColor('var(--gold-primary)', this)"></div>
                        <div class="pix-color-btn" style="background: #00ff00; color: #00ff00;" onclick="setPixelColor('#00ff00', this)"></div>
                        <div class="pix-color-btn" style="background: #ffffff; color: #ffffff;" onclick="setPixelColor('#ffffff', this)"></div>
                        <div class="pix-color-btn" style="background: #000000; border-color: #333;" onclick="setPixelColor('#000000', this)">
                            <i class="fas fa-eraser" style="color:#666; font-size:12px; display:flex; justify-content:center; align-items:center; height:100%;"></i>
                        </div>
                    </div>
                    
                    <div class="pix-hud">
                        <span>PITCH RESOLUTION</span>
                        <span id="pxPitchVal" style="color:var(--cyan-neon);">P4 (Medium)</span>
                    </div>
                    <input type="range" class="app-slider" id="pixelPitchSlider" min="2" max="10" value="4" oninput="updatePixelPitch(this.value)">
                    
                    <button class="app-btn-outline" style="width:100%; border-color: var(--red-alert); color: var(--red-alert);" onclick="clearPixelWall()">
                        <i class="fas fa-trash-alt"></i> FORMAT DRIVE
                    </button>
                </div>
            </div>
        </div>

        <style>
            .voltage-matrix-wrapper {
                background: #000;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
                display: flex; flex-direction: column; gap: 15px;
                box-shadow: inset 0 0 30px rgba(0, 255, 0, 0.05);
            }

            .volt-gauges { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
            .v-gauge-card { background: #0a0a0f; border: 1px solid #1a1a24; border-radius: 8px; padding: 12px; text-align: center; }
            .vg-val { font-family: var(--font-tech); font-size: 22px; font-weight: 900; color: #fff; display: block; margin-bottom: 5px; }
            .vg-lbl { font-family: var(--font-data); font-size: 9px; color: #888; letter-spacing: 1px; }

            /* Scrolling Chart Canvas */
            .ekg-container {
                width: 100%; height: 140px; background: #020502; border: 1px solid #00ff00; border-radius: 8px; position: relative; overflow: hidden;
                box-shadow: inset 0 0 20px rgba(0,255,0,0.1);
            }
            .ekg-grid {
                position: absolute; inset: 0; pointer-events: none; z-index: 1;
                background-image: linear-gradient(rgba(0, 255, 0, 0.15) 1px, transparent 1px), linear-gradient(90deg, rgba(0, 255, 0, 0.15) 1px, transparent 1px);
                background-size: 20px 20px;
            }
            #ekgCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2; }
            
            .ekg-labels { position: absolute; left: 5px; top: 5px; bottom: 5px; display: flex; flex-direction: column; justify-content: space-between; z-index: 3; pointer-events: none; }
            .ekg-lbl { font-family: var(--font-tech); font-size: 8px; color: #00ff00; opacity: 0.8; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">VOLTAGE MATRIX EKG</h2>
                <div class="section-icon"><i class="fas fa-charging-station"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Live power telemetry of the FOH Generator Core.</p>

            <div class="voltage-matrix-wrapper">
                <div class="volt-gauges">
                    <div class="v-gauge-card">
                        <span class="vg-val" id="fuelGaugeVal">84%</span>
                        <span class="vg-lbl">DIESEL RESERVE</span>
                        <div style="width:100%; height:4px; background:#222; margin-top:8px; border-radius:2px; overflow:hidden;"><div id="fuelBarLine" style="width:84%; height:100%; background:#ffff00;"></div></div>
                    </div>
                    <div class="v-gauge-card">
                        <span class="vg-val" id="tempGaugeVal">72°C</span>
                        <span class="vg-lbl">CORE TEMP</span>
                        <div style="width:100%; height:4px; background:#222; margin-top:8px; border-radius:2px; overflow:hidden;"><div id="tempBarLine" style="width:60%; height:100%; background:#00e5ff;"></div></div>
                    </div>
                </div>

                <div style="display:flex; justify-content:space-between; align-items:center;">
                    <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">LIVE LOAD DRAW (kVA)</span>
                    <span style="background:#00ff00; color:#000; font-family:var(--font-tech); font-size:8px; padding:3px 6px; border-radius:4px; font-weight:bold; animation:blink 2s infinite;">SYNCED</span>
                </div>
                
                <div class="ekg-container" id="ekgWrap">
                    <div class="ekg-grid"></div>
                    <div class="ekg-labels">
                        <span class="ekg-lbl">100kW</span><span class="ekg-lbl">50kW</span><span class="ekg-lbl">0kW</span>
                    </div>
                    <canvas id="ekgCanvas"></canvas>
                </div>
            </div>
        </div>

        <script>
            // --- 1. CRYO-JET CO2 FLUID DYNAMICS ENGINE ---
            const cryoCanvas = document.getElementById('cryoCanvas');
            let cryoCtx = null;
            const cryoWrap = document.getElementById('cryoWrap');
            const cryoEnv = document.getElementById('cryoEnv');
            
            let isCryoFiring = false;
            let cryoParticles = [];
            let cryoAnimFrame = null;

            function initCryoEngine() {
                if(!cryoWrap || !cryoCanvas) return;
                cryoCanvas.width = cryoWrap.clientWidth;
                cryoCanvas.height = cryoWrap.clientHeight;
                cryoCtx = cryoCanvas.getContext('2d');
            }
            window.addEventListener('resize', initCryoEngine);
            setTimeout(initCryoEngine, 500);

            function startCryoBlast(e) {
                if(e) e.preventDefault(); // Prevent touch selection
                if(typeof playTap === 'function') playTap();
                isCryoFiring = true;
                
                // Add extreme UI effects
                document.body.classList.add('frozen-screen');
                cryoEnv.style.transform = 'translate(0, 2px)';
                
                // Continuous heavy haptic if supported
                if(navigator.vibrate) navigator.vibrate([100, 50, 100, 50, 100, 50, 100]); 
                
                // Play audio from Part 3 engine if active (white noise burst)
                if(typeof playSynth === 'function') playSynth('snare1', null); 
                
                if(!cryoAnimFrame) animateCryoFluid();
            }

            function stopCryoBlast(e) {
                if(e) e.preventDefault();
                isCryoFiring = false;
                document.body.classList.remove('frozen-screen');
                cryoEnv.style.transform = 'translate(0, 0)';
            }

            class CO2Gas {
                constructor(cx, cy) {
                    this.x = cx + (Math.random() * 10 - 5); // Spawn slightly randomized around nozzle
                    this.y = cy;
                    // Extreme upward velocity
                    this.vy = -(Math.random() * 18 + 12);
                    // Lateral spread outward
                    this.vx = (Math.random() - 0.5) * 6;
                    this.radius = Math.random() * 8 + 4; // Starts small
                    this.life = 1.0;
                    this.decay = Math.random() * 0.04 + 0.01; // Dissipates fast
                }
                update() {
                    this.x += this.vx;
                    this.y += this.vy;
                    // Air friction slows it down rapidly
                    this.vy *= 0.90;
                    this.vx *= 0.92;
                    // Gravity slowly pulls the heavy cold gas down once momentum is lost
                    this.vy += 0.8;
                    
                    // Gas expands exponentially as it rises
                    this.radius += 1.5;
                    this.life -= this.decay;
                }
                draw(ctx) {
                    ctx.globalAlpha = Math.max(0, this.life);
                    
                    // Center is bright white, edges are slight cyan glow
                    const grad = ctx.createRadialGradient(this.x, this.y, 0, this.x, this.y, this.radius);
                    grad.addColorStop(0, 'rgba(255, 255, 255, 1)');
                    grad.addColorStop(0.5, 'rgba(200, 240, 255, 0.8)');
                    grad.addColorStop(1, 'rgba(255, 255, 255, 0)');
                    
                    ctx.fillStyle = grad;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                    ctx.fill();
                    
                    ctx.globalAlpha = 1.0;
                }
            }

            function animateCryoFluid() {
                // If button is released AND all particles are gone, stop the loop to save battery
                if(!isCryoFiring && cryoParticles.length === 0) {
                    cryoAnimFrame = null;
                    cryoCtx.clearRect(0,0, cryoCanvas.width, cryoCanvas.height);
                    return;
                }
                cryoAnimFrame = requestAnimationFrame(animateCryoFluid);

                // Use a dark translucent fill to create motion trails for the smoke
                cryoCtx.fillStyle = 'rgba(0, 5, 10, 0.5)';
                cryoCtx.fillRect(0,0, cryoCanvas.width, cryoCanvas.height);

                cryoCtx.globalCompositeOperation = 'screen';

                // Spawn new particles rapidly while firing
                if(isCryoFiring) {
                    const cx = cryoCanvas.width / 2;
                    const cy = cryoCanvas.height;
                    // Spawn 20 particles per frame for massive density
                    for(let i=0; i<20; i++) {
                        cryoParticles.push(new CO2Gas(cx, cy));
                    }
                }

                // Update and draw existing particles backwards (to safely splice array)
                for(let i = cryoParticles.length - 1; i >= 0; i--) {
                    let p = cryoParticles[i];
                    p.update();
                    p.draw(cryoCtx);
                    if(p.life <= 0) cryoParticles.splice(i, 1);
                }
                
                cryoCtx.globalCompositeOperation = 'source-over';
            }


            // --- 2. LED WALL PIXEL MAPPER LOGIC ---
            const pixCanvas = document.getElementById('pixelCanvas');
            let pixCtx = null;
            const pixWrap = document.getElementById('pixelWrap');
            
            let activePixColor = 'var(--cyan-neon)'; // Fallback string, resolved in draw
            let pixSize = 4; // Pixel pitch (resolution)
            let isPixDrawing = false;

            // We need a backing array to store the grid colors so it scales correctly
            let pixelGrid = [];
            let gridCols = 0;
            let gridRows = 0;

            function initPixelMapper() {
                if(!pixWrap || !pixCanvas) return;
                
                const w = pixWrap.clientWidth;
                const h = pixWrap.clientHeight;
                
                pixCanvas.width = w;
                pixCanvas.height = h;
                pixCtx = pixCanvas.getContext('2d', { willReadFrequently: true });
                
                setupPixelGrid();
            }
            window.addEventListener('resize', initPixelMapper);
            setTimeout(initPixelMapper, 800);

            function setupPixelGrid() {
                gridCols = Math.floor(pixCanvas.width / pixSize);
                gridRows = Math.floor(pixCanvas.height / pixSize);
                
                // Initialize 2D array with null (black)
                pixelGrid = new Array(gridRows).fill(null).map(() => new Array(gridCols).fill(null));
                drawEntireGrid();
            }

            function setPixelColor(colorStr, el) {
                if(typeof playTap === 'function') playTap();
                document.querySelectorAll('.pix-color-btn').forEach(b => b.classList.remove('active'));
                el.classList.add('active');
                activePixColor = colorStr;
            }

            function updatePixelPitch(val) {
                pixSize = parseInt(val);
                
                const pitchText = document.getElementById('pxPitchVal');
                if(pixSize <= 3) pitchText.innerText = `P${pixSize} (Ultra-HD)`;
                else if(pixSize <= 6) pitchText.innerText = `P${pixSize} (Medium)`;
                else pitchText.innerText = `P${pixSize} (Low-Res)`;
                
                setupPixelGrid(); // Re-initialize grid at new resolution
            }

            function clearPixelWall() {
                if(typeof triggerToast === 'function') triggerToast("LED Wall Formatted.");
                if(navigator.vibrate) navigator.vibrate(20);
                setupPixelGrid();
            }

            // Mouse/Touch Drawing Event Listeners
            pixCanvas.addEventListener('mousedown', pixStart);
            pixCanvas.addEventListener('touchstart', (e) => { e.preventDefault(); pixStart(e); }, {passive: false});
            
            document.addEventListener('mousemove', pixMove);
            document.addEventListener('touchmove', pixMove, {passive: false});
            
            document.addEventListener('mouseup', () => isPixDrawing = false);
            document.addEventListener('touchend', () => isPixDrawing = false);

            function getPixCoords(e) {
                const rect = pixCanvas.getBoundingClientRect();
                const clientX = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                const clientY = e.type.includes('touch') ? e.touches[0].clientY : e.clientY;
                
                const x = clientX - rect.left;
                const y = clientY - rect.top;
                
                // Convert screen coordinates to Grid Col/Row
                const col = Math.floor(x / pixSize);
                const row = Math.floor(y / pixSize);
                return { col, row };
            }

            // Helper to resolve CSS variables to actual hex/rgb for canvas storage
            function resolveColor(cssVarStr) {
                if(cssVarStr.startsWith('var(')) {
                    // Extract variable name, e.g., 'var(--cyan-neon)' -> '--cyan-neon'
                    const varName = cssVarStr.slice(4, -1);
                    return getComputedStyle(document.documentElement).getPropertyValue(varName).trim();
                }
                return cssVarStr; // Return as is if it's already hex/rgb
            }

            function paintPixel(col, row) {
                if(col >= 0 && col < gridCols && row >= 0 && row < gridRows) {
                    const resolvedColor = resolveColor(activePixColor);
                    
                    // If painting the same color, skip to save CPU
                    if(pixelGrid[row][col] === resolvedColor) return;
                    
                    pixelGrid[row][col] = resolvedColor;
                    
                    // Draw directly to canvas for speed instead of redrawing whole grid
                    if(resolvedColor === '#000000') {
                        pixCtx.clearRect(col * pixSize, row * pixSize, pixSize, pixSize); // Eraser
                    } else {
                        // Draw slight border to simulate individual LED modules
                        pixCtx.fillStyle = '#000'; 
                        pixCtx.fillRect(col * pixSize, row * pixSize, pixSize, pixSize);
                        
                        pixCtx.fillStyle = resolvedColor;
                        pixCtx.fillRect((col * pixSize) + 1, (row * pixSize) + 1, pixSize - 2, pixSize - 2);
                    }
                }
            }

            function pixStart(e) {
                isPixDrawing = true;
                const coords = getPixCoords(e);
                paintPixel(coords.col, coords.row);
            }

            function pixMove(e) {
                if(!isPixDrawing) return;
                
                // Only process if touch is actually over the canvas
                const rect = pixCanvas.getBoundingClientRect();
                const clientX = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                const clientY = e.type.includes('touch') ? e.touches[0].clientY : e.clientY;
                
                if(clientX >= rect.left && clientX <= rect.right && clientY >= rect.top && clientY <= rect.bottom) {
                    e.preventDefault(); // Stop scroll while actively drawing on canvas
                    const coords = getPixCoords(e);
                    paintPixel(coords.col, coords.row);
                }
            }

            function drawEntireGrid() {
                if(!pixCtx) return;
                pixCtx.clearRect(0,0, pixCanvas.width, pixCanvas.height);
                for(let r=0; r<gridRows; r++) {
                    for(let c=0; c<gridCols; c++) {
                        const color = pixelGrid[r][c];
                        if(color && color !== '#000000') {
                            pixCtx.fillStyle = '#000'; 
                            pixCtx.fillRect(c * pixSize, r * pixSize, pixSize, pixSize);
                            pixCtx.fillStyle = color;
                            pixCtx.fillRect((c * pixSize) + 1, (r * pixSize) + 1, pixSize - 2, pixSize - 2);
                        }
                    }
                }
            }


            // --- 3. VOLTAGE MATRIX EKG TELEMETRY LOGIC ---
            const ekgCanvas = document.getElementById('ekgCanvas');
            let ekgCtx = null;
            const ekgWrap = document.getElementById('ekgWrap');
            
            let ekgData = [];
            let ekgAnimFrame = null;
            
            // System Variables
            let sysFuel = 84.0;
            let sysTemp = 72.0;

            function initEKG() {
                if(!ekgWrap || !ekgCanvas) return;
                ekgCanvas.width = ekgWrap.clientWidth;
                ekgCanvas.height = ekgWrap.clientHeight;
                ekgCtx = ekgCanvas.getContext('2d');
                
                // Pre-fill array with baseline power data based on screen width
                const pointsToFit = Math.floor(ekgCanvas.width / 4); // Point every 4 pixels
                ekgData = new Array(pointsToFit).fill(20); 
                
                if(!ekgAnimFrame) animateEKG();
            }
            window.addEventListener('resize', initEKG);
            setTimeout(initEKG, 1000);

            function animateEKG() {
                ekgAnimFrame = requestAnimationFrame(animateEKG);
                if(!ekgCtx) return;

                // Clear
                ekgCtx.clearRect(0,0, ekgCanvas.width, ekgCanvas.height);

                // Generate new data point representing kW draw
                // Base 30kW + random noise
                let currentLoad = 30 + (Math.random() * 15 - 7.5);
                
                // If Audio engine is playing, add massive spikes to simulate bass hit current draw
                if(typeof isEngineOn !== 'undefined' && isEngineOn) {
                    if(Math.random() > 0.8) currentLoad += 40; 
                }
                // If Strobe is playing, add medium spikes
                if(typeof seqIsPlaying !== 'undefined' && seqIsPlaying) {
                    if(Math.random() > 0.5) currentLoad += 20;
                }
                
                // Clamp
                currentLoad = Math.max(5, Math.min(95, currentLoad));

                // Push new point, remove oldest
                ekgData.push(currentLoad);
                ekgData.shift();

                // Render the line
                ekgCtx.beginPath();
                ekgCtx.strokeStyle = '#00ff00';
                ekgCtx.lineWidth = 2;
                ekgCtx.lineJoin = 'round';
                
                // Add green glow
                ekgCtx.shadowBlur = 8;
                ekgCtx.shadowColor = '#00ff00';

                const stepX = ekgCanvas.width / ekgData.length;
                
                for(let i=0; i<ekgData.length; i++) {
                    const x = i * stepX;
                    // Y axis is inverted (0 is top). Map 0-100kW to canvas height
                    const y = ekgCanvas.height - ((ekgData[i] / 100) * ekgCanvas.height);
                    
                    if(i===0) ekgCtx.moveTo(x, y);
                    else ekgCtx.lineTo(x, y);
                }
                
                ekgCtx.stroke();
                ekgCtx.shadowBlur = 0; // reset
            }

            // Slow Telemetry Update Loop (Simulates fuel draining and temp rising)
            setInterval(() => {
                // Only change stats if the engine or sequencers are drawing power
                let powerActive = false;
                if(typeof isEngineOn !== 'undefined' && isEngineOn) powerActive = true;
                if(typeof seqIsPlaying !== 'undefined' && seqIsPlaying) powerActive = true;
                
                if(!powerActive) return;

                // Drain fuel slowly
                sysFuel -= 0.05;
                if(sysFuel < 0) sysFuel = 0;
                
                // Temp fluctuates upwards
                sysTemp += (Math.random() * 0.5 - 0.1);
                if(sysTemp > 110) sysTemp = 110;

                // Update UI DOM
                const fGauge = document.getElementById('fuelGaugeVal');
                const fBar = document.getElementById('fuelBarLine');
                const tGauge = document.getElementById('tempGaugeVal');
                const tBar = document.getElementById('tempBarLine');

                if(fGauge) {
                    fGauge.innerText = `${Math.floor(sysFuel)}%`;
                    fBar.style.width = `${sysFuel}%`;
                    if(sysFuel < 20) { fBar.style.background = 'var(--red-alert)'; fGauge.style.color = 'var(--red-alert)'; }
                }

                if(tGauge) {
                    tGauge.innerText = `${sysTemp.toFixed(1)}°C`;
                    // Max temp visual scale = 120C
                    tBar.style.width = `${(sysTemp / 120) * 100}%`;
                    if(sysTemp > 90) { tBar.style.background = 'var(--red-alert)'; tGauge.style.color = 'var(--red-alert)'; }
                }

            }, 2000); // Update every 2 seconds
        </script>
        <style>
            .optics-wrapper {
                background: #020202;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .optics-canvas-box {
                width: 100%;
                height: 250px;
                background: #000;
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 40px rgba(0, 229, 255, 0.1);
                cursor: crosshair;
            }
            #opticsCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .optics-hud {
                position: absolute; top: 10px; left: 10px; pointer-events: none; z-index: 5;
            }
            .opt-title { font-family: var(--font-tech); font-size: 10px; font-weight: 900; color: var(--cyan-neon); letter-spacing: 2px; }
            .opt-sub { font-family: var(--font-data); font-size: 8px; color: #fff; margin-top: 2px; display: block;}

            .optics-controls {
                display: flex; gap: 10px; margin-top: 15px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">OPTICAL REFLECTION AI</h2>
                <div class="section-icon"><i class="fas fa-project-diagram"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate high-power DMX laser bounces. Tap inside the canvas to deploy a volumetric scatter prism.</p>

            <div class="optics-wrapper">
                <div class="optics-canvas-box" id="opticsWrap">
                    <div class="optics-hud">
                        <span class="opt-title">PHOTON TRAJECTORY</span>
                        <span class="opt-sub">CALCULATING INCIDENCE ANGLES</span>
                    </div>
                    <canvas id="opticsCanvas"></canvas>
                </div>

                <div class="optics-controls">
                    <button class="app-btn-outline" style="flex: 1; border-color: var(--gold-primary); color: var(--gold-primary);" onclick="changeLaserColor('#D4AF37')">GOLD BEAM</button>
                    <button class="app-btn-outline" style="flex: 1; border-color: var(--cyan-neon); color: var(--cyan-neon);" onclick="changeLaserColor('#00e5ff')">CYAN BEAM</button>
                    <button class="app-btn-outline" style="flex: 1; border-color: var(--red-alert); color: var(--red-alert);" onclick="clearPrisms()">CLEAR PRISMS</button>
                </div>
            </div>
        </div>

        <style>
            .bpm-sync-wrapper {
                background: linear-gradient(135deg, #0a0a0f, #050508);
                border: 1px solid #1a1a24;
                border-radius: 12px;
                padding: 20px;
                text-align: center;
                box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            }

            .bpm-display-box {
                background: #000; border: 2px solid var(--gold-primary); border-radius: 8px;
                padding: 15px; position: relative; overflow: hidden; margin-bottom: 20px;
                box-shadow: inset 0 0 30px rgba(212,175,55,0.1);
            }
            .bpm-wave-bg {
                position: absolute; inset: 0; opacity: 0.2;
                background: repeating-linear-gradient(90deg, transparent, transparent 10px, var(--gold-primary) 10px, var(--gold-primary) 12px);
                transition: background-size 0.2s ease; pointer-events: none;
            }
            
            .bpm-val-text { font-family: var(--font-tech); font-size: 48px; font-weight: 900; color: #fff; text-shadow: 0 0 20px var(--gold-primary); position: relative; z-index: 2;}
            .bpm-lbl-text { font-family: var(--font-data); font-size: 10px; color: var(--gold-primary); letter-spacing: 3px; font-weight: bold; position: relative; z-index: 2;}

            .tap-tempo-btn {
                width: 120px; height: 120px; margin: 0 auto;
                border-radius: 50%; background: radial-gradient(circle at 30% 30%, #222, #050505);
                border: 4px solid #333; box-shadow: 0 10px 20px rgba(0,0,0,0.8), inset 0 5px 15px rgba(255,255,255,0.1);
                display: flex; justify-content: center; align-items: center;
                color: #888; font-family: var(--font-tech); font-size: 20px; font-weight: bold;
                cursor: pointer; user-select: none; touch-action: manipulation; transition: 0.05s;
            }
            .tap-tempo-btn:active, .tap-tempo-btn.tapped {
                transform: scale(0.92);
                border-color: var(--cyan-neon); color: var(--cyan-neon);
                background: radial-gradient(circle at 30% 30%, #003344, #000);
                box-shadow: 0 5px 10px rgba(0,0,0,0.8), inset 0 0 30px rgba(0,229,255,0.4);
            }

            .bpm-status-bar {
                display: flex; justify-content: space-between; margin-top: 20px;
                border-top: 1px dashed #333; padding-top: 15px;
            }
            .bs-item { display: flex; flex-direction: column; align-items: center; }
            .bs-val { font-family: var(--font-body); font-size: 14px; font-weight: bold; color: #fff; }
            .bs-lbl { font-family: var(--font-data); font-size: 8px; color: #666; text-transform: uppercase; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">GLOBAL BPM SYNC</h2>
                <div class="section-icon"><i class="fas fa-stopwatch"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px; text-align: center;">Tap the pad to the beat of the music to lock the global neural tempo.</p>

            <div class="bpm-sync-wrapper">
                <div class="bpm-display-box">
                    <div class="bpm-wave-bg" id="bpmVisualWave"></div>
                    <div class="bpm-val-text" id="globalBpmDisplay">128</div>
                    <div class="bpm-lbl-text">BEATS PER MINUTE</div>
                </div>

                <div class="tap-tempo-btn" id="btnTapTempo">TAP</div>

                <div class="bpm-status-bar">
                    <div class="bs-item">
                        <span class="bs-val" id="bpmIntervalMs">468ms</span>
                        <span class="bs-lbl">WAVELENGTH</span>
                    </div>
                    <div class="bs-item">
                        <span class="bs-val" id="bpmSyncLock" style="color: #00ff00;">LOCKED</span>
                        <span class="bs-lbl">DMX ENGINE LINK</span>
                    </div>
                    <div class="bs-item">
                        <button class="app-btn-outline" style="padding: 5px 10px; font-size: 9px; height: 100%;" onclick="resetGlobalBpm()">RESET</button>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .jcurve-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
                display: flex;
                flex-direction: column;
                gap: 15px;
            }

            .rig-canvas-box {
                width: 100%;
                height: 300px;
                background: linear-gradient(180deg, #050510 0%, #000 100%);
                border: 1px solid #112233;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #rigCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }
            
            /* Virtual Audience Floor */
            .audience-floor {
                position: absolute; bottom: 0; left: 0; width: 100%; height: 30px;
                background: linear-gradient(90deg, #111, #222); border-top: 2px solid #444; z-index: 1;
            }
            .audience-figs { 
                position: absolute; bottom: 30px; left: 80px; width: calc(100% - 80px); height: 25px; 
                background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 15 25"><circle cx="7.5" cy="4" r="3" fill="%23555"/><rect x="5" y="8" width="5" height="12" fill="%23555"/></svg>') repeat-x; 
                background-size: contain; opacity: 0.6; z-index: 1; 
            }

            .rig-controls {
                background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #222;
                display: flex; flex-direction: column; gap: 12px;
            }

            .angle-slider-group { display: flex; flex-direction: column; gap: 5px; }
            .angle-header { display: flex; justify-content: space-between; font-family: var(--font-tech); font-size: 9px; color: var(--gold-primary); font-weight: bold; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">LINE ARRAY J-CURVE AI</h2>
                <div class="section-icon"><i class="fas fa-ruler-combined"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Adjust individual box splay angles to perfectly map the acoustic throw cone across the audience floor.</p>

            <div class="jcurve-wrapper">
                <div class="rig-canvas-box" id="rigWrap">
                    <canvas id="rigCanvas"></canvas>
                    <div class="audience-floor"></div>
                    <div class="audience-figs"></div>
                    <div style="position:absolute; top:10px; left:10px; color:#00e5ff; font-family:var(--font-tech); font-size:8px;">SIDE PROFILE RIGGING</div>
                </div>

                <div class="rig-controls">
                    <div class="angle-slider-group">
                        <div class="angle-header"><span>BOX 1 (TOP/LONG THROW)</span><span id="angVal1">0°</span></div>
                        <input type="range" class="app-slider" id="ang1" min="0" max="15" value="0" oninput="drawRigSystem()">
                    </div>
                    <div class="angle-slider-group">
                        <div class="angle-header"><span>BOX 2 (UPPER MID)</span><span id="angVal2">2°</span></div>
                        <input type="range" class="app-slider" id="ang2" min="0" max="15" value="2" oninput="drawRigSystem()">
                    </div>
                    <div class="angle-slider-group">
                        <div class="angle-header"><span>BOX 3 (LOWER MID)</span><span id="angVal3">5°</span></div>
                        <input type="range" class="app-slider" id="ang3" min="0" max="15" value="5" oninput="drawRigSystem()">
                    </div>
                    <div class="angle-slider-group">
                        <div class="angle-header"><span>BOX 4 (DOWNFILL)</span><span id="angVal4">10°</span></div>
                        <input type="range" class="app-slider" id="ang4" min="0" max="15" value="10" oninput="drawRigSystem()">
                    </div>
                </div>
            </div>
        </div>

        <script>
            // --- 1. OPTICAL REFLECTION AI LOGIC (Laser Bounce) ---
            const optCanvas = document.getElementById('opticsCanvas');
            let optCtx = null;
            const optWrap = document.getElementById('opticsWrap');
            
            let activeLaserColor = '#00e5ff';
            let laserBeam = { x: 10, y: 10, vx: 5, vy: 4 }; // Starting trajectory
            let laserHistory = [];
            let prisms = []; // Nodes that scatter light
            let optAnimFrame = null;

            function initOpticsEngine() {
                if(!optWrap || !optCanvas) return;
                optCanvas.width = optWrap.clientWidth;
                optCanvas.height = optWrap.clientHeight;
                optCtx = optCanvas.getContext('2d');
                laserBeam.y = optCanvas.height / 2; // Start halfway down left side
                if(!optAnimFrame) animateOptics();
            }
            window.addEventListener('resize', initOpticsEngine);
            setTimeout(initOpticsEngine, 500);

            function changeLaserColor(hex) {
                if(typeof playTap === 'function') playTap();
                activeLaserColor = hex;
            }

            function clearPrisms() {
                if(typeof playTap === 'function') playTap();
                prisms = [];
                laserHistory = []; // Reset trail
            }

            // Tap to add prism
            optCanvas.addEventListener('mousedown', addPrism);
            optCanvas.addEventListener('touchstart', (e) => { e.preventDefault(); addPrism(e); }, {passive: false});

            function addPrism(e) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(15);
                
                const rect = optCanvas.getBoundingClientRect();
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                const x = touch.clientX - rect.left;
                const y = touch.clientY - rect.top;
                
                prisms.push({ x: x, y: y, radius: 15 });
            }

            function animateOptics() {
                optAnimFrame = requestAnimationFrame(animateOptics);
                if(!optCtx) return;

                // Motion blur fade
                optCtx.fillStyle = 'rgba(0, 0, 0, 0.15)';
                optCtx.fillRect(0, 0, optCanvas.width, optCanvas.height);

                // Update Laser Physics
                laserBeam.x += laserBeam.vx;
                laserBeam.y += laserBeam.vy;

                let bounced = false;

                // Wall Bounces
                if (laserBeam.x <= 0 || laserBeam.x >= optCanvas.width) {
                    laserBeam.vx *= -1;
                    laserBeam.x = laserBeam.x <= 0 ? 0 : optCanvas.width;
                    bounced = true;
                }
                if (laserBeam.y <= 0 || laserBeam.y >= optCanvas.height) {
                    laserBeam.vy *= -1;
                    laserBeam.y = laserBeam.y <= 0 ? 0 : optCanvas.height;
                    bounced = true;
                }

                // Prism Collision (Circle collision)
                prisms.forEach(prism => {
                    const dx = laserBeam.x - prism.x;
                    const dy = laserBeam.y - prism.y;
                    const dist = Math.hypot(dx, dy);
                    
                    if(dist < prism.radius) {
                        // Scatter! Deflect randomly
                        const angle = Math.random() * Math.PI * 2;
                        const speed = Math.hypot(laserBeam.vx, laserBeam.vy);
                        laserBeam.vx = Math.cos(angle) * speed;
                        laserBeam.vy = Math.sin(angle) * speed;
                        
                        // Draw scatter burst
                        optCtx.globalCompositeOperation = 'lighter';
                        optCtx.fillStyle = activeLaserColor;
                        for(let i=0; i<8; i++) {
                            optCtx.beginPath();
                            optCtx.moveTo(prism.x, prism.y);
                            optCtx.lineTo(prism.x + (Math.random()-0.5)*100, prism.y + (Math.random()-0.5)*100);
                            optCtx.strokeStyle = `rgba(${activeLaserColor === '#00e5ff' ? '0,229,255' : '212,175,55'}, 0.3)`;
                            optCtx.stroke();
                        }
                        optCtx.globalCompositeOperation = 'source-over';
                        bounced = true;
                    }
                });

                if (bounced && typeof playSynth === 'function' && window.isEngineOn) {
                    // Make a tiny tick sound on bounce if audio engine is active
                    playSynth('hihatC', null);
                }

                // Keep trail history
                laserHistory.push({x: laserBeam.x, y: laserBeam.y});
                if (laserHistory.length > 50) {
                    laserHistory.shift();
                }

                // Draw Prisms
                prisms.forEach(p => {
                    optCtx.beginPath();
                    optCtx.arc(p.x, p.y, p.radius, 0, Math.PI*2);
                    optCtx.fillStyle = 'rgba(255,255,255,0.1)';
                    optCtx.fill();
                    optCtx.strokeStyle = '#fff';
                    optCtx.lineWidth = 1;
                    optCtx.stroke();
                    // Inner diamond
                    optCtx.beginPath();
                    optCtx.moveTo(p.x, p.y - p.radius + 2);
                    optCtx.lineTo(p.x + p.radius - 2, p.y);
                    optCtx.lineTo(p.x, p.y + p.radius - 2);
                    optCtx.lineTo(p.x - p.radius + 2, p.y);
                    optCtx.closePath();
                    optCtx.stroke();
                });

                // Draw Laser Trail
                optCtx.globalCompositeOperation = 'lighter';
                optCtx.beginPath();
                for (let i = 0; i < laserHistory.length; i++) {
                    const pt = laserHistory[i];
                    if (i === 0) optCtx.moveTo(pt.x, pt.y);
                    else optCtx.lineTo(pt.x, pt.y);
                }
                
                optCtx.strokeStyle = activeLaserColor;
                optCtx.lineWidth = 3;
                optCtx.shadowBlur = 15;
                optCtx.shadowColor = activeLaserColor;
                optCtx.stroke();
                
                optCtx.shadowBlur = 0;
                optCtx.globalCompositeOperation = 'source-over';
            }


            // --- 2. GLOBAL NEURAL BPM SYNC ENGINE LOGIC ---
            let globalTapTimes = [];
            const globalBtnTap = document.getElementById('btnTapTempo');
            const globalDispBpm = document.getElementById('globalBpmDisplay');
            const globalDispMs = document.getElementById('bpmIntervalMs');
            const globalWaveBg = document.getElementById('bpmVisualWave');
            const globalSyncLock = document.getElementById('bpmSyncLock');

            // Attach Global Variables so other scripts can access them
            window.mndGlobalBPM = 128; 

            globalBtnTap.addEventListener('mousedown', handleGlobalTap);
            globalBtnTap.addEventListener('touchstart', (e) => { e.preventDefault(); handleGlobalTap(); }, {passive: false});

            function handleGlobalTap() {
                const now = Date.now();
                
                // Visual Button feedback
                globalBtnTap.classList.add('tapped');
                setTimeout(() => globalBtnTap.classList.remove('tapped'), 50);
                if(navigator.vibrate) navigator.vibrate(25); // Crisp haptic

                // Play drum sound if engine is active
                if(typeof playSynth === 'function' && window.isEngineOn) playSynth('kick', null);

                // Reset array if more than 2.5s passed since last tap
                if (globalTapTimes.length > 0 && now - globalTapTimes[globalTapTimes.length - 1] > 2500) {
                    globalTapTimes = [];
                }

                globalTapTimes.push(now);

                if (globalTapTimes.length > 1) {
                    // Keep last 6 taps for moving average
                    if (globalTapTimes.length > 6) globalTapTimes.shift();

                    let intervals = [];
                    for (let i = 1; i < globalTapTimes.length; i++) {
                        intervals.push(globalTapTimes[i] - globalTapTimes[i - 1]);
                    }

                    // Average ms between beats
                    const avgMs = intervals.reduce((a, b) => a + b) / intervals.length;
                    
                    // Convert ms to BPM
                    const bpm = Math.round(60000 / avgMs);
                    window.mndGlobalBPM = bpm; // Update Global OS State

                    // Update UI
                    globalDispBpm.innerText = bpm;
                    globalDispMs.innerText = `${Math.round(avgMs)}ms`;
                    
                    // Shift background wave CSS based on tempo
                    const waveDensity = Math.max(4, 35 - (bpm / 8)); 
                    globalWaveBg.style.backgroundSize = `${waveDensity}px 100%`;

                    globalSyncLock.innerText = "CALCULATING...";
                    globalSyncLock.style.color = "var(--gold-primary)";

                    clearTimeout(window.globalBpmTimeout);
                    window.globalBpmTimeout = setTimeout(() => {
                        globalSyncLock.innerText = "LOCKED";
                        globalSyncLock.style.color = "#00ff00";
                        
                        // Push to Strobe Sequencer (from Part 7) if it exists
                        const seqBpmInput = document.getElementById('sequencerBpm');
                        if(seqBpmInput) seqBpmInput.value = bpm;
                        
                    }, 800);
                }
            }

            function resetGlobalBpm() {
                if(typeof playTap === 'function') playTap();
                globalTapTimes = [];
                globalDispBpm.innerText = "---";
                globalDispMs.innerText = "---";
                globalWaveBg.style.backgroundSize = "20px 100%";
                globalSyncLock.innerText = "STANDBY";
                globalSyncLock.style.color = "#888";
            }


            // --- 3. LINE ARRAY J-CURVE RIGGING LOGIC ---
            const rigCanvas = document.getElementById('rigCanvas');
            let rigCtx = null;

            function initRigSystem() {
                const wrap = document.getElementById('rigWrap');
                if(!wrap || !rigCanvas) return;
                rigCanvas.width = wrap.clientWidth;
                rigCanvas.height = wrap.clientHeight;
                rigCtx = rigCanvas.getContext('2d');
                drawRigSystem();
            }
            window.addEventListener('resize', initRigSystem);
            setTimeout(initRigSystem, 600);
            
            function drawRigSystem() {
                if(!rigCtx) return;
                rigCtx.clearRect(0,0, rigCanvas.width, rigCanvas.height);

                // Fetch slider angles
                const a1 = parseInt(document.getElementById('ang1').value);
                const a2 = parseInt(document.getElementById('ang2').value);
                const a3 = parseInt(document.getElementById('ang3').value);
                const a4 = parseInt(document.getElementById('ang4').value);

                // Update UI text
                document.getElementById('angVal1').innerText = `${a1}°`;
                document.getElementById('angVal2').innerText = `${a2}°`;
                document.getElementById('angVal3').innerText = `${a3}°`;
                document.getElementById('angVal4').innerText = `${a4}°`;

                // Starting coordinates for the hoist/bumper
                const startX = 40; 
                const startY = 30;
                
                rigCtx.save();
                rigCtx.translate(startX, startY);

                // Draw Top Hoist Motor & Chain
                rigCtx.strokeStyle = '#555'; 
                rigCtx.lineWidth = 3;
                rigCtx.beginPath(); rigCtx.moveTo(0, -30); rigCtx.lineTo(0, 0); rigCtx.stroke();
                // Bumper frame
                rigCtx.fillStyle = '#444';
                rigCtx.fillRect(-25, 0, 50, 5);

                // Box dimensions
                const boxH = 20; 
                const boxW = 40;
                const angles = [a1, a2, a3, a4];
                let cumulativeAngle = 0;

                // Move down below bumper
                rigCtx.translate(0, 5);

                angles.forEach((ang) => {
                    cumulativeAngle += ang;
                    const rad = cumulativeAngle * (Math.PI / 180);
                    
                    // Rotate context based on cumulative splay
                    rigCtx.rotate(rad);
                    
                    // Draw Line Array Box (facing right)
                    rigCtx.fillStyle = '#111'; 
                    rigCtx.strokeStyle = 'var(--gold-primary)'; 
                    rigCtx.lineWidth = 1;
                    
                    // Anchor point is top-center of the box for rigging math
                    rigCtx.fillRect(-boxW/2, 0, boxW, boxH);
                    rigCtx.strokeRect(-boxW/2, 0, boxW, boxH);
                    
                    // Draw Acoustic Throw Wave (Cone of sound)
                    // Blend mode makes overlapping waves brighter
                    rigCtx.globalCompositeOperation = 'screen';
                    rigCtx.fillStyle = 'rgba(0, 229, 255, 0.12)';
                    
                    rigCtx.beginPath();
                    // Sound originates from center of the right face
                    rigCtx.moveTo(boxW/2, boxH/2);
                    // Draw a long wedge out into the "audience"
                    rigCtx.lineTo(800, -150);
                    rigCtx.lineTo(800, 200);
                    rigCtx.closePath();
                    rigCtx.fill();
                    rigCtx.globalCompositeOperation = 'source-over';

                    // Move translation matrix down to the bottom of THIS box for the next box
                    rigCtx.translate(0, boxH + 1); 
                    
                    // Undo rotation so the next box calculates its angle relative to this hinge point
                    rigCtx.rotate(-rad); 
                });

                rigCtx.restore();
            }
        </script>
        <style>
            .feedback-eliminator-wrapper {
                background: #020202;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.9);
            }

            .rta-canvas-container {
                width: 100%;
                height: 180px;
                background: #050505;
                border: 1px solid #00ff00;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 20px rgba(0,255,0,0.1);
            }
            .rta-canvas-container.ringing {
                border-color: var(--red-alert);
                box-shadow: inset 0 0 30px rgba(255,51,51,0.3);
                animation: rtaShake 0.1s infinite;
            }
            @keyframes rtaShake { 0% {transform: translateX(2px);} 50% {transform: translateX(-2px);} 100% {transform: translateX(0);} }

            #rtaCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2; }
            
            .rta-grid {
                position: absolute; inset: 0; pointer-events: none; z-index: 1;
                background-image: 
                    linear-gradient(rgba(0, 255, 0, 0.2) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(0, 255, 0, 0.2) 1px, transparent 1px);
                background-size: 25px 25px;
            }

            /* 8-Band Graphic EQ Faders */
            .eq-fader-board {
                display: flex; justify-content: space-between; margin-top: 20px;
                background: #0a0a0f; padding: 15px 5px; border-radius: 8px; border: 1px solid #1a1a24;
            }
            .eq-channel { display: flex; flex-direction: column; align-items: center; gap: 5px; flex: 1; }
            
            .eq-slider {
                -webkit-appearance: none; width: 100px; height: 6px; background: #111;
                border-radius: 3px; outline: none; transform: rotate(-90deg); margin: 50px 0;
                border: 1px solid #333; box-shadow: inset 0 2px 5px rgba(0,0,0,0.8);
            }
            .eq-slider::-webkit-slider-thumb {
                -webkit-appearance: none; appearance: none; width: 18px; height: 28px;
                background: linear-gradient(180deg, #555, #222); border: 2px solid var(--gold-primary);
                border-radius: 4px; cursor: grab; box-shadow: 0 0 10px rgba(212,175,55,0.4);
            }
            .eq-slider::-webkit-slider-thumb:active { cursor: grabbing; background: var(--gold-primary); }

            .eq-freq-lbl { font-family: var(--font-tech); font-size: 8px; color: #888; text-align: center; }
            
            .fe-hud { display: flex; justify-content: space-between; align-items: center; margin-top: 15px; }
        </style>

        <div class="app-section" id="feEnvironment">
            <div class="section-header">
                <h2 class="section-title">FEEDBACK ELIMINATOR</h2>
                <div class="section-icon"><i class="fas fa-wave-square" style="color: var(--red-alert);"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">When a mic feedback ring occurs, locate the spiked frequency on the RTA and pull the fader down instantly.</p>

            <div class="feedback-eliminator-wrapper">
                <div class="rta-canvas-container" id="rtaWrap">
                    <div class="rta-grid"></div>
                    <div style="position:absolute; top:5px; left:5px; color:#00ff00; font-family:var(--font-tech); font-size:9px; z-index:5;" id="rtaStatusTxt">RTA: STABLE</div>
                    <canvas id="rtaCanvas"></canvas>
                </div>

                <div class="eq-fader-board">
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="0" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">63Hz</span></div>
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="1" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">160Hz</span></div>
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="2" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">400Hz</span></div>
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="3" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">1kHz</span></div>
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="4" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">2.5kHz</span></div>
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="5" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">6.3kHz</span></div>
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="6" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">10kHz</span></div>
                    <div class="eq-channel"><input type="range" class="eq-slider fe-fader" data-band="7" min="-20" max="20" value="0" oninput="checkFeedbackKill()"><span class="eq-freq-lbl">16kHz</span></div>
                </div>

                <div class="fe-hud">
                    <button class="app-btn-outline" style="border-color: var(--red-alert); color: var(--red-alert);" onclick="triggerRandomFeedback()">
                        <i class="fas fa-exclamation-circle"></i> SIMULATE RING
                    </button>
                    <div style="font-family: var(--font-data); font-size: 12px; color: var(--gold-primary);">
                        SCORE: <span id="feScore" style="font-family: var(--font-tech); font-size: 16px; font-weight: bold; color: #fff;">0</span>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .harmonic-wrapper {
                background: #050508;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .harmonic-ui {
                display: flex; gap: 15px; align-items: center; justify-content: center; margin-top: 10px;
            }

            .key-selector {
                display: flex; flex-direction: column; gap: 10px; align-items: center;
                background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #222;
            }
            .key-input {
                background: #000; border: 2px solid var(--cyan-neon); color: var(--cyan-neon);
                font-family: var(--font-tech); font-size: 24px; font-weight: 900; text-align: center;
                width: 80px; height: 80px; border-radius: 50%; outline: none;
                box-shadow: 0 0 15px rgba(0,229,255,0.2); transition: 0.3s;
            }
            .key-input:focus { box-shadow: 0 0 25px var(--cyan-neon); transform: scale(1.05); }

            .compat-grid {
                display: grid; grid-template-columns: 1fr 1fr; gap: 10px; flex: 1;
            }
            .compat-card {
                background: rgba(0,0,0,0.6); border: 1px solid #333; border-radius: 6px;
                padding: 10px; text-align: center; display: flex; flex-direction: column;
            }
            .compat-lbl { font-family: var(--font-data); font-size: 9px; color: #888; text-transform: uppercase; }
            .compat-val { font-family: var(--font-tech); font-size: 16px; color: #fff; font-weight: bold; margin-top: 5px; }

            .compat-card.perfect { border-color: #00ff00; box-shadow: inset 0 0 10px rgba(0,255,0,0.2); }
            .compat-card.energy { border-color: var(--red-alert); box-shadow: inset 0 0 10px rgba(255,51,51,0.2); }
            .compat-card.relative { border-color: var(--gold-primary); box-shadow: inset 0 0 10px rgba(212,175,55,0.2); }
            .compat-card.chill { border-color: var(--cyan-neon); box-shadow: inset 0 0 10px rgba(0,229,255,0.2); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">HARMONIC MIXING AI</h2>
                <div class="section-icon"><i class="fas fa-compact-disc"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 10px;">Input the current track's Camelot Key (e.g., 8A) to calculate mathematically compatible keys for flawless beatmatching.</p>

            <div class="harmonic-wrapper">
                <div class="harmonic-ui">
                    <div class="key-selector">
                        <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">CURRENT KEY</span>
                        <input type="text" class="key-input" id="currentKeyInp" value="8A" maxlength="3" oninput="calculateHarmonics()">
                        <span id="musicalNoteName" style="font-family:var(--font-tech); font-size:10px; color:#555;">A Minor</span>
                    </div>

                    <div class="compat-grid">
                        <div class="compat-card perfect">
                            <span class="compat-lbl">Perfect Match</span>
                            <span class="compat-val" id="kPerf">8A</span>
                        </div>
                        <div class="compat-card relative">
                            <span class="compat-lbl">Relative (Mood Shift)</span>
                            <span class="compat-val" id="kRel">8B</span>
                        </div>
                        <div class="compat-card energy">
                            <span class="compat-lbl">Energy Boost (+1)</span>
                            <span class="compat-val" id="kUp">9A</span>
                        </div>
                        <div class="compat-card chill">
                            <span class="compat-lbl">Deep Drop (-1)</span>
                            <span class="compat-val" id="kDown">7A</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .prism-wrapper {
                background: radial-gradient(circle at center, #111 0%, #000 100%);
                border: 2px solid #222;
                border-radius: 12px;
                padding: 30px 10px;
                display: flex; flex-direction: column; align-items: center;
                box-shadow: inset 0 0 50px rgba(0,0,0,1);
            }

            .scene-3d {
                width: 150px;
                height: 150px;
                perspective: 800px;
                margin-bottom: 40px;
                position: relative;
            }
            
            /* Ground reflection glow */
            .scene-3d::after {
                content: ''; position: absolute; bottom: -30px; left: 50%; transform: translateX(-50%);
                width: 100px; height: 20px; background: rgba(0, 229, 255, 0.4); filter: blur(15px); border-radius: 50%;
            }

            .prism-object {
                width: 100%;
                height: 100%;
                position: relative;
                transform-style: preserve-3d;
                transition: transform 0.1s linear;
                transform: rotateX(-15deg) rotateY(0deg);
            }

            /* Constructing a 4-sided pyramid/prism */
            .prism-face {
                position: absolute;
                width: 150px;
                height: 150px;
                background: linear-gradient(135deg, rgba(0,229,255,0.4), rgba(212,175,55,0.1));
                border: 2px solid var(--cyan-neon);
                /* Triangle shape */
                clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
                transform-origin: bottom center;
                backdrop-filter: blur(5px); -webkit-backdrop-filter: blur(5px);
                box-shadow: inset 0 0 20px rgba(0,229,255,0.5);
            }

            /* Math for a perfect pyramid: angle is approx 30deg inward */
            .face-front  { transform: translateZ(75px) rotateX(30deg); }
            .face-right  { transform: rotateY(90deg) translateZ(75px) rotateX(30deg); }
            .face-back   { transform: rotateY(180deg) translateZ(75px) rotateX(30deg); }
            .face-left   { transform: rotateY(-90deg) translateZ(75px) rotateX(30deg); }
            
            /* Bottom base */
            .face-bottom {
                position: absolute; width: 150px; height: 150px;
                background: rgba(255,255,255,0.1); border: 2px solid var(--cyan-neon);
                transform: rotateX(90deg) translateZ(-75px);
                box-shadow: 0 0 30px rgba(0,229,255,0.8);
            }

            .prism-controls {
                width: 100%; background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #222;
            }
            .p-ctrl-row { display: flex; align-items: center; justify-content: space-between; margin-bottom: 10px; }
            .p-lbl { font-family: var(--font-data); font-size: 10px; color: #888; font-weight: bold; letter-spacing: 1px; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">HOLOGRAPHIC DMX PRISM</h2>
                <div class="section-icon"><i class="fas fa-gem"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Manipulate the physical 3D properties of the volumetric laser refraction crystal.</p>

            <div class="prism-wrapper">
                <div class="scene-3d">
                    <div class="prism-object" id="dmxPrism">
                        <div class="prism-face face-front"></div>
                        <div class="prism-face face-right"></div>
                        <div class="prism-face face-back"></div>
                        <div class="prism-face face-left"></div>
                        <div class="face-bottom"></div>
                    </div>
                </div>

                <div class="prism-controls">
                    <div class="p-ctrl-row">
                        <span class="p-lbl">Y-AXIS ROTATION</span>
                        <span class="p-lbl" id="pryVal" style="color:var(--cyan-neon);">0°</span>
                    </div>
                    <input type="range" class="app-slider" id="prismRotY" min="0" max="360" value="0" oninput="updatePrism3D()">

                    <div class="p-ctrl-row" style="margin-top: 15px;">
                        <span class="p-lbl">X-AXIS TILT</span>
                        <span class="p-lbl" id="prxVal" style="color:var(--gold-primary);">-15°</span>
                    </div>
                    <input type="range" class="app-slider" id="prismRotX" min="-60" max="60" value="-15" oninput="updatePrism3D()">
                </div>
                
                <button class="app-btn-outline" style="width: 100%; margin-top: 15px;" id="btnAutoSpin" onclick="togglePrismAutoSpin()">
                    <i class="fas fa-sync"></i> ENGAGE AUTO-SPIN
                </button>
            </div>
        </div>

        <script>
            // --- 1. ACOUSTIC FEEDBACK ELIMINATOR LOGIC ---
            const rtaCanvas = document.getElementById('rtaCanvas');
            let rtaCtx = null;
            const rtaWrap = document.getElementById('rtaWrap');
            
            let isRinging = false;
            let ringingBandIndex = -1; // 0 to 7
            let rtaAnimFrame = null;
            let feedbackAudioOsc = null;
            let feScore = 0;
            let ambientNoiseOffset = 0;

            function initRTA() {
                if(!rtaWrap || !rtaCanvas) return;
                rtaCanvas.width = rtaWrap.clientWidth;
                rtaCanvas.height = rtaWrap.clientHeight;
                rtaCtx = rtaCanvas.getContext('2d');
                if(!rtaAnimFrame) animateRTA();
            }
            window.addEventListener('resize', initRTA);
            setTimeout(initRTA, 500);

            function triggerRandomFeedback() {
                if(isRinging) return;
                if(typeof playTap === 'function') playTap();
                
                isRinging = true;
                // Pick a random band (0 to 7)
                ringingBandIndex = Math.floor(Math.random() * 8);
                
                // UI Alerts
                rtaWrap.classList.add('ringing');
                const txt = document.getElementById('rtaStatusTxt');
                txt.innerText = `WARNING: FEEDBACK AT BAND ${ringingBandIndex + 1}!`;
                txt.style.color = "var(--red-alert)";
                
                if(navigator.vibrate) navigator.vibrate([100, 50, 100, 50, 500]); // Alarm vibration

                // Generate physical sound if Web Audio Engine from Part 3 is active
                if(typeof actx !== 'undefined' && actx && actx.state === 'running') {
                    feedbackAudioOsc = actx.createOscillator();
                    const gain = actx.createGain();
                    
                    // Map band 0-7 to annoying frequencies (1k to 8k)
                    const freqs = [63, 160, 400, 1000, 2500, 4000, 6300, 10000];
                    feedbackAudioOsc.type = 'sine';
                    feedbackAudioOsc.frequency.value = freqs[ringingBandIndex] || 2000;
                    
                    feedbackAudioOsc.connect(gain);
                    gain.connect(actx.destination);
                    
                    gain.gain.setValueAtTime(0, actx.currentTime);
                    gain.gain.linearRampToValueAtTime(0.5, actx.currentTime + 0.5); // Fade in ring
                    feedbackAudioOsc.start();
                }
            }

            function checkFeedbackKill() {
                if(!isRinging) return;

                // Get all faders
                const faders = document.querySelectorAll('.fe-fader');
                const targetFader = faders[ringingBandIndex];
                
                // If user pulls the correct fader below -10, they win
                if(parseInt(targetFader.value) <= -10) {
                    killFeedback();
                }
            }

            function killFeedback() {
                isRinging = false;
                rtaWrap.classList.remove('ringing');
                
                const txt = document.getElementById('rtaStatusTxt');
                txt.innerText = "RTA: STABLE // FREQ NOTCHED";
                txt.style.color = "#00ff00";
                
                if(navigator.vibrate) navigator.vibrate(50);
                
                feScore += 100;
                document.getElementById('feScore').innerText = feScore;

                // Kill audio spike
                if(feedbackAudioOsc && typeof actx !== 'undefined') {
                    feedbackAudioOsc.stop(actx.currentTime + 0.1);
                    feedbackAudioOsc = null;
                }

                // Reset all faders physically after a delay
                setTimeout(() => {
                    const faders = document.querySelectorAll('.fe-fader');
                    faders.forEach(f => f.value = 0);
                    txt.innerText = "RTA: STABLE";
                }, 1500);
            }

            function animateRTA() {
                rtaAnimFrame = requestAnimationFrame(animateRTA);
                if(!rtaCtx) return;

                rtaCtx.clearRect(0, 0, rtaCanvas.width, rtaCanvas.height);
                ambientNoiseOffset += 0.1;

                const bins = 8;
                const barWidth = rtaCanvas.width / bins;
                
                // Draw 8 bars matching the graphic EQ
                for(let i=0; i<bins; i++) {
                    const x = i * barWidth;
                    let heightPct = 0;

                    if(isRinging && i === ringingBandIndex) {
                        // Massive red spike
                        heightPct = 0.9 + (Math.random() * 0.1); // Jitter at top
                        rtaCtx.fillStyle = 'var(--red-alert)';
                        rtaCtx.shadowBlur = 15;
                        rtaCtx.shadowColor = 'var(--red-alert)';
                    } else {
                        // Normal green ambient noise
                        let noise = Math.sin(i + ambientNoiseOffset) * Math.cos(i * 0.5 - ambientNoiseOffset);
                        heightPct = Math.abs(noise) * 0.3 + 0.1; // 10% to 40% high
                        rtaCtx.fillStyle = 'rgba(0, 255, 0, 0.6)';
                        rtaCtx.shadowBlur = 0;
                    }
                    
                    // Add physical fader offset to the visual display
                    const faders = document.querySelectorAll('.fe-fader');
                    if(faders[i]) {
                        // Slider is -20 to 20. Map to -0.2 to 0.2 height modification
                        const faderMod = parseInt(faders[i].value) / 100;
                        heightPct += faderMod;
                    }
                    
                    // Clamp
                    heightPct = Math.max(0.05, Math.min(1.0, heightPct));
                    
                    const h = heightPct * rtaCanvas.height;
                    const y = rtaCanvas.height - h;
                    
                    rtaCtx.fillRect(x + 2, y, barWidth - 4, h);
                    
                    // Top cap
                    rtaCtx.fillStyle = '#fff';
                    rtaCtx.fillRect(x + 2, y, barWidth - 4, 3);
                }
                rtaCtx.shadowBlur = 0; // reset
            }


            // --- 2. HARMONIC MIXING AI LOGIC ---
            // Camelot Wheel Dictionary mapping keys to their Musical Equivalents
            const camelotMap = {
                '1A': 'Ab Minor', '1B': 'B Major',
                '2A': 'Eb Minor', '2B': 'F# Major',
                '3A': 'Bb Minor', '3B': 'Db Major',
                '4A': 'F Minor',  '4B': 'Ab Major',
                '5A': 'C Minor',  '5B': 'Eb Major',
                '6A': 'G Minor',  '6B': 'Bb Major',
                '7A': 'D Minor',  '7B': 'F Major',
                '8A': 'A Minor',  '8B': 'C Major',
                '9A': 'E Minor',  '9B': 'G Major',
                '10A': 'B Minor', '10B': 'D Major',
                '11A': 'F# Minor','11B': 'A Major',
                '12A': 'Db Minor','12B': 'E Major'
            };

            function calculateHarmonics() {
                const inputEl = document.getElementById('currentKeyInp');
                let key = inputEl.value.toUpperCase().trim();
                
                // Allow user to keep typing, only calculate if valid format (Number + A/B)
                const regex = /^([1-9]|1[0-2])[AB]$/;
                
                if(regex.test(key)) {
                    if(navigator.vibrate) navigator.vibrate(10);
                    inputEl.style.borderColor = "var(--cyan-neon)";
                    inputEl.style.boxShadow = "0 0 15px rgba(0,229,255,0.2)";

                    // Update Musical Name
                    document.getElementById('musicalNoteName').innerText = camelotMap[key] || "Unknown";

                    // Math Logic
                    let num = parseInt(key.slice(0, -1));
                    let letter = key.slice(-1);

                    // Perfect Match = Same Key
                    document.getElementById('kPerf').innerText = key;

                    // Relative Match = Swap A/B
                    document.getElementById('kRel').innerText = num + (letter === 'A' ? 'B' : 'A');

                    // Energy Up = +1
                    let upNum = num + 1;
                    if(upNum > 12) upNum = 1;
                    document.getElementById('kUp').innerText = upNum + letter;

                    // Energy Down = -1
                    let downNum = num - 1;
                    if(downNum < 1) downNum = 12;
                    document.getElementById('kDown').innerText = downNum + letter;

                } else if (key.length >= 2) {
                    // Invalid input warning
                    inputEl.style.borderColor = "var(--red-alert)";
                    inputEl.style.boxShadow = "0 0 15px rgba(255,51,51,0.5)";
                    document.getElementById('musicalNoteName').innerText = "INVALID KEY";
                    document.getElementById('kPerf').innerText = "-";
                    document.getElementById('kRel').innerText = "-";
                    document.getElementById('kUp').innerText = "-";
                    document.getElementById('kDown').innerText = "-";
                }
            }
            // Init run on load
            calculateHarmonics();


            // --- 3. 3D DMX HOLOGRAPHIC PRISM LOGIC ---
            const prismObj = document.getElementById('dmxPrism');
            let prismRotY = 0;
            let prismRotX = -15;
            let pAutoSpinTimer = null;

            function updatePrism3D() {
                // If dragging sliders manually, stop auto-spin
                if(pAutoSpinTimer) togglePrismAutoSpin(); 

                prismRotY = parseInt(document.getElementById('prismRotY').value);
                prismRotX = parseInt(document.getElementById('prismRotX').value);
                
                applyPrismTransform();
            }

            function applyPrismTransform() {
                // Update UI text
                document.getElementById('pryVal').innerText = `${prismRotY}°`;
                document.getElementById('prxVal').innerText = `${prismRotX}°`;

                // Apply CSS Transform
                prismObj.style.transform = `rotateX(${prismRotX}deg) rotateY(${prismRotY}deg)`;
            }

            function togglePrismAutoSpin() {
                if(typeof playTap === 'function') playTap();
                const btn = document.getElementById('btnAutoSpin');
                
                if(pAutoSpinTimer) {
                    // Stop
                    clearInterval(pAutoSpinTimer);
                    pAutoSpinTimer = null;
                    btn.innerHTML = '<i class="fas fa-sync"></i> ENGAGE AUTO-SPIN';
                    btn.style.color = "var(--cyan-neon)";
                    btn.style.borderColor = "var(--cyan-neon)";
                } else {
                    // Start
                    btn.innerHTML = '<i class="fas fa-pause"></i> HALT MOTORS';
                    btn.style.color = "var(--red-alert)";
                    btn.style.borderColor = "var(--red-alert)";
                    
                    pAutoSpinTimer = setInterval(() => {
                        prismRotY += 2; // Spin speed
                        if(prismRotY >= 360) prismRotY = 0;
                        
                        // Sync slider visually so it moves by itself
                        document.getElementById('prismRotY').value = prismRotY;
                        applyPrismTransform();
                    }, 30); // 30ms frame update
                }
            }
        </script>
        <style>
            .cardioid-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            }

            .cardioid-canvas-box {
                width: 100%;
                height: 250px;
                background: #050a10;
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #cardioidCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .sub-array-visual {
                position: absolute; top: 50%; left: 30%; transform: translate(-50%, -50%);
                display: flex; flex-direction: column; gap: 2px; z-index: 10;
            }
            .sub-box {
                width: 16px; height: 24px; background: #111; border: 1px solid #555; border-radius: 2px;
                display: flex; justify-content: center; align-items: center; position: relative;
            }
            .sub-box::after { content:''; width:8px; height:8px; background:#000; border-radius:50%; }
            
            /* The inverted sub in a cardioid setup */
            .sub-box.inverted { border-color: var(--red-alert); background: #2a0000; }
            .sub-box.inverted::after { left: -2px; position: absolute; } /* Represents speaker facing backward */

            .cardioid-controls {
                display: flex; justify-content: space-between; gap: 10px; margin-top: 15px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">SUB ARRAY PHYSICS</h2>
                <div class="section-icon"><i class="fas fa-broadcast-tower"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate rear-cancellation. Toggle Cardioid mode to prevent bass bleed onto the FOH stage.</p>

            <div class="cardioid-wrapper">
                <div class="cardioid-canvas-box" id="cardioidWrap">
                    <canvas id="cardioidCanvas"></canvas>
                    <div class="sub-array-visual" id="subArrayDOM">
                        <div class="sub-box"></div>
                        <div class="sub-box inverted" id="rearSub"></div>
                        <div class="sub-box"></div>
                    </div>
                    <div style="position:absolute; top:10px; left:10px; color:#fff; font-family:var(--font-tech); font-size:8px; opacity:0.5;">STAGE LEFT &nbsp; | &nbsp; AUDIENCE RIGHT</div>
                </div>

                <div class="cardioid-controls">
                    <button class="app-btn-outline" id="btnOmni" style="flex:1; border-color:var(--red-alert); color:var(--red-alert);" onclick="setArrayMode('omni')">OMNIDIRECTIONAL</button>
                    <button class="app-btn-outline active" id="btnCardioid" style="flex:1; border-color:var(--cyan-neon); color:var(--cyan-neon); background: rgba(0,229,255,0.1);" onclick="setArrayMode('cardioid')">CARDIOID MODE</button>
                </div>
            </div>
        </div>

        <style>
            .vector-wrapper {
                background: #020202;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .vector-canvas-box {
                width: 100%;
                height: 260px;
                background: radial-gradient(circle at center, #111 0%, #000 100%);
                border: 2px solid var(--gold-primary);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                touch-action: none; /* Crucial for dragging target */
            }
            #vectorCanvas { width: 100%; height: 100%; display: block; z-index: 1; position: relative;}

            /* Virtual Moving Head Fixture (Top Down) */
            .fixture-base {
                position: absolute; top: 20px; left: 50%; transform: translateX(-50%);
                width: 40px; height: 40px; background: #111; border: 2px solid #444; border-radius: 50%;
                z-index: 5; display: flex; justify-content: center; align-items: center;
                box-shadow: 0 5px 15px rgba(0,0,0,0.9);
            }
            .fixture-head {
                width: 20px; height: 30px; background: #222; border: 2px solid var(--gold-primary); border-radius: 4px;
                position: relative; transform-origin: center center; transition: transform 0.1s ease-out;
            }
            .fixture-lens { position: absolute; bottom: -2px; left: 2px; width: 12px; height: 4px; background: #fff; border-radius: 2px; box-shadow: 0 0 10px #fff;}

            /* Draggable Target Reticle */
            .vector-target {
                position: absolute; top: 180px; left: 50%; transform: translate(-50%, -50%);
                width: 30px; height: 30px; border: 2px dashed var(--red-alert); border-radius: 50%;
                z-index: 10; cursor: grab; display: flex; justify-content: center; align-items: center;
                animation: pulseTarget 2s infinite;
            }
            .vector-target::after { content: '+'; color: var(--red-alert); font-family: monospace; font-size: 20px; }
            .vector-target:active { cursor: grabbing; border-style: solid; background: rgba(255,51,51,0.2); }
            
            @keyframes pulseTarget { 0% { transform: translate(-50%, -50%) scale(1); } 50% { transform: translate(-50%, -50%) scale(1.2); } 100% { transform: translate(-50%, -50%) scale(1); } }

            .vector-hud {
                display: flex; justify-content: space-between; margin-top: 15px;
                background: #0a0a0f; padding: 10px; border-radius: 6px; border: 1px solid #222;
            }
            .vh-val { font-family: var(--font-tech); font-size: 14px; color: var(--cyan-neon); font-weight: bold; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">VECTOR TARGETING AI</h2>
                <div class="section-icon"><i class="fas fa-crosshairs"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Drag the red reticle. The AI mathematically calculates the arctangent vector to rotate the DMX fixture.</p>

            <div class="vector-wrapper">
                <div class="vector-canvas-box" id="vectorWrap">
                    <canvas id="vectorCanvas"></canvas>
                    
                    <div class="fixture-base" id="fixBase">
                        <div class="fixture-head" id="fixHead"><div class="fixture-lens"></div></div>
                    </div>
                    
                    <div class="vector-target" id="vectorTarget" onmousedown="startVecDrag(event)" ontouchstart="startVecDrag(event)"></div>
                </div>

                <div class="vector-hud">
                    <div style="display:flex; flex-direction:column;">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888;">PAN ANGLE (θ)</span>
                        <span class="vh-val" id="vecAngleDisplay">0.0°</span>
                    </div>
                    <div style="display:flex; flex-direction:column; text-align:right;">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888;">DISTANCE (r)</span>
                        <span class="vh-val" id="vecDistDisplay" style="color:var(--gold-primary);">0.0m</span>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .foh-wrapper {
                background: linear-gradient(180deg, #111, #050505);
                border: 2px solid #222;
                border-radius: 12px;
                padding: 20px 10px;
                box-shadow: inset 0 0 20px rgba(0,0,0,1);
            }

            .foh-fader-board {
                display: flex; justify-content: space-around; position: relative;
            }

            .foh-channel {
                display: flex; flex-direction: column; align-items: center; width: 40px;
            }

            /* The Fader Track */
            .foh-track {
                width: 8px; height: 150px; background: #000; border-radius: 4px;
                position: relative; border: 1px solid #333; box-shadow: inset 0 2px 10px rgba(0,0,0,1);
                margin: 20px 0;
            }
            /* Measurement lines next to fader */
            .foh-track::before {
                content: ''; position: absolute; left: -10px; top: 0; bottom: 0; width: 4px;
                background: repeating-linear-gradient(180deg, #555 0px, #555 2px, transparent 2px, transparent 15px);
            }

            /* The Motorized Knob */
            .foh-knob {
                width: 26px; height: 40px;
                background: linear-gradient(180deg, #ddd, #888);
                border: 2px solid #111; border-radius: 4px;
                position: absolute; bottom: 10px; left: 50%; transform: translateX(-50%);
                box-shadow: 0 10px 15px rgba(0,0,0,0.8); cursor: grab;
                transition: bottom 0.8s cubic-bezier(0.25, 1, 0.5, 1); /* Slow robotic glide */
            }
            /* Indentation on knob */
            .foh-knob::after { content: ''; position: absolute; top: 50%; left: 5px; right: 5px; height: 3px; background: #000; transform: translateY(-50%); }
            
            .foh-knob.dragging { transition: none; cursor: grabbing; }

            .foh-ch-label {
                background: #222; padding: 5px; width: 100%; text-align: center;
                font-family: var(--font-data); font-size: 10px; font-weight: bold; border-radius: 3px;
                color: #aaa; text-transform: uppercase; border-bottom: 2px solid var(--cyan-neon);
            }

            /* Master Fader specific styles */
            .ch-master .foh-ch-label { color: #fff; border-bottom-color: var(--red-alert); background: #330000;}
            .ch-master .foh-knob { background: linear-gradient(180deg, #ff6666, #990000); }

            .foh-controls {
                display: flex; gap: 10px; margin-top: 15px; border-top: 1px dashed #333; padding-top: 15px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">MOTORIZED FOH CONSOLE</h2>
                <div class="section-icon"><i class="fas fa-sliders-h"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate physical motorized faders. Tap the auto-mix protocol to watch the hardware slide into position.</p>

            <div class="foh-wrapper">
                <div class="foh-fader-board" id="fohBoard">
                    
                    <div class="foh-channel">
                        <div class="foh-track"><div class="foh-knob" id="fdrKick" style="bottom: 10%;"></div></div>
                        <div class="foh-ch-label" style="border-color:#ff3333;">KICK</div>
                    </div>
                    
                    <div class="foh-channel">
                        <div class="foh-track"><div class="foh-knob" id="fdrBass" style="bottom: 10%;"></div></div>
                        <div class="foh-ch-label" style="border-color:var(--gold-primary);">BASS</div>
                    </div>

                    <div class="foh-channel">
                        <div class="foh-track"><div class="foh-knob" id="fdrVox" style="bottom: 10%;"></div></div>
                        <div class="foh-ch-label" style="border-color:var(--cyan-neon);">VOX</div>
                    </div>

                    <div style="width: 2px; background: #222; border-right: 1px solid #111; margin: 0 5px;"></div>

                    <div class="foh-channel ch-master">
                        <div class="foh-track"><div class="foh-knob" id="fdrMaster" style="bottom: 10%;"></div></div>
                        <div class="foh-ch-label">MASTER</div>
                    </div>

                </div>

                <div class="foh-controls">
                    <button class="app-btn-outline" style="flex: 1;" onclick="resetFaders()">ZERO MIX</button>
                    <button class="app-btn-primary" style="flex: 2; padding: 10px;" onclick="engageAutoMix()">
                        <i class="fas fa-robot"></i> AUTO-MIX PROTOCOL
                    </button>
                </div>
            </div>
        </div>

        <script>
            // --- 1. CARDIOID SUBWOOFER ARRAY LOGIC ---
            const cCanvas = document.getElementById('cardioidCanvas');
            let cCtx = null;
            const cWrap = document.getElementById('cardioidWrap');
            let cardioidMode = 'cardioid'; // 'omni' or 'cardioid'
            let cAnimFrame = null;
            let cWaveTime = 0;

            function initCardioid() {
                if(!cWrap || !cCanvas) return;
                cCanvas.width = cWrap.clientWidth;
                cCanvas.height = cWrap.clientHeight;
                cCtx = cCanvas.getContext('2d');
                if(!cAnimFrame) animateCardioid();
            }
            window.addEventListener('resize', initCardioid);
            setTimeout(initCardioid, 500);

            function setArrayMode(mode) {
                if(typeof playTap === 'function') playTap();
                cardioidMode = mode;
                
                const btnOmni = document.getElementById('btnOmni');
                const btnCard = document.getElementById('btnCardioid');
                const rearSub = document.getElementById('rearSub');

                if(mode === 'omni') {
                    btnOmni.classList.add('active');
                    btnOmni.style.background = 'rgba(255,51,51,0.1)';
                    btnCard.classList.remove('active');
                    btnCard.style.background = 'transparent';
                    
                    // Visually flip the rear sub to face forward (standard array)
                    rearSub.classList.remove('inverted');
                    if(navigator.vibrate) navigator.vibrate(20);
                } else {
                    btnCard.classList.add('active');
                    btnCard.style.background = 'rgba(0,229,255,0.1)';
                    btnOmni.classList.remove('active');
                    btnOmni.style.background = 'transparent';
                    
                    // Flip rear sub backward
                    rearSub.classList.add('inverted');
                    if(navigator.vibrate) navigator.vibrate(20);
                }
            }

            function animateCardioid() {
                cAnimFrame = requestAnimationFrame(animateCardioid);
                if(!cCtx) return;

                // Motion fade
                cCtx.fillStyle = 'rgba(5, 10, 16, 0.4)';
                cCtx.fillRect(0, 0, cCanvas.width, cCanvas.height);

                cWaveTime += 1.5;

                // Sub array is fixed at left 30%, center Y
                const cx = cCanvas.width * 0.3;
                const cy = cCanvas.height / 2;

                cCtx.lineWidth = 3;

                // Draw 6 expanding waves
                for(let i=0; i<6; i++) {
                    let r = (cWaveTime + (i * 45)) % 250;
                    
                    if(r > 0) {
                        const alpha = 1 - (r / 250);
                        
                        if(cardioidMode === 'omni') {
                            // Perfect circles expanding in all directions
                            cCtx.strokeStyle = `rgba(255, 51, 51, ${alpha})`; // Red
                            cCtx.beginPath();
                            cCtx.arc(cx, cy, r, 0, Math.PI*2);
                            cCtx.stroke();
                        } else {
                            // Cardioid physics trick: Heart shape/Directed beam
                            // Draw front wave (Right side)
                            cCtx.strokeStyle = `rgba(0, 229, 255, ${alpha})`; // Cyan
                            cCtx.beginPath();
                            // Arc from top to bottom, curving right
                            cCtx.arc(cx, cy, r, -Math.PI/2, Math.PI/2);
                            cCtx.stroke();

                            // The magic visual cancellation at the rear
                            // We draw a smaller, fainter, flattened wave to the left
                            const rearR = r * 0.4; // Massively reduced energy
                            if(rearR > 0) {
                                cCtx.strokeStyle = `rgba(100, 100, 100, ${alpha * 0.5})`; // Faint grey
                                cCtx.beginPath();
                                cCtx.ellipse(cx, cy, rearR, r*0.8, 0, Math.PI/2, -Math.PI/2);
                                cCtx.stroke();
                            }
                        }
                    }
                }
            }


            // --- 2. MOVING HEAD VECTOR TARGETING AI LOGIC ---
            const vCanvas = document.getElementById('vectorCanvas');
            let vCtx = null;
            const vWrap = document.getElementById('vectorWrap');
            const target = document.getElementById('vectorTarget');
            const fixHead = document.getElementById('fixHead');
            const fixBase = document.getElementById('fixBase');
            
            let isVecDragging = false;
            let vecAnimFrame = null;

            function initVectorEngine() {
                if(!vWrap || !vCanvas) return;
                vCanvas.width = vWrap.clientWidth;
                vCanvas.height = vWrap.clientHeight;
                vCtx = vCanvas.getContext('2d');
                if(!vecAnimFrame) animateVectorBeam();
            }
            window.addEventListener('resize', initVectorEngine);
            setTimeout(initVectorEngine, 800);

            function startVecDrag(e) {
                if(e.type === 'touchstart') e.preventDefault();
                if(typeof playTap === 'function') playTap();
                isVecDragging = true;
                target.style.animation = 'none'; // Stop pulsing while dragging
            }

            document.addEventListener('mousemove', vecDragMove);
            document.addEventListener('touchmove', vecDragMove, {passive: false});

            function vecDragMove(e) {
                if (!isVecDragging) return;
                e.preventDefault();
                
                const rect = vWrap.getBoundingClientRect();
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                
                let x = touch.clientX - rect.left;
                let y = touch.clientY - rect.top;
                
                // Clamp
                if(x < 15) x = 15; if(x > rect.width - 15) x = rect.width - 15;
                if(y < 15) y = 15; if(y > rect.height - 15) y = rect.height - 15;

                target.style.left = `${x}px`;
                target.style.top = `${y}px`;
            }

            document.addEventListener('mouseup', endVecDrag);
            document.addEventListener('touchend', endVecDrag);

            function endVecDrag() {
                if(isVecDragging) {
                    isVecDragging = false;
                    target.style.animation = 'pulseTarget 2s infinite';
                }
            }

            function animateVectorBeam() {
                vecAnimFrame = requestAnimationFrame(animateVectorBeam);
                if(!vCtx) return;

                // 1. Math Calculation
                // Get absolute coordinates relative to the wrapper
                const tRect = target.getBoundingClientRect();
                const bRect = fixBase.getBoundingClientRect();
                const wRect = vWrap.getBoundingClientRect();

                // Target center
                const tx = (tRect.left - wRect.left) + (tRect.width/2);
                const ty = (tRect.top - wRect.top) + (tRect.height/2);

                // Fixture center
                const fx = (bRect.left - wRect.left) + (bRect.width/2);
                const fy = (bRect.top - wRect.top) + (bRect.height/2);

                // Trigonometry: Math.atan2 gives angle in radians from X-axis.
                // We want 0 degrees to be pointing STRAIGHT DOWN (Y-axis positive).
                const dx = tx - fx;
                const dy = ty - fy;
                let angleRad = Math.atan2(dy, dx);
                
                // Convert to degrees. Default CSS has it pointing up, so we subtract 90.
                let angleDeg = (angleRad * (180 / Math.PI)) - 90;

                // Update physical CSS rotation of the moving head
                fixHead.style.transform = `rotate(${angleDeg}deg)`;

                // Math Distance
                const distPx = Math.hypot(dx, dy);
                // Fake meters (10px = 1m)
                const distM = (distPx * 0.1).toFixed(1);

                // Update HUD
                document.getElementById('vecAngleDisplay').innerText = `${Math.round(angleDeg + 90)}°`;
                document.getElementById('vecDistDisplay').innerText = `${distM}m`;

                // 2. Draw the volumetric beam on Canvas
                vCtx.clearRect(0,0, vCanvas.width, vCanvas.height);

                vCtx.globalCompositeOperation = 'screen';
                
                // Create gradient beam
                const grad = vCtx.createLinearGradient(fx, fy, tx, ty);
                grad.addColorStop(0, 'rgba(212, 175, 55, 0.8)'); // Gold at source
                grad.addColorStop(1, 'rgba(212, 175, 55, 0.0)'); // Fade out

                vCtx.fillStyle = grad;
                
                // Draw a triangle cone from fixture to target
                // Calculate perpendicular offsets for beam spread
                const spread = distPx * 0.2; // Beam gets wider the further it goes
                const perpAngle = angleRad + (Math.PI/2);
                const p1x = tx + Math.cos(perpAngle) * spread;
                const p1y = ty + Math.sin(perpAngle) * spread;
                const p2x = tx - Math.cos(perpAngle) * spread;
                const p2y = ty - Math.sin(perpAngle) * spread;

                vCtx.beginPath();
                vCtx.moveTo(fx, fy); // Point of fixture
                vCtx.lineTo(p1x, p1y);
                vCtx.lineTo(p2x, p2y);
                vCtx.closePath();
                vCtx.fill();
                
                vCtx.globalCompositeOperation = 'source-over';
            }


            // --- 3. MOTORIZED FOH MIXING CONSOLE LOGIC ---
            // Touch/Drag logic for custom faders
            const knobs = document.querySelectorAll('.foh-knob');
            let activeFader = null;
            let faderStartY = 0;
            let faderStartBot = 0; // The bottom %

            knobs.forEach(knob => {
                knob.addEventListener('mousedown', faderDragStart);
                knob.addEventListener('touchstart', (e) => { e.preventDefault(); faderDragStart(e); }, {passive: false});
            });

            function faderDragStart(e) {
                if(typeof playTap === 'function') playTap();
                activeFader = e.currentTarget;
                activeFader.classList.add('dragging'); // Removes CSS transition for instant tracking
                
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                faderStartY = touch.clientY;
                // Parse current bottom %
                faderStartBot = parseFloat(activeFader.style.bottom) || 10;
            }

            document.addEventListener('mousemove', faderDragMove);
            document.addEventListener('touchmove', faderDragMove, {passive: false});

            function faderDragMove(e) {
                if (!activeFader) return;
                e.preventDefault();
                
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                const deltaY = faderStartY - touch.clientY; // Inverted because bottom is 0
                
                // Track is 150px tall. Translate pixel delta to percentage.
                const deltaPct = (deltaY / 150) * 100;
                
                let newBot = faderStartBot + deltaPct;
                // Clamp 0 to 100%
                if(newBot < 0) newBot = 0;
                if(newBot > 100) newBot = 100;
                
                activeFader.style.bottom = `${newBot}%`;
            }

            document.addEventListener('mouseup', faderDragEnd);
            document.addEventListener('touchend', faderDragEnd);

            function faderDragEnd() {
                if(activeFader) {
                    activeFader.classList.remove('dragging');
                    activeFader = null;
                }
            }

            function resetFaders() {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                
                knobs.forEach(knob => {
                    knob.style.bottom = '0%';
                });
            }

            function engageAutoMix() {
                if(typeof triggerToast === 'function') triggerToast("Auto-Mix Protocol Executing.");
                if(navigator.vibrate) navigator.vibrate([100, 50, 100, 50, 200]);
                
                // Target preset positions for a "heavy dance mix"
                const presets = {
                    'fdrKick': 85,
                    'fdrBass': 90,
                    'fdrVox': 60,
                    'fdrMaster': 80
                };

                // Because we set CSS transition: bottom 0.8s, setting the inline style 
                // causes them to physically "glide" like real motorized FOH faders.
                for (const [id, val] of Object.entries(presets)) {
                    // Stagger the movement slightly for realism
                    setTimeout(() => {
                        const knob = document.getElementById(id);
                        if(knob) knob.style.bottom = `${val}%`;
                    }, Math.random() * 200);
                }
            }
        </script>
        <style>
            .safe-zone-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
                position: relative;
            }

            .laser-canvas-box {
                width: 100%;
                height: 280px;
                background: linear-gradient(180deg, #05050a 0%, #001122 100%);
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                touch-action: none;
                box-shadow: inset 0 0 30px rgba(0, 229, 255, 0.1);
            }
            #laserSafetyCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Virtual Laser Emitter */
            .laser-rig-top {
                position: absolute; top: 0; left: 50%; transform: translateX(-50%);
                width: 100px; height: 10px; background: #333; border-bottom: 2px solid var(--cyan-neon);
                display: flex; justify-content: space-around; align-items: flex-end; z-index: 5;
            }
            .laser-node { width: 6px; height: 6px; background: #fff; border-radius: 50%; box-shadow: 0 0 10px #fff; margin-bottom: -3px; }

            /* Draggable Audience Safety Line */
            .safety-barrier {
                position: absolute; left: 0; right: 0; height: 4px;
                background: var(--red-alert); box-shadow: 0 0 15px var(--red-alert);
                cursor: ns-resize; z-index: 10; display: flex; justify-content: center; align-items: center;
            }
            .safety-barrier::before {
                content: 'CROWD EYE-LEVEL LIMIT'; position: absolute; top: -15px;
                font-family: var(--font-tech); font-size: 8px; color: var(--red-alert); letter-spacing: 2px;
            }
            .safety-barrier-handle {
                width: 40px; height: 16px; background: #111; border: 2px solid var(--red-alert);
                border-radius: 8px; display: flex; justify-content: center; align-items: center; gap: 2px;
            }
            .safety-barrier-handle span { width: 4px; height: 4px; background: var(--red-alert); border-radius: 50%; }
            .safety-zone-fill {
                position: absolute; bottom: 0; left: 0; right: 0;
                background: repeating-linear-gradient(45deg, rgba(255,51,51,0.1), rgba(255,51,51,0.1) 10px, transparent 10px, transparent 20px);
                pointer-events: none; z-index: 1; border-top: 1px dashed rgba(255,51,51,0.5);
            }

            .sz-controls { display: flex; justify-content: space-between; margin-top: 15px; }
            .sz-stat { background: #0a0a0f; border: 1px solid #222; padding: 10px; border-radius: 6px; flex: 1; margin: 0 5px; text-align: center; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">LASER SAFE-ZONE MAPPER</h2>
                <div class="section-icon"><i class="fas fa-shield-alt"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Drag the red barrier to set the Crowd Eye-Level. The AI mathematically cuts off intersecting high-power beams.</p>

            <div class="safe-zone-wrapper">
                <div class="laser-canvas-box" id="safeZoneWrap">
                    <div class="laser-rig-top">
                        <div class="laser-node"></div><div class="laser-node"></div><div class="laser-node"></div>
                    </div>
                    
                    <canvas id="laserSafetyCanvas"></canvas>
                    
                    <div class="safety-zone-fill" id="szFill" style="height: 80px;"></div>
                    <div class="safety-barrier" id="szBarrier" style="bottom: 80px;">
                        <div class="safety-barrier-handle"><span></span><span></span><span></span></div>
                    </div>
                </div>

                <div class="sz-controls">
                    <div class="sz-stat">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888; display:block;">STATUS</span>
                        <span style="font-family:var(--font-tech); font-size:14px; color:#00ff00; font-weight:bold;" id="szStatus">SECURE</span>
                    </div>
                    <div class="sz-stat">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888; display:block;">CUTOFF Y-AXIS</span>
                        <span style="font-family:var(--font-tech); font-size:14px; color:var(--red-alert); font-weight:bold;" id="szLimitVal">80px</span>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .compressor-wrapper {
                background: #020408;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .comp-display {
                width: 100%;
                height: 180px;
                background: #000;
                border: 2px solid #333;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 20px rgba(0,0,0,0.8);
            }
            #compCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2; }
            
            /* Center Line */
            .comp-display::before {
                content: ''; position: absolute; top: 50%; left: 0; width: 100%; height: 1px;
                background: rgba(255,255,255,0.2); z-index: 1; pointer-events: none;
            }

            .comp-hud {
                display: flex; justify-content: space-between; margin-top: 15px;
                background: #0a0a10; padding: 10px; border-radius: 6px; border: 1px solid #222;
            }
            .ch-box { display: flex; flex-direction: column; align-items: center; }
            .ch-lbl { font-family: var(--font-data); font-size: 9px; color: #888; letter-spacing: 1px; margin-bottom: 4px; }
            .ch-val { font-family: var(--font-tech); font-size: 16px; font-weight: 900; color: #fff; }

            .comp-slider-box { margin-top: 15px; }
            
            /* Gain Reduction Meter */
            .gr-meter { width: 100%; height: 8px; background: #111; border-radius: 4px; margin-top: 10px; border: 1px solid #333; overflow: hidden; display: flex; justify-content: flex-end;}
            .gr-fill { width: 0%; height: 100%; background: var(--red-alert); transition: width 0.1s; transform-origin: right; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DYNAMICS COMPRESSOR</h2>
                <div class="section-icon"><i class="fas fa-compress-arrows-alt"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Adjust the Threshold slider to squash audio peaks and protect the speaker cones from blowing out.</p>

            <div class="compressor-wrapper">
                <div class="comp-display" id="compWrap">
                    <canvas id="compCanvas"></canvas>
                    <div style="position:absolute; top:5px; left:5px; color:#aaa; font-family:var(--font-tech); font-size:8px; z-index:5;">AUDIO WAVEFORM</div>
                </div>

                <div class="comp-hud">
                    <div class="ch-box">
                        <span class="ch-lbl">THRESHOLD LIMIT</span>
                        <span class="ch-val" id="compThreshVal" style="color:var(--gold-primary);">100%</span>
                    </div>
                    <div class="ch-box">
                        <span class="ch-lbl">RATIO</span>
                        <span class="ch-val" style="color:var(--cyan-neon);">4:1</span>
                    </div>
                    <div class="ch-box">
                        <span class="ch-lbl">GAIN REDUCTION</span>
                        <span class="ch-val" id="compGrVal" style="color:var(--red-alert);">-0.0 dB</span>
                    </div>
                </div>

                <div class="comp-slider-box">
                    <span style="font-family:var(--font-data); font-size:10px; color:#fff; font-weight:bold;">THRESHOLD dB</span>
                    <input type="range" class="app-slider" id="compSlider" min="10" max="100" value="100" style="margin-top: 5px;" oninput="updateCompressor()">
                    
                    <span style="font-family:var(--font-data); font-size:9px; color:#888; display:block; margin-top:10px;">GR METER</span>
                    <div class="gr-meter"><div class="gr-fill" id="grBar"></div></div>
                </div>
            </div>
        </div>

        <style>
            .gen-sync-wrapper {
                background: #000;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .sync-canvas-box {
                width: 100%;
                height: 160px;
                background: #050505;
                border: 1px solid #111;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #syncCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .sync-hud {
                display: flex; justify-content: space-between; align-items: center;
                background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #222; margin-top: 15px;
            }
            .sh-stat { text-align: center; }
            .sh-lbl { font-family: var(--font-data); font-size: 9px; color: #888; font-weight: bold; margin-bottom: 5px; display: block;}
            .sh-val { font-family: var(--font-tech); font-size: 16px; font-weight: 900; color: #fff; }
            
            .sh-status-indicator {
                padding: 8px 15px; border-radius: 4px; font-family: var(--font-tech); font-size: 11px;
                font-weight: bold; background: rgba(255,51,51,0.1); border: 1px solid var(--red-alert); color: var(--red-alert);
                transition: 0.3s;
            }
            .sh-status-indicator.locked {
                background: rgba(0,255,0,0.1); border-color: #00ff00; color: #00ff00; box-shadow: 0 0 15px rgba(0,255,0,0.4);
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">PARALLEL SYNC MATRIX</h2>
                <div class="section-icon"><i class="fas fa-link"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Adjust Gen B Alternator Phase to perfectly overlap the AC sine waves before combining power lines.</p>

            <div class="gen-sync-wrapper">
                <div class="sync-canvas-box" id="syncWrap">
                    <canvas id="syncCanvas"></canvas>
                    <div style="position:absolute; top:5px; left:5px; color:var(--cyan-neon); font-family:var(--font-data); font-size:9px;">GEN A (REFERENCE)</div>
                    <div style="position:absolute; bottom:5px; left:5px; color:var(--gold-primary); font-family:var(--font-data); font-size:9px;">GEN B (ADJUSTING)</div>
                </div>

                <div class="sync-hud">
                    <div class="sh-stat">
                        <span class="sh-lbl">PHASE DIFFERENCE</span>
                        <span class="sh-val" id="phaseDiffVal">180°</span>
                    </div>
                    <div class="sh-status-indicator" id="syncStatusPlate">OUT OF PHASE</div>
                </div>

                <div style="margin-top: 15px; text-align: center;">
                    <span style="font-family:var(--font-data); font-size:10px; color:#fff; font-weight:bold;">ALTERNATOR RPM ADJUST</span>
                    <input type="range" class="app-slider" id="genSyncSlider" min="0" max="360" value="180" style="margin-top: 10px;" oninput="updateGenPhase(this.value)">
                </div>
            </div>
        </div>

        <script>
            // --- 1. LASER SAFE-ZONE MAPPER LOGIC ---
            const szCanvas = document.getElementById('laserSafetyCanvas');
            let szCtx = null;
            const szWrap = document.getElementById('safeZoneWrap');
            const szBarrier = document.getElementById('szBarrier');
            const szFill = document.getElementById('szFill');
            
            let isSzDragging = false;
            let szStartY = 0;
            let szStartBottom = 80;
            let szAnimFrame = null;
            let szTime = 0;

            function initSafeZone() {
                if(!szWrap || !szCanvas) return;
                szCanvas.width = szWrap.clientWidth;
                szCanvas.height = szWrap.clientHeight;
                szCtx = szCanvas.getContext('2d');
                if(!szAnimFrame) animateLaserSafeZone();
            }
            window.addEventListener('resize', initSafeZone);
            setTimeout(initSafeZone, 500);

            // Drag logic for the Red Barrier
            szBarrier.addEventListener('mousedown', szDragStart);
            szBarrier.addEventListener('touchstart', (e) => { e.preventDefault(); szDragStart(e); }, {passive: false});

            function szDragStart(e) {
                if(typeof playTap === 'function') playTap();
                isSzDragging = true;
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                szStartY = touch.clientY;
                szStartBottom = parseInt(szBarrier.style.bottom) || 80;
            }

            document.addEventListener('mousemove', szDragMove);
            document.addEventListener('touchmove', szDragMove, {passive: false});

            function szDragMove(e) {
                if (!isSzDragging) return;
                e.preventDefault();
                
                const touch = e.type.includes('touch') ? e.touches[0] : e;
                const deltaY = szStartY - touch.clientY; // Inverted
                
                let newBottom = szStartBottom + deltaY;
                
                // Clamp between 10px and height-20px
                const maxH = szWrap.clientHeight - 20;
                if(newBottom < 10) newBottom = 10;
                if(newBottom > maxH) newBottom = maxH;
                
                szBarrier.style.bottom = `${newBottom}px`;
                szFill.style.height = `${newBottom}px`;
                document.getElementById('szLimitVal').innerText = `${Math.round(newBottom)}px`;
            }

            document.addEventListener('mouseup', szDragEnd);
            document.addEventListener('touchend', szDragEnd);

            function szDragEnd() {
                if(isSzDragging) {
                    isSzDragging = false;
                    if(navigator.vibrate) navigator.vibrate(10);
                }
            }

            function animateLaserSafeZone() {
                szAnimFrame = requestAnimationFrame(animateLaserSafeZone);
                if(!szCtx) return;

                // Heavy motion blur
                szCtx.fillStyle = 'rgba(0, 0, 0, 0.2)';
                szCtx.fillRect(0, 0, szCanvas.width, szCanvas.height);

                szTime += 0.05; // Sweep speed

                // We have 3 laser nodes at the top
                const w = szCanvas.width;
                const h = szCanvas.height;
                const nodes = [ w*0.2, w*0.5, w*0.8 ];
                
                // Get current Y-pixel coordinate of the safety barrier
                const safeBottomPx = parseInt(szBarrier.style.bottom) || 80;
                // Canvas 0 is top. Barrier bottom is from bottom. Convert to canvas Y.
                const safeZoneY = h - safeBottomPx;

                szCtx.globalCompositeOperation = 'screen';
                szCtx.lineWidth = 2;

                nodes.forEach((nx, i) => {
                    // Calculate sweeping angle using sine waves offset by index
                    const sweepAngle = Math.sin(szTime + i) * 0.8; // -0.8 to 0.8 radians (sweep left to right)
                    
                    // Target points way off screen bottom
                    const length = 500; 
                    const tx = nx + Math.sin(sweepAngle) * length;
                    const ty = Math.cos(sweepAngle) * length; // 0 is top, pointing down

                    // PHYSICS: Line Intersection Math
                    // Does the line from (nx,0) to (tx,ty) cross the horizontal line y = safeZoneY?
                    let endX = tx;
                    let endY = ty;
                    let hitBarrier = false;

                    if(ty > safeZoneY) {
                        // It crosses the barrier. Calculate exact X coordinate of intersection.
                        // slope m = dy/dx
                        const m = (ty - 0) / (tx - nx);
                        // x = (y - y1)/m + x1
                        if(m !== 0) {
                            endX = (safeZoneY - 0) / m + nx;
                        } else {
                            endX = nx; // Straight down
                        }
                        endY = safeZoneY;
                        hitBarrier = true;
                    }

                    // Draw Beam
                    szCtx.beginPath();
                    szCtx.moveTo(nx, 0); // Nodes are at top (y=0)
                    szCtx.lineTo(endX, endY);
                    
                    // Style
                    const hue = 'var(--cyan-neon)';
                    szCtx.strokeStyle = hue;
                    szCtx.shadowBlur = 10;
                    szCtx.shadowColor = hue;
                    szCtx.stroke();

                    // If it hit the barrier, draw a glowing "burn" point
                    if(hitBarrier) {
                        szCtx.beginPath();
                        szCtx.arc(endX, endY, 4, 0, Math.PI*2);
                        szCtx.fillStyle = '#fff';
                        szCtx.fill();
                    }
                });

                szCtx.shadowBlur = 0;
                szCtx.globalCompositeOperation = 'source-over';
            }


            // --- 2. MULTI-BAND DYNAMICS COMPRESSOR LOGIC ---
            const coCanvas = document.getElementById('compCanvas');
            let coCtx = null;
            const coWrap = document.getElementById('compWrap');
            
            let coAnimFrame = null;
            let coTime = 0;
            let compThresholdPct = 1.0; // 0.1 to 1.0

            function initCompressor() {
                if(!coWrap || !coCanvas) return;
                coCanvas.width = coWrap.clientWidth;
                coCanvas.height = coWrap.clientHeight;
                coCtx = coCanvas.getContext('2d');
                if(!coAnimFrame) animateCompressor();
            }
            window.addEventListener('resize', initCompressor);
            setTimeout(initCompressor, 500);

            function updateCompressor() {
                const val = document.getElementById('compSlider').value;
                document.getElementById('compThreshVal').innerText = `${val}%`;
                compThresholdPct = parseInt(val) / 100;
            }

            function animateCompressor() {
                coAnimFrame = requestAnimationFrame(animateCompressor);
                if(!coCtx) return;

                coCtx.clearRect(0,0, coCanvas.width, coCanvas.height);
                coTime += 0.1; // Wave speed

                const w = coCanvas.width;
                const h = coCanvas.height;
                const midY = h / 2;
                
                // Raw simulated audio wave
                let maxPeak = 0; // Track highest peak for Gain Reduction meter
                
                coCtx.beginPath();
                for(let x=0; x<w; x+=2) {
                    // Complex waveform (fundamental + harmonic + noise)
                    let rawY = Math.sin(x * 0.05 + coTime) * 40;
                    rawY += Math.cos(x * 0.1 - coTime * 1.5) * 20;
                    if(Math.random() > 0.8) rawY += (Math.random() - 0.5) * 15; // transients
                    
                    // Store raw amplitude
                    const absAmp = Math.abs(rawY);
                    
                    // Calculate pixel threshold from center based on percentage
                    // Max possible height is roughly 75px. 
                    const threshPx = 75 * compThresholdPct;
                    
                    // Compression Logic (Squash if over threshold)
                    let finalY = rawY;
                    if (absAmp > threshPx) {
                        // Exceeds threshold. Apply 4:1 Ratio reduction.
                        const excess = absAmp - threshPx;
                        const compressedExcess = excess / 4; // 4:1 ratio
                        
                        // Calculate Gain Reduction amount
                        const reduction = excess - compressedExcess;
                        if(reduction > maxPeak) maxPeak = reduction;
                        
                        // Apply back with correct sign
                        finalY = Math.sign(rawY) * (threshPx + compressedExcess);
                    }

                    if(x===0) coCtx.moveTo(x, midY + finalY);
                    else coCtx.lineTo(x, midY + finalY);
                }

                // Draw Waveform
                coCtx.lineWidth = 2;
                coCtx.strokeStyle = 'var(--cyan-neon)';
                coCtx.stroke();
                
                // Fill beneath wave
                coCtx.lineTo(w, midY);
                coCtx.lineTo(0, midY);
                coCtx.fillStyle = 'rgba(0, 229, 255, 0.1)';
                coCtx.fill();

                // Draw Threshold Lines (Top and Bottom mirrored)
                const threshPxVisual = 75 * compThresholdPct;
                coCtx.strokeStyle = 'var(--gold-primary)';
                coCtx.lineWidth = 1;
                coCtx.setLineDash([5, 5]);
                
                // Top Thresh
                coCtx.beginPath(); coCtx.moveTo(0, midY - threshPxVisual); coCtx.lineTo(w, midY - threshPxVisual); coCtx.stroke();
                // Bot Thresh
                coCtx.beginPath(); coCtx.moveTo(0, midY + threshPxVisual); coCtx.lineTo(w, midY + threshPxVisual); coCtx.stroke();
                
                coCtx.setLineDash([]);

                // Update UI Gain Reduction Meter
                // Max theoretical reduction is roughly 60px.
                let grPct = (maxPeak / 60) * 100;
                if(grPct > 100) grPct = 100;
                
                document.getElementById('grBar').style.width = `${grPct}%`;
                document.getElementById('compGrVal').innerText = `-${(grPct * 0.12).toFixed(1)} dB`;
            }


            // --- 3. GENERATOR PHASE SYNC MATRIX LOGIC ---
            const syCanvas = document.getElementById('syncCanvas');
            let syCtx = null;
            const syWrap = document.getElementById('syncWrap');
            
            let syAnimFrame = null;
            let syTime = 0;
            let genPhaseOffset = 180; // Starts completely out of phase

            function initGenSync() {
                if(!syWrap || !syCanvas) return;
                syCanvas.width = syWrap.clientWidth;
                syCanvas.height = syWrap.clientHeight;
                syCtx = syCanvas.getContext('2d');
                if(!syAnimFrame) animateGenSync();
            }
            window.addEventListener('resize', initGenSync);
            setTimeout(initGenSync, 500);

            function updateGenPhase(val) {
                genPhaseOffset = parseInt(val);
                document.getElementById('phaseDiffVal').innerText = `${genPhaseOffset}°`;
                if(navigator.vibrate) navigator.vibrate(10);
            }

            function animateGenSync() {
                syAnimFrame = requestAnimationFrame(animateGenSync);
                if(!syCtx) return;

                syCtx.clearRect(0,0, syCanvas.width, syCanvas.height);
                syTime += 0.08; // Frequency (50Hz AC simulation speed)

                const w = syCanvas.width;
                const h = syCanvas.height;
                const midY = h / 2;
                const amp = h * 0.3;
                const freq = 0.04;

                syCtx.lineWidth = 3;

                // Draw Gen A (Fixed Reference)
                syCtx.beginPath();
                syCtx.strokeStyle = 'var(--cyan-neon)';
                for(let x=0; x<w; x+=3) {
                    const y = midY + Math.sin(x * freq + syTime) * amp;
                    if(x===0) syCtx.moveTo(x,y); else syCtx.lineTo(x,y);
                }
                syCtx.stroke();

                // Draw Gen B (Variable Phase)
                const offsetRad = genPhaseOffset * (Math.PI / 180);
                syCtx.beginPath();
                syCtx.strokeStyle = 'var(--gold-primary)';
                for(let x=0; x<w; x+=3) {
                    const y = midY + Math.sin(x * freq + syTime + offsetRad) * amp;
                    if(x===0) syCtx.moveTo(x,y); else syCtx.lineTo(x,y);
                }
                syCtx.stroke();

                // Math: Calculate difference to determine Sync state
                // If phase offset is 0 or 360, they are perfectly synced.
                let diff = Math.min(genPhaseOffset, 360 - genPhaseOffset); // Shortest distance to 0
                
                const plate = document.getElementById('syncStatusPlate');
                
                if(diff < 5) {
                    plate.className = 'sh-status-indicator locked';
                    plate.innerText = "SYNC LOCKED: PARALLEL OK";
                    
                    // Fill area between them bright green to show lock
                    syCtx.globalCompositeOperation = 'lighter';
                    syCtx.beginPath();
                    for(let x=0; x<w; x+=3) {
                        const yA = midY + Math.sin(x * freq + syTime) * amp;
                        if(x===0) syCtx.moveTo(x,yA); else syCtx.lineTo(x,yA);
                    }
                    for(let x=w; x>=0; x-=3) {
                        const yB = midY + Math.sin(x * freq + syTime + offsetRad) * amp;
                        syCtx.lineTo(x,yB);
                    }
                    syCtx.fillStyle = 'rgba(0, 255, 0, 0.4)';
                    syCtx.fill();
                    syCtx.globalCompositeOperation = 'source-over';

                } else if (diff < 45) {
                    plate.className = 'sh-status-indicator';
                    plate.style.borderColor = 'var(--gold-primary)';
                    plate.style.color = 'var(--gold-primary)';
                    plate.style.background = 'rgba(212,175,55,0.1)';
                    plate.innerText = "ALIGNING PHASE...";
                } else {
                    plate.className = 'sh-status-indicator';
                    plate.style.borderColor = 'var(--red-alert)';
                    plate.style.color = 'var(--red-alert)';
                    plate.style.background = 'rgba(255,51,51,0.1)';
                    plate.innerText = "OUT OF PHASE: DO NOT COMBINE";
                }
            }
        </script>
        <style>
            .thermal-amp-wrapper {
                background: #020202;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 20px 15px;
                box-shadow: inset 0 0 30px rgba(255, 51, 51, 0.05);
            }

            .amp-rack {
                display: grid;
                grid-template-columns: repeat(4, 1fr);
                gap: 10px;
                margin-bottom: 20px;
            }

            .amp-channel {
                background: #0a0a0f;
                border: 1px solid #333;
                border-radius: 8px;
                padding: 10px 5px;
                display: flex;
                flex-direction: column;
                align-items: center;
                position: relative;
            }

            /* Thermal Bar */
            .therm-bar-bg {
                width: 20px; height: 120px; background: #000; border-radius: 10px;
                border: 1px solid #222; position: relative; overflow: hidden;
                box-shadow: inset 0 2px 10px rgba(0,0,0,0.8);
            }
            .therm-bar-fill {
                position: absolute; bottom: 0; left: 0; width: 100%; height: 20%;
                background: linear-gradient(0deg, var(--cyan-neon), #00ff00, #ffff00, var(--red-alert));
                transition: height 0.3s ease-out, filter 0.3s;
            }

            .amp-lbl { font-family: var(--font-tech); font-size: 10px; color: #888; margin-top: 10px; font-weight: bold; }
            .amp-temp { font-family: var(--font-data); font-size: 12px; color: var(--cyan-neon); font-weight: bold; margin-top: 5px; transition: color 0.3s;}

            /* Fan indicators */
            .cooling-fan {
                width: 20px; height: 20px; border-radius: 50%; border: 1px dashed #555; margin-top: 10px;
                display: flex; justify-content: center; align-items: center; color: #555; font-size: 10px;
            }
            .cooling-fan.spin { animation: fanSpin 0.2s linear infinite; color: var(--cyan-neon); border-color: var(--cyan-neon); box-shadow: 0 0 10px rgba(0,229,255,0.3); }
            @keyframes fanSpin { 100% { transform: rotate(360deg); } }

            .thermal-controls {
                background: #111; border: 1px solid #222; border-radius: 8px; padding: 15px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">THERMAL AMP MATRIX</h2>
                <div class="section-icon"><i class="fas fa-fire-alt" style="color: var(--red-alert);"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Monitor Class-D amplifier heat dissipation. Push the master drive to test thermal limits.</p>

            <div class="thermal-amp-wrapper">
                <div class="amp-rack">
                    <div class="amp-channel">
                        <div class="therm-bar-bg"><div class="therm-bar-fill" id="thermCH1"></div></div>
                        <span class="amp-temp" id="tempCH1">35°C</span>
                        <span class="amp-lbl">CH 1: SUB L</span>
                        <div class="cooling-fan" id="fanCH1"><i class="fas fa-fan"></i></div>
                    </div>
                    <div class="amp-channel">
                        <div class="therm-bar-bg"><div class="therm-bar-fill" id="thermCH2"></div></div>
                        <span class="amp-temp" id="tempCH2">36°C</span>
                        <span class="amp-lbl">CH 2: SUB R</span>
                        <div class="cooling-fan" id="fanCH2"><i class="fas fa-fan"></i></div>
                    </div>
                    <div class="amp-channel">
                        <div class="therm-bar-bg"><div class="therm-bar-fill" id="thermCH3"></div></div>
                        <span class="amp-temp" id="tempCH3">30°C</span>
                        <span class="amp-lbl">CH 3: MID</span>
                        <div class="cooling-fan" id="fanCH3"><i class="fas fa-fan"></i></div>
                    </div>
                    <div class="amp-channel">
                        <div class="therm-bar-bg"><div class="therm-bar-fill" id="thermCH4"></div></div>
                        <span class="amp-temp" id="tempCH4">28°C</span>
                        <span class="amp-lbl">CH 4: HIGH</span>
                        <div class="cooling-fan" id="fanCH4"><i class="fas fa-fan"></i></div>
                    </div>
                </div>

                <div class="thermal-controls">
                    <div style="display:flex; justify-content:space-between; margin-bottom:10px;">
                        <span style="font-family:var(--font-tech); font-size:10px; color:#fff;">MASTER SYSTEM DRIVE</span>
                        <span id="sysDriveVal" style="font-family:var(--font-data); font-size:12px; color:var(--cyan-neon); font-weight:bold;">20%</span>
                    </div>
                    <input type="range" class="app-slider" id="masterDriveSlider" min="0" max="100" value="20" oninput="updateThermalDrive(this.value)">
                </div>
            </div>
        </div>

        <style>
            .gobo-wrapper {
                background: #000;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .gobo-canvas-container {
                width: 100%;
                height: 250px;
                background: radial-gradient(circle at center, #111 0%, #000 100%);
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 50px rgba(0,229,255,0.1);
            }
            #goboCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .gobo-selector {
                display: flex; gap: 10px; margin: 15px 0;
            }
            .gobo-btn {
                flex: 1; background: #0a0a0f; border: 1px solid #333; border-radius: 6px; padding: 10px 0;
                text-align: center; cursor: pointer; transition: 0.2s;
            }
            .gobo-btn.active { border-color: var(--gold-primary); box-shadow: 0 0 10px rgba(212,175,55,0.3); background: rgba(212,175,55,0.1); }
            .gobo-btn i { font-size: 18px; color: var(--gold-primary); }

            .lens-focus-ctrl {
                background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #222;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DMX GOBO ENGINE</h2>
                <div class="section-icon"><i class="fas fa-sun"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate physical light stencils (Gobos). Adjust the mechanical lens focus for sharp imagery or atmospheric blur.</p>

            <div class="gobo-wrapper">
                <div class="gobo-canvas-container" id="goboWrap">
                    <canvas id="goboCanvas"></canvas>
                    <div style="position:absolute; bottom:10px; right:10px; font-family:var(--font-tech); font-size:9px; color:var(--cyan-neon); opacity:0.6;">DMX OPTICAL OUTPUT</div>
                </div>

                <div class="gobo-selector">
                    <div class="gobo-btn active" onclick="setGoboPattern('starburst', this)"><i class="fas fa-certificate"></i></div>
                    <div class="gobo-btn" onclick="setGoboPattern('dots', this)"><i class="fas fa-braille"></i></div>
                    <div class="gobo-btn" onclick="setGoboPattern('bio', this)"><i class="fas fa-radiation"></i></div>
                </div>

                <div class="lens-focus-ctrl">
                    <div style="display:flex; justify-content:space-between; margin-bottom:5px;">
                        <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">LENS FOCUS (BLUR)</span>
                        <span id="focusValDisplay" style="font-family:var(--font-tech); font-size:10px; color:#fff;">SHARP</span>
                    </div>
                    <input type="range" class="app-slider" id="goboFocus" min="0" max="20" value="0" step="1" oninput="updateGoboFocus(this.value)">
                </div>
            </div>
        </div>

        <style>
            .delay-tower-wrapper {
                background: #050508;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 10px 20px rgba(0,0,0,0.8);
            }

            .time-align-display {
                width: 100%;
                height: 120px;
                background: #000;
                border: 1px solid #112233;
                border-radius: 8px;
                position: relative;
                margin-bottom: 20px;
                overflow: hidden;
            }
            
            /* Physical Distance Track */
            .align-track {
                position: absolute; top: 50%; left: 10%; right: 10%; height: 2px;
                background: #333; transform: translateY(-50%);
            }
            
            .align-node {
                position: absolute; top: 50%; transform: translate(-50%, -50%);
                display: flex; flex-direction: column; align-items: center;
            }
            .align-node i { font-size: 20px; }
            .align-node span { font-family: var(--font-data); font-size: 9px; color: #888; position: absolute; top: 25px; white-space: nowrap; }

            .node-main { left: 10%; color: var(--cyan-neon); }
            .node-delay { left: 90%; color: var(--gold-primary); transition: left 0.2s; }

            /* Moving sound wave visual */
            .sound-pulse {
                position: absolute; top: 50%; left: 10%; transform: translate(-50%, -50%);
                width: 10px; height: 30px; background: rgba(255,255,255,0.5); border-radius: 5px;
                box-shadow: 0 0 10px #fff; opacity: 0;
            }
            @keyframes shootPulse { 0% { left: 10%; opacity: 1; } 100% { left: 90%; opacity: 0; } }

            .delay-calc-box {
                background: rgba(0,229,255,0.05); border: 1px solid var(--cyan-neon);
                border-radius: 8px; padding: 15px; text-align: center;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DELAY TOWER ALIGNMENT</h2>
                <div class="section-icon"><i class="fas fa-stopwatch"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Sound travels at 343 m/s. Calculate the exact digital delay required so rear FOH speakers hit the crowd at the exact same millisecond as the main stage.</p>

            <div class="delay-tower-wrapper">
                <div class="time-align-display" id="alignDisplayBox">
                    <div class="align-track"></div>
                    <div class="align-node node-main">
                        <i class="fas fa-speaker"></i>
                        <span>MAIN L/R</span>
                    </div>
                    <div class="align-node node-delay" id="delaySpeakerNode">
                        <i class="fas fa-speaker"></i>
                        <span>DELAY FOH</span>
                    </div>
                    <div class="sound-pulse" id="demoPulse"></div>
                </div>

                <div style="margin-bottom: 20px;">
                    <div style="display:flex; justify-content:space-between; margin-bottom:5px;">
                        <span style="font-family:var(--font-tech); font-size:10px; color:#aaa;">DISTANCE TO FOH TOWER</span>
                        <span id="towerDistDisplay" style="font-family:var(--font-tech); font-size:12px; color:#fff; font-weight:bold;">50 Meters</span>
                    </div>
                    <input type="range" class="app-slider" id="towerDistSlider" min="10" max="150" value="50" oninput="calculateDelayTime()">
                </div>

                <div class="delay-calc-box">
                    <span style="font-family:var(--font-data); font-size:10px; color:var(--cyan-neon); letter-spacing:2px; display:block;">REQUIRED DSP DELAY TIME</span>
                    <div id="msDelayResult" style="font-family:var(--font-tech); font-size:36px; color:#fff; font-weight:900; margin:5px 0; text-shadow:0 0 15px rgba(0,229,255,0.4);">145.8 ms</div>
                    <button class="app-btn-outline" style="width:100%; margin-top:10px;" onclick="triggerAlignmentPulse()">
                        <i class="fas fa-wifi"></i> TEST ACOUSTIC PULSE
                    </button>
                </div>
            </div>
        </div>

        <script>
            // --- 1. AMPLIFIER THERMAL OVERDRIVE LOGIC ---
            let sysDrive = 20; // 0 to 100
            let ampTemps = [35, 36, 30, 28]; // Base temps for CH 1-4
            let thermalInterval = null;

            function updateThermalDrive(val) {
                sysDrive = parseInt(val);
                
                const disp = document.getElementById('sysDriveVal');
                disp.innerText = `${sysDrive}%`;
                
                // Color code the text based on danger level
                if(sysDrive > 85) disp.style.color = "var(--red-alert)";
                else if(sysDrive > 60) disp.style.color = "var(--gold-primary)";
                else disp.style.color = "var(--cyan-neon)";

                // Haptic feedback for pushing too hard
                if(sysDrive > 85 && navigator.vibrate) navigator.vibrate(10);
            }

            function simulateThermals() {
                // Subs (CH 1 & 2) heat up faster than Mid/Highs
                const heatRates = [0.08, 0.08, 0.04, 0.03]; 
                
                for(let i=0; i<4; i++) {
                    let targetTemp = 30 + (sysDrive * heatRates[i] * 10);
                    
                    // Move current temp slowly towards target temp (thermal inertia)
                    ampTemps[i] += (targetTemp - ampTemps[i]) * 0.1;
                    
                    // Add slight random fluctuation
                    ampTemps[i] += (Math.random() - 0.5) * 0.5;

                    // Update UI
                    const barFill = document.getElementById(`thermCH${i+1}`);
                    const tempText = document.getElementById(`tempCH${i+1}`);
                    const fan = document.getElementById(`fanCH${i+1}`);

                    // Max simulated temp is ~100C.
                    let heightPct = (ampTemps[i] / 100) * 100;
                    if(heightPct > 100) heightPct = 100;
                    if(heightPct < 5) heightPct = 5;

                    barFill.style.height = `${heightPct}%`;
                    tempText.innerText = `${Math.round(ampTemps[i])}°C`;

                    // Smart Cooling Fan Logic & Color Changes
                    if(ampTemps[i] > 75) {
                        // Critical
                        barFill.style.background = "var(--red-alert)";
                        tempText.style.color = "var(--red-alert)";
                        fan.classList.add('spin');
                        fan.style.color = "var(--red-alert)";
                        fan.style.borderColor = "var(--red-alert)";
                        
                        // Fake Thermal Throttling: If it hits 95C, auto-pull the fader down
                        if(ampTemps[i] > 95 && sysDrive > 50) {
                            if(typeof triggerToast === 'function') triggerToast(`CH ${i+1} THERMAL PROTECT ENGAGED`);
                            document.getElementById('masterDriveSlider').value = 40;
                            updateThermalDrive(40);
                            if(navigator.vibrate) navigator.vibrate([100, 50, 200]);
                        }
                    } else if(ampTemps[i] > 55) {
                        // Warning
                        barFill.style.background = "var(--gold-primary)";
                        tempText.style.color = "var(--gold-primary)";
                        fan.classList.add('spin');
                        fan.style.color = "var(--gold-primary)";
                        fan.style.borderColor = "var(--gold-primary)";
                    } else {
                        // Normal
                        barFill.style.background = "var(--cyan-neon)";
                        tempText.style.color = "var(--cyan-neon)";
                        // Fans turn off if cool enough
                        if(ampTemps[i] < 40) {
                            fan.classList.remove('spin');
                            fan.style.color = "#555";
                            fan.style.borderColor = "#555";
                        }
                    }
                }
            }
            
            // Run thermal simulation loop
            thermalInterval = setInterval(simulateThermals, 200);


            // --- 2. DMX GOBO PROJECTION ENGINE LOGIC ---
            const gbCanvas = document.getElementById('goboCanvas');
            let gbCtx = null;
            const gbWrap = document.getElementById('goboWrap');
            
            let goboAnimFrame = null;
            let currentGoboPattern = 'starburst';
            let goboRotation = 0;
            let goboBlurLevel = 0;

            function initGoboEngine() {
                if(!gbWrap || !gbCanvas) return;
                gbCanvas.width = gbWrap.clientWidth;
                gbCanvas.height = gbWrap.clientHeight;
                gbCtx = gbCanvas.getContext('2d');
                if(!goboAnimFrame) animateGobo();
            }
            window.addEventListener('resize', initGoboEngine);
            setTimeout(initGoboEngine, 800);

            function setGoboPattern(type, btnEl) {
                if(typeof playTap === 'function') playTap();
                document.querySelectorAll('.gobo-btn').forEach(b => b.classList.remove('active'));
                btnEl.classList.add('active');
                currentGoboPattern = type;
            }

            function updateGoboFocus(val) {
                goboBlurLevel = parseInt(val);
                const disp = document.getElementById('focusValDisplay');
                if(goboBlurLevel === 0) disp.innerText = "SHARP";
                else if(goboBlurLevel < 10) disp.innerText = "SOFT";
                else disp.innerText = "DEFOCUSED (WASH)";
            }

            function drawStar(ctx, cx, cy, spikes, outerRadius, innerRadius) {
                let rot = Math.PI / 2 * 3;
                let x = cx;
                let y = cy;
                let step = Math.PI / spikes;

                ctx.beginPath();
                ctx.moveTo(cx, cy - outerRadius);
                for (let i = 0; i < spikes; i++) {
                    x = cx + Math.cos(rot) * outerRadius;
                    y = cy + Math.sin(rot) * outerRadius;
                    ctx.lineTo(x, y);
                    rot += step;

                    x = cx + Math.cos(rot) * innerRadius;
                    y = cy + Math.sin(rot) * innerRadius;
                    ctx.lineTo(x, y);
                    rot += step;
                }
                ctx.lineTo(cx, cy - outerRadius);
                ctx.closePath();
                ctx.fill();
            }

            function animateGobo() {
                goboAnimFrame = requestAnimationFrame(animateGobo);
                if(!gbCtx) return;

                // Clear
                gbCtx.fillStyle = '#000';
                gbCtx.fillRect(0, 0, gbCanvas.width, gbCanvas.height);

                goboRotation += 0.01; // Constant rotation

                const cx = gbCanvas.width / 2;
                const cy = gbCanvas.height / 2;

                gbCtx.save();
                gbCtx.translate(cx, cy);
                gbCtx.rotate(goboRotation);

                // Apply dynamic focal blur using Shadow Blur (Better performance than CSS filter)
                gbCtx.shadowBlur = goboBlurLevel * 3;
                
                // Get current neon color from CSS variables
                const rootStyle = getComputedStyle(document.documentElement);
                const neonColor = rootStyle.getPropertyValue('--cyan-neon').trim() || '#00e5ff';
                
                gbCtx.shadowColor = neonColor;
                gbCtx.fillStyle = neonColor;

                // Draw chosen pattern
                if (currentGoboPattern === 'starburst') {
                    // Multi-pointed star
                    drawStar(gbCtx, 0, 0, 12, 80, 20);
                } 
                else if (currentGoboPattern === 'dots') {
                    // Ring of dots
                    for(let i=0; i<12; i++) {
                        const angle = (Math.PI * 2 / 12) * i;
                        const px = Math.cos(angle) * 60;
                        const py = Math.sin(angle) * 60;
                        gbCtx.beginPath();
                        gbCtx.arc(px, py, 10, 0, Math.PI*2);
                        gbCtx.fill();
                    }
                    // Center dot
                    gbCtx.beginPath(); gbCtx.arc(0,0, 15, 0, Math.PI*2); gbCtx.fill();
                }
                else if (currentGoboPattern === 'bio') {
                    // 3 large wedges
                    for(let i=0; i<3; i++) {
                        const angle = (Math.PI * 2 / 3) * i;
                        gbCtx.beginPath();
                        gbCtx.moveTo(0,0);
                        gbCtx.arc(0,0, 80, angle, angle + Math.PI/2);
                        gbCtx.closePath();
                        gbCtx.fill();
                    }
                    // Cut out center
                    gbCtx.globalCompositeOperation = 'destination-out';
                    gbCtx.beginPath(); gbCtx.arc(0,0, 20, 0, Math.PI*2); gbCtx.fill();
                    gbCtx.globalCompositeOperation = 'source-over';
                }

                gbCtx.restore();
            }


            // --- 3. DELAY TOWER TIME-ALIGNMENT LOGIC ---
            const SPEED_OF_SOUND_MS = 343; // meters per second
            
            function calculateDelayTime() {
                const distMeters = parseInt(document.getElementById('towerDistSlider').value);
                document.getElementById('towerDistDisplay').innerText = `${distMeters} Meters`;
                
                // Formula: Time = Distance / Speed
                // Since speed is m/s, result is seconds. Multiply by 1000 for milliseconds.
                const delayMs = (distMeters / SPEED_OF_SOUND_MS) * 1000;
                
                document.getElementById('msDelayResult').innerText = `${delayMs.toFixed(1)} ms`;

                // Update visual node position on the track
                // Track visual bounds: 10% to 90% (80% total width)
                // Slider bounds: 10 to 150m.
                const pct = (distMeters - 10) / (150 - 10);
                const leftPos = 10 + (pct * 80);
                document.getElementById('delaySpeakerNode').style.left = `${leftPos}%`;
            }

            function triggerAlignmentPulse() {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                
                const pulse = document.getElementById('demoPulse');
                
                // Restart animation
                pulse.style.animation = 'none';
                void pulse.offsetWidth; // Force reflow
                
                // Read current distance for animation timing
                const distMeters = parseInt(document.getElementById('towerDistSlider').value);
                // Make animation duration loosely representative of distance (0.5s to 1.5s)
                const animDuration = 0.5 + (distMeters / 150); 
                
                pulse.style.animation = `shootPulse ${animDuration}s cubic-bezier(0.25, 1, 0.5, 1) forwards`;

                // Audio feedback if engine running (Part 3)
                if(typeof playSynth === 'function' && typeof isEngineOn !== 'undefined' && isEngineOn) {
                    playSynth('hihatC', null); // Front speaker shoots
                    
                    const delayMs = (distMeters / SPEED_OF_SOUND_MS) * 1000;
                    
                    // Simulate the delayed speaker firing perfectly in sync when wave arrives
                    setTimeout(() => {
                        playSynth('hihatO', null);
                        if(navigator.vibrate) navigator.vibrate([30, 30, 30]); // Secondary success haptic
                        
                        // Flash the delay node to show activation
                        const delayNode = document.getElementById('delaySpeakerNode');
                        delayNode.style.color = '#fff';
                        delayNode.style.textShadow = '0 0 15px #fff';
                        setTimeout(() => {
                            delayNode.style.color = 'var(--gold-primary)';
                            delayNode.style.textShadow = 'none';
                        }, 200);

                    }, delayMs);
                }
            }
            
            // Init
            calculateDelayTime();
        </script>
        <style>
            .rf-wrapper {
                background: #020202;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .rf-canvas-box {
                width: 100%;
                height: 160px;
                background: #000;
                border: 1px solid #004400;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 30px rgba(0, 255, 0, 0.1);
            }
            #rfCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2; }
            
            /* Radar Sweep Line */
            .rf-sweep {
                position: absolute; top: 0; bottom: 0; width: 2px;
                background: #00ff00; box-shadow: 0 0 15px #00ff00;
                z-index: 3; pointer-events: none; left: -10px;
            }
            .rf-sweep::after {
                content: ''; position: absolute; top: 0; bottom: 0; right: 0; width: 50px;
                background: linear-gradient(90deg, transparent, rgba(0, 255, 0, 0.3));
            }

            .rf-hud {
                display: flex; justify-content: space-between; align-items: center; margin-top: 15px;
                background: #0a0a0f; padding: 12px; border-radius: 6px; border: 1px solid #1a1a24;
            }
            .rf-stat { display: flex; flex-direction: column; }
            .rf-lbl { font-family: var(--font-data); font-size: 9px; color: #888; }
            .rf-val { font-family: var(--font-tech); font-size: 16px; font-weight: bold; color: var(--cyan-neon); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">RF SPECTRUM ANALYZER</h2>
                <div class="section-icon"><i class="fas fa-broadcast-tower"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Scan the UHF frequency band to find clean channels for wireless microphones, avoiding local interference.</p>

            <div class="rf-wrapper">
                <div class="rf-canvas-box" id="rfWrap">
                    <canvas id="rfCanvas"></canvas>
                    <div class="rf-sweep" id="rfSweepLine"></div>
                    <div style="position:absolute; top:5px; left:5px; color:#00ff00; font-family:var(--font-tech); font-size:8px; z-index:5;">UHF BAND: 470 - 608 MHz</div>
                </div>

                <div class="rf-hud">
                    <div class="rf-stat">
                        <span class="rf-lbl">ACTIVE CH FREQUENCY</span>
                        <span class="rf-val" id="rfFreqVal">512.400 MHz</span>
                    </div>
                    <button class="app-btn-outline" style="width: auto; padding: 10px 20px; font-size: 10px;" onclick="triggerAutoScan()" id="btnRfScan">
                        <i class="fas fa-search"></i> AUTO-SCAN
                    </button>
                </div>
            </div>
        </div>

        <style>
            .spark-wrapper {
                background: #050508;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .spark-canvas-box {
                width: 100%;
                height: 280px;
                background: radial-gradient(circle at bottom center, #1a1a1a 0%, #000 100%);
                border: 2px solid #333;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #sparkCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Virtual Machines */
            .spark-machine {
                position: absolute; bottom: 0; width: 24px; height: 16px;
                background: #111; border: 1px solid #555; border-radius: 2px 2px 0 0;
                transform: translateX(-50%); z-index: 5; display: flex; justify-content: center;
            }
            .spark-machine::after { content:''; width:8px; height:2px; background:#000; position:absolute; top:2px; }
            .sm-1 { left: 20%; } .sm-2 { left: 50%; } .sm-3 { left: 80%; }

            .spark-controls {
                display: flex; flex-direction: column; gap: 15px; margin-top: 15px;
            }
            .spark-slider-row {
                display: flex; justify-content: space-between; align-items: center; gap: 15px;
                background: #0a0a0f; padding: 12px; border-radius: 6px; border: 1px solid #1a1a24;
            }
            
            .btn-fire-sparks {
                width: 100%; padding: 15px; border-radius: 8px; font-family: var(--font-tech); font-weight: 900; font-size: 16px;
                background: linear-gradient(180deg, var(--gold-glow), #b38000); color: #000; border: none;
                box-shadow: 0 10px 20px rgba(255,223,0,0.3), inset 0 2px 5px rgba(255,255,255,0.6); cursor: pointer;
                user-select: none; touch-action: manipulation; transition: 0.1s; letter-spacing: 2px;
            }
            .btn-fire-sparks:active { transform: scale(0.96); box-shadow: 0 2px 5px rgba(255,223,0,0.3), inset 0 5px 10px rgba(0,0,0,0.5); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">PYROTECHNIC AI</h2>
                <div class="section-icon"><i class="fas fa-fire"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Control the kinetic height of the cold spark fountains. Hold button to initiate continuous burn.</p>

            <div class="spark-wrapper">
                <div class="spark-canvas-box" id="sparkWrap">
                    <canvas id="sparkCanvas"></canvas>
                    <div class="spark-machine sm-1"></div>
                    <div class="spark-machine sm-2"></div>
                    <div class="spark-machine sm-3"></div>
                </div>

                <div class="spark-controls">
                    <div class="spark-slider-row">
                        <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">BURST HEIGHT</span>
                        <input type="range" class="app-slider" id="sparkHeightSlider" min="2" max="6" step="0.5" value="4" style="flex:1;">
                        <span id="sparkHeightVal" style="font-family:var(--font-tech); font-size:14px; color:var(--gold-primary); font-weight:bold; width: 40px; text-align:right;">4.0m</span>
                    </div>

                    <button class="btn-fire-sparks" onmousedown="fireSparks(true)" onmouseup="fireSparks(false)" onmouseleave="fireSparks(false)" ontouchstart="fireSparks(true)" ontouchend="fireSparks(false)">
                        IGNITE SPARKS
                    </button>
                </div>
            </div>
        </div>

        <style>
            .sub-synth-wrapper {
                background: #000;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .sub-synth-display {
                width: 100%;
                height: 140px;
                background: #050505;
                border-radius: 8px;
                border: 1px solid #111;
                position: relative;
                overflow: hidden;
                margin-bottom: 15px;
            }
            #subSynthCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2; mix-blend-mode: screen; }
            
            .sub-synth-hud {
                display: flex; justify-content: space-between; background: #0a0a0f; padding: 12px; border-radius: 8px; border: 1px solid #1a1a24;
            }

            /* Massive Drive Knob Simulator */
            .sub-drive-container {
                display: flex; flex-direction: column; align-items: center; margin-top: 20px;
            }
            .sub-drive-track {
                width: 100%; height: 12px; background: #111; border-radius: 6px; position: relative; border: 1px solid #333; overflow: hidden;
            }
            .sub-drive-fill {
                position: absolute; top: 0; left: 0; bottom: 0; width: 0%;
                background: linear-gradient(90deg, #111, var(--red-alert)); transition: width 0.1s;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">SUB-HARMONIC SYNTH</h2>
                <div class="section-icon"><i class="fas fa-drum"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Generate artificial sub-octaves below the fundamental frequency to add massive weight to older tracks.</p>

            <div class="sub-synth-wrapper">
                <div class="sub-synth-display" id="subSynthWrap">
                    <canvas id="subSynthCanvas"></canvas>
                    <div style="position:absolute; top:5px; left:5px; color:#fff; font-family:var(--font-data); font-size:9px; z-index:5;">ORIGINAL AUDIO SIGNAL (GREY)</div>
                    <div style="position:absolute; bottom:5px; left:5px; color:var(--red-alert); font-family:var(--font-data); font-size:9px; z-index:5;">GENERATED SUB-OCTAVE (RED)</div>
                </div>

                <div class="sub-synth-hud">
                    <div style="display:flex; flex-direction:column;">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888;">FUNDAMENTAL</span>
                        <span style="font-family:var(--font-tech); font-size:14px; color:#ccc;">80 Hz</span>
                    </div>
                    <div style="display:flex; flex-direction:column; text-align:right;">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888;">SYNTHESIZED</span>
                        <span style="font-family:var(--font-tech); font-size:14px; color:var(--red-alert);">40 Hz</span>
                    </div>
                </div>

                <div class="sub-drive-container">
                    <span style="font-family:var(--font-tech); font-size:12px; color:var(--red-alert); letter-spacing:2px; margin-bottom:10px;">SUB-HARMONIC DRIVE</span>
                    <input type="range" class="app-slider" id="subDriveSlider" min="0" max="100" value="0" oninput="updateSubSynth()">
                    <div class="sub-drive-track" style="margin-top:10px;"><div class="sub-drive-fill" id="subDriveBar"></div></div>
                </div>
            </div>
        </div>

        <script>
            // --- 1. RF SPECTRUM ANALYZER LOGIC ---
            const rfCanvas = document.getElementById('rfCanvas');
            let rfCtx = null;
            const rfWrap = document.getElementById('rfWrap');
            const rfSweep = document.getElementById('rfSweepLine');
            
            let rfAnimFrame = null;
            let rfInterferenceData = [];
            let isScanning = false;

            function initRFSpectrum() {
                if(!rfWrap || !rfCanvas) return;
                rfCanvas.width = rfWrap.clientWidth;
                rfCanvas.height = rfWrap.clientHeight;
                rfCtx = rfCanvas.getContext('2d');
                
                // Generate fake RF interference landscape
                generateRFData();
                if(!rfAnimFrame) animateRFSpectrum();
            }
            window.addEventListener('resize', initRFSpectrum);
            setTimeout(initRFSpectrum, 500);

            function generateRFData() {
                rfInterferenceData = [];
                const points = 100;
                for(let i=0; i<points; i++) {
                    // Create massive interference spikes in the middle
                    let noise = Math.random() * 20;
                    if(i > 30 && i < 50) noise += Math.random() * 80; // TV Station
                    if(i > 70 && i < 80) noise += Math.random() * 60; // Cell towers
                    rfInterferenceData.push(noise);
                }
            }

            function triggerAutoScan() {
                if(isScanning) return;
                if(typeof playTap === 'function') playTap();
                isScanning = true;
                
                const btn = document.getElementById('btnRfScan');
                btn.innerHTML = '<i class="fas fa-sync fa-spin"></i> SCANNING...';
                btn.style.color = "var(--gold-primary)";
                btn.style.borderColor = "var(--gold-primary)";
                
                if(navigator.vibrate) navigator.vibrate(50);

                // CSS Animation for the sweep line
                rfSweep.style.transition = 'left 1.5s cubic-bezier(0.25, 1, 0.5, 1)';
                rfSweep.style.left = '100%';

                setTimeout(() => {
                    // Pick a clean frequency (where noise is low, e.g., index 15)
                    const safeFreq = (470 + (15 / 100) * (608 - 470)).toFixed(3);
                    document.getElementById('rfFreqVal').innerText = `${safeFreq} MHz`;
                    document.getElementById('rfFreqVal').style.color = "#00ff00";

                    // Move sweep line to the safe zone
                    rfSweep.style.transition = 'left 0.5s ease-out';
                    rfSweep.style.left = '15%';

                    btn.innerHTML = '<i class="fas fa-check"></i> FREQ LOCKED';
                    btn.style.color = "#00ff00";
                    btn.style.borderColor = "#00ff00";
                    
                    if(navigator.vibrate) navigator.vibrate([30, 30, 30]);
                    
                    setTimeout(() => {
                        isScanning = false;
                        btn.innerHTML = '<i class="fas fa-search"></i> AUTO-SCAN';
                        btn.style.color = "var(--cyan-neon)";
                        btn.style.borderColor = "var(--cyan-neon)";
                    }, 2000);

                }, 1500);
            }

            function animateRFSpectrum() {
                rfAnimFrame = requestAnimationFrame(animateRFSpectrum);
                if(!rfCtx) return;

                rfCtx.fillStyle = '#000';
                rfCtx.fillRect(0, 0, rfCanvas.width, rfCanvas.height);

                const w = rfCanvas.width;
                const h = rfCanvas.height;
                const step = w / rfInterferenceData.length;

                // Draw Background Noise Floor (Greenish)
                rfCtx.beginPath();
                rfCtx.moveTo(0, h);
                
                for(let i=0; i<rfInterferenceData.length; i++) {
                    // Add slight live jitter to data
                    let jitter = rfInterferenceData[i] + (Math.random() * 5 - 2.5);
                    if(jitter < 0) jitter = 0;
                    
                    const x = i * step;
                    const y = h - jitter;
                    rfCtx.lineTo(x, y);
                }
                
                rfCtx.lineTo(w, h);
                rfCtx.closePath();
                
                // Color gradient
                const grad = rfCtx.createLinearGradient(0, h, 0, 0);
                grad.addColorStop(0, 'rgba(0, 255, 0, 0.3)');
                grad.addColorStop(0.5, 'rgba(255, 255, 0, 0.5)');
                grad.addColorStop(1, 'rgba(255, 0, 0, 0.8)');
                
                rfCtx.fillStyle = grad;
                rfCtx.fill();
                
                // Outline
                rfCtx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
                rfCtx.lineWidth = 1;
                rfCtx.stroke();
            }


            // --- 2. SPARKULAR (COLD SPARK) DIRECTOR LOGIC ---
            const spkCanvas = document.getElementById('sparkCanvas');
            let spkCtx = null;
            const spkWrap = document.getElementById('sparkWrap');
            
            let isSparking = false;
            let sparkParticles = [];
            let spkAnimFrame = null;
            let currentSparkHeight = 4.0; // Slider value

            function initSparkEngine() {
                if(!spkWrap || !spkCanvas) return;
                spkCanvas.width = spkWrap.clientWidth;
                spkCanvas.height = spkWrap.clientHeight;
                spkCtx = spkCanvas.getContext('2d');
            }
            window.addEventListener('resize', initSparkEngine);
            setTimeout(initSparkEngine, 800);

            // Hook up slider
            document.getElementById('sparkHeightSlider').addEventListener('input', function() {
                currentSparkHeight = parseFloat(this.value);
                document.getElementById('sparkHeightVal').innerText = `${currentSparkHeight.toFixed(1)}m`;
            });

            function fireSparks(state) {
                if(state && !isSparking) {
                    if(typeof playTap === 'function') playTap();
                    if(navigator.vibrate) navigator.vibrate([50, 50, 50, 50]);
                }
                isSparking = state;
                if(state && !spkAnimFrame) animateSparks();
            }

            class SparkParticle {
                constructor(x, y, maxH) {
                    this.x = x + (Math.random() * 8 - 4); // Spread at nozzle
                    this.y = y;
                    
                    // Velocity based on target height (physics approximation)
                    // Higher height = stronger negative Y velocity
                    const force = 8 + (maxH * 2); 
                    this.vy = -(Math.random() * (force * 0.3) + (force * 0.7));
                    this.vx = (Math.random() - 0.5) * (maxH * 0.5); // Spread increases with height
                    
                    this.life = 1.0;
                    this.decay = Math.random() * 0.02 + 0.01; // Burnout speed
                    
                    // Color shifts from bright white -> yellow -> orange -> dark red
                    this.colors = [
                        'rgba(255, 255, 255, 1)',
                        'rgba(255, 223, 0, 1)',
                        'rgba(255, 100, 0, 0.8)',
                        'rgba(255, 0, 0, 0.5)'
                    ];
                }
                update() {
                    this.x += this.vx;
                    this.y += this.vy;
                    
                    // Gravity pulls it down
                    this.vy += 0.4; 
                    
                    this.life -= this.decay;
                }
                draw(ctx) {
                    if(this.life <= 0) return;
                    
                    // Determine color based on life
                    let colorIndex = 0;
                    if(this.life < 0.3) colorIndex = 3;
                    else if(this.life < 0.6) colorIndex = 2;
                    else if(this.life < 0.9) colorIndex = 1;
                    
                    ctx.fillStyle = this.colors[colorIndex];
                    
                    // Draw a tiny bright streak (line) based on velocity to simulate motion blur
                    ctx.beginPath();
                    ctx.moveTo(this.x, this.y);
                    ctx.lineTo(this.x - (this.vx * 1.5), this.y - (this.vy * 1.5));
                    ctx.strokeStyle = this.colors[colorIndex];
                    ctx.lineWidth = 2;
                    ctx.stroke();
                }
            }

            function animateSparks() {
                if(!isSparking && sparkParticles.length === 0) {
                    spkAnimFrame = null;
                    spkCtx.clearRect(0,0, spkCanvas.width, spkCanvas.height);
                    return;
                }
                spkAnimFrame = requestAnimationFrame(animateSparks);

                // Heavy motion blur trailing
                spkCtx.fillStyle = 'rgba(0, 0, 0, 0.3)';
                spkCtx.fillRect(0, 0, spkCanvas.width, spkCanvas.height);

                spkCtx.globalCompositeOperation = 'screen';

                // Spawn new particles from the 3 machines
                if(isSparking) {
                    const w = spkCanvas.width;
                    const h = spkCanvas.height;
                    const machines = [w*0.2, w*0.5, w*0.8];
                    
                    machines.forEach(mx => {
                        // 10 particles per machine per frame = massive density
                        for(let i=0; i<10; i++) {
                            sparkParticles.push(new SparkParticle(mx, h, currentSparkHeight));
                        }
                    });
                }

                // Update & Draw
                for(let i = sparkParticles.length - 1; i >= 0; i--) {
                    let p = sparkParticles[i];
                    p.update();
                    p.draw(spkCtx);
                    if(p.life <= 0) sparkParticles.splice(i, 1);
                }
                
                spkCtx.globalCompositeOperation = 'source-over';
            }


            // --- 3. SUB-HARMONIC BASS SYNTHESIZER LOGIC ---
            const subCanvas = document.getElementById('subSynthCanvas');
            let subCtx = null;
            const subWrap = document.getElementById('subSynthWrap');
            
            let subAnimFrame = null;
            let subTime = 0;
            let subDrivePct = 0;

            function initSubSynth() {
                if(!subWrap || !subCanvas) return;
                subCanvas.width = subWrap.clientWidth;
                subCanvas.height = subWrap.clientHeight;
                subCtx = subCanvas.getContext('2d');
                if(!subAnimFrame) animateSubSynth();
            }
            window.addEventListener('resize', initSubSynth);
            setTimeout(initSubSynth, 1000);

            function updateSubSynth() {
                const val = document.getElementById('subDriveSlider').value;
                subDrivePct = parseInt(val) / 100;
                document.getElementById('subDriveBar').style.width = `${val}%`;
                
                if(val > 0 && navigator.vibrate) {
                    // Vibrate intensity based on slider
                    const vTime = Math.floor(val / 2);
                    navigator.vibrate(vTime);
                }
            }

            function animateSubSynth() {
                subAnimFrame = requestAnimationFrame(animateSubSynth);
                if(!subCtx) return;

                subCtx.fillStyle = '#050505';
                subCtx.fillRect(0, 0, subCanvas.width, subCanvas.height);
                
                subTime += 0.05;
                
                const w = subCanvas.width;
                const h = subCanvas.height;
                const midY = h / 2;

                subCtx.globalCompositeOperation = 'screen';

                // 1. Draw Fundamental (Original Track) - 80Hz simulation
                subCtx.beginPath();
                subCtx.strokeStyle = 'rgba(255, 255, 255, 0.3)'; // Grey
                subCtx.lineWidth = 2;
                for(let x=0; x<w; x+=3) {
                    // Fast wave
                    const y = Math.sin(x * 0.1 + subTime * 2) * 30;
                    if(x===0) subCtx.moveTo(x, midY + y); else subCtx.lineTo(x, midY + y);
                }
                subCtx.stroke();

                // 2. Draw Sub-Harmonic (Generated) - 40Hz simulation
                // Amplitude and opacity driven by the slider
                if(subDrivePct > 0) {
                    subCtx.beginPath();
                    // Color shifts to deep red as drive increases
                    subCtx.strokeStyle = `rgba(255, 51, 51, ${subDrivePct})`; 
                    subCtx.lineWidth = 3 + (subDrivePct * 3);
                    subCtx.shadowBlur = subDrivePct * 20;
                    subCtx.shadowColor = 'var(--red-alert)';

                    for(let x=0; x<w; x+=3) {
                        // Half the frequency (0.05 vs 0.1), double the visual amplitude
                        const amp = 40 + (subDrivePct * 30);
                        const y = Math.sin(x * 0.05 + subTime) * amp;
                        if(x===0) subCtx.moveTo(x, midY + y); else subCtx.lineTo(x, midY + y);
                    }
                    subCtx.stroke();
                    subCtx.shadowBlur = 0; // reset
                }

                subCtx.globalCompositeOperation = 'source-over';
            }
        </script>
        <style>
            .wind-shear-wrapper {
                background: #020305;
                border: 2px solid #112233;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            }

            .wind-canvas-box {
                width: 100%;
                height: 250px;
                background: radial-gradient(circle at center top, #0a111a 0%, #000 100%);
                border: 1px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 40px rgba(0, 229, 255, 0.05);
            }
            #windCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Virtual Stage & Audience Zones */
            .ws-stage {
                position: absolute; top: 0; left: 50%; transform: translateX(-50%);
                width: 80px; height: 15px; background: #222; border-bottom: 2px solid var(--gold-primary);
                display: flex; justify-content: space-between; padding: 0 10px; align-items: center; z-index: 5;
            }
            .ws-speaker { width: 10px; height: 10px; background: #111; border: 1px solid #555; border-radius: 2px; }
            
            .ws-audience {
                position: absolute; bottom: 20px; left: 50%; transform: translateX(-50%);
                width: 150px; height: 40px; border: 1px dashed rgba(255,255,255,0.3); border-radius: 4px;
                display: flex; justify-content: center; align-items: center; color: rgba(255,255,255,0.4);
                font-family: var(--font-tech); font-size: 8px; letter-spacing: 2px; z-index: 1; pointer-events: none;
            }

            .wind-controls {
                display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 15px;
                background: #050505; padding: 15px; border-radius: 8px; border: 1px solid #1a1a1a;
            }
            .wc-group { display: flex; flex-direction: column; gap: 5px; }
            .wc-lbl { font-family: var(--font-data); font-size: 9px; color: #888; font-weight: bold; letter-spacing: 1px; }
            .wc-val { font-family: var(--font-tech); font-size: 14px; color: var(--cyan-neon); text-align: right; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">AERO-ACOUSTIC PHYSICS</h2>
                <div class="section-icon"><i class="fas fa-wind" style="color: var(--cyan-neon);"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate crosswind shear on high-frequency sound waves. Heavy winds will blow the acoustic payload off the target audience zone.</p>

            <div class="wind-shear-wrapper">
                <div class="wind-canvas-box" id="windWrap">
                    <canvas id="windCanvas"></canvas>
                    <div class="ws-stage"><div class="ws-speaker"></div><div class="ws-speaker"></div></div>
                    <div class="ws-audience">TARGET AUDIENCE ZONE</div>
                    
                    <i class="fas fa-long-arrow-alt-right" id="windArrow" style="position:absolute; top:20px; left:20px; color:rgba(255,255,255,0.5); font-size:24px; transition: transform 0.3s, color 0.3s; z-index:5;"></i>
                </div>

                <div class="wind-controls">
                    <div class="wc-group">
                        <div style="display:flex; justify-content:space-between;"><span class="wc-lbl">WIND SPEED</span><span class="wc-val" id="wsSpeedVal">0 km/h</span></div>
                        <input type="range" class="app-slider" id="wsSpeed" min="0" max="60" value="0" oninput="updateWindPhysics()">
                    </div>
                    <div class="wc-group">
                        <div style="display:flex; justify-content:space-between;"><span class="wc-lbl">DIRECTION</span><span class="wc-val" id="wsDirVal" style="color:var(--gold-primary);">CENTER</span></div>
                        <input type="range" class="app-slider" id="wsDir" min="-100" max="100" value="0" oninput="updateWindPhysics()">
                    </div>
                </div>
            </div>
        </div>

        <style>
            .pdu-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .phase-meters {
                display: flex; justify-content: space-around; align-items: flex-end;
                height: 140px; background: #0a0a0f; border: 1px solid #1a1a24; border-radius: 8px;
                padding: 15px 10px 30px 10px; margin-bottom: 20px; position: relative;
            }

            .phase-bar-container {
                width: 30px; height: 100%; background: #111; border: 1px solid #333;
                border-radius: 4px; position: relative; overflow: hidden;
            }
            .phase-fill {
                position: absolute; bottom: 0; left: 0; width: 100%; height: 0%;
                transition: height 0.3s ease-out, background 0.3s;
            }
            /* Specific Phase Colors */
            #fillL1 { background: linear-gradient(0deg, #550000, var(--red-alert)); }
            #fillL2 { background: linear-gradient(0deg, #555500, #ffff00); }
            #fillL3 { background: linear-gradient(0deg, #000055, #0055ff); }

            .phase-lbl {
                position: absolute; bottom: -22px; left: 50%; transform: translateX(-50%);
                font-family: var(--font-tech); font-size: 10px; font-weight: bold; color: #fff;
            }
            .phase-val {
                position: absolute; top: -20px; left: 50%; transform: translateX(-50%);
                font-family: var(--font-data); font-size: 10px; color: #aaa; white-space: nowrap;
            }

            /* 63A Trip Line */
            .pdu-trip-line {
                position: absolute; top: 20%; left: 0; right: 0; height: 1px;
                background: var(--red-alert); border-bottom: 1px dashed #ff9999; z-index: 5;
            }
            .pdu-trip-line::before {
                content: '63A MAX'; position: absolute; right: 5px; top: -12px;
                color: var(--red-alert); font-family: var(--font-tech); font-size: 8px;
            }

            .pdu-sliders { display: flex; flex-direction: column; gap: 15px; }
            .pdu-row { display: flex; align-items: center; gap: 10px; }
            .pdu-row-lbl { font-family: var(--font-data); font-size: 10px; color: #888; width: 60px; font-weight: bold;}

            .neutral-warning {
                margin-top: 15px; padding: 10px; border-radius: 6px; text-align: center;
                font-family: var(--font-body); font-size: 11px; font-weight: bold; transition: 0.3s;
                border: 1px solid transparent;
            }
            .nw-safe { background: rgba(0,255,0,0.1); color: #00ff00; border-color: #00ff00; }
            .nw-danger { background: rgba(255,51,51,0.1); color: var(--red-alert); border-color: var(--red-alert); animation: blink 0.5s infinite; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">3-PHASE PDU BALANCER</h2>
                <div class="section-icon"><i class="fas fa-plug" style="color: #ffff00;"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Balance the Amperage load across Red, Yellow, and Blue phases. Imbalance causes neutral wire overheating.</p>

            <div class="pdu-wrapper">
                <div class="phase-meters">
                    <div class="pdu-trip-line"></div>
                    
                    <div class="phase-bar-container">
                        <div class="phase-fill" id="fillL1"></div>
                        <span class="phase-val" id="valL1">0A</span>
                        <span class="phase-lbl" style="color:var(--red-alert);">L1</span>
                    </div>
                    <div class="phase-bar-container">
                        <div class="phase-fill" id="fillL2"></div>
                        <span class="phase-val" id="valL2">0A</span>
                        <span class="phase-lbl" style="color:#ffff00;">L2</span>
                    </div>
                    <div class="phase-bar-container">
                        <div class="phase-fill" id="fillL3"></div>
                        <span class="phase-val" id="valL3">0A</span>
                        <span class="phase-lbl" style="color:#0055ff;">L3</span>
                    </div>
                </div>

                <div class="pdu-sliders">
                    <div class="pdu-row">
                        <span class="pdu-row-lbl">SUBWOOFERS</span>
                        <input type="range" class="app-slider" id="pduL1" min="0" max="80" value="0" oninput="calculatePDU()">
                    </div>
                    <div class="pdu-row">
                        <span class="pdu-row-lbl">LINE ARRAY</span>
                        <input type="range" class="app-slider" id="pduL2" min="0" max="80" value="0" oninput="calculatePDU()">
                    </div>
                    <div class="pdu-row">
                        <span class="pdu-row-lbl">DMX LIGHTS</span>
                        <input type="range" class="app-slider" id="pduL3" min="0" max="80" value="0" oninput="calculatePDU()">
                    </div>
                </div>

                <div class="neutral-warning nw-safe" id="neutralStatus">
                    NEUTRAL CURRENT: 0.0A (BALANCED)
                </div>
            </div>
        </div>

        <style>
            .artnet-wrapper {
                background: #020408;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .net-canvas-box {
                width: 100%;
                height: 200px;
                background: #000;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                border: 1px solid #003344;
            }
            #netCanvas { width: 100%; height: 100%; display: block; position: relative; z-index: 2;}
            
            /* Physical Nodes rendered via DOM over Canvas for crispness */
            .net-node {
                position: absolute; transform: translate(-50%, -50%);
                background: #111; border: 2px solid #555; border-radius: 6px;
                display: flex; flex-direction: column; align-items: center; justify-content: center;
                padding: 5px; z-index: 10; box-shadow: 0 5px 15px rgba(0,0,0,0.8);
            }
            .net-node i { font-size: 16px; color: #ccc; }
            .net-node span { font-family: var(--font-data); font-size: 8px; color: #888; margin-top: 4px; font-weight: bold; }
            
            /* Active state for nodes */
            .net-node.active { border-color: var(--cyan-neon); box-shadow: 0 0 15px rgba(0,229,255,0.4); }
            .net-node.active i { color: var(--cyan-neon); }

            #nodeFOH { top: 85%; left: 50%; }
            #nodeSwitch { top: 50%; left: 50%; border-radius: 50%; width: 40px; height: 40px; }
            #nodeTrussL { top: 15%; left: 20%; }
            #nodeTrussR { top: 15%; left: 80%; }

            .net-controls {
                display: flex; justify-content: space-between; align-items: center; margin-top: 15px;
                background: #0a0a0f; padding: 12px; border-radius: 6px; border: 1px solid #1a1a24;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">ART-NET TOPOGRAPHY</h2>
                <div class="section-icon"><i class="fas fa-network-wired"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Monitor digital DMX-over-Ethernet packets traveling from FOH to the stage rig.</p>

            <div class="artnet-wrapper">
                <div class="net-canvas-box" id="netWrap">
                    <canvas id="netCanvas"></canvas>
                    
                    <div class="net-node active" id="nodeFOH">
                        <i class="fas fa-laptop"></i><span>FOH CONSOLE</span>
                    </div>
                    <div class="net-node active" id="nodeSwitch">
                        <i class="fas fa-ethernet"></i>
                    </div>
                    <div class="net-node active" id="nodeTrussL">
                        <i class="fas fa-lightbulb"></i><span>RIG LEFT</span>
                    </div>
                    <div class="net-node active" id="nodeTrussR">
                        <i class="fas fa-lightbulb"></i><span>RIG RIGHT</span>
                    </div>
                </div>

                <div class="net-controls">
                    <div style="display:flex; flex-direction:column;">
                        <span style="font-family:var(--font-data); font-size:9px; color:#888;">PACKET LATENCY</span>
                        <span id="netLatencyVal" style="font-family:var(--font-tech); font-size:14px; color:#00ff00; font-weight:bold;">1.2 ms</span>
                    </div>
                    <button class="app-btn-outline" style="width: auto; padding: 10px 20px;" onclick="pingArtNet()">
                        <i class="fas fa-satellite-transmit"></i> PING NETWORK
                    </button>
                </div>
            </div>
        </div>

        <script>
            // --- 1. AERO-ACOUSTIC WIND SHEAR LOGIC ---
            const wCanvas = document.getElementById('windCanvas');
            let wCtx = null;
            const wWrap = document.getElementById('windWrap');
            
            let windSpeed = 0;   // 0 to 60
            let windDir = 0;     // -100 to 100 (Left to Right)
            let acousticParticles = [];
            let wAnimFrame = null;

            function initWindEngine() {
                if(!wWrap || !wCanvas) return;
                wCanvas.width = wWrap.clientWidth;
                wCanvas.height = wWrap.clientHeight;
                wCtx = wCanvas.getContext('2d');
                if(!wAnimFrame) animateWindAcoustics();
            }
            window.addEventListener('resize', initWindEngine);
            setTimeout(initWindEngine, 500);

            function updateWindPhysics() {
                windSpeed = parseInt(document.getElementById('wsSpeed').value);
                windDir = parseInt(document.getElementById('wsDir').value);
                
                document.getElementById('wsSpeedVal').innerText = `${windSpeed} km/h`;
                
                const dirText = windDir < 0 ? `LEFT ${Math.abs(windDir)}%` : windDir > 0 ? `RIGHT ${windDir}%` : 'CENTER';
                document.getElementById('wsDirVal').innerText = dirText;

                // Update Arrow UI
                const arrow = document.getElementById('windArrow');
                if(windSpeed === 0) {
                    arrow.style.color = "rgba(255,255,255,0.2)";
                    arrow.style.transform = `rotate(90deg) scale(1)`; // point down (no wind)
                } else {
                    // Map -100 to 100 to roughly 0deg to 180deg
                    const angle = 90 + (windDir * 0.9);
                    // Scale arrow size based on speed
                    const scale = 1 + (windSpeed / 60);
                    arrow.style.color = "var(--red-alert)";
                    arrow.style.transform = `rotate(${angle}deg) scale(${scale})`;
                }
                
                if(navigator.vibrate && windSpeed > 40) navigator.vibrate(10);
            }

            class SoundWaveParticle {
                constructor(startX, startY) {
                    this.x = startX;
                    this.y = startY;
                    
                    // Base trajectory is straight down towards audience
                    // Spread slightly like a speaker cone
                    this.vx = (Math.random() - 0.5) * 2; 
                    this.vy = Math.random() * 2 + 2; // Move down
                    
                    this.life = 1.0;
                    this.size = Math.random() * 10 + 5;
                }
                update() {
                    // Apply Wind Physics
                    // windDir is -100 to 100. windSpeed is 0 to 60.
                    // Normalize to a pixel force multiplier
                    const forceX = (windDir / 100) * (windSpeed / 20);
                    
                    this.vx += forceX * 0.1; // Gradual push
                    
                    this.x += this.vx;
                    this.y += this.vy;
                    
                    // Fade out as it gets further
                    this.life -= 0.01;
                    this.size += 0.5; // Wave expands
                }
                draw(ctx) {
                    if(this.life <= 0) return;
                    
                    // Color transitions from white to cyan to blue
                    ctx.fillStyle = `rgba(0, 229, 255, ${this.life * 0.3})`;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size, 0, Math.PI*2);
                    ctx.fill();
                }
            }

            function animateWindAcoustics() {
                wAnimFrame = requestAnimationFrame(animateWindAcoustics);
                if(!wCtx) return;

                wCtx.fillStyle = 'rgba(10, 17, 26, 0.4)'; // Motion blur
                wCtx.fillRect(0,0, wCanvas.width, wCanvas.height);

                wCtx.globalCompositeOperation = 'screen';

                // Spawn new particles from the stage (Top Center)
                // Coordinates match CSS: left 50%, width 80px -> roughly cx - 30 and cx + 30
                const cx = wCanvas.width / 2;
                
                // Only spawn if system is "on" (just doing continuous for visual)
                if(Math.random() > 0.3) {
                    acousticParticles.push(new SoundWaveParticle(cx - 30, 15)); // Left speaker
                    acousticParticles.push(new SoundWaveParticle(cx + 30, 15)); // Right speaker
                }

                for(let i = acousticParticles.length - 1; i >= 0; i--) {
                    let p = acousticParticles[i];
                    p.update();
                    p.draw(wCtx);
                    if(p.life <= 0 || p.y > wCanvas.height) {
                        acousticParticles.splice(i, 1);
                    }
                }
                wCtx.globalCompositeOperation = 'source-over';
            }


            // --- 2. 3-PHASE FOH POWER DISTRO LOGIC ---
            const MAX_AMP_LIMIT = 80; // Slider max
            const TRIP_AMP_LIMIT = 63; // Red line max

            function calculatePDU() {
                const l1 = parseInt(document.getElementById('pduL1').value);
                const l2 = parseInt(document.getElementById('pduL2').value);
                const l3 = parseInt(document.getElementById('pduL3').value);

                // Update visual bars
                const updateBar = (id, val) => {
                    document.getElementById(`val${id}`).innerText = `${val}A`;
                    const fill = document.getElementById(`fill${id}`);
                    
                    // Max height is represented by 80A. 
                    let pct = (val / MAX_AMP_LIMIT) * 100;
                    fill.style.height = `${pct}%`;

                    // Blink if tripped
                    if(val >= TRIP_AMP_LIMIT) {
                        fill.style.animation = 'blink 0.2s infinite';
                    } else {
                        fill.style.animation = 'none';
                    }
                };

                updateBar('L1', l1);
                updateBar('L2', l2);
                updateBar('L3', l3);

                // Check for trips
                if(l1 >= TRIP_AMP_LIMIT || l2 >= TRIP_AMP_LIMIT || l3 >= TRIP_AMP_LIMIT) {
                    if(navigator.vibrate) navigator.vibrate([100, 50, 100]);
                }

                // Math: Calculate Neutral Current due to phase imbalance
                // In a perfectly balanced 3-phase star system, neutral current = 0.
                // Simplified rough formula for visualization: Max diff between highest and lowest phase
                const maxLoad = Math.max(l1, l2, l3);
                const minLoad = Math.min(l1, l2, l3);
                
                // If everything is 0, it's balanced.
                if(maxLoad === 0) {
                    setNeutralStatus(0, true);
                    return;
                }

                const imbalance = maxLoad - minLoad;
                
                // Fake complex math representation
                const neutralAmps = (imbalance * 0.8).toFixed(1);

                // If imbalance is greater than 20 Amps, it's dangerous
                if(imbalance > 20) {
                    setNeutralStatus(neutralAmps, false);
                    if(navigator.vibrate) navigator.vibrate(10); // Warning buzz
                } else {
                    setNeutralStatus(neutralAmps, true);
                }
            }

            function setNeutralStatus(amps, isSafe) {
                const statBox = document.getElementById('neutralStatus');
                if(isSafe) {
                    statBox.className = 'neutral-warning nw-safe';
                    statBox.innerText = `NEUTRAL CURRENT: ${amps}A (BALANCED)`;
                } else {
                    statBox.className = 'neutral-warning nw-danger';
                    statBox.innerText = `CRITICAL IMBALANCE! NEUTRAL CURRENT: ${amps}A`;
                }
            }


            // --- 3. ART-NET DMX NETWORK TOPOGRAPHY LOGIC ---
            const nCanvas = document.getElementById('netCanvas');
            let nCtx = null;
            const nWrap = document.getElementById('netWrap');
            
            let netAnimFrame = null;
            let dataPackets = [];
            
            // Define node coordinates relative to canvas (matches CSS percentages roughly)
            let nFOH = {x:0, y:0};
            let nSW = {x:0, y:0};
            let nTL = {x:0, y:0};
            let nTR = {x:0, y:0};

            function initNetworkEngine() {
                if(!nWrap || !nCanvas) return;
                nCanvas.width = nWrap.clientWidth;
                nCanvas.height = nWrap.clientHeight;
                nCtx = nCanvas.getContext('2d');
                
                const w = nCanvas.width;
                const h = nCanvas.height;
                
                nFOH = { x: w*0.5, y: h*0.85 };
                nSW =  { x: w*0.5, y: h*0.5 };
                nTL =  { x: w*0.2, y: h*0.15 };
                nTR =  { x: w*0.8, y: h*0.15 };

                if(!netAnimFrame) animateNetwork();
            }
            window.addEventListener('resize', initNetworkEngine);
            setTimeout(initNetworkEngine, 800);

            class DataPacket {
                constructor(startX, startY, targetX, targetY, color) {
                    this.x = startX;
                    this.y = startY;
                    this.tx = targetX;
                    this.ty = targetY;
                    this.color = color;
                    this.speed = 0.1; // Lerp speed
                    this.arrived = false;
                }
                update() {
                    this.x += (this.tx - this.x) * this.speed;
                    this.y += (this.ty - this.y) * this.speed;
                    
                    const dist = Math.hypot(this.tx - this.x, this.ty - this.y);
                    if(dist < 5) this.arrived = true;
                }
                draw(ctx) {
                    ctx.fillStyle = this.color;
                    ctx.shadowBlur = 10;
                    ctx.shadowColor = this.color;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, 3, 0, Math.PI*2);
                    ctx.fill();
                    ctx.shadowBlur = 0;
                }
            }

            function pingArtNet() {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                
                document.getElementById('netLatencyVal').innerText = "PINGING...";
                document.getElementById('netLatencyVal').style.color = "var(--gold-primary)";

                // Fire a manual diagnostic packet
                dataPackets.push(new DataPacket(nFOH.x, nFOH.y, nSW.x, nSW.y, '#fff'));

                setTimeout(() => {
                    const latency = (Math.random() * 1.5 + 0.5).toFixed(2); // 0.5 to 2.0 ms
                    document.getElementById('netLatencyVal').innerText = `${latency} ms`;
                    document.getElementById('netLatencyVal').style.color = "#00ff00";
                    
                    // Flash nodes
                    document.querySelectorAll('.net-node').forEach(n => {
                        n.style.background = 'rgba(0,255,0,0.2)';
                        setTimeout(()=> n.style.background = '#111', 200);
                    });
                }, 800); // Fake delay
            }

            function animateNetwork() {
                netAnimFrame = requestAnimationFrame(animateNetwork);
                if(!nCtx) return;

                nCtx.clearRect(0,0, nCanvas.width, nCanvas.height);

                // Draw solid connecting lines (Cables)
                nCtx.strokeStyle = '#003344';
                nCtx.lineWidth = 2;
                nCtx.beginPath();
                nCtx.moveTo(nFOH.x, nFOH.y); nCtx.lineTo(nSW.x, nSW.y); // FOH to Switch
                nCtx.moveTo(nSW.x, nSW.y); nCtx.lineTo(nTL.x, nTL.y);   // Switch to Left
                nCtx.moveTo(nSW.x, nSW.y); nCtx.lineTo(nTR.x, nTR.y);   // Switch to Right
                nCtx.stroke();

                // Randomly generate background DMX traffic
                if(Math.random() > 0.85) {
                    // Send to switch
                    dataPackets.push(new DataPacket(nFOH.x, nFOH.y, nSW.x, nSW.y, 'var(--cyan-neon)'));
                }

                // Update Packets
                for(let i = dataPackets.length - 1; i >= 0; i--) {
                    let p = dataPackets[i];
                    p.update();
                    p.draw(nCtx);
                    
                    // Routing Logic
                    if(p.arrived) {
                        // If it hit the switch, route it to L and R
                        if(p.tx === nSW.x && p.ty === nSW.y) {
                            dataPackets.push(new DataPacket(nSW.x, nSW.y, nTL.x, nTL.y, 'var(--gold-primary)'));
                            dataPackets.push(new DataPacket(nSW.x, nSW.y, nTR.x, nTR.y, 'var(--gold-primary)'));
                        }
                        // Remove original packet
                        dataPackets.splice(i, 1);
                    }
                }
            }
        </script>
        <style>
            .impedance-wrapper {
                background: linear-gradient(180deg, #050508, #111);
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: inset 0 0 20px rgba(0,0,0,0.8);
            }

            .imp-hud {
                display: flex; justify-content: space-between; align-items: center;
                background: #000; border: 1px solid #333; padding: 15px; border-radius: 8px; margin-bottom: 15px;
            }
            .imp-stat { text-align: center; flex: 1; border-right: 1px dashed #222; }
            .imp-stat:last-child { border-right: none; }
            .imp-lbl { font-family: var(--font-data); font-size: 9px; color: #888; font-weight: bold; letter-spacing: 1px; display: block; margin-bottom: 5px; }
            .imp-val { font-family: var(--font-tech); font-size: 20px; font-weight: 900; color: #fff; transition: 0.3s; }

            .wiring-display {
                width: 100%; min-height: 120px; background: #0a0a0f; border: 1px solid #1a1a24;
                border-radius: 8px; padding: 15px; display: flex; flex-direction: column; gap: 10px;
                overflow-x: auto; position: relative;
            }

            .wire-group {
                display: flex; align-items: center; gap: 10px; padding: 10px;
                background: rgba(255,255,255,0.02); border: 1px dashed #333; border-radius: 6px;
            }
            .spk-icon {
                width: 40px; height: 40px; background: #111; border: 2px solid #444; border-radius: 4px;
                display: flex; justify-content: center; align-items: center; position: relative;
            }
            .spk-icon::before { content: ''; width: 20px; height: 20px; border-radius: 50%; border: 2px solid #666; }
            .spk-icon::after { content: '8Ω'; position: absolute; bottom: -15px; font-family: var(--font-tech); font-size: 9px; color: #aaa; }

            /* Wiring Lines */
            .wire-line { height: 2px; flex: 1; min-width: 20px; background: var(--gold-primary); box-shadow: 0 0 5px var(--gold-primary); position: relative; }
            .wire-line.parallel { background: var(--cyan-neon); box-shadow: 0 0 5px var(--cyan-neon); }

            .imp-controls { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px; }
            
            .amp-protect { color: var(--red-alert) !important; text-shadow: 0 0 10px rgba(255,51,51,0.8); animation: blink 0.5s infinite; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">IMPEDANCE MATCHING AI</h2>
                <div class="section-icon"><i class="fas fa-wave-square"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Wire 8-Ohm subwoofers in Series (adds resistance) or Parallel (divides resistance). Keep the total load above 2.0Ω to prevent amplifier meltdown.</p>

            <div class="impedance-wrapper">
                <div class="imp-hud">
                    <div class="imp-stat">
                        <span class="imp-lbl">TOTAL LOAD</span>
                        <span class="imp-val" id="totalOhmVal" style="color: #00ff00;">8.0 Ω</span>
                    </div>
                    <div class="imp-stat">
                        <span class="imp-lbl">AMP STATUS</span>
                        <span class="imp-val" id="ampStateVal" style="font-size: 14px; margin-top: 4px; display: inline-block;">STABLE</span>
                    </div>
                </div>

                <div class="wiring-display" id="wiringBoard">
                    <div class="wire-group" id="circuit1">
                        <div style="font-family:var(--font-data); font-size:9px; color:#555; width:30px;">AMP<br>OUT</div>
                        <div class="wire-line"></div>
                        <div class="spk-icon"></div>
                    </div>
                </div>

                <div class="imp-controls">
                    <button class="app-btn-outline" style="border-color: var(--cyan-neon); color: var(--cyan-neon);" onclick="addSpeaker('parallel')">
                        + ADD PARALLEL
                    </button>
                    <button class="app-btn-outline" style="border-color: var(--gold-primary); color: var(--gold-primary);" onclick="addSpeaker('series')">
                        + ADD SERIES
                    </button>
                    <button class="app-btn-outline" style="grid-column: span 2; border-color: var(--red-alert); color: var(--red-alert);" onclick="resetImpedance()">
                        <i class="fas fa-trash"></i> CLEAR CIRCUIT
                    </button>
                </div>
            </div>
        </div>

        <style>
            .universe-wrapper {
                background: #000;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .dmx-grid-container {
                display: grid;
                /* 32 columns x 16 rows = 512 channels */
                grid-template-columns: repeat(32, 1fr);
                gap: 1px;
                background: #222;
                border: 2px solid #333;
                padding: 2px;
                border-radius: 4px;
                margin-top: 15px;
                margin-bottom: 15px;
            }

            .dmx-ch-block {
                aspect-ratio: 1 / 1;
                background: #0a0a0f;
                transition: background 0.2s, transform 0.1s;
            }
            /* Colors for different fixture types */
            .ch-sharpy { background: var(--cyan-neon); box-shadow: 0 0 5px rgba(0,229,255,0.5); }
            .ch-par { background: var(--gold-primary); }
            .ch-smoke { background: #fff; }

            .uni-hud { display: flex; justify-content: space-between; margin-bottom: 10px; }
            .uh-lbl { font-family: var(--font-data); font-size: 10px; color: #888; font-weight: bold; }
            .uh-val { font-family: var(--font-tech); font-size: 14px; color: #fff; font-weight: bold; }

            .uni-bar-bg { width: 100%; height: 6px; background: #111; border-radius: 3px; overflow: hidden; margin-bottom: 20px;}
            .uni-bar-fill { height: 100%; width: 0%; background: linear-gradient(90deg, #00ff00, var(--cyan-neon), var(--red-alert)); transition: width 0.3s; }

            .patch-controls { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }
            .patch-btn {
                background: #0a0a0f; border: 1px solid #333; border-radius: 6px; padding: 10px 5px;
                text-align: center; cursor: pointer; transition: 0.2s; display: flex; flex-direction: column; align-items: center; gap: 5px;
            }
            .patch-btn:active { transform: scale(0.95); border-color: #fff; }
            .patch-btn i { font-size: 16px; }
            .patch-btn span { font-family: var(--font-tech); font-size: 8px; color: #aaa; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DMX UNIVERSE PATCH BAY</h2>
                <div class="section-icon"><i class="fas fa-microchip"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Allocate digital network memory. A single DMX universe holds 512 channels. Different fixtures require different footprints.</p>

            <div class="universe-wrapper">
                <div class="uni-hud">
                    <span class="uh-lbl">UNIVERSE 1 (ADDRESSES)</span>
                    <span class="uh-val" id="uniCountVal">0 / 512</span>
                </div>
                <div class="uni-bar-bg"><div class="uni-bar-fill" id="uniBarFill"></div></div>

                <div class="dmx-grid-container" id="dmxMemoryGrid">
                    </div>

                <div class="patch-controls">
                    <div class="patch-btn" style="color:var(--cyan-neon); border-color:rgba(0,229,255,0.3);" onclick="patchFixture('sharpy', 16)">
                        <i class="fas fa-lightbulb"></i><span>SHARPY (16CH)</span>
                    </div>
                    <div class="patch-btn" style="color:var(--gold-primary); border-color:rgba(212,175,55,0.3);" onclick="patchFixture('par', 4)">
                        <i class="fas fa-sun"></i><span>LED PAR (4CH)</span>
                    </div>
                    <div class="patch-btn" style="color:#fff; border-color:rgba(255,255,255,0.3);" onclick="patchFixture('smoke', 2)">
                        <i class="fas fa-wind"></i><span>HAZER (2CH)</span>
                    </div>
                </div>
                <button class="app-btn-outline" style="width:100%; margin-top:10px; border-color:var(--red-alert); color:var(--red-alert);" onclick="clearDmxUniverse()">WIPE MEMORY</button>
            </div>
        </div>

        <style>
            .haze-wrapper {
                background: #020406;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .haze-canvas-box {
                width: 100%;
                height: 220px;
                background: radial-gradient(circle at center, #0a0a0f 0%, #000 100%);
                border: 1px solid #1a2233;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #hazeCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; filter: blur(4px); }

            /* Virtual Hazer Machine */
            .hazer-machine {
                position: absolute; top: 50%; left: 10%; transform: translateY(-50%);
                width: 15px; height: 25px; background: #111; border: 1px solid var(--gold-primary);
                border-radius: 3px; z-index: 5;
            }
            .hazer-machine::after {
                content: ''; position: absolute; right: -4px; top: 50%; transform: translateY(-50%);
                width: 4px; height: 10px; background: var(--gold-primary); border-radius: 0 4px 4px 0;
            }

            .haze-controls {
                display: flex; flex-direction: column; gap: 10px; margin-top: 15px;
                background: #050505; padding: 15px; border-radius: 8px; border: 1px solid #111;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">ATMOSPHERIC HAZE AI</h2>
                <div class="section-icon"><i class="fas fa-smog" style="color: #fff;"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate micro-fluid particle diffusion. Haze reveals laser beams without dropping the ambient temperature.</p>

            <div class="haze-wrapper">
                <div class="haze-canvas-box" id="hazeWrap">
                    <canvas id="hazeCanvas"></canvas>
                    <div class="hazer-machine"></div>
                    <div style="position:absolute; bottom:10px; right:10px; color:rgba(255,255,255,0.3); font-family:var(--font-tech); font-size:8px; z-index:10;">TOP-DOWN DIFFUSION</div>
                </div>

                <div class="haze-controls">
                    <div style="display:flex; justify-content:space-between;">
                        <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">HAZER OUTPUT FLOW</span>
                        <span id="hazeFlowVal" style="font-family:var(--font-tech); font-size:12px; color:#fff;">30%</span>
                    </div>
                    <input type="range" class="app-slider" id="hazeSlider" min="0" max="100" value="30" oninput="updateHazeFlow()">
                </div>
            </div>
        </div>

        <script>
            // --- 1. ACOUSTIC IMPEDANCE MATRIX LOGIC ---
            let speakerLoadList = [8]; // Start with one 8-ohm speaker
            let currentCircuitIndex = 1;

            function updateImpedanceUI() {
                // Calculate Total Impedance
                // In this simplified FOH simulator, we treat the 'circuit' array.
                // If the user presses "Series", we sum. If "Parallel", we use reciprocal math.
                // To keep the math straightforward for the UI simulation, we recalculate based on the DOM structure.

                const circuits = document.querySelectorAll('.wire-group');
                let masterImpedance = 0;

                // Let's assume all speakers added inside a 'wire-group' are in PARALLEL with each other.
                // And multiple 'wire-groups' connected end-to-end are in SERIES.
                
                circuits.forEach(group => {
                    const speakersInGroup = group.querySelectorAll('.spk-icon').length;
                    if(speakersInGroup > 0) {
                        // Parallel math for identical 8-ohm speakers: R_total = R / n
                        const groupImpedance = 8 / speakersInGroup;
                        masterImpedance += groupImpedance; // Series addition for groups
                    }
                });

                const ohmVal = document.getElementById('totalOhmVal');
                const ampState = document.getElementById('ampStateVal');
                
                const finalOhms = masterImpedance.toFixed(1);
                ohmVal.innerText = `${finalOhms} Ω`;

                // Amplifier Logic
                if(masterImpedance < 2.0) {
                    ohmVal.className = 'imp-val amp-protect';
                    ampState.className = 'imp-val amp-protect';
                    ampState.innerText = 'PROTECT MODE';
                    if(navigator.vibrate) navigator.vibrate([200, 100, 300]);
                    if(typeof triggerToast === 'function') triggerToast("CRITICAL: Amp load below 2 Ohms!");
                } else if(masterImpedance < 4.0) {
                    ohmVal.className = 'imp-val';
                    ohmVal.style.color = 'var(--gold-primary)';
                    ampState.className = 'imp-val';
                    ampState.style.color = 'var(--gold-primary)';
                    ampState.innerText = 'HEAVY LOAD';
                } else {
                    ohmVal.className = 'imp-val';
                    ohmVal.style.color = '#00ff00';
                    ampState.className = 'imp-val';
                    ampState.style.color = '#00ff00';
                    ampState.innerText = 'STABLE';
                }
            }

            function addSpeaker(type) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(10);

                const board = document.getElementById('wiringBoard');

                if(type === 'parallel') {
                    // Add speaker to the current/last active circuit group
                    const currentGroup = document.getElementById(`circuit${currentCircuitIndex}`);
                    if(currentGroup) {
                        const line = document.createElement('div');
                        line.className = 'wire-line parallel';
                        const spk = document.createElement('div');
                        spk.className = 'spk-icon';
                        currentGroup.appendChild(line);
                        currentGroup.appendChild(spk);
                    }
                } else if(type === 'series') {
                    // Create a new circuit group linked end-to-end
                    currentCircuitIndex++;
                    const newGroup = document.createElement('div');
                    newGroup.className = 'wire-group';
                    newGroup.id = `circuit${currentCircuitIndex}`;
                    
                    const connector = document.createElement('div');
                    connector.innerHTML = '<i class="fas fa-link" style="color:var(--gold-primary); font-size:10px;"></i>';
                    
                    const line = document.createElement('div');
                    line.className = 'wire-line';
                    const spk = document.createElement('div');
                    spk.className = 'spk-icon';
                    
                    newGroup.appendChild(connector);
                    newGroup.appendChild(line);
                    newGroup.appendChild(spk);
                    
                    board.appendChild(newGroup);
                }

                // Scroll to right
                board.scrollLeft = board.scrollWidth;
                updateImpedanceUI();
            }

            function resetImpedance() {
                if(typeof playTap === 'function') playTap();
                const board = document.getElementById('wiringBoard');
                board.innerHTML = `
                    <div class="wire-group" id="circuit1">
                        <div style="font-family:var(--font-data); font-size:9px; color:#555; width:30px;">AMP<br>OUT</div>
                        <div class="wire-line"></div>
                        <div class="spk-icon"></div>
                    </div>
                `;
                currentCircuitIndex = 1;
                updateImpedanceUI();
            }


            // --- 2. DMX-512 UNIVERSE PATCH BAY LOGIC ---
            const MAX_DMX = 512;
            let currentDmxAddress = 0; // The next available channel

            function initDmxGrid() {
                const grid = document.getElementById('dmxMemoryGrid');
                grid.innerHTML = '';
                // Inject 512 tiny div blocks
                for(let i=0; i<MAX_DMX; i++) {
                    const blk = document.createElement('div');
                    blk.className = 'dmx-ch-block';
                    blk.id = `dmxCh${i}`;
                    grid.appendChild(blk);
                }
                updateDmxUI();
            }
            // Run on load
            setTimeout(initDmxGrid, 200);

            function patchFixture(type, channels) {
                if(currentDmxAddress + channels > MAX_DMX) {
                    if(typeof triggerToast === 'function') triggerToast("Universe Full! Add a DMX Splitter.");
                    if(navigator.vibrate) navigator.vibrate([50, 50, 50]);
                    return;
                }
                
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(15);

                // Add delay for digital writing effect
                let chIndex = 0;
                const patchInterval = setInterval(() => {
                    if(chIndex >= channels) {
                        clearInterval(patchInterval);
                        updateDmxUI();
                        return;
                    }
                    
                    const block = document.getElementById(`dmxCh${currentDmxAddress}`);
                    if(block) {
                        block.className = `dmx-ch-block ch-${type}`;
                        // Add pop animation
                        block.style.transform = 'scale(1.5)';
                        setTimeout(() => block.style.transform = 'scale(1)', 100);
                    }
                    
                    currentDmxAddress++;
                    chIndex++;
                    
                }, 20); // 20ms per channel write speed
            }

            function clearDmxUniverse() {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(50);
                
                for(let i=0; i<MAX_DMX; i++) {
                    const block = document.getElementById(`dmxCh${i}`);
                    if(block) block.className = 'dmx-ch-block';
                }
                currentDmxAddress = 0;
                updateDmxUI();
                if(typeof triggerToast === 'function') triggerToast("DMX Memory Wiped.");
            }

            function updateDmxUI() {
                document.getElementById('uniCountVal').innerText = `${currentDmxAddress} / ${MAX_DMX}`;
                const pct = (currentDmxAddress / MAX_DMX) * 100;
                document.getElementById('uniBarFill').style.width = `${pct}%`;
            }


            // --- 3. ATMOSPHERIC HAZE DIFFUSION AI ---
            const hzCanvas = document.getElementById('hazeCanvas');
            let hzCtx = null;
            const hzWrap = document.getElementById('hazeWrap');
            
            let hazeParticles = [];
            let hzAnimFrame = null;
            let hazeFlowRate = 30; // Output percentage

            function initHazeEngine() {
                if(!hzWrap || !hzCanvas) return;
                hzCanvas.width = hzWrap.clientWidth;
                hzCanvas.height = hzWrap.clientHeight;
                hzCtx = hzCanvas.getContext('2d');
                if(!hzAnimFrame) animateHaze();
            }
            window.addEventListener('resize', initHazeEngine);
            setTimeout(initHazeEngine, 600);

            function updateHazeFlow() {
                hazeFlowRate = parseInt(document.getElementById('hazeSlider').value);
                document.getElementById('hazeFlowVal').innerText = `${hazeFlowRate}%`;
                
                // Audio cue from Part 3 if available (hissing sound)
                if(hazeFlowRate > 0 && typeof playSynth === 'function' && window.isEngineOn) {
                    if(Math.random() > 0.5) playSynth('snare1', null); 
                }
            }

            class HazeParticle {
                constructor(startX, startY) {
                    this.x = startX;
                    this.y = startY;
                    
                    // Brownian motion setup
                    // Initial velocity pushes right from machine
                    this.vx = Math.random() * 2 + 1; 
                    this.vy = (Math.random() - 0.5) * 1.5;
                    
                    this.size = Math.random() * 20 + 10;
                    this.maxSize = this.size + 100; // Haze expands massively
                    
                    // Haze lasts a long time and stays faint
                    this.life = Math.random() * 0.4 + 0.1; // Max 50% opacity
                    this.decay = 0.001; 
                }
                update(w, h) {
                    // Random Brownian drift
                    this.vx += (Math.random() - 0.5) * 0.2;
                    this.vy += (Math.random() - 0.5) * 0.2;
                    
                    // Dampen velocity to simulate air resistance
                    this.vx *= 0.98;
                    this.vy *= 0.98;
                    
                    // Add slight right-drift representing generic HVAC air flow
                    this.vx += 0.05;

                    this.x += this.vx;
                    this.y += this.vy;

                    // Expand
                    if(this.size < this.maxSize) this.size += 0.5;

                    // Decay
                    this.life -= this.decay;
                }
                draw(ctx) {
                    if(this.life <= 0) return;
                    
                    const grad = ctx.createRadialGradient(this.x, this.y, 0, this.x, this.y, this.size);
                    grad.addColorStop(0, `rgba(200, 200, 220, ${this.life})`);
                    grad.addColorStop(1, 'rgba(200, 200, 220, 0)');
                    
                    ctx.fillStyle = grad;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size, 0, Math.PI*2);
                    ctx.fill();
                }
            }

            function animateHaze() {
                hzAnimFrame = requestAnimationFrame(animateHaze);
                if(!hzCtx) return;

                hzCtx.clearRect(0,0, hzCanvas.width, hzCanvas.height);

                // Add particles based on flow rate
                // Flow rate 0-100. Max 2 particles per frame.
                if(Math.random() * 100 < hazeFlowRate) {
                    // Machine is at left: 10%, top: 50%
                    const startX = hzCanvas.width * 0.1 + 15;
                    const startY = hzCanvas.height * 0.5;
                    hazeParticles.push(new HazeParticle(startX, startY));
                }

                // Update & Draw
                for(let i = hazeParticles.length - 1; i >= 0; i--) {
                    let p = hazeParticles[i];
                    p.update(hzCanvas.width, hzCanvas.height);
                    p.draw(hzCtx);
                    if(p.life <= 0) hazeParticles.splice(i, 1);
                }
                
                // Add a faint blue/cyan global wash to simulate ambient lighting hitting the haze
                if(hazeParticles.length > 10) {
                    const ambientAlpha = Math.min(0.2, hazeParticles.length * 0.001);
                    hzCtx.fillStyle = `rgba(0, 100, 255, ${ambientAlpha})`;
                    hzCtx.fillRect(0,0, hzCanvas.width, hzCanvas.height);
                }
            }
        </script>
        <style>
            .kinetic-wrapper {
                background: linear-gradient(180deg, #050505, #111);
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            }

            .kinetic-canvas-box {
                width: 100%;
                height: 250px;
                background: #020202;
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 40px rgba(0, 229, 255, 0.05);
            }
            #kineticCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Truss Bar at top */
            .kinetic-truss {
                position: absolute; top: 10px; left: 5%; right: 5%; height: 10px;
                background: repeating-linear-gradient(45deg, #222 0px, #222 5px, #111 5px, #111 10px);
                border: 1px solid #444; border-radius: 2px; z-index: 5;
            }

            .kinetic-controls {
                display: flex; flex-direction: column; gap: 15px; margin-top: 15px;
                background: #0a0a0f; padding: 15px; border-radius: 8px; border: 1px solid #1a1a24;
            }
            
            .k-btn-row { display: flex; gap: 10px; }
            .k-btn {
                flex: 1; padding: 10px 0; background: #000; border: 1px solid #333; border-radius: 6px;
                color: #888; font-family: var(--font-data); font-weight: bold; font-size: 10px; text-align: center;
                cursor: pointer; transition: 0.2s;
            }
            .k-btn.active { border-color: var(--cyan-neon); color: var(--cyan-neon); box-shadow: inset 0 0 10px rgba(0,229,255,0.2); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">KINETIC WINCH MATRIX</h2>
                <div class="section-icon"><i class="fas fa-arrows-alt-v"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Program the DMX motors to hoist the LED spheres in mathematically synchronized wave patterns.</p>

            <div class="kinetic-wrapper">
                <div class="kinetic-canvas-box" id="kinWrap">
                    <div class="kinetic-truss"></div>
                    <canvas id="kineticCanvas"></canvas>
                    <div style="position:absolute; bottom:5px; left:10px; font-family:var(--font-tech); font-size:8px; color:rgba(255,255,255,0.3);">FRONT ELEVATION VIEW</div>
                </div>

                <div class="kinetic-controls">
                    <div class="k-btn-row">
                        <div class="k-btn active" onclick="setKineticMode('sine', this)">SINE WAVE</div>
                        <div class="k-btn" onclick="setKineticMode('triangle', this)">TRIANGLE</div>
                        <div class="k-btn" onclick="setKineticMode('chaos', this)">SCATTER</div>
                    </div>
                    <div style="display:flex; justify-content:space-between; align-items:center;">
                        <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">MOTOR SPEED</span>
                        <input type="range" class="app-slider" id="kinSpeedSlider" min="1" max="20" value="5" style="width: 60%;">
                    </div>
                </div>
            </div>
        </div>

        <style>
            .holo-fan-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .fan-canvas-box {
                width: 100%;
                height: 280px;
                background: #050505;
                border: 2px solid #111;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                display: flex; justify-content: center; align-items: center;
                box-shadow: inset 0 0 30px rgba(0,0,0,0.9);
            }
            #holoFanCanvas { width: 100%; height: 100%; display: block; position: absolute; inset: 0; z-index: 2; mix-blend-mode: screen; }

            /* Hardware housing behind the fan */
            .fan-motor-housing {
                position: absolute; width: 40px; height: 40px; background: #111;
                border: 3px solid #333; border-radius: 50%; z-index: 1;
                box-shadow: 0 10px 20px rgba(0,0,0,0.8);
            }

            .holo-input-box {
                width: 100%; background: #0a0a0f; border: 1px solid var(--gold-primary);
                color: var(--gold-primary); font-family: var(--font-tech); font-size: 16px;
                padding: 12px; border-radius: 8px; text-align: center; outline: none; margin-top: 15px;
                text-transform: uppercase; box-shadow: inset 0 0 10px rgba(212,175,55,0.1);
            }
            .holo-input-box:focus { box-shadow: inset 0 0 20px rgba(212,175,55,0.3); }

            .fan-hud { display: flex; justify-content: space-between; margin-top: 15px; align-items: center; }
            .fh-val { font-family: var(--font-tech); font-size: 16px; color: var(--cyan-neon); font-weight: 900; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">POV HOLOGRAPHIC FAN</h2>
                <div class="section-icon"><i class="fas fa-fan"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Increase the mechanical RPM to trigger Persistence of Vision (POV) and materialize the text as a 3D hologram.</p>

            <div class="holo-fan-wrapper">
                <div class="fan-canvas-box" id="holoWrap">
                    <div class="fan-motor-housing"></div>
                    <canvas id="holoFanCanvas"></canvas>
                </div>

                <input type="text" class="holo-input-box" id="holoTextInput" value="MND SOUND" maxlength="12" oninput="updateHoloText()">

                <div class="fan-hud">
                    <span style="font-family:var(--font-data); font-size:10px; color:#888; font-weight:bold;">BLADE VELOCITY</span>
                    <span class="fh-val" id="fanRpmVal">0 RPM</span>
                </div>
                <input type="range" class="app-slider" id="fanRpmSlider" min="0" max="1500" value="0" step="10" style="margin-top: 5px;" oninput="updateFanRpm(this.value)">
            </div>
        </div>

        <style>
            .power-factor-wrapper {
                background: linear-gradient(135deg, #020202, #0a0a0f);
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .pf-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px; }
            .pf-stat { background: #000; border: 1px solid #1a1a24; border-radius: 8px; padding: 12px; text-align: center; position: relative; overflow: hidden; }
            
            .pf-val { font-family: var(--font-tech); font-size: 20px; font-weight: 900; display: block; position: relative; z-index: 2; }
            .pf-lbl { font-family: var(--font-data); font-size: 9px; color: #888; letter-spacing: 1px; position: relative; z-index: 2;}
            
            /* SVG Power Triangle Visualization */
            .pf-triangle-box {
                width: 100%; height: 140px; background: #050505; border: 1px dashed #333; border-radius: 8px;
                position: relative; display: flex; justify-content: center; align-items: center;
                box-shadow: inset 0 0 20px rgba(0,0,0,0.8); margin-bottom: 20px;
            }
            #pfSvg { width: 90%; height: 90%; overflow: visible; }
            
            .pf-line { stroke-width: 3; stroke-linecap: round; transition: all 0.3s ease-out; }
            .pf-text { font-family: var(--font-tech); font-size: 12px; font-weight: bold; fill: #fff; transition: all 0.3s ease-out;}

            .cap-bank-btn {
                width: 100%; padding: 15px; border-radius: 8px; background: rgba(0,255,0,0.1);
                border: 2px solid #00ff00; color: #00ff00; font-family: var(--font-tech);
                font-weight: 900; font-size: 14px; cursor: pointer; transition: 0.2s; box-shadow: 0 0 15px rgba(0,255,0,0.2);
            }
            .cap-bank-btn:active { background: #00ff00; color: #000; transform: scale(0.98); }
            
            .pf-warning { color: var(--red-alert) !important; animation: blink 0.5s infinite; text-shadow: 0 0 10px rgba(255,0,0,0.5); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">POWER FACTOR AI</h2>
                <div class="section-icon"><i class="fas fa-industry"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Monitor reactive power loss (kVAR). Heavy bass coils warp the AC phase. Drop below 0.80 PF and the generator risks a thermal shutdown.</p>

            <div class="power-factor-wrapper">
                <div class="pf-grid">
                    <div class="pf-stat">
                        <span class="pf-val" id="pfKwVal" style="color: #00ff00;">50.0</span>
                        <span class="pf-lbl">REAL POWER (kW)</span>
                    </div>
                    <div class="pf-stat">
                        <span class="pf-val" id="pfKvaVal" style="color: var(--cyan-neon);">50.0</span>
                        <span class="pf-lbl">APPARENT (kVA)</span>
                    </div>
                </div>

                <div class="pf-triangle-box">
                    <svg id="pfSvg" viewBox="0 0 200 100">
                        <line x1="20" y1="90" x2="180" y2="90" class="pf-line" stroke="#00ff00" id="svgLineKw"/>
                        <text x="100" y="105" text-anchor="middle" class="pf-text" fill="#00ff00">kW</text>
                        
                        <line x1="180" y1="90" x2="180" y2="90" class="pf-line" stroke="#ff3333" id="svgLineKvar"/>
                        <text x="195" y="50" text-anchor="middle" class="pf-text" fill="#ff3333" id="svgTextKvar">kVAR</text>
                        
                        <line x1="20" y1="90" x2="180" y2="90" class="pf-line" stroke="#00e5ff" id="svgLineKva"/>
                        <text x="90" y="40" text-anchor="middle" class="pf-text" fill="#00e5ff" id="svgTextKva">kVA</text>
                        
                        <path d="M 50 90 A 30 30 0 0 0 45 80" fill="none" stroke="var(--gold-primary)" stroke-width="2" id="svgArcPf"/>
                    </svg>
                </div>

                <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">
                    <span style="font-family:var(--font-data); font-size:10px; color:#888; font-weight:bold;">POWER FACTOR (cos θ)</span>
                    <span id="pfRatioVal" style="font-family:var(--font-tech); font-size:18px; color:#00ff00; font-weight:bold;">1.00</span>
                </div>
                
                <span style="font-family:var(--font-tech); font-size:8px; color:#555;">INDUCTIVE LOAD INTENSITY (SUBWOOFERS)</span>
                <input type="range" class="app-slider" id="inductiveLoadSlider" min="0" max="100" value="0" style="margin-bottom: 20px;" oninput="updatePowerFactor()">

                <button class="cap-bank-btn" id="btnCapBank" onclick="engageCapacitorBank()">
                    <i class="fas fa-car-battery"></i> ENGAGE CAPACITOR BANK
                </button>
            </div>
        </div>

        <script>
            // --- 1. DMX KINETIC WINCH ARRAY LOGIC ---
            const knCanvas = document.getElementById('kineticCanvas');
            let knCtx = null;
            const knWrap = document.getElementById('kinWrap');
            
            let knAnimFrame = null;
            let kinTime = 0;
            let kinMode = 'sine'; // sine, triangle, chaos
            let kinSpeed = 0.05;

            const NUM_WINCHES = 12;

            function initKineticEngine() {
                if(!knWrap || !knCanvas) return;
                knCanvas.width = knWrap.clientWidth;
                knCanvas.height = knWrap.clientHeight;
                knCtx = knCanvas.getContext('2d');
                if(!knAnimFrame) animateKineticWinches();
            }
            window.addEventListener('resize', initKineticEngine);
            setTimeout(initKineticEngine, 500);

            function setKineticMode(mode, el) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(15);
                kinMode = mode;
                document.querySelectorAll('.k-btn').forEach(b => b.classList.remove('active'));
                el.classList.add('active');
            }

            // Sync slider to speed
            document.getElementById('kinSpeedSlider').addEventListener('input', function() {
                // Map slider 1-20 to 0.01 - 0.20
                kinSpeed = parseInt(this.value) * 0.01;
            });

            function animateKineticWinches() {
                knAnimFrame = requestAnimationFrame(animateKineticWinches);
                if(!knCtx) return;

                knCtx.clearRect(0,0, knCanvas.width, knCanvas.height);
                kinTime += kinSpeed;

                const w = knCanvas.width;
                const h = knCanvas.height;
                const topY = 15; // Bottom of the CSS truss
                const maxDrop = h - 40; // Max cable length
                
                // Calculate spacing
                // Start 10% in, end 90% in
                const startX = w * 0.1;
                const endX = w * 0.9;
                const stepX = (endX - startX) / (NUM_WINCHES - 1);

                for(let i=0; i<NUM_WINCHES; i++) {
                    const x = startX + (i * stepX);
                    let targetY = 0;

                    // Math Logic for Wave Patterns
                    if(kinMode === 'sine') {
                        // Classic sine wave offset by index
                        const wave = Math.sin(kinTime + (i * 0.5)); // -1 to 1
                        // Normalize to 0 to 1, then multiply by maxDrop
                        targetY = topY + ((wave + 1) / 2) * maxDrop;
                    } 
                    else if (kinMode === 'triangle') {
                        // Triangle wave logic using modulo and abs
                        const period = Math.PI * 2;
                        const phase = (kinTime + (i * 0.5)) % period;
                        // Map phase to a sharp V shape
                        let val = Math.abs((phase / Math.PI) - 1); // 0 to 1 to 0
                        targetY = topY + val * maxDrop;
                    } 
                    else if (kinMode === 'chaos') {
                        // Pseudo-random but smooth using Perlin-like stacked sines
                        let noise = Math.sin(kinTime * 1.5 + i * 1.2) * Math.cos(kinTime * 0.8 + i * 3.3);
                        targetY = topY + ((noise + 1) / 2) * maxDrop;
                    }

                    // 1. Draw the DMX Cable (Wire)
                    knCtx.beginPath();
                    knCtx.moveTo(x, topY);
                    knCtx.lineTo(x, targetY);
                    knCtx.strokeStyle = '#555';
                    knCtx.lineWidth = 1;
                    knCtx.stroke();

                    // 2. Draw the Glowing LED Sphere
                    // Get primary color from CSS root
                    const rootStyle = getComputedStyle(document.documentElement);
                    const glowColor = rootStyle.getPropertyValue('--cyan-neon').trim() || '#00e5ff';

                    knCtx.globalCompositeOperation = 'screen';
                    knCtx.beginPath();
                    knCtx.arc(x, targetY, 8, 0, Math.PI*2);
                    knCtx.fillStyle = '#fff';
                    knCtx.shadowBlur = 15;
                    knCtx.shadowColor = glowColor;
                    knCtx.fill();
                    
                    // Inner colored core
                    knCtx.beginPath();
                    knCtx.arc(x, targetY, 4, 0, Math.PI*2);
                    knCtx.fillStyle = glowColor;
                    knCtx.fill();
                    
                    knCtx.shadowBlur = 0;
                    knCtx.globalCompositeOperation = 'source-over';
                }
            }


            // --- 2. 3D HOLOGRAPHIC LED FAN SIMULATOR (POV) LOGIC ---
            const hfCanvas = document.getElementById('holoFanCanvas');
            let hfCtx = null;
            const hfWrap = document.getElementById('holoWrap');
            
            let hfAnimFrame = null;
            let fanRotation = 0;
            let fanRpm = 0;
            let displayString = "MND SOUND";

            function initHoloFan() {
                if(!hfWrap || !hfCanvas) return;
                hfCanvas.width = hfWrap.clientWidth;
                hfCanvas.height = hfWrap.clientHeight;
                hfCtx = hfCanvas.getContext('2d');
                if(!hfAnimFrame) animateHoloFan();
            }
            window.addEventListener('resize', initHoloFan);
            setTimeout(initHoloFan, 800);

            function updateHoloText() {
                displayString = document.getElementById('holoTextInput').value.toUpperCase();
            }

            function updateFanRpm(val) {
                fanRpm = parseInt(val);
                document.getElementById('fanRpmVal').innerText = `${fanRpm} RPM`;
                
                // Color mapping based on speed
                const valEl = document.getElementById('fanRpmVal');
                if(fanRpm > 1000) valEl.style.color = "var(--red-alert)";
                else if(fanRpm > 500) valEl.style.color = "var(--gold-primary)";
                else valEl.style.color = "var(--cyan-neon)";
                
                if(fanRpm > 1200 && navigator.vibrate) navigator.vibrate(10); // rumble
            }

            function animateHoloFan() {
                hfAnimFrame = requestAnimationFrame(animateHoloFan);
                if(!hfCtx) return;

                const w = hfCanvas.width;
                const h = hfCanvas.height;
                const cx = w / 2;
                const cy = h / 2;

                // Physics: RPM to Radians per frame (approximate for visual)
                // 1 RPM = 360 deg / 60 sec = 6 deg/sec. 
                // At 60fps, speed per frame = fanRpm * factor
                const speedPerFrame = (fanRpm / 60) * 0.1; 
                fanRotation += speedPerFrame;

                // Persistence of Vision Engine:
                // High RPM = clean text, no blade visible.
                // Low RPM = visible spinning blade, broken text.
                
                // Clear background based on RPM (Slow = fast clear, Fast = slow clear/trail)
                let fadeAlpha = 0.5; // Default fast clear
                if(fanRpm > 500) fadeAlpha = 0.15; // Starts trailing
                if(fanRpm > 1000) fadeAlpha = 0.05; // Full hologram persistence
                
                hfCtx.fillStyle = `rgba(5, 5, 5, ${fadeAlpha})`;
                hfCtx.fillRect(0,0, w, h);

                // --- Draw the actual target hologram text ---
                // We draw it to a temporary layout to mask it
                hfCtx.save();
                
                // Set text styling
                hfCtx.textAlign = 'center';
                hfCtx.textBaseline = 'middle';
                hfCtx.font = `900 ${Math.min(w*0.12, 40)}px "Orbitron", sans-serif`;
                
                // Color shifts slightly based on rotation for iridescent effect
                const hue = (fanRotation * 50) % 360;
                hfCtx.fillStyle = `hsl(${hue}, 100%, 60%)`;
                hfCtx.shadowBlur = 15;
                hfCtx.shadowColor = hfCtx.fillStyle;

                // The Magic Masking:
                // If RPM is low, we ONLY draw the text where the blade currently is using a clipping path
                if(fanRpm < 800) {
                    hfCtx.beginPath();
                    hfCtx.moveTo(cx, cy);
                    // Draw a wedge representing the LED blade
                    // The width of the wedge increases with RPM
                    const wedgeSize = 0.1 + (fanRpm/800) * Math.PI; 
                    hfCtx.arc(cx, cy, w, fanRotation, fanRotation + wedgeSize);
                    hfCtx.lineTo(cx, cy);
                    
                    // Also draw the opposite blade (it's a 2-blade fan)
                    hfCtx.moveTo(cx, cy);
                    hfCtx.arc(cx, cy, w, fanRotation + Math.PI, fanRotation + Math.PI + wedgeSize);
                    hfCtx.lineTo(cx, cy);
                    
                    hfCtx.clip(); // Mask the text!
                }
                
                // If RPM is very low, the text barely renders. If high, it renders fully.
                if(fanRpm > 50) {
                    hfCtx.fillText(displayString, cx, cy);
                }
                
                hfCtx.restore(); // Remove clipping mask

                // --- Draw the physical hardware blade ---
                // Fades out as RPM goes up (motion blur rendering it invisible)
                const bladeAlpha = Math.max(0.05, 1.0 - (fanRpm / 500));
                
                hfCtx.save();
                hfCtx.translate(cx, cy);
                hfCtx.rotate(fanRotation);
                
                hfCtx.fillStyle = `rgba(20, 20, 20, ${bladeAlpha})`;
                hfCtx.strokeStyle = `rgba(100, 100, 100, ${bladeAlpha})`;
                hfCtx.lineWidth = 2;
                
                // Blade 1
                hfCtx.beginPath(); hfCtx.roundRect(15, -6, 120, 12, 6); hfCtx.fill(); hfCtx.stroke();
                // Blade 2
                hfCtx.beginPath(); hfCtx.roundRect(-135, -6, 120, 12, 6); hfCtx.fill(); hfCtx.stroke();
                
                hfCtx.restore();
            }


            // --- 3. INDUSTRIAL POWER FACTOR (PF) LOGIC ---
            let currentKw = 50.0; // Base constant load

            function updatePowerFactor() {
                const indLoad = parseInt(document.getElementById('inductiveLoadSlider').value); // 0 to 100
                
                // Math: Inductive load creates Reactive Power (kVAR)
                // If slider is 0, kVAR is 0. PF = 1.0.
                // If slider is 100, kVAR is massive (e.g. 40 kVAR).
                
                const kvar = (indLoad / 100) * 45; // Max 45 kVAR
                
                // Apparent Power (kVA) = sqrt(kW^2 + kVAR^2)
                const kva = Math.sqrt(Math.pow(currentKw, 2) + Math.pow(kvar, 2));
                
                // Power Factor = kW / kVA
                const pf = currentKw / kva;

                // Update DOM text
                document.getElementById('pfKvaVal').innerText = kva.toFixed(1);
                
                const pfEl = document.getElementById('pfRatioVal');
                pfEl.innerText = pf.toFixed(2);

                // Warning states
                const statBox = pfEl.parentElement;
                const kvaValText = document.getElementById('pfKvaVal');
                
                if(pf < 0.80) {
                    pfEl.className = 'pf-warning';
                    kvaValText.className = 'pf-val pf-warning';
                    if(navigator.vibrate) navigator.vibrate(10);
                } else if(pf < 0.90) {
                    pfEl.className = '';
                    pfEl.style.color = 'var(--gold-primary)';
                    kvaValText.className = 'pf-val';
                    kvaValText.style.color = 'var(--gold-primary)';
                } else {
                    pfEl.className = '';
                    pfEl.style.color = '#00ff00';
                    kvaValText.className = 'pf-val';
                    kvaValText.style.color = 'var(--cyan-neon)';
                }

                updatePFSvg(currentKw, kvar, kva, pf);
            }

            function updatePFSvg(kw, kvar, kva, pf) {
                // SVG canvas is 200w x 100h.
                // Base line (kW) is fixed length horizontally: x1=20, y1=90, x2=180, y2=90. Length = 160px.
                const baseLength = 160; 
                
                // Map physical pixels to our electrical values
                // scale = 160px / 50kW
                const scale = baseLength / kw; 
                
                // Calculate height of the triangle based on kVAR
                const heightPx = kvar * scale;
                
                // The right angle is at (180, 90). The top point goes UP (subtract Y).
                const topY = 90 - heightPx;

                // Update SVG elements
                const lineKvar = document.getElementById('svgLineKvar');
                lineKvar.setAttribute('y2', topY); // Draw line up
                
                const txtKvar = document.getElementById('svgTextKvar');
                txtKvar.setAttribute('y', topY + (heightPx/2)); // Center text

                const lineKva = document.getElementById('svgLineKva');
                lineKva.setAttribute('y2', topY); // Connect hypotenuse
                
                const txtKva = document.getElementById('svgTextKva');
                // Place text roughly in middle of hypotenuse
                txtKva.setAttribute('x', 20 + (160/2) - 15);
                txtKva.setAttribute('y', 90 - (heightPx/2) - 10);

                // Calculate angle for the arc
                // θ = acos(PF). Draw arc at bottom left corner (20, 90)
                const arcNode = document.getElementById('svgArcPf');
                if(pf >= 0.99) {
                    arcNode.setAttribute('d', ''); // Hide if basically flat
                } else {
                    // Radius of arc = 30
                    const arcR = 30;
                    // Angle in radians
                    const angleRad = Math.acos(pf);
                    // Calculate endpoint of arc on the hypotenuse
                    const ex = 20 + arcR * Math.cos(angleRad);
                    const ey = 90 - arcR * Math.sin(angleRad);
                    
                    // SVG Path: M startX startY A rx ry x-axis-rotation large-arc-flag sweep-flag endX endY
                    arcNode.setAttribute('d', `M ${20 + arcR} 90 A ${arcR} ${arcR} 0 0 0 ${ex} ${ey}`);
                }
            }

            function engageCapacitorBank() {
                const slider = document.getElementById('inductiveLoadSlider');
                if(slider.value > 0) {
                    if(typeof playTap === 'function') playTap();
                    if(navigator.vibrate) navigator.vibrate([100, 50, 100]);
                    
                    // Visually animate slider back to 0
                    let val = parseInt(slider.value);
                    const drainInterval = setInterval(() => {
                        val -= 5;
                        if(val <= 0) {
                            val = 0;
                            clearInterval(drainInterval);
                            if(typeof triggerToast === 'function') triggerToast("Capacitor Banks Engaged. PF Corrected to Unity.");
                        }
                        slider.value = val;
                        updatePowerFactor();
                    }, 20);
                }
            }

            // Init
            setTimeout(updatePowerFactor, 500);
        </script>
        <style>
            .lidar-wrapper {
                background: #020202;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
            }

            .lidar-canvas-box {
                width: 100%;
                height: 250px;
                background: radial-gradient(circle at center, #05101a 0%, #000 100%);
                border: 2px solid var(--cyan-neon);
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                box-shadow: inset 0 0 40px rgba(0, 229, 255, 0.1);
            }
            #lidarCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .lidar-hud {
                position: absolute; top: 10px; left: 10px; pointer-events: none; z-index: 5;
            }
            .lidar-title { font-family: var(--font-tech); font-size: 10px; font-weight: 900; color: var(--cyan-neon); letter-spacing: 2px; }
            .lidar-sub { font-family: var(--font-data); font-size: 8px; color: #fff; margin-top: 2px; display: block;}

            .lidar-controls {
                display: flex; gap: 10px; margin-top: 15px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">LIDAR VENUE SCANNER</h2>
                <div class="section-icon"><i class="fas fa-satellite"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate aerial photogrammetry. Scan the physical venue topography to ensure level ground before erecting heavy truss structures.</p>

            <div class="lidar-wrapper">
                <div class="lidar-canvas-box" id="lidarWrap">
                    <div class="lidar-hud">
                        <span class="lidar-title">TOPOLOGICAL RENDER</span>
                        <span class="lidar-sub" id="lidarProgressTxt">SCAN PROGRESS: 0%</span>
                    </div>
                    <canvas id="lidarCanvas"></canvas>
                </div>

                <div class="lidar-controls">
                    <button class="app-btn-outline" style="flex: 1; border-color: var(--cyan-neon); color: var(--cyan-neon);" onclick="initiateLidarScan()">
                        <i class="fas fa-radar"></i> INITIATE SCAN
                    </button>
                    <button class="app-btn-outline" style="flex: 1; border-color: var(--red-alert); color: var(--red-alert);" onclick="clearLidarData()">
                        <i class="fas fa-eraser"></i> WIPE DATA
                    </button>
                </div>
            </div>
        </div>

        <style>
            .cymatics-wrapper {
                background: #000;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            }

            .cymatics-display {
                width: 100%;
                height: 280px;
                background: #050505;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
                border: 1px solid #1a1a1a;
                box-shadow: inset 0 0 50px rgba(212,175,55,0.05);
            }
            #cymaticsCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            .cymatic-plate {
                position: absolute; inset: 10%; border-radius: 50%; border: 1px dashed rgba(212,175,55,0.2);
                pointer-events: none; z-index: 1;
            }

            .cy-hud {
                display: flex; justify-content: space-between; align-items: center; margin-top: 15px;
                background: #0a0a0f; padding: 12px; border-radius: 6px; border: 1px solid #111;
            }
            
            .freq-btn-row { display: flex; gap: 10px; margin-top: 15px; }
            .freq-btn {
                flex: 1; background: #111; border: 1px solid #333; color: #888; border-radius: 6px;
                padding: 10px 0; text-align: center; font-family: var(--font-tech); font-weight: bold; font-size: 12px;
                cursor: pointer; transition: 0.2s;
            }
            .freq-btn.active { background: rgba(212,175,55,0.1); border-color: var(--gold-primary); color: var(--gold-primary); box-shadow: 0 0 10px rgba(212,175,55,0.3); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">CYMATIC RESONANCE AI</h2>
                <div class="section-icon"><i class="fas fa-atom"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Visualize physical sound geometry. The Chladni equations force particles into symmetrical nodes based on the applied bass frequency.</p>

            <div class="cymatics-wrapper">
                <div class="cymatics-display" id="cyWrap">
                    <canvas id="cymaticsCanvas"></canvas>
                    <div class="cymatic-plate"></div>
                    <div style="position:absolute; top:10px; right:10px; font-family:var(--font-tech); font-size:9px; color:var(--gold-primary); text-shadow: 0 0 5px var(--gold-primary);">CHLADNI PLATE SIMULATOR</div>
                </div>

                <div class="cy-hud">
                    <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">RESONANCE FREQUENCY</span>
                    <span id="cyFreqDisplay" style="font-family:var(--font-tech); font-size:16px; color:#fff; font-weight:bold;">432 Hz</span>
                </div>

                <div class="freq-btn-row">
                    <div class="freq-btn" onclick="setCymaticFreq(1, this)">72 Hz</div>
                    <div class="freq-btn active" onclick="setCymaticFreq(2, this)">432 Hz</div>
                    <div class="freq-btn" onclick="setCymaticFreq(3, this)">528 Hz</div>
                    <div class="freq-btn" onclick="setCymaticFreq(4, this)">864 Hz</div>
                </div>
            </div>
        </div>

        <style>
            .xmax-wrapper {
                background: linear-gradient(180deg, #111, #000);
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .xmax-display {
                width: 100%;
                height: 200px;
                background: #050508;
                border-radius: 8px;
                border: 1px solid #1a1a24;
                position: relative;
                display: flex; justify-content: center; align-items: center;
                overflow: hidden; margin-bottom: 15px;
            }

            /* SVG Speaker Cone Side-Profile */
            #speakerSvg { width: 80%; height: 100%; overflow: visible; }
            .cone-path { fill: #222; stroke: #555; stroke-width: 2; transition: d 0.05s linear; }
            .dust-cap { fill: #111; stroke: #444; stroke-width: 2; transition: transform 0.05s linear; }
            .voice-coil { fill: #ff9900; transition: fill 0.2s, transform 0.05s linear; }
            .magnet { fill: #333; stroke: #111; stroke-width: 3; }

            .xmax-status-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 15px; }
            .xm-card { background: rgba(0,0,0,0.5); border: 1px solid #222; border-radius: 6px; padding: 10px; text-align: center; }
            .xm-lbl { font-family: var(--font-data); font-size: 9px; color: #888; font-weight: bold; }
            .xm-val { font-family: var(--font-tech); font-size: 16px; font-weight: 900; color: #fff; margin-top: 5px; display: block; }
            
            .xmax-warning { color: var(--red-alert) !important; text-shadow: 0 0 10px rgba(255,51,51,0.8); animation: blink 0.2s infinite; }
            .coil-melt { fill: var(--red-alert) !important; filter: drop-shadow(0 0 10px var(--red-alert)); }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">VOICE COIL EXCURSION</h2>
                <div class="section-icon"><i class="fas fa-bullseye"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Monitor mechanical limits (Xmax). Pushing extreme watts causes the voice coil to exit the magnetic gap and physically melt.</p>

            <div class="xmax-wrapper">
                <div class="xmax-display">
                    <svg id="speakerSvg" viewBox="0 0 200 100">
                        <rect x="20" y="20" width="40" height="60" class="magnet"/>
                        <rect x="180" y="5" width="10" height="10" fill="#444"/>
                        <rect x="180" y="85" width="10" height="10" fill="#444"/>
                        <g id="movingAssembly">
                            <rect x="40" y="35" width="30" height="30" class="voice-coil" id="vCoilGlow"/>
                            <path d="M 70 35 L 180 15 L 180 85 L 70 65 Z" class="cone-path" id="coneMorph"/>
                            <ellipse cx="75" cy="50" rx="10" ry="20" class="dust-cap"/>
                        </g>
                    </svg>
                    <div style="position:absolute; top:10px; right:10px; color:#555; font-family:var(--font-tech); font-size:8px;">CROSS-SECTION VIEW</div>
                </div>

                <div class="xmax-status-grid">
                    <div class="xm-card">
                        <span class="xm-lbl">APPLIED POWER</span>
                        <span class="xm-val" id="xmaxWattVal" style="color:var(--cyan-neon);">0 W</span>
                    </div>
                    <div class="xm-card">
                        <span class="xm-lbl">CONE DISPLACEMENT</span>
                        <span class="xm-val" id="xmaxDispVal" style="color:#00ff00;">0.0 mm</span>
                    </div>
                </div>

                <div style="display:flex; flex-direction:column; align-items:center;">
                    <span style="font-family:var(--font-data); font-size:10px; color:#fff; font-weight:bold; margin-bottom:10px;">AMPLIFIER OUTPUT</span>
                    <input type="range" class="app-slider" id="wattSlider" min="0" max="4000" value="0" step="50" style="width: 100%;" oninput="updateExcursion(this.value)">
                </div>
            </div>
        </div>

        <script>
            // --- 1. LIDAR VENUE TOPOGRAPHY SCANNER LOGIC ---
            const lCanvas = document.getElementById('lidarCanvas');
            let lCtx = null;
            const lWrap = document.getElementById('lidarWrap');
            
            let lAnimFrame = null;
            let lidarGrid = [];
            let scanLineZ = -100; // Z-axis scanner position
            let isScanningLidar = false;
            
            const lCols = 25;
            const lRows = 25;
            const lSpacing = 20;

            function initLidar() {
                if(!lWrap || !lCanvas) return;
                lCanvas.width = lWrap.clientWidth;
                lCanvas.height = lWrap.clientHeight;
                lCtx = lCanvas.getContext('2d');
                generateLidarTerrain();
                drawLidarStatic(); // Draw initial dark state
            }
            window.addEventListener('resize', initLidar);
            setTimeout(initLidar, 500);

            function generateLidarTerrain() {
                lidarGrid = [];
                // Create a 2D array of heights
                for(let z=0; z<lRows; z++) {
                    let row = [];
                    for(let x=0; x<lCols; x++) {
                        // Generate bumpy terrain. The edges are flat, center has hills.
                        let distanceToCenter = Math.hypot(x - lCols/2, z - lRows/2);
                        let height = 0;
                        if(distanceToCenter < 10) {
                            height = Math.random() * 40; // High variance in center
                        } else {
                            height = Math.random() * 5;  // Flat on edges
                        }
                        
                        // Object holds physical X, Y(height), Z, and whether it has been "scanned"
                        row.push({
                            x: (x * lSpacing) - ((lCols * lSpacing)/2),
                            y: height,
                            z: (z * lSpacing),
                            scanned: false
                        });
                    }
                    lidarGrid.push(row);
                }
            }

            function clearLidarData() {
                if(typeof playTap === 'function') playTap();
                isScanningLidar = false;
                if(lAnimFrame) { cancelAnimationFrame(lAnimFrame); lAnimFrame = null; }
                generateLidarTerrain();
                scanLineZ = -100;
                document.getElementById('lidarProgressTxt').innerText = "SCAN PROGRESS: 0%";
                document.getElementById('lidarProgressTxt').style.color = "#fff";
                drawLidarStatic();
            }

            function initiateLidarScan() {
                if(isScanningLidar) return;
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(20);
                
                isScanningLidar = true;
                scanLineZ = 0; // Reset scanner to front
                if(!lAnimFrame) animateLidar();
            }

            // Simple 3D to 2D projection
            function projectLidar(x, y, z) {
                const focal = 300;
                const camZ = -200;
                // Offset Y to push it down the screen
                const camY = -100; 
                
                const depth = z - camZ;
                const scale = depth > 0 ? focal / depth : 0;
                
                const px = (lCanvas.width / 2) + (x * scale);
                const py = (lCanvas.height / 2) + ((camY - y) * scale);
                return {px, py};
            }

            function drawLidarStatic() {
                if(!lCtx) return;
                lCtx.clearRect(0,0, lCanvas.width, lCanvas.height);
                
                // Draw just faint dots for unscanned terrain
                lCtx.fillStyle = 'rgba(0, 229, 255, 0.1)';
                for(let z=0; z<lRows; z++) {
                    for(let x=0; x<lCols; x++) {
                        const pt = lidarGrid[z][x];
                        const proj = projectLidar(pt.x, 0, pt.z); // Draw flat initially
                        lCtx.fillRect(proj.px, proj.py, 1, 1);
                    }
                }
            }

            function animateLidar() {
                if(!isScanningLidar) return;
                lAnimFrame = requestAnimationFrame(animateLidar);
                
                lCtx.clearRect(0,0, lCanvas.width, lCanvas.height);
                
                scanLineZ += 2.5; // Scanner speed moving away into Z depth
                
                // Calculate progress
                const maxZ = lRows * lSpacing;
                let pct = (scanLineZ / maxZ) * 100;
                if(pct > 100) pct = 100;
                
                const progTxt = document.getElementById('lidarProgressTxt');
                progTxt.innerText = `SCAN PROGRESS: ${Math.floor(pct)}%`;

                if(scanLineZ > maxZ + 50) {
                    isScanningLidar = false;
                    progTxt.innerText = `TERRAIN MAPPED. READY FOR DEPLOYMENT.`;
                    progTxt.style.color = "#00ff00";
                    if(navigator.vibrate) navigator.vibrate([30, 30, 30]);
                    // Don't clear, leave the final state drawn
                }

                // Draw Grid
                for(let z=0; z<lRows; z++) {
                    for(let x=0; x<lCols; x++) {
                        const pt = lidarGrid[z][x];
                        
                        // If scanner line has passed this point, mark as scanned
                        if(pt.z <= scanLineZ) pt.scanned = true;

                        // Use actual Y height if scanned, otherwise flat 0
                        const renderY = pt.scanned ? pt.y : 0;
                        const proj = projectLidar(pt.x, renderY, pt.z);

                        // Draw Points
                        if(pt.scanned) {
                            // Color mapping based on height
                            if(pt.y > 20) lCtx.fillStyle = 'var(--red-alert)';
                            else if(pt.y > 10) lCtx.fillStyle = 'var(--gold-primary)';
                            else lCtx.fillStyle = 'var(--cyan-neon)';
                            
                            lCtx.fillRect(proj.px - 1, proj.py - 1, 2, 2);
                            
                            // Connect lines to the left
                            if(x > 0) {
                                const leftPt = lidarGrid[z][x-1];
                                if(leftPt.scanned) {
                                    const leftProj = projectLidar(leftPt.x, leftPt.y, leftPt.z);
                                    lCtx.beginPath();
                                    lCtx.moveTo(proj.px, proj.py);
                                    lCtx.lineTo(leftProj.px, leftProj.py);
                                    lCtx.strokeStyle = 'rgba(0, 229, 255, 0.2)';
                                    lCtx.stroke();
                                }
                            }
                        } else {
                            lCtx.fillStyle = 'rgba(0, 229, 255, 0.1)';
                            lCtx.fillRect(proj.px, proj.py, 1, 1);
                        }
                    }
                }

                // Draw the sweeping scanner laser line
                if(isScanningLidar) {
                    // Find the canvas X coordinates for the edges of the grid at the current scanLineZ
                    const leftEdgeProj = projectLidar(- (lCols * lSpacing)/2, 0, scanLineZ);
                    const rightEdgeProj = projectLidar(  (lCols * lSpacing)/2, 0, scanLineZ);
                    
                    lCtx.beginPath();
                    lCtx.moveTo(leftEdgeProj.px - 50, leftEdgeProj.py);
                    lCtx.lineTo(rightEdgeProj.px + 50, rightEdgeProj.py);
                    lCtx.strokeStyle = 'rgba(0, 255, 0, 0.8)';
                    lCtx.lineWidth = 2;
                    lCtx.shadowBlur = 15;
                    lCtx.shadowColor = '#00ff00';
                    lCtx.stroke();
                    lCtx.shadowBlur = 0; // reset
                }
            }


            // --- 2. CYMATIC RESONANCE MATRIX LOGIC ---
            const cyCanvas = document.getElementById('cymaticsCanvas');
            let cyCtx = null;
            const cyWrap = document.getElementById('cyWrap');
            
            let cyAnimFrame = null;
            let cyParticles = [];
            const CY_PARTICLE_COUNT = 1500;
            let currentChladniPattern = 2; // 1, 2, 3, 4
            let cyTime = 0;

            function initCymatics() {
                if(!cyWrap || !cyCanvas) return;
                cyCanvas.width = cyWrap.clientWidth;
                cyCanvas.height = cyWrap.clientHeight;
                cyCtx = cyCanvas.getContext('2d');
                
                // Spawn random particles inside a circle
                const cx = cyCanvas.width / 2;
                const cy = cyCanvas.height / 2;
                const radius = Math.min(cx, cy) * 0.8;

                for(let i=0; i<CY_PARTICLE_COUNT; i++) {
                    // Random point in circle
                    const angle = Math.random() * Math.PI * 2;
                    const r = Math.sqrt(Math.random()) * radius;
                    cyParticles.push({
                        x: cx + Math.cos(angle) * r,
                        y: cy + Math.sin(angle) * r,
                        vx: 0, vy: 0
                    });
                }
                
                if(!cyAnimFrame) animateCymatics();
            }
            window.addEventListener('resize', initCymatics);
            setTimeout(initCymatics, 800);

            function setCymaticFreq(patternId, btnEl) {
                if(typeof playTap === 'function') playTap();
                if(navigator.vibrate) navigator.vibrate(10);
                
                document.querySelectorAll('.freq-btn').forEach(b => b.classList.remove('active'));
                btnEl.classList.add('active');
                
                currentChladniPattern = patternId;
                document.getElementById('cyFreqDisplay').innerText = btnEl.innerText;
                
                // Add a shockwave physical scatter when frequency changes
                const cx = cyCanvas.width / 2;
                const cy = cyCanvas.height / 2;
                cyParticles.forEach(p => {
                    const angle = Math.atan2(p.y - cy, p.x - cx);
                    const force = Math.random() * 15 + 5;
                    p.vx += Math.cos(angle) * force;
                    p.vy += Math.sin(angle) * force;
                });
            }

            function getChladniForce(x, y, pattern) {
                // Normalize coordinates -1 to 1 based on canvas center
                const w = cyCanvas.width;
                const h = cyCanvas.height;
                const nx = (x - w/2) / (w/2);
                const ny = (y - h/2) / (h/2);
                
                // Math: Chladni plate equations
                // Chladni(x,y) = cos(n * pi * x) * cos(m * pi * y) - cos(m * pi * x) * cos(n * pi * y)
                // Different combinations of n and m yield different geometric mandalas.
                let n=1, m=1;
                if(pattern === 1) { n=2; m=3; }
                if(pattern === 2) { n=3; m=4; }
                if(pattern === 3) { n=4; m=5; }
                if(pattern === 4) { n=5; m=2; }

                const val = Math.cos(n * Math.PI * nx) * Math.cos(m * Math.PI * ny) - Math.cos(m * Math.PI * nx) * Math.cos(n * Math.PI * ny);
                
                // Return gradient vector (approximate derivative) to push particles towards nodes (where val == 0)
                const eps = 0.01;
                const valX = Math.cos(n * Math.PI * (nx+eps)) * Math.cos(m * Math.PI * ny) - Math.cos(m * Math.PI * (nx+eps)) * Math.cos(n * Math.PI * ny);
                const valY = Math.cos(n * Math.PI * nx) * Math.cos(m * Math.PI * (ny+eps)) - Math.cos(m * Math.PI * nx) * Math.cos(n * Math.PI * (ny+eps));
                
                const dX = (valX - val) / eps;
                const dY = (valY - val) / eps;
                
                // If val is positive, gradient points away from 0. We want to move TOWARDS 0.
                // So we multiply by -val to push towards the zero-lines.
                return { 
                    fx: -dX * val * 0.05, 
                    fy: -dY * val * 0.05 
                };
            }

            function animateCymatics() {
                cyAnimFrame = requestAnimationFrame(animateCymatics);
                if(!cyCtx) return;

                // Motion trail
                cyCtx.fillStyle = 'rgba(0, 0, 0, 0.2)';
                cyCtx.fillRect(0,0, cyCanvas.width, cyCanvas.height);

                const cx = cyCanvas.width / 2;
                const cy = cyCanvas.height / 2;
                const radius = Math.min(cx, cy) * 0.85;

                cyCtx.fillStyle = 'var(--gold-primary)';

                cyParticles.forEach(p => {
                    // Apply resonant force
                    const force = getChladniForce(p.x, p.y, currentChladniPattern);
                    p.vx += force.fx;
                    p.vy += force.fy;
                    
                    // Add micro-vibration noise
                    p.vx += (Math.random() - 0.5) * 0.5;
                    p.vy += (Math.random() - 0.5) * 0.5;

                    // Friction
                    p.vx *= 0.85;
                    p.vy *= 0.85;

                    p.x += p.vx;
                    p.y += p.vy;

                    // Circular boundary containment
                    const distFromCenter = Math.hypot(p.x - cx, p.y - cy);
                    if(distFromCenter > radius) {
                        const angle = Math.atan2(p.y - cy, p.x - cx);
                        p.x = cx + Math.cos(angle) * radius;
                        p.y = cy + Math.sin(angle) * radius;
                        p.vx *= -0.5;
                        p.vy *= -0.5;
                    }

                    // Draw
                    cyCtx.fillRect(p.x, p.y, 1.5, 1.5);
                });
            }


            // --- 3. VOICE COIL EXCURSION (XMAX) LOGIC ---
            let xmAnimFrame = null;
            let xmTime = 0;
            let xmWatts = 0; // 0 to 4000
            
            const XMAX_SAFE = 2500; // Safe wattage limit
            const XMECH_LIMIT = 3500; // Physical destruction limit

            function updateExcursion(val) {
                xmWatts = parseInt(val);
                document.getElementById('xmaxWattVal').innerText = `${xmWatts} W`;
                
                // Audio Engine Link: Modulate volume of the sine wave generator if active
                if(typeof masterGain !== 'undefined' && typeof isEngineOn !== 'undefined' && isEngineOn) {
                    masterGain.gain.value = xmWatts / 4000;
                }
                
                if(!xmAnimFrame && xmWatts > 0) animateExcursion();
            }

            function animateExcursion() {
                // Stop loop if slider goes to 0
                if(xmWatts === 0) {
                    xmAnimFrame = null;
                    document.getElementById('movingAssembly').style.transform = `translateX(0px)`;
                    document.getElementById('coneMorph').setAttribute('d', `M 70 35 L 180 15 L 180 85 L 70 65 Z`);
                    document.getElementById('xmaxDispVal').innerText = `0.0 mm`;
                    document.getElementById('vCoilGlow').classList.remove('coil-melt');
                    return;
                }

                xmAnimFrame = requestAnimationFrame(animateExcursion);
                xmTime += 0.5; // Frequency

                // Math: Calculate mechanical displacement based on watts
                // Map 0-4000W to roughly 0-25px of visual movement
                let amplitude = (xmWatts / 4000) * 25; 
                let displacement = Math.sin(xmTime) * amplitude;

                const dispValEl = document.getElementById('xmaxDispVal');
                const vCoil = document.getElementById('vCoilGlow');
                const assembly = document.getElementById('movingAssembly');
                const conePath = document.getElementById('coneMorph');

                // State handling
                if(xmWatts > XMECH_LIMIT) {
                    // BLOWN SPEAKER SIMULATION
                    dispValEl.className = 'xm-val xmax-warning';
                    vCoil.classList.add('coil-melt');
                    
                    // Violent clipping/distortion. The sine wave is squared off.
                    displacement = Math.sign(Math.sin(xmTime)) * amplitude * 1.2; 
                    
                    // Add chaotic vibration to the cone shape itself (cone breakup)
                    const flutter = (Math.random() - 0.5) * 15;
                    conePath.setAttribute('d', `M 70 35 L ${180+flutter} 15 L ${180-flutter} 85 L 70 65 Z`);
                    
                    dispValEl.innerText = `CRITICAL XMECH`;
                    if(navigator.vibrate) navigator.vibrate([50, 50]); // Constant rumble
                    
                } else if(xmWatts > XMAX_SAFE) {
                    // Heavy Distortion
                    dispValEl.className = 'xm-val';
                    dispValEl.style.color = 'var(--gold-primary)';
                    vCoil.classList.remove('coil-melt');
                    
                    // Add slight soft-clipping distortion
                    displacement = Math.sin(xmTime) * amplitude + (Math.sin(xmTime*3) * 2);
                    conePath.setAttribute('d', `M 70 35 L 180 15 L 180 85 L 70 65 Z`); // Normal shape
                    
                    dispValEl.innerText = `${Math.abs(displacement).toFixed(1)} mm`;
                    
                } else {
                    // Normal Operation
                    dispValEl.className = 'xm-val';
                    dispValEl.style.color = '#00ff00';
                    vCoil.classList.remove('coil-melt');
                    conePath.setAttribute('d', `M 70 35 L 180 15 L 180 85 L 70 65 Z`);
                    
                    dispValEl.innerText = `${Math.abs(displacement).toFixed(1)} mm`;
                }

                // Apply the physical translation to the SVG Group containing the Voice Coil, Dust Cap, and Cone
                assembly.style.transform = `translateX(${displacement}px)`;
            }
        </script>
        <style>
            .beam-steer-wrapper {
                background: #000;
                border: 1px solid #1a2233;
                border-radius: 12px;
                padding: 15px;
                box-shadow: inset 0 0 30px rgba(0, 229, 255, 0.05);
            }

            .beam-canvas-box {
                width: 100%;
                height: 250px;
                background: linear-gradient(90deg, #050a15, #000);
                border: 2px solid #222;
                border-radius: 8px;
                position: relative;
                overflow: hidden;
            }
            #beamCanvas { width: 100%; height: 100%; display: block; mix-blend-mode: screen; }

            /* Virtual Line Array (Left side) */
            .line-array-stack {
                position: absolute; top: 50%; left: 20px; transform: translateY(-50%);
                display: flex; flex-direction: column; gap: 2px; z-index: 5;
            }
            .la-box { width: 12px; height: 18px; background: #111; border: 1px solid var(--cyan-neon); border-radius: 2px; }

            /* Audience Target Indicator */
            .beam-target-line {
                position: absolute; top: 50%; left: 32px; right: 0; height: 1px;
                background: rgba(255,51,51,0.5); border-bottom: 1px dashed var(--red-alert);
                transform-origin: left center; transition: transform 0.2s linear; pointer-events: none; z-index: 1;
            }

            .beam-controls {
                background: #0a0a0f; border: 1px solid #1a1a24; border-radius: 8px;
                padding: 15px; margin-top: 15px;
            }
            .bc-hud { display: flex; justify-content: space-between; margin-bottom: 10px; }
            .bc-lbl { font-family: var(--font-data); font-size: 10px; color: #888; font-weight: bold; }
            .bc-val { font-family: var(--font-tech); font-size: 14px; color: #fff; font-weight: bold; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DSP BEAM STEERING AI</h2>
                <div class="section-icon"><i class="fas fa-wifi" style="transform: rotate(90deg);"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Digitally steer the acoustic wavefront up or down without physically moving the speakers by applying micro-second DSP delays.</p>

            <div class="beam-steer-wrapper">
                <div class="beam-canvas-box" id="beamWrap">
                    <canvas id="beamCanvas"></canvas>
                    <div class="line-array-stack" id="laStack">
                        <div class="la-box"></div><div class="la-box"></div><div class="la-box"></div>
                        <div class="la-box"></div><div class="la-box"></div><div class="la-box"></div>
                        <div class="la-box"></div><div class="la-box"></div>
                    </div>
                    <div class="beam-target-line" id="beamTarget"></div>
                    <div style="position:absolute; bottom:10px; right:10px; font-family:var(--font-tech); font-size:8px; color:var(--cyan-neon);">WAVEFRONT CONSTRUCTIVE INTERFERENCE</div>
                </div>

                <div class="beam-controls">
                    <div class="bc-hud">
                        <span class="bc-lbl">DIGITAL STEERING ANGLE (θ)</span>
                        <span class="bc-val" id="beamAngleVal" style="color:var(--cyan-neon);">0°</span>
                    </div>
                    <input type="range" class="app-slider" id="beamAngleSlider" min="-30" max="30" value="0" oninput="updateBeamAngle()">
                    
                    <div style="display:flex; justify-content:space-between; margin-top:15px; border-top:1px dashed #333; padding-top:10px;">
                        <span class="bc-lbl">MAX DSP DELAY REQ.</span>
                        <span class="bc-val" id="beamDelayVal" style="color:var(--gold-primary); font-size:12px;">0.00 ms</span>
                    </div>
                </div>
            </div>
        </div>

        <style>
            .drone-rig-wrapper {
                background: #000;
                border: 2px solid #222;
                border-radius: 12px;
                padding: 15px;
                position: relative;
            }

            .rigging-environment {
                width: 100%; height: 260px; background: linear-gradient(180deg, #020510 0%, #000 100%);
                border-radius: 8px; border: 1px solid #111; position: relative; overflow: hidden;
            }
            
            /* Virtual Drones */
            .lift-drone {
                position: absolute; top: 20px; width: 40px; height: 15px;
                background: #222; border: 1px solid var(--cyan-neon); border-radius: 4px;
                display: flex; justify-content: space-between; align-items: center; z-index: 10;
            }
            .lift-drone::before, .lift-drone::after {
                content: ''; width: 14px; height: 4px; background: rgba(0, 229, 255, 0.5);
                position: absolute; top: -6px; border-radius: 2px; animation: droneProp 0.1s linear infinite;
            }
            .lift-drone::before { left: -5px; } .lift-drone::after { right: -5px; }
            @keyframes droneProp { 0% { opacity: 0.3; transform: scaleX(0.8); } 50% { opacity: 1; transform: scaleX(1.2); } 100% { opacity: 0.3; transform: scaleX(0.8); } }

            #droneL { left: 20%; transform: translateX(-50%); }
            #droneR { left: 80%; transform: translateX(-50%); }

            /* Cables and Truss */
            .hoist-cable {
                position: absolute; top: 35px; width: 2px; background: #888;
                transform-origin: top center; transition: height 0.1s linear;
            }
            #cableL { left: 20%; } #cableR { left: 80%; }

            .rig-truss {
                position: absolute; left: 15%; right: 15%; height: 12px;
                background: repeating-linear-gradient(45deg, #444 0px, #444 4px, #222 4px, #222 8px);
                border: 2px solid #555; border-radius: 2px; z-index: 5;
                transition: top 0.1s linear, transform 0.1s linear; display: flex; justify-content: center; align-items: center;
            }
            .truss-payload { font-family: var(--font-tech); font-size: 8px; color: #fff; background: #000; padding: 2px 5px; border-radius: 2px;}

            .drone-hud {
                display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px;
            }
            .dh-card { background: #0a0a0f; border: 1px solid #1a1a24; padding: 10px; border-radius: 6px; text-align: center; }
            .dh-val { font-family: var(--font-tech); font-size: 16px; font-weight: 900; color: #00ff00; }
            .dh-lbl { font-family: var(--font-data); font-size: 9px; color: #888; letter-spacing: 1px; display: block; margin-top: 4px; }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">DRONE RIGGING AI</h2>
                <div class="section-icon"><i class="fas fa-helicopter"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Control synchronized heavy-lift drones. Monitor motor tension and battery draw while hoisting physical loads.</p>

            <div class="drone-rig-wrapper">
                <div class="rigging-environment">
                    <div class="lift-drone" id="droneL"></div>
                    <div class="lift-drone" id="droneR"></div>
                    
                    <div class="hoist-cable" id="cableL" style="height: 200px;"></div>
                    <div class="hoist-cable" id="cableR" style="height: 200px;"></div>
                    
                    <div class="rig-truss" id="rigTruss" style="top: 235px;">
                        <span class="truss-payload">250 KG PAYLOAD</span>
                    </div>
                </div>

                <div class="drone-hud">
                    <div class="dh-card">
                        <span class="dh-val" id="droneTensionVal">1.2 kN</span>
                        <span class="dh-lbl">CABLE TENSION</span>
                    </div>
                    <div class="dh-card">
                        <span class="dh-val" id="droneBattVal" style="color:var(--gold-primary);">98%</span>
                        <span class="dh-lbl">SWARM BATTERY</span>
                    </div>
                </div>

                <div style="margin-top: 15px;">
                    <span style="font-family:var(--font-data); font-size:10px; color:#fff; font-weight:bold;">HOIST ALTITUDE</span>
                    <input type="range" class="app-slider" id="hoistSlider" min="0" max="100" value="0" style="margin-top: 5px;" oninput="updateDroneHoist(this.value)">
                </div>
            </div>
        </div>

        <style>
            .tube-matrix-wrapper {
                background: #000;
                border: 1px solid #222;
                border-radius: 12px;
                padding: 15px;
            }

            .tube-display-stage {
                width: 100%; height: 220px; background: #050505; border-radius: 8px;
                border: 1px solid #111; display: flex; justify-content: space-around; align-items: center;
                padding: 20px 10px; position: relative; overflow: hidden;
            }
            
            .led-tube {
                width: 12px; height: 100%; background: #111; border-radius: 6px;
                border: 1px solid #333; position: relative; overflow: hidden;
                box-shadow: 0 5px 15px rgba(0,0,0,0.8);
            }
            /* The inner glowing element */
            .tube-core {
                position: absolute; inset: 1px; border-radius: 4px; background: #000;
                transition: background 0.05s linear, box-shadow 0.05s linear;
            }

            .tube-controls {
                display: flex; justify-content: space-between; gap: 10px; margin-top: 15px;
            }
            .tube-btn {
                flex: 1; background: #0a0a0f; border: 1px solid #333; border-radius: 6px; padding: 10px 0;
                font-family: var(--font-data); font-size: 10px; font-weight: bold; color: #888;
                cursor: pointer; transition: 0.2s; text-align: center;
            }
            .tube-btn.active { background: rgba(0,229,255,0.1); border-color: var(--cyan-neon); color: var(--cyan-neon); box-shadow: inset 0 0 10px rgba(0,229,255,0.2); }

            .tube-speed-box {
                background: #0a0a0f; border: 1px solid #222; border-radius: 6px; padding: 15px; margin-top: 10px;
            }
        </style>

        <div class="app-section">
            <div class="section-header">
                <h2 class="section-title">KINETIC TUBE MATRIX</h2>
                <div class="section-icon"><i class="fas fa-grip-lines-vertical"></i></div>
            </div>
            <p style="font-family: var(--font-body); font-size: 11px; color: #888; margin-bottom: 15px;">Simulate wireless pixel-mapped LED tubes. Engage DMX chase macros to run mathematical fluid animations across the array.</p>

            <div class="tube-matrix-wrapper">
                <div class="tube-display-stage" id="tubeStage">
                    </div>

                <div class="tube-controls">
                    <div class="tube-btn active" onclick="setTubeMacro('plasma', this)">PLASMA</div>
                    <div class="tube-btn" onclick="setTubeMacro('pulse', this)">PULSE</div>
                    <div class="tube-btn" onclick="setTubeMacro('chase', this)">CHASE</div>
                    <div class="tube-btn" onclick="setTubeMacro('strobe', this)" style="border-color:var(--red-alert); color:var(--red-alert);">STROBE</div>
                </div>

                <div class="tube-speed-box">
                    <div style="display:flex; justify-content:space-between; margin-bottom:5px;">
                        <span style="font-family:var(--font-data); font-size:10px; color:#aaa; font-weight:bold;">MACRO SPEED</span>
                        <span id="tubeSpeedVal" style="font-family:var(--font-tech); font-size:12px; color:#fff;">1.0x</span>
                    </div>
                    <input type="range" class="app-slider" id="tubeSpeedSlider" min="1" max="50" value="10" oninput="updateTubeSpeed()">
                </div>
            </div>
        </div>

        <script>
            // --- 1. PHASED ARRAY BEAM STEERING LOGIC ---
            const bmCanvas = document.getElementById('beamCanvas');
            let bmCtx = null;
            const bmWrap = document.getElementById('beamWrap');
            const bmTarget = document.getElementById('beamTarget');
            
            let bmAnimFrame = null;
            let bmTime = 0;
            let bmAngle = 0; // -30 to 30 degrees
            const numSpeakers = 8;
            const speakerSpacing = 16; // pixels

            function initBeamSteering() {
                if(!bmWrap || !bmCanvas) return;
                bmCanvas.width = bmWrap.clientWidth;
                bmCanvas.height = bmWrap.clientHeight;
                bmCtx = bmCanvas.getContext('2d');
                if(!bmAnimFrame) animateBeamSteer();
            }
            window.addEventListener('resize', initBeamSteering);
            setTimeout(initBeamSteering, 500);

            function updateBeamAngle() {
                bmAngle = parseInt(document.getElementById('beamAngleSlider').value);
                
                // Update UI Texts
                document.getElementById('beamAngleVal').innerText = `${bmAngle}°`;
                
                // Physics calculation for required delay
                // Max distance between top and bottom speaker
                const maxDist = (numSpeakers - 1) * 0.3; // Approx meters
                // Delay = (d * sin(theta)) / speed of sound
                const angleRad = Math.abs(bmAngle) * (Math.PI / 180);
                const delayMs = ((maxDist * Math.sin(angleRad)) / 343) * 1000;
                
                document.getElementById('beamDelayVal').innerText = `${delayMs.toFixed(2)} ms`;

                // Rotate target line
                bmTarget.style.transform = `translateY(-50%) rotate(${bmAngle}deg)`;
                
                if(navigator.vibrate) navigator.vibrate(10);
            }

            function animateBeamSteer() {
                bmAnimFrame = requestAnimationFrame(animateBeamSteer);
                if(!bmCtx) return;

                bmCtx.fillStyle = '#050a15';
                bmCtx.fillRect(0,0, bmCanvas.width, bmCanvas.height);

                bmTime += 2.0;

                const startX = 30; // Matches CSS left: 20px + box width
                const centerY = bmCanvas.height / 2;
                // Calculate top Y so array is centered
                const arrayHeight = (numSpeakers - 1) * speakerSpacing;
                const topY = centerY - (arrayHeight / 2);

                bmCtx.globalCompositeOperation = 'screen';
                bmCtx.lineWidth = 2;

                // To steer a beam DOWN (positive angle), the BOTTOM speakers must fire AFTER the top ones.
                // We simulate this by applying a phase/time offset to the expanding rings.
                const phaseStep = bmAngle * 1.5; 

                for(let i=0; i<numSpeakers; i++) {
                    const sy = topY + (i * speakerSpacing);
                    
                    // The delay offset based on speaker position
                    const offset = i * phaseStep;

                    // Draw 4 expanding rings per speaker
                    for(let rWave=0; rWave<4; rWave++) {
                        let r = (bmTime + (rWave * 60) - offset) % 240;
                        
                        if(r > 0) {
                            const alpha = Math.max(0, 1 - (r / 240));
                            bmCtx.strokeStyle = `rgba(0, 229, 255, ${alpha * 0.4})`;
                            
                            bmCtx.beginPath();
                            // Draw an arc facing right
                            bmCtx.arc(startX, sy, r, -Math.PI/2, Math.PI/2);
                            bmCtx.stroke();
                        }
                    }
                }
                bmCtx.globalCompositeOperation = 'source-over';
            }


            // --- 2. AUTOMATED DRONE RIGGING SIMULATOR LOGIC ---
            let droneHoistPct = 0;
            let droneBatt = 100.0;
            let droneInterval = null;

            function updateDroneHoist(val) {
                droneHoistPct = parseInt(val);
                
                const maxDrop = 200; // pixels
                // 0% slider = 200px drop. 100% slider = 20px drop (pulled up).
                const currentDrop = maxDrop - ((droneHoistPct / 100) * (maxDrop - 20));
                
                // Move elements
                document.getElementById('cableL').style.height = `${currentDrop}px`;
                document.getElementById('cableR').style.height = `${currentDrop}px`;
                document.getElementById('rigTruss').style.top = `${currentDrop + 35}px`; // 35 is top offset of cable

                // Calculate mechanical tension (more tension when lifting fast or high)
                const tension = 1.2 + (droneHoistPct / 100) * 0.8;
                document.getElementById('droneTensionVal').innerText = `${tension.toFixed(2)} kN`;
                
                // Add slight mechanical wobble to the truss based on height
                const wobble = (droneHoistPct / 100) * (Math.random() - 0.5) * 2;
                document.getElementById('rigTruss').style.transform = `rotate(${wobble}deg)`;

                if(navigator.vibrate) navigator.vibrate(15);
            }

            // Battery drain simulation loop
            droneInterval = setInterval(() => {
                // Drain battery faster if hoisting high
                const drainRate = 0.01 + (droneHoistPct / 100) * 0.05;
                droneBatt -= drainRate;
                if(droneBatt <= 0) droneBatt = 0;

                const battEl = document.getElementById('droneBattVal');
                if(battEl) {
                    battEl.innerText = `${droneBatt.toFixed(1)}%`;
                    if(droneBatt < 20) battEl.style.color = "var(--red-alert)";
                    else if (droneBatt < 50) battEl.style.color = "var(--gold-primary)";
                }
            }, 1000);


            // --- 3. KINETIC LED TUBE MATRIX LOGIC ---
            const numTubes = 16;
            let tubeMacro = 'plasma'; // plasma, pulse, chase, strobe
            let tubeSpeed = 1.0;
            let tubeAnimFrame = null;
            let tubeTime = 0;
            let tubeCores = [];

            function initTubeMatrix() {
                const stage = document.getElementById('tubeStage');
                if(!stage) return;
                stage.innerHTML = '';
                tubeCores = [];

                for(let i=0; i<numTubes; i++) {
                    const tube = document.createElement('div');
                    tube.className = 'led-tube';
                    
                    const core = document.createElement('div');
                    core.className = 'tube-core';
                    
                    tube.appendChild(core);
                    stage.appendChild(tube);
                    tubeCores.push(core);
                }

                if(!tubeAnimFrame) animateTubes();
            }
            setTimeout(initTubeMatrix, 300);

            function setTubeMacro(mode, btnEl) {
                if(typeof playTap === 'function') playTap();
                tubeMacro = mode;
                document.querySelectorAll('.tube-btn').forEach(b => b.classList.remove('active'));
                btnEl.classList.add('active');
            }

            function updateTubeSpeed() {
                const val = document.getElementById('tubeSpeedSlider').value;
                tubeSpeed = parseInt(val) / 10;
                document.getElementById('tubeSpeedVal').innerText = `${tubeSpeed.toFixed(1)}x`;
            }

            function animateTubes() {
                tubeAnimFrame = requestAnimationFrame(animateTubes);
                tubeTime += 0.05 * tubeSpeed;

                tubeCores.forEach((core, i) => {
                    let colorStr = '#000';
                    let shadowStr = 'none';

                    if(tubeMacro === 'plasma') {
                        // Smooth sine wave across colors
                        const phase = tubeTime + (i * 0.4);
                        const r = Math.sin(phase) * 127 + 128;
                        const g = Math.sin(phase + 2) * 127 + 128;
                        const b = Math.sin(phase + 4) * 127 + 128;
                        colorStr = `rgb(${r},${g},${b})`;
                        shadowStr = `0 0 15px ${colorStr}`;
                    } 
                    else if (tubeMacro === 'pulse') {
                        // All pulse together, cyan
                        const intensity = (Math.sin(tubeTime * 2) + 1) / 2; // 0 to 1
                        colorStr = `rgba(0, 229, 255, ${intensity})`;
                        if(intensity > 0.1) shadowStr = `0 0 ${intensity * 20}px rgba(0, 229, 255, 1)`;
                    }
                    else if (tubeMacro === 'chase') {
                        // Running pixel
                        // Modulo time to get current active tube index
                        const activeIndex = Math.floor(tubeTime * 5) % numTubes;
                        if(i === activeIndex) {
                            colorStr = 'var(--gold-glow)';
                            shadowStr = '0 0 20px var(--gold-glow)';
                        } else if (i === (activeIndex - 1 + numTubes) % numTubes) {
                            // Tail
                            colorStr = 'rgba(212, 175, 55, 0.3)';
                        }
                    }
                    else if (tubeMacro === 'strobe') {
                        // Violent random flashing
                        if(Math.random() > 0.8) {
                            colorStr = '#fff';
                            shadowStr = '0 0 20px #fff';
                        }
                    }

                    core.style.background = colorStr;
                    core.style.boxShadow = shadowStr;
                });
            }
        </script>
        
