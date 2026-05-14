<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>GROUP EIGHT</title>
  <style>
    /* ── Self-contained system font fallbacks (no internet required) ── */
    @font-face {
      font-family: 'Syne';
      src: local('Arial Black'), local('Impact'), local('Franklin Gothic Heavy');
      font-weight: 700 800;
    }
    @font-face {
      font-family: 'DM Sans';
      src: local('Segoe UI'), local('Helvetica Neue'), local('Arial'), local('sans-serif');
      font-weight: 300 400 500;
    }
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg:      #0c0c0e; --surface: #161618; --card: #1e1e22;
      --accent:  #1db954; --accent2: #1ed760;
      --text:    #f0f0f0; --muted:   #888;    --border: #2a2a2e;
    }
    html { scroll-behavior: smooth; }
    body { background: var(--bg); color: var(--text); font-family: 'DM Sans','Segoe UI','Helvetica Neue',Arial,sans-serif; min-height: 100vh; }
    .layout { display: flex; min-height: 100vh; }

    /* ── SIDEBAR ── */
    .sidebar {
      width: 220px; background: #101012;
      display: flex; flex-direction: column; padding: 28px 0 20px;
      position: fixed; top:0; left:0; bottom:0;
      z-index: 200; border-right: 1px solid var(--border);
    }
    .sidebar-logo {
      font-family:'Syne','Arial Black','Impact',sans-serif; font-weight:800; font-size:1.1rem;
      color:var(--accent); letter-spacing:2px; text-transform:uppercase;
      padding:0 24px 28px; border-bottom:1px solid var(--border);
    }
    .sidebar-logo span { color: var(--text); }
    .nav-section { padding: 18px 12px 8px; }
    .nav-label { font-size:.68rem; letter-spacing:2px; text-transform:uppercase; color:var(--muted); padding:0 12px; margin-bottom:6px; }
    .nav-item {
      display:flex; align-items:center; gap:12px; padding:10px 12px;
      border-radius:8px; cursor:pointer; color:var(--muted);
      font-size:.92rem; font-weight:500; transition:all .2s; text-decoration:none;
    }
    .nav-item:hover { background:var(--card); color:var(--text); }
    .nav-item.active { background:var(--card); color:var(--accent); }
    .nav-item .icon { font-size:1.1rem; width:20px; text-align:center; }
    .sidebar-bottom { margin-top:auto; padding:16px 24px; border-top:1px solid var(--border); }
    .user-pill { display:flex; align-items:center; gap:10px; }
    .user-avatar {
      width:34px; height:34px; border-radius:50%;
      background:linear-gradient(135deg,var(--accent),#0a7a32);
      display:flex; align-items:center; justify-content:center;
      font-weight:700; font-size:.8rem; color:#000; flex-shrink:0;
    }
    .user-name { font-size:.88rem; font-weight:500; }
    .user-sub  { font-size:.75rem; color:var(--muted); }

    /* ── MAIN ── */
    .main { margin-left:220px; flex:1; padding-bottom:90px; }

    /* ── PAGES ── */
    .page { display:none; flex-direction:column; }
    .page.active { display:flex; animation:fadeIn .35s ease; }
    @keyframes fadeIn { from{opacity:0;transform:translateY(14px)} to{opacity:1;transform:translateY(0)} }

    /* ── HOME ── */
    #page-home { padding:40px 40px 20px; gap:40px; }
    .hero {
      border-radius:20px; overflow:hidden; height:300px;
      background:
        linear-gradient(120deg,rgba(0,0,0,.92) 35%,transparent 80%),
        linear-gradient(to bottom,transparent 40%,rgba(12,12,14,1) 100%),
        linear-gradient(135deg, #1a1a2e 0%, #16213e 30%, #0f3460 60%, #1db954 100%);
      display:flex; align-items:flex-end; padding:36px;
    }
    .hero-tag  { font-size:.72rem; letter-spacing:3px; text-transform:uppercase; color:var(--accent); font-weight:700; margin-bottom:10px; }
    .hero-title{ font-family:'Syne','Arial Black',Impact,sans-serif; font-size:2.6rem; font-weight:800; line-height:1; color:#fff; margin-bottom:8px; }
    .hero-sub  { color:#aaa; font-size:.92rem; margin-bottom:18px; }
    .hero-btns { display:flex; gap:12px; }
    .btn {
      display:inline-flex; align-items:center; gap:8px;
      padding:10px 22px; border-radius:50px; font-size:.88rem; font-weight:600;
      cursor:pointer; border:none; transition:all .2s; font-family:'DM Sans','Segoe UI','Helvetica Neue',Arial,sans-serif;
    }
    .btn-green { background:var(--accent); color:#000; }
    .btn-green:hover { background:var(--accent2); transform:scale(1.04); }
    .btn-ghost { background:rgba(255,255,255,.12); color:#fff; border:1px solid rgba(255,255,255,.2); }
    .btn-ghost:hover { background:rgba(255,255,255,.2); }
    .sec-header { display:flex; align-items:baseline; justify-content:space-between; margin-bottom:16px; }
    .sec-title { font-family:'Syne','Arial Black',Impact,sans-serif; font-size:1.2rem; font-weight:700; }
    .sec-more { font-size:.78rem; color:var(--muted); cursor:pointer; letter-spacing:.5px; text-transform:uppercase; transition:color .2s; }
    .sec-more:hover { color:var(--text); }
    .album-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(155px,1fr)); gap:18px; }
    .album-card {
      background:var(--card); border-radius:14px; padding:14px;
      cursor:pointer; transition:background .2s,transform .2s; position:relative;
    }
    .album-card:hover { background:#26262c; transform:translateY(-3px); }
    .album-card:hover .album-play { opacity:1; transform:translateY(0); }
    .album-thumb, .album-thumb-placeholder {
      width:100%; aspect-ratio:1; border-radius:10px; margin-bottom:10px;
      display:flex; align-items:center; justify-content:center; font-size:2.2rem;
    }
    .album-play {
      position:absolute; bottom:68px; right:18px;
      width:38px; height:38px; background:var(--accent); border-radius:50%;
      display:flex; align-items:center; justify-content:center;
      font-size:.9rem; color:#000; opacity:0; transform:translateY(6px);
      transition:all .25s; box-shadow:0 6px 20px rgba(29,185,84,.4);
    }
    .album-name   { font-weight:700; font-size:.82rem; margin-bottom:3px; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
    .album-artist { font-size:.75rem; color:var(--muted); white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
    .album-rank {
      position:absolute; top:10px; left:10px;
      background:rgba(0,0,0,.7); color:var(--accent);
      font-size:.7rem; font-weight:800; padding:2px 8px; border-radius:20px; letter-spacing:1px;
    }
    .song-list { display:flex; flex-direction:column; gap:2px; }
    .song-row { display:flex; align-items:center; gap:14px; padding:9px 12px; border-radius:10px; cursor:pointer; transition:background .15s; }
    .song-row:hover { background:var(--card); }
    .song-row.playing { background:rgba(29,185,84,.1); }
    .song-row.playing .song-title { color:var(--accent); }
    .song-num { width:24px; text-align:center; color:var(--muted); font-size:.85rem; font-weight:700; flex-shrink:0; }
    .song-thumb { width:44px; height:44px; border-radius:8px; flex-shrink:0; display:flex; align-items:center; justify-content:center; font-size:1.3rem; }
    .song-info { flex:1; min-width:0; }
    .song-title  { font-weight:500; font-size:.9rem; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
    .song-artist { font-size:.78rem; color:var(--muted); }
    .song-genre { font-size:.68rem; font-weight:700; letter-spacing:1px; padding:2px 8px; border-radius:20px; background:rgba(29,185,84,.12); color:var(--accent); flex-shrink:0; }
    .song-duration { font-size:.82rem; color:var(--muted); flex-shrink:0; }

    /* ── PLAYER PAGE ── */
    #page-player { padding:40px; align-items:center; gap:32px; }
    .player-layout { display:flex; gap:48px; align-items:flex-start; width:100%; max-width:980px; margin:0 auto; }
    .player-left { flex:0 0 300px; display:flex; flex-direction:column; align-items:center; gap:22px; }
    .now-playing-art {
      width:280px; height:280px; border-radius:20px;
      display:flex; align-items:center; justify-content:center;
      font-size:5rem; box-shadow:0 30px 80px rgba(0,0,0,.6);
      transition:background .6s; position:relative; cursor:pointer;
    }
    .now-playing-art.playing::after {
      content:''; position:absolute; inset:-6px; border-radius:26px;
      border:2px solid var(--accent);
      animation:pulse-ring 2s ease-in-out infinite;
    }
    @keyframes pulse-ring { 0%,100%{opacity:.4;transform:scale(1)} 50%{opacity:1;transform:scale(1.03)} }
    .np-info { text-align:center; }
    .np-title  { font-family:'Syne','Arial Black',Impact,sans-serif; font-size:1.5rem; font-weight:800; margin-bottom:4px; }
    .np-artist { color:var(--muted); font-size:.95rem; }
    .np-genre  { font-size:.72rem; letter-spacing:2px; text-transform:uppercase; color:var(--accent); margin-top:6px; }
    .np-actions { display:flex; gap:18px; align-items:center; }
    .action-btn { background:none; border:none; color:var(--muted); font-size:1.2rem; cursor:pointer; transition:color .2s,transform .2s; }
    .action-btn:hover { color:var(--text); transform:scale(1.15); }
    .action-btn.liked { color:var(--accent); }
    .player-controls { width:100%; }
    .controls-row { display:flex; align-items:center; justify-content:center; gap:20px; margin-bottom:16px; }
    .ctrl-btn { background:none; border:none; color:var(--muted); font-size:1.25rem; cursor:pointer; transition:color .2s; }
    .ctrl-btn:hover { color:var(--text); }
    .ctrl-btn.active { color:var(--accent); }
    .play-btn-big {
      width:54px; height:54px; border-radius:50%; background:var(--accent); color:#000; border:none;
      font-size:1.2rem; cursor:pointer; display:flex; align-items:center; justify-content:center;
      transition:all .2s; box-shadow:0 8px 25px rgba(29,185,84,.4);
    }
    .play-btn-big:hover { background:var(--accent2); transform:scale(1.07); }
    .yt-open-btn {
      display:flex; align-items:center; gap:8px;
      background:#ff0000; color:#fff; border:none;
      padding:11px 22px; border-radius:50px; font-size:.88rem; font-weight:600;
      cursor:pointer; font-family:'DM Sans','Segoe UI','Helvetica Neue',Arial,sans-serif; transition:all .2s;
      box-shadow:0 4px 18px rgba(255,0,0,.3);
    }
    .yt-open-btn:hover { background:#cc0000; transform:scale(1.04); }
    .player-right { flex:1; min-width:0; }
    .queue-title    { font-family:'Syne','Arial Black',Impact,sans-serif; font-size:1.1rem; font-weight:700; margin-bottom:6px; }
    .queue-subtitle { font-size:.78rem; color:var(--muted); margin-bottom:14px; }

    /* ── VIDEO MODAL ── */
    #yt-modal {
      display:none; position:fixed; inset:0;
      background:rgba(0,0,0,.88); z-index:9999;
      align-items:center; justify-content:center; flex-direction:column; gap:16px;
    }
    #yt-modal.open { display:flex; animation:fadeIn .2s ease; }
    .modal-label { color:var(--muted); font-size:.84rem; }
    .modal-video-wrap {
      position:relative; width:min(860px,94vw); aspect-ratio:16/9;
      border-radius:16px; overflow:hidden; box-shadow:0 30px 80px rgba(0,0,0,.9);
    }
    .modal-video-wrap iframe { width:100%; height:100%; border:none; display:block; }
    .modal-close-btn {
      background:rgba(255,255,255,.14); border:1px solid rgba(255,255,255,.22);
      color:#fff; padding:10px 32px; border-radius:50px; font-size:.9rem;
      cursor:pointer; font-family:'DM Sans','Segoe UI','Helvetica Neue',Arial,sans-serif; transition:background .2s;
    }
    .modal-close-btn:hover { background:rgba(255,255,255,.25); }

    /* ── BOTTOM BAR ── */
    .player-bar {
      position:fixed; bottom:0; left:0; right:0; height:86px; background:#181818;
      border-top:1px solid var(--border); display:flex; align-items:center;
      padding:0 24px; gap:16px; z-index:300;
    }
    .bar-track { display:flex; align-items:center; gap:14px; flex:0 0 260px; }
    .bar-art {
      width:50px; height:50px; border-radius:8px;
      display:flex; align-items:center; justify-content:center;
      font-size:1.4rem; flex-shrink:0; transition:background .6s; cursor:pointer;
    }
    .bar-title  { font-weight:600; font-size:.88rem; margin-bottom:2px; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; max-width:140px; }
    .bar-artist { font-size:.76rem; color:var(--muted); white-space:nowrap; overflow:hidden; text-overflow:ellipsis; max-width:140px; }
    .bar-like { background:none; border:none; color:var(--muted); font-size:1.1rem; cursor:pointer; transition:color .2s; }
    .bar-like:hover,.bar-like.liked { color:var(--accent); }
    .bar-controls { flex:1; display:flex; flex-direction:column; align-items:center; gap:7px; }
    .bar-ctrl-row { display:flex; align-items:center; gap:18px; }
    .bar-btn { background:none; border:none; color:var(--muted); font-size:1rem; cursor:pointer; transition:color .2s; }
    .bar-btn:hover { color:var(--text); }
    .bar-play {
      width:33px; height:33px; border-radius:50%; background:#fff; color:#000; border:none;
      font-size:.85rem; cursor:pointer; display:flex; align-items:center; justify-content:center; transition:transform .2s;
    }
    .bar-play:hover { transform:scale(1.08); }
    .bar-hint { font-size:.7rem; color:var(--muted); }
    .bar-right { flex:0 0 160px; display:flex; align-items:center; justify-content:flex-end; }

    /* ── SEARCH ── */
    #page-search { padding:40px; gap:24px; }
    .search-input {
      padding:14px 20px; border-radius:50px; border:1px solid var(--border);
      background:var(--card); color:var(--text); font-size:1rem; outline:none;
      max-width:500px; font-family:'DM Sans','Segoe UI','Helvetica Neue',Arial,sans-serif; transition:border-color .2s;
    }
    .search-input:focus { border-color:var(--accent); }

    /* ── RESPONSIVE ── */
    @media(max-width:860px){
      .sidebar{width:60px;}
      .sidebar-logo,.nav-label,.nav-item span,.user-name,.user-sub{display:none;}
      .nav-item{justify-content:center;padding:12px;}
      .main{margin-left:60px;}
      .player-layout{flex-direction:column;align-items:center;}
      .player-right{width:100%;}
    }
    @media(max-width:600px){
      #page-home,#page-player,#page-search{padding:20px 16px;}
      .hero{height:200px;padding:20px;}
      .hero-title{font-size:1.8rem;}
    }
    ::-webkit-scrollbar{width:5px;}
    ::-webkit-scrollbar-track{background:transparent;}
    ::-webkit-scrollbar-thumb{background:var(--border);border-radius:10px;}
  </style>
</head>
<body>

<!-- ══ VIDEO MODAL — opens on play, works from any local file ══ -->
<div id="yt-modal">
  <div class="modal-label" id="modal-label">Now Playing</div>
  <div class="modal-video-wrap">
    <iframe id="yt-iframe" src="" allow="autoplay; encrypted-media" allowfullscreen></iframe>
  </div>
  <button class="modal-close-btn" onclick="closeModal()">✕ &nbsp;Close Player</button>
</div>

<div class="layout">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="sidebar-logo">GROUP<span> EIGHT</span></div>
    <div class="nav-section">
      <div class="nav-label">Menu</div>
      <a class="nav-item active" onclick="showPage('home',this)"><span class="icon">🏠</span><span>Home</span></a>
      <a class="nav-item" onclick="showPage('search',this)"><span class="icon">🔍</span><span>Search</span></a>
      <a class="nav-item" onclick="showPage('player',this)"><span class="icon">🎵</span><span>Now Playing</span></a>
    </div>
    <div class="nav-section">
      <div class="nav-label">Library</div>
      <a class="nav-item" onclick="showPage('liked',this)"><span class="icon">💚</span><span>Liked Songs</span></a>
      <a class="nav-item" onclick="showPage('playlist',this)"><span class="icon">📋</span><span>Playlists</span></a>
      <a class="nav-item" onclick="showPage('members',this)"><span class="icon">👥</span><span>Members</span></a>
    </div>
    <div class="sidebar-bottom">
      <div class="user-pill">
        <div class="user-avatar">G8</div>
        <div><div class="user-name">Group Eight</div><div class="user-sub">Free Plan</div></div>
      </div>
    </div>
  </aside>

  <!-- MAIN -->
  <main class="main">

    <!-- HOME -->
    <div class="page active" id="page-home">
      <div class="hero">
        <div>
          <div class="hero-tag">🇵🇭 Billboard Philippines</div>
          <div class="hero-title">Top Music in the Philippines</div>
          <div class="hero-sub">Featuring trending OPM and popular songs in the Philippines.</div>
          <div class="hero-btns">
            <button class="btn btn-green" onclick="playTrack(0);showPage('player',document.querySelectorAll('.nav-item')[2])">▶ Play All</button>
            <button class="btn btn-ghost">+ Save</button>
          </div>
        </div>
      </div>
      <div>
        <div class="sec-header">
          <div class="sec-title">🔥 Top 10 This Week</div>
          <div class="sec-more">Billboard PH</div>
        </div>
        <div class="album-grid" id="album-grid"></div>
      </div>
      <div>
        <div class="sec-header">
          <div class="sec-title">📋 Full Chart</div>
          <div class="sec-more">See all</div>
        </div>
        <div class="song-list" id="home-song-list"></div>
      </div>
    </div>

    <!-- NOW PLAYING -->
    <div class="page" id="page-player">
      <div class="player-layout">
        <div class="player-left">
          <div class="now-playing-art" id="big-art" onclick="openModal()" title="Click to watch / listen">
            <span id="big-art-emoji">🎵</span>
          </div>
          <div class="np-info">
            <div class="np-title"  id="np-title">Select a track</div>
            <div class="np-artist" id="np-artist">— —</div>
            <div class="np-genre"  id="np-genre"></div>
          </div>
          <div class="np-actions">
            <button class="action-btn" id="like-btn" onclick="toggleLike()">♡</button>
            <button class="action-btn">⋯</button>
            <button class="action-btn">↗</button>
          </div>
          <div class="player-controls">
            <div class="controls-row">
              <button class="ctrl-btn" id="shuffle-btn" onclick="toggleShuffle()">🔀</button>
              <button class="ctrl-btn" onclick="prevTrack()">⏮</button>
              <button class="play-btn-big" id="big-play-btn" onclick="togglePlay()">▶</button>
              <button class="ctrl-btn" onclick="nextTrack()">⏭</button>
              <button class="ctrl-btn" id="repeat-btn" onclick="toggleRepeat()">🔁</button>
            </div>
            <div style="display:flex;justify-content:center;">
              <button class="yt-open-btn" onclick="openModal()">▶ &nbsp;Watch / Listen on YouTube</button>
            </div>
          </div>
        </div>
        <div class="player-right">
          <div class="queue-title">Up Next</div>
          <div class="queue-subtitle">Top 10 Philippines · Billboard PH, May 2026</div>
          <div class="song-list" id="queue-list"></div>
        </div>
      </div>
    </div>

    <!-- SEARCH -->
    <div class="page" id="page-search">
      <div class="sec-title" style="font-size:1.6rem;">🔍 Search</div>
      <input class="search-input" type="text" placeholder="Search songs or artists…" oninput="searchTracks(this.value)"/>
      <div class="song-list" id="search-results"></div>
    </div>

    <!-- LIKED -->
    <div class="page" id="page-liked" style="padding:40px;gap:16px;">
      <div class="sec-title" style="font-family:'Syne','Arial Black',Impact,sans-serif;font-size:1.6rem;">💚 Liked Songs</div>
      <div class="song-list" id="liked-list"></div>
    </div>

    <!-- PLAYLISTS -->
    <div class="page" id="page-playlist" style="padding:40px;gap:16px;">
      <div class="sec-title" style="font-family:'Syne','Arial Black',Impact,sans-serif;font-size:1.6rem;">📋 Playlists</div>
      <p style="color:var(--muted)">No playlists yet. Start by liking some songs!</p>
    </div>

    <!-- MEMBERS -->
    <div class="page" id="page-members" style="padding:40px;gap:20px;">
      <div class="sec-title" style="font-family:'Syne','Arial Black',Impact,sans-serif;font-size:2rem;">👥 Group Members</div>
      <div class="album-grid">
        <div class="album-card">
          <div class="album-thumb-placeholder" style="background:linear-gradient(135deg,#6a11cb,#2575fc)">♐</div>
          <div class="album-name">ALARAS, FRANZEN</div>
          <div class="album-artist">Sagittarius • 20 Years Old</div>
          <p style="margin-top:10px;color:#ccc;font-size:.85rem;">"NO MORE REPEATED CYCLES. IT'S TIME TO GROW NOW."</p>
        </div>
        <div class="album-card">
          <div class="album-thumb-placeholder" style="background:linear-gradient(135deg,#11998e,#38ef7d)">♒</div>
          <div class="album-name">FERRER, RICHARD ANDREW</div>
          <div class="album-artist">Aquarius • 20 Years Old</div>
          <p style="margin-top:10px;color:#ccc;font-size:.85rem;">"STAY FOCUSED AND TRUST GOD'S TIMING"</p>
        </div>
        <div class="album-card">
          <div class="album-thumb-placeholder" style="background:linear-gradient(135deg,#fc466b,#3f5efb)">♍</div>
          <div class="album-name">GAVIOLA, JUAN CARLOS</div>
          <div class="album-artist">Virgo • 19 Years Old</div>
          <p style="margin-top:10px;color:#ccc;font-size:.85rem;">"You are braver than you believe, stronger than you seem, and smarter than you think."</p>
        </div>
      </div>
    </div>

  </main>
</div>

<!-- BOTTOM BAR -->
<div class="player-bar">
  <div class="bar-track">
    <div class="bar-art" id="bar-art" onclick="openModal()" title="Open video">🎵</div>
    <div>
      <div class="bar-title"  id="bar-title">No track playing</div>
      <div class="bar-artist" id="bar-artist">—</div>
    </div>
    <button class="bar-like" id="bar-like-btn" onclick="toggleLike()">♡</button>
  </div>
  <div class="bar-controls">
    <div class="bar-ctrl-row">
      <button class="bar-btn" onclick="toggleShuffle()">🔀</button>
      <button class="bar-btn" onclick="prevTrack()">⏮</button>
      <button class="bar-play" id="bar-play-btn" onclick="togglePlay()">▶</button>
      <button class="bar-btn" onclick="nextTrack()">⏭</button>
      <button class="bar-btn" onclick="toggleRepeat()">🔁</button>
    </div>
    <div class="bar-hint">Press ▶ or click album art to open the video popup</div>
  </div>
  <div class="bar-right">
    <button onclick="openModal()" style="background:rgba(255,0,0,.15);border:1px solid rgba(255,0,0,.35);color:#ff6b6b;padding:8px 16px;border-radius:20px;font-size:.76rem;cursor:pointer;font-family:'DM Sans','Segoe UI','Helvetica Neue',Arial,sans-serif;transition:background .2s;">▶ Open Video</button>
  </div>
</div>

<script>
const tracks = [
  {rank:1,  title:"Palagi",            artist:"TJ Monterde",      genre:"OPM",         emoji:"🎶", color:["#6a11cb","#2575fc"], src:"https://www.youtube.com/embed/v82VtUUGFqk",  duration:"4:12"},
  {rank:2,  title:"Dilaw",             artist:"Maki",             genre:"OPM",         emoji:"💛", color:["#f7971e","#ffd200"], src:"https://www.youtube.com/embed/L215z9C4Zd8",  duration:"3:40"},
  {rank:3,  title:"Sining",            artist:"Dionela ft. Jay R", genre:"R&B",        emoji:"🎨", color:["#fc466b","#3f5efb"], src:"https://www.youtube.com/embed/LLqDfGFMJbk",  duration:"4:01"},
  {rank:4,  title:"Pantropiko",        artist:"BINI",             genre:"P-POP",       emoji:"🌴", color:["#11998e","#38ef7d"], src:"https://www.youtube.com/embed/Zx31bB2vMns",  duration:"3:45"},
  {rank:5,  title:"Salamin, Salamin",  artist:"BINI",             genre:"P-POP",       emoji:"🪞", color:["#8e2de2","#4a00e0"], src:"https://www.youtube.com/embed/J1Ip2sC_lss",  duration:"3:30"},
  {rank:6,  title:"Maybe This Time",   artist:"Sarah Geronimo",   genre:"Pop",         emoji:"💖", color:["#ff758c","#ff7eb3"], src:"https://www.youtube.com/embed/1Q8KI5_wmRk",  duration:"4:10"},
  {rank:7,  title:"Raining in Manila", artist:"Lola Amour",       genre:"Indie",       emoji:"🌧️",color:["#2193b0","#6dd5ed"], src:"https://www.youtube.com/embed/dglBgJSMr-E",  duration:"5:02"},
  {rank:8,  title:"Uhaw",              artist:"Dilaw",            genre:"Alternative", emoji:"🔥", color:["#ff512f","#dd2476"], src:"https://www.youtube.com/embed/c1cRRSozPMw",  duration:"4:22"},
  {rank:9,  title:"Pasilyo",           artist:"SunKissed Lola",   genre:"Indie",       emoji:"🌙", color:["#141e30","#243b55"], src:"https://www.youtube.com/embed/XToA-1dZYWA",  duration:"4:08"},
  {rank:10, title:"Ere",               artist:"Juan Karlos",      genre:"Rock",        emoji:"⚡", color:["#0f2027","#2c5364"], src:"https://www.youtube.com/embed/b3Jvx9ORvx0",  duration:"5:00"}
];

let currentIndex = -1, isPlaying = false, isShuffle = false, isRepeat = false;
const likedSet = new Set();

/* ── Modal ── */
function openModal() {
  if (currentIndex === -1) { playTrack(0); return; }
  const t = tracks[currentIndex];
  document.getElementById('yt-iframe').src = t.src + '?autoplay=1&rel=0';
  document.getElementById('modal-label').textContent = '▶ ' + t.title + ' — ' + t.artist;
  document.getElementById('yt-modal').classList.add('open');
  document.body.style.overflow = 'hidden';
  isPlaying = true;
  updatePlayButtons();
}
function closeModal() {
  document.getElementById('yt-iframe').src = '';
  document.getElementById('yt-modal').classList.remove('open');
  document.body.style.overflow = '';
  isPlaying = false;
  updatePlayButtons();
}
document.getElementById('yt-modal').addEventListener('click', e => { if (e.target === document.getElementById('yt-modal')) closeModal(); });
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });

/* ── Navigation ── */
function showPage(name, el) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  const page = document.getElementById('page-' + name);
  if (page) page.classList.add('active');
  if (el) el.classList.add('active');
  if (name === 'liked') renderLiked();
}

/* ── Render ── */
function renderAlbums() {
  document.getElementById('album-grid').innerHTML = tracks.map((t,i) => `
    <div class="album-card" onclick="playTrack(${i});showPage('player',document.querySelectorAll('.nav-item')[2])">
      <div class="album-rank">#${t.rank}</div>
      <div class="album-thumb" style="background:linear-gradient(135deg,${t.color[0]},${t.color[1]})">${t.emoji}</div>
      <div class="album-play">▶</div>
      <div class="album-name">${t.title}</div>
      <div class="album-artist">${t.artist}</div>
    </div>`).join('');
}
function songRowHTML(t, i, pfx) {
  return `
    <div class="song-row ${i===currentIndex?'playing':''}" id="${pfx}-${i}"
         onclick="playTrack(${i});showPage('player',document.querySelectorAll('.nav-item')[2])">
      <div class="song-num">${t.rank}</div>
      <div class="song-thumb" style="background:linear-gradient(135deg,${t.color[0]},${t.color[1]})">${t.emoji}</div>
      <div class="song-info"><div class="song-title">${t.title}</div><div class="song-artist">${t.artist}</div></div>
      <div class="song-genre">${t.genre}</div>
      <div class="song-duration">${t.duration}</div>
    </div>`;
}
function renderHomeSongs() { document.getElementById('home-song-list').innerHTML = tracks.map((t,i) => songRowHTML(t,i,'home-row')).join(''); }
function renderQueue() {
  document.getElementById('queue-list').innerHTML = tracks.map((t,i) => `
    <div class="song-row ${i===currentIndex?'playing':''}" id="queue-row-${i}" onclick="playTrack(${i})">
      <div class="song-num">${t.rank}</div>
      <div class="song-thumb" style="background:linear-gradient(135deg,${t.color[0]},${t.color[1]})">${t.emoji}</div>
      <div class="song-info"><div class="song-title">${t.title}</div><div class="song-artist">${t.artist}</div></div>
      <div class="song-duration">${t.duration}</div>
    </div>`).join('');
}
function renderLiked() {
  const list = document.getElementById('liked-list');
  if (!likedSet.size) { list.innerHTML = '<p style="color:var(--muted)">Like some songs and they\'ll appear here! ♡</p>'; return; }
  list.innerHTML = [...likedSet].map(idx => songRowHTML(tracks[idx],idx,'liked-row')).join('');
}

/* ── Playback ── */
function playTrack(i) {
  currentIndex = i;
  const t = tracks[i];
  updateTrackInfo(t);
  renderHomeSongs();
  renderQueue();
  openModal();  // auto-open video popup and start playing
}
function updateTrackInfo(t) {
  document.getElementById('big-art-emoji').textContent = t.emoji;
  document.getElementById('big-art').style.background = `linear-gradient(135deg,${t.color[0]},${t.color[1]})`;
  document.getElementById('big-art').classList.add('playing');
  document.getElementById('np-title').textContent  = t.title;
  document.getElementById('np-artist').textContent = t.artist;
  document.getElementById('np-genre').textContent  = t.genre;
  document.getElementById('bar-art').textContent   = t.emoji;
  document.getElementById('bar-art').style.background = `linear-gradient(135deg,${t.color[0]},${t.color[1]})`;
  document.getElementById('bar-title').textContent  = t.title;
  document.getElementById('bar-artist').textContent = t.artist;
}
function togglePlay() {
  if (currentIndex === -1) { playTrack(0); return; }
  isPlaying ? closeModal() : openModal();
}
function updatePlayButtons() {
  document.getElementById('big-play-btn').textContent = isPlaying ? '⏸' : '▶';
  document.getElementById('bar-play-btn').textContent = isPlaying ? '⏸' : '▶';
}
function nextTrack() { playTrack(isShuffle ? Math.floor(Math.random()*tracks.length) : (currentIndex+1)%tracks.length); }
function prevTrack() { playTrack((currentIndex-1+tracks.length)%tracks.length); }
function toggleShuffle() { isShuffle=!isShuffle; document.getElementById('shuffle-btn').classList.toggle('active',isShuffle); }
function toggleRepeat()  { isRepeat =!isRepeat;  document.getElementById('repeat-btn').classList.toggle('active',isRepeat); }
function toggleLike() {
  if (currentIndex===-1) return;
  likedSet.has(currentIndex)?likedSet.delete(currentIndex):likedSet.add(currentIndex);
  const liked=likedSet.has(currentIndex);
  ['like-btn','bar-like-btn'].forEach(id=>{
    document.getElementById(id).textContent=liked?'♥':'♡';
    document.getElementById(id).classList.toggle('liked',liked);
  });
}
function searchTracks(q) {
  const res=document.getElementById('search-results');
  if(!q){res.innerHTML='';return;}
  const found=tracks.filter(t=>t.title.toLowerCase().includes(q.toLowerCase())||t.artist.toLowerCase().includes(q.toLowerCase()));
  res.innerHTML=found.map(t=>songRowHTML(t,tracks.indexOf(t),'search-row')).join('')||'<p style="color:var(--muted);padding:10px">No results found.</p>';
}

renderAlbums(); renderHomeSongs(); renderQueue();
</script>
</body>
</html>

