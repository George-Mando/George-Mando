<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>XenClipse Studios — Control Panel</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
html,body{background:#000;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:16px}
.xp{background:#000;font-family:'Share Tech Mono',monospace;color:#00e5ff;padding:14px;border:1px solid #00e5ff33;border-radius:10px;width:100%;max-width:700px;position:relative;overflow:hidden}
.xp::before{content:'';position:absolute;top:0;left:0;right:0;bottom:0;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,229,255,0.012) 2px,rgba(0,229,255,0.012) 4px);pointer-events:none;z-index:0}
.xp>*{position:relative;z-index:1}
.xp-top{display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #00e5ff22;padding-bottom:10px;margin-bottom:10px;gap:8px;flex-wrap:wrap}
.xp-logo{display:flex;align-items:center;gap:10px}
.xp-eclipse{width:40px;height:40px;border-radius:50%;background:#000;border:2.5px solid #00e5ff;position:relative;overflow:hidden;flex-shrink:0}
.xp-eclipse::after{content:'';position:absolute;width:34px;height:34px;background:#ff6b00;border-radius:50%;top:-5px;right:-9px}
.xp-eclipse::before{content:'';position:absolute;width:30px;height:30px;background:#000;border-radius:50%;top:-3px;right:-5px;z-index:2}
.xp-brand{font-family:'Orbitron',monospace;font-size:15px;font-weight:900;letter-spacing:3px;color:#00e5ff}
.xp-sub{font-size:9px;color:#00e5ff55;letter-spacing:4px;margin-top:2px}
.xp-status{display:flex;gap:10px;align-items:center}
.xp-dot{width:7px;height:7px;border-radius:50%;background:#00ff88;animation:xblink 1.8s ease-in-out infinite}
.xp-dot.warn{background:#ff6b00;animation-delay:0.6s}
.xp-dot.err{background:#ff2244;animation-delay:1.2s}
@keyframes xblink{0%,100%{opacity:1}50%{opacity:0.15}}
.xp-sysline{font-size:9px;color:#00e5ff44;letter-spacing:1px}
.xp-body{display:grid;grid-template-columns:165px 1fr 165px;gap:8px}
@media(max-width:600px){.xp-body{grid-template-columns:1fr}}
.xp-side{display:flex;flex-direction:column;gap:7px}
.xp-panel{background:#000;border:1px solid #00e5ff22;border-radius:5px;padding:9px;position:relative;overflow:hidden}
.xp-panel::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,#00e5ff44,transparent)}
.xp-panel-title{font-size:8px;color:#00e5ff44;letter-spacing:3px;margin-bottom:7px;text-transform:uppercase}
.xp-center{display:flex;flex-direction:column;gap:7px}
.xp-hud-top{border:1px solid #00e5ff22;border-radius:5px;padding:0;overflow:hidden;position:relative}
.xp-hud-top::after{content:'XENCLIPSE';position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);font-family:'Orbitron',monospace;font-size:32px;font-weight:900;color:#00e5ff05;letter-spacing:10px;white-space:nowrap;pointer-events:none}
.xp-stats-row{display:grid;grid-template-columns:repeat(3,1fr);gap:6px}
.xp-stat{border:1px solid #00e5ff22;border-radius:5px;padding:9px;text-align:center}
.xp-stat-val{font-family:'Orbitron',monospace;font-size:20px;font-weight:700;color:#00e5ff}
.xp-stat-val.orange{color:#ff6b00}
.xp-stat-val.green{color:#00ff88}
.xp-stat-label{font-size:8px;color:#00e5ff44;letter-spacing:2px;margin-top:3px}
.xp-games-row{display:grid;grid-template-columns:repeat(3,1fr);gap:5px}
.xp-game-cell{border:1px solid #00e5ff15;border-radius:3px;overflow:hidden}
.xp-game-label{font-size:7px;color:#00e5ff44;letter-spacing:1px;text-align:center;padding:3px;background:#000;border-bottom:1px solid #00e5ff11}
canvas{display:block;width:100%;image-rendering:pixelated;image-rendering:crisp-edges}
.xp-bio-bar{display:flex;align-items:center;gap:7px;margin-bottom:5px}
.xp-bio-label{font-size:8px;color:#00e5ff55;width:40px;flex-shrink:0}
.xp-bio-track{flex:1;height:4px;background:#00e5ff0d;border-radius:2px;overflow:hidden}
.xp-bio-fill{height:100%;border-radius:2px;transition:width 0.8s ease}
.xp-term{background:#000;border:1px solid #00e5ff15;border-radius:5px;padding:8px;height:74px;overflow:hidden}
.xp-term-line{font-size:8px;line-height:1.7;white-space:nowrap;overflow:hidden;color:#00e5ff44}
.xp-term-line.active{color:#00ff88}
.xp-term-cursor{display:inline-block;width:6px;height:9px;background:#00ff88;animation:xblink 1s step-end infinite;vertical-align:middle}
.hex-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:2px}
.hex{aspect-ratio:1;clip-path:polygon(50% 0%,100% 25%,100% 75%,50% 100%,0% 75%,0% 25%);transition:background 0.4s}
.xp-scrollticker{overflow:hidden;white-space:nowrap;border-top:1px solid #00e5ff11;padding-top:6px;margin-top:8px}
.xp-scrollticker-inner{display:inline-block;font-size:8px;color:#00e5ff2e;letter-spacing:2px;animation:xtick 24s linear infinite}
@keyframes xtick{from{transform:translateX(700px)}to{transform:translateX(-100%)}}
.stack-grid{display:grid;grid-template-columns:1fr 1fr;gap:3px}
.stack-badge{font-size:7px;padding:3px 4px;border:1px solid #00e5ff2a;border-radius:2px;color:#00e5ff66;text-align:center;letter-spacing:1px}
</style>
</head>
<body>
<div class="xp">
  <div class="xp-top">
    <div class="xp-logo">
      <div class="xp-eclipse"></div>
      <div>
        <div class="xp-brand">XENCLIPSE</div>
        <div class="xp-sub">STUDIOS // CONTROL PANEL v2.4</div>
      </div>
    </div>
    <div class="xp-sysline" id="clock">SYS-TIME: --:--:--</div>
    <div class="xp-status">
      <div class="xp-dot"></div>
      <div class="xp-dot warn"></div>
      <div class="xp-dot err"></div>
    </div>
  </div>

  <div class="xp-body">
    <div class="xp-side">
      <div class="xp-panel">
        <div class="xp-panel-title">// BIOSCAN</div>
        <canvas id="radarCv" width="147" height="120"></canvas>
      </div>
      <div class="xp-panel">
        <div class="xp-panel-title">// SYSTEMS</div>
        <div class="xp-bio-bar"><div class="xp-bio-label">ENGINE</div><div class="xp-bio-track"><div class="xp-bio-fill" id="b1" style="width:92%;background:#00e5ff"></div></div></div>
        <div class="xp-bio-bar"><div class="xp-bio-label">RENDER</div><div class="xp-bio-track"><div class="xp-bio-fill" id="b2" style="width:78%;background:#00ff88"></div></div></div>
        <div class="xp-bio-bar"><div class="xp-bio-label">AI/ML</div><div class="xp-bio-track"><div class="xp-bio-fill" id="b3" style="width:65%;background:#ff6b00"></div></div></div>
        <div class="xp-bio-bar"><div class="xp-bio-label">NET</div><div class="xp-bio-track"><div class="xp-bio-fill" id="b4" style="width:88%;background:#00e5ff"></div></div></div>
        <div class="xp-bio-bar"><div class="xp-bio-label">AUDIO</div><div class="xp-bio-track"><div class="xp-bio-fill" id="b5" style="width:55%;background:#ff6b00"></div></div></div>
      </div>
      <div class="xp-panel">
        <div class="xp-panel-title">// HEX MAP</div>
        <div class="hex-grid" id="hexGrid"></div>
      </div>
    </div>

    <div class="xp-center">
      <div class="xp-hud-top">
        <canvas id="mainCv" width="326" height="130"></canvas>
      </div>
      <div class="xp-stats-row">
        <div class="xp-stat"><div class="xp-stat-val">247</div><div class="xp-stat-label">// COMMITS</div></div>
        <div class="xp-stat"><div class="xp-stat-val orange">14</div><div class="xp-stat-label">// STREAK</div></div>
        <div class="xp-stat"><div class="xp-stat-val green">8</div><div class="xp-stat-label">// REPOS</div></div>
      </div>
      <div class="xp-games-row">
        <div class="xp-game-cell"><div class="xp-game-label">INVADERS</div><canvas id="g1" width="104" height="84"></canvas></div>
        <div class="xp-game-cell"><div class="xp-game-label">PAC-MAN</div><canvas id="g2" width="104" height="84"></canvas></div>
        <div class="xp-game-cell"><div class="xp-game-label">ASTEROIDS</div><canvas id="g3" width="104" height="84"></canvas></div>
      </div>
      <div class="xp-term" id="termPanel">
        <div class="xp-term-line">&gt; XENCLIPSE STUDIOS BOOT SEQUENCE...</div>
        <div class="xp-term-line">&gt; C++ v17 COMPILER: ACTIVE</div>
        <div class="xp-term-line active">&gt; GEORGE_MANDO.exe LOADED — READY<span class="xp-term-cursor"></span></div>
      </div>
    </div>

    <div class="xp-side">
      <div class="xp-panel">
        <div class="xp-panel-title">// SKILL MATRIX</div>
        <canvas id="skillCv" width="147" height="140"></canvas>
      </div>
      <div class="xp-panel">
        <div class="xp-panel-title">// WAVEFORM</div>
        <canvas id="waveCv" width="147" height="52"></canvas>
      </div>
      <div class="xp-panel">
        <div class="xp-panel-title">// STACK</div>
        <div class="stack-grid" id="stackBadges"></div>
      </div>
    </div>
  </div>

  <div class="xp-scrollticker">
    <div class="xp-scrollticker-inner">XENCLIPSE STUDIOS // GEORGE MANDO // C++ // UNREAL ENGINE 5 // UNITY // GAME DEVELOPER // SYSTEMS ARCHITECT // BLUEPRINT GENERATOR ACTIVE // DR.MARIO BUILD 3 ONLINE // OPEN TO WORK // XENCLIPSE STUDIOS // GEORGE MANDO // C++ //</div>
  </div>
</div>

<script>
const cyan='#00e5ff',orange='#ff6b00',green='#00ff88';
function clock(){const n=new Date(),p=v=>String(v).padStart(2,'0');document.getElementById('clock').textContent=`SYS-TIME: ${p(n.getHours())}:${p(n.getMinutes())}:${p(n.getSeconds())} // SECTOR: 7G // CLEARANCE: ALPHA`;}
setInterval(clock,1000);clock();
const hexColors=['#00e5ff22','#00e5ff33','#00e5ff44','#ff6b0033','#ff6b0022','#00ff8822','#00ff8811','#00e5ff11','#00e5ff0a'];
const hexG=document.getElementById('hexGrid'),hexEls=[];
for(let i=0;i<30;i++){const h=document.createElement('div');h.className='hex';h.style.background=hexColors[Math.floor(Math.random()*hexColors.length)];hexG.appendChild(h);hexEls.push(h);}
setInterval(()=>{const i=Math.floor(Math.random()*hexEls.length);hexEls[i].style.background=hexColors[Math.floor(Math.random()*hexColors.length)];},100);
['C++','C#','UE5','UNITY','PYTHON','GIT','HLSL','BLUEPRINTS'].forEach(s=>{const d=document.createElement('div');d.className='stack-badge';d.textContent=s;document.getElementById('stackBadges').appendChild(d);});

(function radar(){
  const cv=document.getElementById('radarCv'),ctx=cv.getContext('2d');
  const W=147,H=120,cx=73,cy=60,R=50;
  let angle=0,blips=[];
  for(let i=0;i<6;i++)blips.push({a:Math.random()*Math.PI*2,r:Math.random()*R*0.85,life:0,max:60+Math.random()*60});
  setInterval(()=>{
    ctx.fillStyle='#000';ctx.fillRect(0,0,W,H);
    for(let i=5;i>=1;i--){ctx.strokeStyle=`rgba(0,229,255,${0.04+i*0.025})`;ctx.lineWidth=0.5;ctx.beginPath();ctx.arc(cx,cy,R*i/5,0,Math.PI*2);ctx.stroke();}
    ctx.strokeStyle='#00e5ff15';ctx.lineWidth=0.5;
    for(let a=0;a<Math.PI*2;a+=Math.PI/6){ctx.beginPath();ctx.moveTo(cx,cy);ctx.lineTo(cx+Math.cos(a)*R,cy+Math.sin(a)*R);ctx.stroke();}
    for(let i=24;i>=0;i--){const a=angle-i*0.035;ctx.strokeStyle=`rgba(0,229,255,${(24-i)*0.009})`;ctx.lineWidth=R;ctx.beginPath();ctx.moveTo(cx,cy);ctx.arc(cx,cy,R/2,a,a+0.035);ctx.stroke();}
    ctx.strokeStyle=cyan;ctx.lineWidth=1.5;ctx.beginPath();ctx.moveTo(cx,cy);ctx.lineTo(cx+Math.cos(angle)*R,cy+Math.sin(angle)*R);ctx.stroke();
    blips.forEach(b=>{b.life++;if(b.life>b.max){b.a=Math.random()*Math.PI*2;b.r=Math.random()*R*0.85;b.life=0;b.max=60+Math.random()*60;}
    let bx=cx+Math.cos(b.a)*b.r,by=cy+Math.sin(b.a)*b.r,fade=Math.min(1,(b.max-b.life)/18);
    ctx.fillStyle=`rgba(0,255,136,${fade*0.9})`;ctx.beginPath();ctx.arc(bx,by,2.5,0,Math.PI*2);ctx.fill();
    ctx.strokeStyle=`rgba(0,255,136,${fade*0.25})`;ctx.lineWidth=1;ctx.beginPath();ctx.arc(bx,by,5,0,Math.PI*2);ctx.stroke();});
    ctx.strokeStyle='#00e5ff55';ctx.lineWidth=1.5;ctx.beginPath();ctx.arc(cx,cy,R,0,Math.PI*2);ctx.stroke();
    ctx.fillStyle=cyan;ctx.beginPath();ctx.arc(cx,cy,3,0,Math.PI*2);ctx.fill();
    angle+=0.038;
  },36);
})();

(function main(){
  const cv=document.getElementById('mainCv'),ctx=cv.getContext('2d');
  const W=326,H=130;let t=0;
  const lines=[{color:cyan,amp:20,freq:0.038,speed:0.055,off:0},{color:orange,amp:11,freq:0.058,speed:0.085,off:2},{color:green,amp:7,freq:0.075,speed:0.048,off:4}];
  const parts=[];for(let i=0;i<25;i++)parts.push({x:Math.random()*W,y:Math.random()*H,vx:(Math.random()-0.5)*0.35,vy:(Math.random()-0.5)*0.25,s:Math.random()*1.5+0.4,a:Math.random()*0.25+0.04});
  setInterval(()=>{
    ctx.fillStyle='rgba(0,0,0,0.12)';ctx.fillRect(0,0,W,H);
    parts.forEach(p=>{p.x+=p.vx;p.y+=p.vy;if(p.x<0||p.x>W)p.vx*=-1;if(p.y<0||p.y>H)p.vy*=-1;ctx.fillStyle=`rgba(0,229,255,${p.a})`;ctx.fillRect(p.x,p.y,p.s,p.s);});
    lines.forEach((l,li)=>{
      ctx.strokeStyle=l.color;ctx.lineWidth=li===0?1.5:0.7;ctx.globalAlpha=li===0?0.9:0.45;
      ctx.beginPath();
      for(let x=0;x<W;x++){const y=H/2+Math.sin(x*l.freq+t*l.speed+l.off)*l.amp+Math.sin(x*l.freq*2.2+t*l.speed*0.65)*l.amp*0.38;x===0?ctx.moveTo(x,y):ctx.lineTo(x,y);}
      ctx.stroke();ctx.globalAlpha=1;
    });
    for(let i=0;i<W;i+=40){ctx.strokeStyle='#00e5ff0e';ctx.lineWidth=0.5;ctx.beginPath();ctx.moveTo(i,0);ctx.lineTo(i,H);ctx.stroke();}
    for(let j=0;j<H;j+=20){ctx.strokeStyle='#00e5ff08';ctx.lineWidth=0.5;ctx.beginPath();ctx.moveTo(0,j);ctx.lineTo(W,j);ctx.stroke();}
    ctx.strokeStyle='#00e5ff2a';ctx.lineWidth=1;ctx.strokeRect(0,0,W,H);
    t++;
  },28);
})();

(function skills(){
  const cv=document.getElementById('skillCv'),ctx=cv.getContext('2d');
  const W=147,H=140,cx=73,cy=72,R=52;
  const sk=[{n:'C++',v:0.9},{n:'UE5',v:0.82},{n:'UNITY',v:0.75},{n:'C#',v:0.7},{n:'PYTHON',v:0.6},{n:'SYS',v:0.85}];
  let t=0;
  setInterval(()=>{
    ctx.fillStyle='#000';ctx.fillRect(0,0,W,H);
    for(let r=1;r<=4;r++){ctx.strokeStyle=`rgba(0,229,255,${0.04+r*0.03})`;ctx.lineWidth=0.5;ctx.beginPath();ctx.arc(cx,cy,R*r/4,0,Math.PI*2);ctx.stroke();}
    const N=sk.length,wave=Math.sin(t*0.04)*0.05;
    const axes=sk.map((_,i)=>{const a=i*Math.PI*2/N-Math.PI/2;return{x:cx+Math.cos(a)*R,y:cy+Math.sin(a)*R,a};});
    axes.forEach((ax,i)=>{ctx.strokeStyle='#00e5ff15';ctx.lineWidth=0.5;ctx.beginPath();ctx.moveTo(cx,cy);ctx.lineTo(ax.x,ax.y);ctx.stroke();ctx.fillStyle='#00e5ff44';ctx.font='7px Share Tech Mono';ctx.textAlign='center';ctx.fillText(sk[i].n,ax.x+(ax.x-cx)*0.24,ax.y+(ax.y-cy)*0.24+2);});
    ctx.beginPath();
    sk.forEach((s,i)=>{const a=axes[i].a,rv=(s.v+wave)*R,px=cx+Math.cos(a)*rv,py=cy+Math.sin(a)*rv;i===0?ctx.moveTo(px,py):ctx.lineTo(px,py);});
    ctx.closePath();ctx.strokeStyle=cyan;ctx.lineWidth=1.5;ctx.stroke();ctx.fillStyle='rgba(0,229,255,0.08)';ctx.fill();
    sk.forEach((s,i)=>{const a=axes[i].a,rv=(s.v+wave)*R;ctx.fillStyle=cyan;ctx.beginPath();ctx.arc(cx+Math.cos(a)*rv,cy+Math.sin(a)*rv,2.5,0,Math.PI*2);ctx.fill();});
    t++;
  },48);
})();

(function wave(){
  const cv=document.getElementById('waveCv'),ctx=cv.getContext('2d');
  const W=147,H=52;let t=0;
  setInterval(()=>{ctx.fillStyle='#000';ctx.fillRect(0,0,W,H);[cyan,orange].forEach((c,ci)=>{ctx.strokeStyle=c;ctx.lineWidth=1;ctx.globalAlpha=ci===0?0.8:0.38;ctx.beginPath();for(let x=0;x<W;x++){const y=H/2+Math.sin(x*0.12+t*(ci===0?0.1:0.14)+ci*1.4)*11+Math.sin(x*0.24+t*0.07)*4;x===0?ctx.moveTo(x,y):ctx.lineTo(x,y);}ctx.stroke();ctx.globalAlpha=1;});t++;},28);
})();

(function termAnim(){
  const lines=['> XENCLIPSE STUDIOS — BOOT SEQUENCE','> C++ v17 COMPILER: ACTIVE','> UNREAL ENGINE 5.3: ONLINE','> BLUEPRINT_GENERATOR.dll LOADED','> GAMEPLAY_SYSTEMS: INITIALIZED','> GEORGE_MANDO: OPEN_TO_WORK = TRUE','> SCANNING FOR OPPORTUNITIES...','> XENCLIPSE STUDIOS — ALL SYSTEMS GO'];
  let idx=0;const term=document.getElementById('termPanel');
  setInterval(()=>{const rows=term.querySelectorAll('.xp-term-line');rows.forEach(r=>r.classList.remove('active'));const nl=document.createElement('div');nl.className='xp-term-line active';nl.innerHTML=`> ${lines[idx%lines.length]}<span class="xp-term-cursor"></span>`;if(rows.length>=4)term.removeChild(rows[0]);term.appendChild(nl);idx++;},1800);
})();

(function bars(){
  const ids=['b1','b2','b3','b4','b5'],bases=[92,78,65,88,55];
  setInterval(()=>{ids.forEach((id,i)=>{const el=document.getElementById(id),v=Math.max(15,Math.min(99,bases[i]+(Math.random()-0.5)*14));el.style.width=v+'%';});},900);
})();

(function invaders(){
  const cv=document.getElementById('g1'),ctx=cv.getContext('2d');
  const W=104,H=84;let f=0,dir=1,inv=[],bullets=[],px=44,pb=null;
  for(let r=0;r<2;r++)for(let c=0;c<5;c++)inv.push({x:8+c*18,y:10+r*15,alive:true});
  setInterval(()=>{
    ctx.fillStyle='#000';ctx.fillRect(0,0,W,H);f++;
    if(f%14===0){let edge=false;inv.forEach(i=>{if(i.alive){i.x+=dir*4;if(i.x>W-16||i.x<0)edge=true;}});if(edge){dir*=-1;inv.forEach(i=>{if(i.alive)i.y+=5;});}}
    inv.forEach(i=>{if(!i.alive)return;ctx.fillStyle=cyan;ctx.fillRect(i.x+2,i.y,9,3);ctx.fillRect(i.x,i.y+3,13,3);ctx.fillRect(i.x+2,i.y+6,4,2);ctx.fillRect(i.x+7,i.y+6,4,2);});
    if(Math.random()<0.04&&!pb){let al=inv.filter(i=>i.alive);if(al.length){let s=al[Math.floor(Math.random()*al.length)];bullets.push({x:s.x+6,y:s.y+9});}}
    bullets=bullets.filter(b=>{b.y+=3;ctx.fillStyle='#ff2244';ctx.fillRect(b.x,b.y,1.5,5);return b.y<H;});
    if(Math.random()<0.04&&!pb)pb={x:px+5,y:H-14};
    if(pb){pb.y-=4;ctx.fillStyle=green;ctx.fillRect(pb.x,pb.y,1.5,6);inv.forEach(i=>{if(i.alive&&pb&&Math.abs(pb.x-i.x-6)<7&&Math.abs(pb.y-i.y-4)<8){i.alive=false;pb=null;}});if(pb&&pb.y<0)pb=null;}
    px=48+Math.sin(f*0.05)*38;
    ctx.fillStyle=cyan;ctx.fillRect(px,H-12,18,4);ctx.fillRect(px+7,H-16,4,5);
    if(!inv.some(i=>i.alive)){inv=[];for(let r=0;r<2;r++)for(let c=0;c<5;c++)inv.push({x:8+c*18,y:10+r*15,alive:true});}
  },50);
})();

(function pacman(){
  const cv=document.getElementById('g2'),ctx=cv.getContext('2d');
  const W=104,H=84;let px=52,py=42,f=0;
  let ghosts=[{x:22,y:22,dx:1.2,dy:0.8,c:'#ff4444'},{x:82,y=62,dx:-1,dy:1.1,c:'#ff88ff'}];
  let dots=[];for(let r=0;r<5;r++)for(let c=0;c<8;c++)dots.push({x:8+c*11,y:13+r*14,e:false});
  setInterval(()=>{
    f++;ctx.fillStyle='#000';ctx.fillRect(0,0,W,H);
    dots.forEach(d=>{if(!d.e){ctx.fillStyle='#ffff0044';ctx.beginPath();ctx.arc(d.x,d.y,1.8,0,Math.PI*2);ctx.fill();if(Math.abs(px-d.x)<8&&Math.abs(py-d.y)<8)d.e=true;}});
    if(!dots.some(d=>!d.e))dots.forEach(d=>d.e=false);
    px+=Math.cos(f*0.042)*1.5;py+=Math.sin(f*0.032)*1.3;px=Math.max(9,Math.min(W-9,px));py=Math.max(9,Math.min(H-9,py));
    let m=Math.abs(Math.sin(f*0.2))*0.7;
    ctx.fillStyle='#ffff00';ctx.beginPath();ctx.moveTo(px,py);ctx.arc(px,py,7,m,Math.PI*2-m);ctx.closePath();ctx.fill();
    ghosts.forEach(g=>{g.x+=g.dx;g.y+=g.dy;if(g.x<9||g.x>W-9)g.dx*=-1;if(g.y<9||g.y>H-9)g.dy*=-1;ctx.fillStyle=g.c;ctx.beginPath();ctx.arc(g.x,g.y-1,7,Math.PI,0);ctx.rect(g.x-7,g.y-1,14,8);ctx.fill();ctx.fillStyle='#fff';ctx.beginPath();ctx.arc(g.x-2.5,g.y-1,2.5,0,Math.PI*2);ctx.arc(g.x+2.5,g.y-1,2.5,0,Math.PI*2);ctx.fill();ctx.fillStyle='#000';ctx.beginPath();ctx.arc(g.x-1.5,g.y-1,1.5,0,Math.PI*2);ctx.arc(g.x+3.5,g.y-1,1.5,0,Math.PI*2);ctx.fill();});
  },50);
})();

(function asteroids(){
  const cv=document.getElementById('g3'),ctx=cv.getContext('2d');
  const W=104,H=84;let ship={x:52,y=42,a:0,vx:0,vy:0},roids=[],bullets=[],f=0;
  function mkR(x,y,r){let pts=[];for(let i=0;i<7;i++){let a=i*Math.PI*2/7,d=r*(0.6+Math.random()*0.5);pts.push([Math.cos(a)*d,Math.sin(a)*d]);}return{x:x??Math.random()*W,y:y??Math.random()*H,vx:(Math.random()-0.5)*1.5,vy:(Math.random()-0.5)*1.5,r,rot:0,rv:(Math.random()-0.5)*0.05,pts};}
  for(let i=0;i<4;i++)roids.push(mkR());
  setInterval(()=>{
    f++;ctx.fillStyle='#000';ctx.fillRect(0,0,W,H);
    ship.vx+=Math.cos(ship.a)*0.08;ship.vy+=Math.sin(ship.a)*0.08;ship.vx*=0.98;ship.vy*=0.98;
    ship.x=(ship.x+ship.vx+W)%W;ship.y=(ship.y+ship.vy+H)%H;ship.a+=0.04;
    if(f%22===0)bullets.push({x:ship.x,y:ship.y,vx:Math.cos(ship.a)*5,vy:Math.sin(ship.a)*5,life:32});
    bullets=bullets.filter(b=>{b.x=(b.x+b.vx+W)%W;b.y=(b.y+b.vy+H)%H;b.life--;ctx.fillStyle='#ffff44';ctx.fillRect(b.x,b.y,2,2);roids=roids.filter(r=>{if(Math.hypot(b.x-r.x,b.y-r.y)<r.r){b.life=0;if(r.r>10){roids.push(mkR(r.x,r.y,r.r*0.55));roids.push(mkR(r.x,r.y,r.r*0.55));}return false;}return true;});return b.life>0;});
    roids.forEach(r=>{r.x=(r.x+r.vx+W)%W;r.y=(r.y+r.vy+H)%H;r.rot+=r.rv;ctx.strokeStyle='#88ffcc';ctx.lineWidth=1;ctx.beginPath();r.pts.forEach(([px,py],i)=>{let rx=Math.cos(r.rot)*px-Math.sin(r.rot)*py+r.x,ry=Math.sin(r.rot)*px+Math.cos(r.rot)*py+r.y;i===0?ctx.moveTo(rx,ry):ctx.lineTo(rx,ry);});ctx.closePath();ctx.stroke();});
    if(roids.length<3)roids.push(mkR());
    ctx.save();ctx.translate(ship.x,ship.y);ctx.rotate(ship.a);ctx.strokeStyle=cyan;ctx.lineWidth=1.2;ctx.beginPath();ctx.moveTo(9,0);ctx.lineTo(-6,5);ctx.lineTo(-4,0);ctx.lineTo(-6,-5);ctx.closePath();ctx.stroke();if(f%4<2){ctx.strokeStyle=orange;ctx.lineWidth=1;ctx.beginPath();ctx.moveTo(-4,0);ctx.lineTo(-11,0);ctx.stroke();}ctx.restore();
  },48);
})();
</script>
</body>
</html>
