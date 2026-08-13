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
    }
    body.style-dark-compact {
      --bg-gradient: linear-gradient(135deg, #0f1724 0%, #0b1220 100%);
      --bg-light: #0b1220;
      --text: #e6eef8;
      --card-bg: #071129;
      --shadow: rgba(0,0,0,0.6);
    }
    body.style-pastel {
      --bg-gradient: linear-gradient(135deg, #f9f2ff 0%, #fff7f2 100%);
      --bg-light: #fffaf6;
      --text: #2d3748;
      --card-bg: #ffffff;
      --shadow: rgba(0, 0, 0, 0.04);
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
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:0.75rem;
    }

    .logo { font-size:1.6rem; font-weight:700; font-family:var(--font-accent); display:flex; gap:0.5rem; cursor:pointer; }
    .logo-emoji { animation:bounce 2s infinite; }
    @keyframes bounce { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-6px)} }

    .header-controls { display:flex; gap:0.75rem; align-items:center; }
    .btn { padding:0.6rem 1.2rem; border:none; border-radius:50px; font-weight:600; cursor:pointer; transition:all .18s; }
    .btn-primary{ background:var(--accent-pink); color:white; }
    .btn-secondary{ background:white; color:var(--accent-blue); }
    .btn-success{ background:var(--accent-green); color:white; }

    .theme-toggle{ background:rgba(255,255,255,0.12); border-radius:50px; padding:.38rem .8rem; display:flex; gap:.4rem; align-items:center; cursor:pointer; }

    .container{ max-width:1200px; margin:0 auto; padding:1.25rem; }

    .tabs{ display:flex; gap:.75rem; margin-bottom:1.5rem; }
    .tab{ padding:.8rem 1.2rem; background:var(--card-bg); border-radius:12px; cursor:pointer; font-weight:600; box-shadow:0 2px 8px var(--shadow); }
    .tab.active{ background:var(--bg-gradient); color:white; }

    .notebook-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(220px,1fr)); gap:1rem; margin-bottom:1.2rem; }
    .notebook-card{ background:var(--card-bg); border-radius:12px; padding:1rem; box-shadow:0 6px 18px var(--shadow); cursor:pointer; }
    .notebook-card:hover{ transform:translateY(-6px); }
    .notebook-icon{ font-size:2rem; margin-bottom:0.5rem; }
    .notebook-title{ font-weight:700; margin-bottom:0.25rem; }
    .notebook-meta{ color:#7a8797; font-size:.9rem; }

    .notebook-actions{ display:flex; gap:.4rem; justify-content:flex-end; margin-top:.4rem; }
    .action-btn{ padding:.4rem; border-radius:6px; border:none; cursor:pointer; background:var(--bg-light); }

    .create-card{ display:flex; align-items:center; justify-content:center; flex-direction:column; min-height:160px; border-radius:12px; background:linear-gradient(135deg,var(--accent-pink),var(--accent-purple)); color:white; cursor:pointer; }

    .template-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(280px,1fr)); gap:1rem; }
    .template-card{ background:var(--card-bg); border-radius:12px; padding:1rem; box-shadow:0 6px 18px var(--shadow); cursor:pointer; border-left:6px solid; display:flex; flex-direction:column; gap:.5rem; }
    .template-title{ font-weight:700; }
    .template-desc{ color:#718096; }

    .template-card:nth-child(1){ border-color:var(--accent-pink); }
    .template-card:nth-child(2){ border-color:var(--accent-blue); }
    .template-card:nth-child(3){ border-color:var(--accent-yellow); }
    .template-card:nth-child(4){ border-color:var(--accent-green); }
    .template-card:nth-child(5){ border-color:var(--accent-purple); }
    .template-card:nth-child(6){ border-color:var(--accent-pink); }

    .modal{ display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,.45); z-index:1000; align-items:center; justify-content:center; }
    .modal-content{ background:var(--card-bg); border-radius:12px; padding:1rem; width:90%; max-width:520px; box-shadow:0 12px 40px var(--shadow); }

    .settings-menu{ list-style:none; padding-left:0; margin-top:.6rem; }
    .settings-item{ padding:.6rem; background:var(--bg-light); border-radius:8px; margin-bottom:.4rem; cursor:pointer; }

    .style-options{ display:flex; gap:.5rem; flex-wrap:wrap; margin-top:.5rem; }
    .style-option{ padding:.45rem .7rem; border-radius:8px; cursor:pointer; background:var(--bg-light); border:1px solid rgba(0,0,0,.06); }
    .style-option.active{ box-shadow:0 6px 18px var(--shadow); transform:translateY(-3px); border-color:var(--accent-blue); }

    .footer{ text-align:center; padding:1.5rem; background:var(--card-bg); margin-top:1.5rem; border-top:1px solid rgba(0,0,0,.06); }

    /* Editor */
    .editor-page{ display:none; min-height:100vh; }
    .editor-page.active{ display:block; }
    .editor-header{ background:var(--bg-gradient); padding:.9rem 1rem; display:flex; justify-content:space-between; align-items:center; gap:.5rem; color:white; }
    .editor-title-input{ background:rgba(255,255,255,.12); border:1px solid transparent; padding:.45rem .6rem; border-radius:8px; color:white; font-weight:700; }
    .editor-container{ max-width:900px; margin:1rem auto; padding:1rem; }
    .editor-toolbar{ background:var(--card-bg); padding:.6rem; border-radius:8px; display:flex; gap:.4rem; margin-bottom:.8rem; box-shadow:0 6px 18px var(--shadow); align-items:center; }
    .editor-content{ background:var(--card-bg); border-radius:8px; padding:0; min-height:420px; box-shadow:0 6px 18px var(--shadow); overflow:hidden; position:relative; }
    .text-editor{ width:100%; min-height:420px; border:none; outline:none; font-family:var(--font-main); font-size:1rem; line-height:1.6; color:var(--text); padding:1.25rem; background:transparent; }
    .text-editor:focus{ outline:2px solid rgba(0,0,0,.06); }

    /* Paper style overlays applied to .editor-content */
    .paper-lined .text-editor { background-image:
      repeating-linear-gradient( to bottom, transparent 0px, transparent 28px, rgba(0,0,0,0.05) 29px );
      background-size:100% 28px;
    }
    .paper-grid .text-editor {
      background-image:
        linear-gradient(to right, rgba(0,0,0,0.04) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(0,0,0,0.04) 1px, transparent 1px);
      background-size: 40px 40px, 40px 40px;
    }
    .paper-dotted .text-editor {
      background-image:
        radial-gradient(rgba(0,0,0,0.06) 1px, transparent 1px);
      background-size: 20px 20px;
    }

    @media (max-width:900px) { .template-grid{ grid-template-columns:1fr 1fr; } }
    @media (max-width:560px) { .template-grid{ grid-template-columns:1fr; } .notebook-grid{ grid-template-columns:repeat(auto-fill, minmax(160px,1fr)); } }

  </style>
