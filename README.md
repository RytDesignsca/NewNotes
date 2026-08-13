<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>New Notes</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Quicksand:wght@400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      --bg-light: #f8f9ff;
      --text: #2d3748;
      --card-bg: #ffffff;
      --accent-pink: #ff6b9d;
      --accent-blue: #4facfe;
      --accent-yellow: #feca57;
      --accent-green: #1dd1a1;
      --accent-purple: #a29bfe;
      --shadow: rgba(0, 0, 0, 0.1);
      --font-main: 'Quicksand', sans-serif;
      --font-accent: 'Poppins', sans-serif;
    }
    
    /* Alternate styles (applied via body.classList) */
    body.style-minimal {
      --bg-gradient: linear-gradient(180deg, #ffffff 0%, #f6f7fb 100%);
      --bg-light: #ffffff;
      --text: #222;
      --card-bg: #fff;
      --shadow: rgba(0,0,0,0.05);
      --accent-pink: #ff6b9d;
      --accent-blue: #4facfe;
    }
    body.style-dark-compact {
      --bg-gradient: linear-gradient(135deg, #0f1724 0%, #0b1220 100%);
      --bg-light: #0b1220;
      --text: #e6eef8;
      --card-bg: #071129;
      --shadow: rgba(0,0,0,0.6);
      --accent-pink: #ff6b9d;
      --accent-blue: #4facfe;
    }
    body.style-pastel {
      --bg-gradient: linear-gradient(135deg, #f9f2ff 0%, #fff7f2 100%);
      --bg-light: #fffaf6;
      --text: #2d3748;
      --card-bg: #ffffff;
      --shadow: rgba(0, 0, 0, 0.04);
      --accent-pink: #f78da7;
      --accent-blue: #a0d2ff;
    }
    
    body.dark-mode {
      --bg-light: #1a1a2e;
      --text: #eee;
      --card-bg: #16213e;
      --shadow: rgba(0, 0, 0, 0.3);
    }
    
    * { margin: 0; padding: 0; box-sizing: border-box; }
    
    body {
      font-family: var(--font-main);
      background: var(--bg-light);
      color: var(--text);
      min-height: 100vh;
      transition: all 0.25s ease;
    }
    
    /* Cute Header */
    .header {
      background: var(--bg-gradient);
      padding: 1.25rem 1.5rem;
      color: white;
      box-shadow: 0 4px 20px var(--shadow);
      position: sticky;
      top: 0;
      z-index: 100;
    }
    
    .header-content {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 0.75rem;
    }
    
    .logo {
      font-size: 1.6rem;
      font-weight: 700;
      font-family: var(--font-accent);
      display: flex;
      align-items: center;
      gap: 0.5rem;
      cursor: pointer;
    }
    
    .logo-emoji {
      animation: bounce 2s infinite;
    }
    
    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-6px); }
    }
    
    .header-controls {
      display: flex;
      gap: 0.75rem;
      align-items: center;
      flex-wrap: wrap;
    }
    
    .btn {
      padding: 0.6rem 1.2rem;
      border: none;
      border-radius: 50px;
      font-family: var(--font-main);
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
    }
    
    .btn:hover { transform: translateY(-2px); }
    .btn-primary { background: var(--accent-pink); color: white; }
    .btn-secondary { background: white; color: var(--accent-blue); }
    .btn-success { background: var(--accent-green); color: white; }
    
    .theme-toggle {
      background: rgba(255, 255, 255, 0.12);
      backdrop-filter: blur(6px);
      border-radius: 50px;
      padding: 0.38rem 0.8rem;
      display: flex;
      align-items: center;
      gap: 0.4rem;
      cursor: pointer;
      transition: all 0.2s ease;
    }
    
    /* Main Content */
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 1.25rem;
    }
    
    /* Tab Navigation */
    .tabs {
      display: flex;
      gap: 0.75rem;
      margin-bottom: 1.5rem;
      flex-wrap: wrap;
    }
    
    .tab {
      padding: 0.8rem 1.2rem;
      background: var(--card-bg);
      border-radius: 16px;
      cursor: pointer;
      font-weight: 600;
      transition: all 0.2s ease;
      box-shadow: 0 2px 8px var(--shadow);
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.95rem;
    }
    
    .tab.active { background: var(--bg-gradient); color: white; }
    
    /* Notebook Grid */
    .notebook-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 1rem;
      margin-bottom: 2rem;
    }
    
    .notebook-card {
      background: var(--card-bg);
      border-radius: 18px;
      padding: 1.25rem;
      box-shadow: 0 6px 18px var(--shadow);
      cursor: pointer;
      transition: all 0.2s ease;
      position: relative;
      overflow: hidden;
    }
    .notebook-card:hover { transform: translateY(-6px); }
    .notebook-icon { font-size: 2.5rem; margin-bottom: 0.6rem;}
    .notebook-title { font-size: 1.05rem; font-weight:700; margin-bottom:0.25rem;}
    .notebook-meta { font-size:0.85rem; color:#7a8797; margin-bottom:0.5rem;}
    .notebook-actions{ display:flex; gap:0.4rem; justify-content:flex-end; margin-top:0.25rem;}
    .action-btn{ padding:0.4rem;background:var(--bg-light);border-radius:8px;border:none;cursor:pointer;}
    
    /* Create New Card */
    .create-card {
      background: linear-gradient(135deg, var(--accent-pink), var(--accent-purple));
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 160px;
      border-radius: 18px;
      cursor: pointer;
    }
    .create-icon{ font-size:2.25rem; margin-bottom:0.5rem; }
    
    /* Template Section */
    .section-title {
      font-size: 1.6rem;
      font-weight: 700;
      margin: 1.5rem 0 1rem;
      font-family: var(--font-accent);
      display: flex;
      align-items: center;
      gap: 0.75rem;
    }
    
    .template-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 1rem;
    }
    
    .template-card {
      background: var(--card-bg);
      border-radius: 14px;
      padding: 1.2rem;
      box-shadow: 0 6px 18px var(--shadow);
      transition: all 0.18s ease;
      border-left: 6px solid;
      cursor: pointer;
      display:flex;
      flex-direction:column;
      gap:0.5rem;
    }
    .template-card:hover { transform: translateY(-6px); box-shadow: 0 10px 30px var(--shadow); }
    .template-emoji{ font-size:1.8rem; }
    .template-title{ font-size:1.05rem; font-weight:700; }
    .template-desc{ color:#718096; font-size:0.92rem; line-height:1.4; }
    
    .template-card:nth-child(1) { border-color: var(--accent-pink); }
    .template-card:nth-child(2) { border-color: var(--accent-blue); }
    .template-card:nth-child(3) { border-color: var(--accent-yellow); }
    .template-card:nth-child(4) { border-color: var(--accent-green); }
    .template-card:nth-child(5) { border-color: var(--accent-purple); }
    .template-card:nth-child(6) { border-color: var(--accent-pink); }
    
    /* Modal */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      backdrop-filter: blur(4px);
      z-index: 1000;
      align-items: center;
      justify-content: center;
      animation: fadeIn 0.2s ease;
    }
    .modal-content { background:var(--card-bg); border-radius:12px; padding:1rem; width:90%; max-width:520px; box-shadow: 0 12px 40px var(--shadow); }
    .modal-close{ float:right; cursor:pointer; padding:6px; border-radius:6px; background:var(--bg-light); }
    
    /* Settings content */
    .style-options { display:flex; gap:0.5rem; flex-wrap:wrap; margin-top:0.5rem; }
    .style-option { padding:0.5rem 0.8rem; border-radius:8px; cursor:pointer; border:1px solid rgba(0,0,0,0.06); background:var(--bg-light); }
    .style-option.active { box-shadow:0 4px 16px var(--shadow); transform:translateY(-3px); border-color:var(--accent-blue); }
    
    /* Footer */
    .footer { text-align:center; padding:2rem 1rem; background:var(--card-bg); margin-top:2rem; border-top:1px solid rgba(0,0,0,0.06); }
    .footer-heart{ color:var(--accent-pink); animation:heartbeat 1.5s infinite; }
    @keyframes heartbeat { 0%,100%{transform:scale(1)} 50%{transform:scale(1.12)} }

    /* EDITOR PAGE */
    .editor-page { display:none; min-height:100vh; background:var(--bg-light); }
    .editor-page.active { display:block; }
    .editor-header { background:var(--bg-gradient); padding:1rem; color:white; display:flex; justify-content:space-between; align-items:center; gap:0.5rem; border-radius:0 0 10px 10px; }
    .editor-title-input { background:rgba(255,255,255,0.15); border:1px solid transparent; padding:0.5rem 0.75rem; border-radius:8px; color:white; font-weight:700; }
    .editor-actions { display:flex; gap:0.5rem; align-items:center; }
    .editor-container { max-width:900px; margin:1rem auto; padding:1rem; }
    .editor-toolbar { background:var(--card-bg); padding:0.6rem; border-radius:8px; display:flex; gap:0.4rem; margin-bottom:0.8rem; box-shadow:0 6px 18px var(--shadow); }
    .editor-content{ background:var(--card-bg); border-radius:8px; padding:1rem; min-height:420px; box-shadow:0 6px 18px var(--shadow); }
    .text-editor { width:100%; min-height:320px; border:none; outline:none; font-family:var(--font-main); font-size:1rem; line-height:1.6; color:var(--text); background:transparent; }
    .text-editor:focus { outline:2px solid rgba(0,0,0,0.06); }

    /* Responsive */
    @media (max-width:900px) {
      .template-grid { grid-template-columns: 1fr 1fr; }
    }
    @media (max-width:560px) {
      .template-grid { grid-template-columns: 1fr; }
      .notebook-grid { grid-template-columns: repeat(auto-fill, minmax(160px,1fr)); }
    }
  </style>
