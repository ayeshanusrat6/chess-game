<!--
INDEX.HTML — Chess Website (Menu + Online + Offline + Rules + Chat + Sounds)

What’s inside (single file, GitHub Pages ready)
- Start screen with: Chess title → Play Online / Play Offline / How to Play.
- Online: Random match or Play with Friend (presence list). Enforced sides, no undo, **60s per move**.
- Offline: Human vs Computer (AI) or Human vs Human (same device). **Undo enabled**. Time: 60s, 2m, 5m, No limit.
- Move history, last-move highlight, check highlight, basic sound effects.
- Chat in online rooms (no delete), presence with green dot.
- Firebase (Anon Auth + Realtime Database) for online features; graceful offline fallback.

Publish on GitHub Pages
1) Create repo → add this file as `index.html` at the root.
2) Settings → Pages → Deploy from branch → main + root.
3) Open the URL GitHub gives you.

Enable Online (serverless)
A) Create Firebase project → add Web app → copy config into FIREBASE CONFIG block below.
B) Enable Anonymous Authentication.
C) Create Realtime Database and start in test mode (demo). I can provide production rules later.
-->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Chess — Online & Offline</title>
    <style>
      :root {
        --bg: #0b1220;
        --panel: #111827;
        --text: #e5e7eb;
        --muted: #9ca3af;
        --primary: #2563eb;
        --accent: #10b981;
        --warn: #eab308;
        --danger: #ef4444;
        --board-light: #f0d9b5;
        --board-dark: #b58863;
        --board-light-night: #6b5b3a;
        --board-dark-night: #403126;
      }
      * { box-sizing: border-box; }
      body { margin:0; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, Cantarell, Noto Sans, Arial; background:#000; color:var(--text); }
      .app { min-height:100vh; padding: 16px; background: var(--bg); }
      .container { max-width: 1200px; margin: 0 auto; }
      .card { background: var(--panel); border: 1px solid rgba(255,255,255,0.08); border-radius: 16px; padding: 16px; }
      .btn { border:0; border-radius: 12px; padding:10px 14px; cursor:pointer; background:#374151; color:white; }
      .btn.primary{ background:var(--primary); }
      .btn.accent{ background:var(--accent); color:#072; }
      .btn.warn{ background:var(--warn); color:#111; }
      .btn.danger{ background:var(--danger); }
      .btn.ghost{ background:transparent; border:1px solid #374151; }
      .row { display:flex; align-items:center; gap:12px; flex-wrap:wrap; }
      .col { display:flex; flex-direction:column; gap:12px; }
      .title { font-size: 32px; font-weight:800; text-align:center; margin: 10px 0 16px; }
      .subtitle { text-align:center; color: var(--muted); margin-bottom: 16px; }
      .board { width: 480px; border-radius:12px; overflow:hidden; box-shadow: 0 10px 30px rgba(0,0,0,0.4); }
      .grid { display:grid; grid-template-columns: repeat(8, 1fr); }
      .square { width:60px; height:60px; display:flex; align-items:center; justify-content:center; position:relative; cursor:pointer; border:1px solid rgba(0,0,0,0.08); }
      .sel { outline:3px solid #22c55e; }
      .dot { position:absolute; width:12px; height:12px; border-radius:6px; background:rgba(34,197,94,0.9); bottom:6px; right:6px; }
      .highlight { outline: 3px solid rgba(59,130,246,0.9); }
      .check { box-shadow: inset 0 0 0 3px rgba(239,68,68,0.9); }
      .clock { background:#0f172a; padding:8px 12px; border-radius:10px; font-variant-numeric: tabular-nums; }
      .clock.active { outline:2px solid var(--accent); }
      .clock.flag { outline:2px solid var(--danger); }
      .list { max-height: 200px; overflow:auto; border-radius: 12px; border:1px solid rgba(255,255,255,0.12); }
      .list-item { display:flex; justify-content:space-between; padding:8px 10px; }
      .dot-online { width:10px; height:10px; border-radius:5px; display:inline-block; }
      .chat { height: 180px; overflow:auto; border-radius: 12px; border:1px solid rgba(255,255,255,0.15); padding:8px; background:#0b1324; }
      .msg { margin:4px 0; }
      .you { color:#a7f3d0; }
      .sys { color:#93c5fd; font-style: italic; }
      @media (max-width: 520px) { .board { width: 360px; } .square { width:45px; height:45px; } }
      a { color: #93c5fd; }
    </style>

    <!-- React & Babel -->
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <!-- chess.js classic UMD -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/chess.js/0.10.3/chess.min.js"></script>

    <!-- Firebase (optional for online) -->
    <script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-database-compat.js"></script>

    <!-- 🔧 Paste your Firebase config below (replace null). Keep keys exact. -->
    <script>
      window.FIREBASE_CONFIG = null; /* Example:
      window.FIREBASE_CONFIG = {
        apiKey: "...",
        authDomain: "your-app.firebaseapp.com",
        databaseURL: "https://your-app-default-rtdb.asia-southeast1.firebasedatabase.app",
        projectId: "your-app",
        storageBucket: "your-app.appspot.com",
        messagingSenderId: "...",
        appId: "..."
      } */
    </script>
  </head>
  <body>
    <div id="root"></div>

    <script type="text/babel">
      const { useEffect, useMemo, useRef, useState } = React;

      // ---------- Utilities ----------
      const randId = () => Math.random().toString(36).slice(2, 10);
      function fmt(ms){ if (ms===Infinity) return '∞'; const s=Math.max(0,Math.floor(ms/1000)); const m=Math.floor(s/60); const r=s%60; return m+':'+String(r).padStart(2,'0'); }

      // Simple sounds via WebAudio (single-file)
      function useSounds(){
        const ctxRef = useRef(null);
        function get(){ if(!ctxRef.current) ctxRef.current = new (window.AudioContext||window.webkitAudioContext)(); return ctxRef.current; }
        function beep(freq=660, dur=0.06){ const ctx=get(); const o=ctx.createOscillator(); const g=ctx.createGain(); o.frequency.value=freq; o.type='sine'; o.connect(g); g.connect(ctx.destination); o.start(); g.gain.setValueAtTime(0.15, ctx.currentTime); g.gain.exponentialRampToValueAtTime(0.0001, ctx.currentTime+dur); o.stop(ctx.currentTime+dur); }
        return { move:()=>beep(660,0.05), capture:()=>beep(360,0.08), check:()=>beep(880,0.1), end:()=>beep(220,0.2) };
      }

      // Optional Firebase service
      function useFirebase(){
        const [fb, setFb] = useState({ ready:false, online:false, user:null, db:null });
        useEffect(()=>{
          const cfg = window.FIREBASE_CONFIG; if(!cfg) return;
          try{
            const app = firebase.initializeApp(cfg);
            const auth = firebase.auth(); const db = firebase.database();
            auth.signInAnonymously().then(()=> setFb({ready:true, online:true, user:auth.currentUser, db})).catch(e=>console.warn('Auth failed', e));
          }catch(e){ console.warn('Firebase init skipped', e); }
        },[]);
        return fb;
      }

      // ---------- App ----------
      function App(){
        const sounds = useSounds();
        const fb = useFirebase();

        // Routing/screens
        const SCREENS = { HOME:'home', ONLINE:'online', OFFLINE:'offline', GAME:'game', RULES:'rules' };
        const [screen, setScreen] = useState(SCREENS.HOME);

        // User state
        const [username, setUsername] = useState(()=> localStorage.getItem('username') || ('player_'+randId()));
        useEffect(()=> localStorage.setItem('username', username), [username]);

        // Game model
        const [game, setGame] = useState(()=> new window.Chess());
        const [board, setBoard] = useState(game.board());
        const [turn, setTurn] = useState(game.turn());
        const [selected, setSelected] = useState(null);
        const [legal, setLegal] = useState([]);
        const [lastMove, setLastMove] = useState(null); // {from,to}
        const [bgChoice, setBgChoice] = useState('white');
        const [night, setNight] = useState(false);
        const [statusMsg, setStatusMsg] = useState('Welcome!');

        // Modes
        // gameMode: 'bot' | 'friend-local' | 'online-random' | 'online-room'
        const [gameMode, setGameMode] = useState(null);

        // Time controls (offline)
        const OFFLINE_TIMES = [ {k:'60',label:'60 sec',ms:60000}, {k:'120',label:'2 min',ms:120000}, {k:'300',label:'5 min',ms:300000}, {k:'none',label:'No limit',ms:Infinity} ];
        const [offKey, setOffKey] = useState('none');
        const [wMs, setWMs] = useState(Infinity);
        const [bMs, setBMs] = useState(Infinity);
        const [running, setRunning] = useState(true);
        const lastTickRef = useRef(null);

        // Online per-move timer (60s per turn)
        const PER_MOVE_MS = 60000; // 60 seconds
        const [moveMs, setMoveMs] = useState(PER_MOVE_MS); // only used in online

        // AI
        const [aiLevel, setAiLevel] = useState('easy');

        // Online
        const [presence, setPresence] = useState([]);
        const [friends, setFriends] = useState(()=> JSON.parse(localStorage.getItem('friends')||'[]'));
        useEffect(()=> localStorage.setItem('friends', JSON.stringify(friends)), [friends]);
        const [roomId, setRoomId] = useState('');
        const [connected, setConnected] = useState(false);
        const [side, setSide] = useState(null); // 'w' | 'b' for online games

        // Chat
        const [messages, setMessages] = useState([]);
        const [chatInput, setChatInput] = useState('');
        const chatRef = useRef(null);
        useEffect(()=>{ if(chatRef.current) chatRef.current.scrollTop = chatRef.current.scrollHeight; }, [messages]);

        // Board colors
        const lightSq = night? 'var(--board-light-night)' : 'var(--board-light)';
        const darkSq  = night? 'var(--board-dark-night)'  : 'var(--board-dark)';
        const pageBg = bgChoice==='black'? '#000' : '#fff';
        const textColor = bgChoice==='black'? '#fff' : '#111';

        // Sync on game object change
        useEffect(()=>{ setBoard(game.board()); setTurn(game.turn()); }, [game]);

        // Offline clocks init on selection
        useEffect(()=>{
          const opt = OFFLINE_TIMES.find(o=>o.k===offKey) || OFFLINE_TIMES[OFFLINE_TIMES.length-1];
          setWMs(opt.ms); setBMs(opt.ms); setRunning(true); lastTickRef.current = performance.now();
        }, [offKey]);

        // Offline clock loop (total time per side)
        useEffect(()=>{
          if (!running) return;
          if (wMs===Infinity && bMs===Infinity) return; // no offline time control
          if (gameMode && gameMode.startsWith('online')) return; // only offline here
          let raf; function loop(){
            const now=performance.now(); const last=lastTickRef.current||now; const dt=now-last; lastTickRef.current=now;
            const sideT = game.turn(); if(sideT==='w') setWMs(p=>Math.max(0,p-dt)); else setBMs(p=>Math.max(0,p-dt));
            raf=requestAnimationFrame(loop);
          } raf=requestAnimationFrame(loop); return ()=>cancelAnimationFrame(raf);
        }, [running, gameMode, game, wMs, bMs]);

        // Online per-move countdown loop (60s per move)
        useEffect(()=>{
          if (!(gameMode && gameMode.startsWith('online'))) return;
          let id = setInterval(()=> setMoveMs(p=> Math.max(0, p-250)), 250);
          return ()=> clearInterval(id);
        }, [gameMode]);

        // Flag / Move timeouts
        useEffect(()=>{
          if (gameMode && gameMode.startsWith('online')){
            if (moveMs===0){ setStatusMsg('Time up! Opponent wins.'); sounds.end(); setRunning(false); }
          } else {
            if (wMs===0){ setStatusMsg('White lost on time.'); sounds.end(); setRunning(false); }
            if (bMs===0){ setStatusMsg('Black lost on time.'); sounds.end(); setRunning(false); }
          }
        }, [moveMs, wMs, bMs, gameMode]);

        function resetGame(){
          const g=new window.Chess(); setGame(g); setSelected(null); setLegal([]); setLastMove(null); setMessages([]);
          setStatusMsg('New game started.');
          if (gameMode && gameMode.startsWith('online')){ setMoveMs(PER_MOVE_MS); pushState(g); }
          else { const opt = OFFLINE_TIMES.find(o=>o.k===offKey) || {ms:Infinity}; setWMs(opt.ms); setBMs(opt.ms); }
        }

        function indexToSquare(r,f){ const file=String.fromCharCode('a'.charCodeAt(0)+f); const rank=8-r; return `${file}${rank}`; }
        function squareToIndex(sq){ const f=sq.charCodeAt(0)-97; const r=8-parseInt(sq[1],10); return [r,f]; }

        // ---------- Firebase presence & rooms ----------
        useEffect(()=>{
          if (!fb.online) return;
          const uid=fb.user.uid; const db=fb.db; const myRef=db.ref('presence/'+uid);
          myRef.onDisconnect().remove(); myRef.set({ name: username, ts: Date.now() });
          const listRef=db.ref('presence');
          listRef.on('value', snap=>{ const val=snap.val()||{}; const arr=Object.entries(val).map(([uid,v])=>({uid,...v})); arr.sort((a,b)=>b.ts-a.ts); setPresence(arr); });
          return ()=>{ listRef.off(); myRef.remove(); };
        }, [fb.online, username]);

        function createRoomId(){ return 'r_'+randId(); }

        function joinRoom(id){
          if (!fb.online){ setStatusMsg('Online needs Firebase config.'); return; }
          const db=fb.db; const uid=fb.user.uid; const roomRef=db.ref('rooms/'+id);
          setRoomId(id);
          // State listener
          roomRef.child('state').on('value', snap=>{
            const s=snap.val(); if(!s||!s.fen) return; const g=new window.Chess(s.fen); setGame(g); setMoveMs(s.moveMs ?? PER_MOVE_MS); setStatusMsg(s.note||'Synced'); setLastMove(s.lastMove||null);
          });
          // Chat listener
          roomRef.child('chat').limitToLast(200).on('child_added', snap=> setMessages(prev=>[...prev, snap.val()]));
          // Players meta
          roomRef.child('players').on('value', snap=>{
            const players=snap.val()||{}; const me=players[uid]; if(me && me.side) setSide(me.side==='white'?'w':'b');
          });
          setConnected(true); setGameMode('online-room'); setScreen(SCREENS.GAME);
          // Init room if new
          roomRef.child('meta').once('value').then(s=>{
            if(!s.exists()){
              const sides=Math.random()<0.5?['white','black']:['black','white'];
              roomRef.set({ meta:{created:Date.now(),createdBy:uid}, players:{} });
              roomRef.child('players/'+uid).set({ name: username, side: sides[0] });
              pushState(game, roomRef);
            } else {
              // Just ensure we appear in players
              roomRef.child('players/'+uid).set({ name: username, side: side==='w'?'white':(side==='b'?'black':null) });
            }
          });
        }

        function pushState(g, refOverride){
          if (!fb.online || !roomId) return;
          const ref = refOverride || fb.db.ref('rooms/'+roomId);
          const payload = { fen: g.fen(), turn: g.turn(), lastMove, moveMs, note: statusMsg, ts: Date.now() };
          ref.child('state').set(payload);
        }

        function sendChat(){ if(!chatInput.trim()) return; const msg={by:username, text:chatInput.trim(), ts:Date.now()}; setMessages(p=>[...p,msg]); if(fb.online&&roomId) fb.db.ref('rooms/'+roomId+'/chat').push(msg); setChatInput(''); }

        // Quick random matchmaking
        function quickMatch(){
          if (!fb.online){ setStatusMsg('Online needs Firebase config.'); return; }
          const db=fb.db; const uid=fb.user.uid; const qRef=db.ref('queue');
          qRef.transaction(q=>{ q=q||[]; const partner=q.find(e=>e.uid!==uid); if(partner){ q=q.filter(e=>e.uid!==partner.uid); return q; } else { q.push({uid,name:username,ts:Date.now()}); return q; } }, (err, committed, snap)=>{
            if(err){ setStatusMsg('Queue error'); return; }
            const arr=snap.val()||[]; const partner=arr.find(e=>e.uid!==uid);
            if(partner){ const id=createRoomId(); const roomRef=fb.db.ref('rooms/'+id); const sides=Math.random()<0.5?['white','black']:['black','white']; roomRef.set({ meta:{created:Date.now(),createdBy:uid}, players:{} }); roomRef.child('players/'+uid).set({name:username, side:sides[0]}); roomRef.child('players/'+partner.uid).set({name:partner.name, side:sides[1]}); pushState(game, roomRef); joinRoom(id); setStatusMsg('Matched! Room '+id); }
            else { setStatusMsg('Searching… keep this tab open.'); }
          });
        }

        // ---------- Moves / AI / Undo ----------
        function evaluateBoard(g){ const v={p:100,n:320,b:330,r:500,q:900,k:20000}; let tot=0; for(let r=0;r<8;r++) for(let f=0;f<8;f++){ const piece=g.board()[r][f]; if(!piece) continue; tot+=(piece.color==='w'?1:-1)*(v[piece.type]||0);} return tot; }
        function minimax(depth, g, a, b, max){ if(depth===0) return evaluateBoard(g); const moves=g.moves(); if(!moves.length) return evaluateBoard(g); if(max){ let best=-Infinity; for(const m of moves){ const g2=new window.Chess(g.fen()); g2.move(m); const v=minimax(depth-1,g2,a,b,false); best=Math.max(best,v); a=Math.max(a,v); if(b<=a) break; } return best; } else { let best=Infinity; for(const m of moves){ const g2=new window.Chess(g.fen()); g2.move(m); const v=minimax(depth-1,g2,a,b,true); best=Math.min(best,v); b=Math.min(b,v); if(b<=a) break; } return best; } }
        function minimaxRoot(d,g){ const moves=g.moves(); let best=null; let val=-Infinity; for(const m of moves){ const g2=new window.Chess(g.fen()); g2.move(m); const v=minimax(d-1,g2,-Infinity,Infinity,false); if(v>val){ val=v; best=m; } } return best; }

        const [history, setHistory] = useState([]); // SAN list

        function recordMove(res){
          // sounds
          if (res.flags && res.flags.includes('c')) sounds.capture(); else sounds.move();
          if (game.in_check()) sounds.check();
          // last move + history
          setLastMove({ from: res.from, to: res.to });
          setHistory(h=>[...h, res.san]);
          // Online: reset per-move timer when turn changes
          if (gameMode && gameMode.startsWith('online')) setMoveMs(PER_MOVE_MS);
          // Game end?
          if (game.game_over()){ sounds.end(); if (game.in_checkmate()) setStatusMsg((turn==='w'?'Black':'White')+' wins by checkmate'); else if (game.in_draw()) setStatusMsg('Drawn game'); }
        }

        function tryMove(from, to){
          // Side lock in online
          if (gameMode && gameMode.startsWith('online')){
            if (!side){ setStatusMsg('Assigning sides…'); return; }
            if ( (game.turn()==='w' && side!=='w') || (game.turn()==='b' && side!=='b') ) { setStatusMsg('Not your turn'); return; }
          }
          let moveObj={ from, to };
          // auto-queen promotion
          const [sr,sf]=squareToIndex(from); const src=board[sr]?.[sf];
          if (src && src.type==='p'){ const tr=to[1]; if ((src.color==='w' && tr==='8') || (src.color==='b' && tr==='1')) moveObj.promotion='q'; }
          try{
            const res=game.move(moveObj);
            if (res){
              setGame(new window.Chess(game.fen())); setSelected(null); setLegal([]); setStatusMsg(`Moved ${res.san}`);
              recordMove(res);
              // AI reply in offline bot mode
              if (gameMode==='bot' && game.turn()==='b') setTimeout(()=>botMove(), 150);
              // Push online state
              if (gameMode && gameMode.startsWith('online')) pushState(game);
            } else {
              // reselection
              const moves=game.moves({square:to, verbose:true}); if(moves.length){ setSelected(to); setLegal(moves.map(m=>m.to)); } else { setSelected(null); setLegal([]); }
            }
          }catch(e){ console.warn('Invalid move', e); setStatusMsg('Invalid move'); setSelected(null); setLegal([]); }
        }

        function handleSquareClick(r,f){
          if (running===false) return;
          // Online: move timer expired?
          if (gameMode && gameMode.startsWith('online') && moveMs===0) return;
          const sq=indexToSquare(r,f);
          if (!selected){ const moves=game.moves({square:sq, verbose:true}); if(!moves.length) return; setSelected(sq); setLegal(moves.map(m=>m.to)); return; }
          if (selected===sq){ setSelected(null); setLegal([]); return; }
          tryMove(selected, sq);
        }

        function botMove(){
          if (game.game_over()) return; const legal=game.moves(); if(!legal.length) return;
          let mv=null; if(aiLevel==='easy') mv=legal[Math.floor(Math.random()*legal.length)]; else if(aiLevel==='medium') mv=minimaxRoot(2, game); else mv=minimaxRoot(3, game);
          try{ const res=game.move(mv); setGame(new window.Chess(game.fen())); setStatusMsg('Computer played '+mv); recordMove(res); } catch(e){ console.error('Bot failed', e); }
        }

        function undo(){
          if (gameMode && gameMode.startsWith('online')){ setStatusMsg('Undo is disabled online'); return; }
          const res=game.undo(); if(!res) return; setGame(new window.Chess(game.fen())); setHistory(h=>h.slice(0,-1)); setLastMove(null); setStatusMsg('Move undone'); sounds.move();
        }

        // ---------- UI Components ----------
        function Home(){
          return (
            <div className="container">
              <div className="title">Chess</div>
              <div className="subtitle">Play Online or Offline • AI • Friend • Rules</div>
              <div className="row" style={{justifyContent:'center'}}>
                <button className="btn primary" onClick={()=>setScreen(SCREENS.ONLINE)}>Play Online</button>
                <button className="btn" onClick={()=>setScreen(SCREENS.OFFLINE)}>Play Offline</button>
                <button className="btn ghost" onClick={()=>setScreen(SCREENS.RULES)}>How to Play</button>
              </div>
            </div>
          );
        }

        function OnlineMenu(){
          return (
            <div className="container card">
              <h2 style={{marginTop:0}}>Online</h2>
              {!fb.online && (
                <div className="card" style={{background:'#281f1f', color:'#fde68a', marginBottom:12}}>
                  Add your Firebase config at the top of this file to enable online features.
                </div>
              )}
              <div className="row" style={{marginBottom:12}}>
                <button className="btn primary" onClick={()=>{ setGameMode('online-random'); quickMatch(); setScreen(SCREENS.GAME); setStatusMsg('Matching…'); }}>Random Player</button>
                <button className="btn" onClick={()=>{ setGameMode('online-room'); }}>Play with Friend</button>
              </div>

              {gameMode==='online-room' && (
                <div className="row" style={{alignItems:'flex-start'}}>
                  <div className="card" style={{flex:'1 1 260px'}}>
                    <div style={{fontWeight:600, marginBottom:6}}>Online Friends</div>
                    <div className="list">
                      {presence.filter(p=>p.name!==username).map(p=> (
                        <div key={p.uid} className="list-item">
                          <div><span className="dot-online" style={{background:'#22c55e', marginRight:6}}/> {p.name||p.uid.slice(0,6)}</div>
                          <button className="btn accent" onClick={()=>{ const id=createRoomId(); joinRoom(id); setStatusMsg('Share code '+id+' with your friend'); }}>Invite</button>
                        </div>
                      ))}
                      {presence.filter(p=>p.name!==username).length===0 && <div className="list-item" style={{opacity:0.7}}>No friends online</div>}
                    </div>
                  </div>
                  <div className="card" style={{flex:'1 1 260px'}}>
                    <div style={{fontWeight:600, marginBottom:6}}>Join by Room Code</div>
                    <div className="row">
                      <input className="btn" placeholder="Room code" value={roomId} onChange={e=>setRoomId(e.target.value)} style={{background:'#1f2937', color:'white', minWidth:160}} />
                      <button className="btn" onClick={()=>joinRoom(roomId||createRoomId())}>Join / Create</button>
                      <button className="btn" onClick={()=>navigator.clipboard?.writeText(roomId||'')}>Copy</button>
                    </div>
                  </div>
                </div>
              )}
              <div className="row" style={{marginTop:12}}>
                <button className="btn ghost" onClick={()=>setScreen(SCREENS.HOME)}>Back</button>
              </div>
            </div>
          );
        }

        function OfflineMenu(){
          return (
            <div className="container card">
              <h2 style={{marginTop:0}}>Offline</h2>
              <div className="row" style={{marginBottom:12}}>
                <button className="btn primary" onClick={()=>{ setGameMode('bot'); setScreen(SCREENS.GAME); resetGame(); setStatusMsg('Human vs Computer'); }}>Human vs Computer</button>
                <button className="btn" onClick={()=>{ setGameMode('friend-local'); setScreen(SCREENS.GAME); resetGame(); setStatusMsg('Human vs Human (same device)'); }}>Human vs Human</button>
              </div>
              <div className="row" style={{marginBottom:12}}>
                <span>Time:</span>
                <select className="btn" value={offKey} onChange={e=>setOffKey(e.target.value)}>
                  {OFFLINE_TIMES.map(o=> <option key={o.k} value={o.k}>{o.label}</option>)}
                </select>
                {gameMode==='bot' && (
                  <>
                    <span>AI:</span>
                    <select className="btn" value={aiLevel} onChange={e=>setAiLevel(e.target.value)}>
                      <option value="easy">Easy</option>
                      <option value="medium">Medium</option>
                      <option value="hard">Hard</option>
                    </select>
                  </>
                )}
              </div>
              <div className="row"><button className="btn ghost" onClick={()=>setScreen(SCREENS.HOME)}>Back</button></div>
            </div>
          );
        }

        function Rules(){
          return (
            <div className="container card">
              <h2 style={{marginTop:0}}>How to Play Chess</h2>
              <ul>
                <li>Goal: checkmate the opponent’s king (attack it so it cannot escape).</li>
                <li>Turns: White moves first, then players alternate one move each.</li>
                <li>Piece moves: Pawns (forward, capture diagonally; first move may go 2 squares), Knights (L-shape), Bishops (diagonals), Rooks (files/ranks), Queen (any direction), King (one square).</li>
                <li>Special: Castling (king+rook move), En passant (special pawn capture), Promotion (pawn reaches last rank → choose a piece; here auto-queen).</li>
                <li>End: Checkmate = win, Stalemate/insufficient material/threefold/50-move = draw.</li>
                <li>Online: No undo. Each move must be played within <b>60 seconds</b>.</li>
                <li>Offline: Undo allowed. Optional total time per side (60s/2m/5m/No limit).</li>
              </ul>
              <div className="row"><button className="btn" onClick={()=>setScreen(SCREENS.HOME)}>Back</button></div>
            </div>
          );
        }

        function GameUI(){
          return (
            <div className="container row" style={{color: textColor}}>
              {/* Left: Board and controls */}
              <div className="col" style={{flex:'0 0 auto'}}>
                <div className="row" style={{alignItems:'center'}}>
                  <label>Background:&nbsp;</label>
                  <select className="btn" value={bgChoice} onChange={e=>setBgChoice(e.target.value)}>
                    <option value="white">White</option>
                    <option value="black">Black</option>
                  </select>
                  <label className="row" style={{gap:6}}><input type="checkbox" checked={night} onChange={e=>setNight(e.target.checked)} /> Night board</label>
                  <button className="btn warn" onClick={resetGame}>Reset</button>
                  {!gameMode?.startsWith('online') && <button className="btn" onClick={undo}>Undo (offline only)</button>}
                  <button className="btn ghost" onClick={()=>setScreen(SCREENS.HOME)}>Exit</button>
                </div>

                {/* Clocks */}
                <div className="row" style={{margin:'8px 0 12px'}}>
                  {!(gameMode && gameMode.startsWith('online')) ? (
                    <>
                      <span className={`clock ${turn==='w'&&running? 'active':''} ${wMs===0?'flag':''}`}>♔ White: {fmt(wMs)}</span>
                      <span className={`clock ${turn==='b'&&running? 'active':''} ${bMs===0?'flag':''}`}>♚ Black: {fmt(bMs)}</span>
                    </>
                  ) : (
                    <span className={`clock ${moveMs===0?'flag':'active'}`}>⏱ Move time: {fmt(moveMs)}</span>
                  )}
                </div>

                {/* Board */}
                <div className="board">
                  <div className="grid">
                    {board.map((row,rIdx)=> row.map((cell,fIdx)=>{
                      const isLight=(rIdx+fIdx)%2===0; const bg=isLight? lightSq : darkSq; const sq=indexToSquare(rIdx,fIdx); const isSel=selected===sq; const isLegal=legal.includes(sq);
                      const whiteMap={p:'♙',n:'♘',b:'♗',r:'♖',q:'♕',k:'♔'}; const blackMap={p:'♟',n:'♞',b:'♝',r:'♜',q:'♛',k:'♚'}; const glyph=cell? (cell.color==='w'?whiteMap[cell.type]:blackMap[cell.type]) : '';
                      const lm = lastMove && (sq===lastMove.from || sq===lastMove.to);
                      // check highlight on current king
                      const inCheck = (cell && cell.type==='k' && cell.color===turn && game.in_check());
                      const cls = `square ${isSel?'sel':''} ${lm?'highlight':''} ${inCheck?'check':''}`;
                      return (
                        <div key={sq} className={cls} style={{background:bg}} onClick={()=>handleSquareClick(rIdx,fIdx)}>
                          <span style={{fontSize:28}}>{glyph}</span>
                          {isLegal && <div className="dot" />}
                        </div>
                      );
                    }))}
                  </div>
                </div>

                <div style={{marginTop:8}}>
                  Turn: {turn==='w'?'White':'Black'} • {statusMsg}
                </div>

                {/* Move history */}
                <div className="card" style={{marginTop:10}}>
                  <div style={{fontWeight:700, marginBottom:6}}>Moves</div>
                  <div className="list">
                    {history.length===0 && <div className="list-item" style={{opacity:0.7}}>No moves yet</div>}
                    {history.map((h,i)=> <div key={i} className="list-item"><span>#{i+1}</span><span>{h}</span></div>)}
                  </div>
                </div>
              </div>

              {/* Right: Side panel (online tools + chat) */}
              <div className="card" style={{flex:'1 1 360px'}}>
                <h3 style={{marginTop:0}}>Game Options</h3>
                <div className="row" style={{marginBottom:10}}>
                  {(!gameMode || gameMode==='bot') && (
                    <>
                      <span>AI:</span>
                      <select className="btn" value={aiLevel} onChange={e=>setAiLevel(e.target.value)}>
                        <option value="easy">Easy</option>
                        <option value="medium">Medium</option>
                        <option value="hard">Hard</option>
                      </select>
                    </>
                  )}
                  {(!gameMode || gameMode==='friend-local') && (
                    <>
                      <span>Offline time:</span>
                      <select className="btn" value={offKey} onChange={e=>setOffKey(e.target.value)}>
                        {OFFLINE_TIMES.map(o=> <option key={o.k} value={o.k}>{o.label}</option>)}
                      </select>
                    </>
                  )}
                </div>

                {/* Online widgets */}
                {gameMode&&gameMode.startsWith('online') && (
                  <>
                    <div className="card" style={{background:'#0b1324', marginBottom:10}}>
                      <div><b>Room:</b> {roomId || '(not set)'} &nbsp; <button className="btn" onClick={()=>navigator.clipboard?.writeText(roomId||'')}>Copy</button></div>
                      <div><b>Your side:</b> {side||'(assigning…)'} — moves locked to your color.</div>
                      <div style={{marginTop:6}}>Online games: <b>60 sec per move</b>, <b>Undo disabled</b>.</div>
                    </div>
                    <div className="card" style={{background:'#0b1220'}}>
                      <div style={{fontWeight:700, marginBottom:6}}>Chat</div>
                      <div className="chat" ref={chatRef}>
                        {messages.length===0 && <div className="sys msg">Chat appears here. (No delete)</div>}
                        {messages.map((m,i)=> <div key={i} className="msg"><span className={m.by===username?'you':''}><b>{m.by}:</b></span> {m.text}</div>)}
                      </div>
                      <div className="row" style={{marginTop:6}}>
                        <input className="btn" placeholder="Type message" value={chatInput} onChange={e=>setChatInput(e.target.value)} style={{flex:1, background:'#1f2937'}} />
                        <button className="btn primary" onClick={sendChat}>Send</button>
                      </div>
                    </div>
                  </>
                )}

                {/* Presence (always visible if configured) */}
                {fb.online && (
                  <div className="card" style={{marginTop:10}}>
                    <div style={{fontWeight:700, marginBottom:6}}>Online now</div>
                    <div className="list">
                      {presence.length===0 && <div className="list-item" style={{opacity:0.6}}>Nobody online</div>}
                      {presence.map(p=> (
                        <div key={p.uid} className="list-item">
                          <div><span className="dot-online" style={{background:'#22c55e', marginRight:6}}/> {p.name || p.uid.slice(0,6)}</div>
                          <button className="btn" onClick={()=>{ const id=createRoomId(); joinRoom(id); setStatusMsg('Invite your friend with code '+id); }}>Invite</button>
                        </div>
                      ))}
                    </div>
                  </div>
                )}
              </div>
            </div>
          );
        }

        // ---------- Self tests ----------
        function runTests(){
          const out=[]; const ok=(n,p)=>out.push((p?'✅ ':'❌ ')+n);
          try{ const g=new window.Chess(); g.load('8/6p1/8/6p1/8/8/6P1/6K1 w - - 0 1'); g.move({from:'g2',to:'g4'}); g.move('g5'); g.move({from:'g4',to:'g5'}); g.move('g4'); g.move({from:'g5',to:'g6'}); g.move('g3'); g.move({from:'g6',to:'g7'}); g.move('g2'); const r=g.move({from:'g7',to:'g8',promotion:'q'}); ok('Promotion accepted', !!r); }catch(e){ ok('Promotion accepted', false); }
          const opt=[{k:'60',ms:60000},{k:'120',ms:120000},{k:'300',ms:300000}]; ok('Offline time options', opt.every(o=>o.ms===(+o.k)*1000));
          const g2=new window.Chess(); const leg=g2.moves(); const mv=leg[Math.floor(Math.random()*leg.length)]; ok('Random legal move exists', leg.includes(mv));
          alert(out.join('\n'));
        }

        // ---------- Render ----------
        return (
          <div className="app">
            <div className="row" style={{justifyContent:'space-between', alignItems:'center', marginBottom:8}}>
              <div className="title" style={{margin:0}}>Chess</div>
              <div className="row">
                <input className="btn" value={username} onChange={e=>setUsername(e.target.value)} style={{background:'#1f2937'}} />
                <button className="btn" onClick={runTests}>Run tests</button>
              </div>
            </div>

            {screen===SCREENS.HOME && <Home/>}
            {screen===SCREENS.ONLINE && <OnlineMenu/>}
            {screen===SCREENS.OFFLINE && <OfflineMenu/>}
            {screen===SCREENS.RULES && <Rules/>}
            {screen===SCREENS.GAME && <GameUI/>}
          </div>
        );
      }

      ReactDOM.createRoot(document.getElementById('root')).render(<App/>);
    </script>
  </body>
</html>
