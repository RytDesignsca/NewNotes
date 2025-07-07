<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>New Notes</title>
  <!-- Inter + other UI fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #FFFBDE;
      --text: #333;
      --header-bg: #4682A9;
      --accent: #91C8E4;
      --border: #749BC2;
      --card-bg: #fff;
      --font-family: 'Inter', sans-serif;
    }
    body.dark-mode {
      --bg: #333;
      --text: #eee;
      --header-bg: #222;
      --accent: #91C8E4;
      --border: #555;
      --card-bg: #444;
    }
    * { margin:0; padding:0; box-sizing:border-box; }
    body {
      display:flex; height:100vh;
      background:var(--bg); color:var(--text);
      font-family: var(--font-family);
    }
    a { color: var(--accent); text-decoration:none; }
    a:hover { text-decoration:underline; }

    /* Sidebar */
    .sidebar {
      width:200px; background:var(--card-bg);
      border-right:1px solid var(--border);
      display:flex; flex-direction:column; padding:1rem;
    }
    .logo {
      font-weight:600; font-size:1.25rem;
      color:var(--header-bg); text-align:center;
      margin-bottom:2rem;
    }
    .nav-list { list-style:none; flex:1; }
    .nav-list li {
      padding:.5rem 1rem; border-radius:4px;
      cursor:pointer; transition:background .2s;
    }
    .nav-list li.active,
    .nav-list li:hover { background:var(--header-bg); color:#fff; }
    .sidebar label {
      margin-top:1rem; font-size:.9rem;
      display:flex; align-items:center;
    }
    .sidebar input { margin-right:.5rem; }

    /* Main */
    .main-container { flex:1; display:flex; flex-direction:column; }
    .topbar {
      background:var(--header-bg); color:#fff;
      display:flex; justify-content:space-between;
      align-items:center; padding:1rem;
    }
    .controls * { margin-left:.5rem; }
    button {
      border:none; border-radius:4px; cursor:pointer;
    }
    #new-btn, #login-btn, #settings-btn {
      background:var(--accent); color:#fff;
      padding:.5rem .75rem; font-size:.9rem;
    }
    #sort-select {
      padding:.4rem; border-radius:4px; border:1px solid #888;
      background:#fff; color:#000;
    }

    /* Content */
    main {
      flex:1; overflow-y:auto; padding:1rem; position:relative;
    }
    section + hr {
      margin:2rem 0; border:none; border-top:1px solid var(--border);
    }

    /* Notebooks */
    #notebook-list {
      display:flex; flex-wrap:wrap; gap:1rem;
    }
    .notebook-card {
      position:relative; width:150px; height:180px;
      background:var(--card-bg); border:1px solid var(--border);
      border-radius:8px; padding:.5rem;
      display:flex; flex-direction:column; justify-content:space-between;
      transition:box-shadow .2s, border-color .2s;
    }
    .notebook-card:hover {
      box-shadow:0 4px 12px rgba(0,0,0,0.1);
      border-color:var(--accent);
    }
    .notebook-cover { font-size:3rem; text-align:center; }
    .star {
      position:absolute; top:8px; right:8px;
      font-size:1.2rem; color:#ccc; cursor:pointer;
      transition:color .2s;
    }
    .star.active { color:gold; }
    .notebook-details { text-align:center; }
    .notebook-title {
      font-weight:600; cursor:text;
    }
    .notebook-date {
      font-size:.75rem; color:#666;
    }
    .fab {
      position:absolute; bottom:1.5rem; right:1.5rem;
      width:48px; height:48px; border-radius:50%;
      background:var(--accent); color:#fff;
      font-size:1.5rem; display:flex;
      align-items:center; justify-content:center;
      box-shadow:0 2px 6px rgba(0,0,0,0.2);
    }

    /* Templates */
    .cards {
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
      gap:1rem; margin-bottom:1.5rem;
    }
    .card {
      background:var(--card-bg); border:1px solid var(--border);
      border-radius:8px; padding:1rem;
      transition:transform .2s, box-shadow .2s;
    }
    .card:hover {
      box-shadow:0 4px 12px rgba(0,0,0,0.1);
      transform:translateY(-3px);
    }

    /* Tables */
    table {
      width:100%; border-collapse:collapse;
    }
    th,td {
      text-align:left; padding:.75rem;
      border-bottom:1px solid var(--border);
    }
    th { background:var(--card-bg); }

    /* Context Menu */
    .context-menu {
      position:absolute; display:none; background:var(--card-bg);
      border:1px solid var(--border); border-radius:4px;
      z-index:1000;
    }
    .context-menu ul { list-style:none; margin:0; padding:.5rem 0; }
    .context-menu li {
      padding:.5rem 1.5rem; cursor:pointer;
      transition:background .2s;
    }
    .context-menu li:hover { background:var(--accent); color:#fff; }

    /* Modal */
    .modal {
      display:none; position:fixed; inset:0;
      background:rgba(0,0,0,0.4);
      align-items:center; justify-content:center;
      z-index:2000;
    }
    .modal .content {
      background:var(--card-bg); padding:2rem;
      border-radius:8px; width:320px; position:relative;
      text-align:left;
    }
    .modal .close {
      position:absolute; top:1rem; right:1rem;
      font-size:1.5rem; cursor:pointer; color:#666;
    }

    /* Settings Modal */
    .profile {
      display:flex; align-items:center; margin-bottom:1.5rem;
    }
    .avatar {
      font-size:2rem; margin-right:.75rem;
    }
    .profile-info .name {
      font-weight:600; margin-bottom:.25rem;
    }
    .profile-info .email {
      font-size:.85rem; color:#666;
    }
    .settings-menu {
      list-style:none; padding:0; margin:0;
    }
    .settings-menu li {
      padding:.75rem 1rem; border-radius:4px;
      cursor:pointer; transition:background .2s;
    }
    .settings-menu li:hover {
      background:var(--accent); color:#fff;
    }

    /* Login Modal Buttons */
    #login-modal .content button {
      width:100%; margin:.5rem 0;
      padding:.6rem; border:none; border-radius:4px;
      background:var(--accent); color:#fff;
      cursor:pointer; font-size:.95rem;
    }

    /* Footer */
    footer {
      text-align:center; padding:1rem;
      background:var(--card-bg); font-size:.85rem;
    }
  </style>
