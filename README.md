# Loftify-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>Loftify – Free Music Streaming</title>
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#0a0a0f">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Loftify">
<meta name="description" content="Loftify – Free music streaming. All premium features free. No ads, no limits.">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500;9..40,600&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0a0a0f;--surface:#13131a;--surface2:#1c1c28;--surface3:#252535;
  --accent:#c8f04c;--accent2:#7c6af5;--accent3:#f05c8a;
  --text:#f0f0f8;--muted:#6a6a90;--border:#2a2a3f;--ph:88px;
}
*{margin:0;padding:0;box-sizing:border-box;}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:'DM Sans',sans-serif;overflow:hidden;}

/* ── LAYOUT ── */
#app{display:grid;grid-template-columns:240px 1fr;grid-template-rows:1fr var(--ph);height:100vh;}
#sidebar{grid-row:1;background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;overflow:hidden;}
#main{grid-row:1;overflow-y:auto;position:relative;scroll-behavior:smooth;}
#player{grid-column:1/3;background:var(--surface);border-top:1px solid var(--border);}

/* ── SIDEBAR ── */
.logo{padding:24px 20px 16px;display:flex;align-items:center;gap:10px;flex-shrink:0;}
.logo-icon{width:34px;height:34px;background:var(--accent);border-radius:9px;display:grid;place-items:center;flex-shrink:0;}
.logo-icon svg{width:18px;height:18px;}
.logo-name{font-family:'Syne',sans-serif;font-weight:800;font-size:19px;letter-spacing:-.5px;}
.logo-badge{background:var(--accent);color:#000;font-size:9px;font-weight:800;padding:2px 6px;border-radius:20px;margin-left:3px;vertical-align:middle;}

.nav{flex:1;overflow-y:auto;padding:0 10px;}
.nav::-webkit-scrollbar{width:0;}
.nl{font-size:10px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px;padding:0 10px;margin:16px 0 6px;}
.ni{display:flex;align-items:center;gap:10px;padding:9px 10px;border-radius:9px;cursor:pointer;font-size:13.5px;color:var(--muted);transition:all .15s;user-select:none;}
.ni:hover{background:var(--surface2);color:var(--text);}
.ni.active{background:rgba(200,240,76,.1);color:var(--accent);}
.ni svg{width:17px;height:17px;flex-shrink:0;}
.ni span{flex:1;}
.ni .badge{font-size:10px;background:var(--surface3);padding:1px 6px;border-radius:10px;}
.ni .badge.accent{background:var(--accent);color:#000;}

.sb-card{margin:10px;background:linear-gradient(135deg,#1a1030,#0d1a30);border:1px solid rgba(124,106,245,.3);border-radius:14px;padding:14px;flex-shrink:0;}
.sb-card h4{font-family:'Syne',sans-serif;font-size:12px;font-weight:700;color:var(--accent);margin-bottom:4px;}
.sb-card p{font-size:11px;color:var(--muted);line-height:1.5;margin-bottom:10px;}
.sb-btn{background:var(--accent);color:#000;border:none;border-radius:8px;padding:7px 12px;font-size:11px;font-weight:700;cursor:pointer;width:100%;font-family:'Syne',sans-serif;}

/* ── PAGES ── */
.page{display:none;min-height:100%;}
.page.active{display:block;}

/* Hero */
.hero{padding:40px 28px 32px;position:relative;overflow:hidden;}
.hero::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,#1a1a2e,#0f3460);z-index:0;}
.hero::after{content:'';position:absolute;top:-80px;right:-80px;width:320px;height:320px;background:radial-gradient(circle,rgba(200,240,76,.12),transparent 65%);border-radius:50%;pointer-events:none;}
.hero>*{position:relative;z-index:1;}
.hero-sub{font-size:12px;color:var(--muted);margin-bottom:6px;}
.hero-title{font-family:'Syne',sans-serif;font-size:30px;font-weight:800;line-height:1.1;margin-bottom:8px;}
.hero-title em{color:var(--accent);font-style:normal;}
.hero-desc{font-size:13px;color:var(--muted);margin-bottom:20px;}
.hero-pills{display:flex;flex-wrap:wrap;gap:7px;}
.pill{background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.1);padding:5px 12px;border-radius:20px;font-size:11px;display:flex;align-items:center;gap:5px;}
.pill .dot{width:5px;height:5px;border-radius:50%;background:var(--accent);}

/* Section */
.sec{padding:24px 24px 0;}
.sec-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;}
.sec-title{font-family:'Syne',sans-serif;font-size:16px;font-weight:700;}
.see-all{font-size:12px;color:var(--muted);cursor:pointer;transition:color .15s;}
.see-all:hover{color:var(--accent);}

/* Cards grid */
.cards{display:grid;gap:12px;}
.c5{grid-template-columns:repeat(5,1fr);}
.c4{grid-template-columns:repeat(4,1fr);}
.c3{grid-template-columns:repeat(3,1fr);}
.c2{grid-template-columns:1fr 1fr;}

.card{background:var(--surface2);border-radius:12px;overflow:hidden;cursor:pointer;transition:transform .2s,background .2s;position:relative;}
.card:hover{transform:translateY(-3px);background:var(--surface3);}
.card-art{aspect-ratio:1;position:relative;overflow:hidden;}
.card-art img{width:100%;height:100%;object-fit:cover;}
.card-art .fallback{width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-size:36px;}
.card-play{position:absolute;bottom:8px;right:8px;width:34px;height:34px;background:var(--accent);border-radius:50%;display:flex;align-items:center;justify-content:center;opacity:0;transform:translateY(6px);transition:all .2s;border:none;cursor:pointer;}
.card:hover .card-play{opacity:1;transform:translateY(0);}
.card-info{padding:10px;}
.card-title{font-size:12px;font-weight:600;margin-bottom:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.card-sub{font-size:11px;color:var(--muted);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}

/* Featured row */
.feat-row{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.feat-card{background:var(--surface2);border-radius:12px;padding:14px;display:flex;gap:12px;align-items:center;cursor:pointer;transition:all .2s;border:1px solid transparent;}
.feat-card:hover{border-color:var(--border);background:var(--surface3);}
.feat-art{width:52px;height:52px;border-radius:8px;flex-shrink:0;overflow:hidden;display:flex;align-items:center;justify-content:center;font-size:22px;}
.feat-art img{width:100%;height:100%;object-fit:cover;}
.feat-title{font-weight:600;font-size:13px;margin-bottom:3px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.feat-sub{font-size:11px;color:var(--muted);}

/* Track list */
.tracklist{padding:0 20px 110px;}
.tl-header{display:grid;grid-template-columns:40px 1fr 120px 60px 50px;gap:10px;padding:8px 12px;border-bottom:1px solid var(--border);margin-bottom:4px;}
.tl-header span{font-size:11px;color:var(--muted);font-weight:600;text-transform:uppercase;letter-spacing:.8px;}
.tl-header span:last-child{text-align:center;}
.track{display:grid;grid-template-columns:40px 1fr 120px 60px 50px;gap:10px;align-items:center;padding:8px 12px;border-radius:8px;cursor:pointer;transition:background .15s;group;}
.track:hover{background:var(--surface2);}
.track.playing{background:rgba(200,240,76,.06);}
.t-num{font-size:13px;color:var(--muted);text-align:center;}
.track.playing .t-num{display:none;}
.track.playing .t-eq{display:flex!important;}
.t-eq{display:none;align-items:flex-end;gap:2px;height:16px;justify-content:center;}
.t-eq span{width:3px;background:var(--accent);border-radius:1px;animation:eq .5s ease-in-out infinite alternate;}
.t-eq span:nth-child(1){height:5px;animation-delay:0s;}
.t-eq span:nth-child(2){height:13px;animation-delay:.15s;}
.t-eq span:nth-child(3){height:8px;animation-delay:.3s;}
.t-eq span:nth-child(4){height:13px;animation-delay:.1s;}
@keyframes eq{to{height:3px;}}
.t-paused .t-eq span{animation:none;height:4px;}
.t-info{display:flex;align-items:center;gap:10px;min-width:0;}
.t-thumb{width:38px;height:38px;border-radius:6px;flex-shrink:0;overflow:hidden;display:flex;align-items:center;justify-content:center;font-size:16px;background:var(--surface3);}
.t-thumb img{width:100%;height:100%;object-fit:cover;}
.t-name{font-size:13px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.t-artist{font-size:11px;color:var(--muted);}
.track.playing .t-name{color:var(--accent);}
.t-album{font-size:12px;color:var(--muted);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.t-dur{font-size:12px;color:var(--muted);text-align:center;}
.t-like{text-align:center;opacity:0;transition:opacity .15s;}
.track:hover .t-like{opacity:1;}
.t-like.on{opacity:1;color:var(--accent3)!important;}
.t-like svg{width:15px;height:15px;}

/* Search */
.search-wrap{padding:24px 24px 0;}
.search-box{display:flex;align-items:center;gap:10px;background:var(--surface2);border:1px solid var(--border);border-radius:11px;padding:11px 16px;margin-bottom:20px;transition:border-color .2s;}
.search-box:focus-within{border-color:var(--accent2);}
.search-box svg{width:16px;height:16px;color:var(--muted);flex-shrink:0;}
.search-box input{flex:1;background:none;border:none;outline:none;font-size:14px;color:var(--text);font-family:'DM Sans',sans-serif;}
.search-box input::placeholder{color:var(--muted);}
.genre-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;}
.genre{border-radius:12px;padding:18px 14px 14px;cursor:pointer;transition:transform .2s;position:relative;overflow:hidden;aspect-ratio:1.5;}
.genre:hover{transform:scale(1.03);}
.genre h3{font-family:'Syne',sans-serif;font-size:14px;font-weight:700;position:relative;z-index:1;}
.genre .gi{position:absolute;bottom:-6px;right:2px;font-size:44px;opacity:.5;transform:rotate(12deg);pointer-events:none;}
#search-results .track{padding:8px 12px;}

/* Library */
.lib-tabs{display:flex;gap:8px;padding:20px 24px 0;}
.tab{padding:7px 16px;border-radius:20px;cursor:pointer;font-size:12px;font-weight:600;background:var(--surface2);color:var(--muted);border:1px solid transparent;transition:all .15s;}
.tab.active{background:var(--accent);color:#000;border-color:var(--accent);}

/* Premium page */
.prem{padding:36px 28px 100px;}
.prem-hero{text-align:center;margin-bottom:40px;}
.prem-badge{display:inline-flex;align-items:center;gap:6px;background:rgba(200,240,76,.12);border:1px solid rgba(200,240,76,.3);color:var(--accent);font-size:12px;font-weight:700;padding:6px 14px;border-radius:20px;margin-bottom:14px;}
.prem h1{font-family:'Syne',sans-serif;font-size:36px;font-weight:800;margin-bottom:10px;}
.prem h1 span{color:var(--accent);}
.prem p{font-size:14px;color:var(--muted);max-width:440px;margin:0 auto;}
.feat-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;}
.fi{background:var(--surface2);border:1px solid var(--border);border-radius:14px;padding:20px;}
.fi-icon{font-size:26px;margin-bottom:10px;}
.fi h3{font-family:'Syne',sans-serif;font-size:13px;font-weight:700;margin-bottom:5px;}
.fi p{font-size:12px;color:var(--muted);line-height:1.6;}
.fi-ul{display:flex;align-items:center;gap:5px;margin-top:8px;font-size:11px;color:var(--accent);font-weight:600;}
.fi-ul svg{width:12px;height:12px;}

/* Privacy */
.priv{padding:36px 28px 100px;max-width:720px;}
.priv h1{font-family:'Syne',sans-serif;font-size:28px;font-weight:800;margin-bottom:6px;}
.priv .updated{font-size:11px;color:var(--muted);margin-bottom:28px;}
.priv-sec{margin-bottom:24px;}
.priv-sec h2{font-family:'Syne',sans-serif;font-size:14px;font-weight:700;color:var(--accent);margin-bottom:8px;}
.priv-sec p,.priv-sec li{font-size:13px;color:#a0a0c0;line-height:1.85;}
.priv-sec ul{padding-left:18px;}
.priv-sec li{margin-bottom:5px;}

/* ── PLAYER BAR ── */
#player{display:grid;grid-template-columns:280px 1fr 260px;align-items:center;padding:0 20px;height:var(--ph);gap:16px;}
.now{display:flex;align-items:center;gap:12px;min-width:0;}
.now-art{width:50px;height:50px;border-radius:8px;flex-shrink:0;overflow:hidden;display:flex;align-items:center;justify-content:center;font-size:22px;background:var(--surface3);}
.now-art img{width:100%;height:100%;object-fit:cover;}
.now-art.spinning{animation:spin 8s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.now-info{min-width:0;}
.now-title{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.now-artist{font-size:11px;color:var(--muted);}
.now-acts{display:flex;gap:10px;align-items:center;flex-shrink:0;}
.now-acts button{background:none;border:none;cursor:pointer;color:var(--muted);display:flex;align-items:center;padding:2px;transition:color .15s;}
.now-acts button:hover{color:var(--text);}
.now-acts button.on{color:var(--accent3);}
.now-acts button svg{width:15px;height:15px;}

.ctrl{display:flex;flex-direction:column;align-items:center;gap:6px;}
.ctrl-btns{display:flex;align-items:center;gap:12px;}
.cb{background:none;border:none;color:var(--muted);cursor:pointer;display:flex;align-items:center;padding:4px;transition:color .15s;border-radius:6px;}
.cb:hover{color:var(--text);}
.cb.on{color:var(--accent);}
.cb svg{width:18px;height:18px;}
.pp{width:38px;height:38px;border-radius:50%;background:var(--accent);border:none;color:#000;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:transform .1s;flex-shrink:0;}
.pp:hover{transform:scale(1.08);}
.pp:active{transform:scale(.95);}
.pp svg{width:16px;height:16px;}
.prog{width:100%;display:flex;align-items:center;gap:8px;}
.prog-t{font-size:10px;color:var(--muted);min-width:32px;font-variant-numeric:tabular-nums;}
.prog-t:last-child{text-align:right;}
.prog-bar{flex:1;height:4px;background:var(--surface3);border-radius:2px;cursor:pointer;position:relative;}
.prog-fill{height:100%;background:var(--accent);border-radius:2px;position:relative;transition:width .2s;}
.prog-fill::after{content:'';position:absolute;right:-5px;top:50%;transform:translateY(-50%);width:10px;height:10px;background:white;border-radius:50%;opacity:0;transition:opacity .15s;}
.prog-bar:hover .prog-fill::after{opacity:1;}
#prog-bar{position:relative;}
#prog-buf{position:absolute;top:0;left:0;height:100%;background:rgba(255,255,255,.12);border-radius:2px;pointer-events:none;}

.extras{display:flex;align-items:center;gap:10px;justify-content:flex-end;}
.extras button{background:none;border:none;color:var(--muted);cursor:pointer;display:flex;align-items:center;padding:3px;transition:color .15s;}
.extras button:hover{color:var(--text);}
.extras button.on{color:var(--accent);}
.extras button svg{width:16px;height:16px;}
.vol-wrap{display:flex;align-items:center;gap:6px;}
#vol-slider{-webkit-appearance:none;appearance:none;width:70px;height:3px;background:var(--surface3);border-radius:2px;outline:none;cursor:pointer;}
#vol-slider::-webkit-slider-thumb{-webkit-appearance:none;width:12px;height:12px;background:white;border-radius:50%;cursor:pointer;}

/* ── MODALS ── */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:1000;display:none;align-items:center;justify-content:center;backdrop-filter:blur(6px);}
.modal-bg.open{display:flex;}
.modal{background:var(--surface);border:1px solid var(--border);border-radius:18px;padding:28px;width:90%;max-width:480px;position:relative;max-height:85vh;overflow-y:auto;}
.modal h2{font-family:'Syne',sans-serif;font-size:19px;font-weight:800;margin-bottom:6px;}
.modal-close{position:absolute;top:14px;right:14px;background:var(--surface2);border:none;color:var(--muted);cursor:pointer;width:28px;height:28px;border-radius:50%;font-size:16px;display:flex;align-items:center;justify-content:center;transition:all .15s;}
.modal-close:hover{background:var(--surface3);color:var(--text);}

/* EQ */
.eq-bands{display:flex;gap:8px;align-items:flex-end;justify-content:center;padding:20px 0;height:160px;}
.eq-band{display:flex;flex-direction:column;align-items:center;gap:6px;flex:1;}
.eq-band input[type=range]{-webkit-appearance:none;appearance:none;writing-mode:vertical-lr;direction:rtl;width:24px;height:100px;background:transparent;cursor:pointer;outline:none;}
.eq-band input[type=range]::-webkit-slider-runnable-track{width:4px;background:var(--surface3);border-radius:2px;}
.eq-band input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:14px;height:14px;background:var(--accent);border-radius:50%;margin-left:-5px;}
.eq-band label{font-size:9px;color:var(--muted);text-align:center;}
.eq-band .eq-val{font-size:10px;color:var(--accent);font-weight:600;min-width:28px;text-align:center;}
.eq-presets{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px;}
.eq-preset{padding:5px 12px;border-radius:20px;border:1px solid var(--border);background:var(--surface2);cursor:pointer;font-size:11px;color:var(--muted);transition:all .15s;}
.eq-preset:hover,.eq-preset.active{background:var(--accent);color:#000;border-color:var(--accent);}

/* Lyrics modal */
#lyrics-text{font-size:14px;line-height:2;color:#c0c0e0;white-space:pre-line;max-height:400px;overflow-y:auto;padding:10px 0;}
#lyrics-text.loading{color:var(--muted);text-align:center;padding:40px 0;}

/* Now Playing fullscreen */
#np-fullscreen{position:fixed;inset:0;background:var(--bg);z-index:500;display:none;flex-direction:column;align-items:center;justify-content:center;padding:40px;}
#np-fullscreen.open{display:flex;}
#np-big-art{width:260px;height:260px;border-radius:20px;overflow:hidden;display:flex;align-items:center;justify-content:center;font-size:80px;background:var(--surface2);margin-bottom:28px;}
#np-big-art img{width:100%;height:100%;object-fit:cover;}
.np-info{text-align:center;margin-bottom:28px;}
.np-info h2{font-family:'Syne',sans-serif;font-size:22px;font-weight:800;margin-bottom:4px;}
.np-info p{color:var(--muted);font-size:14px;}
#np-canvas{width:260px;height:60px;border-radius:8px;background:var(--surface2);margin-bottom:16px;}

/* Playlist modal */
#pl-list{display:flex;flex-direction:column;gap:8px;max-height:300px;overflow-y:auto;margin:14px 0;}
.pl-item{display:flex;align-items:center;gap:10px;padding:10px 12px;border-radius:8px;background:var(--surface2);cursor:pointer;transition:background .15s;}
.pl-item:hover{background:var(--surface3);}
.pl-item span{flex:1;font-size:13px;}
.pl-item .pc{font-size:11px;color:var(--muted);}
.pl-new{display:flex;gap:8px;margin-top:8px;}
.pl-new input{flex:1;background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:9px 12px;font-size:13px;color:var(--text);outline:none;font-family:'DM Sans',sans-serif;}
.pl-new input:focus{border-color:var(--accent2);}
.pl-new button{background:var(--accent);color:#000;border:none;border-radius:8px;padding:9px 16px;font-size:12px;font-weight:700;cursor:pointer;font-family:'Syne',sans-serif;}

/* Toast */
#toast{position:fixed;bottom:100px;left:50%;transform:translateX(-50%) translateY(16px);background:var(--surface2);border:1px solid var(--border);padding:10px 22px;border-radius:25px;font-size:13px;opacity:0;transition:all .3s;z-index:2000;pointer-events:none;white-space:nowrap;box-shadow:0 8px 32px rgba(0,0,0,.5);}
#toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

/* Loading spinner */
.spinner{display:flex;align-items:center;justify-content:center;padding:40px;color:var(--muted);}
.spin-circle{width:28px;height:28px;border:3px solid var(--surface3);border-top-color:var(--accent);border-radius:50%;animation:rotate .7s linear infinite;}
@keyframes rotate{to{transform:rotate(360deg);}}

/* Welcome modal */
#welcome-modal .modal{text-align:center;}
.wm-icon{font-size:48px;margin-bottom:14px;}
.wm-btn{background:var(--accent);color:#000;border:none;border-radius:12px;padding:14px 32px;font-size:15px;font-weight:700;cursor:pointer;width:100%;font-family:'Syne',sans-serif;margin-top:4px;transition:transform .1s;}
.wm-btn:hover{transform:scale(1.02);}

/* Scrollbar */
::-webkit-scrollbar{width:4px;}
::-webkit-scrollbar-track{background:transparent;}
::-webkit-scrollbar-thumb{background:var(--surface3);border-radius:2px;}

/* Mobile responsive */
@media(max-width:768px){
  #app{grid-template-columns:1fr;grid-template-rows:1fr var(--ph) 56px;}
  #sidebar{display:none;}
  #player{grid-column:1;grid-template-columns:1fr;padding:0 14px;}
  .now{display:none;}
  .extras{display:none;}
  .ctrl{width:100%;}
  .cards.c5,.cards.c4{grid-template-columns:repeat(2,1fr);}
  .feat-grid{grid-template-columns:1fr;}
  .mobile-nav{display:flex!important;}
}
.mobile-nav{display:none;position:fixed;bottom:var(--ph);left:0;right:0;background:var(--surface);border-top:1px solid var(--border);z-index:100;justify-content:space-around;padding:8px 0;}
.mn-item{display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;padding:4px 12px;color:var(--muted);transition:color .15s;}
.mn-item.active{color:var(--accent);}
.mn-item svg{width:20px;height:20px;}
.mn-item span{font-size:9px;font-weight:600;}
</style>
</head>
<body>
<div id="app">

<!-- ══ SIDEBAR ══ -->
<aside id="sidebar">
  <div class="logo">
    <div class="logo-icon">
      <svg viewBox="0 0 24 24" fill="black"><path d="M12 3v10.55A4 4 0 1 0 14 17V7h4V3z"/></svg>
    </div>
    <div>
      <div class="logo-name">Loftify<span class="logo-badge">FREE</span></div>
    </div>
  </div>
  <nav class="nav">
    <div class="nl">Discover</div>
    <div class="ni active" onclick="nav('home')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/></svg><span>Home</span></div>
    <div class="ni" onclick="nav('search')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M15.5 14h-.79l-.28-.27A6.47 6.47 0 0016 9.5 6.5 6.5 0 109.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/></svg><span>Search</span></div>
    <div class="ni" onclick="nav('library')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M4 6H2v14c0 1.1.9 2 2 2h14v-2H4V6zm16-4H8c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm-7 14l-5-5 1.41-1.41L12 14.17l7.59-7.59L21 8l-9 9z"/></svg><span>Library</span><span class="badge" id="pl-count">0</span></div>
    <div class="ni" onclick="nav('liked')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg><span>Liked Songs</span><span class="badge accent" id="liked-count">0</span></div>
    <div class="ni" onclick="nav('history')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M13 3a9 9 0 0 0-9 9H1l3.89 3.89.07.14L9 12H6c0-3.87 3.13-7 7-7s7 3.13 7 7-3.13 7-7 7c-1.93 0-3.68-.79-4.94-2.06l-1.42 1.42A8.954 8.954 0 0013 21a9 9 0 0 0 0-18zm-1 5v5l4.28 2.54.72-1.21-3.5-2.08V8H12z"/></svg><span>History</span></div>
    <div class="nl">Your Playlists</div>
    <div id="sidebar-playlists"></div>
    <div class="ni" onclick="openNewPlaylistModal()"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/></svg><span>New Playlist</span></div>
    <div class="nl">More</div>
    <div class="ni" onclick="nav('premium')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg><span>All Features Free</span></div>
    <div class="ni" onclick="nav('privacy')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 1L3 5v6c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V5l-9-4z"/></svg><span>Privacy Policy</span></div>
  </nav>
  <div class="sb-card">
    <h4>🎉 All Premium Free!</h4>
    <p>No ads, HD audio, offline downloads, unlimited skips — everything.</p>
    <button class="sb-btn" onclick="nav('premium')">See All Features</button>
  </div>
</aside>

<!-- ══ MAIN CONTENT ══ -->
<main id="main">

  <!-- HOME -->
  <div class="page active" id="page-home">
    <div class="hero">
      <div class="hero-sub">Good evening 🎵</div>
      <div class="hero-title">Your music,<br><em>no limits.</em></div>
      <div class="hero-desc">Every premium feature. Completely free. No subscription needed.</div>
      <div class="hero-pills">
        <div class="pill"><span class="dot"></span>No Ads</div>
        <div class="pill"><span class="dot"></span>HD Audio</div>
        <div class="pill"><span class="dot"></span>Offline Play</div>
        <div class="pill"><span class="dot"></span>Free Downloads</div>
        <div class="pill"><span class="dot"></span>Unlimited Skips</div>
      </div>
    </div>

    <div class="sec">
      <div class="sec-hd"><div class="sec-title">Jump Back In</div></div>
      <div class="feat-row" id="home-featured"></div>
    </div>

    <div class="sec" style="margin-top:20px">
      <div class="sec-hd">
        <div class="sec-title">Trending Now 🔥</div>
        <div class="see-all" onclick="searchByTag('pop')">See all</div>
      </div>
      <div class="cards c5" id="home-trending"></div>
    </div>

    <div class="sec" style="margin-top:20px">
      <div class="sec-hd">
        <div class="sec-title">Top Tracks</div>
        <div class="see-all" onclick="searchByTag('electronic')">See all</div>
      </div>
    </div>
    <div class="tracklist" id="home-tracklist">
      <div class="tl-header"><span>#</span><span>Title</span><span>Album</span><span>Time</span><span>♥</span></div>
      <div id="home-tracks"></div>
    </div>
  </div>

  <!-- SEARCH -->
  <div class="page" id="page-search">
    <div class="search-wrap">
      <div style="font-family:'Syne',sans-serif;font-size:22px;font-weight:800;margin-bottom:18px;">Search Music</div>
      <div class="search-box">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M15.5 14h-.79l-.28-.27A6.47 6.47 0 0016 9.5 6.5 6.5 0 109.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/></svg>
        <input type="text" id="search-input" placeholder="Songs, artists, albums…" autocomplete="off">
      </div>
      <div id="search-results" style="display:none;padding-bottom:20px;"></div>
      <div id="genre-browse">
        <div class="sec-hd" style="margin-bottom:12px;"><div class="sec-title">Browse Genres</div></div>
        <div class="genre-grid">
          <div class="genre" style="background:linear-gradient(135deg,#667eea,#764ba2)" onclick="searchByTag('pop')"><h3>Pop</h3><span class="gi">🎤</span></div>
          <div class="genre" style="background:linear-gradient(135deg,#f093fb,#f5576c)" onclick="searchByTag('hiphop')"><h3>Hip-Hop</h3><span class="gi">🎧</span></div>
          <div class="genre" style="background:linear-gradient(135deg,#4facfe,#00f2fe)" onclick="searchByTag('electronic')"><h3>Electronic</h3><span class="gi">🎛️</span></div>
          <div class="genre" style="background:linear-gradient(135deg,#43e97b,#38f9d7)" onclick="searchByTag('rnb')"><h3>R&amp;B</h3><span class="gi">🎵</span></div>
          <div class="genre" style="background:linear-gradient(135deg,#fa709a,#fee140)" onclick="searchByTag('rock')"><h3>Rock</h3><span class="gi">🎸</span></div>
          <div class="genre" style="background:linear-gradient(135deg,#a18cd1,#fbc2eb)" onclick="searchByTag('lofi')"><h3>Lo-fi</h3><span class="gi">☕</span></div>
          <div class="genre" style="background:linear-gradient(135deg,#fda085,#f6d365)" onclick="searchByTag('jazz')"><h3>Jazz</h3><span class="gi">🎷</span></div>
          <div class="genre" style="background:linear-gradient(135deg,#30cfd0,#330867)" onclick="searchByTag('classical')"><h3>Classical</h3><span class="gi">🎻</span></div>
        </div>
      </div>
    </div>
  </div>

  <!-- LIBRARY -->
  <div class="page" id="page-library">
    <div class="sec">
      <div class="sec-hd" style="margin-top:8px;"><div class="sec-title">Your Library</div><div class="see-all" onclick="openNewPlaylistModal()">+ New Playlist</div></div>
      <div class="lib-tabs" style="padding:0;margin-bottom:16px;">
        <div class="tab active" onclick="switchLibTab('playlists',this)">Playlists</div>
        <div class="tab" onclick="switchLibTab('liked',this)">Liked</div>
        <div class="tab" onclick="switchLibTab('history',this)">History</div>
      </div>
      <div id="lib-content"></div>
    </div>
  </div>

  <!-- LIKED -->
  <div class="page" id="page-liked">
    <div class="hero" style="background:linear-gradient(135deg,#1a0533,#3d1266);">
      <div style="font-size:44px;margin-bottom:10px">❤️</div>
      <div class="hero-title">Liked Songs</div>
      <div class="hero-desc" id="liked-sub">0 songs</div>
      <div style="display:flex;gap:10px;margin-top:16px;">
        <button onclick="playLiked()" style="background:var(--accent);color:#000;border:none;padding:11px 24px;border-radius:25px;font-weight:700;font-size:13px;cursor:pointer;font-family:'Syne',sans-serif">▶ Play All</button>
        <button onclick="shuffleLiked()" style="background:var(--surface2);color:var(--text);border:1px solid var(--border);padding:11px 24px;border-radius:25px;font-weight:600;font-size:13px;cursor:pointer;">Shuffle</button>
      </div>
    </div>
    <div class="tracklist" id="liked-tracklist" style="padding-top:16px;">
      <div class="tl-header"><span>#</span><span>Title</span><span>Album</span><span>Time</span><span>♥</span></div>
      <div id="liked-tracks"></div>
    </div>
  </div>

  <!-- HISTORY -->
  <div class="page" id="page-history">
    <div class="sec">
      <div class="sec-hd" style="margin-top:8px;"><div class="sec-title">Recently Played</div><div class="see-all" onclick="clearHistory()">Clear</div></div>
      <div id="history-content" class="tracklist" style="padding:0 0 100px;">
        <div class="tl-header"><span>#</span><span>Title</span><span>Album</span><span>Time</span><span>♥</span></div>
        <div id="history-tracks"></div>
      </div>
    </div>
  </div>

  <!-- PREMIUM -->
  <div class="page" id="page-premium">
    <div class="prem">
      <div class="prem-hero">
        <div class="prem-badge"><svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>100% FREE — NO CREDIT CARD EVER</div>
        <h1>Everything <span>Unlocked</span>.<br>Nothing Hidden.</h1>
        <p>Loftify gives you every premium music feature completely free. No tricks, no trials, no hidden upgrades.</p>
      </div>
      <div class="feat-grid">
        <div class="fi"><div class="fi-icon">🚫</div><h3>Zero Ads</h3><p>Listen without interruption. No audio ads, banner ads, or video ads. Ever.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">⬇️</div><h3>Free Downloads</h3><p>Download unlimited songs and playlists. Listen anywhere without internet.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">🎵</div><h3>HD Audio</h3><p>High-quality 320kbps MP3 and lossless audio. Hear every detail the artist intended.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">⏭️</div><h3>Unlimited Skips</h3><p>Skip songs freely — no limits. Total control over your listening experience.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">🎛️</div><h3>10-Band Equalizer</h3><p>Full EQ with presets: Bass Boost, Vocal, Electronic, Classical, and more.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">📖</div><h3>Lyrics View</h3><p>Real lyrics for millions of songs powered by free lyric database.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">📋</div><h3>Unlimited Playlists</h3><p>Create, manage and share as many playlists as you want. No limits.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">📊</div><h3>Audio Visualizer</h3><p>Real-time frequency visualizer powered by Web Audio API.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
        <div class="fi"><div class="fi-icon">📱</div><h3>Install as App (PWA)</h3><p>Install Loftify on your phone or desktop — works like a native app, offline too.</p><div class="fi-ul"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>Active</div></div>
      </div>
    </div>
  </div>

  <!-- PRIVACY POLICY -->
  <div class="page" id="page-privacy">
    <div class="priv">
      <h1>Privacy Policy</h1>
      <div class="updated">Loftify App — Last updated: March 2026</div>
      <div class="priv-sec"><h2>1. Introduction</h2><p>Welcome to Loftify. We are committed to protecting your personal information and your right to privacy. This Privacy Policy explains how we collect, use, and safeguard your information when you use our service. Loftify is a free music streaming service powered by Creative Commons licensed music via the Jamendo API.</p></div>
      <div class="priv-sec"><h2>2. Information We Collect</h2><ul><li>General device info: browser type, IP address, platform, device model, OS version</li><li>Information you provide: email (if creating account), preferences</li><li>Usage data: session times, tracks played, search queries</li><li>Local storage: playlists, liked songs, equalizer settings (stored only on your device)</li></ul><p style="margin-top:10px">We do not and will not request your credit card, debit card PIN, or financial passwords.</p></div>
      <div class="priv-sec"><h2>3. How We Use Your Information</h2><ul><li>To personalize music recommendations</li><li>To sync your listening history and playlists</li><li>To improve our service and fix bugs</li><li>To comply with legal obligations</li></ul></div>
      <div class="priv-sec"><h2>4. Information Sharing</h2><p>We share data only with service providers necessary to operate Loftify. Music is served via the Jamendo API (jamendo.com) under Creative Commons licenses. Lyrics are fetched from the lyrics.ovh free API. We do not sell your personal data.</p><ul style="margin-top:10px"><li><strong>4.3 Law &amp; Harm:</strong> We may disclose data to comply with law or protect safety.</li><li><strong>4.4 Business Transfers:</strong> In a merger, data transfers under same policy terms.</li><li><strong>4.5 International Transfers:</strong> Cross-border data storage is bound by confidentiality.</li></ul></div>
      <div class="priv-sec"><h2>5. Age of Consent</h2><p>Loftify is primarily for users aged 16 and above. Users may allow minor dependents under 13 to access the service with parental consent.</p></div>
      <div class="priv-sec"><h2>6. Children Policy</h2><p>Loftify does not knowingly collect personal data from children under 13. If you believe your child has provided us data, contact us at <strong style="color:var(--accent)">support@loftify.app</strong> and we will remove it promptly.</p></div>
      <div class="priv-sec"><h2>7. Your Data Rights</h2><ul><li>Delete your account and all associated data</li><li>Export your playlists and liked songs</li><li>Withdraw consent at any time by stopping use</li><li>Request restriction of data processing</li></ul></div>
      <div class="priv-sec"><h2>8. Third-Party Services</h2><p>Loftify uses the following free third-party services: <strong>Jamendo API</strong> for Creative Commons music, <strong>lyrics.ovh</strong> for song lyrics, <strong>Google Fonts</strong> for typography. Each service has their own privacy policy which we encourage you to read.</p></div>
      <div class="priv-sec"><h2>9. Data Security</h2><p>We implement reasonable technical safeguards. Your playlists and preferences are stored locally on your device using browser localStorage — they are never uploaded to our servers without your consent. Internet transmissions are inherently not 100% secure.</p></div>
      <div class="priv-sec"><h2>10. Support</h2><p>For privacy concerns or data removal requests: <strong style="color:var(--accent)">support@loftify.app</strong></p></div>
      <div class="priv-sec"><h2>11. Changes to Policy</h2><p>We may update this policy from time to time. Material changes will be communicated via in-app notification. Continued use after changes constitutes acceptance of the updated policy.</p></div>
    </div>
  </div>

</main>

<!-- ══ PLAYER BAR ══ -->
<div id="player">
  <div class="now">
    <div class="now-art" id="now-art">🎵</div>
    <div class="now-info">
      <div class="now-title" id="now-title">Select a track to play</div>
      <div class="now-artist" id="now-artist">Loftify Music</div>
    </div>
    <div class="now-acts">
      <button id="like-btn" onclick="toggleLikeCurrent()" title="Like">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>
      </button>
      <button onclick="openPlaylistModal()" title="Add to playlist">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/></svg>
      </button>
    </div>
  </div>

  <div class="ctrl">
    <div class="ctrl-btns">
      <button class="cb" id="shuffle-btn" onclick="toggleShuffle()" title="Shuffle">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M10.59 9.17L5.41 4 4 5.41l5.17 5.17 1.42-1.41zM14.5 4l2.04 2.04L4 18.59 5.41 20 17.96 7.46 20 9.5V4h-5.5zm.33 9.41l-1.41 1.41 3.13 3.13L14.5 20H20v-5.5l-2.04 2.04-3.13-3.13z"/></svg>
      </button>
      <button class="cb" onclick="prevTrack()" title="Previous">
        <svg viewBox="0 0 24 24" fill="currentColor" width="22" height="22"><path d="M6 6h2v12H6zm3.5 6 8.5 6V6z"/></svg>
      </button>
      <button class="pp" id="pp-btn" onclick="togglePlay()">
        <svg id="pp-icon" viewBox="0 0 24 24" fill="currentColor"><path d="M8 5v14l11-7z"/></svg>
      </button>
      <button class="cb" onclick="nextTrack()" title="Next">
        <svg viewBox="0 0 24 24" fill="currentColor" width="22" height="22"><path d="M6 18l8.5-6L6 6v12zM16 6v12h2V6h-2z"/></svg>
      </button>
      <button class="cb" id="repeat-btn" onclick="toggleRepeat()" title="Repeat">
        <svg id="repeat-icon" viewBox="0 0 24 24" fill="currentColor"><path d="M7 7h10v3l4-4-4-4v3H5v6h2V7zm10 10H7v-3l-4 4 4 4v-3h12v-6h-2v4z"/></svg>
      </button>
    </div>
    <div class="prog">
      <span class="prog-t" id="cur-t">0:00</span>
      <div class="prog-bar" id="prog-bar" onclick="seekTo(event)">
        <div id="prog-buf"></div>
        <div class="prog-fill" id="prog-fill" style="width:0%"></div>
      </div>
      <span class="prog-t" id="dur-t">0:00</span>
    </div>
  </div>

  <div class="extras">
    <button onclick="openLyrics()" title="Lyrics"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 3v10.55A4 4 0 1 0 14 17V7h4V3z"/></svg></button>
    <button onclick="downloadCurrent()" title="Download"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M19 9h-4V3H9v6H5l7 7 7-7zM5 18v2h14v-2H5z"/></svg></button>
    <button onclick="openEQ()" title="Equalizer"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M10 20h4V4h-4v16zm-6 0h4v-8H4v8zM16 9v11h4V9h-4z"/></svg></button>
    <button onclick="openFullscreen()" title="Full Player"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M7 14H5v5h5v-2H7v-3zm-2-4h2V7h3V5H5v5zm12 7h-3v2h5v-5h-2v3zM14 5v2h3v3h2V5h-5z"/></svg></button>
    <div class="vol-wrap">
      <button onclick="toggleMute()" id="mute-btn" title="Volume">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M3 9v6h4l5 5V4L7 9H3zm13.5 3c0-1.77-1.02-3.29-2.5-4.03v8.05c1.48-.73 2.5-2.25 2.5-4.02z"/></svg>
      </button>
      <input type="range" id="vol-slider" min="0" max="100" value="80" oninput="setVolume(this.value)">
    </div>
  </div>
</div>
</div>

<!-- ══ MOBILE NAV ══ -->
<div class="mobile-nav">
  <div class="mn-item active" onclick="nav('home')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/></svg><span>Home</span></div>
  <div class="mn-item" onclick="nav('search')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M15.5 14h-.79l-.28-.27A6.47 6.47 0 0016 9.5 6.5 6.5 0 109.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/></svg><span>Search</span></div>
  <div class="mn-item" onclick="nav('library')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M4 6H2v14c0 1.1.9 2 2 2h14v-2H4V6zm16-4H8c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm-7 14l-5-5 1.41-1.41L12 14.17l7.59-7.59L21 8l-9 9z"/></svg><span>Library</span></div>
  <div class="mn-item" onclick="nav('liked')"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg><span>Liked</span></div>
</div>

<!-- ══ MODALS ══ -->

<!-- EQ Modal -->
<div class="modal-bg" id="eq-modal">
  <div class="modal" style="max-width:520px">
    <button class="modal-close" onclick="closeModal('eq-modal')">✕</button>
    <h2>🎛️ Equalizer</h2>
    <p style="font-size:12px;color:var(--muted);margin-top:4px;">Drag sliders to adjust frequency. Saved automatically.</p>
    <div class="eq-bands" id="eq-bands"></div>
    <div class="eq-presets" id="eq-presets"></div>
  </div>
</div>

<!-- Lyrics Modal -->
<div class="modal-bg" id="lyrics-modal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('lyrics-modal')">✕</button>
    <h2>📖 Lyrics</h2>
    <p style="font-size:12px;color:var(--muted);margin-top:2px;" id="lyrics-track-info">—</p>
    <div id="lyrics-text" class="loading">Loading lyrics…</div>
  </div>
</div>

<!-- Playlist Modal -->
<div class="modal-bg" id="playlist-modal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('playlist-modal')">✕</button>
    <h2>📋 Add to Playlist</h2>
    <div id="pl-list"></div>
    <div class="pl-new">
      <input type="text" id="new-pl-name" placeholder="New playlist name…" onkeydown="if(event.key==='Enter')createPlaylist()">
      <button onclick="createPlaylist()">Create</button>
    </div>
  </div>
</div>

<!-- New Playlist Modal -->
<div class="modal-bg" id="newpl-modal">
  <div class="modal" style="max-width:380px">
    <button class="modal-close" onclick="closeModal('newpl-modal')">✕</button>
    <h2>➕ New Playlist</h2>
    <div class="pl-new" style="margin-top:16px">
      <input type="text" id="newpl-name" placeholder="Playlist name…" onkeydown="if(event.key==='Enter')createNewPlaylist()">
      <button onclick="createNewPlaylist()">Create</button>
    </div>
  </div>
</div>

<!-- Fullscreen Now Playing -->
<div id="np-fullscreen">
  <button onclick="closeFullscreen()" style="position:absolute;top:20px;right:20px;background:var(--surface2);border:none;color:var(--muted);cursor:pointer;width:36px;height:36px;border-radius:50%;font-size:18px;">✕</button>
  <div id="np-big-art">🎵</div>
  <div class="np-info">
    <h2 id="np-big-title">—</h2>
    <p id="np-big-artist">—</p>
  </div>
  <canvas id="np-canvas"></canvas>
  <div class="prog" style="width:300px;margin-bottom:20px;">
    <span class="prog-t" id="np-cur-t">0:00</span>
    <div class="prog-bar" style="flex:1" onclick="seekTo(event)">
      <div id="np-prog-buf" style="position:absolute;top:0;left:0;height:100%;background:rgba(255,255,255,.12);border-radius:2px;pointer-events:none;"></div>
      <div class="prog-fill" id="np-prog-fill" style="width:0%"></div>
    </div>
    <span class="prog-t" id="np-dur-t">0:00</span>
  </div>
  <div class="ctrl-btns">
    <button class="cb" id="np-shuffle" onclick="toggleShuffle()"><svg viewBox="0 0 24 24" fill="currentColor" width="20" height="20"><path d="M10.59 9.17L5.41 4 4 5.41l5.17 5.17 1.42-1.41zM14.5 4l2.04 2.04L4 18.59 5.41 20 17.96 7.46 20 9.5V4h-5.5zm.33 9.41l-1.41 1.41 3.13 3.13L14.5 20H20v-5.5l-2.04 2.04-3.13-3.13z"/></svg></button>
    <button class="cb" onclick="prevTrack()"><svg viewBox="0 0 24 24" fill="currentColor" width="26" height="26"><path d="M6 6h2v12H6zm3.5 6 8.5 6V6z"/></svg></button>
    <button class="pp" onclick="togglePlay()" style="width:50px;height:50px"><svg id="np-pp-icon" viewBox="0 0 24 24" fill="currentColor"><path d="M8 5v14l11-7z"/></svg></button>
    <button class="cb" onclick="nextTrack()"><svg viewBox="0 0 24 24" fill="currentColor" width="26" height="26"><path d="M6 18l8.5-6L6 6v12zM16 6v12h2V6h-2z"/></svg></button>
    <button class="cb" onclick="toggleRepeat()"><svg viewBox="0 0 24 24" fill="currentColor" width="20" height="20"><path d="M7 7h10v3l4-4-4-4v3H5v6h2V7zm10 10H7v-3l-4 4 4 4v-3h12v-6h-2v4z"/></svg></button>
  </div>
</div>

<!-- Welcome Modal -->
<div class="modal-bg open" id="welcome-modal">
  <div class="modal" style="text-align:center;max-width:400px">
    <div class="wm-icon">🎶</div>
    <h2>Welcome to Loftify!</h2>
    <p style="font-size:13px;color:var(--muted);margin:8px 0 18px;line-height:1.7">All premium features are <strong style="color:var(--accent)">completely free</strong>. Real music from Jamendo's Creative Commons library — no ads, no limits, no subscription.</p>
    <div style="background:var(--surface2);border-radius:10px;padding:12px;margin-bottom:18px;font-size:12px;color:var(--muted);text-align:left">
      <strong style="color:var(--text)">🎵 Powered by Jamendo API</strong><br>
      Loftify streams Creative Commons licensed music. Free for everyone, forever.
    </div>
    <button class="wm-btn" onclick="closeModal('welcome-modal')">Start Listening Free →</button>
  </div>
</div>

<!-- Toast -->
<div id="toast"></div>

<!-- Hidden audio element -->
<audio id="audio" preload="auto" crossorigin="anonymous"></audio>

<script>
// ══════════════════════════════════════════
//  CONFIGURATION
// ══════════════════════════════════════════
const CFG = {
  JAMENDO_ID: 'b6747d04',       // Free Jamendo API client ID (from developer.jamendo.com)
  JAMENDO: 'https://api.jamendo.com/v3.0',
  LYRICS: 'https://api.lyrics.ovh/v1',
};

// Sample fallback tracks using SoundHelix (free, always available for demos)
const SAMPLE_TRACKS = [
  {id:'sh1',name:'Electric Dreams',artist_name:'Sonic Wave',album_name:'Neon Nights',duration:372,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3',image:null,_color:'#667eea'},
  {id:'sh2',name:'Midnight Journey',artist_name:'The Travelers',album_name:'Horizons',duration:336,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3',image:null,_color:'#f093fb'},
  {id:'sh3',name:'City Lights',artist_name:'Urban Groove',album_name:'Metropolis',duration:289,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3',image:null,_color:'#4facfe'},
  {id:'sh4',name:'Ocean Wave',artist_name:'Blue Horizon',album_name:'Deep Blue',duration:344,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3',image:null,_color:'#43e97b'},
  {id:'sh5',name:'Fire Dance',artist_name:'Rhythm Kings',album_name:'Heat',duration:258,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-5.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-5.mp3',image:null,_color:'#fa709a'},
  {id:'sh6',name:'Star Gazer',artist_name:'Cosmos Band',album_name:'Infinity',duration:310,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-6.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-6.mp3',image:null,_color:'#a18cd1'},
  {id:'sh7',name:'Forest Walk',artist_name:'Nature Sound',album_name:'Wilderness',duration:395,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-7.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-7.mp3',image:null,_color:'#fda085'},
  {id:'sh8',name:'Thunder Road',artist_name:'Storm Drive',album_name:'Velocity',duration:267,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3',image:null,_color:'#30cfd0'},
  {id:'sh9',name:'Dream Catcher',artist_name:'Night Owl',album_name:'Reverie',duration:420,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-9.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-9.mp3',image:null,_color:'#764ba2'},
  {id:'sh10',name:'Golden Hour',artist_name:'Daybreak',album_name:'Sunrise',duration:302,audio:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-10.mp3',audiodownload:'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-10.mp3',image:null,_color:'#f6d365'},
];

// ══════════════════════════════════════════
//  STATE
// ══════════════════════════════════════════
const S = {
  queue: [],
  qIdx: -1,
  playing: false,
  shuffle: false,
  repeat: 'none',  // none | one | all
  page: 'home',
  currentTrack: null,
  liked: new Set(JSON.parse(localStorage.getItem('lf_liked') || '[]')),
  playlists: JSON.parse(localStorage.getItem('lf_playlists') || '[]'),
  history: JSON.parse(localStorage.getItem('lf_history') || '[]'),
  volume: parseInt(localStorage.getItem('lf_vol') || '80'),
  muted: false,
  eqGains: JSON.parse(localStorage.getItem('lf_eq') || '[0,0,0,0,0,0,0,0,0,0]'),
  audioReady: false,
  searchTimer: null,
  pendingPlaylist: null, // track to add to playlist
};

// DOM shortcuts
const $ = id => document.getElementById(id);
const $a = sel => document.querySelectorAll(sel);

// ══════════════════════════════════════════
//  WEB AUDIO API
// ══════════════════════════════════════════
const audioEl = $('audio');
let audioCtx = null, srcNode = null, gainNode = null, analyserNode = null;
let eqFilters = [];
const EQ_BANDS = [32, 64, 125, 250, 500, 1000, 2000, 4000, 8000, 16000];
const EQ_PRESETS = {
  'Flat':     [0,0,0,0,0,0,0,0,0,0],
  'Bass':     [8,6,4,2,0,0,0,0,0,0],
  'Treble':   [0,0,0,0,0,2,4,6,6,7],
  'Vocal':    [-2,0,2,4,6,4,2,0,-1,-2],
  'Electronic':[6,5,0,-2,0,4,5,5,4,5],
  'Classical':[-3,0,2,3,2,0,-3,-3,-3,-3],
  'Rock':     [5,4,3,0,-1,0,3,4,5,5],
  'Jazz':     [3,2,0,2,3,3,0,1,2,3],
};
let animFrame = null;

function initAudio() {
  if (S.audioReady) { audioCtx && audioCtx.state === 'suspended' && audioCtx.resume(); return; }
  try {
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    srcNode = audioCtx.createMediaElementSource(audioEl);
    gainNode = audioCtx.createGain();
    analyserNode = audioCtx.createAnalyser();
    analyserNode.fftSize = 256;
    gainNode.gain.value = S.volume / 100;

    eqFilters = EQ_BANDS.map((freq, i) => {
      const f = audioCtx.createBiquadFilter();
      f.type = i === 0 ? 'lowshelf' : i === EQ_BANDS.length - 1 ? 'highshelf' : 'peaking';
      f.frequency.value = freq;
      f.gain.value = S.eqGains[i];
      f.Q.value = 1;
      return f;
    });

    let prev = srcNode;
    eqFilters.forEach(f => { prev.connect(f); prev = f; });
    prev.connect(gainNode);
    gainNode.connect(analyserNode);
    analyserNode.connect(audioCtx.destination);
    S.audioReady = true;
  } catch(e) {
    console.warn('AudioContext init failed:', e);
    audioEl.volume = S.volume / 100;
  }
}

function setEqBand(i, val) {
  S.eqGains[i] = val;
  if (eqFilters[i]) eqFilters[i].gain.value = val;
  localStorage.setItem('lf_eq', JSON.stringify(S.eqGains));
}

function applyEqPreset(name) {
  const gains = EQ_PRESETS[name];
  if (!gains) return;
  gains.forEach((v, i) => setEqBand(i, v));
  renderEQModal();
  $a('#eq-presets .eq-preset').forEach(b => b.classList.toggle('active', b.dataset.preset === name));
}

// ══════════════════════════════════════════
//  JAMENDO API
// ══════════════════════════════════════════
async function jamendo(endpoint, params = {}) {
  const q = new URLSearchParams({
    client_id: CFG.JAMENDO_ID, format: 'json',
    audioformat: 'mp32', ...params
  });
  try {
    const r = await fetch(`${CFG.JAMENDO}${endpoint}?${q}`);
    const d = await r.json();
    return d.results || [];
  } catch(e) {
    console.warn('Jamendo API error:', e);
    return [];
  }
}

async function loadHomeTrending() {
  const el = $('home-trending');
  el.innerHTML = '<div class="spinner"><div class="spin-circle"></div></div>';
  let tracks = await jamendo('/tracks/', {limit: 10, order: 'popularity_total', boost: 'popularity_month'});
  if (!tracks.length) tracks = SAMPLE_TRACKS.slice(0, 5);
  el.innerHTML = tracks.slice(0, 5).map(t => cardHTML(t)).join('');
}

async function loadHomeTopTracks() {
  const el = $('home-tracks');
  el.innerHTML = '<div class="spinner"><div class="spin-circle"></div></div>';
  let tracks = await jamendo('/tracks/', {limit: 12, order: 'popularity_total', tags: 'pop|electronic|rock'});
  if (!tracks.length) tracks = SAMPLE_TRACKS;
  const queue = tracks;
  el.innerHTML = tracks.map((t, i) => trackRowHTML(t, i, queue)).join('');
}

async function loadHomeFeatured() {
  const el = $('home-featured');
  el.innerHTML = '<div class="spinner"><div class="spin-circle"></div></div>';
  let tracks = await jamendo('/tracks/', {limit: 8, order: 'popularity_total', boost: 'popularity_week'});
  if (!tracks.length) tracks = SAMPLE_TRACKS;
  const items = [
    {t: tracks[0] || SAMPLE_TRACKS[0], label: 'Trending Today'},
    {t: tracks[2] || SAMPLE_TRACKS[2], label: 'Staff Pick'},
    {t: tracks[4] || SAMPLE_TRACKS[4], label: 'New Release'},
    {t: tracks[6] || SAMPLE_TRACKS[6], label: 'Top Chart'},
  ];
  el.innerHTML = items.map(({t, label}) => `
    <div class="feat-card" onclick="playTrack(${JSON.stringify(t).replace(/"/g,'&quot;')})">
      <div class="feat-art" style="background:${t._color || '#2a2a3f'}">
        ${t.image ? `<img src="${t.image}" alt="">` : artEmoji(t)}
      </div>
      <div>
        <div class="feat-title">${esc(t.name)}</div>
        <div class="feat-sub">${label} · ${esc(t.artist_name)}</div>
      </div>
    </div>`).join('');
}

async function searchTracks(query) {
  if (!query.trim()) {
    $('search-results').style.display = 'none';
    $('genre-browse').style.display = 'block';
    return;
  }
  $('search-results').style.display = 'block';
  $('genre-browse').style.display = 'none';
  $('search-results').innerHTML = '<div class="spinner"><div class="spin-circle"></div></div>';
  let tracks = await jamendo('/tracks/', {limit: 20, search: query});
  if (!tracks.length) {
    $('search-results').innerHTML = `<div style="color:var(--muted);padding:30px 0;text-align:center">No results for "<strong style="color:var(--text)">${esc(query)}</strong>"<br><small>Try a different search term</small></div>`;
    return;
  }
  $('search-results').innerHTML = `
    <div style="font-weight:600;margin-bottom:10px;font-size:14px">Results for "<em style="color:var(--accent)">${esc(query)}</em>"</div>
    <div class="tl-header"><span>#</span><span>Title</span><span>Album</span><span>Time</span><span>♥</span></div>
    ${tracks.map((t, i) => trackRowHTML(t, i, tracks)).join('')}`;
}

async function searchByTag(tag) {
  nav('search');
  $('search-input').value = tag;
  $('search-results').style.display = 'block';
  $('genre-browse').style.display = 'none';
  $('search-results').innerHTML = '<div class="spinner"><div class="spin-circle"></div></div>';
  let tracks = await jamendo('/tracks/', {limit: 20, tags: tag, order: 'popularity_total'});
  if (!tracks.length) tracks = SAMPLE_TRACKS;
  $('search-results').innerHTML = `
    <div style="font-weight:600;margin-bottom:10px;font-size:14px">Genre: <em style="color:var(--accent)">${tag}</em></div>
    <div class="tl-header"><span>#</span><span>Title</span><span>Album</span><span>Time</span><span>♥</span></div>
    ${tracks.map((t, i) => trackRowHTML(t, i, tracks)).join('')}`;
}

// ══════════════════════════════════════════
//  PLAYER
// ══════════════════════════════════════════
function playTrack(track, queue = null) {
  initAudio();
  S.currentTrack = track;
  S.playing = true;
  if (queue) { S.queue = queue; S.qIdx = queue.findIndex(t => t.id === track.id || t.audio === track.audio); }
  else if (!S.queue.find(t => t.audio === track.audio)) { S.queue.push(track); S.qIdx = S.queue.length - 1; }
  else { S.qIdx = S.queue.findIndex(t => t.audio === track.audio); }

  audioEl.src = track.audio;
  audioEl.load();
  audioEl.play().catch(e => { console.warn('Play error:', e); toast('⚠️ Could not play track'); });

  // Add to history
  S.history = [track, ...S.history.filter(t => t.audio !== track.audio)].slice(0, 50);
  localStorage.setItem('lf_history', JSON.stringify(S.history));

  updatePlayerUI();
  saveRecentTracks();
}

function playQueue(tracks, startIdx = 0) {
  S.queue = [...tracks];
  playTrack(tracks[startIdx], tracks);
}

function togglePlay() {
  if (!S.currentTrack) { toast('🎵 Pick a track first!'); return; }
  initAudio();
  if (S.playing) {
    audioEl.pause();
    S.playing = false;
  } else {
    audioEl.play().catch(()=>{});
    S.playing = true;
  }
  updatePlayBtn();
  updateEqAnimClass();
}

function nextTrack() {
  if (!S.queue.length) return;
  if (S.shuffle) {
    S.qIdx = Math.floor(Math.random() * S.queue.length);
  } else {
    S.qIdx = (S.qIdx + 1) % S.queue.length;
  }
  playTrack(S.queue[S.qIdx], null);
}

function prevTrack() {
  if (audioEl.currentTime > 3) { audioEl.currentTime = 0; return; }
  if (!S.queue.length) return;
  S.qIdx = (S.qIdx - 1 + S.queue.length) % S.queue.length;
  playTrack(S.queue[S.qIdx], null);
}

function toggleShuffle() {
  S.shuffle = !S.shuffle;
  $('shuffle-btn').classList.toggle('on', S.shuffle);
  const nb = $('np-shuffle'); if (nb) nb.classList.toggle('on', S.shuffle);
  toast(S.shuffle ? '🔀 Shuffle ON' : '🔀 Shuffle OFF');
}

function toggleRepeat() {
  const modes = ['none', 'all', 'one'];
  S.repeat = modes[(modes.indexOf(S.repeat) + 1) % modes.length];
  const icons = {
    none: '<path d="M7 7h10v3l4-4-4-4v3H5v6h2V7zm10 10H7v-3l-4 4 4 4v-3h12v-6h-2v4z"/>',
    all:  '<path d="M7 7h10v3l4-4-4-4v3H5v6h2V7zm10 10H7v-3l-4 4 4 4v-3h12v-6h-2v4z"/>',
    one:  '<path d="M7 7h10v3l4-4-4-4v3H5v6h2V7zm10 10H7v-3l-4 4 4 4v-3h12v-6h-2v4z"/><text x="12" y="13" text-anchor="middle" font-size="7" fill="currentColor" font-weight="bold">1</text>',
  };
  $('repeat-icon').innerHTML = icons[S.repeat];
  $('repeat-btn').classList.toggle('on', S.repeat !== 'none');
  toast({none:'↩️ Repeat OFF', all:'🔁 Repeat ALL', one:'🔂 Repeat ONE'}[S.repeat]);
}

function seekTo(e) {
  const bar = e.currentTarget;
  const rect = bar.getBoundingClientRect();
  const pct = Math.max(0, Math.min(1, (e.clientX - rect.left) / rect.width));
  if (audioEl.duration) { audioEl.currentTime = audioEl.duration * pct; }
}

function setVolume(v) {
  S.volume = parseInt(v);
  S.muted = false;
  if (gainNode) gainNode.gain.value = S.volume / 100;
  else audioEl.volume = S.volume / 100;
  localStorage.setItem('lf_vol', v);
  $('mute-btn').style.opacity = S.volume === 0 ? '.4' : '1';
}

function toggleMute() {
  S.muted = !S.muted;
  if (gainNode) gainNode.gain.value = S.muted ? 0 : S.volume / 100;
  else audioEl.volume = S.muted ? 0 : S.volume / 100;
  $('mute-btn').style.opacity = S.muted ? '.4' : '1';
  toast(S.muted ? '🔇 Muted' : '🔊 Unmuted');
}

// Audio events
audioEl.addEventListener('timeupdate', () => {
  const cur = audioEl.currentTime;
  const dur = audioEl.duration || 0;
  const pct = dur ? (cur / dur * 100) : 0;
  $('prog-fill').style.width = pct + '%';
  $('np-prog-fill') && ($('np-prog-fill').style.width = pct + '%');
  $('cur-t').textContent = fmtTime(cur);
  $('np-cur-t') && ($('np-cur-t').textContent = fmtTime(cur));
  if (S.playing && !$('np-fullscreen').classList.contains('open')) {} // nothing extra
});

audioEl.addEventListener('loadedmetadata', () => {
  $('dur-t').textContent = fmtTime(audioEl.duration);
  $('np-dur-t') && ($('np-dur-t').textContent = fmtTime(audioEl.duration));
});

audioEl.addEventListener('progress', () => {
  if (audioEl.buffered.length && audioEl.duration) {
    const pct = (audioEl.buffered.end(audioEl.buffered.length - 1) / audioEl.duration * 100) + '%';
    $('prog-buf').style.width = pct;
    $('np-prog-buf') && ($('np-prog-buf').style.width = pct);
  }
});

audioEl.addEventListener('ended', () => {
  if (S.repeat === 'one') { audioEl.currentTime = 0; audioEl.play(); }
  else if (S.repeat === 'all' || S.qIdx < S.queue.length - 1) { nextTrack(); }
  else { S.playing = false; updatePlayBtn(); updateEqAnimClass(); }
});

audioEl.addEventListener('play', () => {
  S.playing = true; updatePlayBtn(); updateEqAnimClass();
  cancelAnimationFrame(animFrame); drawVisualizer();
});

audioEl.addEventListener('pause', () => {
  S.playing = false; updatePlayBtn(); updateEqAnimClass();
  cancelAnimationFrame(animFrame);
});

audioEl.addEventListener('error', () => {
  toast('⚠️ Could not load track. Try another.');
  S.playing = false; updatePlayBtn();
});

// ══════════════════════════════════════════
//  LIKES & PLAYLISTS
// ══════════════════════════════════════════
function isLiked(track) {
  return S.liked.has(track.audio || track.id);
}

function toggleLike(track) {
  const key = track.audio || track.id;
  if (S.liked.has(key)) {
    S.liked.delete(key);
    toast('💔 Removed from Liked Songs');
  } else {
    S.liked.add(key);
    // Store full track for liked page
    const likedTracks = JSON.parse(localStorage.getItem('lf_liked_tracks') || '[]');
    likedTracks.unshift(track);
    localStorage.setItem('lf_liked_tracks', JSON.stringify(likedTracks.slice(0, 200)));
    toast('❤️ Added to Liked Songs!');
  }
  localStorage.setItem('lf_liked', JSON.stringify([...S.liked]));
  $('liked-count').textContent = S.liked.size;
  updatePlayerLikeBtn();
  refreshTrackLikeBtns();
}

function toggleLikeCurrent() {
  if (!S.currentTrack) return;
  toggleLike(S.currentTrack);
}

function updatePlayerLikeBtn() {
  if (!S.currentTrack) return;
  const liked = isLiked(S.currentTrack);
  $('like-btn').classList.toggle('on', liked);
  $('like-btn').title = liked ? 'Unlike' : 'Like';
}

function refreshTrackLikeBtns() {
  $a('[data-track-audio]').forEach(el => {
    const key = el.dataset.trackAudio;
    el.classList.toggle('on', S.liked.has(key));
  });
}

function savePlaylists() {
  localStorage.setItem('lf_playlists', JSON.stringify(S.playlists));
  $('pl-count').textContent = S.playlists.length;
  renderSidebarPlaylists();
}

function createPlaylist() {
  const name = $('new-pl-name').value.trim();
  if (!name) { toast('Enter a name!'); return; }
  const pl = {id: Date.now(), name, tracks: []};
  if (S.pendingPlaylist) {
    pl.tracks.push(S.pendingPlaylist);
    toast(`✅ Added to "${name}"`);
  }
  S.playlists.push(pl);
  savePlaylists();
  $('new-pl-name').value = '';
  closeModal('playlist-modal');
}

function createNewPlaylist() {
  const name = $('newpl-name').value.trim();
  if (!name) { toast('Enter a name!'); return; }
  S.playlists.push({id: Date.now(), name, tracks: []});
  savePlaylists();
  $('newpl-name').value = '';
  closeModal('newpl-modal');
  toast(`✅ Playlist "${name}" created!`);
  renderLibContent('playlists');
}

function addToPlaylist(plId) {
  const pl = S.playlists.find(p => p.id === plId);
  if (!pl || !S.pendingPlaylist) return;
  if (!pl.tracks.find(t => t.audio === S.pendingPlaylist.audio)) {
    pl.tracks.push(S.pendingPlaylist);
    savePlaylists();
    toast(`✅ Added to "${pl.name}"`);
  } else {
    toast('Already in this playlist!');
  }
  closeModal('playlist-modal');
}

function openPlaylistModal(track) {
  S.pendingPlaylist = track || S.currentTrack;
  if (!S.pendingPlaylist) { toast('Play a track first!'); return; }
  const list = $('pl-list');
  list.innerHTML = S.playlists.length
    ? S.playlists.map(pl => `<div class="pl-item" onclick="addToPlaylist(${pl.id})"><span>${esc(pl.name)}</span><span class="pc">${pl.tracks.length} songs</span></div>`).join('')
    : '<div style="color:var(--muted);font-size:13px;padding:8px 0">No playlists yet — create one below!</div>';
  openModal('playlist-modal');
}

function openNewPlaylistModal() { openModal('newpl-modal'); }

function renderSidebarPlaylists() {
  $('sidebar-playlists').innerHTML = S.playlists.slice(0, 8).map(pl => `
    <div class="ni" onclick="showPlaylist(${pl.id})">
      <span style="font-size:14px">📋</span><span>${esc(pl.name)}</span><span class="badge">${pl.tracks.length}</span>
    </div>`).join('');
}

function showPlaylist(id) {
  const pl = S.playlists.find(p => p.id === id);
  if (!pl) return;
  nav('library');
  switchLibTab('playlists', null);
  // Scroll to or highlight playlist
  renderLibContent('playlists');
}

// ══════════════════════════════════════════
//  DOWNLOADS
// ══════════════════════════════════════════
function downloadCurrent() {
  if (!S.currentTrack) { toast('Play a track first!'); return; }
  const track = S.currentTrack;
  const a = document.createElement('a');
  a.href = track.audiodownload || track.audio;
  a.download = `${track.artist_name} - ${track.name}.mp3`;
  a.target = '_blank';
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  toast(`⬇️ Downloading: ${track.name}`);
}

function downloadTrack(track) {
  const a = document.createElement('a');
  a.href = track.audiodownload || track.audio;
  a.download = `${track.artist_name} - ${track.name}.mp3`;
  a.target = '_blank';
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  toast(`⬇️ Downloading: ${track.name}`);
}

// ══════════════════════════════════════════
//  LYRICS
// ══════════════════════════════════════════
async function openLyrics() {
  if (!S.currentTrack) { toast('Play a track first!'); return; }
  const track = S.currentTrack;
  $('lyrics-track-info').textContent = `${track.name} — ${track.artist_name}`;
  $('lyrics-text').textContent = 'Loading lyrics…';
  $('lyrics-text').className = 'loading';
  openModal('lyrics-modal');
  try {
    const r = await fetch(`${CFG.LYRICS}/${encodeURIComponent(track.artist_name)}/${encodeURIComponent(track.name)}`);
    const d = await r.json();
    if (d.lyrics) {
      $('lyrics-text').textContent = d.lyrics;
      $('lyrics-text').className = '';
    } else {
      $('lyrics-text').textContent = 'Lyrics not found for this track.\n\nTry searching on Genius or AZLyrics for:\n"' + track.name + '" by ' + track.artist_name;
      $('lyrics-text').className = '';
    }
  } catch {
    $('lyrics-text').textContent = 'Could not load lyrics. Check your connection.';
    $('lyrics-text').className = '';
  }
}

// ══════════════════════════════════════════
//  EQUALIZER UI
// ══════════════════════════════════════════
function renderEQModal() {
  const bandsEl = $('eq-bands');
  bandsEl.innerHTML = EQ_BANDS.map((freq, i) => `
    <div class="eq-band">
      <div class="eq-val" id="eq-val-${i}">${S.eqGains[i] > 0 ? '+' : ''}${S.eqGains[i]}dB</div>
      <input type="range" min="-12" max="12" step="1" value="${S.eqGains[i]}"
        oninput="setEqBand(${i},parseFloat(this.value));$('eq-val-${i}').textContent=(this.value>0?'+':'')+this.value+'dB'">
      <label>${freq >= 1000 ? (freq/1000)+'k' : freq}</label>
    </div>`).join('');

  $('eq-presets').innerHTML = Object.keys(EQ_PRESETS).map(name => `
    <div class="eq-preset ${JSON.stringify(EQ_PRESETS[name])===JSON.stringify(S.eqGains)?'active':''}"
      data-preset="${name}" onclick="applyEqPreset('${name}')">${name}</div>`).join('');
}

function openEQ() { renderEQModal(); openModal('eq-modal'); }

// ══════════════════════════════════════════
//  AUDIO VISUALIZER
// ══════════════════════════════════════════
function drawVisualizer() {
  const canvas = $('np-canvas');
  if (!canvas || !analyserNode || !$('np-fullscreen').classList.contains('open')) return;
  const ctx = canvas.getContext('2d');
  const W = canvas.width = canvas.offsetWidth;
  const H = canvas.height = canvas.offsetHeight;
  const data = new Uint8Array(analyserNode.frequencyBinCount);
  analyserNode.getByteFrequencyData(data);
  ctx.clearRect(0, 0, W, H);
  const barW = W / data.length * 2.5;
  for (let i = 0; i < data.length; i++) {
    const h = (data[i] / 255) * H;
    const hue = (i / data.length) * 120 + 60;
    ctx.fillStyle = `hsl(${hue}, 90%, 55%)`;
    ctx.fillRect(i * (barW + 1), H - h, barW, h);
  }
  animFrame = requestAnimationFrame(drawVisualizer);
}

// ══════════════════════════════════════════
//  FULLSCREEN PLAYER
// ══════════════════════════════════════════
function openFullscreen() {
  $('np-fullscreen').classList.add('open');
  updateFullscreenUI();
  if (S.playing && analyserNode) { cancelAnimationFrame(animFrame); drawVisualizer(); }
}

function closeFullscreen() {
  $('np-fullscreen').classList.remove('open');
  cancelAnimationFrame(animFrame);
}

function updateFullscreenUI() {
  if (!S.currentTrack) return;
  const t = S.currentTrack;
  const bigArt = $('np-big-art');
  bigArt.innerHTML = t.image ? `<img src="${t.image}" alt="">` : artEmoji(t);
  $('np-big-title').textContent = t.name;
  $('np-big-artist').textContent = t.artist_name;
  const ni = $('np-pp-icon');
  if (ni) ni.innerHTML = S.playing ? '<path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z"/>' : '<path d="M8 5v14l11-7z"/>';
}

// ══════════════════════════════════════════
//  UI HELPERS
// ══════════════════════════════════════════
function updatePlayerUI() {
  if (!S.currentTrack) return;
  const t = S.currentTrack;
  const art = $('now-art');
  if (t.image) { art.innerHTML = `<img src="${t.image}" alt="">`; }
  else { art.innerHTML = artEmoji(t); art.style.background = t._color || '#2a2a3f'; }
  art.classList.toggle('spinning', S.playing);
  $('now-title').textContent = t.name;
  $('now-artist').textContent = t.artist_name;
  updatePlayBtn();
  updatePlayerLikeBtn();
  updateFullscreenUI();
  // Highlight active track in lists
  $a('.track').forEach(el => el.classList.remove('playing'));
  $a(`[data-track-audio="${CSS.escape(t.audio)}"]`).forEach(el => {
    const row = el.closest('.track');
    if (row) row.classList.add('playing');
  });
}

function updatePlayBtn() {
  const icon = '<path d="M8 5v14l11-7z"/>';
  const pauseIcon = '<path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z"/>';
  const si = S.playing ? pauseIcon : icon;
  $('pp-icon').innerHTML = si;
  const npi = $('np-pp-icon'); if (npi) npi.innerHTML = si;
  $('now-art').classList.toggle('spinning', S.playing);
}

function updateEqAnimClass() {
  $a('.track.playing').forEach(el => el.classList.toggle('t-paused', !S.playing));
}

function cardHTML(t) {
  const art = t.image ? `<img src="${t.image}" alt="${esc(t.name)}" loading="lazy">` : `<div class="fallback" style="background:${t._color||'#2a2a3f'}">${artEmoji(t)}</div>`;
  return `<div class="card" onclick='playTrack(${JSON.stringify(t).replace(/'/g,"&#39;")})'>
    <div class="card-art">${art}<button class="card-play"><svg width="14" height="14" viewBox="0 0 24 24" fill="black"><path d="M8 5v14l11-7z"/></svg></button></div>
    <div class="card-info"><div class="card-title">${esc(t.name)}</div><div class="card-sub">${esc(t.artist_name)}</div></div>
  </div>`;
}

function trackRowHTML(t, i, queue) {
  const liked = isLiked(t);
  const art = t.image ? `<img src="${t.image}" alt="" loading="lazy">` : artEmoji(t);
  const safeT = JSON.stringify(t).replace(/'/g, '&#39;');
  const safeQ = JSON.stringify(queue).replace(/'/g, '&#39;');
  return `<div class="track" onclick='playQueue(${safeQ},${i})' data-track-audio="${esc(t.audio)}">
    <div class="t-num">${i+1}</div>
    <div class="t-eq"><span></span><span></span><span></span><span></span></div>
    <div class="t-info">
      <div class="t-thumb" style="background:${t._color||'#2a2a3f'}">${art}</div>
      <div><div class="t-name">${esc(t.name)}</div><div class="t-artist">${esc(t.artist_name)}</div></div>
    </div>
    <div class="t-album">${esc(t.album_name||'—')}</div>
    <div class="t-dur">${fmtTime(t.duration||0)}</div>
    <div class="t-like ${liked?'on':''}" data-track-audio="${esc(t.audio)}"
      onclick="event.stopPropagation();toggleLike(${safeT})">
      <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>
    </div>
  </div>`;
}

// ══════════════════════════════════════════
//  NAVIGATION
// ══════════════════════════════════════════
function nav(page) {
  $a('.page').forEach(p => p.classList.remove('active'));
  $(`page-${page}`)?.classList.add('active');
  $a('.ni').forEach(n => n.classList.remove('active'));
  $a('.mn-item').forEach(n => n.classList.remove('active'));
  S.page = page;
  $('main').scrollTop = 0;

  // Activate corresponding nav item
  const maps = {home:0, search:1, library:2, liked:3};
  if (maps[page] !== undefined) {
    $a('.ni')[maps[page]]?.classList.add('active');
    $a('.mn-item')[maps[page]]?.classList.add('active');
  }

  if (page === 'liked') renderLikedPage();
  if (page === 'history') renderHistoryPage();
  if (page === 'library') renderLibContent('playlists');
}

// ══════════════════════════════════════════
//  PAGE RENDERERS
// ══════════════════════════════════════════
function renderLikedPage() {
  const tracks = JSON.parse(localStorage.getItem('lf_liked_tracks') || '[]')
    .filter(t => S.liked.has(t.audio || t.id));
  $('liked-sub').textContent = `${tracks.length} song${tracks.length !== 1 ? 's' : ''}`;
  $('liked-tracks').innerHTML = tracks.length
    ? tracks.map((t, i) => trackRowHTML(t, i, tracks)).join('')
    : '<div style="color:var(--muted);text-align:center;padding:40px">No liked songs yet!<br>Heart a track to save it here.</div>';
}

function playLiked() {
  const tracks = JSON.parse(localStorage.getItem('lf_liked_tracks') || '[]')
    .filter(t => S.liked.has(t.audio || t.id));
  if (tracks.length) playQueue(tracks, 0);
  else toast('No liked songs yet!');
}

function shuffleLiked() {
  const tracks = JSON.parse(localStorage.getItem('lf_liked_tracks') || '[]')
    .filter(t => S.liked.has(t.audio || t.id));
  if (!tracks.length) { toast('No liked songs yet!'); return; }
  const shuffled = [...tracks].sort(() => Math.random() - .5);
  playQueue(shuffled, 0);
}

function renderHistoryPage() {
  $('history-tracks').innerHTML = S.history.length
    ? S.history.map((t, i) => trackRowHTML(t, i, S.history)).join('')
    : '<div style="color:var(--muted);text-align:center;padding:40px">No history yet.<br>Play some tracks!</div>';
}

function clearHistory() {
  S.history = [];
  localStorage.removeItem('lf_history');
  renderHistoryPage();
  toast('🗑️ History cleared');
}

function renderLibContent(tab) {
  const el = $('lib-content');
  if (tab === 'playlists') {
    if (!S.playlists.length) {
      el.innerHTML = '<div style="color:var(--muted);text-align:center;padding:40px;">No playlists yet.<br><button onclick="openNewPlaylistModal()" style="margin-top:12px;background:var(--accent);color:#000;border:none;padding:10px 20px;border-radius:20px;cursor:pointer;font-weight:700">Create Playlist</button></div>';
      return;
    }
    el.innerHTML = `<div class="cards c4" style="padding-bottom:100px">${S.playlists.map(pl => `
      <div class="card" onclick="playPlaylist(${pl.id})">
        <div class="card-art"><div class="fallback" style="background:linear-gradient(135deg,#667eea,#764ba2);font-size:32px">📋</div>
          <button class="card-play"><svg width="14" height="14" viewBox="0 0 24 24" fill="black"><path d="M8 5v14l11-7z"/></svg></button></div>
        <div class="card-info">
          <div class="card-title">${esc(pl.name)}</div>
          <div class="card-sub">${pl.tracks.length} songs
            <span onclick="event.stopPropagation();deletePlaylist(${pl.id})" style="margin-left:8px;color:var(--muted);font-size:10px;cursor:pointer">🗑️</span>
          </div>
        </div>
      </div>`).join('')}</div>`;
  } else if (tab === 'liked') {
    renderLikedPage();
    el.innerHTML = $('liked-tracks').innerHTML;
  } else if (tab === 'history') {
    renderHistoryPage();
    el.innerHTML = $('history-tracks').innerHTML;
  }
}

function switchLibTab(tab, btn) {
  $a('.lib-tabs .tab').forEach(t => t.classList.remove('active'));
  if (btn) btn.classList.add('active');
  renderLibContent(tab);
}

function playPlaylist(id) {
  const pl = S.playlists.find(p => p.id === id);
  if (!pl || !pl.tracks.length) { toast('Empty playlist!'); return; }
  playQueue(pl.tracks, 0);
}

function deletePlaylist(id) {
  S.playlists = S.playlists.filter(p => p.id !== id);
  savePlaylists();
  renderLibContent('playlists');
  toast('🗑️ Playlist deleted');
}

// ══════════════════════════════════════════
//  MODAL HELPERS
// ══════════════════════════════════════════
function openModal(id) { $(id).classList.add('open'); }
function closeModal(id) { $(id).classList.remove('open'); }
document.querySelectorAll('.modal-bg').forEach(m => {
  m.addEventListener('click', e => { if (e.target === m) m.classList.remove('open'); });
});

// ══════════════════════════════════════════
//  KEYBOARD SHORTCUTS
// ══════════════════════════════════════════
document.addEventListener('keydown', e => {
  if (['INPUT','TEXTAREA'].includes(e.target.tagName)) return;
  switch(e.key) {
    case ' ': e.preventDefault(); togglePlay(); break;
    case 'ArrowRight': if (e.altKey) { e.preventDefault(); nextTrack(); } break;
    case 'ArrowLeft':  if (e.altKey) { e.preventDefault(); prevTrack(); } break;
    case 'ArrowUp':    if (e.altKey) { e.preventDefault(); setVolume(Math.min(100, S.volume+5)); $('vol-slider').value = S.volume; } break;
    case 'ArrowDown':  if (e.altKey) { e.preventDefault(); setVolume(Math.max(0, S.volume-5)); $('vol-slider').value = S.volume; } break;
    case 'm': case 'M': toggleMute(); break;
    case 'l': case 'L': toggleLikeCurrent(); break;
    case 's': case 'S': toggleShuffle(); break;
    case 'f': case 'F': if ($('np-fullscreen').classList.contains('open')) closeFullscreen(); else openFullscreen(); break;
    case 'Escape': closeFullscreen(); $a('.modal-bg.open').forEach(m => m.classList.remove('open')); break;
  }
});

// ══════════════════════════════════════════
//  UTILITIES
// ══════════════════════════════════════════
function fmtTime(s) {
  s = Math.floor(s || 0);
  return Math.floor(s/60) + ':' + String(s%60).padStart(2,'0');
}

function esc(s) {
  return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

const EMOJIS = ['🎵','🎶','🎸','🎤','🎹','🎺','🎻','🥁','🎧','🎼'];
function artEmoji(t) {
  const idx = (t.id || t.name || '').toString().charCodeAt(0) % EMOJIS.length;
  return EMOJIS[idx];
}

let toastTimer;
function toast(msg) {
  const el = $('toast');
  el.textContent = msg;
  el.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => el.classList.remove('show'), 2500);
}

function saveRecentTracks() { /* history already saved in playTrack */ }

// ══════════════════════════════════════════
//  SEARCH HANDLER
// ══════════════════════════════════════════
$('search-input').addEventListener('input', e => {
  clearTimeout(S.searchTimer);
  const q = e.target.value.trim();
  if (!q) { $('search-results').style.display = 'none'; $('genre-browse').style.display = 'block'; return; }
  S.searchTimer = setTimeout(() => searchTracks(q), 400);
});

// ══════════════════════════════════════════
//  VOLUME INIT
// ══════════════════════════════════════════
$('vol-slider').value = S.volume;

// ══════════════════════════════════════════
//  PWA SERVICE WORKER
// ══════════════════════════════════════════
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('sw.js').then(() => console.log('SW registered')).catch(()=>{});
}

// ══════════════════════════════════════════
//  APP INIT
// ══════════════════════════════════════════
(async function init() {
  // Update badge counts
  $('liked-count').textContent = S.liked.size;
  $('pl-count').textContent = S.playlists.length;

  // Render sidebar playlists
  renderSidebarPlaylists();

  // Load home page data
  await Promise.all([
    loadHomeFeatured(),
    loadHomeTrending(),
    loadHomeTopTracks(),
  ]);

  // Restore volume
  if (!S.audioReady) audioEl.volume = S.volume / 100;
})();
</script>
</body>
</html>
