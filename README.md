<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>NewNotes</title>
  <!-- Inter font -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
  <!-- Firebase SDK -->
  <script src="https://www.gstatic.com/firebasejs/9.5.0/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.5.0/firebase-auth.js"></script>
  <style>
    :root {
      --bg: #F5E7DE;
      --text: #333;
      --header-bg: #4682A9;
      --accent: #91C8E4;
      --border: #749BC2;
      --card-bg: #fff;
      --font: 'Inter', sans-serif;
    }
    body {
      margin: 0; padding: 0;
      font-family: var(--font);
      background: var(--bg);
      color: var(--text);
      display: flex;
      height: 100vh;
      overflow: hidden;
    }
    /* Sidebar */
    .sidebar {
      width: 240px;
      background: var(--card-bg);
      border-right: 1px solid var(--border);
      padding: 1rem;
      box-sizing: border-box;
    }
    .sidebar h2 {
      margin-bottom: 1.5rem;
      color: var(--header-bg);
      font-size: 1.25rem;
    }
    .sidebar ul {
      list-style: none; padding: 0;
    }
    .sidebar li {
      margin: .75rem 0;
      cursor: pointer;
      padding: .5rem;
      border-radius: 4px;
      transition: background .2s;
    }
    .sidebar li:hover,
    .sidebar li.active {
      background: var(--accent);
      color: #fff;
    }
    .sidebar label {
      display: flex;
      align-items: center;
      margin-top: 2rem;
      font-size: .9rem;
    }
    .sidebar input { margin-right: .5rem; }

    /* Main area */
    .main {
      flex: 1;
      display: flex;
      flex-direction: column;
      position: relative;
    }
    /* Topbar */
    .topbar {
      background: var(--header-bg);
      color: #fff;
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .topbar .controls > * {
      margin-left: .5rem;
    }
    .topbar button,
    .topbar select {
      border: none;
      border-radius: 4px;
      font-size: .9rem;
      padding: .5rem .75rem;
      cursor: pointer;
    }
    .topbar button {
      background: var(--accent);
      color: #fff;
    }
    .topbar select {
      background: #fff;
      color: #000;
      border: 1px solid #888;
    }

    /* Login panel */
    #login-panel {
      position: absolute;
      top: 72px;
      right: 1rem;
      width: 260px;
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1rem;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      display: none;
      z-index: 100;
    }
    #login-panel h2 {
      font-size: 1rem;
      margin-bottom: .75rem;
      color: var(--header-bg);
    }
    #login-panel input {
      width: 100%;
      padding: .4rem;
      margin-bottom: .75rem;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: .9rem;
    }
    #login-panel button {
      width: 100%;
      padding: .5rem;
      margin-bottom: .5rem;
      background: var(--accent);
      color: #fff;
      border: none;
      border-radius: 4px;
      font-size: .9rem;
    }

    /* Content area */
    main {
      flex: 1;
      overflow-y: auto;
      padding: 1rem;
    }
    section + hr {
      margin: 2rem 0;
      border: none;
      border-top: 1px solid var(--border);
    }

    /* Notebooks */
    #notebook-list {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
    }
    .notebook-card {
      position: relative;
      width: 150px;
      height: 180px;
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: .5rem;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      cursor: default;
      transition: box-shadow .2s, border-color .2s;
    }
    .notebook-card:hover {
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      border-color: var(--accent);
    }
    .notebook-cover { font-size: 3rem; text-align: center; }
    .notebook-details { text-align: center; }
    .notebook-title {
      font-weight: 600;
      cursor: text;
    }
    .notebook-date {
      font-size: .75rem;
      color: #666;
    }
    .fab {
      position: absolute;
      bottom: 1.5rem;
      right: 1.5rem;
      width: 48px;
      height: 48px;
      border-radius: 50%;
      background: var(--accent);
      color: #fff;
      font-size: 1.5rem;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
      border: none;
      cursor: pointer;
    }

    /* Templates */
    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(200px,1fr));
      gap: 1rem;
      margin-bottom: 1.5rem;
    }
    .card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1rem;
      transition: transform .2s, box-shadow .2s;
    }
    .card:hover {
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      transform: translateY(-3px);
    }

    /* Table */
    table {
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      text-align: left;
      padding: .75rem;
      border-bottom: 1px solid var(--border);
    }
    th { background: var(--card-bg); }

    /* Footer */
    footer {
      text-align: center;
      padding: 1rem;
      background: var(--card-bg);
      font-size: .85rem;
    }
  </style>
