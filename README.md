<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>✨ NewNotes ✨</title>
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

    body.dark-mode { --bg-light:#1a1a2e; --text:#eee; --card-bg:#16213e; --shadow:rgba(0,0,0,0.3); }
    body.green-mode { --bg-gradient:linear-gradient(135deg,#11998e 0%,#38ef7d 100%); --bg-light:#e8f5e9; --text:#1b5e20; --card-bg:#fff; }
    /* ... other theme styles omitted for brevity (kept in final file) ... */

    *{margin:0;padding:0;box-sizing:border-box}
    body{font-family:var(--font-main);background:var(--bg-light);color:var(--text);min-height:100vh;transition:all .3s}
    .header{background:var(--bg-gradient);padding:1.5rem 2rem;color:#fff;box-shadow:0 4px 20px var(--shadow);position:sticky;top:0;z-index:100}
    .header-content{max-width:1400px;margin:0 auto;display:flex;justify-content:space-between;align-items:center;gap:1rem;flex-wrap:wrap}
    .logo{font-size:2rem;font-weight:700;font-family:var(--font-accent);display:flex;align-items:center;gap:.5rem;cursor:pointer}
    .header-controls{display:flex;gap:1rem;align-items:center}
    .btn{padding:.75rem 1.5rem;border:none;border-radius:50px;font-weight:600;cursor:pointer}
    .btn-primary{background:var(--accent-pink);color:white}
    .container{max-width:1400px;margin:0 auto;padding:2rem}
    .tabs{display:flex;gap:1rem;margin-bottom:2rem;flex-wrap:wrap}
    .tab{padding:1rem 2rem;background:var(--card-bg);border-radius:20px;cursor:pointer;font-weight:600;box-shadow:0 2px 10px var(--shadow)}
    .tab.active{background:var(--bg-gradient);color:#fff}
    .notebook-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:2rem;margin-bottom:3rem}
    .notebook-card{background:var(--card-bg);border-radius:25px;padding:2rem;box-shadow:0 4px 20px var(--shadow);cursor:pointer;position:relative;overflow:hidden}
    .create-card{background:linear-gradient(135deg,var(--accent-pink),var(--accent-purple));color:#fff;display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:280px;border:3px dashed rgba(255,255,255,.5)}
    .editor-page{display:none}
    .editor-page.active{display:block}
    .editor-header{background:var(--bg-gradient);padding:1.5rem 2rem;color:#fff;display:flex;justify-content:space-between;align-items:center;gap:1rem}
    .editor-container{max-width:900px;margin:0 auto;padding:2rem}
    .editor-toolbar{background:var(--card-bg);padding:1rem;border-radius:15px;margin-bottom:1rem;box-shadow:0 2px 10px var(--shadow);display:flex;gap:.5rem;flex-wrap:wrap;align-items:center}
    .editor-content{background:var(--card-bg);border-radius:20px;padding:3rem;box-shadow:0 4px 20px var(--shadow);min-height:500px;position:relative;overflow:hidden}
    .text-editor{width:100%;min-height:500px;border:none;outline:none;font-size:1.1rem;line-height:1.8}
    .paper-menu{position:absolute;top:65px;right:20px;background:var(--card-bg);border-radius:12px;box-shadow:0 8px 30px rgba(0,0,0,.15);padding:.5rem;display:none;z-index:50;width:220px}
    .paper-menu.open{display:block}
    .paper-option{padding:.6rem;cursor:pointer;border-radius:8px;font-weight:600}
    .error-banner{position:fixed;left:50%;transform:translateX(-50%);top:90px;background:#ffeeee;color:#900;padding:.5rem 1rem;border-radius:8px;box-shadow:0 6px 30px rgba(0,0,0,.12);display:none;z-index:200}
    .info-banner{position:fixed;left:50%;transform:translateX(-50%);top:140px;background:#e8f8ef;color:#064;padding:.5rem 1rem;border-radius:8px;box-shadow:0 6px 30px rgba(0,0,0,.12);display:none;z-index:200}
    /* keep responsive tweaks */
    @media(max-width:768px){.header-content{flex-direction:column;text-align:center}}
  </style>
</head>
<body>
  <div class="header">
    <div class="header-content">
      <div class="logo" id="logo-home"><span>✨</span><span>NewNotes</span></div>
      <div class="header-controls">
        <button class="btn btn-primary" id="new-note-btn">➕ New Note</button>
        <button class="btn" id="settings-btn">⚙️ Settings</button>
        <button class="btn" id="theme-btn">🎨 Themes</button>
      </div>
    </div>
  </div>

  <!-- Visible banners for errors/info -->
  <div id="error-banner" class="error-banner" role="alert"></div>
  <div id="info-banner" class="info-banner" role="status"></div>

  <div class="container home-page" id="home-page">
    <div class="tabs">
      <div class="tab active" data-tab="all" id="tab-all">📚 All Notes</div>
      <div class="tab" data-tab="favorites" id="tab-favorites">⭐ Favorites</div>
      <div class="tab" data-tab="trash" id="tab-trash">🗑️ Recycle Bin</div>
      <div class="tab" data-tab="templates" id="tab-templates">🎨 Templates</div>
    </div>

    <section id="all-notes-section">
      <h2>📖 My Notebooks</h2>
      <div id="loading-notebooks" style="display:none;">Loading your notes...</div>
      <div class="notebook-grid" id="notebook-grid">
        <div class="notebook-card create-card" id="create-new" role="button" tabindex="0">
          <div style="font-size:48px">➕</div>
          <div style="margin-top:8px;font-weight:700">Create New</div>
        </div>
      </div>
    </section>

    <section id="favorites-section" style="display:none;">
      <h2>⭐ Favorites</h2>
      <div class="notebook-grid" id="favorites-grid"></div>
    </section>

    <section id="trash-section" style="display:none;">
      <h2>🗑️ Recycle Bin</h2>
      <div class="notebook-grid" id="trash-grid"></div>
      <div style="margin-top:2rem;text-align:center;">
        <button class="btn" id="empty-trash-btn">🗑️ Empty Recycle Bin</button>
      </div>
    </section>

    <section id="templates-section" style="display:none;">
      <h2>🎨 Templates</h2>
      <div class="template-grid" id="template-grid"></div>
    </section>
  </div>

  <!-- Editor page -->
  <div class="editor-page" id="editor-page">
    <div class="editor-header">
      <div style="display:flex;gap:12px;align-items:center;flex:1">
        <button class="btn" id="back-btn">←</button>
        <input id="note-title-editor" placeholder="Untitled Note" style="font-size:18px;padding:8px;border-radius:10px;border:none;max-width:600px" />
      </div>
      <div style="display:flex;gap:8px;align-items:center">
        <div id="save-status" style="background:rgba(255,255,255,.15);padding:.5rem 1rem;border-radius:50px;color:#fff">💾 <span id="save-text">Auto-saved</span></div>
        <button class="btn btn-primary" id="save-btn">💾 Save</button>
      </div>
    </div>

    <div class="editor-container">
      <div class="editor-toolbar">
        <button class="btn" onclick="document.execCommand('bold')"><strong>B</strong></button>
        <button class="btn" onclick="document.execCommand('italic')"><em>I</em></button>
        <button class="btn" onclick="document.execCommand('underline')"><u>U</u></button>

        <div style="margin-left:auto;position:relative">
          <button id="paper-btn" class="btn">📄 Paper</button>
          <div id="paper-menu" class="paper-menu" aria-hidden="true">
            <div class="paper-option" data-paper="blank">🟦 Blank</div>
            <div class="paper-option" data-paper="lined">📏 Lined</div>
            <div class="paper-option" data-paper="ruled">📐 Ruled</div>
            <div class="paper-option" data-paper="grid">🔲 Grid</div>
            <div class="paper-option" data-paper="sepia">🌰 Sepia</div>
            <div class="paper-option" data-paper="dark">🌙 Dark</div>
          </div>
        </div>
      </div>

      <div class="editor-content editor-paper-blank" id="editor-content">
        <div id="text-editor" class="text-editor" contenteditable="true" spellcheck="true">Start writing your notes here...</div>
      </div>
    </div>
  </div>

  <!-- Minimal modals reused from earlier file (login/settings) -->
  <div class="modal" id="login-modal" style="display:none;align-items:center;justify-content:center">
    <div style="background:var(--card-bg);padding:2rem;border-radius:12px;max-width:420px;width:90%">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h3>🔐 Login</h3><button id="login-close" style="background:#eee;border:none;border-radius:8px;padding:4px 8px">✕</button>
      </div>
      <div style="margin-top:12px;display:flex;flex-direction:column;gap:8px">
        <button id="google-login" class="btn">Continue with Google</button>
        <button id="microsoft-login" class="btn">Continue with Microsoft</button>
        <button id="email-login-btn" class="btn">Login with Email</button>
      </div>
    </div>
  </div>

  <!-- Keep other modals and UI bits (omitted in this preview for brevity) -->
  <!-- ... -->

  <script type="module">
    // Import Firebase modular SDK
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-app.js";
    import { getAuth, GoogleAuthProvider, OAuthProvider, signInWithPopup, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, EmailAuthProvider, reauthenticateWithCredential, deleteUser, signOut } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-auth.js";
    import { getFirestore, collection, doc, setDoc, getDocs, deleteDoc, serverTimestamp, query, orderBy } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-firestore.js";

    // ------------ CONFIG: update to match YOUR Firebase project if different ------------
    const firebaseConfig = {
      apiKey: "AIzaSyCirWobFVvTyc4ALEw3XMWBCCZlEP3s048",
      authDomain: "newnotes-6942f.firebaseapp.com",
      projectId: "newnotes-6942f",
      storageBucket: "newnotes-6942f.appspot.com",
      messagingSenderId: "108980754671",
      appId: "1:108980754671:web:f584d61feffc9e438aa31a",
      measurementId: "G-P8KVQS62FB"
    };
    // -------------------------------------------------------------------------------------

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);

    // ELEMENTS
    const errorBanner = document.getElementById('error-banner');
    const infoBanner = document.getElementById('info-banner');

    function showError(msg, timeout = 8000) {
      errorBanner.textContent = msg;
      errorBanner.style.display = 'block';
      clearTimeout(showError._t);
      showError._t = setTimeout(() => errorBanner.style.display = 'none', timeout);
      console.error(msg);
    }
    function showInfo(msg, timeout = 5000) {
      infoBanner.textContent = msg;
      infoBanner.style.display = 'block';
      clearTimeout(showInfo._t);
      showInfo._t = setTimeout(() => infoBanner.style.display = 'none', timeout);
      console.log(msg);
    }

    // In-memory and local-storage state
    let notebooks = [];
    let trashedNotebooks = [];
    let currentNoteId = null;
    let currentIconNoteId = null;
    let pendingLocal = loadPendingLocal(); // unsynced local notes

    // Basic templates & emoji (kept small)
    const emojiList = ['📗','📘','📙','📔','🎨','🌟','✏️','📝','🎯','📅'];

    // Utility: load pending local notes from localStorage
    function loadPendingLocal() {
      try {
        const raw = localStorage.getItem('newnotes_pending') || '[]';
        return JSON.parse(raw);
      } catch {
        return [];
      }
    }
    function savePendingLocal() {
      try { localStorage.setItem('newnotes_pending', JSON.stringify(pendingLocal || [])); } catch {}
    }

    // Show a persistent message if there are pending local notes
    function updatePendingUi() {
      if (pendingLocal && pendingLocal.length) {
        showInfo(`You have ${pendingLocal.length} note(s) saved locally. They will be synced when possible.`, 6000);
      }
    }

    // --- Firestore helpers with robust error handling and local fallback ---
    async function saveNotebookToFirestore(notebook, isNew = false) {
      // notebook must contain an id
      if (!notebook || !notebook.id) {
        showError('Invalid notebook object');
        return false;
      }

      if (!auth.currentUser) {
        // not signed in: save to local pending list instead
        pendingLocal.push({...notebook, _savedAt: new Date().toISOString()});
        savePendingLocal();
        updatePendingUi();
        showInfo('Saved locally (not signed in). Sign in to sync.');
        return false;
      }

      try {
        const notebookRef = doc(collection(db, 'users', auth.currentUser.uid, 'notebooks'), notebook.id);
        const payload = {
          title: notebook.title || 'Untitled Note',
          emoji: notebook.emoji || '📘',
          content: notebook.content || '',
          date: notebook.date || new Date().toLocaleDateString(),
          favorite: !!notebook.favorite,
          trash: !!notebook.trash,
          theme: notebook.theme || 'blank',
          updatedAt: serverTimestamp()
        };
        if (isNew) payload.createdAt = serverTimestamp();
        await setDoc(notebookRef, payload, { merge: true });
        return true;
      } catch (err) {
        // On errors we save locally and show diagnostics
        const msg = (err && err.message) ? err.message : String(err);
        showError('Failed to save to Firestore: ' + msg);
        pendingLocal.push({...notebook, _savedAt: new Date().toISOString(), _error: msg});
        savePendingLocal();
        updatePendingUi();
        return false;
      }
    }

    async function deleteNotebookFromFirestore(notebookId) {
      if (!auth.currentUser) {
        showError('Must be signed in to permanently delete a remote note.');
        return false;
      }
      try {
        const notebookRef = doc(collection(db, 'users', auth.currentUser.uid, 'notebooks'), notebookId);
        await deleteDoc(notebookRef);
        return true;
      } catch (err) {
        showError('Failed to delete from Firestore: ' + (err.message || err));
        return false;
      }
    }

    // Sync any pending local notes to Firestore (called after login or when retry requested)
    async function syncPendingLocal() {
      if (!auth.currentUser || !pendingLocal.length) return;
      showInfo('Syncing local notes...');
      const toKeep = [];
      for (const note of pendingLocal) {
        try {
          // Ensure id exists
          const noteCopy = {...note};
          if (!noteCopy.id) noteCopy.id = Date.now().toString() + Math.random().toString(36).slice(2,9);
          const ok = await saveNotebookToFirestore(noteCopy, true);
          if (!ok) {
            // keep if still failed
            toKeep.push(note);
          }
        } catch (err) {
          toKeep.push(note);
        }
      }
      pendingLocal = toKeep;
      savePendingLocal();
      updatePendingUi();
      await loadNotebooks(); // refresh server-backed list
      showInfo('Sync finished.');
    }

    // --- Loading notebooks from Firestore (and merging pending local) ---
    async function loadNotebooks() {
      // Clear current lists
      notebooks = [];
      trashedNotebooks = [];
      document.getElementById('loading-notebooks').style.display = 'block';

      if (!auth.currentUser) {
        // If not signed in, render local pending as notebooks so user can still open/edit locally
        notebooks = pendingLocal.map(n => ({...n}));
        renderNotebooks();
        document.getElementById('loading-notebooks').style.display = 'none';
        updatePendingUi();
        return;
      }

      try {
        const notebooksRef = collection(db, 'users', auth.currentUser.uid, 'notebooks');
        let q;
        try { q = query(notebooksRef, orderBy('updatedAt','desc')); } catch { q = notebooksRef; }
        const snaps = await getDocs(q);
        snaps.forEach(s => {
          const data = { id: s.id, ...s.data() };
          data.title = data.title || 'Untitled Note';
          data.emoji = data.emoji || '📘';
          data.content = data.content || '';
          data.date = data.date || new Date().toLocaleDateString();
          data.favorite = !!data.favorite;
          data.trash = !!data.trash;
          data.theme = data.theme || 'blank';
          if (data.trash) trashedNotebooks.push(data);
          else notebooks.push(data);
        });
        // merge pendingLocal (if any) but mark as unsynced in UI
        if (pendingLocal.length) {
          for (const p of pendingLocal) {
            // if already present by id skip
            if (!notebooks.find(n => n.id === p.id)) {
              notebooks.unshift({...p, _local: true});
            }
          }
        }
        renderNotebooks();
      } catch (err) {
        showError('Error loading notebooks: ' + (err.message || err));
      } finally {
        document.getElementById('loading-notebooks').style.display = 'none';
      }
    }

    // --- Render / UI functions ---
    function renderNotebooks() {
      const grid = document.getElementById('notebook-grid');
      const createCard = document.getElementById('create-new');
      grid.innerHTML = '';
      // reattach create card (prevents losing handler after DOM replace)
      if (createCard) {
        createCard.id = 'create-new';
        createCard.className = 'notebook-card create-card';
        createCard.onclick = createNotebook;
        createCard.onkeypress = (e) => { if (e.key==='Enter') createNotebook(); };
        grid.appendChild(createCard);
      }
      if (!notebooks.length) {
        // empty state
        // keep create card visible
        const empty = document.createElement('div');
        empty.style.gridColumn = '1/-1';
        empty.style.textAlign = 'center';
        empty.style.color = '#718096';
        empty.style.padding = '2rem';
        empty.innerHTML = '<div style="font-size:36px">🗂️</div><div>No notebooks yet — create one!</div>';
        grid.appendChild(empty);
        return;
      }
      notebooks.forEach(nb => {
        const card = createNotebookCardElement(nb);
        grid.appendChild(card);
      });
    }

    function createNotebookCardElement(notebook) {
      const card = document.createElement('div');
      card.className = 'notebook-card';
      card.dataset.noteId = notebook.id || '';
      card.innerHTML = `
        <div style="font-size:40px;text-align:center">${notebook.emoji || '📘'}</div>
        <div style="font-weight:700;text-align:center;margin-top:8px">${escapeHtml(notebook.title)}</div>
        <div style="text-align:center;color:#718096;margin-top:6px">📅 ${notebook.date || ''} ${notebook._local ? '(local)' : ''}</div>
        <div style="display:flex;justify-content:center;gap:8px;margin-top:12px">
          <button class="btn small star-btn">${notebook.favorite ? '★' : '☆'}</button>
          <button class="btn small share-btn">🔗</button>
          <button class="btn small delete-btn">🗑️</button>
        </div>
      `;
      // clicking card opens editor
      card.addEventListener('click', (e) => {
        // avoid opening when clicking action buttons
        if (e.target.closest('.star-btn') || e.target.closest('.share-btn') || e.target.closest('.delete-btn')) return;
        openNote(notebook.id);
      });

      // star
      const star = card.querySelector('.star-btn');
      star.onclick = async (e) => {
        e.stopPropagation();
        notebook.favorite = !notebook.favorite;
        const ok = await saveNotebookToFirestore(notebook);
        if (ok) await loadNotebooks();
      };

      // share (simple)
      const shareBtn = card.querySelector('.share-btn');
      shareBtn.onclick = (e) => {
        e.stopPropagation();
        prompt('Copy share link (local simulation):', `${location.origin}${location.pathname}?share=${encodeURIComponent(notebook.id)}`);
      };

      // delete -> move to trash
      const delBtn = card.querySelector('.delete-btn');
      delBtn.onclick = async (e) => {
        e.stopPropagation();
        if (confirm('Move to recycle bin?')) {
          notebook.trash = true;
          const ok = await saveNotebookToFirestore(notebook);
          if (ok) await loadNotebooks();
          else {
            // if not saved to Firestore (maybe local), remove from notebooks and add to trashed local list
            notebooks = notebooks.filter(n => n.id !== notebook.id);
            trashedNotebooks.push(notebook);
            renderNotebooks();
          }
        }
      };

      return card;
    }

    function escapeHtml(str){ if (!str) return ''; return String(str).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;'); }

    // --- Create notebook flow ---
    async function createNotebook() {
      // Create dialog prompt
      // Use auth.currentUser to decide whether to attempt Firestore save immediately
      const title = prompt('📝 Name your notebook:', 'My New Notebook');
      if (!title) return;

      const id = Date.now().toString() + Math.random().toString(36).slice(2,9);
      const notebook = {
        id,
        title,
        emoji: emojiList[Math.floor(Math.random()*emojiList.length)],
        content: '',
        date: new Date().toLocaleDateString(),
        favorite: false,
        trash: false,
        theme: 'blank'
      };

      // Try saving to Firestore; if it fails we keep it locally (pending)
      const saved = await saveNotebookToFirestore(notebook, true);
      if (saved) {
        showInfo('Saved to cloud ✔️');
        await loadNotebooks();
        openNote(id);
      } else {
        showInfo('Saved locally. It will sync when possible.');
        // add to in-memory list for immediate visibility
        notebooks.unshift({...notebook, _local:true});
        renderNotebooks();
        openNote(id);
      }
    }

    // --- Editor open/save ---
    const homePageEl = document.getElementById('home-page');
    const editorPage = document.getElementById('editor-page');
    const backBtn = document.getElementById('back-btn');
    const saveBtn = document.getElementById('save-btn');
    const textEditor = document.getElementById('text-editor');
    const noteTitleEditor = document.getElementById('note-title-editor');
    const editorContent = document.getElementById('editor-content');

    function openNote(noteId) {
      // find in notebooks or trashed or pendingLocal
      let note = notebooks.find(n=>n.id===noteId) || trashedNotebooks.find(n=>n.id===noteId) || pendingLocal.find(n=>n.id===noteId);
      if (!note) {
        showError('Note not found');
        return;
      }
      if (note.trash) { showError('This note is in the recycle bin. Restore first.'); return; }

      currentNoteId = noteId;
      noteTitleEditor.value = note.title || '';
      textEditor.innerHTML = note.content || '';
      applyEditorPaper(note.theme || 'blank');

      homePageEl.style.display = 'none';
      editorPage.classList.add('active');
      window.scrollTo(0,0);
    }

    async function saveNote() {
      if (!currentNoteId) return;
      // find note in notebooks or pendingLocal
      let note = notebooks.find(n=>n.id===currentNoteId) || pendingLocal.find(n=>n.id===currentNoteId);
      if (!note) {
        // if not found create a new local note object
        note = { id: currentNoteId };
        notebooks.unshift(note);
      }
      note.title = noteTitleEditor.value || 'Untitled Note';
      note.content = textEditor.innerHTML;
      note.date = new Date().toLocaleDateString();
      note.theme = note.theme || 'blank';

      const ok = await saveNotebookToFirestore(note);
      if (ok) {
        document.getElementById('save-text').textContent = 'Saved!';
        setTimeout(()=> document.getElementById('save-text').textContent = 'Auto-saved', 1500);
        await loadNotebooks();
      } else {
        // saved locally
        // ensure pendingLocal contains it
        if (!pendingLocal.find(p=>p.id===note.id)) pendingLocal.push({...note, _savedAt:new Date().toISOString()});
        savePendingLocal();
        updatePendingUi();
        showInfo('Saved locally (will retry sync).');
        // reflect in UI
        notebooks = notebooks.filter(n=>n.id!==note.id); // avoid duplicates
        notebooks.unshift({...note, _local:true});
        renderNotebooks();
      }
    }

    backBtn.onclick = () => { saveNote(); homePageEl.style.display = ''; editorPage.classList.remove('active'); currentNoteId = null; window.scrollTo(0,0); };
    saveBtn.onclick = saveNote;

    // Auto-save every 10s while editing
    setInterval(()=>{ if (currentNoteId) saveNote(); }, 10000);

    // --- Paper menu UI & logic ---
    const paperBtn = document.getElementById('paper-btn');
    const paperMenu = document.getElementById('paper-menu');
    function openPaperMenu(){ paperMenu.classList.add('open'); paperMenu.setAttribute('aria-hidden','false'); }
    function closePaperMenu(){ paperMenu.classList.remove('open'); paperMenu.setAttribute('aria-hidden','true'); }
    paperBtn.addEventListener('click', (e)=>{ e.stopPropagation(); paperMenu.classList.contains('open') ? closePaperMenu() : openPaperMenu(); });
    document.addEventListener('click', (e)=>{ if (!paperMenu.contains(e.target) && e.target !== paperBtn) closePaperMenu(); });
    paperMenu.querySelectorAll('.paper-option').forEach(opt=>{
      opt.onclick = async ()=>{
        const style = opt.dataset.paper;
        applyEditorPaper(style);
        if (currentNoteId) {
          // persist selection in note object (local or cloud)
          let note = notebooks.find(n=>n.id===currentNoteId) || pendingLocal.find(n=>n.id===currentNoteId);
          if (note) {
            note.theme = style;
            await saveNotebookToFirestore(note);
          }
        }
        closePaperMenu();
      };
    });

    function applyEditorPaper(style){
      editorContent.classList.remove('editor-paper-blank','editor-paper-lined','editor-paper-ruled','editor-paper-grid','editor-paper-sepia','editor-paper-dark');
      switch(style){
        case 'lined': editorContent.classList.add('editor-paper-lined'); break;
        case 'ruled': editorContent.classList.add('editor-paper-ruled'); break;
        case 'grid': editorContent.classList.add('editor-paper-grid'); break;
        case 'sepia': editorContent.classList.add('editor-paper-sepia'); break;
        case 'dark': editorContent.classList.add('editor-paper-dark'); break;
        default: editorContent.classList.add('editor-paper-blank');
      }
    }

    // --- Authentication & auth-state handling ---
    onAuthStateChanged(auth, async (user) => {
      console.log('onAuthStateChanged', user);
      if (user) {
        showInfo(`Signed in as ${user.email || user.uid}`, 3000);
        // after login try to sync any pending local notes
        await syncPendingLocal();
        await loadNotebooks();
      } else {
        showInfo('Not signed in');
        await loadNotebooks();
      }
    });

    // Simple login button hookups (popup-based)
    document.getElementById('new-note-btn').onclick = () => {
      // If not signed in, offer to create local note (we also let createNotebook handle that)
      createNotebook();
    };
    document.getElementById('create-new').onclick = createNotebook;

    // Minimal login flows: show login modal and wire google/ms/email actions
    const loginModal = document.getElementById('login-modal');
    document.getElementById('settings-btn').onclick = ()=>{ alert('Settings opens (kept simple in this build)'); };
    document.getElementById('theme-btn').onclick = ()=>{ alert('Theme selector (use editor paper for per-note)'); };
    document.getElementById('login-close').onclick = ()=> loginModal.style.display='none';
    document.getElementById('google-login').onclick = async ()=>{
      try { await signInWithPopup(auth, new GoogleAuthProvider()); loginModal.style.display='none'; }
      catch(e){ showError('Google login failed: ' + (e.message||e)); }
    };
    document.getElementById('microsoft-login').onclick = async ()=>{
      try { const provider = new OAuthProvider('microsoft.com'); await signInWithPopup(auth, provider); loginModal.style.display='none'; }
      catch(e){ showError('Microsoft login failed: ' + (e.message||e)); }
    };
    document.getElementById('email-login-btn').onclick = ()=>{ loginModal.style.display='none'; const email = prompt('Email:'); const pass = prompt('Password:'); if (email && pass) signInWithEmailAndPassword(auth, email, pass).catch(e=>showError(e.message)); };

    // Empty trash (permanently delete)
    document.getElementById('empty-trash-btn').onclick = async ()=>{
      if (!confirm('Permanently delete all notes in Recycle Bin?')) return;
      // Attempt to delete remote trashed items; local trashed ones will be cleared client-side
      for (const t of trashedNotebooks) {
        if (auth.currentUser) {
          await deleteNotebookFromFirestore(t.id);
        }
      }
      trashedNotebooks = [];
      renderNotebooks();
      showInfo('Recycle bin emptied');
    };

    // Manual retry sync button (exposed via info banner click)
    infoBanner.onclick = ()=>{ syncPendingLocal(); };

    // Start: load local UI and attempt to load server-backed items if signed in
    loadNotebooks();
    updatePendingUi();

    // For debugging: expose a few helpers to window
    window.__newnotes = { savePendingLocal, loadPendingLocal, pendingLocal, saveNotebookToFirestore, syncPendingLocal };

      background: var(--card-bg);
      margin-top: 4rem;
      border-top: 1px solid rgba(0,0,0,0.1);
    }
    
    .footer-heart {
      color: var(--accent-pink);
      animation: heartbeat 1.5s infinite;
    }
    
    @keyframes heartbeat {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.2); }
    }

    .editor-page {
      display: none;
      min-height: 100vh;
      background: var(--bg-light);
    }

    .editor-page.active {
      display: block;
    }

    .editor-header {
      background: var(--bg-gradient);
      padding: 1.5rem 2rem;
      color: white;
      box-shadow: 0 4px 20px var(--shadow);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
    }

    .editor-title-section {
      display: flex;
      align-items: center;
      gap: 1rem;
      flex: 1;
    }

    .back-btn {
      background: rgba(255, 255, 255, 0.2);
      border: none;
      color: white;
      font-size: 1.5rem;
      width: 50px;
      height: 50px;
      border-radius: 50%;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .back-btn:hover {
      background: rgba(255, 255, 255, 0.3);
      transform: scale(1.1);
    }

    .editor-title-input {
      background: rgba(255, 255, 255, 0.2);
      border: 2px solid transparent;
      color: white;
      font-size: 1.8rem;
      font-weight: 700;
      font-family: var(--font-accent);
      padding: 0.5rem 1rem;
      border-radius: 15px;
      outline: none;
      transition: all 0.3s ease;
      flex: 1;
      max-width: 500px;
    }

    .editor-title-input::placeholder {
      color: rgba(255, 255, 255, 0.7);
    }

    .editor-title-input:focus {
      background: white;
      color: var(--text);
      border-color: var(--accent-pink);
    }

    .editor-actions {
      display: flex;
      gap: 1rem;
      align-items: center;
      flex-wrap: wrap;
    }

    .save-status {
      background: rgba(255, 255, 255, 0.2);
      padding: 0.5rem 1.5rem;
      border-radius: 50px;
      font-size: 0.9rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .save-status.saved {
      background: var(--accent-green);
    }

    .editor-container {
      max-width: 900px;
      margin: 0 auto;
      padding: 2rem;
    }

    .editor-toolbar {
      background: var(--card-bg);
      padding: 1rem;
      border-radius: 15px;
      margin-bottom: 1rem;
      box-shadow: 0 2px 10px var(--shadow);
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
      align-items: center;
    }

    .toolbar-btn {
      background: var(--bg-light);
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 10px;
      cursor: pointer;
      font-size: 1rem;
      transition: all 0.3s ease;
      font-weight: 600;
      display: inline-flex;
      gap: 0.5rem;
      align-items: center;
    }

    .toolbar-btn:hover {
      background: var(--accent-purple);
      color: white;
      transform: translateY(-2px);
    }

    .editor-content {
      background: var(--card-bg);
      border-radius: 20px;
      padding: 3rem;
      box-shadow: 0 4px 20px var(--shadow);
      min-height: 500px;
      position: relative;
      transition: background 0.3s ease, color 0.3s ease;
      overflow: hidden;
    }

    /* PAPER / NOTE STYLES (GoodNotes-like) */
    .editor-paper-blank { background: var(--card-bg); }
    .editor-paper-lined {
      background:
        repeating-linear-gradient(
          to bottom,
          transparent 0px,
          transparent 28px,
          rgba(0,0,0,0.04) 29px
        );
      background-color: var(--card-bg);
    }
    .editor-paper-ruled {
      background:
        linear-gradient(var(--card-bg), var(--card-bg)) padding-box,
        repeating-linear-gradient(
          to bottom,
          rgba(0,0,0,0.03) 0 1px,
          transparent 1px 28px
        ) border-box;
      background-color: var(--card-bg);
    }
    .editor-paper-grid {
      background:
        linear-gradient(0deg, rgba(0,0,0,0.03) 1px, transparent 1px) 0 0 / 28px 28px,
        linear-gradient(90deg, rgba(0,0,0,0.03) 1px, transparent 1px) 0 0 / 28px 28px;
      background-color: var(--card-bg);
    }
    .editor-paper-sepia {
      background: #fbf0df;
      color: #3d2b1f;
    }
    .editor-paper-dark {
      background: #0f1724;
      color: #dbeafe;
    }

    .text-editor {
      width: 100%;
      min-height: 500px;
      border: none;
      outline: none;
      font-family: var(--font-main);
      font-size: 1.1rem;
      line-height: 1.8;
      color: var(--text);
      background: transparent;
    }

    .text-editor:focus {
      outline: 2px solid var(--accent-blue);
      outline-offset: 5px;
      border-radius: 10px;
    }

    /* PAPER MENU */
    .paper-menu {
      position: absolute;
      top: 65px;
      right: 20px;
      background: var(--card-bg);
      border-radius: 12px;
      box-shadow: 0 8px 30px rgba(0,0,0,0.15);
      padding: 0.5rem;
      display: none;
      z-index: 50;
      width: 220px;
    }
    .paper-option {
      display: flex;
      gap: 0.75rem;
      align-items: center;
      padding: 0.6rem;
      cursor: pointer;
      border-radius: 8px;
      font-weight: 600;
    }
    .paper-option:hover { background: rgba(0,0,0,0.04); }

    .loading {
      text-align: center;
      padding: 2rem;
      color: #718096;
    }

    .error {
      background: #fee;
      color: #c33;
      padding: 1rem;
      border-radius: 10px;
      margin: 1rem 0;
      text-align: center;
    }

    .success {
      background: #efe;
      color: #3c3;
      padding: 1rem;
      border-radius: 10px;
      margin: 1rem 0;
      text-align: center;
    }

    .share-link-container {
      margin-top: 1rem;
      padding: 1rem;
      background: var(--bg-light);
      border-radius: 10px;
    }

    .share-link {
      width: 100%;
      padding: 0.75rem;
      border: 2px solid var(--accent-blue);
      border-radius: 10px;
      font-family: monospace;
      background: white;
    }
    
    @media (max-width: 768px) {
      .header-content {
        flex-direction: column;
        text-align: center;
      }
      
      .notebook-grid {
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
        gap: 1rem;
      }
      
      .template-grid {
        grid-template-columns: 1fr;
      }

      .editor-title-input {
        font-size: 1.3rem;
        max-width: 100%;
      }

      .editor-content {
        padding: 1.5rem;
      }

      .theme-selector {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    .home-page.hidden {
      display: none;
    }

    .empty-state {
      text-align: center;
      padding: 3rem;
      color: #718096;
    }

    .empty-state-icon {
      font-size: 5rem;
      margin-bottom: 1rem;
    }

    /* small helper for paper menu open state */
    .paper-menu.open { display: block; }
  </style>
</head>
<body>
  <!-- HOME PAGE -->
  <div class="home-page">
    <header class="header">
      <div class="header-content">
        <div class="logo" id="logo-home">
          <span class="logo-emoji">✨</span>
          <span>NewNotes</span>
        </div>
        <div class="header-controls">
          <button class="btn btn-primary" id="new-note-btn">
            ➕ New Note
          </button>
          <button class="btn btn-secondary" id="settings-btn">
            ⚙️ Settings
          </button>
          <button class="btn btn-secondary" id="theme-btn">
            🎨 Themes
          </button>
        </div>
      </div>
    </header>

    <div class="container">
      <div class="tabs">
        <div class="tab active" data-tab="all" id="tab-all">
          <span>📚</span> All Notes
        </div>
        <div class="tab" data-tab="favorites" id="tab-favorites">
          <span>⭐</span> Favorites
        </div>
        <div class="tab" data-tab="trash" id="tab-trash">
          <span>🗑️</span> Recycle Bin
        </div>
        <div class="tab" data-tab="templates" id="tab-templates">
          <span>🎨</span> Templates
        </div>
      </div>

      <!-- All Notes Section -->
      <section id="all-notes-section">
        <h2 class="section-title">
          <span>📖</span> My Notebooks
        </h2>
        <div id="loading-notebooks" class="loading" style="display: none;">
          Loading your notes...
        </div>
        <div class="notebook-grid" id="notebook-grid">
          <div class="notebook-card create-card" id="create-new" role="button" tabindex="0">
            <div class="create-icon">➕</div>
            <div class="create-text">Create New</div>
          </div>
        </div>
      </section>

      <!-- Favorites Section -->
      <section id="favorites-section" style="display: none;">
        <h2 class="section-title">
          <span>⭐</span> Favorite Notes
        </h2>
        <div class="notebook-grid" id="favorites-grid"></div>
      </section>

      <!-- Trash Section -->
      <section id="trash-section" style="display: none;">
        <h2 class="section-title">
          <span>🗑️</span> Recycle Bin
        </h2>
        <div class="notebook-grid" id="trash-grid"></div>
        <div style="margin-top: 2rem; text-align: center;">
          <button class="btn btn-danger" id="empty-trash-btn">
            🗑️ Empty Recycle Bin
          </button>
        </div>
      </section>

      <!-- Templates Section -->
      <section id="templates-section" style="display: none;">
        <h2 class="section-title">
          <span>🎨</span> Popular Templates
        </h2>
        <div class="template-grid" id="template-grid">
          <!-- Templates will be added by JavaScript -->
        </div>
      </section>
    </div>

    <footer class="footer">
      <p>Made with <span class="footer-heart">💖</span> by Ryt Designs</p>
      <p style="margin-top: 0.5rem; color: #718096;">© 2025 • Keep your thoughts organized beautifully!</p>
    </footer>
  </div>

  <!-- EDITOR PAGE -->
  <div class="editor-page" id="editor-page">
    <div class="editor-header">
      <div class="editor-title-section">
        <button class="back-btn" id="back-btn">←</button>
        <input 
          type="text" 
          class="editor-title-input" 
          id="note-title-editor"
          placeholder="Untitled Note"
        />
      </div>
      <div class="editor-actions">
        <div class="save-status" id="save-status">
          <span>💾</span>
          <span id="save-text">Auto-saved</span>
        </div>
        <button class="btn btn-success" id="save-btn">
          💾 Save
        </button>
      </div>
    </div>

    <div class="editor-container">
      <div class="editor-toolbar">
        <button class="toolbar-btn" onclick="document.execCommand('bold')">
          <strong>B</strong>
        </button>
        <button class="toolbar-btn" onclick="document.execCommand('italic')">
          <em>I</em>
        </button>
        <button class="toolbar-btn" onclick="document.execCommand('underline')">
          <u>U</u>
        </button>
        <button class="toolbar-btn" onclick="document.execCommand('insertUnorderedList')">
          • List
        </button>
        <button class="toolbar-btn" onclick="document.execCommand('insertOrderedList')">
          1. List
        </button>
        <button class="toolbar-btn" onclick="document.execCommand('justifyLeft')">
          ⬅️ Left
        </button>
        <button class="toolbar-btn" onclick="document.execCommand('justifyCenter')">
          ↔️ Center
        </button>
        <button class="toolbar-btn" onclick="document.execCommand('justifyRight')">
          ➡️ Right
        </button>

        <!-- Paper (GoodNotes-like) -->
        <div style="position: relative; margin-left: auto;">
          <button id="paper-btn" class="toolbar-btn" title="Paper style">📄 Paper</button>
          <div id="paper-menu" class="paper-menu" aria-hidden="true">
            <div class="paper-option" data-paper="blank">🟦 Blank</div>
            <div class="paper-option" data-paper="lined">📏 Lined</div>
            <div class="paper-option" data-paper="ruled">📐 Ruled</div>
            <div class="paper-option" data-paper="grid">🔲 Grid</div>
            <div class="paper-option" data-paper="sepia">🌰 Sepia</div>
            <div class="paper-option" data-paper="dark">🌙 Dark</div>
          </div>
        </div>
      </div>

      <div class="editor-content editor-paper-blank" id="editor-content">
        <div 
          class="text-editor" 
          id="text-editor"
          contenteditable="true"
          spellcheck="true"
        >Start writing your notes here...</div>
      </div>
    </div>
  </div>

  <!-- Login Modal -->
  <div class="modal" id="login-modal">
    <div class="modal-content">
      <div class="modal-close" id="login-close">×</div>
      <h2 class="modal-title">🔐 Welcome to NewNotes!</h2>
      <div class="auth-buttons">
        <button class="auth-btn auth-google" id="google-login">
          <span>🔵</span> Continue with Google
        </button>
        <button class="auth-btn auth-microsoft" id="microsoft-login">
          <span>🔷</span> Continue with Microsoft
        </button>
        <button class="auth-btn auth-email" id="email-login-btn">
          <span>✉️</span> Login with Email
        </button>
      </div>
    </div>
  </div>

  <!-- Email Login Modal -->
  <div class="modal" id="email-modal">
    <div class="modal-content">
      <div class="modal-close" id="email-close">×</div>
      <h2 class="modal-title">✉️ Email Login</h2>
      <form id="email-form">
        <div class="form-group">
          <label for="email-input">Email</label>
          <input type="email" id="email-input" placeholder="your@email.com" required />
        </div>
        <div class="form-group">
          <label for="password-input">Password</label>
          <input type="password" id="password-input" placeholder="••••••••" required />
        </div>
        <div id="email-error" class="error" style="display: none;"></div>
        <div class="auth-buttons">
          <button type="submit" class="btn btn-primary" style="width: 100%;">
            Login
          </button>
          <button type="button" class="btn btn-secondary" id="signup-btn" style="width: 100%;">
            Create Account
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- Settings Modal -->
  <div class="modal" id="settings-modal">
    <div class="modal-content">
      <div class="modal-close" id="settings-close">×</div>
      <h2 class="modal-title">⚙️ Settings</h2>
      
      <div class="profile-section">
        <div class="profile-avatar">👤</div>
        <div class="profile-info">
          <h3 id="user-name">Guest</h3>
          <p id="user-email">Not signed in</p>
        </div>
      </div>

      <ul class="settings-menu">
        <li class="settings-item" id="login-settings-btn">🔐 Login / Sign Up</li>
        <li class="settings-item" id="logout-btn" style="display: none;">🚪 Logout</li>
        <li class="settings-item" id="export-data-btn">📤 Export All Notes</li>
        <li class="settings-item" id="import-data-btn">📥 Import Notes</li>
        <li class="settings-item" id="help-btn">❓ Help & Support</li>
        <li class="settings-item" id="about-btn">ℹ️ About NewNotes</li>
        <li class="settings-item" id="delete-account" style="color: var(--accent-pink); display: none;">🗑️ Delete Account</li>
      </ul>
    </div>
  </div>

  <!-- Theme Selector Modal -->
  <div class="modal" id="theme-modal">
    <div class="modal-content">
      <div class="modal-close" id="theme-close">×</div>
      <h2 class="modal-title">🎨 Choose Your Theme</h2>
      <div class="theme-selector">
        <div class="theme-option theme-light active" data-theme="light">
          ✨ Light
        </div>
        <div class="theme-option theme-dark" data-theme="dark">
          🌙 Dark
        </div>
        <div class="theme-option theme-green" data-theme="green">
          🌿 Green
        </div>
        <div class="theme-option theme-ocean" data-theme="ocean">
          🌊 Ocean
        </div>
        <div class="theme-option theme-sunset" data-theme="sunset">
          🌅 Sunset
        </div>
        <div class="theme-option theme-neon" data-theme="neon">
          💜 Neon
        </div>
      </div>
    </div>
  </div>

  <!-- Icon Picker Modal -->
  <div class="modal" id="icon-modal">
    <div class="modal-content">
      <div class="modal-close" id="icon-close">×</div>
      <h2 class="modal-title">Choose an Icon</h2>
      <div class="emoji-picker" id="emoji-picker"></div>
    </div>
  </div>

  <!-- Share Modal -->
  <div class="modal" id="share-modal">
    <div class="modal-content">
      <div class="modal-close" id="share-close">×</div>
      <h2 class="modal-title">📤 Share Note</h2>
      <form id="share-form">
        <div class="form-group">
          <label for="share-email">Share with (Email)</label>
          <input type="email" id="share-email" placeholder="friend@example.com" required />
        </div>
        <div class="form-group">
          <label for="share-message">Message (Optional)</label>
          <textarea id="share-message" rows="3" placeholder="Check out this note!"></textarea>
        </div>
        <div id="share-success" class="success" style="display: none;"></div>
        <button type="submit" class="btn btn-primary" style="width: 100%;">
          📧 Send Share Link
        </button>
      </form>
      <div class="share-link-container">
        <p style="margin-bottom: 0.5rem; font-weight: 600;">Or copy this link:</p>
        <input type="text" class="share-link" id="share-link" readonly />
        <button class="btn btn-secondary" id="copy-link-btn" style="width: 100%; margin-top: 1rem;">
          📋 Copy Link
        </button>
      </div>
    </div>
  </div>

  <!-- Help Modal -->
  <div class="modal" id="help-modal">
    <div class="modal-content">
      <div class="modal-close" id="help-close">×</div>
      <h2 class="modal-title">❓ Help & Troubleshooting</h2>
      <div style="text-align: left;">
        <h3 style="margin-top: 1.5rem;">🔧 Common Issues</h3>
        <p style="margin: 1rem 0;"><strong>Notes not saving?</strong><br>
        • Make sure you're logged in<br>
        • Check your internet connection<br>
        • Try refreshing the page<br>
        • Clear browser cache</p>

        <p style="margin: 1rem 0;"><strong>Can't login?</strong><br>
        • Check your email and password<br>
        • Try "Forgot Password"<br>
        • Use a different login method<br>
        • Check if popup blockers are enabled</p>

        <p style="margin: 1rem 0;"><strong>Missing notes?</strong><br>
        • Check the Recycle Bin<br>
        • Make sure you're logged into the correct account<br>
        • Notes are saved per account</p>

        <p style="margin: 1rem 0;"><strong>Sharing not working?</strong><br>
        • Both users need to have NewNotes accounts<br>
        • Check the email address is correct<br>
        • Ask them to check spam folder</p>

        <h3 style="margin-top: 1.5rem;">💡 Tips</h3>
        <p style="margin: 1rem 0;">
        • Use templates to get started quickly<br>
        • Favorite important notes with the ⭐ button<br>
        • Change note icons by clicking on them<br>
        • Try different themes from the Themes button<br>
        • Notes auto-save every 10 seconds</p>

        <h3 style="margin-top: 1.5rem;">📧 Contact Support</h3>
        <p style="margin: 1rem 0;">
        Email: support@rytdesigns.com<br>
        We typically respond within 24 hours.
        </p>
      </div>
    </div>
  </div>

  <!-- About Modal -->
  <div class="modal" id="about-modal">
    <div class="modal-content">
      <div class="modal-close" id="about-close">×</div>
      <h2 class="modal-title">ℹ️ About NewNotes</h2>
      <div style="text-align: center;">
        <p style="font-size: 3rem; margin: 1rem 0;">✨</p>
        <h3 style="margin: 1rem 0;">NewNotes v1.1</h3>
        <p style="color: #718096; margin: 1rem 0;">
          A beautiful, modern note-taking app designed to help you organize your thoughts and ideas.
        </p>
        <div style="margin: 2rem 0; padding: 1.5rem; background: var(--bg-light); border-radius: 15px;">
          <h4 style="margin-bottom: 1rem;">Features</h4>
          <p style="text-align: left; line-height: 1.8;">
            ✅ Cloud sync across devices<br>
            ✅ Beautiful templates<br>
            ✅ Rich text editing<br>
            ✅ Favorites & organization<br>
            ✅ Recycle bin for recovery<br>
            ✅ Share notes with others<br>
            ✅ Multiple theme options<br>
            ✅ Customizable note icons<br>
            ✅ Paper styles (lined, grid, sepia, dark)
          </p>
        </div>
        <p style="margin-top: 2rem; font-weight: 600;">
          Made with 💖 by Ryt Designs
        </p>
        <p style="color: #718096; margin-top: 0.5rem;">
          © 2025 All rights reserved
        </p>
      </div>
    </div>
  </div>

  <script type="module">
    // Use CDN modular imports (works in browser without bundler)
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-analytics.js";
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
      deleteUser,
      signOut
    } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-auth.js";
    import {
      getFirestore,
      collection,
      doc,
      setDoc,
      getDoc,
      getDocs,
      deleteDoc,
      serverTimestamp,
      query,
      orderBy
    } from "https://www.gstatic.com/firebasejs/9.14.0/firebase-firestore.js";

    // Firebase config — make sure these match your Firebase project settings
    const firebaseConfig = {
      apiKey: "AIzaSyCirWobFVvTyc4ALEw3XMWBCCZlEP3s048",
      authDomain: "newnotes-6942f.firebaseapp.com",
      projectId: "newnotes-6942f",
      storageBucket: "newnotes-6942f.appspot.com",
      messagingSenderId: "108980754671",
      appId: "1:108980754671:web:f584d61feffc9e438aa31a",
      measurementId: "G-P8KVQS62FB"
    };

    // Initialize Firebase
    const app = initializeApp(firebaseConfig);

    // Initialize Analytics (optional) — wrapped in try/catch for environments where analytics isn't available
    try {
      const analytics = getAnalytics(app);
      console.log('Firebase Analytics initialized');
    } catch (err) {
      console.warn('Analytics not available:', err && err.message ? err.message : err);
    }

    const auth = getAuth(app);
    const db = getFirestore(app);

    // Debug: initial auth state log
    console.log('Firebase auth initialized. auth.currentUser at load:', auth.currentUser);

    // TEMPLATES DATA
    const templates = [
      {
        emoji: '📅',
        title: 'Daily Planner',
        desc: 'Organize your day with time blocks, goals, and priorities.',
        content: `<h2>Daily Planner - ${new Date().toLocaleDateString()}</h2>
<h3>🌅 Morning Routine</h3>
<ul><li>Wake up time: _____</li><li>Exercise: _____</li><li>Breakfast: _____</li></ul>
<h3>📋 Today's Top 3 Goals</h3>
<ol><li>_____</li><li>_____</li><li>_____</li></ol>
<h3>⏰ Time Blocks</h3>
<p>9:00 AM - _____<br>12:00 PM - Lunch<br>2:00 PM - _____<br>5:00 PM - _____</p>
<h3>📝 Notes & Reminders</h3>
<p>_____</p>
<h3>🌙 Evening Reflection</h3>
<p>What went well: _____<br>What to improve: _____</p>`
      },
      {
        emoji: '✅',
        title: 'Bullet Journal',
        desc: 'Track habits, moods, and reflections in a creative way.',
        content: `<h2>Bullet Journal - Week of ${new Date().toLocaleDateString()}</h2>
<h3>📊 Habit Tracker</h3>
<p>□ Exercise<br>□ Read 30 min<br>□ Drink 8 glasses of water<br>□ Meditate<br>□ No social media after 9 PM</p>
<h3>😊 Mood Tracker</h3>
<p>Monday: _____<br>Tuesday: _____<br>Wednesday: _____<br>Thursday: _____<br>Friday: _____</p>
<h3>🎯 Weekly Goals</h3>
<ol><li>_____</li><li>_____</li><li>_____</li></ol>
<h3>💭 Weekly Reflection</h3>
<p>_____</p>`
      },
      {
        emoji: '📚',
        title: 'Study Notes',
        desc: 'Cornell notes with cue columns and summary sections.',
        content: `<h2>Study Notes - [Subject]</h2>
<p><strong>Date:</strong> ${new Date().toLocaleDateString()}<br><strong>Topic:</strong> _____</p>
<h3>📌 Key Points</h3>
<ul><li>_____</li><li>_____</li><li>_____</li></ul>
<h3>📝 Main Notes</h3>
<p>_____</p>
<h3>❓ Questions</h3>
<ol><li>_____</li><li>_____</li></ol>
<h3>📖 Summary</h3>
<p>_____</p>
<h3>💡 Key Takeaways</h3>
<p>_____</p>`
      },
      {
        emoji: '💰',
        title: 'Budget Tracker',
        desc: 'Monitor income, expenses, and savings goals.',
        content: `<h2>💰 Budget Tracker - ${new Date().toLocaleDateString('en-US', {month: 'long', year: 'numeric'})}</h2>
<h3>💵 Income</h3>
<p>Salary: $_____<br>Other: $_____<br><strong>Total Income: $_____</strong></p>
<h3>💸 Fixed Expenses</h3>
<p>Rent/Mortgage: $_____<br>Utilities: $_____<br>Insurance: $_____<br>Phone: $_____<br><strong>Total Fixed: $_____</strong></p>
<h3>🛒 Variable Expenses</h3>
<p>Groceries: $_____<br>Dining Out: $_____<br>Entertainment: $_____<br>Shopping: $_____<br><strong>Total Variable: $_____</strong></p>
<h3>💎 Savings Goals</h3>
<p>Emergency Fund: $_____<br>Vacation: $_____<br>Other: $_____</p>
<h3>📊 Summary</h3>
<p>Total Income: $_____<br>Total Expenses: $_____<br><strong>Remaining: $_____</strong></p>`
      },
      {
        emoji: '🏃',
        title: 'Fitness Plan',
        desc: 'Plan workouts, meals, and track your progress.',
        content: `<h2>🏃 Fitness Plan - Week ${new Date().toLocaleDateString()}</h2>
<h3>💪 Workout Schedule</h3>
<p><strong>Monday:</strong> Chest & Triceps<br><strong>Tuesday:</strong> Cardio<br><strong>Wednesday:</strong> Back & Biceps<br><strong>Thursday:</strong> Rest<br><strong>Friday:</strong> Legs<br><strong>Saturday:</strong> Cardio<br><strong>Sunday:</strong> Rest</p>
<h3>🍎 Meal Plan</h3>
<p><strong>Breakfast:</strong> _____<br><strong>Lunch:</strong> _____<br><strong>Dinner:</strong> _____<br><strong>Snacks:</strong> _____</p>
<h3>📊 Progress Tracker</h3>
<p>Weight: _____ lbs<br>Body Fat: _____%<br>Measurements: _____</p>
<h3>🎯 This Week's Goals</h3>
<ol><li>_____</li><li>_____</li><li>_____</li></ol>`
      },
      {
        emoji: '✏️',
        title: 'Blank Canvas',
        desc: 'Freeform notes, sketches, and creative writing.',
        content: '<h2>Blank Canvas</h2><p>Start writing anything you want...</p>'
      },
      {
        emoji: '📝',
        title: 'Meeting Notes',
        desc: 'Capture meeting agendas, discussions, and action items.',
        content: `<h2>📝 Meeting Notes</h2>
<p><strong>Date:</strong> ${new Date().toLocaleDateString()}<br><strong>Time:</strong> _____<br><strong>Attendees:</strong> _____</p>
<h3>📋 Agenda</h3>
<ol><li>_____</li><li>_____</li><li>_____</li></ol>
<h3>💬 Discussion Points</h3>
<p>_____</p>
<h3>✅ Action Items</h3>
<ul><li>[ ] _____ (Assigned to: _____)</li><li>[ ] _____ (Assigned to: _____)</li></ul>
<h3>📅 Next Meeting</h3>
<p>Date: _____<br>Topics: _____</p>`
      },
      {
        emoji: '🎯',
        title: 'Goal Setting',
        desc: 'Set SMART goals and track your progress.',
        content: `<h2>🎯 Goal Setting</h2>
<h3>Vision</h3>
<p>What do I want to achieve? _____</p>
<h3>SMART Goal</h3>
<p><strong>Specific:</strong> _____<br><strong>Measurable:</strong> _____<br><strong>Achievable:</strong> _____<br><strong>Relevant:</strong> _____<br><strong>Time-bound:</strong> _____</p>
<h3>Action Steps</h3>
<ol><li>_____</li><li>_____</li><li>_____</li></ol>
<h3>Progress Tracker</h3>
<p>Week 1: _____<br>Week 2: _____<br>Week 3: _____<br>Week 4: _____</p>
<h3>Reflection</h3>
<p>What's working: _____<br>Challenges: _____<br>Adjustments: _____</p>`
      },
      {
        emoji: '🎨',
        title: 'Project Planner',
        desc: 'Plan and track your creative projects.',
        content: `<h2>🎨 Project Planner</h2>
<p><strong>Project Name:</strong> _____<br><strong>Start Date:</strong> ${new Date().toLocaleDateString()}<br><strong>Deadline:</strong> _____</p>
<h3>🎯 Project Goals</h3>
<p>_____</p>
<h3>📋 Milestones</h3>
<ol><li>_____ (Due: _____)</li><li>_____ (Due: _____)</li><li>_____ (Due: _____)</li></ol>
<h3>✅ Task List</h3>
<ul><li>[ ] _____</li><li>_____</li><li>_____</li></ul>
<h3>💡 Ideas & Notes</h3>
<p>_____</p>
<h3>📊 Progress</h3>
<p>_____% Complete</p>`
      }
    ];

    // EMOJI LIST
    const emojiList = ['📗', '📕', '📙', '📔', '🎨', '🌸', '🌟', '🍀', '🎯', '💎', '📘', '💝', '🍳', '✏️', '🎵', '⚽', '🎮', '📷', '🍕', '☕', '🚗', '✈️', '🏠', '💼', '🎓', '💡', '🔬', '🎭', '🎪', '🎬', '📱', '💻', '⌚', '📺', '🎸', '🎹', '🎺', '🎻', '🥁', '🎤', '🎧', '📻', '🎮', '🕹️', '🎲', '🧩', '🎯', '🎱', '🏀', '🏈', '⚾', '🎾', '🏐', '🏉', '🥏', '🎳', '🏏', '🏑', '🏒', '🥍', '🏓', '🏸', '🥊', '🥋'];

    // UI ELEMENTS
    const loginModal = document.getElementById('login-modal');
    const emailModal = document.getElementById('email-modal');
    const settingsModal = document.getElementById('settings-modal');
    const themeModal = document.getElementById('theme-modal');
    const iconModal = document.getElementById('icon-modal');
    const shareModal = document.getElementById('share-modal');
    const helpModal = document.getElementById('help-modal');
    const aboutModal = document.getElementById('about-modal');

    // MODAL CONTROLS
    function closeAllModals() {
      [loginModal, emailModal, settingsModal, themeModal, iconModal, shareModal, helpModal, aboutModal].forEach(modal => {
        modal.style.display = 'none';
      });
      // close paper menu if open
      closePaperMenu();
    }

    document.querySelectorAll('.modal-close').forEach(btn => {
      btn.onclick = closeAllModals;
    });

    window.onclick = (e) => {
      if (e.target.classList.contains('modal')) {
        closeAllModals();
      }
    };

    document.getElementById('settings-btn').onclick = () => settingsModal.style.display = 'flex';
    document.getElementById('theme-btn').onclick = () => themeModal.style.display = 'flex';
    document.getElementById('help-btn').onclick = () => {
      settingsModal.style.display = 'none';
      helpModal.style.display = 'flex';
    };
    document.getElementById('about-btn').onclick = () => {
      settingsModal.style.display = 'none';
      aboutModal.style.display = 'flex';
    };

    // THEME SELECTOR
    let currentTheme = localStorage.getItem('theme') || 'light';
    
    function applyTheme(theme) {
      document.body.className = '';
      if (theme !== 'light') {
        document.body.classList.add(theme + '-mode');
      }
      currentTheme = theme;
      localStorage.setItem('theme', theme);
      
      document.querySelectorAll('.theme-option').forEach(opt => {
        opt.classList.remove('active');
        if (opt.dataset.theme === theme) {
          opt.classList.add('active');
        }
      });
    }

    document.querySelectorAll('.theme-option').forEach(opt => {
      opt.onclick = () => {
        applyTheme(opt.dataset.theme);
        setTimeout(() => closeAllModals(), 300);
      };
    });

    applyTheme(currentTheme);

    // TAB NAVIGATION
    const tabs = document.querySelectorAll('.tab');
    const allNotesSection = document.getElementById('all-notes-section');
    const favoritesSection = document.getElementById('favorites-section');
    const trashSection = document.getElementById('trash-section');
    const templatesSection = document.getElementById('templates-section');

    tabs.forEach(tab => {
      tab.addEventListener('click', () => {
        tabs.forEach(t => t.classList.remove('active'));
        tab.classList.add('active');
        
        [allNotesSection, favoritesSection, trashSection, templatesSection].forEach(s => s.style.display = 'none');
        
        const tabName = tab.dataset.tab;
        if (tabName === 'all') allNotesSection.style.display = 'block';
        else if (tabName === 'favorites') {
          favoritesSection.style.display = 'block';
          renderFavorites();
        }
        else if (tabName === 'trash') {
          trashSection.style.display = 'block';
          renderTrash();
        }
        else if (tabName === 'templates') {
          templatesSection.style.display = 'block';
          renderTemplates();
        }
      });
    });

    // RENDER TEMPLATES
    function renderTemplates() {
      const grid = document.getElementById('template-grid');
      grid.innerHTML = '';
      templates.forEach(template => {
        const card = document.createElement('div');
        card.className = 'template-card';
        card.innerHTML = `
          <div class="template-emoji">${template.emoji}</div>
          <h3 class="template-title">${template.title}</h3>
          <p class="template-desc">${template.desc}</p>
          <button class="btn btn-primary" style="width: 100%; margin-top: 1rem;">Use Template</button>
        `;
        card.querySelector('.btn').onclick = (e) => {
          e.stopPropagation();
          useTemplate(template);
        };
        grid.appendChild(card);
      });
    }

    async function useTemplate(template) {
      // prefer auth.currentUser for freshest state
      if (!auth.currentUser) {
        alert('⚠️ Please login to use templates');
        loginModal.style.display = 'flex';
        return;
      }

      const notebook = {
        id: Date.now().toString() + Math.random().toString(36).substr(2, 9),
        title: template.title,
        emoji: template.emoji,
        content: template.content,
        date: new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' }),
        favorite: false,
        trash: false,
        theme: 'blank'
      };

      const saved = await saveNotebookToFirestore(notebook, true);
      if (saved) {
        notebooks.unshift(notebook);
        await loadNotebooks(); // refresh from server
        openNote(notebook.id);
      }
    }

    // NOTEBOOK MANAGEMENT
    let notebooks = [];
    let trashedNotebooks = [];
    let currentNoteId = null;
    let currentUser = null;
    let currentIconNoteId = null;

    async function loadNotebooks() {
      if (!auth.currentUser) {
        notebooks = [];
        trashedNotebooks = [];
        renderNotebooks();
        return;
      }

      try {
        document.getElementById('loading-notebooks').style.display = 'block';
        const notebooksRef = collection(db, 'users', auth.currentUser.uid, 'notebooks');
        // safe query: orderBy 'updatedAt' but guard in case no field exist
        let q;
        try {
          q = query(notebooksRef, orderBy('updatedAt', 'desc'));
        } catch (err) {
          // fallback to no order if some older docs missing updatedAt
          q = notebooksRef;
        }
        const querySnapshot = await getDocs(q);
        
        notebooks = [];
        trashedNotebooks = [];
        querySnapshot.forEach((docSnap) => {
          const data = { id: docSnap.id, ...docSnap.data() };
          // ensure defaults to avoid missing props
          data.title = data.title || 'Untitled Note';
          data.emoji = data.emoji || '📘';
          data.content = data.content || '';
          data.date = data.date || new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
          data.favorite = !!data.favorite;
          data.trash = !!data.trash;
          data.theme = data.theme || 'blank';
          if (data.trash) {
            trashedNotebooks.push(data);
          } else {
            notebooks.push(data);
          }
        });
        
        renderNotebooks();
      } catch (error) {
        console.error('Error loading notebooks:', error);
      } finally {
        document.getElementById('loading-notebooks').style.display = 'none';
      }
    }

    // Save accepts optional isNew param to set createdAt
    async function saveNotebookToFirestore(notebook, isNew = false) {
      // prefer auth.currentUser because it reflects actual signed-in user
      if (!auth.currentUser) {
        alert('⚠️ Please login to save notes');
        return false;
      }

      try {
        const notebookRef = doc(db, 'users', auth.currentUser.uid, 'notebooks', notebook.id);
        const payload = {
          title: notebook.title || 'Untitled Note',
          emoji: notebook.emoji || '📘',
          content: notebook.content || '',
          date: notebook.date || new Date().toLocaleDateString(),
          favorite: !!notebook.favorite,
          trash: !!notebook.trash,
          theme: notebook.theme || 'blank',
          updatedAt: serverTimestamp()
        };
        if (isNew) {
          payload.createdAt = serverTimestamp();
        }
        console.log('Saving notebook to Firestore', { uid: auth.currentUser.uid, notebookId: notebook.id });
        await setDoc(notebookRef, payload, { merge: true });
        return true;
      } catch (error) {
        console.error('Error saving notebook:', error);
        alert('Failed to save: ' + (error.message || error));
        return false;
      }
    }

    async function deleteNotebookFromFirestore(notebookId) {
      if (!auth.currentUser) return false;

      try {
        const notebookRef = doc(db, 'users', auth.currentUser.uid, 'notebooks', notebookId);
        await deleteDoc(notebookRef);
        return true;
      } catch (error) {
        console.error('Error deleting notebook:', error);
        return false;
      }
    }

    function renderNotebooks() {
      const notebookGrid = document.getElementById('notebook-grid');
      // Keep the "create" card element persistent and reattach after clearing
      const createCard = document.getElementById('create-new');
      // Reset grid and re-add create card as first child
      notebookGrid.innerHTML = '';
      if (createCard) {
        // ensure the create card has the right id and click handler
        createCard.id = 'create-new';
        createCard.className = 'notebook-card create-card';
        createCard.onclick = createNotebook;
        createCard.onkeypress = (e) => { if (e.key === 'Enter') createNotebook(); };
        notebookGrid.appendChild(createCard);
      }

      // render notebooks
      notebooks.forEach(notebook => {
        addNotebookCard(notebook);
      });
    }

    function renderFavorites() {
      const grid = document.getElementById('favorites-grid');
      grid.innerHTML = '';
      
      const favorites = notebooks.filter(n => n.favorite);
      
      if (favorites.length === 0) {
        grid.innerHTML = '<div class="empty-state"><div class="empty-state-icon">⭐</div><p>No favorite notes yet!<br>Click the star icon on any note to add it here.</p></div>';
        return;
      }

      favorites.forEach(notebook => {
        const card = createNotebookCardElement(notebook);
        grid.appendChild(card);
      });
    }

    function renderTrash() {
      const grid = document.getElementById('trash-grid');
      grid.innerHTML = '';
      
      if (trashedNotebooks.length === 0) {
        grid.innerHTML = '<div class="empty-state"><div class="empty-state-icon">🗑️</div><p>Recycle bin is empty!</p></div>';
        return;
      }

      trashedNotebooks.forEach(notebook => {
        const card = createTrashCardElement(notebook);
        grid.appendChild(card);
      });
    }

    function createNotebookCardElement(notebook) {
      const card = document.createElement('div');
      card.className = 'notebook-card';
      if (notebook.favorite) card.classList.add('favorite');
      card.dataset.noteId = notebook.id;
      card.innerHTML = `
        <div class="notebook-icon" data-note-id="${notebook.id}">${notebook.emoji}</div>
        <div class="notebook-title">${escapeHtml(notebook.title)}</div>
        <div class="notebook-meta">📅 ${notebook.date}</div>
        <div class="notebook-actions">
          <button class="action-btn star-btn ${notebook.favorite ? 'favorited' : ''}" title="Favorite">⭐</button>
          <button class="action-btn share-btn" title="Share">🔗</button>
          <button class="action-btn delete-btn" title="Delete">🗑️</button>
        </div>
      `;

      card.addEventListener('click', (e) => {
        // If clicking the icon, star or action buttons, let their handlers run; otherwise open note
        if (!e.target.classList.contains('action-btn') && !e.target.classList.contains('notebook-icon')) {
          openNote(notebook.id);
        }
      });

      const iconEl = card.querySelector('.notebook-icon');
      iconEl.onclick = (e) => {
        e.stopPropagation();
        currentIconNoteId = notebook.id;
        showIconPicker();
      };

      const starBtn = card.querySelector('.star-btn');
      starBtn.onclick = async (e) => {
        e.stopPropagation();
        notebook.favorite = !notebook.favorite;
        const saved = await saveNotebookToFirestore(notebook);
        if (saved) await loadNotebooks();
      };

      const shareBtn = card.querySelector('.share-btn');
      shareBtn.onclick = (e) => {
        e.stopPropagation();
        showShareModal(notebook);
      };

      const deleteBtn = card.querySelector('.delete-btn');
      deleteBtn.onclick = async (e) => {
        e.stopPropagation();
        notebook.trash = true;
        const saved = await saveNotebookToFirestore(notebook);
        if (saved) await loadNotebooks();
      };

      return card;
    }

    function createTrashCardElement(notebook) {
      const card = document.createElement('div');
      card.className = 'notebook-card';
      card.style.opacity = '0.7';
      card.innerHTML = `
        <div class="notebook-icon">${notebook.emoji}</div>
        <div class="notebook-title">${escapeHtml(notebook.title)}</div>
        <div class="notebook-meta">📅 ${notebook.date}</div>
        <div class="notebook-actions">
          <button class="action-btn restore-btn" title="Restore">♻️</button>
          <button class="action-btn delete-btn" title="Delete Forever">❌</button>
        </div>
      `;

      const restoreBtn = card.querySelector('.restore-btn');
      restoreBtn.onclick = async (e) => {
        e.stopPropagation();
        notebook.trash = false;
        const saved = await saveNotebookToFirestore(notebook);
        if (saved) {
          await loadNotebooks();
          renderTrash();
        }
      };

      const deleteBtn = card.querySelector('.delete-btn');
      deleteBtn.onclick = async (e) => {
        e.stopPropagation();
        if (confirm('⚠️ Permanently delete this note? This cannot be undone!')) {
          await deleteNotebookFromFirestore(notebook.id);
          trashedNotebooks = trashedNotebooks.filter(n => n.id !== notebook.id);
          renderTrash();
        }
      };

      return card;
    }

    function addNotebookCard(notebook) {
      const notebookGrid = document.getElementById('notebook-grid');
      const card = createNotebookCardElement(notebook);
      notebookGrid.appendChild(card);
    }

    // ICON PICKER
    function showIconPicker() {
      const picker = document.getElementById('emoji-picker');
      picker.innerHTML = '';
      emojiList.forEach(emoji => {
        const opt = document.createElement('div');
        opt.className = 'emoji-option';
        opt.textContent = emoji;
        opt.onclick = async () => {
          const notebook = notebooks.find(n => n.id === currentIconNoteId);
          if (notebook) {
            notebook.emoji = emoji;
            const saved = await saveNotebookToFirestore(notebook);
            if (saved) {
              await loadNotebooks();
              closeAllModals();
            }
          }
        };
        picker.appendChild(opt);
      });
      iconModal.style.display = 'flex';
    }

    // SHARE MODAL
    function showShareModal(notebook) {
      const shareLink = document.getElementById('share-link');
      shareLink.value = `${window.location.origin}${window.location.pathname}?share=${notebook.id}`;
      
      document.getElementById('copy-link-btn').onclick = () => {
        try {
          shareLink.select();
          document.execCommand('copy');
          alert('✅ Link copied to clipboard!');
        } catch {
          alert('Copy not supported on this browser');
        }
      };

      document.getElementById('share-form').onsubmit = async (e) => {
        e.preventDefault();
        const email = document.getElementById('share-email').value;
        const message = document.getElementById('share-message').value;
        
        // In a real app, you would send this via email API
        const successMsg = document.getElementById('share-success');
        successMsg.textContent = `✅ Share link sent to ${email}!`;
        successMsg.style.display = 'block';
        
        setTimeout(() => {
          successMsg.style.display = 'none';
          closeAllModals();
        }, 2000);
      };

      shareModal.style.display = 'flex';
    }

    // EMPTY TRASH
    document.getElementById('empty-trash-btn').onclick = async () => {
      if (trashedNotebooks.length === 0) {
        alert('Recycle bin is already empty!');
        return;
      }

      if (!confirm(`⚠️ Permanently delete all ${trashedNotebooks.length} notes in the recycle bin? This cannot be undone!`)) {
        return;
      }

      for (const notebook of [...trashedNotebooks]) {
        await deleteNotebookFromFirestore(notebook.id);
      }
      
      trashedNotebooks = [];
      renderTrash();
      alert('✅ Recycle bin emptied!');
    };

    // CREATE NOTEBOOK
    async function createNotebook() {
      // Use auth.currentUser for immediate latest auth state
      if (!auth.currentUser) {
        alert('⚠️ Please login to create notes');
        loginModal.style.display = 'flex';
        return;
      }

      const title = prompt('📝 Name your notebook:', 'My New Notebook');
      if (!title) return;

      const emoji = emojiList[Math.floor(Math.random() * emojiList.length)];
      const notebook = {
        id: Date.now().toString() + Math.random().toString(36).substr(2, 9),
        title: title,
        emoji: emoji,
        content: '',
        date: new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' }),
        favorite: false,
        trash: false,
        theme: 'blank'
      };

      console.log('createNotebook called; saving notebook for user:', auth.currentUser.uid, notebook.id);

      const saved = await saveNotebookToFirestore(notebook, true);
      if (saved) {
        // prefer refreshing from server to keep canonical ordering and fields
        await loadNotebooks();
        openNote(notebook.id);
      }
    }

    // Always ensure create-new is responsive
    const createNewEl = document.getElementById('create-new');
    if (createNewEl) {
      createNewEl.onclick = createNotebook;
      createNewEl.onkeypress = (e) => { if (e.key === 'Enter') createNotebook(); };
    }
    document.getElementById('new-note-btn').onclick = () => {
      // If user isn't signed in direct them to login modal
      if (!auth.currentUser) {
        loginModal.style.display = 'flex';
        return;
      }
      createNotebook();
    };

    // EDITOR
    const homePage = document.querySelector('.home-page');
    const editorPage = document.getElementById('editor-page');
    const backBtn = document.getElementById('back-btn');
    const saveBtn = document.getElementById('save-btn');
    const noteTitleEditor = document.getElementById('note-title-editor');
    const textEditor = document.getElementById('text-editor');
    const saveStatus = document.getElementById('save-status');
    const saveText = document.getElementById('save-text');
    const editorContent = document.getElementById('editor-content');

    function openNote(noteId) {
      const notebook = [...notebooks, ...trashedNotebooks].find(n => n.id === noteId);
      if (!notebook) return;

      if (notebook.trash) {
        alert('⚠️ This note is in the recycle bin. Please restore it first.');
        return;
      }

      currentNoteId = noteId;
      noteTitleEditor.value = notebook.title;
      textEditor.innerHTML = notebook.content || 'Start writing your notes here...';

      // Apply per-note paper style
      applyEditorPaper(notebook.theme || 'blank');

      homePage.classList.add('hidden');
      editorPage.classList.add('active');
      window.scrollTo(0, 0);
    }

    function closeEditor() {
      saveNote();
      homePage.classList.remove('hidden');
      editorPage.classList.remove('active');
      currentNoteId = null;
      window.scrollTo(0, 0);
    }

    async function saveNote() {
      if (!currentNoteId || !auth.currentUser) return;

      const notebook = notebooks.find(n => n.id === currentNoteId);
      if (notebook) {
        notebook.title = noteTitleEditor.value || 'Untitled Note';
        notebook.content = textEditor.innerHTML;
        notebook.date = new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
        // ensure theme is kept
        notebook.theme = notebook.theme || 'blank';

        const saved = await saveNotebookToFirestore(notebook);
        if (saved) {
          renderNotebooks();
          saveStatus.classList.add('saved');
          saveText.textContent = 'Saved!';
          setTimeout(() => {
            saveStatus.classList.remove('saved');
            saveText.textContent = 'Auto-saved';
          }, 2000);
        }
      }
    }

    // Auto-save
    setInterval(() => {
      if (currentNoteId && auth.currentUser) {
        saveNote();
      }
    }, 10000);

    backBtn.onclick = closeEditor;
    saveBtn.onclick = saveNote;
    noteTitleEditor.addEventListener('blur', saveNote);
    document.getElementById('logo-home').onclick = () => window.scrollTo(0, 0);

    // PAPER (GoodNotes-like) UI & logic
    const paperBtn = document.getElementById('paper-btn');
    const paperMenu = document.getElementById('paper-menu');

    function openPaperMenu() {
      paperMenu.classList.add('open');
      paperMenu.setAttribute('aria-hidden', 'false');
    }
    function closePaperMenu() {
      paperMenu.classList.remove('open');
      paperMenu.setAttribute('aria-hidden', 'true');
    }

    paperBtn.addEventListener('click', (e) => {
      e.stopPropagation();
      if (paperMenu.classList.contains('open')) closePaperMenu();
      else openPaperMenu();
    });

    // close paper menu when clicking elsewhere
    document.addEventListener('click', (e) => {
      if (!paperMenu.contains(e.target) && e.target !== paperBtn) {
        closePaperMenu();
      }
    });

    paperMenu.querySelectorAll('.paper-option').forEach(opt => {
      opt.onclick = async (e) => {
        const selected = opt.dataset.paper;
        applyEditorPaper(selected);
        // persist to current notebook if open
        if (currentNoteId) {
          const notebook = notebooks.find(n => n.id === currentNoteId);
          if (notebook) {
            notebook.theme = selected;
            await saveNotebookToFirestore(notebook);
            renderNotebooks();
          }
        }
        closePaperMenu();
      };
    });

    function applyEditorPaper(style) {
      // remove existing paper classes
      editorContent.classList.remove('editor-paper-blank','editor-paper-lined','editor-paper-ruled','editor-paper-grid','editor-paper-sepia','editor-paper-dark');
      switch (style) {
        case 'lined':
          editorContent.classList.add('editor-paper-lined'); break;
        case 'ruled':
          editorContent.classList.add('editor-paper-ruled'); break;
        case 'grid':
          editorContent.classList.add('editor-paper-grid'); break;
        case 'sepia':
          editorContent.classList.add('editor-paper-sepia'); break;
        case 'dark':
          editorContent.classList.add('editor-paper-dark'); break;
        default:
          editorContent.classList.add('editor-paper-blank');
      }
    }

    // AUTHENTICATION
    onAuthStateChanged(auth, async (user) => {
      console.log('onAuthStateChanged fired, user:', user);
      const userName = document.getElementById('user-name');
      const userEmail = document.getElementById('user-email');
      const logoutBtn = document.getElementById('logout-btn');
      const deleteAccountBtn = document.getElementById('delete-account');
      const loginSettingsBtn = document.getElementById('login-settings-btn');
      
      if (user) {
        currentUser = user;
        userName.textContent = user.displayName || (user.email ? user.email.split('@')[0] : 'User');
        userEmail.textContent = user.email || '';
        logoutBtn.style.display = 'block';
        deleteAccountBtn.style.display = 'block';
        loginSettingsBtn.style.display = 'none';
        
        await loadNotebooks();
      } else {
        currentUser = null;
        userName.textContent = 'Guest';
        userEmail.textContent = 'Not signed in';
        logoutBtn.style.display = 'none';
        deleteAccountBtn.style.display = 'none';
        loginSettingsBtn.style.display = 'block';
        
        notebooks = [];
        trashedNotebooks = [];
        renderNotebooks();
        
        // Show login modal for new users (only once)
        setTimeout(() => {
          if (!localStorage.getItem('hasVisited')) {
            loginModal.style.display = 'flex';
            localStorage.setItem('hasVisited', 'true');
          }
        }, 1000);
      }
    });

    // LOGIN
    document.getElementById('login-settings-btn').onclick = () => {
      settingsModal.style.display = 'none';
      loginModal.style.display = 'flex';
    };

    document.getElementById('google-login').onclick = async () => {
      try {
        await signInWithPopup(auth, new GoogleAuthProvider());
        closeAllModals();
      } catch (error) {
        alert('❌ Login failed: ' + (error.message || error));
      }
    };

    document.getElementById('microsoft-login').onclick = async () => {
      try {
        const provider = new OAuthProvider('microsoft.com');
        await signInWithPopup(auth, provider);
        closeAllModals();
      } catch (error) {
        alert('❌ Login failed: ' + (error.message || error));
      }
    };

    document.getElementById('email-login-btn').onclick = () => {
      loginModal.style.display = 'none';
      emailModal.style.display = 'flex';
    };

    document.getElementById('email-form').onsubmit = async (e) => {
      e.preventDefault();
      const email = document.getElementById('email-input').value;
      const password = document.getElementById('password-input').value;
      const errorDiv = document.getElementById('email-error');

      try {
        await signInWithEmailAndPassword(auth, email, password);
        closeAllModals();
        document.getElementById('email-form').reset();
        errorDiv.style.display = 'none';
      } catch (error) {
        errorDiv.textContent = error.message || error;
        errorDiv.style.display = 'block';
      }
    };

    document.getElementById('signup-btn').onclick = async () => {
      const email = document.getElementById('email-input').value;
      const password = document.getElementById('password-input').value;
      const errorDiv = document.getElementById('email-error');

      if (!email || !password) {
        errorDiv.textContent = 'Please fill in all fields';
        errorDiv.style.display = 'block';
        return;
      }

      if (password.length < 6) {
        errorDiv.textContent = 'Password must be at least 6 characters';
        errorDiv.style.display = 'block';
        return;
      }

      try {
        await createUserWithEmailAndPassword(auth, email, password);
        closeAllModals();
        document.getElementById('email-form').reset();
        errorDiv.style.display = 'none';
      } catch (error) {
        errorDiv.textContent = error.message || error;
        errorDiv.style.display = 'block';
      }
    };

    // LOGOUT
    document.getElementById('logout-btn').onclick = async () => {
      if (confirm('🚪 Are you sure you want to logout?')) {
        try {
          await signOut(auth);
          closeAllModals();
          alert('✅ Logged out successfully');
        } catch (error) {
          alert('❌ Error logging out: ' + (error.message || error));
        }
      }
    };

    // DELETE ACCOUNT
    document.getElementById('delete-account').onclick = async () => {
      if (!auth.currentUser) {
        alert('⚠️ Please sign in first');
        return;
      }

      if (!confirm('⚠️ Delete your account permanently? All your notes will be lost forever! This cannot be undone!')) return;

      try {
        await deleteUser(auth.currentUser);
        alert('✅ Account deleted successfully');
        closeAllModals();
      } catch (error) {
        if (error.code === 'auth/requires-recent-login') {
          const email = prompt('✉️ Re-enter your email:');
          const password = prompt('🔒 Re-enter your password:');
          if (email && password) {
            const credential = EmailAuthProvider.credential(email, password);
            await reauthenticateWithCredential(auth.currentUser, credential);
            await deleteUser(auth.currentUser);
            alert('✅ Account deleted successfully');
            closeAllModals();
          }
        } else {
          alert('❌ Error: ' + (error.message || error));
        }
      }
    };

    // EXPORT DATA
    document.getElementById('export-data-btn').onclick = () => {
      if (notebooks.length === 0) {
        alert('⚠️ No notes to export!');
        return;
      }

      const data = JSON.stringify(notebooks, null, 2);
      const blob = new Blob([data], { type: 'application/json' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `newnotes-backup-${new Date().toISOString().split('T')[0]}.json`;
      a.click();
      alert('✅ Notes exported successfully!');
    };

    // IMPORT DATA
    document.getElementById('import-data-btn').onclick = () => {
      const input = document.createElement('input');
      input.type = 'file';
      input.accept = '.json';
      input.onchange = async (e) => {
        const file = e.target.files[0];
        if (!file) return;

        const reader = new FileReader();
        reader.onload = async (event) => {
          try {
            const importedNotes = JSON.parse(event.target.result);
            if (!Array.isArray(importedNotes)) {
              throw new Error('Invalid file format');
            }

            for (const note of importedNotes) {
              note.id = Date.now().toString() + Math.random().toString(36).substr(2, 9);
              note.favorite = !!note.favorite;
              note.trash = !!note.trash;
              note.theme = note.theme || 'blank';
              await saveNotebookToFirestore(note, true);
            }

            await loadNotebooks();
            alert(`✅ Imported ${importedNotes.length} notes successfully!`);
          } catch (error) {
            alert('❌ Error importing notes: ' + (error.message || error));
          }
        };
        reader.readAsText(file);
      };
      input.click();
    };

    // Utilities
    function escapeHtml(text) {
      if (!text) return '';
      return String(text)
        .replace(/&/g, '&amp;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#39;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;');
    }

    // Initialize UI
    renderTemplates();
    renderNotebooks(); // ensure create-new remains wired
  </script>
</body>
</html>
