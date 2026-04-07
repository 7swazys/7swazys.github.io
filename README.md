<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>7swazys · DevHub | Dashboard + Repos + Links</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #0a0f1e 0%, #0c1222 100%);
            font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', 'Fira Code', monospace;
            min-height: 100vh;
            padding: 1.5rem;
            overflow-x: hidden;
        }

        /* ENTRY SCREEN STYLES - Clean version */
        .entry-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(145deg, #0a0f1e 0%, #0c1222 100%);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: opacity 0.8s ease, visibility 0.8s ease;
            cursor: pointer;
        }

        .entry-screen.hide {
            opacity: 0;
            visibility: hidden;
        }

        .entry-card {
            background: rgba(18, 25, 45, 0.85);
            backdrop-filter: blur(20px);
            border-radius: 2.5rem;
            border: 1px solid rgba(72, 187, 255, 0.4);
            padding: 3rem 4rem;
            text-align: center;
            animation: floatGlow 2s ease-in-out infinite;
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.6), 0 0 0 1px rgba(56, 189, 248, 0.2);
            transition: transform 0.2s;
        }

        .entry-card:hover {
            transform: scale(1.02);
        }

        @keyframes floatGlow {
            0%, 100% { transform: translateY(0px); box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.6); }
            50% { transform: translateY(-10px); box-shadow: 0 35px 55px -12px rgba(59, 130, 246, 0.3); }
        }

        .entry-title {
            font-size: 3rem;
            font-weight: 600;
            background: linear-gradient(135deg, #c0e0ff, #3b82f6);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            margin-bottom: 1rem;
            letter-spacing: 2px;
        }

        .enter-text {
            font-size: 1.2rem;
            color: #8caee0;
            letter-spacing: 4px;
            text-transform: uppercase;
            margin-top: 1rem;
            opacity: 0.8;
            transition: opacity 0.2s;
        }

        .entry-card:hover .enter-text {
            opacity: 1;
            color: #3b82f6;
        }

        /* Audio Control Button */
        .audio-control {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 100;
            background: rgba(18, 25, 45, 0.8);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(72, 187, 255, 0.3);
            border-radius: 3rem;
            padding: 0.5rem 1rem;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.8rem;
            color: #8caee0;
        }

        .audio-control:hover {
            border-color: #3b82f6;
            transform: scale(1.05);
        }

        /* Rest of your original styles */
        .glass-card {
            max-width: 1400px;
            width: 100%;
            margin: 0 auto;
            background: rgba(18, 25, 45, 0.75);
            backdrop-filter: blur(14px);
            border-radius: 2.5rem;
            border: 1px solid rgba(72, 187, 255, 0.25);
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.6), 0 0 0 1px rgba(56, 189, 248, 0.1);
            overflow: hidden;
        }

        .header {
            padding: 1.75rem 2rem;
            background: rgba(12, 18, 34, 0.7);
            border-bottom: 1px solid rgba(56, 189, 248, 0.3);
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            gap: 1rem;
        }

        .header-left h1 {
            font-size: 1.9rem;
            font-weight: 600;
            background: linear-gradient(135deg, #c0e0ff, #3b82f6);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: -0.3px;
            display: inline-flex;
            align-items: center;
            gap: 12px;
        }

        .header-left h1::before {
            content: "⚡";
            font-size: 2rem;
            background: none;
            color: #3b82f6;
        }

        .sub {
            color: #9ab3d5;
            margin-top: 0.5rem;
            font-size: 0.85rem;
            border-left: 3px solid #3b82f6;
            padding-left: 0.85rem;
            font-family: monospace;
        }

        .social-links {
            display: flex;
            gap: 1rem;
            align-items: center;
            flex-wrap: wrap;
        }

        .social-btn {
            background: linear-gradient(100deg, #2563eb, #1e40af);
            padding: 0.6rem 1.3rem;
            border-radius: 2rem;
            font-weight: 600;
            color: white;
            text-decoration: none;
            font-size: 0.85rem;
            transition: transform 0.1s, background 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 10px rgba(37, 99, 235, 0.3);
            cursor: pointer;
        }

        .social-btn:hover {
            background: linear-gradient(100deg, #3b82f6, #1e3a8a);
            transform: scale(0.98);
        }

        .tabs {
            display: flex;
            flex-wrap: wrap;
            background: rgba(0, 0, 0, 0.3);
            border-bottom: 1px solid #26324a;
            gap: 0.25rem;
            padding: 0 1.5rem;
        }

        .tab-btn {
            background: transparent;
            border: none;
            padding: 1rem 1.8rem;
            font-size: 0.9rem;
            font-weight: 500;
            color: #8caee0;
            cursor: pointer;
            transition: all 0.2s;
            border-bottom: 2px solid transparent;
            font-family: inherit;
            box-shadow: none;
        }

        .tab-btn:hover {
            color: white;
            background: rgba(59, 130, 246, 0.1);
        }

        .tab-btn.active {
            color: #3b82f6;
            border-bottom-color: #3b82f6;
        }

        .tab-content {
            display: none;
            padding: 2rem;
            animation: fadeIn 0.25s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(6px);}
            to { opacity: 1; transform: translateY(0);}
        }

        .repo-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 1.5rem;
            margin-top: 1rem;
        }

        .repo-card {
            background: rgba(12, 18, 34, 0.7);
            border: 1px solid #26324a;
            border-radius: 1.5rem;
            padding: 1.3rem;
            transition: all 0.2s;
            backdrop-filter: blur(4px);
        }

        .repo-card:hover {
            border-color: #3b82f6;
            transform: translateY(-3px);
            background: rgba(20, 30, 50, 0.8);
        }

        .repo-name {
            font-size: 1.1rem;
            font-weight: 600;
            color: #c0e0ff;
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            gap: 8px;
            flex-wrap: wrap;
        }

        .repo-name a {
            color: #7aa9ff;
            text-decoration: none;
        }

        .repo-name a:hover {
            text-decoration: underline;
            color: #3b82f6;
        }

        .repo-desc {
            font-size: 0.8rem;
            color: #9ab3d5;
            margin-bottom: 0.75rem;
            line-height: 1.4;
        }

        .repo-meta {
            display: flex;
            gap: 1rem;
            font-size: 0.7rem;
            color: #5f7faf;
            border-top: 1px solid #1e2a3e;
            padding-top: 0.7rem;
            margin-top: 0.5rem;
        }

        .lang-badge {
            background: #1e293b;
            padding: 0.2rem 0.6rem;
            border-radius: 2rem;
        }

        .loading-skeleton {
            color: #6a86b3;
            text-align: center;
            padding: 3rem;
        }

        .profile-row {
            display: flex;
            flex-wrap: wrap;
            gap: 2rem;
            align-items: center;
            margin-bottom: 1.8rem;
            background: rgba(0, 0, 0, 0.25);
            border-radius: 1.5rem;
            padding: 1rem 1.5rem;
        }

        .github-stats {
            display: flex;
            gap: 1.5rem;
            flex-wrap: wrap;
        }

        .stat-badge {
            background: #0f1422;
            padding: 0.3rem 1rem;
            border-radius: 2rem;
            font-size: 0.8rem;
            color: #7aa9ff;
        }

        .refresh-btn {
            background: #1e293b;
            padding: 0.4rem 1rem;
            border-radius: 2rem;
            font-size: 0.75rem;
            cursor: pointer;
            border: none;
            color: #b9e2ff;
        }

        .links-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin: 1.2rem 0;
        }

        .profile-card {
            background: rgba(12, 18, 34, 0.6);
            border-radius: 1.5rem;
            padding: 1.5rem;
            border: 1px solid #26324a;
            margin-bottom: 1.5rem;
        }

        .roblox-embed {
            background: #0b1020;
            border-radius: 1rem;
            padding: 0.8rem;
            margin-top: 0.8rem;
            border: 1px solid #2a3a60;
            font-family: monospace;
            font-size: 0.8rem;
            word-break: break-all;
        }

        footer {
            padding: 1rem 2rem;
            text-align: center;
            font-size: 0.7rem;
            color: #4c6188;
            border-top: 1px solid rgba(72, 120, 184, 0.2);
            background: rgba(0, 0, 0, 0.2);
        }

        @media (max-width: 700px) {
            body { padding: 0.8rem; }
            .header { flex-direction: column; align-items: start; }
            .tab-btn { padding: 0.7rem 1rem; }
            .tab-content { padding: 1rem; }
            .entry-title { font-size: 2rem; }
            .entry-card { padding: 2rem 2.5rem; }
        }
    </style>