</head>
<body>
  <div class="sidebar">
    <h2>NewNotes</h2>
    <ul>
      <li class="active">Documents</li>
      <li>Favorites</li>
      <li>Shared</li>
      <li>Marketplace</li>
      <li>Trash</li>
    </ul>
    <label><input type="checkbox" id="theme-switch"> Dark Mode</label>
  </div>

  <div class="main">
    <header class="topbar">
      <h1>Documents</h1>
      <div class="controls">
        <button id="new-btn">New</button>
        <select id="sort-select">
          <option value="date">Sort by Date</option>
          <option value="name">Sort by Name</option>
        </select>
        <button id="login-btn">Login</button>
      </div>
    </header>

    <!-- Login Panel (top right) -->
    <div id="login-panel">
      <h2>Login / Sign Up</h2>
      <input type="email" id="auth-email" placeholder="Email">
      <input type="password" id="auth-password" placeholder="Password">
      <button id="auth-signup">Sign Up</button>
      <button id="auth-login">Log In</button>
      <button id="auth-delete">Delete Account</button>
    </div>

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
          <div class="card"><h3>Daily &amp; Weekly Planners</h3><p>Time blocks, goals, to-dos.</p></div>
          <div class="card"><h3>Bullet Journals</h3><p>Habit tracking, mood logs, reflections.</p></div>
          <div class="card"><h3>Study &amp; Cornell Notes</h3><p>Cue columns, summaries, review.</p></div>
          <div class="card"><h3>Budget &amp; Finance</h3><p>Income, expenses, savings goals.</p></div>
          <div class="card"><h3>Meal &amp; Fitness</h3><p>Plan meals, workouts, track progress.</p></div>
          <div class="card"><h3>Dot Grid &amp; Lined</h3><p>Freeform notes, sketches.</p></div>
        </div>
        <h2>Where to Find Templates</h2>
        <table>
          <thead><tr><th>Source</th><th>Highlights</th></tr></thead>
          <tbody>
            <tr><td><a href="https://gridfiti.com/goodnotes-templates/" target="_blank">Gridfiti’s Templates</a></td><td>Aesthetic planners, journals.</td></tr>
            <tr><td><a href="https://rigorousthemes.com/free-goodnotes-templates/" target="_blank">Rigorous Templates</a></td><td>Cornell notes, trackers.</td></tr>
            <tr><td><a href="https://flexcil.com/templates/" target="_blank">Flexcil Roundup</a></td><td>Kraftora, Dash, IHeart Org.</td></tr>
          </tbody>
        </table>
      </section>
    </main>

    <footer>&copy; 2025 NewNotes. All rights reserved.</footer>
  </div>

  <script>
    // Initialize Firebase
    const firebaseConfig = {
      apiKey: "AIzaSyCirWobFVvTyc4ALEw3XMWBCCZlEP3s048",
      authDomain: "newnotes-6942f.firebaseapp.com",
      projectId: "newnotes-6942f"
    };
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();

    // Theme toggle
    document.getElementById('theme-switch')
      .addEventListener('change', e => document.body.classList.toggle('dark-mode'));

    // Login panel toggle
    const loginPanel = document.getElementById('login-panel');
    document.getElementById('login-btn').onclick = () =>
      loginPanel.style.display = loginPanel.style.display === 'flex' ? 'none' : 'flex';
    window.addEventListener('click', e => {
      if (!loginPanel.contains(e.target) && e.target.id !== 'login-btn') {
        loginPanel.style.display = 'none';
      }
    });

    // Auth handlers
    document.getElementById('auth-signup').onclick = () => {
      const email = document.getElementById('auth-email').value;
      const pass  = document.getElementById('auth-password').value;
      auth.createUserWithEmailAndPassword(email, pass)
        .then(() => alert('Signed up!'))
        .catch(err => alert(err.message));
    };
    document.getElementById('auth-login').onclick = () => {
      const email = document.getElementById('auth-email').value;
      const pass  = document.getElementById('auth-password').value;
      auth.signInWithEmailAndPassword(email, pass)
        .then(() => alert('Logged in!'))
        .catch(err => alert(err.message));
    };
    document.getElementById('auth-delete').onclick = () => {
      const user = auth.currentUser;
      if (!user) return alert('Not signed in');
      user.delete()
        .then(() => alert('Account deleted'))
        .catch(err => alert(err.message));
    };

    // Notebook UI
    let notebookCount = 0;
    function fmtDate(d=new Date()){
      return d.toLocaleString('en-US',{month:'short',day:'numeric',year:'numeric',
        hour:'numeric',minute:'2-digit'});
    }
    function addNotebook({title,cover='📓',meta}={}) {
      notebookCount++;
      const list = document.getElementById('notebook-list');
      const card = document.createElement('div');
      card.className = 'notebook-card';
      card.innerHTML = `
        <div class="notebook-cover">${cover}</div>
        <div class="notebook-details">
          <div class="notebook-title">${title||'Untitled '+notebookCount}</div>
          <div class="notebook-date">${meta||fmtDate()}</div>
        </div>`;
      // rename on double-click
      card.querySelector('.notebook-title')
        .ondblclick = e => {
          const n = prompt('New name:', e.target.textContent);
          if (n) e.target.textContent = n;
        };
      list.appendChild(card);
      card.scrollIntoView({behavior:'smooth'});
    }
    // init sample
    addNotebook({title:'Science',cover:'📘',meta:'Jul 4, 2025 4:14 PM'});
    document.getElementById('new-btn')
      .onclick = ()=> addNotebook();
    document.getElementById('create-notebook-btn')
      .onclick = ()=> addNotebook();
  </script>
</body>
</html>
```
