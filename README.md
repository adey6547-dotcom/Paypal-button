
<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Glowing PayPal Button Studio</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter & JetBrains Mono -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    }
                }
            }
        }
    </script>

    <style>
        /* Core Animated Rainbow Neon Button Styles */
        :root {
            --glow-speed: 3.5s;
            --glow-blur: 18px;
            --glow-spread: -2px;
            --btn-radius: 9999px;
            --btn-bg: rgba(10, 12, 22, 0.88);
        }

        @keyframes rainbow-shift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        @keyframes shimmer-sweep {
            0% { transform: translateX(-150%) skewX(-25deg); }
            100% { transform: translateX(250%) skewX(-25deg); }
        }

        .neon-pay-btn {
            position: relative;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            padding: 18px 40px;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            font-size: 1.125rem;
            font-weight: 700;
            letter-spacing: 0.02em;
            color: #ffffff;
            text-decoration: none;
            border-radius: var(--btn-radius);
            z-index: 1;
            transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.3s ease;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            cursor: pointer;
        }

        /* Animated Rainbow Border Layer */
        .neon-pay-btn::before {
            content: "";
            position: absolute;
            inset: -3px;
            border-radius: inherit;
            background: linear-gradient(
                90deg,
                #ff007f,
                #ff7700,
                #ffdd00,
                #00ff88,
                #00d4ff,
                #7a00ff,
                #ff007f
            );
            background-size: 300% 300%;
            animation: rainbow-shift var(--glow-speed) ease infinite;
            z-index: -2;
            transition: inset 0.3s ease;
        }

        /* Soft Outer Neon Aura */
        .neon-pay-btn::after {
            content: "";
            position: absolute;
            inset: var(--glow-spread);
            border-radius: inherit;
            background: linear-gradient(
                90deg,
                #ff007f,
                #ff7700,
                #ffdd00,
                #00ff88,
                #00d4ff,
                #7a00ff,
                #ff007f
            );
            background-size: 300% 300%;
            animation: rainbow-shift var(--glow-speed) ease infinite;
            filter: blur(var(--glow-blur));
            opacity: 0.8;
            z-index: -3;
            transition: filter 0.35s ease, opacity 0.35s ease, inset 0.35s ease;
        }

        /* Inner Surface Plate */
        .neon-pay-surface {
            position: absolute;
            inset: 2px;
            background: var(--btn-bg);
            border-radius: inherit;
            z-index: -1;
            overflow: hidden;
            transition: background 0.3s ease;
            backdrop-filter: blur(12px);
        }

        /* Subtle light sweep across button on hover */
        .neon-pay-surface::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 45%;
            height: 100%;
            background: linear-gradient(
                90deg,
                rgba(255, 255, 255, 0) 0%,
                rgba(255, 255, 255, 0.18) 50%,
                rgba(255, 255, 255, 0) 100%
            );
            transform: translateX(-150%) skewX(-25deg);
        }

        /* Hover & Focus States */
        .neon-pay-btn:hover {
            transform: scale(1.06) translateY(-2px);
        }

        .neon-pay-btn:hover::after {
            filter: blur(calc(var(--glow-blur) * 1.45));
            opacity: 1;
            inset: -6px;
        }

        .neon-pay-btn:hover .neon-pay-surface {
            background: rgba(15, 18, 34, 0.72);
        }

        .neon-pay-btn:hover .neon-pay-surface::after {
            animation: shimmer-sweep 0.85s ease-out forwards;
        }

        /* Active / Click Feedback */
        .neon-pay-btn:active {
            transform: scale(0.96) translateY(1px);
        }

        .neon-pay-btn:focus-visible {
            outline: 2px solid #00d4ff;
            outline-offset: 6px;
        }

        /* Grid Background for Preview Canvas */
        .preview-grid-dark {
            background-color: #070913;
            background-image: 
                radial-gradient(circle at 50% 50%, rgba(56, 189, 248, 0.08) 0%, transparent 60%),
                linear-gradient(to right, rgba(255, 255, 255, 0.04) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.04) 1px, transparent 1px);
            background-size: 100% 100%, 28px 28px, 28px 28px;
        }

        .preview-grid-light {
            background-color: #f8fafc;
            background-image: 
                radial-gradient(circle at 50% 50%, rgba(168, 85, 247, 0.08) 0%, transparent 60%),
                linear-gradient(to right, rgba(15, 23, 42, 0.05) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(15, 23, 42, 0.05) 1px, transparent 1px);
            background-size: 100% 100%, 28px 28px, 28px 28px;
        }

        /* Custom Scrollbar for Code Box */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(15, 23, 42, 0.6);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(100, 116, 139, 0.5);
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: rgba(148, 163, 184, 0.8);
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 font-sans min-h-screen selection:bg-fuchsia-500 selection:text-white">

    <!-- Top Header -->
    <header class="border-b border-slate-800/80 bg-slate-900/60 backdrop-blur-md sticky top-0 z-30">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 py-4 flex flex-wrap items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-pink-500 via-purple-500 to-cyan-400 p-[2px] shadow-lg shadow-purple-500/20">
                    <div class="w-full h-full bg-slate-950 rounded-[10px] flex items-center justify-center">
                        <svg class="w-5 h-5 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
                        </svg>
                    </div>
                </div>
                <div>
                    <h1 class="text-lg font-bold tracking-tight text-white flex items-center gap-2">
                        Neon Glow Button Studio
                        <span class="text-xs font-medium px-2.5 py-0.5 rounded-full bg-cyan-500/10 text-cyan-300 border border-cyan-500/20">PayPal Ready</span>
                    </h1>
                    <p class="text-xs text-slate-400">Interactive preview & copy-paste embed generator</p>
                </div>
            </div>

            <div class="flex items-center gap-3">
                <a href="https://www.paypal.com/ncp/payment/VU4AEZ4NKSR2U" target="_blank" rel="noopener noreferrer" 
                   class="text-xs sm:text-sm font-medium text-slate-300 hover:text-white bg-slate-800/90 hover:bg-slate-800 border border-slate-700 px-3.5 py-2 rounded-lg transition flex items-center gap-2">
                    <span>Test Direct Link</span>
                    <svg class="w-3.5 h-3.5 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
                    </svg>
                </a>
            </div>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="max-w-6xl mx-auto px-4 sm:px-6 py-8 space-y-8">
        
        <!-- Top Grid: Live Interactive Stage + Customizer Controls -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-stretch">
            
            <!-- Left Column: Live Button Stage (7 cols) -->
            <div class="lg:col-span-7 flex flex-col rounded-2xl border border-slate-800 bg-slate-900/40 overflow-hidden shadow-2xl">
                
                <!-- Stage Toolbar -->
                <div class="px-5 py-3.5 bg-slate-900/90 border-b border-slate-800 flex items-center justify-between">
                    <div class="flex items-center gap-2">
                        <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 animate-pulse"></span>
                        <span class="text-xs font-semibold uppercase tracking-wider text-slate-400">Live Interactive Preview</span>
                    </div>
                    
                    <!-- Stage Background Toggle -->
                    <div class="flex items-center gap-1.5 bg-slate-950 p-1 rounded-lg border border-slate-800">
                        <button id="bgDarkBtn" onclick="setStageTheme('dark')" class="px-2.5 py-1 rounded-md text-xs font-medium bg-slate-800 text-white shadow transition">
                            Dark Stage
                        </button>
                        <button id="bgLightBtn" onclick="setStageTheme('light')" class="px-2.5 py-1 rounded-md text-xs font-medium text-slate-400 hover:text-white transition">
                            Light Stage
                        </button>
                    </div>
                </div>

                <!-- Interactive Preview Canvas -->
                <div id="previewStage" class="preview-grid-dark flex-1 min-h-[320px] sm:min-h-[360px] flex flex-col items-center justify-center p-8 relative transition-colors duration-300">
                    
                    <!-- The Actual Glowing Button -->
                    <a id="livePayButton" 
                       href="https://www.paypal.com/ncp/payment/VU4AEZ4NKSR2U" 
                       target="_blank" 
                       rel="noopener noreferrer"
                       class="neon-pay-btn group">
                        <span class="neon-pay-surface"></span>
                        
                        <!-- PayPal Inspired Emblem SVG -->
                        <svg id="btnIcon" class="w-6 h-6 text-cyan-300 transition-transform duration-300 group-hover:rotate-12 group-hover:scale-110" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M7.076 21.337H2.47a.641.641 0 0 1-.633-.74L4.944.901C5.026.382 5.474 0 5.998 0h7.46c2.57 0 4.578.543 5.69 1.81 1.01 1.15 1.304 2.42 1.012 4.287-.023.143-.047.288-.077.437-.983 5.05-4.349 6.797-8.647 6.797h-2.19c-.524 0-.968.382-1.05.9l-1.12 7.106zm14.146-14.42a3.35 3.35 0 0 0-.607-.541c-.013.076-.026.175-.041.254-.93 4.778-4.005 7.201-9.138 7.201h-2.19a.563.563 0 0 0-.556.479l-1.187 7.527h-.506l-.24 1.516a.56.56 0 0 0 .554.647h3.882c.46 0 .85-.334.922-.788.06-.26.76-4.852.816-5.09a.932.932 0 0 1 .923-.788h.58c3.76 0 6.705-1.528 7.565-5.946.36-1.847.174-3.388-.777-4.471z"/>
                        </svg>

                        <span id="liveButtonText">Pay Now with PayPal</span>

                        <!-- Right Arrow Indicator -->
                        <svg class="w-5 h-5 opacity-80 transition-transform duration-300 group-hover:translate-x-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M13 7l5 5m0 0l-5 5m5-5H6"/>
                        </svg>
                    </a>

                    <!-- Helper Caption Below Button -->
                    <div id="stageCaption" class="mt-10 text-center space-y-1">
                        <p class="text-xs font-medium text-slate-400">
                            Hover to amplify neon aura • Click to open PayPal checkout in a new tab
                        </p>
                        <p class="text-[11px] font-mono text-slate-500 break-all px-4">
                            https://www.paypal.com/ncp/payment/VU4AEZ4NKSR2U
                        </p>
                    </div>
                </div>
            </div>

            <!-- Right Column: Real-Time Customizer (5 cols) -->
            <div class="lg:col-span-5 rounded-2xl border border-slate-800 bg-slate-900/60 p-6 flex flex-col justify-between space-y-6">
                <div class="space-y-5">
                    <div class="flex items-center justify-between border-b border-slate-800 pb-3">
                        <h2 class="text-base font-semibold text-white flex items-center gap-2">
                            <svg class="w-4 h-4 text-fuchsia-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"/>
                            </svg>
                            Customize Button
                        </h2>
                        <button onclick="resetDefaults()" class="text-xs text-slate-400 hover:text-cyan-300 transition">
                            Reset Defaults
                        </button>
                    </div>

                    <!-- Button Label Input -->
                    <div>
                        <label for="labelInput" class="block text-xs font-medium text-slate-300 mb-1.5">Button Text</label>
                        <input id="labelInput" type="text" value="Pay Now with PayPal" 
                               oninput="updateCustomization()"
                               class="w-full px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-800 text-sm text-white focus:outline-none focus:border-cyan-500 transition">
                    </div>

                    <!-- Glow Intensity Slider -->
                    <div>
                        <div class="flex justify-between text-xs mb-1.5">
                            <label for="blurSlider" class="font-medium text-slate-300">Neon Glow Blur</label>
                            <span id="blurValue" class="font-mono text-cyan-400">18px</span>
                        </div>
                        <input id="blurSlider" type="range" min="8" max="40" value="18" 
                               oninput="updateCustomization()"
                               class="w-full accent-fuchsia-500 cursor-pointer">
                    </div>

                    <!-- Rainbow Animation Speed Slider -->
                    <div>
                        <div class="flex justify-between text-xs mb-1.5">
                            <label for="speedSlider" class="font-medium text-slate-300">Rainbow Flow Speed</label>
                            <span id="speedValue" class="font-mono text-cyan-400">3.5s</span>
                        </div>
                        <input id="speedSlider" type="range" min="1.5" max="8" step="0.5" value="3.5" 
                               oninput="updateCustomization()"
                               class="w-full accent-cyan-400 cursor-pointer">
                    </div>

                    <!-- Corner Shape Selector -->
                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-2">Button Shape</label>
                        <div class="grid grid-cols-3 gap-2">
                            <button onclick="setRadius('9999px', this)" class="shape-btn active-shape py-2 px-3 rounded-lg text-xs font-medium border border-cyan-500/50 bg-cyan-500/10 text-cyan-300 transition">
                                Pill (Full)
                            </button>
                            <button onclick="setRadius('14px', this)" class="shape-btn py-2 px-3 rounded-lg text-xs font-medium border border-slate-800 bg-slate-950 text-slate-400 hover:text-white transition">
                                Rounded
                            </button>
                            <button onclick="setRadius('6px', this)" class="shape-btn py-2 px-3 rounded-lg text-xs font-medium border border-slate-800 bg-slate-950 text-slate-400 hover:text-white transition">
                                Sharp
                            </button>
                        </div>
                    </div>

                    <!-- Surface Style Selector -->
                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-2">Inner Button Fill</label>
                        <div class="grid grid-cols-2 gap-2">
                            <button id="fillDarkBtn" onclick="setFillMode('dark')" class="py-2 px-3 rounded-lg text-xs font-medium border border-cyan-500/50 bg-cyan-500/10 text-cyan-300 transition">
                                Cyber Dark Core
                            </button>
                            <button id="fillVibrantBtn" onclick="setFillMode('vibrant')" class="py-2 px-3 rounded-lg text-xs font-medium border border-slate-800 bg-slate-950 text-slate-400 hover:text-white transition">
                                Full Rainbow Core
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Destination Status Card -->
                <div class="p-3.5 rounded-xl bg-slate-950/90 border border-slate-800/80 flex items-center gap-3">
                    <div class="w-8 h-8 rounded-lg bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center shrink-0">
                        <svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"/>
                        </svg>
                    </div>
                    <div class="min-w-0 flex-1">
                        <p class="text-xs font-semibold text-slate-200">Verified Target Link Attached</p>
                        <p class="text-[11px] text-slate-400 truncate">Opens PayPal checkout (`VU4AEZ4NKSR2U`) in a new tab</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Bottom Section: Ready-to-Embed HTML & CSS Code Snippet -->
        <div class="rounded-2xl border border-slate-800 bg-slate-900/60 overflow-hidden shadow-xl">
            <div class="px-6 py-4 bg-slate-900 border-b border-slate-800 flex flex-wrap items-center justify-between gap-4">
                <div>
                    <h2 class="text-base font-semibold text-white flex items-center gap-2">
                        <svg class="w-5 h-5 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
                        </svg>
                        Embed Code (HTML + CSS)
                    </h2>
                    <p class="text-xs text-slate-400">Self-contained snippet updated live with your settings above. Paste anywhere into your website.</p>
                </div>

                <button id="copyCodeBtn" onclick="copySnippet()" 
                        class="px-4 py-2.5 rounded-xl font-semibold text-xs sm:text-sm bg-gradient-to-r from-pink-500 via-purple-500 to-cyan-500 text-white shadow-lg shadow-purple-500/20 hover:opacity-95 active:scale-95 transition flex items-center gap-2">
                    <svg id="copyIcon" class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"/>
                    </svg>
                    <span id="copyBtnText">Copy Embed Code</span>
                </button>
            </div>

            <div class="relative bg-slate-950 p-4 sm:p-6 overflow-x-auto">
                <pre class="text-xs sm:text-sm font-mono text-slate-300 leading-relaxed"><code id="codeOutput"></code></pre>
            </div>
        </div>

    </main>

    <!-- Toast Notification for Copy Action -->
    <div id="copyToast" class="fixed bottom-5 right-5 transform translate-y-20 opacity-0 pointer-events-none transition-all duration-300 z-50 bg-slate-900 border border-emerald-500/40 text-white px-4 py-3 rounded-xl shadow-2xl flex items-center gap-3">
        <div class="w-6 h-6 rounded-full bg-emerald-500/20 text-emerald-400 flex items-center justify-center">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M5 13l4 4L19 7"/>
            </svg>
        </div>
        <span class="text-sm font-medium">HTML & CSS snippet copied to clipboard!</span>
    </div>

    <script>
        // Current State Configuration
        let currentConfig = {
            text: "Pay Now with PayPal",
            blur: 18,
            speed: 3.5,
            radius: "9999px",
            fillMode: "dark" // 'dark' or 'vibrant'
        };

        const root = document.documentElement;
        const liveButtonText = document.getElementById('liveButtonText');
        const labelInput = document.getElementById('labelInput');
        const blurSlider = document.getElementById('blurSlider');
        const speedSlider = document.getElementById('speedSlider');
        const blurValue = document.getElementById('blurValue');
        const speedValue = document.getElementById('speedValue');
        const codeOutput = document.getElementById('codeOutput');

        // Update Live CSS Variables & Snippet
        function updateCustomization() {
            currentConfig.text = labelInput.value.trim() || "Pay Now with PayPal";
            currentConfig.blur = blurSlider.value;
            currentConfig.speed = speedSlider.value;

            // Update DOM & CSS Variables
            liveButtonText.textContent = currentConfig.text;
            blurValue.textContent = `${currentConfig.blur}px`;
            speedValue.textContent = `${currentConfig.speed}s`;

            root.style.setProperty('--glow-blur', `${currentConfig.blur}px`);
            root.style.setProperty('--glow-speed', `${currentConfig.speed}s`);
            root.style.setProperty('--btn-radius', currentConfig.radius);

            if (currentConfig.fillMode === 'vibrant') {
                root.style.setProperty('--btn-bg', 'rgba(15, 23, 42, 0.15)');
            } else {
                root.style.setProperty('--btn-bg', 'rgba(10, 12, 22, 0.88)');
            }

            generateCodeSnippet();
        }

        // Update Button Border Radius
        function setRadius(radiusValue, btnElement) {
            currentConfig.radius = radiusValue;
            document.querySelectorAll('.shape-btn').forEach(btn => {
                btn.className = "shape-btn py-2 px-3 rounded-lg text-xs font-medium border border-slate-800 bg-slate-950 text-slate-400 hover:text-white transition";
            });
            btnElement.className = "shape-btn active-shape py-2 px-3 rounded-lg text-xs font-medium border border-cyan-500/50 bg-cyan-500/10 text-cyan-300 transition";
            updateCustomization();
        }

        // Update Inner Core Fill Style
        function setFillMode(mode) {
            currentConfig.fillMode = mode;
            const darkBtn = document.getElementById('fillDarkBtn');
            const vibrantBtn = document.getElementById('fillVibrantBtn');

            if (mode === 'dark') {
                darkBtn.className = "py-2 px-3 rounded-lg text-xs font-medium border border-cyan-500/50 bg-cyan-500/10 text-cyan-300 transition";
                vibrantBtn.className = "py-2 px-3 rounded-lg text-xs font-medium border border-slate-800 bg-slate-950 text-slate-400 hover:text-white transition";
            } else {
                vibrantBtn.className = "py-2 px-3 rounded-lg text-xs font-medium border border-cyan-500/50 bg-cyan-500/10 text-cyan-300 transition";
                darkBtn.className = "py-2 px-3 rounded-lg text-xs font-medium border border-slate-800 bg-slate-950 text-slate-400 hover:text-white transition";
            }
            updateCustomization();
        }

        // Switch Preview Stage Background (Dark / Light)
        function setStageTheme(theme) {
            const stage = document.getElementById('previewStage');
            const darkBtn = document.getElementById('bgDarkBtn');
            const lightBtn = document.getElementById('bgLightBtn');

            if (theme === 'light') {
                stage.classList.remove('preview-grid-dark');
                stage.classList.add('preview-grid-light');
                lightBtn.className = "px-2.5 py-1 rounded-md text-xs font-medium bg-slate-800 text-white shadow transition";
                darkBtn.className = "px-2.5 py-1 rounded-md text-xs font-medium text-slate-400 hover:text-white transition";
            } else {
                stage.classList.remove('preview-grid-light');
                stage.classList.add('preview-grid-dark');
                darkBtn.className = "px-2.5 py-1 rounded-md text-xs font-medium bg-slate-800 text-white shadow transition";
                lightBtn.className = "px-2.5 py-1 rounded-md text-xs font-medium text-slate-400 hover:text-white transition";
            }
        }

        // Reset to Default Settings
        function resetDefaults() {
            labelInput.value = "Pay Now with PayPal";
            blurSlider.value = 18;
            speedSlider.value = 3.5;
            const firstShapeBtn = document.querySelector('.shape-btn');
            setRadius('9999px', firstShapeBtn);
            setFillMode('dark');
        }

        // Generate Self-Contained Copyable Code
        function generateCodeSnippet() {
            const bgRgba = currentConfig.fillMode === 'vibrant' ? 'rgba(15, 23, 42, 0.15)' : 'rgba(10, 12, 22, 0.88)';
            const hoverBgRgba = currentConfig.fillMode === 'vibrant' ? 'rgba(15, 23, 42, 0.05)' : 'rgba(15, 18, 34, 0.72)';

            const snippet = `<!-- Glowing Colorful PayPal Payment Button -->
<a href="https://www.paypal.com/ncp/payment/VU4AEZ4NKSR2U" target="_blank" rel="noopener noreferrer" class="glowing-paypal-btn">
  <span class="glowing-paypal-surface"></span>
  <svg class="glowing-paypal-icon" viewBox="0 0 24 24" fill="currentColor">
    <path d="M7.076 21.337H2.47a.641.641 0 0 1-.633-.74L4.944.901C5.026.382 5.474 0 5.998 0h7.46c2.57 0 4.578.543 5.69 1.81 1.01 1.15 1.304 2.42 1.012 4.287-.023.143-.047.288-.077.437-.983 5.05-4.349 6.797-8.647 6.797h-2.19c-.524 0-.968.382-1.05.9l-1.12 7.106z"/>
  </svg>
  <span>${currentConfig.text}</span>
</a>

<style>
  @keyframes paypal-rainbow-flow {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  .glowing-paypal-btn {
    position: relative;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    padding: 16px 36px;
    font-family: system-ui, -apple-system, sans-serif;
    font-size: 18px;
    font-weight: 700;
    color: #ffffff;
    text-decoration: none;
    border-radius: ${currentConfig.radius};
    z-index: 1;
    transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  }

  .glowing-paypal-btn::before,
  .glowing-paypal-btn::after {
    content: "";
    position: absolute;
    inset: -3px;
    border-radius: inherit;
    background: linear-gradient(90deg, #ff007f, #ff7700, #ffdd00, #00ff88, #00d4ff, #7a00ff, #ff007f);
    background-size: 300% 300%;
    animation: paypal-rainbow-flow ${currentConfig.speed}s ease infinite;
    z-index: -2;
  }

  .glowing-paypal-btn::after {
    filter: blur(${currentConfig.blur}px);
    opacity: 0.85;
    z-index: -3;
    transition: filter 0.3s ease, opacity 0.3s ease, inset 0.3s ease;
  }

  .glowing-paypal-surface {
    position: absolute;
    inset: 2px;
    background: ${bgRgba};
    border-radius: inherit;
    z-index: -1;
    transition: background 0.3s ease;
  }

  .glowing-paypal-icon {
    width: 22px;
    height: 22px;
    color: #38bdf8;
  }

  .glowing-paypal-btn:hover {
    transform: scale(1.06) translateY(-2px);
  }

  .glowing-paypal-btn:hover::after {
    filter: blur(${Math.round(currentConfig.blur * 1.4)}px);
    opacity: 1;
    inset: -6px;
  }

  .glowing-paypal-btn:hover .glowing-paypal-surface {
    background: ${hoverBgRgba};
  }

  .glowing-paypal-btn:active {
    transform: scale(0.96);
  }
</style>`;

            codeOutput.textContent = snippet;
        }

        // Copy Snippet to Clipboard (compatible with iframe environments)
        function copySnippet() {
            const textToCopy = codeOutput.textContent;
            const textArea = document.createElement("textarea");
            textArea.value = textToCopy;
            textArea.style.position = "fixed";
            textArea.style.left = "-9999px";
            document.body.appendChild(textArea);
            textArea.focus();
            textArea.select();

            try {
                document.execCommand('copy');
                showCopyFeedback();
            } catch (err) {
                console.error('Copy failed', err);
            }

            document.body.removeChild(textArea);
        }

        function showCopyFeedback() {
            const toast = document.getElementById('copyToast');
            const copyBtnText = document.getElementById('copyBtnText');
            
            copyBtnText.textContent = "Copied!";
            toast.classList.remove('translate-y-20', 'opacity-0');
            
            setTimeout(() => {
                copyBtnText.textContent = "Copy Embed Code";
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 2600);
        }

        // Initialize on load
        window.onload = function() {
            updateCustomization();
        };
    </script>
</body>
</html>