</head>
<body>

<!-- ENTRY SCREEN - Clean, click anywhere to enter -->
<div id="entryScreen" class="entry-screen">
    <div class="entry-card">
        <div class="entry-title">7swazys</div>
        <div class="enter-text">ENTER</div>
    </div>
</div>

<!-- AUDIO CONTROL BUTTON -->
<div id="audioControl" class="audio-control" style="display: none;">
    <span>🔊</span> <span id="audioStatus">Music Playing</span>
</div>

<div class="glass-card">
    <div class="header">
        <div class="header-left">
            <h1>7swazys · DevHub</h1>
            <div class="sub">roblox scripts · tools · open source</div>
        </div>
        <div class="social-links">
            <a href="https://github.com/7swazys" target="_blank" class="social-btn">GitHub</a>
        </div>
    </div>

    <div class="tabs">
        <button class="tab-btn active" data-tab="repos">Repositories</button>
        <button class="tab-btn" data-tab="about">About & Links</button>
    </div>

    <div id="reposTab" class="tab-content active">
        <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; margin-bottom: 1.2rem;">
            <div class="profile-row" style="margin-bottom: 0; flex:1">
                <div class="github-stats">
                    <span class="stat-badge" id="repoCount">loading repos...</span>
                    <span class="stat-badge" id="lastUpdated">live from GitHub</span>
                </div>
                <button id="refreshReposBtn" class="refresh-btn">refresh</button>
            </div>
        </div>
        <div id="reposContainer" class="repo-grid">
            <div class="loading-skeleton">fetching repositories from github.com/7swazys ...</div>
        </div>
        <div style="margin-top: 1rem; font-size:0.7rem; color:#4c6188; text-align:center;">repositories update automatically on refresh — shows latest pushes</div>
    </div>

    <div id="aboutTab" class="tab-content">
        <div style="max-width: 900px;">
            <div class="profile-card">
                <h3 style="color:#c0e0ff; margin-bottom: 0.75rem;">7swazys</h3>
                <p style="color:#9ab3d5; line-height: 1.5; margin-bottom: 1rem;">
                Roblox script developer and open-source enthusiast. Creating loadstring tools, automation scripts, 
                and utilities for the community. All repositories are free to use and modify.
                </p>
                <div style="display: flex; gap: 1rem; flex-wrap: wrap; margin-bottom: 1rem;">
                    <span class="stat-badge">Joined GitHub: Apr 2026</span>
                    <span class="stat-badge">8+ public repos</span>
                    <span class="stat-badge">Languages: Luau, HTML, JavaScript</span>
                </div>
            </div>

            <div class="profile-card">
                <h3 style="color:#c0e0ff; margin-bottom: 0.75rem;">Roblox Profile</h3>
                <p style="color:#9ab3d5; margin-bottom: 0.5rem;">User ID: 5181378476</p>
                <div class="links-grid">
                    <a href="https://www.roblox.com/user.aspx?ID=5181378476" target="_blank" class="social-btn" style="background:#1e293b;">View Roblox Profile</a>
                </div>
                <div class="roblox-embed" style="display: flex; align-items: center; gap: 1rem; flex-wrap: wrap;">
                    <img src="https://www.roblox.com/headshot-thumbnail/image?userId=5181378476&width=100&height=100&format=png" alt="Roblox avatar" style="border-radius: 1rem; background: #0f1422; width: 64px; height: 64px; object-fit: cover;" 
                         onerror="this.src='https://www.roblox.com/headshot-thumbnail/image?userId=5181378476&width=100&height=100&format=png'; this.onerror=null;">
                    <div>
                        <span style="color:#b9e2ff;">7swazys on Roblox</span><br>
                        <span style="font-size:0.7rem; color:#7aa9ff;">Roblox developer & scripter</span>
                    </div>
                </div>
                <div style="margin-top: 0.8rem; font-size:0.75rem; color:#6a86b3;">
                    Roblox ID: 5181378476 · join profile for game updates and script showcases.
                </div>
            </div>

            <div class="profile-card">
                <h3 style="color:#c0e0ff; margin-bottom: 0.75rem;">Roblox Group</h3>
                <p style="color:#9ab3d5;">SGNRS - script hub & community group</p>
                <div class="links-grid">
                    <a href="https://www.roblox.com/communities/826801520/SGNRS" target="_blank" class="social-btn" style="background:#1e293b;">Join SGNRS Group</a>
                </div>
                <div class="roblox-embed" style="margin-top: 0.5rem;">
                    <span style="color:#8caee0;">SGNRS · 167 members</span><br>
                    <span style="font-size:0.7rem;">haiiii remzy/tdx here join this group for updatess</span>
                </div>
            </div>

            <div class="profile-card">
                <h3 style="color:#c0e0ff; margin-bottom: 0.75rem;">Discord Community</h3>
                <p style="color:#9ab3d5;">Join the official server for script support, updates, and dev talks.</p>
                <div class="links-grid">
                    <a href="https://discord.gg/8JJxWmhU" target="_blank" class="social-btn discord-btn" style="background: linear-gradient(100deg, #5865F2, #4752c4);">Join Discord Server</a>
                </div>
            </div>

            <div class="profile-card">
                <h3 style="color:#c0e0ff; margin-bottom: 0.75rem;">TikTok</h3>
                <p style="color:#9ab3d5;">Follow for roblox scripting content and showcases.</p>
                <div class="links-grid">
                    <a href="https://www.tiktok.com/@xle8b" target="_blank" class="social-btn" style="background:#1e293b;">TikTok: @xle8b</a>
                </div>
            </div>

            <div class="profile-card" style="text-align:center;">
                <a href="https://github.com/7swazys" target="_blank" class="social-btn" style="padding:0.4rem 1.2rem;">View all repositories on GitHub</a>
            </div>
        </div>
    </div>

    <footer>
        7swazys devhub · repositories fetched live from GitHub API · roblox profile & group links · discord community
    </footer>