</head>
<body>
  <aside class="sidebar">
    <h2 class="logo">New Notes</h2>
    <ul class="nav-list">
      <li class="active">Documents</li>
      <li>Favorites</li>
      <li>Shared</li>
      <li>Marketplace</li>
      <li>Trash</li>
    </ul>
    <label><input type="checkbox" id="theme-switch"> Dark Mode</label>
  </aside>

  <div class="main-container">
    <header class="topbar">
      <h1>Documents</h1>
      <div class="controls">
        <button id="new-btn">New</button>
        <select id="sort-select">
          <option value="date">Sort by Date</option>
          <option value="name">Sort by Name</option>
        </select>
        <button id="settings-btn">⚙️</button>
        <button id="login-btn">Login</button>
      </div>
    </header>

    <main>
      <section id="notebooks">
        <h2>My Notebooks</h2>
        <div id="notebook-list"></div>
        <button id="create-notebook-btn" class="fab">➕</button>
      </section>

      <hr>

      <section id="templates">
        <h2>Popular Template Categories</h2>
        <div class="cards">
          <div class="card">
            <h3>Daily & Weekly Planners</h3>
            <p>Structure your day with time blocks, goals, and to-dos.</p>
          </div>
          <div class="card">
            <h3>Bullet Journals</h3>
            <p>Habit tracking, mood logs, reflections.</p>
          </div>
          <div class="card">
            <h3>Study & Cornell Notes</h3>
            <p>Cue columns, summaries, review sections.</p>
          </div>
          <div class="card">
            <h3>Budget & Finance Trackers</h3>
            <p>Income, expenses, savings goals, overviews.</p>
          </div>
          <div class="card">
            <h3>Meal & Fitness Planners</h3>
            <p>Plan meals, workouts, track progress.</p>
          </div>
          <div class="card">
            <h3>Dot Grid & Lined Paper</h3>
            <p>Freeform notes, sketches, structured writing.</p>
          </div>
        </div>

        <h2>Where to Find Templates</h2>
        <table>
          <thead><tr><th>Source</th><th>Highlights</th></tr></thead>
          <tbody>
            <tr>
              <td><a href="https://gridfiti.com/goodnotes-templates/" target="_blank">Gridfiti’s Notability Templates</a></td>
              <td>Aesthetic planners, journals, calendars—GoodNotes-ready</td>
            </tr>
            <tr>
              <td><a href="https://rigorousthemes.com/free-goodnotes-templates/" target="_blank">Rigorous Themes’ Free Templates</a></td>
              <td>Cornell notes, budget trackers, habit logs</td>
            </tr>
            <tr>
              <td><a href="https://flexcil.com/templates/" target="_blank">Flexcil’s Roundup</a></td>
              <td>Links to Kraftora, Dash Planner, IHeart Organizing</td>
            </tr>
          </tbody>
        </table>
      </section>
    </main>

    <footer>&copy; 2025 New Notes. All rights reserved.</footer>
  </div>

  <!-- Context Menu -->
  <div id="ctx-menu" class="context-menu">
    <ul>
      <li id="ctx-rename">Rename</li>
      <li id="ctx-duplicate">Duplicate</li>
      <li id="ctx-export">Export as PDF</li>
      <li id="ctx-share">Share link</li>
      <li id="ctx-delete">Move to Trash</li>
    </ul>
  </div>

  <!-- Settings Modal -->
  <div id="settings-modal" class="modal">
    <div class="content">
      <span class="close" id="settings-close">&times;</span>
      <div class="profile">
        <div class="avatar">👤</div>
        <div class="profile-info">
          <div class="name" id="user-name">Guest</div>
          <div class="email" id="user-email">Not signed in</div>
        </div>
      </div>
      <ul class="settings-menu">
        <li id="delete-account">Delete Account</li>
        <li>Manage Notebook Templates</li>
        <li>Settings</li>
        <li>Help</li>
        <li>About</li>
      </ul>
    </div>
  </div>

  <!-- Login Modal -->
  <div id="login-modal" class="modal">
    <div class="content">
      <span class="close" id="login-close">&times;</span>
      <h2>Login</h2>
      <button id="btn-google">Continue with Google</button>
      <button id="btn-microsoft">Continue with Microsoft</button>
      <button id="btn-email">Login with Email</button>
      <button id="btn-phone">Login with Phone</button>
    </div>
  </div>

  <script type="module">
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

    // Initialize Firebase
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID"
    };
    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);

    // UI Elements
    const themeSwitch = document.getElementById('theme-switch');
    const sm = document.getElementById('settings-modal');
    const lm = document.getElementById('login-modal');
    const userNameEl = document.getElementById('user-name');
    const userEmailEl = document.getElementById('user-email');
    const deleteBtn = document.getElementById('delete-account');

    // Theme toggle
    themeSwitch.addEventListener('change', () =>
      document.body.classList.toggle('dark-mode')
    );

    // Settings modal
    document.getElementById('settings-btn').onclick = () => sm.style.display = 'flex';
    document.getElementById('settings-close').onclick = () => sm.style.display = 'none';
    window.addEventListener('click', e => { if (e.target === sm) sm.style.display = 'none'; });

    // Login modal
    document.getElementById('login-btn').onclick = () => lm.style.display = 'flex';
    document.getElementById('login-close').onclick = () => lm.style.display = 'none';
    window.addEventListener('click', e => { if (e.target === lm) lm.style.display = 'none'; });

    // Auth state changes
    onAuthStateChanged(auth, user => {
      if (user) {
        userNameEl.textContent = user.displayName || user.email;
        userEmailEl.textContent = user.email;
      } else {
        userNameEl.textContent = 'Guest';
        userEmailEl.textContent = 'Not signed in';
      }
    });

    // Login flows
    document.getElementById('btn-google').onclick = () => {
      signInWithPopup(auth, new GoogleAuthProvider())
        .catch(console.error);
    };
    document.getElementById('btn-microsoft').onclick = () => {
      const ms = new OAuthProvider('microsoft.com');
      signInWithPopup(auth, ms).catch(console.error);
    };
    document.getElementById('btn-email').onclick = async () => {
      const email = prompt('Email:');
      const pass = prompt('Password:');
      try {
        await signInWithEmailAndPassword(auth, email, pass);
      } catch {
        await createUserWithEmailAndPassword(auth, email, pass);
      }
    };
    document.getElementById('btn-phone').onclick = () => {
      alert('Phone login not implemented in this demo.');
    };

    // Delete account
    deleteBtn.onclick = async () => {
      if (!auth.currentUser) return alert('Not signed in');
      if (!confirm('Delete your account? This is irreversible.')) return;
      try {
        await deleteUser(auth.currentUser);
        alert('Account deleted');
      } catch (e) {
        if (e.code === 'auth/requires-recent-login') {
          const email = prompt('Re-enter email:');
          const pass = prompt('Re-enter password:');
          const cred = EmailAuthProvider.credential(email, pass);
          await reauthenticateWithCredential(auth.currentUser, cred);
          await deleteUser(auth.currentUser);
          alert('Account deleted after re-authentication');
        } else {
          console.error(e);
          alert('Error deleting account: ' + e.message);
        }
      }
      sm.style.display = 'none';
    };

    // Notebook & context menu logic
    let notebookCount = 0, ctxTarget = null;
    const menu = document.getElementById('ctx-menu');

    function fmtDate(d = new Date()) {
      return d.toLocaleString('en-US', {
        month:'short',day:'numeric',year:'numeric',
        hour:'numeric',minute:'2-digit'
      });
    }
    function addNotebook({ title, cover='📓', meta } = {}) {
      notebookCount++;
      const list = document.getElementById('notebook-list'),
            card = document.createElement('div');
      card.className = 'notebook-card';
      card.innerHTML = `
        <div class="star">☆</div>
        <div class="notebook-cover">${cover}</div>
        <div class="notebook-details">
          <div class="notebook-title">${title||'Untitled '+notebookCount}</div>
          <div class="notebook-date">${meta||fmtDate()}</div>
        </div>`;
      card.querySelector('.star').onclick = e => {
        const s = e.target;
        s.classList.toggle('active');
        s.textContent = s.classList.contains('active')?'★':'☆';
      };
      const ttl = card.querySelector('.notebook-title');
      ttl.ondblclick = () => {
        const n = prompt('New name:', ttl.textContent);
        if (n) ttl.textContent = n;
      };
      card.oncontextmenu = e => {
        e.preventDefault();
        ctxTarget = card;
        menu.style.top = e.clientY + 'px';
        menu.style.left = e.clientX + 'px';
        menu.style.display = 'block';
      };
      list.append(card);
      card.scrollIntoView({ behavior: 'smooth' });
    }

    // initialize one sample notebook
    addNotebook({ title:'Science', cover:'📘', meta:'Jul 4, 2025 4:14 PM' });
    document.getElementById('new-btn').onclick = () => addNotebook();
    document.getElementById('create-notebook-btn').onclick = () => addNotebook();

    // global click hides context menu
    window.addEventListener('click', () => menu.style.display = 'none');

    // context menu actions
    document.getElementById('ctx-rename').onclick = () => {
      const ttl = ctxTarget.querySelector('.notebook-title'),
            n = prompt('Rename:', ttl.textContent);
      if (n) ttl.textContent = n;
    };
    document.getElementById('ctx-duplicate').onclick = () => {
      const ttl = ctxTarget.querySelector('.notebook-title').textContent,
            cv = ctxTarget.querySelector('.notebook-cover').textContent;
      addNotebook({ title:ttl, cover:cv });
    };
    document.getElementById('ctx-export').onclick = () => {
      const ttl = ctxTarget.querySelector('.notebook-title').textContent;
      alert(`(Stub) Exported "${ttl}" as PDF`);
    };
    document.getElementById('ctx-share').onclick = () => {
      const e = prompt('Share with email:');
      if (e) alert(`(Stub) Shared with ${e}`);
    };
    document.getElementById('ctx-delete').onclick = () => {
      if (confirm('Move to Trash?')) ctxTarget.remove();
    };
  </script>
</body>
</html>
```