</head>
<body>
  <!-- HOME PAGE -->
  <div class="home-page">
    <!-- Header -->
    <header class="header">
      <div class="header-content">
        <div class="logo" id="logo-home">
          <span class="logo-emoji">✨</span>
          <span id="app-title">New Notes</span>
        </div>
        <div class="header-controls">
          <button class="btn btn-primary" id="new-note-btn">➕ New Note</button>
          <button class="btn btn-secondary" id="login-btn">🔐 Login</button>
          <div class="theme-toggle" id="theme-toggle"><span id="theme-icon">🌙</span> <span id="theme-text">Dark Mode</span></div>
        </div>
      </div>
    </header>

    <!-- Main Container -->
    <div class="container">
      <!-- Tabs -->
      <div class="tabs">
        <div class="tab active" data-tab="all"><span>📚</span> All Notes</div>
        <div class="tab" data-tab="favorites"><span>⭐</span> Favorites</div>
        <div class="tab" data-tab="shared"><span>👥</span> Shared</div>
        <div class="tab" data-tab="templates"><span>🎨</span> Templates</div>
      </div>

      <!-- My Notebooks Section -->
      <section id="notebooks-section">
        <h2 class="section-title"><span>📖</span> My Notebooks</h2>
        <div class="notebook-grid" id="notebook-grid">
          <!-- Create New Card -->
          <div class="notebook-card create-card" id="create-new">
            <div class="create-icon">➕</div>
            <div class="create-text">Create New</div>
          </div>
        </div>
      </section>

      <!-- Templates Section -->
      <section id="templates-section">
        <h2 class="section-title"><span>🎨</span> Popular Templates</h2>
        <div class="template-grid" id="template-grid">
          <div class="template-card" data-template="daily-planner">
            <div class="template-emoji">📅</div>
            <h3 class="template-title">Daily / Weekly Planner</h3>
            <p class="template-desc">A weekly view with time blocks and a daily checklist for planning your week.</p>
          </div>

          <div class="template-card" data-template="bullet-journal">
            <div class="template-emoji">✅</div>
            <h3 class="template-title">Bullet Journal</h3>
            <p class="template-desc">Rapid logging: tasks, events, notes, habit trackers, and reflections.</p>
          </div>

          <div class="template-card" data-template="study-notes">
            <div class="template-emoji">📚</div>
            <h3 class="template-title">Study Notes (Cornell)</h3>
            <p class="template-desc">Two-column Cornell layout — notes, cues, and a bottom summary section.</p>
          </div>

          <div class="template-card" data-template="budget-tracker">
            <div class="template-emoji">💰</div>
            <h3 class="template-title">Budget Tracker</h3>
            <p class="template-desc">Income, expense table and running totals to keep your finances clear.</p>
          </div>

          <div class="template-card" data-template="fitness-plan">
            <div class="template-emoji">🏃</div>
            <h3 class="template-title">Fitness Plan</h3>
            <p class="template-desc">Weekly workout schedule, meal plan, goals and progress trackers.</p>
          </div>

          <div class="template-card" data-template="blank-canvas">
            <div class="template-emoji">✏️</div>
            <h3 class="template-title">Blank Canvas</h3>
            <p class="template-desc">Freeform notes, sketches and creative writing — a clean blank space.</p>
          </div>
        </div>
      </section>
    </div>

    <!-- Footer -->
    <footer class="footer">
      <p>Made with <span class="footer-heart">💖</span> by New Notes</p>
      <p style="margin-top: 0.5rem; color: #718096;">© 2026 • Keep your thoughts organized!</p>
    </footer>
  </div>

  <!-- EDITOR PAGE -->
  <div class="editor-page" id="editor-page">
    <div class="editor-header">
      <div style="display:flex;align-items:center;gap:0.6rem;">
        <button class="back-btn btn-secondary" id="back-btn">←</button>
        <input type="text" class="editor-title-input" id="note-title-editor" placeholder="Untitled Note" />
      </div>
      <div class="editor-actions">
        <div class="save-status" id="save-status"><span>💾</span> <span id="save-text">Auto-saved</span></div>
        <button class="btn btn-success" id="save-btn">💾 Save</button>
      </div>
    </div>

    <div class="editor-container">
      <div class="editor-toolbar">
        <button class="toolbar-btn" onclick="document.execCommand('bold')"><strong>B</strong></button>
        <button class="toolbar-btn" onclick="document.execCommand('italic')"><em>I</em></button>
        <button class="toolbar-btn" onclick="document.execCommand('underline')"><u>U</u></button>
        <button class="toolbar-btn" onclick="document.execCommand('insertUnorderedList')">• List</button>
        <button class="toolbar-btn" onclick="document.execCommand('insertOrderedList')">1. List</button>
      </div>

      <div class="editor-content">
        <div class="text-editor" id="text-editor" contenteditable="true" spellcheck="true">Start writing your notes here...</div>
      </div>
    </div>
  </div>

  <!-- Login Modal -->
  <div class="modal" id="login-modal">
    <div class="modal-content">
      <div style="display:flex;justify-content:space-between;align-items:center;">
        <h3 class="modal-title">🔐 Sign In</h3>
        <div class="modal-close" id="login-close">×</div>
      </div>
      <div style="margin-top:0.5rem;">
        <button class="auth-btn auth-google" id="google-login" style="width:100%;margin-bottom:0.5rem;background:#4285f4;color:#fff;">🔵 Continue with Google</button>
        <button class="auth-btn auth-microsoft" id="microsoft-login" style="width:100%;margin-bottom:0.5rem;background:#00a4ef;color:#fff;">🔷 Continue with Microsoft</button>
        <button class="auth-btn auth-email" id="email-login" style="width:100%;background:var(--accent-purple);color:#fff;">✉️ Email / Password</button>
        <p style="font-size:0.9rem;color:#6b7380;margin-top:0.6rem;">Signed in users keep notes synced across devices (requires Firestore enabled).</p>
      </div>
    </div>
  </div>

  <!-- Settings Modal -->
  <div class="modal" id="settings-modal">
    <div class="modal-content">
      <div style="display:flex;justify-content:space-between;align-items:center;">
        <h3 class="modal-title">⚙️ Settings</h3>
        <div class="modal-close" id="settings-close">×</div>
      </div>

      <div style="margin-top:0.6rem;">
        <div class="profile-section" style="background:transparent;padding:0;">
          <div class="profile-avatar" id="profile-avatar">👤</div>
          <div class="profile-info">
            <h3 id="user-name">Guest</h3>
            <p id="user-email">Not signed in</p>
          </div>
        </div>

        <div style="margin-top:0.8rem;">
          <div style="font-weight:700;margin-bottom:0.4rem;">Interface Style</div>
          <div class="style-options" id="style-options">
            <div class="style-option" data-style="default">Cute (Default)</div>
            <div class="style-option" data-style="style-minimal">Minimal</div>
            <div class="style-option" data-style="style-dark-compact">Dark Compact</div>
            <div class="style-option" data-style="style-pastel">Pastel</div>
          </div>
        </div>

        <ul class="settings-menu" style="margin-top:0.9rem; list-style:none; padding-left:0;">
          <li class="settings-item">📝 Manage Templates</li>
          <li class="settings-item">⚙️ Preferences</li>
          <li class="settings-item">❓ Help & Support</li>
          <li class="settings-item">ℹ️ About</li>
          <li class="settings-item" id="delete-account" style="color: var(--accent-pink);">🗑️ Delete Account</li>
        </ul>
      </div>
    </div>
  </div>

  <script type="module">
    // Firebase imports (Firestore + Auth)
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-app.js";
    import {
      getAuth,
      GoogleAuthProvider,
      OAuthProvider,
      signInWithPopup,
      createUserWithEmailAndPassword,
      signInWithEmailAndPassword,
      onAuthStateChanged,
      EmailAuthProvider,
      reauthenticateWithCredential,
      deleteUser
    } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-auth.js";
    import {
      getFirestore,
      collection,
      doc,
      setDoc,
      getDocs,
      onSnapshot,
      deleteDoc,
      query,
      orderBy,
      updateDoc
    } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-firestore.js";

    // Firebase config - keep single initialization
    const firebaseConfig = {
      apiKey: "AIzaSyCirWobFVvTyc4ALEw3XMWBCCZlEP3s048",
      authDomain: "newnotes-6942f.firebaseapp.com",
      projectId: "newnotes-6942f"
    };
    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);

    // UI elements
    const themeToggle = document.getElementById('theme-toggle');
    const themeIcon = document.getElementById('theme-icon');
    const themeText = document.getElementById('theme-text');
    const loginModal = document.getElementById('login-modal');
    const settingsModal = document.getElementById('settings-modal');
    const loginBtn = document.getElementById('login-btn');
    const loginClose = document.getElementById('login-close');
    const settingsClose = document.getElementById('settings-close');

    // Theme toggle
    themeToggle.addEventListener('click', () => {
      document.body.classList.toggle('dark-mode');
      const isDark = document.body.classList.contains('dark-mode');
      themeIcon.textContent = isDark ? '☀️' : '🌙';
      themeText.textContent = isDark ? 'Light Mode' : 'Dark Mode';
      localStorage.setItem('darkMode', isDark ? 'true' : 'false');
    });
    if (localStorage.getItem('darkMode') === 'true') {
      document.body.classList.add('dark-mode');
      themeIcon.textContent = '☀️'; themeText.textContent = 'Light Mode';
    }

    // Settings open/close
    loginBtn.onclick = () => loginModal.style.display = 'flex';
    loginClose.onclick = () => loginModal.style.display = 'none';
    settingsClose.onclick = () => settingsModal.style.display = 'none';
    window.onclick = (e) => {
      if (e.target === loginModal) loginModal.style.display = 'none';
      if (e.target === settingsModal) settingsModal.style.display = 'none';
    };

    // Tabs behavior
    const tabs = document.querySelectorAll('.tab');
    tabs.forEach(tab => tab.addEventListener('click', () => {
      tabs.forEach(t => t.classList.remove('active'));
      tab.classList.add('active');
    }));

    // Notebooks & templates
    const emojis = ['📗','📕','📙','📔','🎨','🌸','🌟','🍀','🎯','💎','📘','💝','🍳','✏️'];
    let notebooks = JSON.parse(localStorage.getItem('notebooks')) || [];
    let currentNoteId = null;
    let notebooksUnsub = null; // firestore listener unsubscribe

    // Templates (improved content)
    const templates = {
      'daily-planner': {
        title: 'Weekly Planner',
        emoji: '📅',
        content: (function(){ // return string
          const days = ['Mon','Tue','Wed','Thu','Fri','Sat','Sun'];
          let header = '<h2 style="margin-bottom:6px;">Weekly Planner</h2>';
          header += `<p style="color:#6b7280;margin-top:0;margin-bottom:8px;"><strong>Week of:</strong> ${new Date().toLocaleDateString()}</p>`;
          // week grid
          let table = '<table style="width:100%;border-collapse:collapse;font-size:0.95rem;">';
          table += '<thead><tr><th style="text-align:left;padding:6px;border-bottom:1px solid #e6e6e6;width:110px;">Time</th>';
          for (const d of days) table += `<th style="padding:6px;border-bottom:1px solid #e6e6e6;text-align:left;">${d}</th>`;
          table += '</tr></thead><tbody>';
          const times = ['6am','8am','10am','12pm','2pm','4pm','6pm','8pm'];
          for (const t of times) {
            table += `<tr><td style="padding:6px;border-bottom:1px solid #f1f5f9;font-weight:600;">${t}</td>`;
            for (let i=0;i<7;i++) table += `<td contenteditable="true" style="padding:6px;border-bottom:1px solid #f1f5f9;min-height:28px;"></td>`;
            table += '</tr>';
          }
          table += '</tbody></table>';
          const footer = '<h3 style="margin-top:10px;margin-bottom:6px;">Top Priorities</h3><ul><li contenteditable="true"></li><li contenteditable="true"></li><li contenteditable="true"></li></ul>';
          return header + table + footer;
        })()
      },
      'bullet-journal': {
        title: 'Bullet Journal',
        emoji: '✅',
        content: `
          <h2>Bullet Journal</h2>
          <h3>Rapid Log</h3>
          <ul>
            <li contenteditable="true">• Task: [ ] </li>
            <li contenteditable="true">• Event: </li>
            <li contenteditable="true">• Note: </li>
          </ul>
          <h3>Habit Tracker</h3>
          <p contenteditable="true">Exercise ☐  Read ☐  Meditate ☐  Sleep by 11pm ☐</p>
          <h3>Monthly Collections</h3>
          <p contenteditable="true"></p>
          <h3>Reflection</h3><p contenteditable="true"></p>
        `
      },
      'study-notes': {
        title: 'Study Notes (Cornell)',
        emoji: '📚',
        content: `
          <h2>Study Notes</h2>
          <p><em>Course / Topic:</em> <span contenteditable="true"></span></p>
          <div style="display:flex;gap:12px;">
            <div style="flex:1;">
              <h3 style="margin-bottom:6px;">Notes</h3>
              <div contenteditable="true" style="min-height:160px;border:1px dashed #e6e6e6;padding:8px;border-radius:6px;"></div>
            </div>
            <div style="width:180px;">
              <h3 style="margin-bottom:6px;">Cues / Questions</h3>
              <div contenteditable="true" style="min-height:160px;border:1px dashed #e6e6e6;padding:8px;border-radius:6px;"></div>
            </div>
          </div>
          <h3 style="margin-top:10px;">Summary</h3>
          <div contenteditable="true" style="min-height:60px;border:1px dashed #e6e6e6;padding:8px;border-radius:6px;"></div>
        `
      },
      'budget-tracker': {
        title: 'Budget Tracker',
        emoji: '💰',
        content: `
          <h2>Budget Tracker</h2>
          <p><strong>Month:</strong> ${new Date().toLocaleString('en-US', {month:'long', year:'numeric'})}</p>
          <h3>Income</h3>
          <ul><li contenteditable="true">Source: <strong>$0.00</strong></li></ul>
          <h3>Expenses</h3>
          <table style="width:100%;border-collapse:collapse;">
            <thead><tr><th style="text-align:left;border-bottom:1px solid #ddd;padding:6px;">Item</th><th style="text-align:right;border-bottom:1px solid #ddd;padding:6px;">Amount</th></tr></thead>
            <tbody>
              <tr><td contenteditable="true" style="padding:6px;border-bottom:1px solid #f1f1f1;">Rent</td><td contenteditable="true" style="padding:6px;text-align:right;border-bottom:1px solid #f1f1f1;">$0.00</td></tr>
              <tr><td contenteditable="true" style="padding:6px;border-bottom:1px solid #f1f1f1;">Groceries</td><td contenteditable="true" style="padding:6px;text-align:right;border-bottom:1px solid #f1f1f1;">$0.00</td></tr>
            </tbody>
          </table>
          <h3>Totals</h3>
          <p>Income: <strong>$0.00</strong> | Expenses: <strong>$0.00</strong> | Savings: <strong>$0.00</strong></p>
        `
      },
      'fitness-plan': {
        title: 'Fitness Plan',
        emoji: '🏃',
        content: `
          <h2>Fitness Plan</h2>
          <h3>Weekly Schedule</h3>
          <ul>
            <li contenteditable="true">Monday: Strength</li>
            <li contenteditable="true">Tuesday: Cardio</li>
            <li contenteditable="true">Wednesday: Mobility / Yoga</li>
            <li contenteditable="true">Thursday: Strength</li>
            <li contenteditable="true">Friday: Cardio</li>
            <li contenteditable="true">Saturday: Active Recovery</li>
            <li contenteditable="true">Sunday: Rest</li>
          </ul>
          <h3>Meals</h3><p contenteditable="true">Breakfast: <br/>Lunch: <br/>Dinner: </p>
          <h3>Goals</h3><p contenteditable="true"></p>
          <h3>Progress</h3><p contenteditable="true"></p>
        `
      },
      'blank-canvas': {
        title: 'Blank Canvas',
        emoji: '✏️',
        content: `<h2>Blank Canvas</h2><p contenteditable="true"></p>`
      }
    };

    // Helpers to persist local cache
    function saveLocal() { localStorage.setItem('notebooks', JSON.stringify(notebooks)); }
    function loadLocal() { notebooks = JSON.parse(localStorage.getItem('notebooks')) || []; }

    // Render notebook cards
    function loadNotebooks() {
      const notebookGrid = document.getElementById('notebook-grid');
      const createCard = document.getElementById('create-new');
      // clear and keep create card first
      notebookGrid.innerHTML = '';
      notebookGrid.appendChild(createCard);
      // show notebooks newest-first
      const list = [...notebooks].sort((a,b)=> (b.dateCreated||0) - (a.dateCreated||0));
      list.forEach(notebook => addNotebookCard(notebook));
    }

    function addNotebookCard(notebook) {
      const notebookGrid = document.getElementById('notebook-grid');
      const card = document.createElement('div');
      card.className = 'notebook-card';
      card.dataset.id = notebook.id;
      card.innerHTML = `
        <div class="notebook-icon">${notebook.emoji || '📓'}</div>
        <div class="notebook-title">${notebook.title}</div>
        <div class="notebook-meta">📅 ${notebook.date}</div>
        <div class="notebook-actions">
          <button class="action-btn star-btn" title="Star">⭐</button>
          <button class="action-btn share-btn" title="Share">🔗</button>
          <button class="action-btn delete-btn" title="Delete">🗑️</button>
        </div>
      `;
      // open note except when clicking action btns
      card.addEventListener('click', (e) => {
        if (!e.target.classList.contains('action-btn')) openNote(notebook.id);
      });

      // actions
      const starBtn = card.querySelector('.star-btn');
      const shareBtn = card.querySelector('.share-btn');
      const deleteBtn = card.querySelector('.delete-btn');

      starBtn.onclick = (e)=> { e.stopPropagation(); starBtn.style.transform='scale(1.15)'; setTimeout(()=>starBtn.style.transform='scale(1)',200); }
      shareBtn.onclick = (e)=> { e.stopPropagation(); alert('🔗 Share link copied! (Demo)'); }
      deleteBtn.onclick = async (e)=> {
        e.stopPropagation();
        if (!confirm('🗑️ Move to trash?')) return;
        // remove locally
        notebooks = notebooks.filter(n => n.id !== notebook.id);
        saveLocal();
        loadNotebooks();
        // If signed in, delete from Firestore
        const user = auth.currentUser;
        if (user) {
          try {
            await deleteDoc(doc(db, 'users', user.uid, 'notebooks', notebook.id));
          } catch (err) {
            console.warn('Firestore delete error', err);
          }
        }
      };

      notebookGrid.appendChild(card);
    }

    // Create new manual notebook
    function createNotebook() {
      const title = prompt('📝 Name your notebook:', 'My New Notebook');
      if (!title) return;
      const emoji = emojis[Math.floor(Math.random()*emojis.length)];
      const id = Date.now().toString();
      const notebook = {
        id,
        title,
        emoji,
        content: '',
        date: new Date().toLocaleDateString('en-US', { month:'short', day:'numeric', year:'numeric' }),
        dateCreated: Date.now()
      };
      notebooks.push(notebook);
      saveLocal();
      loadNotebooks();
      // Save to Firestore if signed in
      const user = auth.currentUser;
      if (user) {
        setDoc(doc(db, 'users', user.uid, 'notebooks', id), notebook).catch(err=>console.warn('fs save err', err));
      }
      openNote(id);
    }

    // Create from template (prefill and open)
    async function createNotebookFromTemplate(key) {
      const t = templates[key]; if (!t) return;
      const id = Date.now().toString();
      const notebook = {
        id,
        title: t.title,
        emoji: t.emoji,
        content: t.content,
        date: new Date().toLocaleDateString('en-US', { month:'short', day:'numeric', year:'numeric' }),
        dateCreated: Date.now()
      };
      notebooks.push(notebook);
      saveLocal();
      loadNotebooks();

      // Save to Firestore if signed in
      const user = auth.currentUser;
      if (user) {
        try {
          await setDoc(doc(db, 'users', user.uid, 'notebooks', id), notebook);
        } catch (err) {
          console.warn('fs create err', err);
        }
      }
      openNote(id);
    }

    // Wire template cards to actions
    document.addEventListener('DOMContentLoaded', ()=> {
      document.querySelectorAll('.template-card').forEach(card => {
        card.addEventListener('click', ()=> {
          const key = card.dataset.template;
          createNotebookFromTemplate(key);
        });
      });
    });

    // Wire create buttons
    document.getElementById('create-new').onclick = createNotebook;
    document.getElementById('new-note-btn').onclick = createNotebook;

    // EDITOR
    const homePage = document.querySelector('.home-page');
    const editorPage = document.getElementById('editor-page');
    const backBtn = document.getElementById('back-btn');
    const saveBtn = document.getElementById('save-btn');
    const noteTitleEditor = document.getElementById('note-title-editor');
    const textEditor = document.getElementById('text-editor');
    const saveStatus = document.getElementById('save-status');
    const saveText = document.getElementById('save-text');

    function openNote(noteId) {
      const notebook = notebooks.find(n => n.id === noteId);
      if (!notebook) return;
      currentNoteId = noteId;
      noteTitleEditor.value = notebook.title;
      // Insert content as HTML (templates already contain formatted HTML)
      textEditor.innerHTML = notebook.content || '<p>Start writing your notes here...</p>';
      homePage.classList.add('hidden');
      editorPage.classList.add('active');
      window.scrollTo(0,0);
    }

    async function saveNote() {
      if (!currentNoteId) return;
      const notebook = notebooks.find(n => n.id === currentNoteId);
      if (!notebook) return;
      notebook.title = noteTitleEditor.value || 'Untitled Note';
      notebook.content = textEditor.innerHTML;
      notebook.date = new Date().toLocaleDateString('en-US', { month:'short', day:'numeric', year:'numeric' });
      notebook.dateModified = Date.now();
      saveLocal();
      loadNotebooks();
      // Save to Firestore if signed in
      const user = auth.currentUser;
      if (user) {
        try {
          const ref = doc(db, 'users', user.uid, 'notebooks', notebook.id);
          // use setDoc or updateDoc; setDoc ensures doc exists/created
          await setDoc(ref, notebook);
          // show saved indicator
        } catch (err) {
          console.warn('fs save err', err);
        }
      }
      // UI saved indicator
      saveStatus.classList.add('saved');
      saveText.textContent = 'Saved!';
      setTimeout(()=>{ saveStatus.classList.remove('saved'); saveText.textContent = 'Auto-saved'; }, 1300);
    }

    function closeEditor() { saveNote(); homePage.classList.remove('hidden'); editorPage.classList.remove('active'); currentNoteId = null; window.scrollTo(0,0); }

    // Auto-save every 8s while editing
    setInterval(()=> { if (currentNoteId) saveNote(); }, 8000);

    backBtn.onclick = closeEditor;
    saveBtn.onclick = saveNote;
    noteTitleEditor.addEventListener('blur', saveNote);

    // Logo click to go home
    document.getElementById('logo-home').onclick = ()=> { homePage.classList.remove('hidden'); editorPage.classList.remove('active'); window.scrollTo(0,0); }

    // Load local notebooks initially
    loadLocal(); loadNotebooks();

    // FIRESTORE SYNC: when user signs in, listen to their notebooks collection; otherwise use local storage.
    async function setupFirestoreSync(user) {
      // unsubscribe previous if present
      if (notebooksUnsub) { notebooksUnsub(); notebooksUnsub = null; }
      if (!user) return;
      const colRef = collection(db, 'users', user.uid, 'notebooks');
      const q = query(colRef, orderBy('dateCreated', 'desc'));
      notebooksUnsub = onSnapshot(q, snap => {
        // replace local notebooks with server data (merge local unsynced items optionally)
        const serverNotes = [];
        snap.forEach(docSnap => serverNotes.push(docSnap.data()));
        // keep local-only notes that have not been uploaded (no server counterpart)
        const local = JSON.parse(localStorage.getItem('notebooks')) || [];
        const localOnly = local.filter(l => !serverNotes.some(s => s.id === l.id));
        // merge: server priority, then local-only appended
        notebooks = [...serverNotes, ...localOnly].sort((a,b)=> (b.dateCreated||0)-(a.dateCreated||0));
        saveLocal();
        loadNotebooks();
      }, err => {
        console.warn('onSnapshot error', err);
      });
    }

    // AUTH STATE handling and login actions
    onAuthStateChanged(auth, async (user) => {
      const userName = document.getElementById('user-name');
      const userEmail = document.getElementById('user-email');
      const profileAvatar = document.getElementById('profile-avatar');
      if (user) {
        userName.textContent = user.displayName || (user.email ? user.email.split('@')[0] : 'User');
        userEmail.textContent = user.email || '';
        profileAvatar.textContent = user.photoURL ? '🙂' : '👤';
        loginBtn.textContent = '⚙️ Settings';
        loginBtn.onclick = () => settingsModal.style.display = 'flex';
        // Now set up Firestore listener
        setupFirestoreSync(user);
      } else {
        userName.textContent = 'Guest';
        userEmail.textContent = 'Not signed in';
        profileAvatar.textContent = '👤';
        loginBtn.textContent = '🔐 Login';
        loginBtn.onclick = () => loginModal.style.display = 'flex';
        // Stop firestore sync if any
        if (notebooksUnsub) { notebooksUnsub(); notebooksUnsub = null; }
        // Use local cache only
        loadLocal(); loadNotebooks();
      }
    });

    // Login handlers
    document.getElementById('google-login').onclick = async () => {
      try { await signInWithPopup(auth, new GoogleAuthProvider()); loginModal.style.display='none'; }
      catch (err) { alert('❌ Login failed: ' + err.message); console.error(err); }
    };
    document.getElementById('microsoft-login').onclick = async () => {
      try { const provider = new OAuthProvider('microsoft.com'); await signInWithPopup(auth, provider); loginModal.style.display='none'; }
      catch (err) { alert('❌ Login failed: ' + err.message); console.error(err); }
    };
    document.getElementById('email-login').onclick = async () => {
      const email = prompt('✉️ Enter your email:');
      if (!email) return;
      const password = prompt('🔒 Enter your password:');
      if (!password) return;
      try {
        await signInWithEmailAndPassword(auth, email, password);
        loginModal.style.display='none';
      } catch (error) {
        if (error.code === 'auth/user-not-found') {
          if (confirm('Create new account?')) {
            try { await createUserWithEmailAndPassword(auth, email, password); loginModal.style.display='none'; }
            catch(e){ alert('❌ Create account failed: ' + e.message); }
          }
        } else {
          alert('❌ Login failed: ' + error.message);
        }
      }
    };

    // Delete account handler
    document.getElementById('delete-account').onclick = async () => {
      if (!auth.currentUser) { alert('⚠️ Please sign in first'); return; }
      if (!confirm('⚠️ Delete your account permanently? This cannot be undone!')) return;
      try {
        await deleteUser(auth.currentUser);
        alert('✅ Account deleted successfully');
        settingsModal.style.display='none';
      } catch (error) {
        if (error.code === 'auth/requires-recent-login') {
          const email = prompt('✉️ Re-enter your email:');
          const password = prompt('🔒 Re-enter your password:');
          if (email && password) {
            const credential = EmailAuthProvider.credential(email, password);
            try {
              await reauthenticateWithCredential(auth.currentUser, credential);
              await deleteUser(auth.currentUser);
              alert('✅ Account deleted successfully');
              settingsModal.style.display='none';
            } catch (reauthErr) { alert('❌ Re-authentication failed: ' + reauthErr.message); }
          }
        } else {
          alert('❌ Error: ' + error.message);
        }
      }
    };

    // STYLES selection
    const styleOptions = document.getElementById('style-options');
    function applyStyle(styleKey) {
      // remove previous style-* classes
      document.body.classList.remove('style-minimal','style-dark-compact','style-pastel');
      if (styleKey && styleKey !== 'default') document.body.classList.add(styleKey);
      // mark active button
      document.querySelectorAll('.style-option').forEach(el => el.classList.toggle('active', el.dataset.style === styleKey));
      localStorage.setItem('uiStyle', styleKey || 'default');
    }
    // load saved style
    const savedStyle = localStorage.getItem('uiStyle') || 'default';
    // mark options and set listeners
    document.querySelectorAll('.style-option').forEach(el => {
      el.classList.toggle('active', el.dataset.style === savedStyle);
      el.addEventListener('click', ()=> applyStyle(el.dataset.style));
    });
    applyStyle(savedStyle);

    // Ensure saving changes to Firestore when editing title or content happens
    // We already save on blur and on interval. Optionally listen for input events too.
    // Persistence is handled in saveNote() which writes to Firestore when signed in.

    // Accessibility: allow Escape to close modals
    window.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        loginModal.style.display = 'none';
        settingsModal.style.display = 'none';
      }
    });
  </script>
</body>
</html>
