<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>NewNotes</title>

  <!-- Inter font for UI clarity -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">

  <!-- Firebase SDKs -->
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
      font-family: var(--font);
      background: var(--bg);
      color: var(--text);
      overflow: hidden;
    }
    a { color: var(--accent); text-decoration:none; }
    a:hover { text-decoration:underline; }

    /* Sidebar */
    .sidebar {
      width:220px;
      background: var(--card-bg);
      border-right:1px solid var(--border);
      padding:1.5rem 1rem;
      display:flex; flex-direction:column;
    }
    .sidebar h2 {
      color: var(--header-bg);
      font-size:1.25rem;
      margin-bottom:2rem;
    }
    .sidebar ul {
      list-style:none; flex:1;
    }
    .sidebar li {
      padding:.6rem .8rem;
      border-radius:4px;
      cursor:pointer;
      transition:background .2s;
      font-weight:500;
    }
    .sidebar li.active,
    .sidebar li:hover {
      background: var(--accent);
      color:#fff;
    }
    .sidebar label {
      font-size:.9rem;
      margin-top:2rem;
      display:flex; align-items:center;
    }
    .sidebar input { margin-right:.5rem; }

    /* Main */
    .main {
      flex:1;
      display:flex;
      flex-direction:column;
      position:relative;
    }
    .topbar {
      background: var(--header-bg);
      color:#fff;
      padding:1rem 1.5rem;
      display:flex; align-items:center; justify-content:space-between;
      box-shadow:0 1px 3px rgba(0,0,0,.2);
    }
    .topbar h1 { font-weight:400; }
    .controls { display:flex; align-items:center; }
    .controls * { margin-left:.6rem; }
    .controls button,
    .controls select {
      border:none; border-radius:4px; font-size:.9rem;
      cursor:pointer;
    }
    .controls button {
      background: var(--accent);
      color:#fff;
      padding:.5rem .75rem;
    }
    .controls select {
      background:#fff;
      color:#000;
      padding:.4rem .6rem;
      border:1px solid #888;
    }

    /* Login Panel */
    #login-panel {
      position:absolute;
      top:60px; right:1.5rem;
      width:260px;
      background: var(--card-bg);
      border:1px solid var(--border);
      border-radius:8px;
      padding:1rem;
      box-shadow:0 2px 8px rgba(0,0,0,.1);
      display:none; z-index:100;
    }
    #login-panel h2 {
      margin-bottom:.75rem;
      font-size:1rem;
      color: var(--header-bg);
    }
    #login-panel input {
      width:100%;
      padding:.4rem;
      margin-bottom:.75rem;
      border:1px solid #ccc;
      border-radius:4px;
      font-size:.9rem;
    }
    #login-panel button {
      width:100%;
      padding:.5rem;
      margin-bottom:.5rem;
      background: var(--accent);
      color:#fff;
      border:none;
      border-radius:4px;
      font-size:.9rem;
    }

    /* Content */
    main {
      flex:1;
      overflow-y:auto;
      padding:1.5rem;
    }
    section + hr {
      margin:2.5rem 0;
      border:none; border-top:1px solid var(--border);
    }

    /* Notebooks */
    #notebook-list {
      display:flex; flex-wrap:wrap; gap:1rem;
    }
    .notebook-card {
      position:relative;
      width:150px; height:180px;
      background:var(--card-bg);
      border:1px solid var(--border);
      border-radius:8px;
      padding:.5rem;
      display:flex; flex-direction:column; justify-content:space-between;
      transition:box-shadow .2s, border-color .2s;
    }
    .notebook-card:hover {
      box-shadow:0 4px 12px rgba(0,0,0,.1);
      border-color:var(--accent);
    }
    .notebook-cover { font-size:3rem; text-align:center; }
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
      box-shadow:0 2px 6px rgba(0,0,0,.2);
      border:none; cursor:pointer;
    }

    /* Templates */
    .cards {
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
      gap:1rem; margin-bottom:1.5rem;
    }
    .card {
      background:var(--card-bg);
      border:1px solid var(--border);
      border-radius:8px; padding:1rem;
      transition:transform .2s, box-shadow .2s;
    }
    .card:hover {
      box-shadow:0 4px 12px rgba(0,0,0,.1);
      transform:translateY(-3px);
    }

    /* Table */
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
      position:absolute; display:none;
      background:var(--card-bg);
      border:1px solid var(--border);
      border-radius:4px; z-index:200;
    }
    .context-menu ul { list-style:none; margin:0; padding:.5rem 0; }
    .context-menu li {
      padding:.5rem 1.5rem; cursor:pointer;
      transition:background .2s;
    }
    .context-menu li:hover {
      background:var(--accent); color:#fff;
    }

    /* Settings Modal */
    .modal {
      display:none; position:fixed; inset:0;
      background:rgba(0,0,0,.4);
      align-items:center; justify-content:center; z-index:300;
    }
    .modal .content {
      background:var(--card-bg);
      padding:2rem;
      border-radius:8px;
      width:300px; position:relative;
      text-align:left;
    }
    .modal .close {
      position:absolute; top:1rem; right:1rem;
      font-size:1.2rem; cursor:pointer; color:#666;
    }
    .profile {
      display:flex; align-items:center; margin-bottom:1.5rem;
    }
    .avatar { font-size:2rem; margin-right:.75rem; }
    .profile-info .name { font-weight:600; margin-bottom:.25rem; }
    .profile-info .email { font-size:.85rem; color:#666; }
    .settings-menu { list-style:none; padding:0; margin:0; }
    .settings-menu li {
      padding:.75rem 1rem; border-radius:4px;
      cursor:pointer; transition:background .2s;
    }
    .settings-menu li:hover {
      background:var(--accent); color:#fff;
    }

    /* Footer */
    footer {
      text-align:center; padding:1rem;
      background:var(--card-bg); font-size:.85rem;
    }
  </style>
</head>
<body>

  <!-- Sidebar -->
  <aside class="sidebar">
    <h2>NewNotes</h2>
    <ul>
      <li class="active">Documents</li>
      <li>Favorites</li>
      <li>Shared</li>
      <li>Marketplace</li>
      <li>Trash</li>
    </ul>
    <label><input type="checkbox" id="theme-switch"> Dark Mode</label>
  </aside>

  <!-- Main -->
  <div class="main">
    <!-- Topbar -->
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

    <!-- Login Panel -->
    <div id="login-panel">
      <h2>Login / Sign Up</h2>
      <input type="email" id="auth-email" placeholder="Email">
      <input type="password" id="auth-password" placeholder="Password">
      <button id="auth-signup">Sign Up</button>
      <button id="auth-login">Log In</button>
      <button id="auth-delete">Delete Account</button>
    </div>

    <!-- Main Content -->
    <main>
      <!-- Notebooks -->
      <section id="notebooks">
        <h2>My Notebooks</h2>
        <div id="notebook-list"></div>
        <button id="create-notebook-btn" class="fab">➕</button>
      </section>

      <hr>

      <!-- Templates -->
      <section id="templates">
        <h2>Popular Template Categories</h2>
        <div class="cards">
          <div class="card"><h3>Daily &amp; Weekly Planners</h3><p>Time blocks, goals, to-dos.</p></div>
          <div class="card"><h3>Bullet Journals</h3><p>Habit tracking, mood logs.</p></div>
          <div class="card"><h3>Study &amp; Cornell Notes</h3><p>Cue columns, summaries.</p></div>
          <div class="card"><h3>Budget &amp; Finance</h3><p>Income, expenses, goals.</p></div>
          <div class="card"><h3>Meal &amp; Fitness</h3><p>Plan meals, workouts.</p></div>
          <div class="card"><h3>Dot Grid &amp; Lined</h3><p>Notes, sketches.</p></div>
        </div>

        <h2>Where to Find Templates</h2>
        <table>
          <thead><tr><th>Source</th><th>Highlights</th></tr></thead>
          <tbody>
            <tr>
              <td><a href="https://gridfiti.com/goodnotes-templates/" target="_blank">Gridfiti’s Templates</a></td>
              <td>Aesthetic planners &amp; journals</td>
            </tr>
            <tr>
              <td><a href="https://rigorousthemes.com/free-goodnotes-templates/" target="_blank">Rigorous Themes</a></td>
              <td>Cornell notes, trackers</td>
            </tr>
            <tr>
              <td><a href="https://flexcil.com/templates/" target="_blank">Flexcil Roundup</a></td>
              <td>Kraftora, Dash, IHeart Org.</td>
            </tr>
          </tbody>
        </table>
      </section>
    </main>

    <footer>&copy; 2025 NewNotes. All rights reserved.</footer>
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

  <script>
    // Firebase init
    const firebaseConfig = {
      apiKey: "AIzaSyCirWobFVvTyc4ALEw3XMWBCCZlEP3s048",
      authDomain: "newnotes-6942f.firebaseapp.com",
      projectId: "newnotes-6942f"
    };
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();

    // Theme toggle
    document.getElementById('theme-switch').addEventListener('change', e =>
      document.body.classList.toggle('dark-mode')
    );

    // Login panel
    const loginPanel = document.getElementById('login-panel');
    document.getElementById('login-btn').onclick = () =>
      loginPanel.style.display = loginPanel.style.display === 'flex' ? 'none' : 'flex';
    window.addEventListener('click', e => {
      if (!loginPanel.contains(e.target) && e.target.id !== 'login-btn')
        loginPanel.style.display = 'none';
    });

    // Auth actions
    document.getElementById('auth-signup').onclick = () => {
      const email = document.getElementById('auth-email').value;
      const pass = document.getElementById('auth-password').value;
      auth.createUserWithEmailAndPassword(email, pass)
        .then(() => alert('Signed up!'))
        .catch(e => alert(e.message));
    };
    document.getElementById('auth-login').onclick = () => {
      const email = document.getElementById('auth-email').value;
      const pass = document.getElementById('auth-password').value;
      auth.signInWithEmailAndPassword(email, pass)
        .then(() => alert('Logged in!'))
        .catch(e => alert(e.message));
    };
    document.getElementById('auth-delete').onclick = () => {
      const u = auth.currentUser;
      if (!u) return alert('Not signed in');
      u.delete()
       .then(() => alert('Account deleted'))
       .catch(e => alert(e.message));
    };

    // Settings modal
    const sm = document.getElementById('settings-modal');
    document.getElementById('settings-btn').onclick = () => sm.style.display='flex';
    document.getElementById('settings-close').onclick = () => sm.style.display='none';
    window.addEventListener('click', e => { if(e.target===sm) sm.style.display='none'; });

    // Auth state -> profile
    auth.onAuthStateChanged(u => {
      document.getElementById('user-name').textContent = u ? (u.displayName||u.email) : 'Guest';
      document.getElementById('user-email').textContent = u ? u.email : 'Not signed in';
    });

    // Notebook + context menu
    let notebookCount = 0, ctxTarget=null;
    const menu = document.getElementById('ctx-menu');
    function fmtDate(d=new Date()){
      return d.toLocaleString('en-US',{month:'short',day:'numeric',year:'numeric',
        hour:'numeric',minute:'2-digit'});
    }
    function addNotebook({title,cover='📓',meta}={}) {
      notebookCount++;
      const list = document.getElementById('notebook-list');
      const card = document.createElement('div');
      card.className='notebook-card';
      card.innerHTML=`
        <div class="notebook-cover">${cover}</div>
        <div class="notebook-details">
          <div class="notebook-title">${title||'Untitled '+notebookCount}</div>
          <div class="notebook-date">${meta||fmtDate()}</div>
        </div>`;
      // rename double-click
      card.querySelector('.notebook-title').ondblclick=e=>{
        const n=prompt('New name:',e.target.textContent);
        if(n) e.target.textContent=n;
      };
      // context menu
      card.oncontextmenu=e=>{
        e.preventDefault();
        ctxTarget=card;
        menu.style.top=e.clientY+'px';
        menu.style.left=e.clientX+'px';
        menu.style.display='block';
      };
      list.appendChild(card);
      card.scrollIntoView({behavior:'smooth'});
    }
    // init sample
    addNotebook({title:'Science',cover:'📘',meta:'Jul 4, 2025 4:14 PM'});
    document.getElementById('new-btn').onclick=()=>addNotebook();
    document.getElementById('create-notebook-btn').onclick=()=>addNotebook();
    window.addEventListener('click',()=>menu.style.display='none');

    // context actions
    document.getElementById('ctx-rename').onclick=()=>{
      const ttl=ctxTarget.querySelector('.notebook-title');
      const n=prompt('Rename:',ttl.textContent);
      if(n) ttl.textContent=n;
    };
    document.getElementById('ctx-duplicate').onclick=()=>{
      const ttl=ctxTarget.querySelector('.notebook-title').textContent;
      const cv=ctxTarget.querySelector('.notebook-cover').textContent;
      addNotebook({title:ttl,cover:cv});
    };
    document.getElementById('ctx-export').onclick=()=>{
      alert(`Exported "${ctxTarget.querySelector('.notebook-title').textContent}" as PDF`);
    };
    document.getElementById('ctx-share').onclick=()=>{
      const mail=prompt('Share with email:');
      if(mail) alert(`Shared with ${mail}`);
    };
    document.getElementById('ctx-delete').onclick=()=>{
      if(confirm('Move to Trash?')) ctxTarget.remove();
    };
  </script>
</body>
</html>
```