</head>
<body>
  <div class="home-page">
    <header class="header">
      <div class="header-content">
        <div class="logo" id="logo-home"><span class="logo-emoji">✨</span><span id="app-title">New Notes</span></div>
        <div class="header-controls">
          <button class="btn btn-primary" id="new-note-btn">➕ New Note</button>
          <button class="btn btn-secondary" id="login-btn">🔐 Login</button>
          <div class="theme-toggle" id="theme-toggle"><span id="theme-icon">🌙</span><span id="theme-text">Dark Mode</span></div>
        </div>
      </div>
    </header>

    <div class="container">
      <div class="tabs">
        <div class="tab active" data-tab="all">📚 All Notes</div>
        <div class="tab" data-tab="favorites">⭐ Favorites</div>
        <div class="tab" data-tab="shared">👥 Shared</div>
        <div class="tab" data-tab="templates">🎨 Templates</div>
      </div>

      <section id="notebooks-section">
        <h2 class="section-title">📖 My Notebooks</h2>
        <div class="notebook-grid" id="notebook-grid">
          <!-- Create New Card is kept in DOM so we never lose its listeners -->
          <div class="notebook-card create-card" id="create-new">
            <div class="create-icon">➕</div>
            <div class="create-text">Create New</div>
          </div>
        </div>
      </section>

      <section id="templates-section">
        <h2 class="section-title">🎨 Popular Templates</h2>
        <div class="template-grid" id="template-grid">
          <div class="template-card" data-template="daily-planner"><div class="template-emoji">📅</div><h3 class="template-title">Weekly Planner</h3><p class="template-desc">Weekly grid with time blocks for planning.</p></div>
          <div class="template-card" data-template="bullet-journal"><div class="template-emoji">✅</div><h3 class="template-title">Bullet Journal</h3><p class="template-desc">Rapid logs, tasks, habit trackers and reflections.</p></div>
          <div class="template-card" data-template="study-notes"><div class="template-emoji">📚</div><h3 class="template-title">Study Notes (Cornell)</h3><p class="template-desc">Notes and cue column with summary area.</p></div>
          <div class="template-card" data-template="budget-tracker"><div class="template-emoji">💰</div><h3 class="template-title">Budget Tracker</h3><p class="template-desc">Income, expenses and totals for a month.</p></div>
          <div class="template-card" data-template="fitness-plan"><div class="template-emoji">🏃</div><h3 class="template-title">Fitness Plan</h3><p class="template-desc">Workout schedule, meals and progress.</p></div>
          <div class="template-card" data-template="blank-canvas"><div class="template-emoji">✏️</div><h3 class="template-title">Blank Canvas</h3><p class="template-desc">A clean blank page to start writing or sketching.</p></div>
        </div>
      </section>
    </div>

    <footer class="footer">
      <p>Made with <span class="footer-heart">💖</span> by New Notes</p>
      <p style="color:#718096;margin-top:.3rem;">© 2026 • Keep your thoughts organized!</p>
    </footer>
  </div>

  <!-- EDITOR PAGE -->
  <div class="editor-page" id="editor-page">
    <div class="editor-header">
      <div style="display:flex;align-items:center;gap:.6rem;">
        <button class="btn btn-secondary" id="back-btn">←</button>
        <input type="text" class="editor-title-input" id="note-title-editor" placeholder="Untitled Note" />
      </div>
      <div style="display:flex;align-items:center;gap:.6rem;">
        <label style="color:white;font-weight:600;font-size:.9rem;">Page:</label>
        <select id="page-style-select" style="padding:.35rem .5rem;border-radius:8px;border:none;">
          <option value="blank">Blank</option>
          <option value="lined">Lined</option>
          <option value="grid">Grid</option>
          <option value="dotted">Dotted</option>
        </select>
        <div class="save-status" id="save-status" style="background:rgba(255,255,255,.12);padding:.4rem .7rem;border-radius:999px;color:white;">💾 <span id="save-text">Auto-saved</span></div>
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

      <div class="editor-content" id="editor-content">
        <div class="text-editor" id="text-editor" contenteditable="true" spellcheck="true">Start writing your notes here...</div>
      </div>
    </div>
  </div>

  <!-- LOGIN MODAL -->
  <div class="modal" id="login-modal">
    <div class="modal-content">
      <div style="display:flex;justify-content:space-between;align-items:center;">
        <h3>🔐 Sign In</h3>
        <div id="login-close" style="cursor:pointer;">×</div>
      </div>
      <div style="margin-top:.5rem;">
        <button id="google-login" class="auth-btn" style="width:100%;margin:.4rem 0;padding:.6rem;background:#4285f4;color:#fff;border-radius:8px;border:none;">🔵 Continue with Google</button>
        <button id="microsoft-login" class="auth-btn" style="width:100%;margin:.4rem 0;padding:.6rem;background:#00a4ef;color:#fff;border-radius:8px;border:none;">🔷 Continue with Microsoft</button>
        <button id="email-login" class="auth-btn" style="width:100%;margin:.4rem 0;padding:.6rem;background:var(--accent-purple);color:#fff;border-radius:8px;border:none;">✉️ Email / Password</button>
        <p style="color:#6b7380;font-size:.9rem;margin-top:.4rem;">Signed in users keep notes synced across devices (Firestore required).</p>
      </div>
    </div>
  </div>

  <!-- SETTINGS MODAL -->
  <div class="modal" id="settings-modal">
    <div class="modal-content">
      <div style="display:flex;justify-content:space-between;align-items:center;">
        <h3>⚙️ Settings</h3>
        <div id="settings-close" style="cursor:pointer;">×</div>
      </div>

      <div style="margin-top:.6rem;">
        <div style="display:flex;gap:.8rem;align-items:center;">
          <div id="profile-avatar" style="font-size:2rem;">👤</div>
          <div><div id="user-name" style="font-weight:700;">Guest</div><div id="user-email" style="color:#718096;font-size:.95rem;">Not signed in</div></div>
        </div>

        <div style="margin-top:.8rem;">
          <div style="font-weight:700;margin-bottom:.4rem;">Interface Style</div>
          <div class="style-options" id="style-options">
            <div class="style-option" data-style="default">Cute (Default)</div>
            <div class="style-option" data-style="style-minimal">Minimal</div>
            <div class="style-option" data-style="style-dark-compact">Dark Compact</div>
            <div class="style-option" data-style="style-pastel">Pastel</div>
          </div>
        </div>

        <ul class="settings-menu">
          <li class="settings-item">📝 Manage Templates</li>
          <li class="settings-item">⚙️ Preferences</li>
          <li class="settings-item">❓ Help & Support</li>
          <li class="settings-item">ℹ️ About</li>
          <li class="settings-item" id="delete-account" style="color:var(--accent-pink);">🗑️ Delete Account</li>
        </ul>
      </div>
    </div>
  </div>

  <script type="module">
    // Firebase imports
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
      onSnapshot,
      deleteDoc,
      query,
      orderBy
    } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-firestore.js";

    // FIREBASE CONFIG - keep single initialization
    const firebaseConfig = {
      apiKey: "AIzaSyCirWobFVvTyc4ALEw3XMWBCCZlEP3s048",
      authDomain: "newnotes-6942f.firebaseapp.com",
      projectId: "newnotes-6942f"
    };
    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);

    // UI references
    const themeToggle = document.getElementById('theme-toggle');
    const themeIcon = document.getElementById('theme-icon');
    const themeText = document.getElementById('theme-text');
    const loginModal = document.getElementById('login-modal');
    const settingsModal = document.getElementById('settings-modal');
    const loginBtn = document.getElementById('login-btn');
    const loginClose = document.getElementById('login-close');
    const settingsClose = document.getElementById('settings-close');

    // Editor refs
    const homePage = document.querySelector('.home-page');
    const editorPage = document.getElementById('editor-page');
    const backBtn = document.getElementById('back-btn');
    const saveBtn = document.getElementById('save-btn');
    const noteTitleEditor = document.getElementById('note-title-editor');
    const textEditor = document.getElementById('text-editor');
    const editorContent = document.getElementById('editor-content');
    const saveStatus = document.getElementById('save-status');
    const saveText = document.getElementById('save-text');
    const pageStyleSelect = document.getElementById('page-style-select');

    // Other refs
    const createNewBtn = document.getElementById('create-new');
    const notebookGrid = document.getElementById('notebook-grid');
    const templateGrid = document.getElementById('template-grid');

    // state
    const emojis = ['📗','📕','📙','📔','🎨','🌸','🌟','🍀','🎯','💎','📘','💝','🍳','✏️'];
    let notebooks = []; // in-memory
    let currentNoteId = null;
    let notebooksUnsub = null;

    // Templates improved
    const templates = {
      'daily-planner': {
        title: 'Weekly Planner',
        emoji: '📅',
        content: (function(){
          const days = ['Mon','Tue','Wed','Thu','Fri','Sat','Sun'];
          let html = '<h2>Weekly Planner</h2><p style="color:#6b7280;margin-top:0;margin-bottom:8px;"><strong>Week of:</strong> ' + new Date().toLocaleDateString() + '</p>';
          html += '<table style="width:100%;border-collapse:collapse;font-size:0.95rem;">';
          html += '<thead><tr><th style="text-align:left;padding:6px;border-bottom:1px solid #e6e6e6;width:110px;">Time</th>';
          for (const d of days) html += `<th style="padding:6px;border-bottom:1px solid #e6e6e6;text-align:left;">${d}</th>`;
          html += '</tr></thead><tbody>';
          const times = ['6am','8am','10am','12pm','2pm','4pm','6pm','8pm'];
          for (const t of times){
            html += `<tr><td style="padding:6px;border-bottom:1px solid #f1f5f9;font-weight:600;">${t}</td>`;
            for (let i=0;i<7;i++) html += `<td contenteditable="true" style="padding:6px;border-bottom:1px solid #f1f5f9;min-height:28px;"></td>`;
            html += '</tr>';
          }
          html += '</tbody></table>';
          html += '<h3 style="margin-top:10px;margin-bottom:6px;">Top Priorities</h3><ul><li contenteditable="true"></li><li contenteditable="true"></li><li contenteditable="true"></li></ul>';
          return html;
        })()
      },
      'bullet-journal': {
        title: 'Bullet Journal',
        emoji: '✅',
        content: `<h2>Bullet Journal</h2><h3>Rapid Log</h3><ul><li contenteditable="true">• Task: [ ] </li><li contenteditable="true">• Event: </li><li contenteditable="true">• Note: </li></ul><h3>Habit Tracker</h3><p contenteditable="true">Exercise ☐ Read ☐ Meditate ☐ Sleep by 11pm ☐</p><h3>Reflection</h3><p contenteditable="true"></p>`
      },
      'study-notes': {
        title: 'Study Notes (Cornell)',
        emoji: '📚',
        content: `<h2>Study Notes</h2><p><em>Course / Topic:</em> <span contenteditable="true"></span></p><div style="display:flex;gap:12px;"><div style="flex:1;"><h3>Notes</h3><div contenteditable="true" style="min-height:160px;border:1px dashed #e6e6e6;padding:8px;border-radius:6px;"></div></div><div style="width:180px;"><h3>Cues / Questions</h3><div contenteditable="true" style="min-height:160px;border:1px dashed #e6e6e6;padding:8px;border-radius:6px;"></div></div></div><h3>Summary</h3><div contenteditable="true" style="min-height:60px;border:1px dashed #e6e6e6;padding:8px;border-radius:6px;"></div>`
      },
      'budget-tracker': {
        title: 'Budget Tracker',
        emoji: '💰',
        content: `<h2>Budget Tracker</h2><p><strong>Month:</strong> ${new Date().toLocaleString('en-US',{month:'long',year:'numeric'})}</p><h3>Income</h3><ul><li contenteditable="true">Source: <strong>$0.00</strong></li></ul><h3>Expenses</h3><table style="width:100%;border-collapse:collapse;"><thead><tr><th style="text-align:left;border-bottom:1px solid #ddd;padding:6px;">Item</th><th style="text-align:right;border-bottom:1px solid #ddd;padding:6px;">Amount</th></tr></thead><tbody><tr><td contenteditable="true" style="padding:6px;border-bottom:1px solid #f1f1f1;">Rent</td><td contenteditable="true" style="padding:6px;text-align:right;border-bottom:1px solid #f1f1f1;">$0.00</td></tr><tr><td contenteditable="true" style="padding:6px;border-bottom:1px solid #f1f1f1;">Groceries</td><td contenteditable="true" style="padding:6px;text-align:right;border-bottom:1px solid #f1f1f1;">$0.00</td></tr></tbody></table><h3>Totals</h3><p>Income: <strong>$0.00</strong> | Expenses: <strong>$0.00</strong> | Savings: <strong>$0.00</strong></p>`
      },
      'fitness-plan': {
        title: 'Fitness Plan',
        emoji: '🏃',
        content: `<h2>Fitness Plan</h2><h3>Weekly Schedule</h3><ul><li contenteditable="true">Monday: Strength</li><li contenteditable="true">Tuesday: Cardio</li><li contenteditable="true">Wednesday: Mobility / Yoga</li><li contenteditable="true">Thursday: Strength</li><li contenteditable="true">Friday: Cardio</li><li contenteditable="true">Saturday: Active Recovery</li><li contenteditable="true">Sunday: Rest</li></ul><h3>Meals</h3><p contenteditable="true">Breakfast:<br/>Lunch:<br/>Dinner:</p><h3>Goals</h3><p contenteditable="true"></p><h3>Progress</h3><p contenteditable="true"></p>`
      },
      'blank-canvas': {
        title: 'Blank Canvas',
        emoji: '✏️',
        content: `<h2>Blank Canvas</h2><p contenteditable="true"></p>`
      }
    };

    // DOM utility
    function $id(id){ return document.getElementById(id); }

    // Save / load local cache
    function saveLocal(){ localStorage.setItem('notebooks', JSON.stringify(notebooks)); }
    function loadLocal(){ notebooks = JSON.parse(localStorage.getItem('notebooks')) || []; }

    // Keep create-new element intact and clear other notebook cards
    function clearNotebookGridKeepCreate(){
      const createCard = $id('create-new');
      Array.from(notebookGrid.children).forEach(child => {
        if (child !== createCard) child.remove();
      });
    }

    function loadNotebooks(){
      clearNotebookGridKeepCreate();
      const list = [...notebooks].sort((a,b) => (b.dateCreated||0) - (a.dateCreated||0));
      for (const notebook of list) addNotebookCard(notebook);
    }

    function addNotebookCard(notebook){
      if (notebookGrid.querySelector(`[data-id="${notebook.id}"]`)) return;
      const card = document.createElement('div');
      card.className = 'notebook-card';
      card.dataset.id = notebook.id;
      card.innerHTML = `
        <div class="notebook-icon">${notebook.emoji || '📓'}</div>
        <div class="notebook-title">${sanitize(notebook.title)}</div>
        <div class="notebook-meta">📅 ${sanitize(notebook.date || '')}</div>
        <div class="notebook-actions">
          <button class="action-btn star-btn" title="Star">⭐</button>
          <button class="action-btn share-btn" title="Share">🔗</button>
          <button class="action-btn delete-btn" title="Delete">🗑️</button>
        </div>
      `;
      card.addEventListener('click', (e) => {
        if (!e.target.classList.contains('action-btn')) openNote(notebook.id);
      });
      const starBtn = card.querySelector('.star-btn');
      const shareBtn = card.querySelector('.share-btn');
      const deleteBtn = card.querySelector('.delete-btn');

      starBtn.onclick = (e) => { e.stopPropagation(); starBtn.style.transform='scale(1.12)'; setTimeout(()=>starBtn.style.transform='scale(1)',150); };
      shareBtn.onclick = (e) => { e.stopPropagation(); alert('🔗 Share link copied! (Demo)'); };
      deleteBtn.onclick = async (e) => {
        e.stopPropagation();
        if (!confirm('🗑️ Delete this note?')) return;
        notebooks = notebooks.filter(n => n.id !== notebook.id);
        saveLocal();
        loadNotebooks();
        const user = auth.currentUser;
        if (user) {
          try { await deleteDoc(doc(db, 'users', user.uid, 'notebooks', notebook.id)); }
          catch(err){ console.warn('Firestore delete error', err); }
        }
      };

      notebookGrid.appendChild(card);
    }

    // sanitize for titles/dates
    function sanitize(str){ return String(str).replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

    function createNotebook(){
      const title = prompt('📝 Name your notebook:', 'My New Notebook');
      if (!title) return;
      const emoji = emojis[Math.floor(Math.random()*emojis.length)];
      const id = Date.now().toString();
      const notebook = {
        id,
        title,
        emoji,
        content: '<p></p>',
        pageStyle: 'blank',
        date: new Date().toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'}),
        dateCreated: Date.now()
      };
      notebooks.push(notebook);
      saveLocal();
      loadNotebooks();
      const user = auth.currentUser;
      if (user) {
        setDoc(doc(db, 'users', user.uid, 'notebooks', id), notebook).catch(err => console.warn('fs save err', err));
      }
      openNote(id);
    }

    async function createNotebookFromTemplate(key){
      const t = templates[key]; if (!t) return;
      const id = Date.now().toString();
      const notebook = {
        id,
        title: t.title,
        emoji: t.emoji,
        content: t.content,
        pageStyle: 'blank',
        date: new Date().toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'}),
        dateCreated: Date.now()
      };
      notebooks.push(notebook);
      saveLocal();
      loadNotebooks();
      const user = auth.currentUser;
      if (user) {
        try { await setDoc(doc(db, 'users', user.uid, 'notebooks', id), notebook); }
        catch (err) { console.warn('fs create err', err); }
      }
      openNote(id);
    }

    // Apply page style (blank, lined, grid, dotted)
    function applyPageStyle(style){
      editorContent.classList.remove('paper-lined','paper-grid','paper-dotted');
      if (style === 'lined') editorContent.classList.add('paper-lined');
      else if (style === 'grid') editorContent.classList.add('paper-grid');
      else if (style === 'dotted') editorContent.classList.add('paper-dotted');
      if (pageStyleSelect) pageStyleSelect.value = style || 'blank';
    }

    function openNote(noteId){
      const notebook = notebooks.find(n => n.id === noteId);
      if (!notebook) { alert('Note not found'); return; }
      currentNoteId = noteId;
      noteTitleEditor.value = notebook.title || 'Untitled Note';
      textEditor.innerHTML = notebook.content || '<p></p>';
      applyPageStyle(notebook.pageStyle || 'blank');
      homePage.classList.add('hidden'); editorPage.classList.add('active');
      window.scrollTo(0,0);
    }

    async function saveNote(){
      if (!currentNoteId) return;
      const notebook = notebooks.find(n => n.id === currentNoteId);
      if (!notebook) return;
      notebook.title = noteTitleEditor.value || 'Untitled Note';
      notebook.content = textEditor.innerHTML;
      notebook.pageStyle = pageStyleSelect.value || 'blank';
      notebook.date = new Date().toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'});
      notebook.dateModified = Date.now();
      saveLocal();
      loadNotebooks();
      const user = auth.currentUser;
      if (user) {
        try { await setDoc(doc(db, 'users', user.uid, 'notebooks', notebook.id), notebook); }
        catch(err){ console.warn('fs save err', err); }
      }
      saveStatus.classList.add('saved');
      saveText.textContent = 'Saved!';
      setTimeout(()=>{ saveStatus.classList.remove('saved'); saveText.textContent = 'Auto-saved'; }, 1000);
    }

    function closeEditor(){ saveNote(); homePage.classList.remove('hidden'); editorPage.classList.remove('active'); currentNoteId = null; window.scrollTo(0,0); }

    // Initialization after DOM ready
    document.addEventListener('DOMContentLoaded', () => {
      loadLocal();
      loadNotebooks();

      // create new
      createNewBtn.addEventListener('click', createNotebook);
      $id('new-note-btn').addEventListener('click', createNotebook);

      // templates via delegation
      templateGrid.addEventListener('click', (e) => {
        const card = e.target.closest('.template-card');
        if (!card) return;
        const key = card.dataset.template;
        createNotebookFromTemplate(key);
      });

      // editor controls
      backBtn.addEventListener('click', closeEditor);
      saveBtn.addEventListener('click', saveNote);
      pageStyleSelect.addEventListener('change', () => {
        const style = pageStyleSelect.value;
        applyPageStyle(style);
        if (currentNoteId){
          const n = notebooks.find(x=>x.id===currentNoteId);
          if (n){ n.pageStyle = style; saveLocal(); const user = auth.currentUser; if (user) setDoc(doc(db,'users',user.uid,'notebooks',n.id),n).catch(e=>console.warn(e)); }
        }
      });

      // theme toggle
      themeToggle.addEventListener('click', () => {
        document.body.classList.toggle('dark-mode');
        const isDark = document.body.classList.contains('dark-mode');
        themeIcon.textContent = isDark ? '☀️' : '🌙';
        themeText.textContent = isDark ? 'Light Mode' : 'Dark Mode';
        localStorage.setItem('darkMode', isDark ? 'true' : 'false');
      });
      if (localStorage.getItem('darkMode') === 'true'){ document.body.classList.add('dark-mode'); themeIcon.textContent='☀️'; themeText.textContent='Light Mode'; }

      // settings and login modal wiring
      loginBtn.onclick = () => { loginModal.style.display = 'flex'; };
      loginClose.onclick = () => { loginModal.style.display = 'none'; };
      settingsClose.onclick = () => { settingsModal.style.display = 'none'; };
      window.onclick = (e) => { if (e.target === loginModal) loginModal.style.display='none'; if (e.target === settingsModal) settingsModal.style.display='none'; };
      $id('google-login').onclick = async () => {
        try { await signInWithPopup(auth, new GoogleAuthProvider()); loginModal.style.display='none'; }
        catch(err){ alert('Login failed: ' + (err.message || err)); console.error(err); }
      };
      $id('microsoft-login').onclick = async () => {
        try { const provider = new OAuthProvider('microsoft.com'); await signInWithPopup(auth, provider); loginModal.style.display='none'; }
        catch(err){ alert('Login failed: ' + (err.message || err)); console.error(err); }
      };
      $id('email-login').onclick = async () => {
        const email = prompt('✉️ Enter your email:');
        if (!email) return;
        const password = prompt('🔒 Enter your password:');
        if (!password) return;
        try {
          await signInWithEmailAndPassword(auth, email, password);
          loginModal.style.display='none';
        } catch (error) {
          if (error.code === 'auth/user-not-found') {
            if (confirm('No account found. Create one?')) {
              try { await createUserWithEmailAndPassword(auth, email, password); loginModal.style.display='none'; }
              catch(e){ alert('Create account failed: ' + (e.message || e)); }
            }
          } else {
            alert('Sign-in failed: ' + (error.message || error));
          }
        }
      };

      // Delete account
      $id('delete-account').addEventListener('click', async () => {
        if (!auth.currentUser) { alert('Please sign in first'); return; }
        if (!confirm('⚠️ Delete your account and all synced notes? This cannot be undone.')) return;
        try {
          await deleteUser(auth.currentUser);
          alert('Account deleted');
          settingsModal.style.display = 'none';
        } catch (error) {
          if (error.code === 'auth/requires-recent-login') {
            const email = prompt('✉️ Re-enter your email:');
            const password = prompt('🔒 Re-enter your password:');
            if (email && password){
              const credential = EmailAuthProvider.credential(email, password);
              try {
                await reauthenticateWithCredential(auth.currentUser, credential);
                await deleteUser(auth.currentUser);
                alert('Account deleted');
                settingsModal.style.display='none';
              } catch (reauthErr){ alert('Re-auth failed: ' + (reauthErr.message || reauthErr)); }
            }
          } else {
            alert('Delete account failed: ' + (error.message || error));
          }
        }
      });

      // style options in settings
      const savedStyle = localStorage.getItem('uiStyle') || 'default';
      document.querySelectorAll('.style-option').forEach(el => {
        el.classList.toggle('active', el.dataset.style === savedStyle);
        el.addEventListener('click', () => {
          document.body.classList.remove('style-minimal','style-dark-compact','style-pastel');
          if (el.dataset.style && el.dataset.style !== 'default') document.body.classList.add(el.dataset.style);
          document.querySelectorAll('.style-option').forEach(x=>x.classList.remove('active'));
          el.classList.add('active');
          localStorage.setItem('uiStyle', el.dataset.style);
        });
      });
      if (savedStyle && savedStyle !== 'default') document.body.classList.add(savedStyle);

      // keyboard: Esc closes modals
      window.addEventListener('keydown', (e) => { if (e.key === 'Escape'){ loginModal.style.display='none'; settingsModal.style.display='none'; } });

      // auto-save periodically
      setInterval(()=>{ if (currentNoteId) saveNote(); }, 8000);

      // ensure clicking logo goes home
      $id('logo-home').addEventListener('click', ()=> { homePage.classList.remove('hidden'); editorPage.classList.remove('active'); window.scrollTo(0,0); });

      // Template: ensure page style select updates when changing
      pageStyleSelect.addEventListener('change', ()=> applyPageStyle(pageStyleSelect.value));
    }); // DOMContentLoaded end

    // Firestore sync: when signed in, listen to user's notebooks collection
    onAuthStateChanged(auth, (user) => {
      const userNameEl = $id('user-name');
      const userEmailEl = $id('user-email');
      const profileAvatar = $id('profile-avatar');
      if (user){
        userNameEl.textContent = user.displayName || (user.email?user.email.split('@')[0]:'User');
        userEmailEl.textContent = user.email || '';
        profileAvatar.textContent = user.photoURL ? '🙂' : '👤';
        loginBtn.textContent = '⚙️ Settings';
        loginBtn.onclick = () => settingsModal.style.display = 'flex';
        if (notebooksUnsub) { notebooksUnsub(); notebooksUnsub = null; }
        try {
          const q = query(collection(db, 'users', user.uid, 'notebooks'), orderBy('dateCreated','desc'));
          notebooksUnsub = onSnapshot(q, snap => {
            const server = [];
            snap.forEach(s => server.push(s.data()));
            const local = JSON.parse(localStorage.getItem('notebooks')) || [];
            const localOnly = local.filter(l => !server.some(s => s.id === l.id));
            notebooks = [...server, ...localOnly].sort((a,b)=> (b.dateCreated||0)-(a.dateCreated||0));
            saveLocal();
            loadNotebooks();
          }, err => {
            console.warn('onSnapshot error', err);
            loadLocal(); loadNotebooks();
          });
        } catch (err) { console.warn('subscribe error', err); loadLocal(); loadNotebooks(); }
      } else {
        userNameEl.textContent = 'Guest';
        userEmailEl.textContent = 'Not signed in';
        profileAvatar.textContent = '👤';
        loginBtn.textContent = '🔐 Login';
        loginBtn.onclick = () => loginModal.style.display = 'flex';
        if (notebooksUnsub) { notebooksUnsub(); notebooksUnsub = null; }
        loadLocal(); loadNotebooks();
      }
    });

  </script>
</body>
</html>
