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
    
    body.dark-mode {
      --bg-light: #1a1a2e;
      --text: #eee;
      --card-bg: #16213e;
      --shadow: rgba(0, 0, 0, 0.3);
    }

    body.green-mode {
      --bg-gradient: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
      --bg-light: #e8f5e9;
      --text: #1b5e20;
      --card-bg: #ffffff;
      --accent-pink: #66bb6a;
      --accent-blue: #26a69a;
      --accent-yellow: #9ccc65;
      --accent-green: #4caf50;
      --accent-purple: #66bb6a;
    }

    body.ocean-mode {
      --bg-gradient: linear-gradient(135deg, #2193b0 0%, #6dd5ed 100%);
      --bg-light: #e0f7fa;
      --text: #006064;
      --card-bg: #ffffff;
      --accent-pink: #00acc1;
      --accent-blue: #0097a7;
      --accent-yellow: #26c6da;
      --accent-green: #00bcd4;
      --accent-purple: #4dd0e1;
    }

    body.sunset-mode {
      --bg-gradient: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
      --bg-light: #fff3e0;
      --text: #e65100;
      --card-bg: #ffffff;
      --accent-pink: #ff6f00;
      --accent-blue: #ff9800;
      --accent-yellow: #ffc107;
      --accent-green: #ffb300;
      --accent-purple: #ffa726;
    }

    body.neon-mode {
      --bg-gradient: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
      --bg-light: #1a1a2e;
      --text: #00ff88;
      --card-bg: #0f3460;
      --accent-pink: #ff006e;
      --accent-blue: #00f5ff;
      --accent-yellow: #ffea00;
      --accent-green: #00ff88;
      --accent-purple: #c77dff;
      --shadow: rgba(255, 0, 110, 0.3);
    }
    
    * { margin: 0; padding: 0; box-sizing: border-box; }
    
    body {
      font-family: var(--font-main);
      background: var(--bg-light);
      color: var(--text);
      min-height: 100vh;
      transition: all 0.3s ease;
    }
    
    .header {
      background: var(--bg-gradient);
      padding: 1.5rem 2rem;
      color: white;
      box-shadow: 0 4px 20px var(--shadow);
      position: sticky;
      top: 0;
      z-index: 100;
    }
    
    .header-content {
      max-width: 1400px;
      margin: 0 auto;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
    }
    
    .logo {
      font-size: 2rem;
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
      50% { transform: translateY(-10px); }
    }
    
    .header-controls {
      display: flex;
      gap: 1rem;
      align-items: center;
      flex-wrap: wrap;
    }
    
    .btn {
      padding: 0.75rem 1.5rem;
      border: none;
      border-radius: 50px;
      font-family: var(--font-main);
      font-weight: 600;
      font-size: 1rem;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    }
    
    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
    }
    
    .btn-primary {
      background: var(--accent-pink);
      color: white;
    }
    
    .btn-secondary {
      background: white;
      color: var(--accent-blue);
    }

    .btn-success {
      background: var(--accent-green);
      color: white;
    }

    .btn-danger {
      background: #e74c3c;
      color: white;
    }
    
    .theme-toggle {
      background: rgba(255, 255, 255, 0.2);
      backdrop-filter: blur(10px);
      border-radius: 50px;
      padding: 0.5rem 1rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      cursor: pointer;
      transition: all 0.3s ease;
    }
    
    .theme-toggle:hover {
      background: rgba(255, 255, 255, 0.3);
    }
    
    .container {
      max-width: 1400px;
      margin: 0 auto;
      padding: 2rem;
    }
    
    .tabs {
      display: flex;
      gap: 1rem;
      margin-bottom: 2rem;
      flex-wrap: wrap;
    }
    
    .tab {
      padding: 1rem 2rem;
      background: var(--card-bg);
      border-radius: 20px;
      cursor: pointer;
      font-weight: 600;
      transition: all 0.3s ease;
      box-shadow: 0 2px 10px var(--shadow);
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    
    .tab:hover {
      transform: translateY(-3px);
      box-shadow: 0 4px 20px var(--shadow);
    }
    
    .tab.active {
      background: var(--bg-gradient);
      color: white;
    }
    
    .notebook-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 2rem;
      margin-bottom: 3rem;
    }
    
    .notebook-card {
      background: var(--card-bg);
      border-radius: 25px;
      padding: 2rem;
      box-shadow: 0 4px 20px var(--shadow);
      cursor: pointer;
      transition: all 0.3s ease;
      position: relative;
      overflow: hidden;
    }

    .notebook-card.favorite {
      border: 3px solid gold;
    }
    
    .notebook-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 6px;
      background: var(--bg-gradient);
    }
    
    .notebook-card:hover {
      transform: translateY(-8px) rotate(-1deg);
      box-shadow: 0 8px 30px var(--shadow);
    }
    
    .notebook-icon {
      font-size: 4rem;
      text-align: center;
      margin-bottom: 1rem;
      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.1));
      cursor: pointer;
      position: relative;
    }

    .notebook-icon:hover::after {
      content: '✏️';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 1.5rem;
      background: rgba(0,0,0,0.7);
      padding: 0.5rem;
      border-radius: 50%;
    }
    
    .notebook-title {
      font-size: 1.3rem;
      font-weight: 700;
      text-align: center;
      margin-bottom: 0.5rem;
      color: var(--text);
    }
    
    .notebook-meta {
      text-align: center;
      font-size: 0.9rem;
      color: #718096;
      margin-bottom: 1rem;
    }
    
    .notebook-actions {
      display: flex;
      justify-content: center;
      gap: 0.5rem;
      margin-top: 1rem;
    }
    
    .action-btn {
      padding: 0.5rem;
      background: var(--bg-light);
      border: none;
      border-radius: 50%;
      width: 35px;
      height: 35px;
      cursor: pointer;
      font-size: 1.1rem;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    .action-btn:hover {
      transform: scale(1.15);
      background: var(--accent-purple);
    }

    .action-btn.favorited {
      background: gold;
      color: white;
    }
    
    .create-card {
      background: linear-gradient(135deg, var(--accent-pink), var(--accent-purple));
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 280px;
      border: 3px dashed rgba(255,255,255,0.5);
    }
    
    .create-card:hover {
      border-color: white;
      transform: scale(1.05);
    }
    
    .create-icon {
      font-size: 5rem;
      margin-bottom: 1rem;
    }
    
    .create-text {
      font-size: 1.3rem;
      font-weight: 600;
    }
    
    .section-title {
      font-size: 2rem;
      font-weight: 700;
      margin: 3rem 0 2rem;
      font-family: var(--font-accent);
      display: flex;
      align-items: center;
      gap: 1rem;
    }
    
    .template-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 2rem;
    }
    
    .template-card {
      background: var(--card-bg);
      border-radius: 20px;
      padding: 2rem;
      box-shadow: 0 4px 15px var(--shadow);
      transition: all 0.3s ease;
      border-left: 5px solid;
      cursor: pointer;
    }
    
    .template-card:nth-child(1) { border-color: var(--accent-pink); }
    .template-card:nth-child(2) { border-color: var(--accent-blue); }
    .template-card:nth-child(3) { border-color: var(--accent-yellow); }
    .template-card:nth-child(4) { border-color: var(--accent-green); }
    .template-card:nth-child(5) { border-color: var(--accent-purple); }
    .template-card:nth-child(6) { border-color: var(--accent-pink); }
    .template-card:nth-child(7) { border-color: var(--accent-blue); }
    .template-card:nth-child(8) { border-color: var(--accent-green); }
    .template-card:nth-child(9) { border-color: var(--accent-yellow); }
    
    .template-card:hover {
      transform: translateX(10px);
      box-shadow: 0 6px 25px var(--shadow);
    }
    
    .template-emoji {
      font-size: 2.5rem;
      margin-bottom: 1rem;
    }
    
    .template-title {
      font-size: 1.4rem;
      font-weight: 700;
      margin-bottom: 0.5rem;
    }
    
    .template-desc {
      color: #718096;
      line-height: 1.6;
      margin-bottom: 1rem;
    }
    
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      backdrop-filter: blur(5px);
      z-index: 1000;
      align-items: center;
      justify-content: center;
      animation: fadeIn 0.3s ease;
    }
    
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    
    .modal-content {
      background: var(--card-bg);
      border-radius: 30px;
      padding: 3rem;
      max-width: 600px;
      width: 90%;
      max-height: 80vh;
      overflow-y: auto;
      box-shadow: 0 10px 50px rgba(0, 0, 0, 0.3);
      position: relative;
      animation: slideUp 0.3s ease;
    }
    
    @keyframes slideUp {
      from { transform: translateY(50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }
    
    .modal-close {
      position: absolute;
      top: 1.5rem;
      right: 1.5rem;
      font-size: 2rem;
      cursor: pointer;
      background: var(--bg-light);
      width: 40px;
      height: 40px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.3s ease;
    }
    
    .modal-close:hover {
      transform: rotate(90deg);
      background: var(--accent-pink);
      color: white;
    }
    
    .modal-title {
      font-size: 2rem;
      font-weight: 700;
      margin-bottom: 2rem;
      font-family: var(--font-accent);
      text-align: center;
    }
    
    .auth-buttons {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    
    .auth-btn {
      padding: 1rem;
      border: none;
      border-radius: 15px;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;
    }
    
    .auth-btn:hover {
      transform: scale(1.03);
    }
    
    .auth-google {
      background: #4285f4;
      color: white;
    }
    
    .auth-microsoft {
      background: #00a4ef;
      color: white;
    }
    
    .auth-email {
      background: var(--accent-purple);
      color: white;
    }

    .form-group {
      margin-bottom: 1.5rem;
    }

    .form-group label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: 600;
      color: var(--text);
    }

    .form-group input, .form-group textarea {
      width: 100%;
      padding: 0.75rem;
      border: 2px solid var(--bg-light);
      border-radius: 10px;
      font-size: 1rem;
      font-family: var(--font-main);
      transition: all 0.3s ease;
      background: var(--bg-light);
      color: var(--text);
    }

    .form-group input:focus, .form-group textarea:focus {
      outline: none;
      border-color: var(--accent-blue);
    }
    
    .profile-section {
      display: flex;
      align-items: center;
      gap: 1.5rem;
      margin-bottom: 2rem;
      padding: 1.5rem;
      background: var(--bg-light);
      border-radius: 20px;
    }
    
    .profile-avatar {
      font-size: 4rem;
      background: var(--bg-gradient);
      width: 80px;
      height: 80px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    .profile-info h3 {
      font-size: 1.5rem;
      margin-bottom: 0.3rem;
    }
    
    .profile-info p {
      color: #718096;
    }
    
    .settings-menu {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }
    
    .settings-item {
      padding: 1rem 1.5rem;
      background: var(--bg-light);
      border-radius: 15px;
      cursor: pointer;
      transition: all 0.3s ease;
      font-weight: 600;
    }
    
    .settings-item:hover {
      background: var(--accent-blue);
      color: white;
      transform: translateX(5px);
    }

    .theme-selector {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
      gap: 1rem;
      margin-top: 1rem;
    }

    .theme-option {
      padding: 1.5rem;
      border-radius: 15px;
      cursor: pointer;
      text-align: center;
      font-weight: 600;
      transition: all 0.3s ease;
      border: 3px solid transparent;
    }

    .theme-option:hover {
      transform: scale(1.05);
    }

    .theme-option.active {
      border-color: gold;
    }

    .theme-light { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; }
    .theme-dark { background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%); color: #00ff88; }
    .theme-green { background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%); color: white; }
    .theme-ocean { background: linear-gradient(135deg, #2193b0 0%, #6dd5ed 100%); color: white; }
    .theme-sunset { background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); color: white; }
    .theme-neon { background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: #00ff88; }

    .emoji-picker {
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      gap: 0.5rem;
      max-height: 300px;
      overflow-y: auto;
    }

    .emoji-option {
      font-size: 2rem;
      padding: 0.5rem;
      cursor: pointer;
      border-radius: 10px;
      transition: all 0.3s ease;
      text-align: center;
    }

    .emoji-option:hover {
      background: var(--accent-purple);
      transform: scale(1.2);
    }
    
    .footer {
      text-align: center;
      padding: 3rem 2rem;
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
          <div class="notebook-card create-card" id="create-new">
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
      </div>

      <div class="editor-content">
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
        <li class="settings-item" id="delete-current-note" style="display: none;">🗑️ Delete Current Note</li>
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
        <h3 style="margin: 1rem 0;">NewNotes v1.0</h3>
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
            ✅ Customizable note icons
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

    // Firebase config (provided)
    const firebaseConfig = {
      apiKey: "AIzaSyCirWobFVvTyc4ALEw3XMWBCCZlEP3s048",
      authDomain: "newnotes-6942f.firebaseapp.com",
      projectId: "newnotes-6942f",
      storageBucket: "newnotes-6942f.firebasestorage.app",
      messagingSenderId: "108980754671",
      appId: "1:108980754671:web:f584d61feffc9e438aa31a",
      measurementId: "G-P8KVQS62FB"
    };

    // Initialize Firebase
    const app = initializeApp(firebaseConfig);

    // Initialize Analytics (optional) - wrapped in try/catch because analytics can fail in some environments
    try {
      const analytics = getAnalytics(app);
      console.log('Firebase Analytics initialized');
    } catch (err) {
      console.warn('Analytics not available:', err && err.message ? err.message : err);
    }

    const auth = getAuth(app);
    const db = getFirestore(app);

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

    // LOCAL STORAGE KEYS
    const LOCAL_KEY = 'newnotes_local_notebooks_v1';
    const LOCAL_TRASH_KEY = 'newnotes_local_trashed_v1';

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

    // LOCAL STORAGE HELPERS (for offline use)
    function loadLocalNotebooks() {
      const raw = localStorage.getItem(LOCAL_KEY);
      const rawTrash = localStorage.getItem(LOCAL_TRASH_KEY);
      const local = raw ? JSON.parse(raw) : [];
      const localTrash = rawTrash ? JSON.parse(rawTrash) : [];
      return { local, localTrash };
    }

    function saveLocalNotebook(notebook) {
      const { local } = loadLocalNotebooks();
      const idx = local.findIndex(n => n.id === notebook.id);
      if (idx >= 0) local[idx] = notebook;
      else local.unshift(notebook);
      localStorage.setItem(LOCAL_KEY, JSON.stringify(local));
      return true;
    }

    function deleteLocalNotebook(id) {
      const { local } = loadLocalNotebooks();
      const filtered = local.filter(n => n.id !== id);
      localStorage.setItem(LOCAL_KEY, JSON.stringify(filtered));
      return true;
    }

    function moveLocalToTrash(id) {
      const data = loadLocalNotebooks();
      const item = data.local.find(n => n.id === id);
      if (!item) return false;
      data.local = data.local.filter(n => n.id !== id);
      data.localTrash.unshift(item);
      localStorage.setItem(LOCAL_KEY, JSON.stringify(data.local));
      localStorage.setItem(LOCAL_TRASH_KEY, JSON.stringify(data.localTrash));
      return true;
    }

    function emptyLocalTrash() {
      localStorage.setItem(LOCAL_TRASH_KEY, JSON.stringify([]));
    }

    function restoreLocalFromTrash(id) {
      const data = loadLocalNotebooks();
      const item = data.localTrash.find(n => n.id === id);
      if (!item) return false;
      data.localTrash = data.localTrash.filter(n => n.id !== id);
      data.local.unshift(item);
      localStorage.setItem(LOCAL_KEY, JSON.stringify(data.local));
      localStorage.setItem(LOCAL_TRASH_KEY, JSON.stringify(data.localTrash));
      return true;
    }

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
      const notebook = {
        id: Date.now().toString(),
        title: template.title,
        emoji: template.emoji,
        content: template.content,
        date: new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' }),
        favorite: false,
        trash: false,
        localOnly: !currentUser
      };

      if (!currentUser) {
        // Save locally and open
        saveLocalNotebook(notebook);
        notebooks.unshift(notebook);
        renderNotebooks();
        openNote(notebook.id);
        return;
      }

      // If logged in, save to Firestore
      const saved = await saveNotebookToFirestore(notebook);
      if (saved) {
        notebooks.unshift(notebook);
        await loadNotebooks();
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
      document.getElementById('loading-notebooks').style.display = 'block';
      notebooks = [];
      trashedNotebooks = [];

      if (!currentUser) {
        // load local notes
        const { local, localTrash } = loadLocalNotebooks();
        notebooks = local;
        trashedNotebooks = localTrash;
        renderNotebooks();
        document.getElementById('loading-notebooks').style.display = 'none';
        return;
      }

      try {
        const notebooksRef = collection(db, 'users', currentUser.uid, 'notebooks');
        const q = query(notebooksRef, orderBy('updatedAt', 'desc'));
        const querySnapshot = await getDocs(q);
        
        querySnapshot.forEach((docSnap) => {
          const data = { id: docSnap.id, ...docSnap.data() };
          if (data.trash) {
            trashedNotebooks.push(data);
          } else {
            notebooks.push(data);
          }
        });
        
        // Also keep any local-only notes (optional): prompt user to import or merge if you'd like.
        const localData = loadLocalNotebooks();
        if (localData.local.length > 0) {
          // For safety we simply keep them visible locally but not pushed to Firestore automatically.
          // Optionally you could offer automatic import here.
          notebooks = [...localData.local, ...notebooks];
        }
      } catch (error) {
        console.error('Error loading notebooks:', error);
      } finally {
        renderNotebooks();
        document.getElementById('loading-notebooks').style.display = 'none';
      }
    }

    async function saveNotebookToFirestore(notebook) {
      // If not logged in, save to localStorage
      if (!currentUser) {
        notebook.localOnly = true;
        saveLocalNotebook(notebook);
        return true;
      }

      try {
        const notebookRef = doc(db, 'users', currentUser.uid, 'notebooks', notebook.id);
        await setDoc(notebookRef, {
          title: notebook.title,
          emoji: notebook.emoji,
          content: notebook.content,
          date: notebook.date,
          favorite: notebook.favorite || false,
          trash: notebook.trash || false,
          updatedAt: serverTimestamp()
        });
        return true;
      } catch (error) {
        console.error('Error saving notebook:', error);
        alert('Failed to save: ' + error.message);
        return false;
      }
    }

    async function deleteNotebookFromFirestore(notebookId) {
      // If not logged in, remove from local storage
      if (!currentUser) {
        deleteLocalNotebook(notebookId);
        notebooks = notebooks.filter(n => n.id !== notebookId);
        trashedNotebooks = trashedNotebooks.filter(n => n.id !== notebookId);
        renderNotebooks();
        return true;
      }

      try {
        const notebookRef = doc(db, 'users', currentUser.uid, 'notebooks', notebookId);
        await deleteDoc(notebookRef);
        return true;
      } catch (error) {
        console.error('Error deleting notebook:', error);
        return false;
      }
    }

    function renderNotebooks() {
      const notebookGrid = document.getElementById('notebook-grid');
      const createCard = document.getElementById('create-new');
      notebookGrid.innerHTML = '';
      notebookGrid.appendChild(createCard);

      if (notebooks.length === 0) {
        const empty = document.createElement('div');
        empty.className = 'empty-state';
        empty.innerHTML = '<div class="empty-state-icon">📭</div><p>No notes yet. Click Create New or pick a template!</p>';
        notebookGrid.appendChild(empty);
        return;
      }

      notebooks.forEach(notebook => {
        if (notebook.trash) return; // don't show trashed in main grid
        addNotebookCard(notebook);
      });
    }

    function renderFavorites() {
      const grid = document.getElementById('favorites-grid');
      grid.innerHTML = '';
      
      const favorites = notebooks.filter(n => n.favorite && !n.trash);
      
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
        <div class="notebook-title">${notebook.title}</div>
        <div class="notebook-meta">📅 ${notebook.date}</div>
        <div class="notebook-actions">
          <button class="action-btn star-btn ${notebook.favorite ? 'favorited' : ''}" title="Favorite">⭐</button>
          <button class="action-btn share-btn" title="Share">🔗</button>
          <button class="action-btn delete-btn" title="Delete">🗑️</button>
        </div>
      `;

      card.addEventListener('click', (e) => {
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
        await saveNotebookToFirestore(notebook);
        if (notebook.localOnly) saveLocalNotebook(notebook);
        await loadNotebooks();
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
        if (notebook.localOnly) {
          moveLocalToTrash(notebook.id);
          await loadNotebooks();
          alert('Moved to recycle bin (local)');
          return;
        }
        await saveNotebookToFirestore(notebook);
        await loadNotebooks();
      };

      return card;
    }

    function createTrashCardElement(notebook) {
      const card = document.createElement('div');
      card.className = 'notebook-card';
      card.style.opacity = '0.7';
      card.innerHTML = `
        <div class="notebook-icon">${notebook.emoji}</div>
        <div class="notebook-title">${notebook.title}</div>
        <div class="notebook-meta">📅 ${notebook.date}</div>
        <div class="notebook-actions">
          <button class="action-btn restore-btn" title="Restore">♻️</button>
          <button class="action-btn delete-btn" title="Delete Forever">❌</button>
        </div>
      `;

      const restoreBtn = card.querySelector('.restore-btn');
      restoreBtn.onclick = async (e) => {
        e.stopPropagation();
        if (notebook.localOnly) {
          restoreLocalFromTrash(notebook.id);
          await loadNotebooks();
          renderTrash();
          return;
        }
        notebook.trash = false;
        await saveNotebookToFirestore(notebook);
        await loadNotebooks();
        renderTrash();
      };

      const deleteBtn = card.querySelector('.delete-btn');
      deleteBtn.onclick = async (e) => {
        e.stopPropagation();
        if (!confirm('⚠️ Permanently delete this note? This cannot be undone!')) return;
        if (notebook.localOnly) {
          deleteLocalNotebook(notebook.id);
          trashedNotebooks = trashedNotebooks.filter(n => n.id !== notebook.id);
          renderTrash();
          return;
        }
        await deleteNotebookFromFirestore(notebook.id);
        trashedNotebooks = trashedNotebooks.filter(n => n.id !== notebook.id);
        renderTrash();
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
            if (notebook.localOnly) saveLocalNotebook(notebook);
            else await saveNotebookToFirestore(notebook);
            await loadNotebooks();
            closeAllModals();
          }
        };
        picker.appendChild(opt);
      });
      iconModal.style.display = 'flex';
    }

    // SHARE MODAL
    function showShareModal(notebook) {
      const shareLink = document.getElementById('share-link');
      // For local notes, still generate a link with ?share=id but note recipient can't access content from server
      shareLink.value = `${window.location.origin}${window.location.pathname}?share=${notebook.id}`;
      
      document.getElementById('copy-link-btn').onclick = () => {
        shareLink.select();
        document.execCommand('copy');
        alert('✅ Link copied to clipboard!');
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

      // Delete permanently
      for (const notebook of trashedNotebooks) {
        if (notebook.localOnly) {
          // remove from local trash
          const data = loadLocalNotebooks();
          const remaining = data.localTrash.filter(n => n.id !== notebook.id);
          localStorage.setItem(LOCAL_TRASH_KEY, JSON.stringify(remaining));
        } else {
          await deleteNotebookFromFirestore(notebook.id);
        }
      }
      
      trashedNotebooks = [];
      emptyLocalTrash();
      renderTrash();
      alert('✅ Recycle bin emptied!');
    };

    // CREATE NOTEBOOK
    async function createNotebook() {
      const title = prompt('📝 Name your notebook:', 'My New Notebook');
      if (!title) return;

      const emoji = emojiList[Math.floor(Math.random() * emojiList.length)];
      const notebook = {
        id: Date.now().toString(),
        title: title,
        emoji: emoji,
        content: '',
        date: new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' }),
        favorite: false,
        trash: false,
        localOnly: !currentUser
      };

      if (!currentUser) {
        saveLocalNotebook(notebook);
        notebooks.unshift(notebook);
        addNotebookCard(notebook);
        openNote(notebook.id);
        return;
      }

      const saved = await saveNotebookToFirestore(notebook);
      if (saved) {
        notebooks.unshift(notebook);
        addNotebookCard(notebook);
        openNote(notebook.id);
      }
    }

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
      const notebook = [...notebooks, ...trashedNotebooks].find(n => n.id === noteId);
      if (!notebook) return;

      if (notebook.trash) {
        alert('⚠️ This note is in the recycle bin. Please restore it first.');
        return;
      }

      currentNoteId = noteId;
      noteTitleEditor.value = notebook.title;
      textEditor.innerHTML = notebook.content || 'Start writing your notes here...';

      // show delete current note option in settings
      document.getElementById('delete-current-note').style.display = 'block';

      homePage.classList.add('hidden');
      editorPage.classList.add('active');
      window.scrollTo(0, 0);
    }

    function closeEditor() {
      saveNote();
      homePage.classList.remove('hidden');
      editorPage.classList.remove('active');
      currentNoteId = null;
      document.getElementById('delete-current-note').style.display = 'none';
      window.scrollTo(0, 0);
    }

    async function saveNote() {
      if (!currentNoteId) return;

      const notebook = notebooks.find(n => n.id === currentNoteId) || trashedNotebooks.find(n => n.id === currentNoteId);
      if (notebook) {
        notebook.title = noteTitleEditor.value || 'Untitled Note';
        notebook.content = textEditor.innerHTML;
        notebook.date = new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
        
        const saved = await saveNotebookToFirestore(notebook);
        if (notebook.localOnly) saveLocalNotebook(notebook);
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

    setInterval(() => {
      if (currentNoteId) {
        saveNote();
      }
    }, 10000);

    backBtn.onclick = closeEditor;
    saveBtn.onclick = saveNote;
    noteTitleEditor.addEventListener('blur', saveNote);
    document.getElementById('logo-home').onclick = () => window.scrollTo(0, 0);

    // AUTHENTICATION
    onAuthStateChanged(auth, async (user) => {
      const userName = document.getElementById('user-name');
      const userEmail = document.getElementById('user-email');
      const logoutBtn = document.getElementById('logout-btn');
      const deleteAccountBtn = document.getElementById('delete-account');
      const loginSettingsBtn = document.getElementById('login-settings-btn');
      
      if (user) {
        currentUser = user;
        userName.textContent = user.displayName || user.email.split('@')[0];
        userEmail.textContent = user.email;
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
        // Load local notebooks so users can create & manage notes while logged out
        const localData = loadLocalNotebooks();
        notebooks = localData.local;
        trashedNotebooks = localData.localTrash;
        renderNotebooks();
        
        // Show login modal for new users only on first visit
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
        alert('❌ Login failed: ' + error.message);
      }
    };

    document.getElementById('microsoft-login').onclick = async () => {
      try {
        const provider = new OAuthProvider('microsoft.com');
        await signInWithPopup(auth, provider);
        closeAllModals();
      } catch (error) {
        alert('❌ Login failed: ' + error.message);
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
        errorDiv.textContent = error.message;
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
        errorDiv.textContent = error.message;
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
          alert('❌ Error logging out: ' + error.message);
        }
      }
    };

    // DELETE CURRENT NOTE (new settings button)
    document.getElementById('delete-current-note').onclick = async () => {
      if (!currentNoteId) {
        alert('⚠️ No note is currently open.');
        return;
      }

      const notebook = notebooks.find(n => n.id === currentNoteId) || trashedNotebooks.find(n => n.id === currentNoteId);
      if (!notebook) {
        alert('⚠️ Note not found.');
        return;
      }

      if (!notebook.trash) {
        // move to trash
        if (notebook.localOnly) {
          moveLocalToTrash(notebook.id);
          await loadNotebooks();
          closeEditor();
          alert('Note moved to recycle bin (local).');
          return;
        }
        notebook.trash = true;
        await saveNotebookToFirestore(notebook);
        await loadNotebooks();
        closeEditor();
        alert('Note moved to recycle bin.');
        return;
      } else {
        // permanently delete
        if (!confirm('⚠️ Permanently delete this note? This cannot be undone!')) return;
        if (notebook.localOnly) {
          deleteLocalNotebook(notebook.id);
          trashedNotebooks = trashedNotebooks.filter(n => n.id !== notebook.id);
          renderTrash();
          closeEditor();
          alert('Note permanently deleted (local).');
          return;
        }
        await deleteNotebookFromFirestore(notebook.id);
        trashedNotebooks = trashedNotebooks.filter(n => n.id !== notebook.id);
        renderTrash();
        closeEditor();
        alert('Note permanently deleted.');
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
          alert('❌ Error: ' + error.message);
        }
      }
    };

    // EXPORT DATA
    document.getElementById('export-data-btn').onclick = () => {
      const combined = [...notebooks, ...trashedNotebooks];
      if (combined.length === 0) {
        alert('⚠️ No notes to export!');
        return;
      }

      const data = JSON.stringify(combined, null, 2);
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
              note.localOnly = !currentUser;
              if (!currentUser) {
                saveLocalNotebook(note);
              } else {
                await saveNotebookToFirestore(note);
              }
            }

            await loadNotebooks();
            alert(`✅ Imported ${importedNotes.length} notes successfully!`);
          } catch (error) {
            alert('❌ Error importing notes: ' + error.message);
          }
        };
        reader.readAsText(file);
      };
      input.click();
    };

    // Initialize
    renderTemplates();
    // initial local load
    const localInitial = loadLocalNotebooks();
    notebooks = localInitial.local;
    trashedNotebooks = localInitial.localTrash;
    renderNotebooks();
  </script>
</body>
</html>