</div>

<script>
    (function() {
        // ========================================
        // AUDIO SYSTEM
        // ========================================
        const clickSoundUrl = 'https://files.catbox.moe/3doj7d.mp3';
        const introMusicUrl = 'https://files.catbox.moe/z3dwlq.mp3';
        const bgMusicUrl = 'https://files.catbox.moe/tgewfw.mp3';
        
        let clickAudio = null;
        let introAudio = null;
        let bgAudio = null;
        let isAudioEnabled = false;
        let isIntroPlaying = false;
        
        // DOM elements
        const entryScreen = document.getElementById('entryScreen');
        const audioControl = document.getElementById('audioControl');
        const audioStatusSpan = document.getElementById('audioStatus');
        
        // Function to play click sound
        function playClickSound() {
            if (!isAudioEnabled) return;
            try {
                if (clickAudio) {
                    clickAudio.currentTime = 0;
                    clickAudio.play().catch(e => console.log('Click play error:', e));
                }
            } catch(e) { console.log('Click error:', e); }
        }
        
        // Initialize audio elements
        function initAudio() {
            clickAudio = new Audio(clickSoundUrl);
            clickAudio.volume = 0.5;
            clickAudio.preload = 'auto';
            
            introAudio = new Audio(introMusicUrl);
            introAudio.volume = 0.7;
            introAudio.preload = 'auto';
            
            bgAudio = new Audio(bgMusicUrl);
            bgAudio.volume = 0.4;
            bgAudio.loop = true;
            bgAudio.preload = 'auto';
            
            // When intro ends, start background music
            introAudio.addEventListener('ended', () => {
                if (isAudioEnabled && bgAudio) {
                    bgAudio.play().catch(e => console.log('BG play error:', e));
                    if (audioStatusSpan) audioStatusSpan.innerText = 'Music Playing';
                }
                isIntroPlaying = false;
            });
        }
        
        // Start the audio sequence
        function startAudioSequence() {
            if (!isAudioEnabled) return;
            
            // Stop any playing audio
            if (bgAudio) {
                bgAudio.pause();
                bgAudio.currentTime = 0;
            }
            
            // Play intro music
            if (introAudio) {
                introAudio.currentTime = 0;
                introAudio.play().catch(e => console.log('Intro play error:', e));
                isIntroPlaying = true;
                if (audioStatusSpan) audioStatusSpan.innerText = 'Playing Intro...';
            }
        }
        
        // Toggle background music
        function toggleMusic() {
            if (!isAudioEnabled) return;
            
            if (bgAudio && !bgAudio.paused && !isIntroPlaying) {
                bgAudio.pause();
                if (audioStatusSpan) audioStatusSpan.innerText = 'Music Paused';
            } else if (bgAudio && bgAudio.paused && !isIntroPlaying) {
                bgAudio.play().catch(e => console.log('Resume error:', e));
                if (audioStatusSpan) audioStatusSpan.innerText = 'Music Playing';
            }
        }
        
        // ENTER SCREEN - click anywhere to enter
        entryScreen.addEventListener('click', () => {
            // Initialize audio system
            initAudio();
            isAudioEnabled = true;
            
            // Hide entry screen with animation
            entryScreen.classList.add('hide');
            
            // Show audio control button
            audioControl.style.display = 'flex';
            
            // Start the audio sequence (intro then bg)
            startAudioSequence();
            
            // Remove entry screen from DOM after animation
            setTimeout(() => {
                entryScreen.style.display = 'none';
            }, 800);
        });
        
        // Audio control click
        audioControl.addEventListener('click', toggleMusic);
        
        // ========================================
        // TAB SWITCHING WITH CLICK SOUNDS
        // ========================================
        const tabs = document.querySelectorAll('.tab-btn');
        const reposTab = document.getElementById('reposTab');
        const aboutTab = document.getElementById('aboutTab');
        
        function switchTab(tabId) {
            playClickSound(); // Play sound on tab switch
            
            if (tabId === 'repos') {
                reposTab.classList.add('active');
                aboutTab.classList.remove('active');
            } else if (tabId === 'about') {
                aboutTab.classList.add('active');
                reposTab.classList.remove('active');
            }
            tabs.forEach(btn => {
                const btnTab = btn.getAttribute('data-tab');
                if (btnTab === tabId) btn.classList.add('active');
                else btn.classList.remove('active');
            });
        }
        
        tabs.forEach(btn => {
            btn.addEventListener('click', () => {
                const tabId = btn.getAttribute('data-tab');
                if (tabId === 'repos') switchTab('repos');
                else if (tabId === 'about') switchTab('about');
            });
        });
        
        // ========================================
        // BUTTON CLICK SOUNDS (all buttons)
        // ========================================
        document.querySelectorAll('.social-btn, .refresh-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                playClickSound();
            });
        });
        
        // Also add to any dynamically created buttons
        const observer = new MutationObserver(() => {
            document.querySelectorAll('.social-btn, .refresh-btn').forEach(btn => {
                if (!btn.hasAttribute('data-sound-bound')) {
                    btn.setAttribute('data-sound-bound', 'true');
                    btn.addEventListener('click', () => playClickSound());
                }
            });
        });
        observer.observe(document.body, { childList: true, subtree: true });
        
        // ========================================
        // GITHUB REPOSITORY FETCHING
        // ========================================
        const reposContainer = document.getElementById('reposContainer');
        const repoCountSpan = document.getElementById('repoCount');
        const lastUpdatedSpan = document.getElementById('lastUpdated');
        const refreshBtn = document.getElementById('refreshReposBtn');
        
        const GITHUB_USERNAME = '7swazys';
        const GITHUB_API_URL = `https://api.github.com/users/${GITHUB_USERNAME}/repos?sort=updated&per_page=50`;
        
        async function fetchAndRenderRepos() {
            reposContainer.innerHTML = '<div class="loading-skeleton">fetching latest repositories from GitHub ...</div>';
            try {
                const controller = new AbortController();
                const timeoutId = setTimeout(() => controller.abort(), 8000);
                const response = await fetch(GITHUB_API_URL, {
                    signal: controller.signal,
                    headers: { 'Accept': 'application/vnd.github.v3+json' }
                });
                clearTimeout(timeoutId);
                
                if (!response.ok) throw new Error(`GitHub API error: ${response.status}`);
                const repos = await response.json();
                if (!Array.isArray(repos) || repos.length === 0) throw new Error('No repositories found');
                
                repos.sort((a,b) => new Date(b.updated_at) - new Date(a.updated_at));
                renderRepoGrid(repos);
                repoCountSpan.innerHTML = `${repos.length} repositories`;
                const lastUpdate = new Date().toLocaleTimeString();
                lastUpdatedSpan.innerHTML = `updated ${lastUpdate}`;
            } catch (err) {
                console.error(err);
                reposContainer.innerHTML = `<div class="loading-skeleton" style="color:#ffaeaa;">failed to fetch repos: ${err.message}<br><button id="retryFetchBtn" style="margin-top:10px; background:#2563eb; border:none; padding:6px 16px; border-radius:30px; color:white;">retry</button></div>`;
                const retryBtn = document.getElementById('retryFetchBtn');
                if (retryBtn) retryBtn.addEventListener('click', () => fetchAndRenderRepos());
                repoCountSpan.innerHTML = `fetch error`;
            }
        }
        
        function renderRepoGrid(repos) {
            if (!reposContainer) return;
            reposContainer.innerHTML = '';
            repos.forEach(repo => {
                const card = document.createElement('div');
                card.className = 'repo-card';
                
                const name = repo.name || 'unnamed';
                const description = repo.description ? repo.description.substring(0, 100) : 'No description provided';
                const language = repo.language || 'N/A';
                const stars = repo.stargazers_count || 0;
                const updatedAt = repo.updated_at ? new Date(repo.updated_at).toLocaleDateString() : 'recent';
                const repoUrl = repo.html_url || `https://github.com/${GITHUB_USERNAME}/${name}`;
                
                card.innerHTML = `
                    <div class="repo-name">
                        <a href="${repoUrl}" target="_blank">${escapeHtml(name)}</a>
                    </div>
                    <div class="repo-desc">${escapeHtml(description)}</div>
                    <div class="repo-meta">
                        <span>⭐ ${stars}</span>
                        <span class="lang-badge">${escapeHtml(language)}</span>
                        <span>updated ${updatedAt}</span>
                    </div>
                `;
                reposContainer.appendChild(card);
            });
            
            if (repos.length === 0) {
                reposContainer.innerHTML = '<div class="loading-skeleton">no public repositories visible? check github profile</div>';
            }
        }
        
        function escapeHtml(str) {
            if (!str) return '';
            return str.replace(/[&<>]/g, function(m) {
                if (m === '&') return '&amp;';
                if (m === '<') return '&lt;';
                if (m === '>') return '&gt;';
                return m;
            });
        }
        
        if (refreshBtn) {
            refreshBtn.addEventListener('click', () => {
                fetchAndRenderRepos();
            });
        }
        
        fetchAndRenderRepos();
        
        setInterval(() => {
            if (reposTab && reposTab.classList.contains('active')) {
                fetchAndRenderRepos().catch(e=>console.warn);
            }
        }, 120000);
        
        async function fetchUserProfile() {
            try {
                const res = await fetch(`https://api.github.com/users/${GITHUB_USERNAME}`);
                if (res.ok) {
                    const userData = await res.json();
                    const publicRepos = userData.public_repos || 0;
                    if (repoCountSpan && !repoCountSpan.innerHTML.includes('fetch error')) {
                        repoCountSpan.innerHTML = `${publicRepos} repos · ${userData.followers || 0} followers`;
                    }
                }
            } catch(e) {}
        }
        fetchUserProfile();
        
        const robloxImg = document.querySelector('.roblox-embed img');
        if (robloxImg) {
            robloxImg.src = `https://www.roblox.com/headshot-thumbnail/image?userId=5181378476&width=100&height=100&format=png`;
        }
    })();
</script>
</body>
</html>
