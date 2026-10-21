[Uploading elfo_y_v67.html…]()
# elfo.html<!DOCTYPE html>
<html lang="en"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>NEON HARBOR</title>
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@500;700&family=Vazirmatn:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{--ink:#070b12;--cy:#36f1ff;--mg:#ff3d8b;--tx:#cfeaf0;--pn:rgba(7,13,24,.72)}
html,body{margin:0;height:100%;background:var(--ink);overflow:hidden;font-family:Rajdhani,'Segoe UI',system-ui,sans-serif;color:var(--tx)}
#gl{display:block;width:100%;height:100%}
.hud{position:fixed;pointer-events:none;background:var(--pn);border:1px solid rgba(54,241,255,.35);border-radius:6px;padding:6px 12px;font-size:18px}
#info{top:max(16px,env(safe-area-inset-top));right:16px;display:flex;gap:16px;align-items:center}
#clock{color:var(--cy);font-size:24px}#money{color:#9dffb0}
#mini{position:fixed;left:16px;bottom:max(16px,env(safe-area-inset-bottom));width:180px;height:180px;border:2px solid var(--cy);border-radius:50%;background:#0b1220;pointer-events:none}
#speed{right:16px;bottom:max(16px,env(safe-area-inset-bottom));width:132px;height:132px;padding:0;display:none;text-align:center}
#speed svg{position:absolute;inset:0;width:100%;height:100%}
#speed path{fill:none;stroke-width:6;stroke-linecap:round}
.bg{stroke:rgba(54,241,255,.15)}.fg{stroke:var(--cy);stroke-dasharray:226.2;stroke-dashoffset:226.2}
#speed div{position:absolute;inset:0;display:flex;flex-direction:column;justify-content:center}
#spd{font-size:40px;line-height:1}#speed small{opacity:.7}
#prompt{left:50%;bottom:22%;transform:translateX(-50%);display:none;color:var(--cy)}
#toast{left:50%;top:70px;transform:translateX(-50%);display:none;color:var(--mg)}
#fps{left:16px;top:16px;display:none;font-size:14px}
#screen{position:fixed;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:10px;background:rgba(5,8,16,.78);cursor:pointer;text-align:center}
#screen h1{margin:0;font-size:clamp(44px,9vw,92px);letter-spacing:.06em;color:var(--cy);text-shadow:0 0 28px rgba(54,241,255,.55),4px 4px 0 var(--mg)}
#sub{font-size:24px;margin:0 0 14px}
.keys{display:grid;grid-template-columns:auto auto;gap:4px 22px;text-align:left;font-size:18px}.keys b{color:var(--cy)}

#shop{display:none;position:fixed;right:18px;top:80px;width:min(330px,calc(100vw - 36px));max-height:78vh;overflow:auto;background:rgba(5,12,24,.96);border:1px solid var(--cy);border-radius:10px;padding:14px;z-index:5;box-shadow:0 0 24px #36f14422}
#shop h2{margin:0 0 8px;color:var(--cy)}#shop p{margin:5px 0 12px}
.shopgrid{display:grid;grid-template-columns:1fr 1fr;gap:7px}
#shop button{background:#101f30;color:#d8faff;border:1px solid #267b8a;padding:9px;border-radius:5px;font:inherit;cursor:pointer}
#shop button:hover{border-color:var(--cy);background:#17354a}
#wanted{color:#ffce54;letter-spacing:3px;font-size:21px}
#bars{top:68px;right:16px;width:210px;display:flex;flex-direction:column;gap:5px;font-size:15px}
.bar{height:9px;background:#0007;border:1px solid #fff4}.bar i{display:block;height:100%;width:100%}
#hbi{background:#d9302c}#abi{background:#d8dde6}#wp{color:#ffdca0;letter-spacing:.08em}
#obj{left:50%;bottom:max(12px,env(safe-area-inset-bottom));transform:translateX(-50%);color:#ffd24a;font-size:20px;white-space:nowrap}
#zone{position:fixed;right:24px;bottom:170px;font-size:clamp(34px,5vw,58px);font-weight:700;font-style:italic;text-transform:uppercase;color:#f0e2b0;text-shadow:2px 2px 0 #000,0 0 14px #000a;opacity:0;pointer-events:none}
@keyframes zn{0%{opacity:0;transform:translateY(12px)}12%,72%{opacity:1;transform:none}100%{opacity:0}}
#ovl{position:fixed;left:0;right:0;top:32%;text-align:center;display:none;pointer-events:none;z-index:6}
#ovl h2{margin:0;font-size:clamp(56px,12vw,150px);letter-spacing:.04em;font-style:italic;text-transform:uppercase;text-shadow:3px 3px 0 #000,0 0 30px #000}
#ovl p{margin:0;font-size:36px;color:#fff;text-shadow:2px 2px #000}
#hit{position:fixed;inset:0;pointer-events:none;background:radial-gradient(transparent 45%,rgba(200,0,0,.7));opacity:0}
#gl.dead{filter:grayscale(1) contrast(1.15)}
#skin{display:none;position:fixed;right:18px;top:80px;width:min(330px,calc(100vw - 36px));max-height:78vh;overflow:auto;background:rgba(5,12,24,.96);border:1px solid var(--cy);border-radius:10px;padding:14px;z-index:5}
#skin h2{margin:0 0 8px;color:var(--cy)}#skin p{margin:5px 0 12px}
#skin button{background:#101f30;color:#d8faff;border:1px solid #267b8a;padding:9px;border-radius:5px;font:inherit;cursor:pointer}#skin button:hover{border-color:var(--cy);background:#17354a}
#mapv{display:none;position:fixed;inset:0;z-index:4;background:rgba(4,8,16,.94);flex-direction:column;align-items:center;justify-content:center;gap:8px}
#mapc{border:2px solid var(--cy);cursor:crosshair;max-width:100%}#mapk{color:var(--cy);font-size:18px}#toast{z-index:7}
#vig{position:fixed;inset:0;pointer-events:none;background:radial-gradient(ellipse at center,transparent 58%,rgba(0,0,0,.42))}
#xh{position:fixed;left:50%;top:50%;width:14px;height:14px;margin:-7px;border:2px solid #fff;border-radius:50%;opacity:.8;pointer-events:none;display:none}
#gl{touch-action:none}
.mn{display:block;width:min(320px,80vw);margin:6px;padding:14px;font:700 24px Rajdhani,sans-serif;letter-spacing:.08em;color:var(--cy);background:#0b1626;border:1px solid var(--cy);border-radius:8px;cursor:pointer}.mn:hover{background:#16344a}
#set{display:none;position:fixed;inset:0;z-index:9;background:rgba(5,8,16,.92);align-items:center;justify-content:center}
.sb{width:min(560px,94vw);max-height:90vh;overflow:auto;background:rgba(5,12,24,.97);border:1px solid var(--cy);border-radius:10px;padding:14px;font-size:18px}
.sb h2,.sb h3{margin:6px 0;color:var(--cy)}.r{display:flex;justify-content:space-between;align-items:center;gap:10px;margin:6px 0}
.r button{background:#101f30;color:#d8faff;border:1px solid #267b8a;padding:7px 12px;border-radius:5px;font:inherit;cursor:pointer}.ch{font-size:14px;opacity:.85;margin:3px 0}.ch b{color:var(--mg)}
#mob{display:none;position:fixed;inset:0;z-index:10;pointer-events:none}
.mbt{position:absolute;transform:translate(-50%,-50%);border-radius:50%;background:#0b1626;border:2px solid var(--cy);color:var(--cy);text-align:center;font-weight:700;pointer-events:auto;touch-action:none;user-select:none}.mbt.on,.mbt.sel{background:var(--cy);color:#000}
#med{display:none;position:fixed;inset:0;z-index:9;background:rgba(5,8,16,.88);align-items:flex-end;justify-content:center}.lg{display:flex;flex-wrap:wrap;gap:2px 12px;font-size:13px;margin-top:6px}.lg b{color:var(--cy)}
#scope{display:none;position:fixed;inset:0;pointer-events:none;z-index:3;background:linear-gradient(#000,#000) center/1px 70% no-repeat,linear-gradient(#000,#000) center/70% 1px no-repeat,radial-gradient(circle at center,transparent 34%,#000 35%)}
body.nc,body.nc *{cursor:none!important}
body.fa,body.fa button,body.fa input,body.fa .mn{font-family:Vazirmatn,Tahoma,sans-serif!important}body.fa *{letter-spacing:0!important}body.fa .sb,body.fa #shop,body.fa #skin{direction:rtl;text-align:right}
</style></head><body>
<canvas id="gl"></canvas><canvas id="mini" width="200" height="200"></canvas><div id="vig"></div><div id="xh"></div>
<div id="info" class="hud"><b id="clock">09:00</b><span id="loc">Downtown</span><span id="wanted">☆☆☆☆☆</span><span id="money">$ 5,000</span></div>
<div id="shop"></div>
<div id="speed" class="hud"><svg viewBox="0 0 120 120"><path class="bg" d="M26.06 93.94A48 48 0 1 1 93.94 93.94"/><path id="arc" class="fg" d="M26.06 93.94A48 48 0 1 1 93.94 93.94"/></svg><div><b id="spd">0</b><small>km/h</small></div></div>
<div id="prompt" class="hud">Press F to enter vehicle</div><div id="toast" class="hud"></div><div id="fps" class="hud"></div>
<div id="bars" class="hud"><div id="wp">FIST</div><div class="bar"><i id="abi" style="width:0"></i></div><div class="bar"><i id="hbi"></i></div></div>
<div id="obj" class="hud"></div><div id="zone"></div><div id="hit"></div><div id="ovl"><h2 id="ot"></h2><p id="os"></p></div>
<div id="skin"></div><div id="mapv"><canvas id="mapc"></canvas><div id="mapk">M / Esc: close · Click the map to set a waypoint</div></div>
<div id="screen"><h1>NEON HARBOR</h1><p id="sub">GTA_elfo</p><button class="mn" id="bStart">Start GTA_elfo</button><button class="mn" id="bSet">Settings</button></div>
<div id="set"></div><div id="mob"></div><div id="med"></div><div id="scope"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
(()=>{'use strict';
const $=id=>document.getElementById(id);let Game;
/* ===== CONFIG ===== */
const C=Object.freeze({seed:1337,half:1250,zs:735,step:120,roadW:16,aveW:24,aves:[3,7],cell:40,walk:4,sprint:8,jump:7,grav:-22,pr:.5,enter:4,cycle:480,start:9,
 car:{max:55,acc:34,brake:45,drag:.06,roll:1.5,steer:.6,wb:2.6,grip:7,hb:1.1,rev:15},
 npc:{n:55,parked:35,cull:340,near:160,far:330,follow:15},
 cam:{fd:6,fh:2.2,cd:9,ch:3.5,fov:70,fovMax:85,idle:2},
 moto:{max:62,acc:42,brake:50,drag:.06,roll:1.5,steer:.8,wb:1.8,grip:9,hb:1.1,rev:8},
 ped:{n:36,cull:260,spread:300,hit:1.7},mis:{reward:1500,r:7}});
/* ===== UTILS ===== */
const U={rng(a){return()=>{a|=0;a=a+0x6D2B79F5|0;let t=Math.imul(a^a>>>15,1|a);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296}},
 clamp:(v,a,b)=>Math.min(b,Math.max(a,v)),lerp:(a,b,t)=>a+(b-a)*t,wrap:a=>Math.atan2(Math.sin(a),Math.cos(a)),
 lerpA:(a,b,t)=>a+U.wrap(b-a)*t,sm:(a,b,x)=>{x=U.clamp((x-a)/(b-a),0,1);return x*x*(3-2*x)}};
const WEAP={Pistol:{dmg:34,rate:.28,rng:60,pel:1,spr:.012,ammo:48,len:.34},SMG:{dmg:18,rate:.075,rng:55,pel:1,spr:.05,ammo:120,len:.5,auto:1},
 Shotgun:{dmg:16,rate:.8,rng:28,pel:7,spr:.12,ammo:24,len:.85},Rifle:{dmg:28,rate:.11,rng:90,pel:1,spr:.025,ammo:90,len:.95,auto:1},Sniper:{dmg:100,rate:1.2,rng:220,pel:1,spr:0,ammo:12,len:1.15}},GUNS=Object.keys(WEAP);
const SHOPS=[],SHOPDEF={gun:{name:'HARBOR ARMS',css:'#ff5a5a',col:0x7a2a2a},att:{name:'ATTACHMENT LAB',css:'#ffb84d',col:0x6a4a1a},car:{name:'PREMIUM MOTORS',css:'#4dffa0',col:0x1a5a3a},moto:{name:'TWO WHEELS',css:'#c77dff',col:0x4a2a6a},garage:{name:'ELFO GARAGE',css:'#ffe94d',col:0x5a5a1a},arena:{name:'CHALLENGE HALL',css:'#ff7a3d',col:0x6a2a14},air:{name:'AIRCRAFT DEALER',css:'#6ad0ff',col:0x2a6a9a},mil:{name:'MILITARY DEPOT',css:'#9bd15a',col:0x3a4a2a},skin:{name:'URBAN THREADS',css:'#4dd2ff',col:0x2a5a7a}},
LOTS={'9,5':'arena','0,3':'mil','5,5':'gun','2,8':'gun','6,4':'att','1,6':'att','3,3':'car','8,7':'car','4,7':'moto','7,4':'moto','6,6':'garage','2,2':'garage','8,3':'garage','3,6':'skin'};
const SKINS=[{n:'Harbor Blue',sh:0x2b6cff,pn:0x222a3a,sk:0xe0b090,price:0},{n:'Tourist',sh:0xf0a030,pn:0x6fa8ff,sk:0xe0b090,price:100},{n:'Street Red',sh:0xc0392b,pn:0x1a1a1a,sk:0xc68c62,price:150},
 {n:'Neon Punk',sh:0xff3d8b,pn:0x1b1030,sk:0xe0b090,price:250},{n:'Cyber Cyan',sh:0x36f1ff,pn:0x0a2a3a,sk:0x8d5a3b,price:300},{n:'Business',sh:0x20242c,pn:0x101216,sk:0xf1cfb0,price:350},
 {n:'Tactical',sh:0x3d4a3a,pn:0x2a2f26,sk:0xc68c62,price:400},{n:'Gold Suit',sh:0xe8c547,pn:0x2a2a2a,sk:0x8d5a3b,price:500}];
const MAPLBL=[['HARBOR DOCKS',0,570],['GREENFIELD PARK',360,-300],['DOWNTOWN',0,-170],['WESTGATE',-420,-60],['EASTSIDE',420,200],['CENTRAL PLAZA',-60,78],['AIRPORT',0,-630],['NORTH HIGHLANDS',0,-1000],['EAST OUTSKIRTS',950,-250],['WEST OUTSKIRTS',-950,-250],['RING HIGHWAY',1150,-700]];
const POI=[],EMPTY=[],CIRC=[-1.3,0,1.3],NOKEY={};
const MAG={Pistol:12,SMG:30,Shotgun:6,Rifle:30,Sniper:5},RL={Pistol:1.2,SMG:1.5,Shotgun:2.1,Rifle:1.8,Sniper:2.3},
ATT=[['sil','Suppressor',400],['stock','Stock',300],['long','Long barrel',500],['short','Short barrel',350],['scp','Scope (aim: RMB / Z)',600],['mag','Extended magazine',450]];
/* d=[length,width,roof,hood,deck,windshieldBase,roofFront,roofRear,deckStart] */
const CARMODELS={Sedan:{n:'Classic Sedan',p:2500,c:0x2c7be5,mx:1,ac:1,d:[4.4,1.8,1.35,.85,.95,.6,-.2,-.7,-1.5]},
 Muscle:{n:'Ford Mustang GT',p:4500,c:0x1f3d9c,mx:1.15,ac:1.2,d:[4.8,1.95,1.3,.95,1,.5,-.3,-1.2,-1.9]},
 SUV:{n:'Range SUV',p:4000,c:0x222222,mx:1,ac:1,d:[4.8,2,1.85,1.2,1.65,1.1,.3,-2.1,-2.2]},
 Porsche:{n:'Porsche 911',p:8000,c:0xc9ccd4,mx:1.25,ac:1.3,d:[4.5,1.85,1.3,.85,1,.65,-.2,-1.1,-1.8]},
 Pickup:{n:'Ford F-150 Pickup',p:5000,c:0xb8402a,mx:1,ac:1.05,d:[5.4,2,1.9,1.25,1.15,1.2,.5,-.5,-.55]},
 Van:{n:'Mercedes Sprinter Van',p:4200,c:0xe8e8e8,mx:.95,ac:.95,d:[5.2,2,2.2,1.3,2.1,1.7,1.3,-2.5,-2.55]},
 Taxi:{n:'City Taxi',p:2600,c:0xf2c200,mx:1,ac:1,d:[4.4,1.8,1.35,.85,.95,.6,-.2,-.7,-1.5]},
 BMW:{n:'BMW M3',p:6500,c:0xf0f0f4,mx:1.2,ac:1.25,d:[4.7,1.9,1.38,.9,1,.7,-.3,-1.2,-1.7]},
 GWagon:{n:'Mercedes G63',p:12000,c:0x111111,mx:1.1,ac:1.1,d:[4.7,2,1.95,1.2,1.75,.9,.2,-2.1,-2.2]},
 Corvette:{n:'Chevrolet Corvette',p:9000,c:0xc83a12,mx:1.3,ac:1.35,sp:1,d:[4.6,1.95,1.18,.75,.92,.7,-.1,-.95,-1.65]},
 McLaren:{n:'McLaren P1',p:22000,c:0xff6a00,mx:1.45,ac:1.55,sp:1,d:[4.6,2,1.12,.66,.88,.9,-.1,-1.1,-1.75]},
 Bugatti:{n:'Bugatti Chiron',p:30000,c:0x123a9a,mx:1.6,ac:1.6,sp:1,d:[4.7,2,1.2,.8,.98,.75,-.2,-1,-1.7]},
 Ferrari:{n:'Ferrari 488',p:14000,c:0xd10000,mx:1.32,ac:1.4,sp:1,d:[4.5,1.95,1.2,.78,.95,.75,-.1,-.9,-1.6]},
 Police2:{n:'Muscle Racer',p:7000,c:0x6a1fb0,mx:1.3,ac:1.35,sp:1,d:[4.8,1.95,1.25,.9,1,.55,-.3,-1.2,-1.9]},Hatch:{n:'City Hatchback',p:1800,c:0x22aa66,mx:.95,ac:1,d:[3.9,1.7,1.4,.8,.9,.55,-.1,-.5,-1.3]},Limo:{n:'Stretch Limo',p:9500,c:0x0a0a0a,mx:1,ac:.9,d:[6.4,2,1.4,.9,1,.6,-.3,-2.4,-2.9]},Revuelto:{n:'Lamborghini Revuelto',p:260000,c:0x121216,lx(L,w,H,hh,dh,B,C){const W=[1,1,1],R=[1,.05,.05],O=[1,.5,.05],o=[];for(const s of[1,-1])o.push(B(.85,.05,.07,s*.62,hh-.28,L/2+.05,W,0,0,-s*.28),B(.45,.05,.07,s*.3,hh-.46,L/2+.05,W,0,0,s*.75),B(.3,.04,.07,s*.78,hh-.4,L/2+.05,O));o.push(B(w-.45,.07,.07,0,dh-.08,-L/2-.05,R),B(.5,.1,.07,.55,dh-.22,-L/2-.05,R),B(.5,.1,.07,-.55,dh-.22,-L/2-.05,R));return o},mx:1.55,ac:1.6,sp:1,d:[4.95,2.03,1.14,.7,.82,.45,-.2,-1.15,-1.8],ex(P,bx,K,ch,L,w,H,hh,dh,gc,z1){P.push(bx(w*.5,.03,1.1,0,hh+.01,L/2-1.3,[.1,.1,.12]),bx(.5,.04,.9,.5,dh+.02,-L/2+.8,[.1,.1,.12]),bx(.5,.04,.9,-.5,dh+.02,-L/2+.8,[.1,.1,.12]),bx(w-.2,.08,.5,0,gc+.05,-L/2+.1,K))}},
RevueltoSV:{n:'Lamborghini Revuelto SV',p:340000,c:0xc4161c,lx(L,w,H,hh,dh,B,C){const W=[1,1,1],R=[1,.05,.05],O=[1,.5,.05],o=[];for(const s of[1,-1])o.push(B(.85,.05,.07,s*.62,hh-.28,L/2+.05,W,0,0,-s*.28),B(.45,.05,.07,s*.3,hh-.46,L/2+.05,W,0,0,s*.75),B(.3,.04,.07,s*.78,hh-.4,L/2+.05,O));o.push(B(w-.45,.07,.07,0,dh-.08,-L/2-.05,R),B(.5,.1,.07,.55,dh-.22,-L/2-.05,R),B(.5,.1,.07,-.55,dh-.22,-L/2-.05,R));return o},mx:1.7,ac:1.75,sp:1,d:[4.95,2.03,1.14,.7,.82,.45,-.2,-1.15,-1.8],ex(P,bx,K,ch,L,w,H,hh,dh,gc,z1,z2,z3){const B=[.03,.03,.04];P.push(bx(w*.78,.035,1.5,0,hh+.02,L/2-1.5,B),bx(w*.62,.04,(z2-z3)*.9,0,H+.01,(z2+z3)/2,B),bx(w+.15,.06,.55,0,dh+.62,-L/2+.05,B),bx(.05,.5,.55,w/2+.07,dh+.4,-L/2+.05,B),bx(.05,.5,.55,-w/2-.07,dh+.4,-L/2+.05,B),bx(.08,.5,.08,.6,dh+.3,-L/2+.1,B),bx(.08,.5,.08,-.6,dh+.3,-L/2+.1,B),bx(w-.2,.08,.5,0,gc+.05,-L/2+.1,B))}},
Ferrari12:{n:'Ferrari 12Cilindri',p:420000,c:0xb3111a,lx(L,w,H,hh,dh,B,C){const W=[1,1,1],R=[1,.05,.05],o=[];for(const s of[1,-1])o.push(B(.75,.05,.07,s*.68,hh-.3,L/2+.04,W,0,0,s*.12),B(.5,.03,.07,s*.7,hh-.38,L/2+.04,W,0,0,s*.12),C(.15,.07,s*.55,dh-.14,-L/2-.05,R),C(.15,.07,s*.85,dh-.14,-L/2-.05,R));return o},mx:1.6,ac:1.5,sp:0,d:[4.73,1.94,1.29,.78,.88,.32,-.55,-1.25,-1.85],ex(P,bx,K,ch,L,w,H,hh,dh,gc,z1,z2,z3){const B=[.03,.03,.04];P.push(bx(w*.5,.03,1.2,0,hh+.015,L/2-1.2,B),bx(w*.6,.04,(z2-z3)*.85,0,H+.01,(z2+z3)/2,B),bx(w-.3,.05,.3,0,dh+.06,-L/2+.2,B))}},
JeepCJ:{n:'Classic Off-road Jeep CJ',p:9000,c:0xd0262b,lx(L,w,H,hh,dh,B,C){const W=[1,1,.9],R=[1,.05,.05],o=[];for(const s of[1,-1])o.push(C(.22,.1,s*.62,hh-.35,L/2+.05,W),C(.09,.1,s*.3,.62,L/2+.28,W),B(.14,.1,.06,s*.7,dh-.12,-L/2-.06,R));for(let i=-2;i<=2;i++)o.push(C(.09,.1,i*.22,H+.14,.7,W));return o},mx:1,ac:1.1,sp:0,d:[3.7,1.75,1.4,1,1.08,.55,.45,-1.55,-1.75],ex(P,bx,K,ch,L,w,H,hh,dh,gc){P.push(bx(w-.3,.1,.1,0,gc+.62,L/2+.2,ch),bx(.1,.5,.1,.5,gc+.4,L/2+.15,ch),bx(.1,.5,.1,-.5,gc+.4,L/2+.15,ch),bx(.1,.1,.1,.0,gc+.4,L/2+.15,ch),bx(.08,.65,.08,w/2-.1,H+.1,-1.55,K),bx(.08,.65,.08,-w/2+.1,H+.1,-1.55,K),bx(w-.2,.08,.08,0,H+.42,-1.55,K),{g:new THREE.CylinderGeometry(.36,.36,.26,14).rotateX(Math.PI/2).translate(0,.95,-L/2-.2),c:K},bx(w+.2,.08,.2,0,gc+.1,L/2+.05,K))}},
Jeep:{n:'Off-road Jeep',p:3500,c:0x4a6b2a,mx:.95,ac:1.05,d:[4.1,1.9,1.85,1.15,1.6,.95,.3,-1.9,-2]},Coupe:{n:'Sport Coupe',p:5500,c:0x8a1ab5,mx:1.12,ac:1.18,d:[4.3,1.8,1.25,.8,.9,.55,-.3,-1,-1.6]},Wagon:{n:'Family Wagon',p:2800,c:0x556b7a,mx:.95,ac:.95,d:[4.9,1.85,1.45,.85,1.1,.7,-.1,-2,-2.3]},Minibus:{n:'City Minibus',p:3800,c:0xf0f0f0,mx:.9,ac:.9,d:[5,2,2.1,1.2,2,1.5,1,-2.3,-2.4]},Lowrider:{n:'Lowrider Cruiser',p:6000,c:0xd4a017,mx:.9,ac:1,d:[5.2,1.95,1.25,.8,.9,.6,-.2,-1.5,-2.2]},Roadster:{n:'Roadster GT',p:11000,c:0xe01070,mx:1.28,ac:1.35,sp:1,d:[3.9,1.75,1.1,.7,.85,.4,-.1,-.8,-1.4]},Lambo:{n:'Lamborghini Aventador',p:18000,c:0xf2c200,mx:1.4,ac:1.5,sp:1,d:[4.8,2.05,1.14,.68,.9,.95,-.05,-1.1,-1.8]}},
MOTOS={Scooter:{n:'City Scooter',p:600,c:0xe8e8e8,mx:.75,ac:.8,sc:[.9,.9,.9]},Naked:{n:'Street Naked',p:1500,c:0x2ecc71,mx:1,ac:1},Chopper:{n:'Harley Chopper',p:3000,c:0x111111,mx:.95,ac:1,sc:[1,1,1.2]},
 Dirt:{n:'Dirt Bike',p:1200,c:0xff8a00,mx:.9,ac:1.1,sc:[.9,1,.95]},Cafe:{n:'Triumph Cafe Racer',p:2800,c:0x3a4a3a,mx:1,ac:1.1},Hayabusa:{n:'Suzuki Hayabusa',p:9000,c:0x222a55,mx:1.5,ac:1.6},Ducati:{n:'Ducati Panigale',p:4000,c:0xd10000,mx:1.2,ac:1.3},Ninja:{n:'Kawasaki Ninja H2',p:7500,c:0x18c93a,mx:1.35,ac:1.5}},NPCM=['Sedan','Muscle','SUV','Porsche','Pickup','Van','BMW','Taxi','Corvette','Hatch','Jeep','Coupe','Wagon','Minibus','Lowrider','Roadster','JeepCJ','Ferrari12','RevueltoSV','RevueltoBlack'];
CARMODELS.RevueltoBlack={...CARMODELS.RevueltoSV,n:'Lamborghini Revuelto (Matte Black)',c:0x0a0a0c,p:360000};CARMODELS.StealthGT={n:'Stealth GT (Matte Black)',p:45000,c:0x0b0b0e,mx:1.5,ac:1.55,sp:1,d:[4.8,2.02,1.12,.68,.85,.5,-.2,-1.1,-1.8]};
MOTOS.Vario={n:'Honda Vario (Black/Gold)',p:2400,c:0x0e0e10,mx:.95,ac:1,sc:[.95,.95,.95]};
Object.assign(MOTOS.Scooter,{nk:.7,fc:0x99ddff,dust:.8});Object.assign(MOTOS.Naked,{nk:1,fc:0xffa030,dust:1});Object.assign(MOTOS.Cafe,{nk:1,fc:0xffd060,dust:1});Object.assign(MOTOS.Dirt,{nk:1.1,fc:0xff7a20,dust:2.2});Object.assign(MOTOS.Chopper,{nk:.9,fc:0xff4020,dust:1.3});Object.assign(MOTOS.Ducati,{nk:1.2,fc:0xff3030,dust:.9});Object.assign(MOTOS.Ninja,{nk:1.35,fc:0x33ff77,dust:.9});Object.assign(MOTOS.Hayabusa,{nk:1.5,fc:0xaa55ff,dust:1});
const ld=(k,d)=>{try{return{...d,...JSON.parse(localStorage.getItem(k))}}catch(e){return d}},sv=(k,v)=>{try{localStorage.setItem(k,JSON.stringify(v))}catch(e){}},kn=c=>c.replace(/^Key|^Digit/,'');
const S=ld('gtaelfo_s',{mode:'pc',q:'high',vol:.8,fov:70,sens:1,fps:false,lang:'en'}),KB=ld('gtaelfo_k',{}),MBL=ld('gtaelfo_m',{});
const FAX={'ON':'روشن','OFF':'خاموش','Back':'بازگشت','Reset':'بازنشانی','Done':'تمام','Close':'بستن','Left':'چپ','Right':'راست','Forward':'جلو','Horn':'بوق','Punch':'مشت','Map':'نقشه','Shop':'شاپ','Pause':'توقف','Language':'زبان','Fullscreen':'تمام‌صفحه','Size':'اندازه','Armor':'زره','Medkit':'کمک‌های اولیه','Settings':'تنظیمات','Controls':'کنترل‌ها','Pistol':'تپانچه','SMG':'مسلسل SMG','Shotgun':'شاتگان','Rifle':'تفنگ تهاجمی','Sniper':'اسنایپر','Stock':'قنداق','Low':'پایین','Medium':'متوسط'};
const FA={'City posters (up to 5, any image size)':'پوسترهای شهر (تا ۵ عدد، هر سایز)','City posters':'پوسترهای شهر','Poster':'پوستر','Clear':'پاک کردن','Interact / talk':'تعامل / صحبت','Edit':'ویرایش','Posters appear on billboards along the city roads.':'پوسترها روی بیلبوردهای کنار خیابان‌ها نمایش داده می‌شن.','Start GTA_elfo':'شروع GTA_elfo','Resume GTA_elfo':'ادامه GTA_elfo','Paused':'مکث','SETTINGS':'تنظیمات','Control mode':'حالت کنترل','PC (default)':'کامپیوتر (پیش‌فرض)','MOBILE':'موبایل','Edit keys':'ویرایش کلیدها','Edit touch layout':'ویرایش چیدمان لمسی','Graphics quality':'کیفیت گرافیک','High (native pixels)':'بالا (پیکسل اصلی)','Ultra (1px, supersampled)':'اولترا (دقت ۱ پیکسل)','Field of view':'میدان دید','Master volume':'صدای کلی','Mouse / touch sensitivity':'حساسیت موس / لمس','Show FPS':'نمایش FPS','Camera view':'نمای دوربین','First person':'اول‌شخص','Third person':'سوم‌شخص','Cheat codes (type during play)':'کدهای تقلب (حین بازی تایپ کن)','PC KEYS — click an action, then press the new key':'کلیدهای کامپیوتر — روی یک عمل کلیک کن و کلید جدید را بزن','Restore defaults':'بازگرداندن پیش‌فرض','press a key…':'یک کلید بزن…',
'Back / brake':'عقب / ترمز','Sprint / Nitro':'دویدن / نیترو','Jump / handbrake':'پرش / ترمز دستی','Enter / exit vehicle':'سوار / پیاده شدن','Reload / Radio':'ریلود / رادیو','Reload / radio':'ریلود / رادیو','Shoot':'شلیک','Switch weapon':'تعویض سلاح','C4 place / detonate':'کار گذاشتن / منفجر کردن C4','C4 place / blow':'C4 کار بگذار / منفجر کن','Aim / Scope':'نشانه‌گیری / اسکوپ','Aim / scope':'نشانه‌گیری / اسکوپ','Air-suspension hop':'پرش تعلیق بادی','Forward / accelerate':'جلو / گاز',
'drag any button to move it':'هر دکمه را بکش تا جابه‌جا شود','Opacity %':'شفافیت ٪','Reset layout':'بازنشانی چیدمان',
'Infinite health (toggle)':'جان بی‌نهایت (روشن/خاموش)','Infinite money':'پول بی‌نهایت','All weapons + ammo':'همه سلاح‌ها + مهمات','Armor + full health':'زره + جان کامل','Clear wanted level':'پاک کردن ستاره‌ها','Wanted +2':'۲ ستاره بیشتر','Spawn Lamborghini':'ساخت لامبورگینی','Spawn Ferrari':'ساخت فراری','Full nitro (in vehicle)':'نیترو کامل','Blow up nearby cars':'منفجر کردن ماشین‌های اطراف','Unlimited upgrades (garage limits removed)':'ارتقای نامحدود (حذف محدودیت گاراژ)','Hyper-tune current vehicle + 9999 NOS':'تیون شدید ماشین فعلی + ۹۹۹۹ نیترو',
'HARBOR ARMS — weapons':'اسلحه‌فروشی — سلاح‌ها','ATTACHMENT LAB':'آزمایشگاه اتچمنت','PREMIUM MOTORS — cars':'نمایشگاه ماشین','TWO WHEELS — bikes':'نمایشگاه موتور','ELFO GARAGE — tuning':'گاراژ الفو — تیونینگ','CHALLENGE HALL — win cash':'سالن چالش — پول ببر','B closes.':'B برای بستن.',
'Ammo (equipped gun)':'مهمات (سلاح فعلی)','Armor plating':'زره‌پوش ماشین','Suppressor':'صداخفه‌کن','Long barrel':'لوله بلند','Short barrel':'لوله کوتاه','Scope (aim: RMB / Z)':'اسکوپ (نشانه: کلیک راست / Z)','Extended magazine':'خشاب بزرگ‌تر','Buy and equip a gun first.':'اول یک اسلحه بخر و بردار.','Nitro refill +100':'شارژ نیترو +۱۰۰','hold Shift':'نگه‌داشتن Shift','Engine / top speed':'موتور / سرعت','Handling / steering':'فرمان‌پذیری','Tires & brakes':'لاستیک و ترمز','Lv ':'سطح ','Spring height ▼ lower':'ارتفاع فنر ▼ پایین','Spring height ▲ raise':'ارتفاع فنر ▲ بالا','Wheel size ▼ smaller':'سایز چرخ ▼ کوچک‌تر','Wheel size ▲ bigger':'سایز چرخ ▲ بزرگ‌تر','Air suspension (V = hop)':'تعلیق بادی (V = پرش)','Air suspension kit':'کیت تعلیق بادی','Repaint (next color)':'رنگ بعدی','UNLIMITED mode on':'حالت نامحدود فعال','Drive a vehicle into the garage marker to tune it.':'برای تیون، با ماشین وارد نشانگر گاراژ شو.',
'Street Brawl: 8 KOs in 60s':'دعوای خیابانی: ۸ ناک‌اوت در ۶۰ ثانیه','win $2,500':'جایزه $2,500','Time Attack: reach the red marker (drive!)':'مسابقه زمانی: برو به نقطه قرمز (با ماشین!)','Survive the Heat: 3 stars for 60s':'فرار از پلیس: ۶۰ ثانیه با ۳ ستاره','win $6,000':'جایزه $6,000','Abandon current challenge':'رها کردن چالش','Pick a challenge. Fight, race or survive.':'یک چالش انتخاب کن.',
'Press F to enter vehicle':'برای سوار شدن F را بزن','Press F to exit (when landed)':'برای پیاده شدن F را بزن (بعد از فرود)','Press F to board':'F را بزن تا سوار شوی:','Press B —':'برای ورود B —',
'3 STARS — POLICE HELICOPTER!':'۳ ستاره — هلیکوپتر پلیس!','5 STARS — TANK DEPLOYED!':'۵ ستاره — تانک آمد!','C4 detonated':'C4 منفجر شد','C4 placed — press X again to detonate':'C4 کار گذاشته شد — دوباره X بزن','Carjacked! The driver is on the ground':'ماشین را گرفتی! راننده روی زمین افتاد','Challenge failed':'چالش شکست خورد','Challenge started!':'چالش شروع شد!','CHALLENGE COMPLETE!':'چالش کامل شد!','Cheat: ':'تقلب: ','Crashed: ':'سقوط: ','hard landing':'فرود سخت','collision':'برخورد','Equip a gun first':'اول یک اسلحه بردار','Land and slow below 90 km/h first':'اول فرود بیا و سرعت را زیر ۹۰ کم کن','Mission failed: out of time':'ماموریت شکست خورد: زمان تمام شد','Not enough cash':'پول کافی نیست','Out of ammo':'مهمات تمام شد','Turn back: edge of the city':'برگرد: لبه شهر','Waypoint set':'نقطه مسیر گذاشته شد','delivered outside':'بیرون تحویل داده شد','purchased':'خریداری شد','equipped':'برداشته شد','MISSION PASSED!':'ماموریت موفق!','WASTED':'مردی','Get in a vehicle':'سوار ماشین شو','Drive to the red marker':'برو به نقطه قرمز','Radio off':'رادیو خاموش','Walk into a shop marker (map: M)':'وارد نشانگر شاپ شو (نقشه: M)','Buy a gun at Harbor Arms (B)':'از اسلحه‌فروشی اسلحه بخر (B)','Shift: throttle':'Shift: گاز','Space: brake':'Space: ترمز','W/S: pitch':'W/S: بالا/پایین','A/D: bank':'A/D: چرخش','J: missile (jets)':'J: موشک (جنگنده)','BRAWL':'دعوا','SURVIVE THE HEAT':'فرار از پلیس','TIME ATTACK':'مسابقه زمانی','reach the red marker in time':'به موقع به نقطه قرمز برس'};
const FAK=Object.keys(FA).sort((a,b)=>b.length-a.length),tr=s=>{if(S.lang!=='fa'||typeof s!=='string')return s;if(FAX[s])return FAX[s];let o=s;for(const k of FAK)if(o.includes(k))o=o.split(k).join(FA[k]);return o};
const BINDS=[['Forward','KeyW'],['Back / brake','KeyS'],['Left','KeyA'],['Right','KeyD'],['Sprint / Nitro','ShiftLeft'],['Jump / handbrake','Space'],['Enter / exit vehicle','KeyF'],['Horn','KeyH'],['Reload / Radio','KeyR'],['Shoot','KeyJ'],['Punch','KeyK'],['Switch weapon','KeyQ'],['C4 place / detonate','KeyX'],['Shop','KeyB'],['Map','KeyM'],['Aim / Scope','KeyZ'],['Air-suspension hop','KeyV'],['Pause','KeyP'],['Interact / talk','KeyE']];
const MB=[['JOY','KeyW',13,66,'Joystick (forward / back / left / right)'],['SPR','ShiftLeft',31,80,'Sprint / Nitro'],['JMP','Space',72,82,'Jump / handbrake'],['SHT','KeyJ',90,66,'Shoot'],['AIM','KeyZ',79,60,'Aim / scope'],['RLD','KeyR',64,70,'Reload / radio'],['ENT','KeyF',90,42,'Enter / exit vehicle'],['PUN','KeyK',88,86,'Punch'],['WPN','KeyQ',76,38,'Switch weapon'],['HRN','KeyH',5,50,'Horn'],['C4','KeyX',5,36,'C4 place / blow'],['HOP','KeyV',62,86,'Air-suspension hop'],['SHP','KeyB',36,12,'Shop'],['MAP','KeyM',46,12,'Map'],['PSE','KeyP',56,12,'Pause'],['INT','KeyE',90,24,'Interact / talk']];
const CHEATS=[['wwsdsksadsjj_ffwsdsa',G=>{G.god=!G.god;G.health=100},'Infinite health (toggle)'],['wsdawdsawds__qkj',G=>{G.rich=true;G.money=999999999;G.cash(0)},'Infinite money'],
['sdwajk_wdsa',G=>{for(const n of GUNS){G.own.add(n);G.am[n]=(G.am[n]||0)+WEAP[n].ammo*3;G.mag[n]=MAG[n]}},'All weapons + ammo'],['wasdwasd_kk',G=>{G.armor=100;G.health=100},'Armor + full health'],
['ssaawwdd_jk',G=>G.setWanted(0),'Clear wanted level'],['wdwdwd_jjk',G=>G.addWanted(2),'Wanted +2'],['dsaw_ffdwas',G=>G.spawnCar('Lambo'),'Spawn Lamborghini'],['dsaw_ffsawd',G=>G.spawnCar('Ferrari'),'Spawn Ferrari'],
['aawwddsskkhjjllmmk_',G=>{G.god=true;G.health=100;G.armor=100;G.rich=true;G.over=true;G.money=999999999;G.nit=9999;G.cash(0);for(const n of GUNS){G.own.add(n);G.am[n]=999;G.mag[n]=MAG[n]}},'EVERYTHING: god mode, infinite money, all weapons, nitro, all upgrades'],['wawdsw__fj',G=>{G.nit=500},'Full nitro (in vehicle)'],['aadwwss_jj',G=>{for(const c of G.cars.slice())if(!c.wreck&&c!==G.driving&&Math.hypot(c.x-G.player.x,c.z-G.player.z)<40)G.explode(c)},'Blow up nearby cars'],['wwddaa_ssjk_f',G=>{G.over=true},'Unlimited upgrades (garage limits removed)'],['ssddww_aajj_k',G=>{G.nit=9999;if(G.driving){G.driving.f.max*=1.5;G.driving.f.acc*=1.5;G.driving.hp+=300}},'Hyper-tune current vehicle + 9999 NOS']];
function push(x,z,r,b){const cx=U.clamp(x,b.x0,b.x1),cz=U.clamp(z,b.z0,b.z1),dx=x-cx,dz=z-cz,d2=dx*dx+dz*dz;
 if(d2>=r*r)return null;if(d2>1e-8){const d=Math.sqrt(d2);return[dx/d,dz/d,r-d]}
 const l=x-b.x0,rr=b.x1-x,t=z-b.z0,bt=b.z1-z,m=Math.min(l,rr,t,bt);
 return m===l?[-1,0,l+r]:m===rr?[1,0,rr+r]:m===t?[0,-1,t+r]:[0,1,bt+r]}
function merge(parts){const P=[],N=[],T=[],K=[],I=[];let o=0;
 for(const p of parts){const g=p.g,pa=g.attributes.position,na=g.attributes.normal,ua=g.attributes.uv;
  for(let i=0;i<pa.count;i++){P.push(pa.getX(i),pa.getY(i),pa.getZ(i));N.push(na.getX(i),na.getY(i),na.getZ(i));
   let u=ua.getX(i),v=ua.getY(i);if(p.uv)[u,v]=p.uv(i>>2,u,v);T.push(u,v);K.push(p.c[0],p.c[1],p.c[2])}
  for(const x of(g.index?g.index.array:[...Array(pa.count).keys()]))I.push(x+o);o+=pa.count}
 const m=new THREE.BufferGeometry();m.setAttribute('position',new THREE.Float32BufferAttribute(P,3));m.setAttribute('normal',new THREE.Float32BufferAttribute(N,3));
 m.setAttribute('uv',new THREE.Float32BufferAttribute(T,2));m.setAttribute('color',new THREE.Float32BufferAttribute(K,3));m.setIndex(I);return m}
/* ===== INPUT ===== */
class Input{constructor(){this.k={};this.dx=0;this.dy=0;this.btn=false;this.locked=false;
 addEventListener('keydown',e=>{if(['Space','F3'].includes(e.code))e.preventDefault();if(Game.binding){e.preventDefault();Game.bindKey(e.code);return}Game.cheatKey(e);const c=Game.kmap(e.code);this.k[c]=1;if(!e.repeat)Game.onKey(c)});
 addEventListener('keyup',e=>this.k[Game.kmap(e.code)]=0);addEventListener('contextmenu',e=>e.preventDefault());
 addEventListener('mousedown',e=>{if(e.button===0)this.btn=true;if(e.button===2)this.k.KeyZ=1});addEventListener('mouseup',e=>{this.btn=false;if(e.button===2)this.k.KeyZ=0});
 addEventListener('mousemove',e=>{if(this.locked||this.btn){this.dx+=e.movementX;this.dy+=e.movementY}})}}
/* ===== AUDIO ===== */
const RADIO=[null,{name:'NEON WAVE 88.1',bpm:104,wave:'sawtooth',root:55,seq:[0,0,12,0,7,7,12,5,0,0,12,0,10,10,7,5],lead:[12,15,19,15,12,10,7,10],kick:4},
 {name:'HARBOR FM 94.5',bpm:88,wave:'triangle',root:41.2,seq:[0,0,-1,0,3,3,0,-5],lead:[7,10,12,10,7,5],kick:3},
 {name:'K-ROCKET 101.1',bpm:140,wave:'square',root:82.4,seq:[0,0,0,7,0,0,5,3],lead:null,kick:2}];
class Sfx{constructor(){this.on=false}
 init(){if(this.on)return;try{const c=this.c=new(window.AudioContext||window.webkitAudioContext)(),o=c.createOscillator();o.type='sawtooth';const mg=c.createGain();mg.gain.value=S.vol;mg.connect(c.destination);Object.defineProperty(c,'destination',{value:mg});this.mg=mg;
  const f=c.createBiquadFilter();f.type='lowpass';f.frequency.value=380;this.eg=c.createGain();this.eg.gain.value=0;o.connect(f);f.connect(this.eg);this.eg.connect(c.destination);o.start();this.eo=o;
  this.hg=c.createGain();this.hg.gain.value=0;this.hg.connect(c.destination);for(const fr of[400,500]){const h=c.createOscillator();h.type='square';h.frequency.value=fr;h.connect(this.hg);h.start()}
  const b=c.createBuffer(1,c.sampleRate,c.sampleRate),d=b.getChannelData(0);for(let i=0;i<d.length;i++)d[i]=Math.random()*2-1;
  const n=c.createBufferSource();n.buffer=b;n.loop=true;const bp=c.createBiquadFilter();bp.type='bandpass';bp.frequency.value=1800;bp.Q.value=2;
  this.sg=c.createGain();this.sg.gain.value=0;n.connect(bp);bp.connect(this.sg);this.sg.connect(c.destination);n.start();this.nb=b;const so=this.so=c.createOscillator();so.type='triangle';this.sn=c.createGain();this.sn.gain.value=0;so.connect(this.sn);this.sn.connect(c.destination);so.start();this.on=true}catch(e){}}
 beep(fr=660){if(!this.on)return;const c=this.c,o=c.createOscillator(),g=c.createGain();o.frequency.value=fr;g.gain.setValueAtTime(.06,c.currentTime);g.gain.exponentialRampToValueAtTime(.001,c.currentTime+.15);o.connect(g);g.connect(c.destination);o.start();o.stop(c.currentTime+.16)}
 shot(v=1){if(!this.on)return;const c=this.c,n=c.createBufferSource(),g=c.createGain();n.buffer=this.nb;g.gain.setValueAtTime(.25*v,c.currentTime);g.gain.exponentialRampToValueAtTime(.001,c.currentTime+.18);n.connect(g);g.connect(c.destination);n.start(c.currentTime,Math.random()*.5,.2)}
 radio(n){clearInterval(this.ri);if(!this.on||!n)return;const S=RADIO[n],c=this.c,dur=30/S.bpm;let k=0;
  this.ri=setInterval(()=>{const t=c.currentTime+.05,st=k++%16,o=c.createOscillator(),g=c.createGain();
   o.type=S.wave;o.frequency.value=S.root*Math.pow(2,S.seq[st%S.seq.length]/12);g.gain.setValueAtTime(.07,t);g.gain.exponentialRampToValueAtTime(.001,t+dur*.9);o.connect(g);g.connect(c.destination);o.start(t);o.stop(t+dur);
   if(S.lead&&st%2===0){const l=c.createOscillator(),lg=c.createGain();l.type='square';l.frequency.value=S.root*4*Math.pow(2,S.lead[(st>>1)%S.lead.length]/12);lg.gain.setValueAtTime(.025,t);lg.gain.exponentialRampToValueAtTime(.001,t+dur*1.6);l.connect(lg);lg.connect(c.destination);l.start(t);l.stop(t+dur*1.7)}
   if(st%S.kick===0){const b=c.createOscillator(),bg=c.createGain();b.frequency.setValueAtTime(140,t);b.frequency.exponentialRampToValueAtTime(40,t+.12);bg.gain.setValueAtTime(.25,t);bg.gain.exponentialRampToValueAtTime(.001,t+.15);b.connect(bg);bg.connect(c.destination);b.start(t);b.stop(t+.16)}
   if(st%2===1){const h=c.createBufferSource(),hg=c.createGain();h.buffer=this.nb;hg.gain.setValueAtTime(.05,t);hg.gain.exponentialRampToValueAtTime(.001,t+.04);h.connect(hg);hg.connect(c.destination);h.start(t,0,.05)}},dur*1000)}
 update(sp,drv,horn,slip,sir){if(!this.on)return;const t=this.c.currentTime;this.so.frequency.setTargetAtTime(850+250*Math.sin(t*7),t,.02);this.sn.gain.setTargetAtTime(sir?.03:0,t,.1);this.eo.frequency.setTargetAtTime(45+sp*140,t,.05);
  this.eg.gain.setTargetAtTime(drv?.04+.05*sp:0,t,.1);this.hg.gain.setTargetAtTime(horn?.08:0,t,.02);this.sg.gain.setTargetAtTime(slip?.05:0,t,.05)}}
/* ===== WORLD ===== */
class Grid{constructor(c){this.c=c;this.m=new Map()}
 key(i,j){return(i+100)*1000+j+100}
 add(b,p=3){const c=this.c;for(let i=Math.floor((b.x0-p)/c);i<=Math.floor((b.x1+p)/c);i++)for(let j=Math.floor((b.z0-p)/c);j<=Math.floor((b.z1+p)/c);j++){const k=this.key(i,j);if(!this.m.has(k))this.m.set(k,[]);this.m.get(k).push(b)}}
 at(x,z){return this.m.get(this.key(Math.floor(x/this.c),Math.floor(z/this.c)))||EMPTY}}
const TOPD=new THREE.Color(0x2f62b8),TOPN=new THREE.Color(0x01020a),NIGHT=new THREE.Color(0x070b1a),DAY=new THREE.Color(0x87b5e8),DUSK=new THREE.Color(0xff8a5c);
class World{
 tex(w,h,draw,rep){const c=document.createElement('canvas');c.width=w;c.height=h;draw(c.getContext('2d'),w,h);const t=new THREE.CanvasTexture(c);if(rep){t.wrapS=t.wrapT=THREE.RepeatWrapping;t.repeat.set(rep,rep)}return t}
 constructor(scene){
  const R=this.R=U.rng(C.seed),L=this.L=[];for(let i=0;i<=10;i++)L.push(-600+C.step*i);
  this.scene=scene;this.grid=new Grid(C.cell);this.boxes=[];this.parks=[];this.edge=false;this.hour=C.start;this.night=0;this.sky=new THREE.Color();
  const hw=this.hw=i=>(C.aves.includes(i)?C.aveW:C.roadW)/2;
  const near=c=>{const i=U.clamp(Math.round((c+600)/C.step),0,10);return Math.abs(c-L[i])<hw(i)+2};
  const D=new THREE.Object3D(),put=(m,n,x,y,z,sx,sy,sz,ry=0)=>{D.position.set(x,y,z);D.scale.set(sx,sy,sz);D.rotation.y=ry;D.updateMatrix();m.setMatrixAt(n,D.matrix)};
  const inst=(g,m,n)=>{const o=new THREE.InstancedMesh(g,m,n);o.frustumCulled=false;scene.add(o);return o};
  const std=(c,r=.9)=>new THREE.MeshStandardMaterial({color:c,roughness:r});
  scene.background=this.sky;scene.fog=new THREE.Fog(0x88aacc,120,650);
  this.du={top:{value:new THREE.Color(0x2f62b8)},hor:{value:new THREE.Color(0x88aacc)},sd:{value:new THREE.Vector3(0,1,0)},nt:{value:0}};
  this.dome=new THREE.Mesh(new THREE.SphereGeometry(700,24,12),new THREE.ShaderMaterial({uniforms:this.du,side:THREE.BackSide,depthWrite:false,fog:false,
   vertexShader:'varying vec3 vP;void main(){vP=normalize(position);gl_Position=projectionMatrix*modelViewMatrix*vec4(position,1.);}',
   fragmentShader:'uniform vec3 top,hor,sd;uniform float nt;varying vec3 vP;float h(vec3 p){return fract(sin(dot(p,vec3(12.9,78.2,37.7)))*43758.5);}void main(){float y=max(vP.y,0.);vec3 c=mix(hor,top,pow(y,.55));float g=max(dot(vP,sd),0.);c+=vec3(1.,.85,.6)*pow(g,220.)*(1.-nt*.5)+vec3(1.,.6,.3)*pow(g,6.)*.18;float st=step(.9972,h(floor(vP*240.)))*nt*step(.08,vP.y);c+=vec3(st);gl_FragColor=vec4(c,1.);}'}));
  this.dome.renderOrder=-10;this.dome.frustumCulled=false;scene.add(this.dome);
  this.hemi=new THREE.HemisphereLight(0xcfe4ff,0x555555,.7);this.sun=new THREE.DirectionalLight(0xffffff,1);
  const sc=this.sun.shadow.camera;sc.left=sc.bottom=-100;sc.right=sc.top=100;sc.near=1;sc.far=500;sc.updateProjectionMatrix();
  this.sun.shadow.mapSize.set(4096,4096);this.sun.shadow.bias=-.0005;this.sun.shadow.normalBias=.4;this.sun.castShadow=true;scene.add(this.hemi,this.sun,this.sun.target);
  // ground + harbor water
  const gt=this.tex(128,128,(g,w,h)=>{g.fillStyle='#8a8d92';g.fillRect(0,0,w,h);for(let i=0;i<900;i++){const v=110+R()*50|0;g.fillStyle=`rgb(${v},${v},${v+4})`;g.fillRect(R()*w,R()*h,2,2)}},50);
  const gr=new THREE.Mesh(new THREE.PlaneGeometry(1500,1368).rotateX(-Math.PI/2),new THREE.MeshStandardMaterial({map:gt,roughness:1}));gr.position.z=-66;gr.receiveShadow=true;scene.add(gr);{const og=new THREE.Mesh(new THREE.PlaneGeometry(3000,1918).rotateX(-Math.PI/2),new THREE.MeshStandardMaterial({color:0x4f6b3c,roughness:1}));og.position.set(0,-.12,-341);og.receiveShadow=true;scene.add(og)}
  const wg=new THREE.PlaneGeometry(3000,800,60,16).rotateX(-Math.PI/2);this.wp=wg.attributes.position;
  this.water=new THREE.Mesh(wg,new THREE.MeshStandardMaterial({color:0x1a5f8f,roughness:.25,metalness:.2,flatShading:true,emissive:0x0a2a44,emissiveIntensity:.5}));this.water.position.set(0,-.6,1018);scene.add(this.water);
  // roads + lane dashes
  const OR=[[-600,-881,16,538],[600,-881,16,538],[0,-1150,2316,16],[-1150,-275,16,1766],[1150,-275,16,1766],[-881,-600,538,16],[881,-600,538,16],[881,0,538,16],[-881,600,538,16],[881,600,538,16]];const rd=inst(new THREE.BoxGeometry(1,1,1),std(0x23272e,.95),22+OR.length);
  for(let i=0;i<=10;i++){put(rd,i*2,L[i],.03,0,hw(i)*2,.06,1224);put(rd,i*2+1,0,.03,L[i],1224,.06,hw(i)*2)}OR.forEach((r,n)=>put(rd,22+n,r[0],.03,r[1],r[2],.06,r[3]));
  const ds=[];for(let i=0;i<=10;i++)for(let c=-596;c<600;c+=14)if(!near(c)){ds.push([L[i],c,0],[c,L[i],Math.PI/2])}for(const r of OR){if(r[2]>r[3]){for(let c=r[0]-r[2]/2+8;c<r[0]+r[2]/2-4;c+=14)ds.push([c,r[1],Math.PI/2])}else{for(let c=r[1]-r[3]/2+8;c<r[1]+r[3]/2-4;c+=14)ds.push([r[0],c,0])}}
  const dm=inst(new THREE.BoxGeometry(.3,.02,4),new THREE.MeshStandardMaterial({color:0xd9b84a,emissive:0x3a2f08}),ds.length);ds.forEach((d,n)=>put(dm,n,d[0],.065,d[1],1,1,1,d[2]));
  // street lights
  const lp=[];for(let i=0;i<=10;i++)for(let c=-600;c<=600;c+=30)if(!near(c)){const o=hw(i)+1.5;lp.push([L[i]+o,c],[c,L[i]+o])}
  this.lampMat=new THREE.MeshStandardMaterial({color:0x222222,emissive:0xffd890,emissiveIntensity:0});
  const pm=inst(new THREE.CylinderGeometry(.12,.15,7,6).translate(0,3.5,0),std(0x4a4f58),lp.length),hm=inst(new THREE.SphereGeometry(.5,6,4).translate(0,7.2,0),this.lampMat,lp.length);
  lp.forEach((p,n)=>{put(pm,n,p[0],0,p[1],1,1,1);put(hm,n,p[0],0,p[1],1,1,1)});
  // traffic lights
  {const tp=[];for(let i=0;i<=10;i++)for(let j=0;j<=10;j++){const a=hw(i)+1.3,b=hw(j)+1.3;tp.push([L[i]+a,L[j]+b,0],[L[i]-a,L[j]-b,0],[L[i]+a,L[j]-b,1],[L[i]-a,L[j]+b,1])}
   const po=inst(new THREE.CylinderGeometry(.1,.12,6,6).translate(0,3,0),std(0x2a2d33),tp.length),hd=inst(new THREE.BoxGeometry(.5,1.2,.4).translate(0,6.2,0),std(0x111111),tp.length),bb=inst(new THREE.SphereGeometry(.42,8,6).translate(0,6.3,0),new THREE.MeshBasicMaterial({color:0xffffff,fog:false}),tp.length);
   tp.forEach((p,n)=>{put(po,n,p[0],0,p[1],1,1,1);put(hd,n,p[0],0,p[1],1,1,1);put(bb,n,p[0],0,p[1],1,1,1);bb.setColorAt(n,new THREE.Color(0xff2a2a))});this.tlb=bb;this.tla=tp.map(p=>p[2])}
  // blocks
  const parts=[],trees=[],pal=[[.62,.62,.6],[.62,.3,.24],[.35,.55,.75],[.8,.7,.5]];
  for(let ix=0;ix<10;ix++)for(let iz=0;iz<10;iz++){
   const x0=L[ix]+hw(ix)+4,x1=L[ix+1]-hw(ix+1)-4,z0=L[iz]+hw(iz)+4,z1=L[iz+1]-hw(iz+1)-4,cx=(x0+x1)/2,cz=(z0+z1)/2;
   if(ix>=7&&ix<=8&&iz>=1&&iz<=2){const p=new THREE.Mesh(new THREE.PlaneGeometry(x1-x0,z1-z0).rotateX(-Math.PI/2),std(0x2f6b3a,1));p.position.set(cx,.02,cz);p.receiveShadow=true;scene.add(p);
    this.parks.push({x0,x1,z0,z1});for(let k=0;k<14;k++)trees.push([x0+3+R()*(x1-x0-6),z0+3+R()*(z1-z0-6),.8+R()*.6])}
   else if(LOTS[ix+','+iz]){const t=LOTS[ix+','+iz],p=new THREE.Mesh(new THREE.PlaneGeometry(x1-x0,z1-z0).rotateX(-Math.PI/2),std(0x55585f,.9));p.position.set(cx,.02,cz);p.receiveShadow=true;scene.add(p);SHOPS.push({...SHOPDEF[t],id:t,w:14,d:10,x:cx,z:cz,mz:cz-1.5})}
   else if(ix===4&&iz===5){const p=new THREE.Mesh(new THREE.PlaneGeometry(x1-x0,z1-z0).rotateX(-Math.PI/2),std(0xb9b4a8,.8));p.position.set(cx,.02,cz);p.receiveShadow=true;scene.add(p);
    const f=(g,m,y)=>{const o=new THREE.Mesh(g,m);o.position.set(cx,y,cz);o.castShadow=true;scene.add(o)};
    f(new THREE.CylinderGeometry(6,6.5,.9,18),std(0x888888),.45);f(new THREE.CylinderGeometry(5.2,5.2,.95,18),new THREE.MeshStandardMaterial({color:0x2a8fd0,emissive:0x0a3a5a,roughness:.2}),.48);f(new THREE.CylinderGeometry(.5,.8,4,8),std(0xaaaaaa),2.5);
    const b={x0:cx-6.5,x1:cx+6.5,z0:cz-6.5,z1:cz+6.5,h:1};this.boxes.push(b);this.grid.add(b)}
   else if(iz<9){
    const mx=cx,mz=cz,cells=[[x0,mx,z0,mz],[mx,x1,z0,mz],[x0,mx,mz,z1],[mx,x1,mz,z1]];let placed=0;
    cells.forEach((c,k)=>{if(R()<.7||(k===3&&!placed)){placed++;const cw=c[1]-c[0],cd=c[3]-c[2],w=14+R()*(Math.min(40,cw-2)-14),d=14+R()*(Math.min(40,cd-2)-14),
     hmax=U.lerp(110,24,U.clamp(Math.hypot(cx,cz)/850,0,1)),h=12+R()*(hmax-12),px=c[0]+w/2+R()*(cw-w),pz=c[2]+d/2+R()*(cd-d),j=(R()-.5)*.16,p=pal[Math.floor(R()*4)];
     parts.push({g:new THREE.BoxGeometry(w,h,d).translate(px,h/2,pz),c:[p[0]+j,p[1]+j,p[2]+j],uv:(f,u,v)=>f<2?[u*d/16,v*h/16]:f<4?[0,0]:[u*w/16,v*h/16]});
     const b={x0:px-w/2,x1:px+w/2,z0:pz-d/2,z1:pz+d/2,h};this.boxes.push(b);this.grid.add(b)}})}}
  const cells=Array.from({length:16},()=>R()<.45),cv=(lit)=>(g,w,h)=>{g.fillStyle=lit?'#000':'#cfcfcf';g.fillRect(0,0,w,h);cells.forEach((on,n)=>{g.fillStyle=lit?(on?'#ffd98a':'#000'):'#566a85';g.fillRect((n%4)*32+6,(n>>2)*32+6,20,20)})};
  this.winMat=new THREE.MeshStandardMaterial({vertexColors:true,map:this.tex(128,128,cv(false),1),emissiveMap:this.tex(128,128,cv(true),1),emissive:0xffffff,emissiveIntensity:0,roughness:.85});
  const bm=new THREE.Mesh(merge(parts),this.winMat);bm.castShadow=bm.receiveShadow=true;scene.add(bm);
  // trees
  const tt=inst(new THREE.CylinderGeometry(.3,.4,3,6).translate(0,1.5,0),std(0x5a3d22),trees.length),tc=inst(new THREE.ConeGeometry(2.2,6,7).translate(0,6,0),std(0x1f6a30),trees.length);
  trees.forEach((t,n)=>{put(tt,n,t[0],0,t[1],t[2],t[2],t[2]);put(tc,n,t[0],0,t[1],t[2],t[2],t[2])});
  // billboards
  const bt=this.tex(256,108,(g,w,h)=>{g.fillStyle='#0b1022';g.fillRect(0,0,w,h);g.strokeStyle='#36f1ff';g.lineWidth=4;g.strokeRect(4,4,w-8,h-8);g.textAlign='center';g.fillStyle='#36f1ff';g.font='bold 40px sans-serif';g.fillText('NEON HARBOR',w/2,58);g.fillStyle='#ff3d8b';g.font='bold 20px sans-serif';g.fillText('DRIVE AFTER DARK',w/2,86)});
  for(const [x,z,ry] of[[-130,10,Math.PI],[130,-10,0],[10,-130,-Math.PI/2],[-10,130,Math.PI/2]]){const g=new THREE.Group(),p=new THREE.Mesh(new THREE.PlaneGeometry(14,6),new THREE.MeshBasicMaterial({map:bt,side:THREE.DoubleSide})),s=new THREE.Mesh(new THREE.BoxGeometry(.4,9,.4),std(0x333333));
   p.position.y=10;s.position.y=4.5;g.add(p,s);g.position.set(x,0,z);g.rotation.y=ry;scene.add(g)}
  // airport (north strip)
  {const slab=(w,d,x,z,c,y)=>{const p=new THREE.Mesh(new THREE.PlaneGeometry(w,d).rotateX(-Math.PI/2),std(c,.9));p.position.set(x,y,z);p.receiveShadow=true;scene.add(p)};
   slab(1100,62,0,-641,0x4a4d54,.04);slab(1100,36,0,-690,0x2a2c31,.05);
   const dm2=inst(new THREE.BoxGeometry(14,.02,.8),new THREE.MeshBasicMaterial({color:0xf2f2f2}),40);for(let i=0;i<40;i++)put(dm2,i,-520+i*27,.07,-690,1,1,1);
   const tw=inst(new THREE.BoxGeometry(.5,.02,12),new THREE.MeshBasicMaterial({color:0xf2f2f2}),12);for(let i=0;i<6;i++){put(tw,i,-545,.07,-696+i*2.4,1,1,1);put(tw,i+6,545,.07,-696+i*2.4,1,1,1)}
   const bld=(w,h,d,x,z,c,gl)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),gl?new THREE.MeshStandardMaterial({color:c,roughness:.15,metalness:.6}):std(c));m.position.set(x,h/2,z);m.castShadow=m.receiveShadow=true;scene.add(m);const b={x0:x-w/2,x1:x+w/2,z0:z-d/2,z1:z+d/2,h};this.boxes.push(b);this.grid.add(b)};
   bld(120,14,36,470,-630,0x9aa6b5,true);bld(90,20,36,-480,-630,0x7a808a);bld(60,18,36,-390,-630,0x6a707a);
   const tc=new THREE.Mesh(new THREE.CylinderGeometry(2.6,3.2,38,10),std(0xcfcfcf));tc.position.set(360,19,-625);tc.castShadow=true;scene.add(tc);const tk=new THREE.Mesh(new THREE.CylinderGeometry(6,4,6,10),new THREE.MeshStandardMaterial({color:0x2a5a7a,roughness:.1,metalness:.7,emissive:0x0a2a3a}));tk.position.set(360,41,-625);scene.add(tk);
   const tb={x0:357,x1:363,z0:-628,z1:-622,h:38};this.boxes.push(tb);this.grid.add(tb);
   const rl=inst(new THREE.BoxGeometry(.6,.4,.6),new THREE.MeshBasicMaterial({color:0xffe9a0}),88);for(let i=0;i<44;i++){put(rl,i,-540+i*25,.25,-673,1,1,1);put(rl,i+44,-540+i*25,.25,-609,1,1,1)}
   const bl=inst(new THREE.BoxGeometry(.5,.4,.5),new THREE.MeshBasicMaterial({color:0x4aa0ff}),44);for(let i=0;i<44;i++)put(bl,i,-540+i*25,.25,-708,1,1,1);
   const mt=std(0x7a8794,.6),dm=std(0x2a2f36,.8);for(const hx of[-420,-290,-160,-30]){const hb=new THREE.Mesh(new THREE.BoxGeometry(40,9,28),mt),ha=new THREE.Mesh(new THREE.CylinderGeometry(20,20,28,16,1,false,-Math.PI/2,Math.PI).rotateX(-Math.PI/2).rotateZ(Math.PI/2).scale(1,.35,1),mt),hd=new THREE.Mesh(new THREE.BoxGeometry(30,8,.3),dm);
    hb.position.set(hx,4.5,-724);ha.position.set(hx,9,-724);hd.position.set(hx,4,-709.8);for(const o of[hb,ha,hd]){o.castShadow=o.receiveShadow=true;scene.add(o)}const q={x0:hx-20,x1:hx+20,z0:-738,z1:-710,h:11};this.boxes.push(q);this.grid.add(q)}
   for(let i=0;i<3;i++){const t=new THREE.Mesh(new THREE.CylinderGeometry(5,5,8,14),std(0xe8e8e8,.5));t.position.set(150+i*14,4,-724);t.castShadow=true;scene.add(t);const q={x0:145+i*14,x1:155+i*14,z0:-729,z1:-719,h:8};this.boxes.push(q);this.grid.add(q)}
   const hp=new THREE.Mesh(new THREE.CircleGeometry(10,24).rotateX(-Math.PI/2),std(0x33363c,.9));hp.position.set(330,.08,-650);scene.add(hp);const hr=new THREE.Mesh(new THREE.RingGeometry(8.4,9.2,32).rotateX(-Math.PI/2),new THREE.MeshBasicMaterial({color:0xf2f2f2}));hr.position.set(330,.1,-650);scene.add(hr);
   for(const[a,b,c]of[[.7,.1,5],[.7,.1,5],[4,.1,.7]]){}const H=(w,d,x)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,.05,d),new THREE.MeshBasicMaterial({color:0xf2f2f2}));m.position.set(330+x,.12,-650);scene.add(m)};H(.8,5,-1.8);H(.8,5,1.8);H(3.8,.8,0);
   const ws=new THREE.Mesh(new THREE.CylinderGeometry(.1,.1,8,6),std(0xcccccc,.5));ws.position.set(-545,4,-603);scene.add(ws);const sk=new THREE.Mesh(new THREE.ConeGeometry(.7,3.5,8).rotateZ(-Math.PI/2),new THREE.MeshBasicMaterial({color:0xff7a2a}));sk.position.set(-543.4,7.5,-603);scene.add(sk)}
  // outer lands: suburbs, forests, mountains
  {const R2=U.rng(4242),pp=[],pal2=[[.62,.62,.6],[.62,.3,.24],[.35,.55,.75],[.8,.7,.5]],bandZ=[-600,0,600],bandX=[-600,600];
   const onR=(x,z,m)=>{if(Math.abs(x)>740||z<-740){for(const c of bandZ)if(Math.abs(z-c)<8+m&&Math.abs(x)>605)return true;for(const c of bandX)if(Math.abs(x-c)<8+m&&z<-605)return true;if(Math.abs(Math.abs(x)-1150)<8+m||Math.abs(z+1150)<8+m)return true}return false};
   for(let xc=-1080;xc<=1080;xc+=90)for(let zc=-1080;zc<=540;zc+=90){
    if(Math.abs(xc)<760&&zc>-760)continue;
    if(bandZ.some(c=>Math.abs(zc-c)<58&&Math.abs(xc)>600)||bandX.some(c=>Math.abs(xc-c)<58&&zc<-600))continue;
    const n=R2()<.8?(R2()<.5?1:2):0;let prev=null;
    for(let k=0;k<n;k++){const w=14+R2()*26,d=14+R2()*26,h=8+R2()*(Math.hypot(xc,zc)>1000?30:46),px=xc+(R2()-.5)*(80-w),pz=zc+(R2()-.5)*(80-d),j=(R2()-.5)*.16,p=pal2[Math.floor(R2()*4)];
     if(prev&&Math.abs(px-prev.x)<(w+prev.w)/2+3&&Math.abs(pz-prev.z)<(d+prev.d)/2+3)continue;
     pp.push({g:new THREE.BoxGeometry(w,h,d).translate(px,h/2,pz),c:[p[0]+j,p[1]+j,p[2]+j],uv:(f,u,v)=>f<2?[u*d/16,v*h/16]:f<4?[0,0]:[u*w/16,v*h/16]});
     const b={x0:px-w/2,x1:px+w/2,z0:pz-d/2,z1:pz+d/2,h};this.boxes.push(b);this.grid.add(b);prev={x:px,z:pz,w,d}}}
   if(pp.length){const m2=new THREE.Mesh(merge(pp),this.winMat);m2.castShadow=m2.receiveShadow=true;scene.add(m2)}
   const tp=[];for(let t=0;t<4000&&tp.length<900;t++){const x=(R2()-.5)*2500,z=-1280+R2()*1880;if(Math.abs(x)<760&&z>-760)continue;if(onR(x,z,6)||!this.free(x,z,4))continue;tp.push([x,z,.8+R2()*.9])}
   const t1=inst(new THREE.CylinderGeometry(.3,.4,3,6).translate(0,1.5,0),std(0x5a3d22),tp.length),t2=inst(new THREE.ConeGeometry(2.2,6,7).translate(0,6,0),std(0x1f6a30),tp.length);
   tp.forEach((t,n)=>{put(t1,n,t[0],0,t[1],t[2],t[2],t[2]);put(t2,n,t[0],0,t[1],t[2],t[2],t[2])});
   const mt=[];for(let i=0;i<60;i++){let x,z;if(i<20){x=-1350-R2()*150;z=-1350+R2()*1900}else if(i<40){x=1350+R2()*150;z=-1350+R2()*1900}else{x=-1350+R2()*2700;z=-1350-R2()*150}mt.push([x,z,90+R2()*110,160+R2()*260])}
   const mo=inst(new THREE.ConeGeometry(1,1,7).translate(0,.5,0),std(0x56606a,1),mt.length);mt.forEach((m,n)=>put(mo,n,m[0],0,m[1],m[2],m[3],m[2]))}
  // minimap base layer
  const S=.5,mm=this.mm=document.createElement('canvas');mm.width=mm.height=1300;const g=mm.getContext('2d'),X=v=>(v+1300)*S;g.fillStyle='#15261a';g.fillRect(0,0,1300,1300);g.fillStyle='#14171d';g.fillRect(X(-750),X(-750),1500*S,1368*S);
  g.fillStyle='#0b2238';g.fillRect(0,X(612),1300,1300-X(612));g.fillStyle='#14385a';for(let i=0;i<1300;i+=14)g.fillRect(i,X(626),7,1);
  g.fillStyle='#15301f';for(const p of this.parks)g.fillRect(X(p.x0),X(p.z0),(p.x1-p.x0)*S,(p.z1-p.z0)*S);
  g.fillStyle='#262b35';for(const b of this.boxes)g.fillRect(X(b.x0),X(b.z0),(b.x1-b.x0)*S,(b.z1-b.z0)*S);
  for(const[c,e]of[['#07090c',2.5],['#59606c',0]])for(let i=0;i<=10;i++){g.fillStyle=c;g.fillRect((L[i]-hw(i)-e+1300)*S,688*S,(hw(i)+e)*2*S,1224*S);g.fillRect(688*S,(L[i]-hw(i)-e+1300)*S,1224*S,(hw(i)+e)*2*S)}g.fillStyle='#59606c';for(const r of OR)g.fillRect(X(r[0]-r[2]/2),X(r[1]-r[3]/2),r[2]*S,r[3]*S);
  g.fillStyle='#3a3e48';g.fillRect(X(-550),X(-672),1100*S,62*S);g.fillStyle='#2c2f37';g.fillRect(X(-550),X(-708),1100*S,36*S);g.fillStyle='#fff';for(let i=0;i<40;i++)g.fillRect(X(-520+i*27),X(-690),8,1.5);g.fillStyle='#8a6d2a';g.fillRect(X(-90),X(-640),180*S,24*S)}
 free(x,z,r){for(const b of this.grid.at(x,z))if(push(x,z,r,b))return false;return true}
 tick(dt,fx,fz,t){
  this.hour=(this.hour+dt*24/C.cycle)%24;const a=(this.hour-6)/24*Math.PI*2,s=Math.sin(a),co=Math.cos(a),day=U.sm(-.12,.3,s);this.night=1-U.sm(-.15,.2,s);
  this.sky.copy(NIGHT).lerp(DAY,day).lerp(DUSK,Math.max(0,1-Math.abs(s)/.3)*.6);this.scene.fog.color.copy(this.sky);this.du.top.value.copy(TOPN).lerp(TOPD,day);this.du.hor.value.copy(this.sky);this.du.nt.value=this.night;
  const k=s>=0?1:-1,vx=co*k,vy=s*k,vz=.25*k,l=Math.hypot(vx,vy,vz);
  this.sun.position.set(fx+vx/l*250,vy/l*250,fz+vz/l*250);this.sun.target.position.set(fx,0,fz);this.du.sd.value.set(vx/l,vy/l,vz/l);
  if(s>=0){this.sun.color.setHex(0xfff1d8);this.sun.intensity=Math.min(1.1,s*3)}else{this.sun.color.setHex(0x6f8fff);this.sun.intensity=.35*Math.min(1,-s*3)}
  this.hemi.intensity=U.lerp(.28,.75,day);this.winMat.emissiveIntensity=this.night*1.3;this.lampMat.emissiveIntensity=this.night*2.5;Car.lm.color.setScalar(.35+.65*this.night);
  for(let i=0;i<this.wp.count;i++){const x=this.wp.getX(i),z=this.wp.getZ(i);this.wp.setY(i,Math.sin(x*.05+t)*.25+Math.cos(z*.07+t*1.3)*.25)}this.wp.needsUpdate=true}}
/* ===== PLAYER ===== */
let OV=null;function ghOf(x,z,y){const o=OV;if(!o||Math.abs(x-o.x)>o.hw||z<o.a||z>o.d)return 0;const g=z<o.b?o.h*(z-o.a)/(o.b-o.a):z<o.c?o.h:o.h*(o.d-z)/(o.d-o.c);return(y!==undefined&&g>2.5&&y<g-2.5)?0:g}
function mkHuman(sh,sk,pn,hr,sho){const g=new THREE.Group(),M=c=>new THREE.MeshStandardMaterial({color:c,roughness:.8}),dk=M(0x111111),wh=M(0xf4f4f4),
 S=(geo,m,x,y,z,p,sx,sy,sz)=>{const o=new THREE.Mesh(geo,m);o.position.set(x,y,z);if(sx)o.scale.set(sx,sy,sz);o.castShadow=true;(p||g).add(o);return o},
 sp=(r,w,h)=>new THREE.SphereGeometry(r,w||12,h||8),cy=(a,b,h,s)=>new THREE.CylinderGeometry(a,b,h,s||12);sho=sho||dk;
 S(cy(.27,.21,.74,14),sh,0,1.35,0,0,1,1,.6);S(sp(.275,14,8),sh,0,1.62,0,0,1,.5,.62);S(sp(.21,12,8),pn,0,1.03,0,0,1,.6,.68);S(cy(.225,.225,.07,14),dk,0,1.08,0,0,1,1,.62);
 S(sp(.12,10,8),sh,.34,1.66,0);S(sp(.12,10,8),sh,-.34,1.66,0);S(cy(.07,.08,.14,8),sk,0,1.77,0);
 const head=new THREE.Group();head.position.set(0,1.95,0);g.add(head);
 S(sp(.2,16,12),sk,0,0,0,head,.92,1.12,1);S(new THREE.SphereGeometry(.212,14,10,0,Math.PI*2,0,Math.PI*.58),hr,0,.02,-.015,head,.93,1.12,1.02);S(sp(.19,10,8),hr,0,-.02,-.08,head,.9,1,.8);
 for(const s of[1,-1]){S(sp(.04,6,5),sk,s*.19,0,0,head,.6,1,1);S(sp(.03,8,6),wh,s*.075,.04,.17,head,1,.8,.6);S(sp(.017,6,5),dk,s*.075,.04,.19,head);S(new THREE.BoxGeometry(.07,.015,.02),hr,s*.075,.09,.18,head)}
 S(new THREE.ConeGeometry(.035,.09,6).rotateX(Math.PI/2),sk,0,-.03,.2,head);S(new THREE.BoxGeometry(.08,.014,.02),M(0x7a2a2a),0,-.09,.185,head);
 const arm=sx=>{const p=new THREE.Group();p.position.set(sx*.41,1.67,0);g.add(p);S(cy(.088,.068,.7,10).translate(0,-.35,0),sh,0,0,0,p);S(sp(.075,8,6),sk,0,-.78,0,p);return p},
 leg=sx=>{const p=new THREE.Group();p.position.set(sx*.13,1,0);g.add(p);S(cy(.12,.088,1,10).translate(0,-.5,0),pn,0,0,0,p);S(new THREE.BoxGeometry(.19,.1,.3),sho,0,-.96,.06,p);S(sp(.1,8,6),sho,0,-.95,.17,p,1,.7,1);return p};
 return{g,head,aL:arm(1),aR:arm(-1),lL:leg(1),lR:leg(-1)}}
function humG(){const T=(geo,x,y,z,sx,sy,sz)=>{if(sx)geo.scale(sx,sy,sz);return geo.translate(x,y,z)},sp=(r,w,h)=>new THREE.SphereGeometry(r,w||10,h||7),cy=(a,b,h,sg)=>new THREE.CylinderGeometry(a,b,h,sg||10),W=[1,1,1],D=[.07,.07,.07];
 const tor=[{g:T(cy(.27,.21,.74,12),0,1.35,0,1,1,.6),c:W},{g:T(sp(.275,12,7),0,1.62,0,1,.5,.62),c:W},{g:T(sp(.21,10,7),0,1.03,0,1,.6,.68),c:W},{g:T(sp(.12,8,6),.34,1.66,0),c:W},{g:T(sp(.12,8,6),-.34,1.66,0),c:W},{g:T(cy(.225,.225,.07,12),0,1.08,0,1,1,.62),c:D}];
 const hd=[{g:T(sp(.2,14,10),0,1.95,0,.92,1.12,1),c:W},{g:T(cy(.07,.08,.14,8),0,1.77,0),c:W},{g:T(sp(.04,6,5),.19,1.95,0,.6,1,1),c:W},{g:T(sp(.04,6,5),-.19,1.95,0,.6,1,1),c:W},{g:T(new THREE.ConeGeometry(.035,.09,6).rotateX(Math.PI/2),0,1.92,.2),c:W},
  {g:T(sp(.03,8,6),.075,1.99,.17,1,.8,.6),c:[1,1,1]},{g:T(sp(.03,8,6),-.075,1.99,.17,1,.8,.6),c:[1,1,1]},{g:T(sp(.017,6,5),.075,1.99,.19),c:D},{g:T(sp(.017,6,5),-.075,1.99,.19),c:D},{g:T(new THREE.BoxGeometry(.08,.014,.02),0,1.86,.185),c:[.35,.1,.1]}];
 const hr=[{g:T(new THREE.SphereGeometry(.212,12,8,0,Math.PI*2,0,Math.PI*.58),0,1.97,-.015,.93,1.12,1.02),c:W},{g:T(sp(.19,8,6),0,1.93,-.08,.9,1,.8),c:W}];
 return{tor:merge(tor),hd:merge(hd),hr:merge(hr),arm:merge([{g:T(cy(.088,.068,.7,8),0,-.35,0),c:W}]),hand:merge([{g:T(sp(.075,8,6),0,-.78,0),c:W}]),leg:merge([{g:T(cy(.12,.088,1,8),0,-.5,0),c:W}]),shoe:merge([{g:T(new THREE.BoxGeometry(.19,.1,.3),0,-.96,.06),c:W},{g:T(sp(.1,8,6),0,-.95,.17,1,.7,1),c:W}])}}
class Player{constructor(scene){this.g=new THREE.Group();const M=c=>new THREE.MeshStandardMaterial({color:c,roughness:.8}),sk=M(0xe0b090),sh=M(0x2b6cff),pn=M(0x222a3a);
 const box=(w,h,d,m,x,y,z,p)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),m);o.position.set(x,y,z);o.castShadow=true;p.add(o)};
 const limb=(w,h,m,x,y)=>{const p=new THREE.Group();p.position.set(x,y,0);this.g.add(p);box(w,h,w,m,0,-h/2,0,p);return p};
 const H=mkHuman(sh,sk,pn,M(0x2a1a10));this.g.add(H.g);this.aL=H.aL;this.aR=H.aR;this.guns={};const gm=M(0x1c1f26),wd=M(0x6b4a2b);
 for(const[n,W]of Object.entries(WEAP)){const g=new THREE.Group(),bx=(w,h,l,m,x,y,z)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,l),m);o.position.set(x,y,z);o.castShadow=true;g.add(o)};
  bx(.09,.13,W.len,gm,0,0,0);bx(.07,.18,.12,gm,0,-.14,-W.len/2+.15);if(n==='Shotgun'||n==='Rifle'||n==='Sniper')bx(.09,.14,.28,wd,0,-.02,-W.len/2-.1);if(n==='Sniper')bx(.06,.07,.3,gm,0,.11,.05);if(n==='SMG')bx(.06,.22,.08,gm,0,-.2,.05);
  const ab=(w,h,l,m,x,y,z)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,l),m);o.position.set(x,y,z);o.visible=false;g.add(o);return o};g.at={sil:ab(.07,.07,.28,gm,0,0,W.len/2+.2),scp:ab(.07,.08,.32,gm,0,.14,.05),lng:ab(.06,.06,.25,gm,0,0,W.len/2+.1),stk:ab(.08,.16,.2,wd,0,-.03,-W.len/2-.15)};
  g.position.set(-.4,1.6,.7);g.visible=false;this.g.add(g);this.guns[n]=g}
 this.flashM=new THREE.Mesh(new THREE.SphereGeometry(.14,6,5),new THREE.MeshBasicMaterial({color:0xffd070,fog:false}));this.flashM.visible=false;this.g.add(this.flashM);this.armed=false;this.lL=H.lL;this.lR=H.lR;
 this.g.rotation.order='YXZ';this.mat={sk,sh,pn};scene.add(this.g);this.x=20;this.z=10;this.y=0;this.vx=this.vz=this.vy=0;this.face=0;this.ph=0}
 step(dt,inp,yaw,w){const k=inp.k,ix=(k.KeyD?1:0)-(k.KeyA?1:0),iz=(k.KeyW?1:0)-(k.KeyS?1:0),sy=Math.sin(yaw),cy=Math.cos(yaw);
  let wx=iz*sy-ix*cy,wz=iz*cy+ix*sy;const len=Math.hypot(wx,wz);if(len>1e-6){wx/=len;wz/=len}else wx=wz=0;
  const sp=(k.ShiftLeft||k.ShiftRight)?C.sprint:C.walk,f=1-Math.exp(-dt*10);this.vx=U.lerp(this.vx,wx*sp,f);this.vz=U.lerp(this.vz,wz*sp,f);
  const gp0=ghOf(this.x,this.z,this.y);if(this.y<=gp0+.05&&k.Space)this.vy=C.jump;this.vy+=C.grav*dt;this.y+=this.vy*dt;if(this.y<gp0){this.y=gp0;this.vy=0}
  this.x+=this.vx*dt;this.z+=this.vz*dt;
  for(let it=0;it<2;it++)for(const b of w.grid.at(this.x,this.z)){const r=push(this.x,this.z,C.pr,b);if(r){this.x+=r[0]*r[2];this.z+=r[1]*r[2]}}
  if(this.x<1400&&Math.abs(this.x)>C.half){this.x=Math.sign(this.x)*C.half;w.edge=true}if(this.x<1400&&(this.z<-C.half||this.z>C.zs)){this.z=U.clamp(this.z,-C.half,C.zs);w.edge=true}
  if(len>1e-6)this.face=U.lerpA(this.face,Math.atan2(wx,wz),1-Math.exp(-dt*12));
  const spd=Math.hypot(this.vx,this.vz);this.ph+=spd*dt*1.6;const sw=Math.sin(this.ph)*Math.min(1,spd/4)*.9;
  this.aL.rotation.x=sw;this.aR.rotation.x=-sw;this.lL.rotation.x=-sw;this.lR.rotation.x=sw;
  this.g.position.set(this.x,this.y+(this.y<=0?Math.abs(Math.sin(this.ph))*.05*Math.min(1,spd/4):0),this.z);this.g.rotation.y=this.face;this.g.rotation.x=Math.min(1,spd/8)*.12}}
/* ===== VEHICLE ===== */
class Car{
 static wg(){return Car._wg||(Car._wg=merge([{g:new THREE.CylinderGeometry(.38,.38,.3,16).rotateZ(Math.PI/2),c:[.04,.04,.04]},{g:new THREE.CylinderGeometry(.24,.24,.32,12).rotateZ(Math.PI/2),c:[.8,.8,.85]}]))}
 static mod(k){const M=CARMODELS[k];if(M.geo)return M.geo;const[L,w,H,hh,dh,z1,z2,z3,z4]=M.d,gc=.3,
  P=[[-L/2,gc],[-L/2,dh-.1],[z4,dh],[z3,H],[z2,H],[z1,hh],[L/2-.35,hh-.08],[L/2,hh-.28],[L/2,gc]],Gl=[[z4+.1,dh+.1],[z3+.03,H-.08],[z2-.03,H-.08],[z1-.1,hh+.1]],
  ex=(pts,wd)=>{const sh=new THREE.Shape();pts.forEach((p,i)=>i?sh.lineTo(p[0],p[1]):sh.moveTo(p[0],p[1]));const d=wd-.16,g=new THREE.ExtrudeGeometry(sh,{depth:d,bevelEnabled:true,bevelSize:.08,bevelThickness:.08,bevelSegments:2});g.translate(0,0,-d/2);g.rotateY(-Math.PI/2);return g},
  wh=(x,z)=>[{g:new THREE.CylinderGeometry(.38,.38,.3,14).rotateZ(Math.PI/2).translate(x,.38,z),c:[.04,.04,.04]},{g:new THREE.CylinderGeometry(.24,.24,.32,10).rotateZ(Math.PI/2).translate(x,.38,z),c:[.75,.75,.8]}],
  parts=[{g:ex(P,w),c:[1,1,1]},{g:ex(Gl,w+.1),c:[.07,.09,.12]}];
  if(M.sp)parts.push({g:new THREE.BoxGeometry(w-.2,.06,.45).translate(0,dh+.3,-L/2+.1),c:[.05,.05,.06]},{g:new THREE.BoxGeometry(.06,.22,.06).translate(.55,dh+.18,-L/2+.2),c:[.05,.05,.06]},{g:new THREE.BoxGeometry(.06,.22,.06).translate(-.55,dh+.18,-L/2+.2),c:[.05,.05,.06]});
  const K=[.04,.04,.05],bx=(a,b,c,x,y,z,col)=>({g:new THREE.BoxGeometry(a,b,c).translate(x,y,z),c:col}),ch=[.85,.86,.9];
  parts.push(bx(w-.05,.17,.14,0,gc+.1,L/2-.04,K),bx(w-.05,.17,.14,0,gc+.1,-L/2+.04,K),bx(w*.55,.13,.05,0,gc+.38,L/2+.02,K),bx(w*.5,.03,.05,0,gc+.3,L/2+.03,ch),
   bx(.07,.1,.5*L*.6,w/2+.01,gc+.14,0,K),bx(.07,.1,.5*L*.6,-w/2-.01,gc+.14,0,K),
   bx(.14,.1,.2,w/2+.06,hh+.06,z1-.2,[1,1,1]),bx(.14,.1,.2,-w/2-.06,hh+.06,z1-.2,[1,1,1]),
   bx(w-.3,.05,.04,0,dh-.12,-L/2-.02,[1,.05,.05]),bx(.02,H-hh-.25,.03,w/2+.01,(H+hh)/2-.05,(z2+z3)/2,K),bx(.02,H-hh-.25,.03,-w/2-.01,(H+hh)/2-.05,(z2+z3)/2,K),
   {g:new THREE.CylinderGeometry(.06,.06,.2,8).rotateX(Math.PI/2).translate(.5,gc+.06,-L/2-.06),c:ch},{g:new THREE.CylinderGeometry(.06,.06,.2,8).rotateX(Math.PI/2).translate(-.5,gc+.06,-L/2-.06),c:ch});
  if(M.sp)parts.push(bx(.5,.05,.7,0,hh+.02,L/2-.9,K));
  if(M.ex)M.ex(parts,bx,K,ch,L,w,H,hh,dh,gc,z1,z2,z3);return M.geo=merge(parts)}
 static lmod(k){const M=CARMODELS[k];if(M.lg)return M.lg;const[L,w,H,hh,dh]=M.d,b=(x,y,z,c)=>({g:new THREE.BoxGeometry(.42,.12,.1).translate(x,y,z),c});
  if(M.lx)return M.lg=merge(M.lx(L,w,H,hh,dh,(a,bb,c,x,y,z,col,rx,ry,rz)=>({g:new THREE.BoxGeometry(a,bb,c).rotateX(rx||0).rotateY(ry||0).rotateZ(rz||0).translate(x,y,z),c:col}),(r,l,x,y,z,col)=>({g:new THREE.CylinderGeometry(r,r,l,14).rotateX(Math.PI/2).translate(x,y,z),c:col})));return M.lg=merge([b(.6,hh-.33,L/2+.09,[1,.95,.7]),b(-.6,hh-.33,L/2+.09,[1,.95,.7]),b(.6,dh-.12,-L/2-.09,[1,.1,.1]),b(-.6,dh-.12,-L/2-.09,[1,.1,.1])])}
 static init(){if(Car.sg)return;const B=(w,h,d,x,y,z,c)=>({g:new THREE.BoxGeometry(w,h,d).translate(x,y,z),c}),W=(x,z)=>({g:new THREE.CylinderGeometry(.38,.38,.3,10).rotateZ(Math.PI/2).translate(x,.38,z),c:[.04,.04,.04]});
  Car.sg=merge([B(2,.7,4.4,0,.75,0,[1,1,1]),B(1.7,.6,2.2,0,1.4,-.2,[.15,.2,.3]),W(1,1.4),W(-1,1.4),W(1,-1.4),W(-1,-1.4)]);
  Car.lg=merge([B(.4,.2,.1,.7,.8,2.2,[1,.95,.7]),B(.4,.2,.1,-.7,.8,2.2,[1,.95,.7]),B(.4,.2,.1,.7,.8,-2.2,[1,.1,.1]),B(.4,.2,.1,-.7,.8,-2.2,[1,.1,.1])]);
  const ec=document.createElement('canvas');ec.width=256;ec.height=128;const eg=ec.getContext('2d'),gr=eg.createLinearGradient(0,0,0,128);gr.addColorStop(0,'#5d93d8');gr.addColorStop(.5,'#e6eef8');gr.addColorStop(.52,'#555a60');gr.addColorStop(1,'#202226');eg.fillStyle=gr;eg.fillRect(0,0,256,128);
  Car.env=new THREE.CanvasTexture(ec);Car.env.mapping=THREE.EquirectangularReflectionMapping;
  const Mp=(g,c)=>({g,c}),bg=(a,b,c,x,y,z,rx=0)=>new THREE.BoxGeometry(a,b,c).rotateX(rx).translate(x,y,z),wh=z=>Mp(new THREE.CylinderGeometry(.42,.42,.18,16).rotateZ(Math.PI/2).translate(0,.42,z),[.04,.04,.04]);
  Car.mg=merge([wh(.95),wh(-.95),Mp(bg(.26,.34,.9,0,.72,0),[.12,.12,.14]),Mp(bg(.3,.3,.55,0,1.08,.22),[1,1,1]),Mp(bg(.3,.1,.55,0,.98,-.4),[.06,.06,.06]),Mp(bg(.3,.07,.4,0,.9,-.9,.15),[1,1,1]),
   Mp(bg(.06,.95,.06,.13,.86,.86,-.23),[.7,.7,.75]),Mp(bg(.06,.95,.06,-.13,.86,.86,-.23),[.7,.7,.75]),Mp(bg(.9,.05,.05,0,1.32,.76),[.7,.7,.75]),Mp(bg(.3,.12,.3,0,.5,.95),[1,1,1]),
   Mp(bg(.14,.14,.6,.22,.45,-.35),[.75,.75,.8]),Mp(bg(.3,.3,.3,0,.55,.1),[.18,.18,.2])]);
  Car.mlg=merge([Mp(bg(.2,.2,.12,0,1.2,1.02),[1,.95,.7]),Mp(bg(.18,.1,.08,0,.95,-1.08),[1,.1,.1])]);
  Car.lm=new THREE.MeshBasicMaterial({vertexColors:true})}
 constructor(scene,color,type,model){Car.init();this.m=new THREE.Group();const mo=type==='motorcycle',MD=model&&(mo?MOTOS:CARMODELS)[model];this.f={...(mo?C.moto:C.car)};if(MD){this.f.max*=MD.mx;this.f.acc*=MD.ac}this.col=color;this.model=model||null;this.nk=(MD&&MD.nk)||1;this.fc=MD&&MD.fc;this.dust=(MD&&MD.dust)||1;this.hp=type==='tank'?700:100;this.y=0;this.vy=0;this.rh=0;this.nit=0;this.nb=false;this.rx=this.rz=0;const s=new THREE.Mesh(mo?Car.mg:(MD?Car.mod(model):Car.sg),new THREE.MeshPhysicalMaterial({color,vertexColors:true,roughness:.28,metalness:.6,clearcoat:1,clearcoatRoughness:.06,envMap:Car.env,envMapIntensity:1.1}));s.castShadow=true;
  this.lmesh=new THREE.Mesh(mo?Car.mlg:(MD?Car.lmod(model):Car.lg),Car.lm);this.m.add(s,this.lmesh);this.wsz=1;this.wh=null;if(MD&&!mo){const[L2,w2]=MD.d;this.wh=[];Car._wm=Car._wm||new THREE.MeshStandardMaterial({vertexColors:true,roughness:.6});for(const[sx,sz]of[[1,1],[-1,1],[1,-1],[-1,-1]]){const gp=new THREE.Group();gp.position.set(sx*(w2/2-.1),.38,sz*L2*.31);const wm=new THREE.Mesh(Car.wg(),Car._wm);wm.castShadow=true;gp.add(wm);this.m.add(gp);this.wh.push({gp,wm,fr:sz>0})}};scene.add(this.m);this.x=this.z=this.h=this.vx=this.vz=this.sp=this.stun=0;this.ai=null;this.slip=false;this.hit=0;this.sk=0;this.body=s;this.type=type||null;if(type==='police')s.material.emissiveIntensity=.6;if(type==='tank')this.m.scale.set(1.25,1.4,1.5);if(mo&&MD&&MD.sc)this.m.scale.set(...MD.sc);this.sc0=this.m.scale.clone();if(mo){const M=c=>new THREE.MeshStandardMaterial({color:c,roughness:.8}),r=this.rider=new THREE.Group(),b=(w,h,d,m,x,y,z,rx)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),m);o.position.set(x,y,z);o.rotation.x=rx||0;o.castShadow=true;r.add(o)};
   this.rmat=[M(0x2b6cff),M(0x222a3a),M(0xe0b090)];const H=mkHuman(this.rmat[0],this.rmat[2],this.rmat[1],M(0x2a1a10),M(0x111111));H.g.rotation.x=.42;H.aL.rotation.x=-1.15;H.aR.rotation.x=-1.15;H.lL.rotation.x=-1.55;H.lR.rotation.x=-1.55;r.add(H.g);r.position.set(0,.5,-.3);r.scale.setScalar(.85);r.visible=false;this.m.add(r)}}
 air(dt){const g0=ghOf(this.x,this.z,this.y);if(this.y>g0+.35||this.vy>0){this.vy-=22*dt;this.y+=this.vy*dt;if(this.spin){this.rx+=this.spin[0]*dt;this.rz+=this.spin[1]*dt}if(this.y<=g0){this.y=g0;if(this.vy<-4)this.vy*=-.25;else{this.vy=0;this.spin=null;this.rx=this.rz=0}}}else{this.y=g0;this.vy=0}}
 step(dt,thr,st,brake,hb){const f=this.f,nb=this.nb,sn=Math.sin(this.h),cs=Math.cos(this.h);let vf=this.vx*sn+this.vz*cs,vl=this.vx*cs-this.vz*sn;
  if(thr>0)vf+=(vf<-.5?f.brake*thr:f.acc*(nb?(this.type==='motorcycle'?3.4*this.nk:3.2):1)*thr*(1-vf/(f.max*(nb?(this.type==='motorcycle'?1.35+.15*this.nk:1.7):1))))*dt;else if(thr<0)vf+=(vf>.5?f.brake*thr:f.acc*.6*thr*(1+vf/f.rev))*dt;
  if(brake)vf*=Math.exp(-3*dt);if(hb)vf-=Math.sign(vf)*Math.min(Math.abs(vf),10*dt);
  vf-=vf*f.drag*dt;if(nb)vf+=(this.type==='motorcycle'?18*this.nk:16)*dt;vf-=Math.sign(vf)*Math.min(Math.abs(vf),f.roll*dt);
  const ang=st*f.steer/(1+Math.abs(vf)*.06);this.h+=U.clamp(vf*Math.tan(ang)/f.wb,-2.6,2.6)*dt;
  vl*=Math.exp(-(hb?f.hb:f.grip)*dt);this.slip=Math.abs(vl)>3;
  this.vx=sn*vf+cs*vl;this.vz=cs*vf-sn*vl;this.x+=this.vx*dt;this.z+=this.vz*dt;this.sp=vf;
  if(this.type==='motorcycle'&&!this.wreck)this.rx=U.lerp(this.rx,this.nb?-.32:0,Math.min(1,dt*5));this.air(dt);if(this.wh){const off=this.rh+(this.wsz-1)*.38,sp=vf*dt/(.38*this.wsz);this.m.position.set(this.x,this.y,this.z);this.body.position.y=off;this.lmesh.position.y=off;for(const w of this.wh){w.wm.rotation.x+=sp;w.gp.scale.setScalar(this.wsz);w.gp.position.y=.38*this.wsz;if(w.fr)w.gp.rotation.y=st*.45}}else this.m.position.set(this.x,this.y+this.rh,this.z);this.m.rotation.set(this.rx,this.h,this.rz);if(this.rider)this.m.rotation.z=this.lean=U.lerp(this.lean||0,U.clamp(-st*Math.min(1,Math.abs(vf)/18)*.55,-.55,.55),.12)}
 collide(w){const sn=Math.sin(this.h),cs=Math.cos(this.h);let imp=0;
  for(const o of CIRC){const cx=this.x+sn*o,cz=this.z+cs*o;
   for(const b of w.grid.at(cx,cz)){const r=push(cx,cz,1.05,b);if(r){this.x+=r[0]*r[2];this.z+=r[1]*r[2];const vn=this.vx*r[0]+this.vz*r[1];
    if(vn<0){this.vx-=1.3*vn*r[0];this.vz-=1.3*vn*r[1];this.vx*=.88;this.vz*=.88;imp=Math.max(imp,-vn)}break}}}
  if(Math.abs(this.x)>C.half){this.x=Math.sign(this.x)*C.half;this.vx=0;w.edge=true}if(this.z<-C.half||this.z>C.zs){this.z=U.clamp(this.z,-C.half,C.zs);this.vz=0;w.edge=true}
  this.hit=imp;if(this.ai&&imp>2)this.stun=2}}
function crash(cars){for(let i=0;i<cars.length;i++){const a=cars[i];for(let j=i+1;j<cars.length;j++){const b=cars[j],dx=b.x-a.x,dz=b.z-a.z;if(dx*dx+dz*dz>25||Math.abs((a.y||0)-(b.y||0))>2.5)continue;
 const as=Math.sin(a.h),ac=Math.cos(a.h),bs=Math.sin(b.h),bc=Math.cos(b.h);
 for(const p of CIRC)for(const q of CIRC){const ex=b.x+bs*q-(a.x+as*p),ez=b.z+bc*q-(a.z+ac*p),d=Math.hypot(ex,ez);
  if(d<2.1&&d>1e-4){const nx=ex/d,nz=ez/d,pen=(2.1-d)/2;a.x-=nx*pen;a.z-=nz*pen;b.x+=nx*pen;b.z+=nz*pen;const rel=(b.vx-a.vx)*nx+(b.vz-a.vz)*nz;
   if(rel<0){const ji=-1.4*rel/2;a.vx-=ji*nx;a.vz-=ji*nz;b.vx+=ji*nx;b.vz+=ji*nz;if(a.ai&&-rel>1.5)a.stun=2;if(b.ai&&-rel>1.5)b.stun=2}}}}}}
/* ===== TRAFFIC ===== */
class Traffic{constructor(w){this.w=w;this.R=w.R;this.t=0}
 st(ax){const u=(this.t+(ax?20:0))%40;return u<16?0:u<19?1:2}
 ri(){return Math.floor(this.R()*11)}
 nb(i,j,ex){const o=[[i+1,j],[i-1,j],[i,j+1],[i,j-1]].filter(n=>n[0]>=0&&n[0]<=10&&n[1]>=0&&n[1]<=10&&!(ex&&n[0]===ex[0]&&n[1]===ex[1]));return o[Math.floor(this.R()*o.length)]}
 geo(a){const L=this.w.L,Ax=L[a.i],Az=L[a.j],dx=Math.sign(L[a.k]-Ax),dz=Math.sign(L[a.l]-Az),ln=this.w.hw(dx?a.j:a.i)/2;
  return{x:Ax-dz*ln,z:Az+dx*ln,dx,dz,len:Math.abs(L[a.k]-Ax)+Math.abs(L[a.l]-Az)}}
 place(car,i,j){const[k,l]=this.nb(i,j);car.ai={i,j,k,l,v:11+this.R()*6};const g=this.geo(car.ai),s=20+this.R()*(g.len-40);
  car.x=g.x+g.dx*s;car.z=g.z+g.dz*s;car.h=Math.atan2(g.dx,g.dz);car.vx=g.dx*8;car.vz=g.dz*8;car.stun=0}
 respawn(car,px,pz){const L=this.w.L;for(let t=0;t<40;t++){const i=this.ri(),j=this.ri(),d=Math.hypot(L[i]-px,L[j]-pz);if(d>C.npc.near&&d<C.npc.far){this.place(car,i,j);return}}}
 drive(car,dt,cars,pl){if(car.stun>0){car.stun-=dt;car.step(dt,0,0,true,false);return}
  let a=car.ai,g=this.geo(a),s=(car.x-g.x)*g.dx+(car.z-g.z)*g.dz;
  if(s>g.len-14){const[ni,nj]=this.nb(a.k,a.l,[a.i,a.j]);a=car.ai={i:a.k,j:a.l,k:ni,l:nj,v:a.v};g=this.geo(a);s=(car.x-g.x)*g.dx+(car.z-g.z)*g.dz}
  const ts=U.clamp(Math.max(s+10,5),0,g.len),err=U.wrap(Math.atan2(g.x+g.dx*ts-car.x,g.z+g.dz*ts-car.z)-car.h);
  let tv=a.v;if(g.len-s<22)tv=7;{const rem=g.len-s,ls=this.st(g.dx?0:1);if(rem>16&&rem<70&&(ls===2||(ls===1&&rem>24)))tv=Math.min(tv,Math.max(0,(rem-17)*.7))}
  const sn=Math.sin(car.h),cs=Math.cos(car.h),chk=(ox,oz)=>{const rx=ox-car.x,rz=oz-car.z,ah=rx*sn+rz*cs;if(ah>0&&ah<C.npc.follow&&Math.abs(rx*cs-rz*sn)<2)tv=Math.min(tv,Math.max(0,(ah-6)*1.2))};
  for(const o of cars)if(o!==car)chk(o.x,o.z);if(pl)chk(pl.x,pl.z);
  car.step(dt,U.clamp((tv-car.sp)*.6,-1,1),U.clamp(err*1.8,-1,1),false,false)}}
/* ===== PEDESTRIANS ===== */
class Peds{constructor(w,scene){this.w=w;this.D=new THREE.Object3D();this.Lm=new THREE.Object3D();this.M=new THREE.Matrix4();this.p=[];const n=C.ped.n,R=w.R,tones=[0xe0b090,0xc68c62,0x8d5a3b,0xf1cfb0],hairs=[0x1a1208,0x4a2a14,0xc9a227,0x777777],
 bx=(a,b,c,x,y,z)=>new THREE.BoxGeometry(a,b,c).translate(x,y,z),mk=(g,cnt)=>{const m=new THREE.InstancedMesh(g,new THREE.MeshStandardMaterial({roughness:.8,vertexColors:true}),cnt);m.frustumCulled=false;m.castShadow=true;scene.add(m);return m};
 const HG=humG();this.tor=mk(HG.tor,n);this.hd=mk(HG.hd,n);this.hr=mk(HG.hr,n);this.arm=mk(HG.arm,2*n);this.hand=mk(HG.hand,2*n);this.leg=mk(HG.leg,2*n);this.shoe=mk(HG.shoe,2*n);
 for(let i=0;i<n;i++){const q={x:0,z:0,t:0,line:0,axis:0,dir:1,sp:1.5,dead:0,down:0,vx:0,vz:0,cd:0,hd:0,free:false,hp:100,gun:false};this.p.push(q);this.place(q,20,10);
  const sh=new THREE.Color().setHSL(R(),.45,.4),pn=new THREE.Color().setHSL(R(),.3,.22),sk=new THREE.Color(tones[i%4]),hr=new THREE.Color(hairs[i%4]),bk=new THREE.Color(0x111111);
  this.tor.setColorAt(i,sh);this.hd.setColorAt(i,sk);this.hr.setColorAt(i,hr);for(let s=0;s<2;s++){this.arm.setColorAt(2*i+s,sh);this.hand.setColorAt(2*i+s,sk);this.leg.setColorAt(2*i+s,pn);this.shoe.setColorAt(2*i+s,bk)}}
 this.all=[this.tor,this.hd,this.hr,this.arm,this.hand,this.leg,this.shoe]}
 place(q,px,pz){const R=this.w.R,L=this.w.L,s=R()<.5?-1:1;q.axis=R()<.5?1:0;const i=U.clamp(Math.round(((q.axis?pz:px)+600)/C.step)+Math.floor(R()*3)-1,0,10);
  q.line=L[i]+(this.w.hw(i)+2)*s;q.t=U.clamp((q.axis?px:pz)+(R()-.5)*C.ped.spread,-585,585);q.dir=R()<.5?-1:1;q.sp=1.2+R()*1.6;q.dead=0;q.down=0;q.free=false;q.hp=100;q.gun=R()<.3;q.pull=0}
 update(dt,px,pz,t,G){const D=this.D,Lm=this.Lm,M=this.M;let n=0;for(const q of this.p){const lie=(q.dead>0||q.down>0)&&!(q.pull>0);
  if(q.dead>0){q.dead-=dt;if(q.dead<=0)this.place(q,px,pz)}
  else if(q.down>0){q.down-=dt;if(q.pull>0){q.pull-=dt;q.x+=q.jv[0]*.5*dt;q.z+=q.jv[1]*.5*dt;if(q.pull<=0){q.vx=q.jv[0];q.vz=q.jv[1];q.fv=9;q.fy=.2;q.bn=0}}
   else{q.x+=q.vx*dt;q.z+=q.vz*dt;q.vx*=.93;q.vz*=.93;q.fv=(q.fv||0)-24*dt;q.fy=Math.max(0,(q.fy||0)+q.fv*dt);if(q.fy<=0){if(q.fv<-6&&!q.bn){q.fv*=-.3;q.bn=1}else q.fv=0}}}
  else if(q.free){const dx=px-q.x,dz=pz-q.z,d=Math.hypot(dx,dz)||1;q.cd-=dt;q.hd=Math.atan2(dx,dz);
   if(q.gun&&d<24&&d>2.5){if(q.cd<=0&&G){q.cd=1.3;G.pedShoot(q)}}
   else if(d>1.6){q.x+=dx/d*5.5*dt;q.z+=dz/d*5.5*dt}
   else if(q.cd<=0&&G&&!G.driving){q.cd=.9;q.atk=.35;G.hurt(7)}
   for(const b of this.w.grid.at(q.x,q.z)){const r=push(q.x,q.z,.5,b);if(r){q.x+=r[0]*r[2];q.z+=r[1]*r[2]}}
   if(d>C.ped.cull)this.place(q,px,pz)}
  else{q.t+=q.dir*q.sp*dt;if(Math.abs(q.t)>585)q.dir=-q.dir}
  if(!q.free){q.x=q.axis?q.t:q.line;q.z=q.axis?q.line:q.t;if(q.dead<=0&&(q.x-px)**2+(q.z-pz)**2>C.ped.cull*C.ped.cull){this.place(q,px,pz);q.x=q.axis?q.t:q.line;q.z=q.axis?q.line:q.t}}
  const ry=q.free?q.hd:q.axis?(q.dir>0?Math.PI/2:-Math.PI/2):(q.dir>0?0:Math.PI),air=(q.fy||0)>.05,mv=!lie&&!(q.pull>0)&&(!q.free||Math.hypot(q.x-px,q.z-pz)>1.7),ph=t*(q.free?11:q.sp*2.6)+n*1.7;
  let aL=0,aR=0,lL=0,lR=0,bob=0;if(mv){const a=Math.sin(ph)*(q.free?1.15:.85);aL=a;aR=-a;lL=-a;lR=a;bob=Math.abs(Math.sin(ph))*.07}
  if(q.atk>0){q.atk-=dt;aR=-1.8*Math.sin((1-q.atk/.35)*Math.PI)}else if(q.free&&q.gun&&!lie&&Math.hypot(q.x-px,q.z-pz)<24)aR=-1.5;
  if(q.pull>0)aL=aR=-2.6;if(lie){aL=air?-2.4:-.5;aR=air?2.4:.5;lL=.25;lR=-.25}
  const rx=lie?(air?-(q.rt=(q.rt||0)+dt*11):-Math.PI/2):0;if(!air)q.rt=0;
  D.position.set(q.x,lie?.3+(q.fy||0):bob,q.z);D.rotation.set(rx,ry,0);D.updateMatrix();this.tor.setMatrixAt(n,D.matrix);this.hd.setMatrixAt(n,D.matrix);this.hr.setMatrixAt(n,D.matrix);
  for(let s=0;s<2;s++){const sd=s?-1:1;Lm.position.set(.4*sd,1.7,0);Lm.rotation.set(s?aR:aL,0,0);Lm.updateMatrix();M.multiplyMatrices(D.matrix,Lm.matrix);this.arm.setMatrixAt(2*n+s,M);this.hand.setMatrixAt(2*n+s,M);
   Lm.position.set(.15*sd,1,0);Lm.rotation.set(s?lR:lL,0,0);Lm.updateMatrix();M.multiplyMatrices(D.matrix,Lm.matrix);this.leg.setMatrixAt(2*n+s,M);this.shoe.setMatrixAt(2*n+s,M)}
  n++}
  for(const m of this.all)m.instanceMatrix.needsUpdate=true}}
const PM=(c,mt=.4,r=.45)=>new THREE.MeshStandardMaterial({color:c,metalness:mt,roughness:r,side:THREE.DoubleSide}),
PF=(r0,r1,len,z,x=0,y=0)=>new THREE.CylinderGeometry(r1,r0,len,12).rotateX(Math.PI/2).translate(x,y,z),
PW=(pts,th,y,z)=>{const sh=new THREE.Shape();pts.forEach((p,i)=>i?sh.lineTo(p[0],p[1]):sh.moveTo(p[0],p[1]));const g=new THREE.ExtrudeGeometry(sh,{depth:th,bevelEnabled:false});g.rotateX(-Math.PI/2);g.translate(0,y,z);return g},
PA=(g,mt,gr,x=0,y=0,z=0)=>{const o=new THREE.Mesh(g,mt);o.position.set(x,y,z);o.castShadow=true;gr.add(o);return o},
PG=(gr,mt,list,r)=>{for(const[x,y,z]of list)PA(new THREE.CylinderGeometry(r,r,r*.7,10).rotateZ(Math.PI/2),mt,gr,x,y,z)},
PLANES={
 Cessna:{name:'Cessna 172',vm:62,vs:24,gy:1.05,camd:17,span:8,jet:0,x:-300,build(){const g=new THREE.Group(),w=PM(0xf2f2f2),r=PM(0xc0392b),k=PM(0x222222),gl=PM(0x2a4a6a,.8,.1);
  PA(PF(.25,.55,7,0),w,g);PA(PW([[-5.5,0],[5.5,0],[5.5,1.5],[-5.5,1.5]],.12,.62,1.2),w,g);PA(PW([[-1.9,0],[1.9,0],[1.9,.9],[-1.9,.9]],.1,.3,-3.1),w,g);PA(new THREE.BoxGeometry(.1,1.3,1.1),r,g,0,.9,-3.1);
  const c=PA(new THREE.SphereGeometry(.5,10,8),gl,g,0,.5,.7);c.scale.set(.9,.7,1.5);g.prop=new THREE.Group();g.prop.position.z=3.55;g.add(g.prop);PA(new THREE.BoxGeometry(.12,2,.1),k,g.prop);PA(new THREE.BoxGeometry(2,.12,.1),k,g.prop);PG(g,k,[[.8,-.75,.9],[-.8,-.75,.9],[0,-.75,2.5]],.25);return g}},
 Boeing:{name:'Boeing 737',vm:118,vs:46,gy:3,camd:42,span:20,jet:0,x:-170,build(){const g=new THREE.Group(),w=PM(0xf4f6f8),b=PM(0x1f4e8c),k=PM(0x222222),gl=PM(0x1a2a3a,.8,.1);
  PA(PF(1.9,1.9,30,0),w,g);PA(PF(1.9,.4,8,19),w,g);PA(PF(.5,1.9,9,-19.5),w,g);PA(PW([[-17,5.5],[-17,7.7],[0,9],[17,7.7],[17,5.5],[0,0]],.3,-.9,4),w,g);
  for(const s of[1,-1]){PA(PF(.8,.9,3.4,5,s*6,-2),k,g)}PA(PW([[-6.5,3],[-6.5,4.6],[0,5],[6.5,4.6],[6.5,3],[0,0]],.2,.9,-17),w,g);PA(new THREE.BoxGeometry(.25,6,5),b,g,0,4.2,-19);
  const c=PA(new THREE.SphereGeometry(.9,10,8),gl,g,0,.8,20.2);c.scale.set(1,.5,.8);PG(g,k,[[2,-2.4,3],[-2,-2.4,3],[0,-2.4,16]],.55);return g}},
 F35:{name:'F-35 Lightning II',vm:235,vs:42,gy:1.6,camd:26,span:8,jet:1,x:-30,build(){const g=new THREE.Group(),w=PM(0x5c636c,.6,.35),d=PM(0x2a2d33),gl=PM(0xd8a030,.9,.05);
  PA(PF(.95,.95,12,0),w,g);PA(PF(.95,.1,5,8.5),w,g);PA(PF(.55,.95,3.5,-7.75),w,g);PA(PF(.5,.6,1.2,-10),d,g);
  PA(PW([[-5.5,3],[-5.5,4.4],[0,5.6],[5.5,4.4],[5.5,3],[0,0]],.15,-.1,1.6),w,g);PA(PW([[-3,1.6],[-3,3],[0,3.4],[3,3],[3,1.6],[0,0]],.12,0,-6),w,g);
  for(const s of[1,-1]){const f=PA(new THREE.BoxGeometry(.1,2.1,2),w,g,s*.95,1.5,-7);f.rotation.z=-s*.28}
  const c=PA(new THREE.SphereGeometry(.7,10,8),gl,g,0,.85,3);c.scale.set(.8,.7,2.6);PG(g,d,[[1.2,-1.2,0],[-1.2,-1.2,0],[0,-1.2,6]],.3);return g}},
 Sukhoi:{name:'Sukhoi Su-57',vm:255,vs:40,gy:1.6,camd:28,span:10,jet:1,x:100,build(){const g=new THREE.Group(),w=PM(0x4d555e,.6,.35),d=PM(0x15171a),gl=PM(0xb08a30,.9,.05);
  PA(PF(.8,.8,13,0),w,g);PA(PF(.8,.08,6,9.5),w,g);PA(PF(.5,.8,3,-8),w,g);
  for(const s of[1,-1]){PA(PF(.6,.65,7,-6,s*1.25,-.2),w,g);PA(PF(.5,.55,1,-10,s*1.25,-.2),d,g);const f=PA(new THREE.BoxGeometry(.1,2.6,2.2),w,g,s*1.9,1.4,-7.5);f.rotation.z=-s*.3}
  PA(PW([[-7.4,2.8],[-7.4,4.4],[0,6.2],[7.4,4.4],[7.4,2.8],[0,0]],.16,-.1,2),w,g);PA(PW([[-3.8,1.8],[-3.8,3.2],[0,3.8],[3.8,3.2],[3.8,1.8],[0,0]],.12,0,-6.5),w,g);
  const c=PA(new THREE.SphereGeometry(.7,10,8),gl,g,0,.8,4);c.scale.set(.75,.65,2.8);PG(g,d,[[1.4,-1.1,0],[-1.4,-1.1,0],[0,-1.1,6.5]],.3);return g}},
 B2:{name:'B-2 Spirit',vm:160,vs:48,gy:1.5,camd:44,span:28,jet:1,x:250,build(){const g=new THREE.Group(),w=PM(0x2b2e33,.5,.5),gl=PM(0x111418,.9,.05);
  PA(PW([[0,0],[26,13],[26,15.5],[14,14],[9,14.5],[4,18.5],[0,16.5],[-4,18.5],[-9,14.5],[-14,14],[-26,15.5],[-26,13]],1.1,-.55,9),w,g);
  const c=PA(new THREE.SphereGeometry(1,10,8),w,g,0,.5,2);c.scale.set(2.2,.9,5);for(const s of[1,-1]){const e=PA(new THREE.SphereGeometry(1,10,8),w,g,s*3.2,.5,-3);e.scale.set(1.5,.8,4)}
  const k=PA(new THREE.SphereGeometry(.8,10,8),gl,g,0,.9,5.5);k.scale.set(1.2,.6,1.8);PG(g,gl,[[2.6,-1.2,0],[-2.6,-1.2,0],[0,-1.2,5]],.45);return g}}};
{const RC=(k,m)=>function(){const g=PLANES[k].build();g.traverse(o=>{if(o.isMesh&&o.material&&o.material.color){const h=o.material.color.getHex();if(m[h]!=null){o.material=o.material.clone();o.material.color.setHex(m[h])}}});return g};
Object.assign(PLANES,{
Biplane:{name:'Vintage Biplane',vm:48,vs:20,gy:.95,camd:15,span:5,jet:0,x:-450,z:-690,build(){const g=new THREE.Group(),w=PM(0xd8c070),r=PM(0xb03030),k=PM(0x222222),gl=PM(0x2a4a6a,.8,.1);
 PA(PF(.35,.6,5.5,0),r,g);const wp=[[-4.6,0],[4.6,0],[4.6,1.3],[-4.6,1.3]];PA(PW(wp,.1,-.1,1),w,g);PA(PW(wp,.1,1.5,1),w,g);
 for(const s of[1,-1])for(const z of[.3,1.8])PA(new THREE.BoxGeometry(.08,1.6,.08),k,g,s*2.4,.7,z);
 PA(PW([[-1.6,0],[1.6,0],[1.6,.8],[-1.6,.8]],.08,.2,-2.9),w,g);PA(new THREE.BoxGeometry(.08,1.1,.9),r,g,0,.75,-2.9);const c=PA(new THREE.SphereGeometry(.4,8,6),gl,g,0,.6,.5);c.scale.set(.9,.7,1.3);
 g.prop=new THREE.Group();g.prop.position.z=3.15;g.add(g.prop);PA(new THREE.BoxGeometry(.1,2.2,.1),k,g.prop);PA(new THREE.BoxGeometry(2.2,.1,.1),k,g.prop);PG(g,k,[[.7,-.75,.9],[-.7,-.75,.9],[0,-.6,-2.6]],.22);return g}},
Learjet:{name:'Learjet 75',vm:150,vs:36,gy:1.4,camd:22,span:8,jet:0,x:-235,build(){const g=new THREE.Group(),w=PM(0xf4f6f8),b=PM(0x2c3e66),k=PM(0x222222),gl=PM(0x1a2a3a,.8,.1);
 PA(PF(.9,.9,10,0),w,g);PA(PF(.9,.15,3.5,6.75),w,g);PA(PF(.25,.9,4,-7),w,g);PA(PW([[-5.5,2],[-5.5,3],[0,3.6],[5.5,3],[5.5,2],[0,0]],.15,-.3,1.5),w,g);
 PA(PW([[-2.2,1],[-2.2,1.8],[0,2.1],[2.2,1.8],[2.2,1],[0,0]],.1,1.7,-6),w,g);PA(new THREE.BoxGeometry(.12,2.2,1.8),b,g,0,1.6,-6.6);
 for(const s of[1,-1])PA(PF(.4,.45,2.4,-5,s*1.3,.5),k,g);const c=PA(new THREE.SphereGeometry(.7,10,8),gl,g,0,.5,5);c.scale.set(.9,.6,1.4);PG(g,k,[[.9,-1.1,.5],[-.9,-1.1,.5],[0,-1.1,5]],.3);return g}},
Concorde:{name:'Concorde',vm:210,vs:56,gy:2.8,camd:36,span:9,jet:0,z:-690,x:-100,build(){const g=new THREE.Group(),w=PM(0xf6f6f6),k=PM(0x222222),gl=PM(0x1a2a3a,.8,.1);
 PA(PF(1,1,26,0),w,g);PA(PF(1,.2,8,17),w,g);PA(PF(.4,1,5,-15.5),w,g);PA(PW([[0,0],[9,16],[-9,16]],.3,-.6,6),w,g);PA(new THREE.BoxGeometry(.2,4,4),w,g,0,3,-13);
 for(const s of[1,-1])for(const x of[2.2,3.8])PA(PF(.6,.7,5,-8,s*x,-1.3),k,g);const c=PA(new THREE.SphereGeometry(.8,10,8),gl,g,0,.7,15);c.scale.set(.8,.5,1.2);PG(g,k,[[2.3,-2.3,-3],[-2.3,-2.3,-3],[0,-2.3,11]],.5);return g}},
Heli:{name:'Apache Helicopter',vm:62,vs:1,gy:1.15,camd:20,span:5,jet:1,heli:1,x:330,build(){const g=new THREE.Group(),w=PM(0x2d3b2a,.5,.4),k=PM(0x1a1a1a),gl=PM(0x2a4a6a,.9,.1);
 const bd=PA(new THREE.SphereGeometry(1,12,10),w,g,0,0,0);bd.scale.set(1.1,1.05,2.7);PA(PF(.2,.55,5,-3.8),w,g);PA(new THREE.BoxGeometry(.1,1.4,.9),w,g,0,.9,-6);PA(new THREE.BoxGeometry(2.4,.08,.5),w,g,0,-.1,-6.2);
 const c=PA(new THREE.SphereGeometry(.8,10,8),gl,g,0,.45,1.9);c.scale.set(.8,.7,1.4);PA(new THREE.BoxGeometry(3.8,.1,.7),w,g,0,.1,.2);
 for(const s of[1,-1]){PA(PF(.18,.18,1.8,.3,s*1.9,-.1),k,g);PA(new THREE.BoxGeometry(.1,.1,3.4),k,g,s*.95,-1.05,0);PA(new THREE.BoxGeometry(.08,.9,.08),k,g,s*.9,-.6,.8);PA(new THREE.BoxGeometry(.08,.9,.08),k,g,s*.9,-.6,-.8)}
 PA(new THREE.CylinderGeometry(.12,.12,.8,6),k,g,0,1.2,0);g.prop=new THREE.Group();g.prop.position.y=1.65;g.add(g.prop);PA(new THREE.BoxGeometry(9,.05,.3),k,g.prop);PA(new THREE.BoxGeometry(.3,.05,9),k,g.prop);return g}},
Airbus:{name:'Airbus A320',vm:112,vs:44,gy:3,camd:40,span:18,jet:0,z:-690,x:-300,build:RC('Boeing',{0x1f4e8c:0xd03a2a})},
Raptor:{name:'F-22 Raptor',vm:260,vs:42,gy:1.6,camd:28,span:9,jet:1,x:35,build:RC('Sukhoi',{0x4d555e:0x8a96a6})},
Stunt:{name:'Stunt Plane',vm:70,vs:24,gy:1.05,camd:17,span:7,jet:0,x:-390,z:-690,build:RC('Cessna',{0xc0392b:0xf1c40f,0xf2f2f2:0x222222})}})}
{const V=(base,name,map,o)=>{const B=PLANES[base];return{...B,name,...(o||{}),build(){const g=B.build();g.traverse(m=>{if(m.isMesh&&m.material&&m.material.color){const h=m.material.color.getHex();if(map[h]!=null){m.material=m.material.clone();m.material.color.setHex(map[h])}}});return g}}};
Object.assign(PLANES,{Cessna2:V('Cessna','Cessna Sky Blue',{0xc0392b:0x2c7be5}),Cessna3:V('Cessna','Cessna Green',{0xc0392b:0x27ae60}),Stunt2:V('Stunt','Stunt Plane Red',{0xf1c40f:0xe74c3c}),Biplane2:V('Biplane','Blue Biplane',{0xd8c070:0x4a90d9}),Learjet2:V('Learjet','Learjet Red',{0x2c3e66:0xc0392b}),
Boeing2:V('Boeing','Boeing 737 Green',{0x1f4e8c:0x2e8b57}),Cargo:V('Boeing','Cargo Freighter',{0xf4f6f8:0xc9a46a,0x1f4e8c:0x7a5a2a}),Airbus2:V('Airbus','Airbus A320 Blue',{0xd03a2a:0x2c3e66}),F35b:V('F35','F-35B Navy',{0x5c636c:0x3a4a6a}),Sukhoi2:V('Sukhoi','Su-57 Desert',{0x4d555e:0xb59a6a}),
Raptor2:V('Raptor','F-22 Shadow',{0x8a96a6:0x1a1c20}),B2b:V('B2','B-2 Steel',{0x2b2e33:0x555a63}),Heli2:V('Heli','Police Helicopter',{0x2d3b2a:0x1c2a48}),Heli3:V('Heli','Rescue Helicopter',{0x2d3b2a:0xb03030})})}
class Plane{constructor(sc,key){const P=PLANES[key];this.P=P;this.g=P.build();this.prop=this.g.prop;sc.add(this.g);this.hx=P.x;this.hz=P.z||-650;this.hh=Math.PI/2;this.fl=true;this.camd=P.camd;this.gy=P.gy;this.reset()}
 flyH(dt,k,G){const P=this.P,up=(k.ShiftLeft?1:0)-(k.Space?1:0),pit=(k.KeyS?1:0)-(k.KeyW?1:0),rol=(k.KeyA?1:0)-(k.KeyD?1:0),e=m=>1-Math.exp(-dt*m),f0=this.gl||0;
  let vt=up*14;if(vt<0)vt=Math.max(vt,-(Math.max(0,this.y-f0)*1.5+1.2));
  this.th=U.lerp(this.th,(this.y-f0>.1||up>0)?1:0,e(2));this.vy=U.lerp(this.vy||0,vt,e(2.5));this.p=U.lerp(this.p,pit*.3,e(2.5));this.r=U.lerp(this.r,rol*.35,e(3));
  this.v=U.lerp(this.v,pit<0?P.vm:pit>0?-P.vm*.35:0,e(.9));this.h+=rol*1.3*dt;const ox=this.x,oz=this.z,oy=this.y;this.y+=this.vy*dt;this.x+=Math.sin(this.h)*this.v*dt;this.z+=Math.cos(this.h)*this.v*dt;this.sp=Math.abs(this.v);
  let crash=null,fl=0;const bs=G.world.grid.at(this.x,this.z);for(const b of bs)if(this.x>b.x0&&this.x<b.x1&&this.z>b.z0&&this.z<b.z1&&oy>=b.h-.6)fl=Math.max(fl,b.h);
  for(const b of bs)if(this.x>b.x0-1&&this.x<b.x1+1&&this.z>b.z0-1&&this.z<b.z1+1&&this.y<b.h-.6&&!(this.x>b.x0&&this.x<b.x1&&this.z>b.z0&&this.z<b.z1&&oy>=b.h-.6)){if(this.y>1&&Math.abs(this.v)>14)crash='collision';this.x=ox;this.z=oz;this.v=0}
  this.gl=fl;if(this.y<=fl){if(this.vy<-14)crash='hard landing';this.y=fl;this.vy=Math.max(0,this.vy);if(!up)this.v*=Math.exp(-2*dt)}
  this.x=U.clamp(this.x,-1250,1250);this.z=U.clamp(this.z,-1250,610);if(this.prop)this.prop.rotation.y+=dt*(12+this.th*45);this.place();return crash}
 reset(){this.vy=0;this.x=this.hx;this.z=this.hz;this.h=this.hh;this.y=0;this.v=0;this.th=0;this.p=0;this.r=0;this.sp=0;this.alive=true;this.dead=0;this.g.visible=true;this.g.rotation.order='YXZ';this.place()}
 place(){this.g.position.set(this.x,this.y+this.gy,this.z);this.g.rotation.set(-this.p,this.h,-this.r)}
 fly(dt,k,G){if(this.P.heli)return this.flyH(dt,k,G);const P=this.P,ctrl=U.clamp(this.v/P.vs,0,1);this.th=U.clamp(this.th+((k.ShiftLeft?1:0)-(k.Space?1:0))*.45*dt,0,1);
  this.v+=(this.th*P.vm-this.v)*(1-Math.exp(-dt*(this.th*P.vm>this.v?.45:.6)));
  const gnd=this.y<=.05,pit=(gnd&&this.v/P.vs>=.85&&this.th>.5)?1:(k.KeyS?1:0)-(k.KeyW?1:0),rol=(k.KeyA?1:0)-(k.KeyD?1:0);if(gnd&&this.th<.02)this.v*=Math.exp(-.5*dt);
  const lift=U.clamp((this.v/P.vs-.75)/.25,0,1);this.p+=pit*(gnd&&lift<1?0:1)*.9*dt*Math.max(ctrl,.15);if(!pit)this.p*=Math.exp(-.3*dt);this.p=U.clamp(this.p,gnd?0:-1.2,1.2);if(!gnd&&lift<1)this.p-=(1-lift)*.6*dt;
  this.r=U.lerp(this.r,gnd?0:rol*1.05,1-Math.exp(-dt*3));this.h+=gnd?rol*.7*dt*U.clamp(this.v/12,0,1):Math.sin(this.r)*1.15*dt*(.4+ctrl*.6);
  const vy=Math.sin(this.p)*this.v*(.3+.7*lift)-(1-lift)*(gnd?0:26),hv=Math.cos(this.p)*this.v;this.y+=vy*dt;const ox=this.x,oz=this.z;this.x+=Math.sin(this.h)*hv*dt;this.z+=Math.cos(this.h)*hv*dt;this.sp=this.v;
  let crash=null;if(this.y<=0){if(!gnd&&(vy<-13||Math.abs(this.r)>.6))crash='hard landing';this.y=0;if(this.p<0)this.p=0}
  for(const b of G.world.grid.at(this.x,this.z))if(this.x>b.x0-1&&this.x<b.x1+1&&this.z>b.z0-1&&this.z<b.z1+1&&this.y<b.h){if(this.y<=.05&&this.v<18){this.x=ox;this.z=oz;this.v=0}else crash='collision'}
  this.x=U.clamp(this.x,-1250,1250);this.z=U.clamp(this.z,-1250,610);if(this.prop)this.prop.rotation.z+=dt*(10+this.th*60);this.place();return crash}}
class Heli{constructor(sc){const M=(c,m=.5)=>new THREE.MeshStandardMaterial({color:c,roughness:.4,metalness:m}),g=this.g=new THREE.Group(),P=(geo,mt,x,y,z,p=g)=>{const o=new THREE.Mesh(geo,mt);o.position.set(x,y,z);o.castShadow=true;p.add(o);return o},bm=M(0x1c2a48);
 P(new THREE.SphereGeometry(1.4,14,10).scale(.9,.85,1.7),bm,0,0,0);P(new THREE.CylinderGeometry(.18,.5,5,8).rotateX(Math.PI/2),bm,0,.3,-3.2);P(new THREE.BoxGeometry(.12,1.3,.7),bm,0,.9,-5.5);P(new THREE.SphereGeometry(.95,12,8).scale(.95,.75,1),M(0x6fb4d8,.9),0,.35,1.2);P(new THREE.BoxGeometry(.2,.4,.2),bm,0,1.5,0);
 P(new THREE.CylinderGeometry(.06,.06,3,6).rotateX(Math.PI/2),bm,.9,-1.25,.2);P(new THREE.CylinderGeometry(.06,.06,3,6).rotateX(Math.PI/2),bm,-.9,-1.25,.2);
 const r=this.rot=new THREE.Group();r.position.y=1.7;g.add(r);P(new THREE.BoxGeometry(.3,.05,8.5),M(0x111111),0,0,0,r);P(new THREE.BoxGeometry(8.5,.05,.3),M(0x111111),0,0,0,r);
 this.tr=new THREE.Group();this.tr.position.set(.2,.9,-5.5);g.add(this.tr);P(new THREE.BoxGeometry(.05,1.6,.15),M(0x111111),0,0,0,this.tr);
 this.bc=P(new THREE.SphereGeometry(.25,8,6),new THREE.MeshBasicMaterial({color:0xff0000,fog:false}),0,-1.2,0);sc.add(g);this.x=this.z=0;this.y=26;this.a=0;this.cd=1}}
/* ===== CAMERA ===== */
class Rig{constructor(cam){this.c=cam;this.yaw=0;this.pit=.25;this.idle=0;this.p=new THREE.Vector3();this.t=new THREE.Vector3();this.init=false}
 update(dt,G){const inp=G.inp,w=G.world,car=G.driving||G.flying,pl=G.player;
  if(inp.dx||inp.dy){const sn=G.sens*this.c.fov/70*.0025;this.yaw-=inp.dx*sn;this.pit=U.clamp(this.pit+inp.dy*sn,-.44,1.05);this.idle=0;inp.dx=inp.dy=0}else this.idle+=dt;
  let d,fy,fx=pl.x,fz=pl.z;
  if(car){fx=car.x;fz=car.z;fy=1.4+(car.y||0)+(car.gy||0);d=car.camd||C.cam.cd;if(this.idle>C.cam.idle||car.fl){const k=1-Math.exp(-2*dt);this.yaw=U.lerpA(this.yaw,car.h,k);this.pit=U.lerp(this.pit,Math.atan2(C.cam.ch,d),k)}}
  else{fy=pl.y+C.cam.fh*.8;d=C.cam.fd}
  const cp=Math.cos(this.pit),ox=-Math.sin(this.yaw)*cp*d,oy=Math.sin(this.pit)*d,oz=-Math.cos(this.yaw)*cp*d;let k=1;
  for(let i=1;i<=8&&k===1;i++){const t=i/8,x=fx+ox*t,z=fz+oz*t,y=fy+oy*t;for(const b of w.grid.at(x,z))if(x>b.x0-.3&&x<b.x1+.3&&z>b.z0-.3&&z<b.z1+.3&&y<b.h){k=Math.max(.12,(i-1)/8);break}}
  const tx=fx+ox*k,ty=Math.max(.5,fy+oy*k),tz=fz+oz*k;
  if(!this.init){this.p.set(tx,ty,tz);this.t.set(fx,fy,fz);this.init=true}else{this.p.lerp(new THREE.Vector3(tx,ty,tz),1-Math.exp(-dt*8));this.t.lerp(new THREE.Vector3(fx,fy,fz),1-Math.exp(-dt*14))}
  if(G.fp&&!car){const hx=pl.x+Math.sin(this.yaw)*.3,hy=pl.y+1.95,hz=pl.z+Math.cos(this.yaw)*.3,cp2=Math.cos(this.pit);this.p.set(hx,hy,hz);this.t.set(hx+Math.sin(this.yaw)*cp2,hy-Math.sin(this.pit),hz+Math.cos(this.yaw)*cp2)}
  this.c.position.copy(this.p);this.c.lookAt(this.t);
  let f=car?C.cam.fov+(C.cam.fovMax-C.cam.fov)*Math.min(1,Math.abs(car.sp)/C.car.max):C.cam.fov;if(car&&car.nb)f+=car.type==='motorcycle'?16:12;if(G.aiming)f=G.scopeFov;
  if(Math.abs(this.c.fov-f)>.05){this.c.fov=U.lerp(this.c.fov,f,1-Math.exp(-dt*4));this.c.updateProjectionMatrix()}}}
/* ===== GAME ===== */
class GameCls{
 constructor(){
  this.state='MENU';this.money=5000;this.health=100;this.armor=0;this.wanted=0;this.c4=[];this.policeSpawned=0;this.tankSpawned=false;this.weaponName='Fist';this.weaponCooldown=0;this.shopOpen=false;this.ammo=60;this.dead=0;this.fee=0;this.bust=0;this.evade=0;this.bigT=0;this.hitT=0;this.radio=0;this.tt=0;this.pn=0;this.kin={k:NOKEY};this.mapOpen=false;this.wp=null;this.owned=new Set([0]);this.skinI=0;this.am={Pistol:48};this.own=new Set(['Pistol']);this.weaponName='Pistol';this.fireT=0;this.flash=0;this.driving=null;this.near=null;this.acc=0;this.last=performance.now();this.loc='';this.fc=0;this.ft=0;this.showFps=false;this.toastT=0;this.hadLock=false;
  const cv=$('gl'),r=this.r=new THREE.WebGLRenderer({canvas:cv,antialias:true});r.setPixelRatio(Math.min(devicePixelRatio,2));r.toneMapping=THREE.ACESFilmicToneMapping;r.toneMappingExposure=1.22;r.shadowMap.enabled=true;r.shadowMap.type=THREE.PCFSoftShadowMap;
  const scene=this.scene=new THREE.Scene(),cam=this.cam=new THREE.PerspectiveCamera(C.cam.fov,1,.5,900);
  this.inp=new Input();this.sfx=new Sfx();this.world=new World(scene);this.player=new Player(scene);this.rig=new Rig(cam);this.traffic=new Traffic(this.world);
  const R=this.world.R,L=this.world.L,hw=this.world.hw,cols=[0xc0392b,0x2c7be5,0xe8c547,0x2ecc71,0xecf0f1,0x8e44ad,0xe67e22,0x16a085];
  this.cars=[];const near=c=>{const i=U.clamp(Math.round((c+600)/C.step),0,10);return Math.abs(c-L[i])<hw(i)+8};
  const first=new Car(scene,0xff3d8b,null,'Sedan');first.x=20;first.z=6.4;first.h=Math.PI/2;this.cars.push(first);[0xe74c3c,0x2c7be5,0xf1c40f].forEach((cl,n)=>{const b=new Car(scene,cl,'motorcycle');b.x=30+n*4;b.z=8;b.h=Math.PI/2;this.cars.push(b)});
  for(let n=1;n<C.npc.parked;n++){const c=new Car(scene,cols[Math.floor(R()*8)],null,NPCM[Math.floor(Math.random()*NPCM.length)]),i=Math.floor(R()*11),side=R()<.5?1:-1;let p=-560+R()*1120;while(near(p))p=-560+R()*1120;
   if(R()<.5){c.x=L[i]+(hw(i)-1.6)*side;c.z=p;c.h=side>0?Math.PI:0}else{c.z=L[i]+(hw(i)-1.6)*side;c.x=p;c.h=side>0?Math.PI/2:-Math.PI/2}this.cars.push(c)}
  for(let n=0;n<C.npc.n;n++){const c=new Car(scene,cols[Math.floor(R()*8)],null,NPCM[Math.floor(Math.random()*NPCM.length)]);let t=0;do{this.traffic.place(c,this.traffic.ri(),this.traffic.ri())}while(Math.hypot(c.x,c.z)<100&&t++<20);this.cars.push(c)}
  // tire smoke
  this.sg=new THREE.BufferGeometry();this.sp=new Float32Array(60*3).fill(-100);this.sl=new Float32Array(60);this.sg.setAttribute('position',new THREE.BufferAttribute(this.sp,3));this.si=0;
  const pts=new THREE.Points(this.sg,new THREE.PointsMaterial({color:0xcccccc,size:2.2,transparent:true,opacity:.45,depthWrite:false}));pts.frustumCulled=false;scene.add(pts);this.dp=new Float32Array(120*3).fill(-100);this.dl=new Float32Array(120);this.di=0;{const dg=new THREE.BufferGeometry();dg.setAttribute('position',new THREE.BufferAttribute(this.dp,3));this.dg=dg;const dpts=new THREE.Points(dg,new THREE.PointsMaterial({color:0xb9a37a,size:1,transparent:true,opacity:.55,depthWrite:false}));dpts.frustumCulled=false;scene.add(dpts)}
  this.mg=$('mini').getContext('2d');this.peds=new Peds(this.world,scene);
  this.mk=new THREE.Mesh(new THREE.CylinderGeometry(5,5,60,20,1,true),new THREE.MeshBasicMaterial({color:0xff2a2a,transparent:true,opacity:.35,side:THREE.DoubleSide,depthWrite:false,blending:THREE.AdditiveBlending,fog:false}));scene.add(this.mk);this.nextMission();this.peds.update(0,20,10,0);SHOPS.push({...SHOPDEF.air,id:'air',w:14,d:10,x:70,z:-722,mz:-723.5});this.buildShops();this.buildSkins();this.planes=[];
  this.fx=[];this.nit=100;this.over=false;this.ch=null;this.msls=[];this.flying=null;this.nearAir=null;this.punchT=0;this.pf=0;this.tl0=-1;this.tl1=-1;this.fl=[0,1].map(()=>{const m=new THREE.Mesh(new THREE.ConeGeometry(.25,2,8).rotateX(-Math.PI/2),new THREE.MeshBasicMaterial({color:0x66b0ff,transparent:true,opacity:.85,blending:THREE.AdditiveBlending,depthWrite:false,fog:false}));m.visible=false;scene.add(m);return m});this.bl=new THREE.PointLight(0xff8830,0,70);scene.add(this.bl);this.polT=0;this.mag={Pistol:12};this.att={};this.attOwn=new Set();this.rl=0;this.rlT=1;this.rlW='';this.god=false;this.rich=false;this.heli=null;this.aiming=false;this.sens=1;this.cb='';this.scopeFov=50;this.editing=false;this.binding=null;
  this.player.magM=new THREE.Mesh(new THREE.BoxGeometry(.06,.16,.08),new THREE.MeshStandardMaterial({color:0x111111}));this.player.magM.visible=false;this.player.g.add(this.player.magM);
  this.trs=[];const tg=new THREE.BoxGeometry(.05,.05,1),tm=new THREE.MeshBasicMaterial({color:0xffe08a,fog:false});for(let i=0;i<24;i++){const m=new THREE.Mesh(tg,tm);m.visible=false;m.life=0;scene.add(m);this.trs.push(m)}
  this.hl=[0,1].map(()=>{const l=new THREE.SpotLight(0xfff2d0,0,80,.55,.6,1);scene.add(l,l.target);return l});
  addEventListener('mousedown',e=>{if(e.button===0&&this.inp.locked&&this.state==='PLAYING'&&(!this.driving||this.driving.mytank))this.shoot()});$('mapc').addEventListener('click',e=>{const r=e.target.getBoundingClientRect();this.wp={x:(e.clientX-r.left)/r.width*2600-1300,z:(e.clientY-r.top)/r.height*2600-1300};this.toast('Waypoint set');this.drawMap()});
  addEventListener('resize',()=>this.resize());this.resize();this.mkRev();this.applyGfx();this.applyLang();this.renderMob();this.showMob();
  {let t=null;cv.addEventListener('pointerdown',e=>{if(e.pointerType==='touch')t={id:e.pointerId,x:e.clientX,y:e.clientY}});cv.addEventListener('pointermove',e=>{if(t&&e.pointerId===t.id&&this.state==='PLAYING'){this.inp.dx+=(e.clientX-t.x)*1.4;this.inp.dy+=(e.clientY-t.y)*1.4;t.x=e.clientX;t.y=e.clientY}});addEventListener('pointerup',e=>{if(t&&e.pointerId===t.id)t=null})}
  $('bStart').onclick=()=>this.resume();cv.addEventListener('click',()=>{if(this.state==='PLAYING'&&S.mode==='pc'&&!this.shopOpen&&!this.mapOpen&&!document.pointerLockElement)this.relock()});$('bSet').onclick=()=>this.openSet();
  document.addEventListener('pointerlockchange',()=>{const l=document.pointerLockElement===cv;this.inp.locked=l;if(l)this.hadLock=true;else if(this.state==='PLAYING'&&this.hadLock&&!this.shopOpen&&!this.mapOpen)this.pause();if(!l)this.hadLock=false});
  $('shop').querySelectorAll('button').forEach(b=>b.addEventListener('click',()=>this.buyItem(b.dataset.item)));
  this.cv=cv;requestAnimationFrame(t=>this.loop(t));setTimeout(()=>{try{if(!this.xin)this.xi()}catch(e){console.error('preload',e)}try{this.r.compile(this.scene,this.cam)}catch(e){}},60)}
 resize(){const w=innerWidth,h=innerHeight;this.r.setSize(w,h,false);this.cam.aspect=w/h;this.cam.updateProjectionMatrix()}
 resume(){this.state='PLAYING';$('screen').style.display='none';this.sfx.init();this.applyGfx();this.showMob();this.last=performance.now();try{if(S.mode!=='pc')throw 0;const p=this.cv.requestPointerLock();if(p&&p.catch)p.catch(()=>{})}catch(e){}}
 pause(){if(this.state!=='PLAYING')return;this.state='PAUSED';this.inp.k={};$('sub').textContent=tr('Paused');$('bStart').textContent=tr('Resume GTA_elfo');$('screen').style.display='flex';this.showMob()}
 onKey(c){if(c==='Escape'&&this.state==='PLAYING'&&(this.mapOpen||this.shopOpen)){if(this.mapOpen)this.toggleMap();else this.closeShop();return}if(c==='F3'){this.showFps=!this.showFps;$('fps').style.display=this.showFps?'block':'none'}
  else if(c==='Escape'||c==='KeyP'){if(this.state==='PLAYING')this.pause();else if(this.state==='PAUSED'&&c==='KeyP')this.resume()}
  else if(c==='KeyE'&&this.state==='PLAYING')this.xe();    else if(c==='KeyF'&&this.state==='PLAYING')this.toggleCar();
   else if(c==='KeyB'&&this.state==='PLAYING')this.toggleShop();
   else if(c==='KeyJ'&&this.state==='PLAYING')this.shoot();
   else if(c==='KeyK'&&this.state==='PLAYING')this.punch();
   else if(c==='KeyX'&&this.state==='PLAYING'){if(this.c4.length)this.detonateC4();else this.placeC4();}
   else if(c==='KeyQ'&&this.state==='PLAYING'){const l=this.list();this.weaponName=l[(l.indexOf(this.weaponName)+1)%l.length];this.toast(this.weaponName)}
   else if(/^Digit[0-9]$/.test(c)&&this.state==='PLAYING')this.equip(+c.slice(5));
   else if(c==='KeyM'&&this.state==='PLAYING'&&!this.shopOpen)this.toggleMap();
   else if(c==='KeyR'&&this.state==='PLAYING'&&this.driving){this.radio=(this.radio+1)%4;this.sfx.radio(this.radio);this.toast(this.radio?'♪ '+RADIO[this.radio].name:'Radio off')}
   else if(c==='KeyR'&&this.state==='PLAYING')this.reload();else if(c==='KeyV'&&this.state==='PLAYING'&&this.driving&&this.driving.air&&this.driving.y<=0){this.driving.vy=6.5;this.sfx.beep(200)}else if(c==='KeyH'&&this.state==='PLAYING')this.sfx.beep(240)} 
  relock(){try{const p=this.cv.requestPointerLock();if(p&&p.catch)p.catch(()=>{})}catch(e){}}
  closeShop(){this.shopOpen=false;$('shop').style.display=$('skin').style.display='none';this.relock()}
  toggleShop(){if(this.shopOpen){this.closeShop();return}if(this.mapOpen)return;const s=this.nearShop;if(!s){this.toast('Walk into a shop marker (map: M)');return}
   this.shopOpen=s.id;this.buildShop(s.id);document.exitPointerLock()}
  toggleMap(){this.mapOpen=!this.mapOpen;$('mapv').style.display=this.mapOpen?'flex':'none';if(this.mapOpen){document.exitPointerLock();this.drawMap()}else this.relock()}
  drawMap(){const cv=$('mapc'),n=Math.floor(Math.min(innerWidth,innerHeight)*.86);if(cv.width!==n)cv.width=cv.height=n;const g=cv.getContext('2d'),k=n/2600,P=v=>(v+1300)*k;g.drawImage(this.world.mm,0,0,n,n);
   g.font='bold '+Math.max(12,n/42|0)+'px Rajdhani,sans-serif';g.textAlign='center';g.fillStyle='rgba(225,232,245,.85)';for(const l of MAPLBL)g.fillText(l[0],P(l[1]),P(l[2]));g.font=Math.max(16,n/26|0)+'px sans-serif';g.fillText('\u2708',P(0),P(-600));
   const dot=(wx,wz,col,r,t)=>{g.fillStyle=col;g.beginPath();g.arc(P(wx),P(wz),r,0,7);g.fill();if(t){g.fillStyle='#fff';g.fillText(t,P(wx),P(wz)-r-4)}};
   for(const o of this.cars)if(o.type==='police'||o.type==='tank')dot(o.x,o.z,'#4da3ff',3);
   for(const q of SHOPS)dot(q.x,q.mz,q.css,6,q.name);for(const o of POI)dot(o.x,o.z,o.c,6,o.t);dot(0,-641,'#ffffff',7,'AIRPORT');dot(this.mis.x,this.mis.z,'#ff3030',7,'MISSION');if(this.wp)dot(this.wp.x,this.wp.z,'#ff4bd8',6,'WAYPOINT');
   const f=this.driving||this.player,h=this.driving?this.driving.h:this.player.face;g.save();g.translate(P(f.x),P(f.z));g.rotate(Math.PI-h);g.fillStyle='#36f1ff';g.strokeStyle='#000';g.beginPath();g.moveTo(0,-9);g.lineTo(-6,7);g.lineTo(6,7);g.closePath();g.fill();g.stroke();g.restore()}
  buildShops(){const w=this.world,M=(c,r=.8)=>new THREE.MeshStandardMaterial({color:c,roughness:r});
   const add=(o,x,y,z)=>{o.position.set(x,y,z);o.castShadow=o.receiveShadow=true;this.scene.add(o);return o},bx=(a,b,c,m,x,y,z)=>add(new THREE.Mesh(new THREE.BoxGeometry(a,b,c),m),x,y,z),
    solid=(x0,x1,z0,z1)=>{const q={x0,x1,z0,z1,h:5};w.boxes.push(q);w.grid.add(q)},
    man=(sh,pn,sk,x,z,ry)=>{const g=new THREE.Group(),p=(a,b,c,m,px,py)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(a,b,c),m);o.position.set(px,py,0);o.castShadow=true;g.add(o)};
     p(.6,.7,.35,M(sh),0,1.35);p(.4,.4,.4,M(sk),0,1.95);p(.25,1,.25,M(pn),.15,.5);p(.25,1,.25,M(pn),-.15,.5);p(.2,.7,.2,M(sh),.4,1.3);p(.2,.7,.2,M(sh),-.4,1.3);g.position.set(x,0,z);g.rotation.y=ry;this.scene.add(g)};
   for(const s of SHOPS){const x=s.x,z=s.z,hw=s.w/2,z0=z-s.d/2,z1=z+s.d/2,wm=M(s.col);
    bx(s.w,.1,s.d,M(0x2b2d33,.9),x,.06,z);bx(s.w,.4,s.d,wm,x,5.2,z);bx(s.w,5,.4,wm,x,2.5,z1-.2);bx(.4,5,s.d,wm,x-hw+.2,2.5,z);bx(.4,5,s.d,wm,x+hw-.2,2.5,z);
    solid(x-hw,x+hw,z1-.4,z1);solid(x-hw,x-hw+.4,z0,z1);solid(x+hw-.4,x+hw,z0,z1);
    const t=w.tex(256,64,(g,W,H)=>{g.fillStyle='#0b1022';g.fillRect(0,0,W,H);g.strokeStyle=s.css;g.lineWidth=4;g.strokeRect(3,3,W-6,H-6);g.fillStyle=s.css;g.font='bold 30px sans-serif';g.textAlign='center';g.fillText(s.name,W/2,43)});
    const sg=new THREE.Mesh(new THREE.PlaneGeometry(s.w-1,2.2),new THREE.MeshBasicMaterial({map:t}));sg.position.set(x,6.5,z0-.05);sg.rotation.y=Math.PI;this.scene.add(sg);
    
    if(s.id==='gun'||s.id==='att'){bx(8,1.1,1.1,M(0x4a3a2a),x,.6,z1-3);solid(x-4,x+4,z1-3.55,z1-2.45);bx(10,2.6,.1,M(0x1a1c22),x,2.7,z1-.5);
     for(let i=0;i<6;i++)bx(1.3,.14,.12,M(i%2?0x3a3a42:0x22242a),x-4.2+i*1.68,3.4-(i%2)*.9,z1-.62);man(0x8a2b2b,0x222222,0xc68c62,x,z1-1.8,Math.PI)}
    else if(s.id==='skin'){for(let i=0;i<8;i++)bx(.5,1.2,.15,M(SKINS[i].sh),x-5+i*1.4,3,z1-.6);man(SKINS[3].sh,SKINS[3].pn,0xe0b090,x-4,z1-2,Math.PI);man(SKINS[6].sh,SKINS[6].pn,0xc68c62,x,z1-2,Math.PI);man(SKINS[7].sh,SKINS[7].pn,0x8d5a3b,x+4,z1-2,Math.PI)}
    else if(s.id==='arena'){man(0xff7a3d,0x222222,0xc68c62,x-3,z1-2,Math.PI);man(0xc0392b,0x222222,0x8d5a3b,x+3,z1-2,Math.PI)}
    else{const mo=s.id==='moto',d=new Car(this.scene,mo?0xd10000:0xf2c200,mo?'motorcycle':null,mo?'Ducati':'Lambo');d.x=x;d.z=z+.5;d.h=2.4;d.step(0,0,0,true,false);man(0x333333,0x222222,0xc68c62,x+4.5,z1-1.8,Math.PI)}
    const mk=new THREE.Mesh(new THREE.CylinderGeometry(2.5,2.5,40,16,1,true),new THREE.MeshBasicMaterial({color:new THREE.Color(s.css),transparent:true,opacity:.3,side:THREE.DoubleSide,depthWrite:false,blending:THREE.AdditiveBlending,fog:false}));mk.position.set(x,20,s.mz);this.scene.add(mk)}}
  buildSkins(){const e=$('skin');e.innerHTML='<h2>URBAN THREADS</h2><p>Pick an outfit. B closes the store.</p><div class="shopgrid"></div>';const gr=e.lastChild;
   SKINS.forEach((k,i)=>{const b=document.createElement('button');b.textContent=k.n+(this.owned.has(i)?(i===this.skinI?' ✓':''):' — $'+k.price);b.onclick=()=>this.pickSkin(i);gr.appendChild(b)});
   const x=document.createElement('button');x.textContent='Close store';x.onclick=()=>this.closeShop();gr.appendChild(x)}
  pickSkin(i){const k=SKINS[i];if(!this.owned.has(i)){if(this.money<k.price){this.toast('Not enough cash');return}this.cash(-k.price);this.owned.add(i)}this.skinI=i;const m=this.player.mat;m.sh.color.setHex(k.sh);m.pn.color.setHex(k.pn);m.sk.color.setHex(k.sk);this.toast(k.n+' equipped');this.buildSkins()}
  buyItem(n){if(n==='Close'){this.closeShop();return}const P={Pistol:300,SMG:900,Shotgun:1200,Rifle:1800,Sniper:2200,Grenade:250,C4:500,Armor:700,Medkit:150,Ammo:100,Motorcycle:1000},pr=P[n]||0;if(this.money<pr){this.toast('Not enough cash');return}
   if(n==='Ammo'&&!WEAP[this.weaponName]){this.toast('Equip a gun first');return}this.cash(-pr);const p=this.player;
   if(n==='Motorcycle'){const c=new Car(this.scene,0x26d6d0,'motorcycle');c.x=p.x+3;c.z=p.z;c.h=p.face;this.cars.push(c)}
   else if(n==='Armor')this.armor=100;else if(n==='Medkit')this.health=100;
   else if(n==='Ammo')this.am[this.weaponName]+=WEAP[this.weaponName].ammo;
   else if(WEAP[n]){this.own.add(n);this.am[n]=(this.am[n]||0)+WEAP[n].ammo;this.weaponName=n}else this.weaponName=n;
   this.toast(n+' purchased')}
  shoot(){this.xshot();if(this.flying){this.fireMsl();return}const dv=this.driving;if(dv&&dv.mytank){if(this.weaponCooldown>0)return;this.weaponCooldown=1.1;const tx=dv.x+Math.sin(dv.h)*38,tz=dv.z+Math.cos(dv.h)*38;this.tracer(dv.x,2.6,dv.z,tx,1,tz);this.boom(tx,tz,9,90);this.sfx.shot(1.6);return}const W=WEAP[this.weaponName]&&this.eff(this.weaponName);if(this.driving||this.weaponCooldown>0||this.dead>0)return;
   if(!W){if(this.weaponName==='Fist')this.punch();else this.toast('Buy a gun at Harbor Arms (B)');return}
   if(this.rl>0)return;const wn=this.weaponName;if(!(this.mag[wn]>0)){if(this.am[wn]>0)this.reload();else{this.toast('Out of ammo');this.weaponCooldown=.4}return}
   this.weaponCooldown=W.rate;this.mag[wn]--;this.quiet=W.sil;const p=this.player,f=this.rig.yaw;p.face=f;p.g.rotation.y=f;this.fireT=.8;this.flash=.05;this.sfx.shot(W.sil?.12:1);
   const tz=.7+W.len/2,mx=p.x+Math.sin(f)*tz-Math.cos(f)*.4,mz=p.z+Math.cos(f)*tz+Math.sin(f)*.4;p.flashM.position.set(-.4,1.6,tz+.1);let hitCar=null;
   for(let k=0;k<W.pel;k++){const a=f+(Math.random()-.5)*W.spr*(this.aiming?.5:1)*2,dx=Math.sin(a),dz=Math.cos(a);let best=W.rng;
    wall:for(let d=1.5;d<best;d+=1.5){const x=p.x+dx*d,z=p.z+dz*d;for(const b of this.world.grid.at(x,z))if(x>b.x0&&x<b.x1&&z>b.z0&&z<b.z1){best=d;break wall}}
    let car=null,ped=null;
    for(const c of this.cars){const rx=c.x-p.x,rz=c.z-p.z,al=rx*dx+rz*dz;if(al>0&&al<best&&Math.abs(rx*dz-rz*dx)<1.2){best=al;car=c}}
    for(const q of this.peds.p){if(q.dead>0)continue;const rx=q.x-p.x,rz=q.z-p.z,al=rx*dx+rz*dz;if(al>0&&al<best&&Math.abs(rx*dz-rz*dx)<.7){best=al;ped=q;car=null}}
    this.tracer(mx,1.55,mz,p.x+dx*best,1.3,p.z+dz*best);
    if(ped)this.hitPed(ped,W.dmg,true);else if(car){car.stun=2;car.vx+=dx*3;car.vz+=dz*3;hitCar=car;this.dmgCar(car,W.dmg*.8)}}
   if(hitCar&&this.wanted<1&&!W.sil)this.addWanted(1);this.quiet=false}
  punch(){if(this.driving||this.flying||this.dead>0||this.weaponCooldown>0)return;this.weaponCooldown=.4;this.punchT=.3;this.pf^=1;const p=this.player;p.face=this.rig.yaw;
   for(const q of this.peds.p)if(q.dead<=0&&q.down<=0&&Math.hypot(q.x-p.x,q.z-p.z)<2){this.hitPed(q,12,true);return}
   for(const c of this.cars)if(Math.hypot(c.x-p.x,c.z-p.z)<2.8){c.stun=2;c.vx+=Math.sin(p.face)*4;c.vz+=Math.cos(p.face)*4;if(this.wanted<1)this.addWanted(1);return}}
  hitPed(q,dmg,by){q.hp-=dmg;this.sfx.beep(120);q.free=true;if(q.hp<=0)this.killPed(q,by)}
  tracer(x0,y0,z0,x1,y1,z1){const t=this.trs.find(o=>!o.visible);if(!t)return;t.position.set((x0+x1)/2,(y0+y1)/2,(z0+z1)/2);t.scale.set(1,1,Math.hypot(x1-x0,y1-y0,z1-z0)||1);t.lookAt(x1,y1,z1);t.visible=true;t.life=.07}
  pedShoot(q){const p=this.driving||this.player;this.tracer(q.x,1.4,q.z,p.x+(Math.random()-.5)*2,1.2,p.z+(Math.random()-.5)*2);this.sfx.shot();if(Math.random()<.45)this.hurt(6)}
  jack(c){const q=this.peds.p.find(o=>o.dead<=0&&!o.free)||this.peds.p[0],sn=Math.sin(c.h),cs=Math.cos(c.h);q.x=c.x+cs*.9;q.z=c.z-sn*.9;q.free=true;q.down=3.5;q.dead=0;q.hp=100;q.vx=q.vz=0;q.jv=[cs*7,-sn*7];q.pull=.45;q.hd=c.h;q.fy=0;q.fv=0;q.rt=0;q.gun=Math.random()<.4;q.cd=1;
   if(c.type==='police'){c.type=null;c.body.material.emissive.setHex(0);this.policeSpawned=Math.max(0,this.policeSpawned-1);this.addWanted(2)}this.toast('Carjacked! The driver is on the ground');this.sfx.beep(180)}
  list(){return['Fist',...GUNS.filter(n=>this.own.has(n))]}
  equip(i){const l=this.list();if(l[i]){this.weaponName=l[i];this.toast(l[i])}}
  placeC4(){if(this.driving)return;const p=this.player;this.c4.push({x:p.x,z:p.z,t:0,mesh:new THREE.Mesh(new THREE.BoxGeometry(.25,.12,.25),new THREE.MeshStandardMaterial({color:0x222222,emissive:0x551100}))});const o=this.c4[this.c4.length-1];o.mesh.position.set(o.x,.12,o.z);this.scene.add(o.mesh);this.toast('C4 placed — press X again to detonate')}
  detonateC4(){if(!this.c4.length)return;for(const b of this.c4){this.boom(b.x,b.z,9,90);this.scene.remove(b.mesh)}this.c4=[];this.addWanted(2);this.toast('C4 detonated')}
  addWanted(n){this.setWanted(this.wanted+n);this.cops()}
  setWanted(n){n=U.clamp(n,0,5);this.wanted=n;this.evade=0;if(n<3&&this.heli){this.scene.remove(this.heli.g);this.heli=null}$('wanted').textContent='★'.repeat(n)+'☆'.repeat(5-n);if(n)return;const p=this.player;
   for(const c of this.cars.slice()){if(c.type==='tank'){this.scene.remove(c.m);this.cars.splice(this.cars.indexOf(c),1)}else if(c.type==='police'){c.type=null;c.body.material.emissive.setHex(0);this.traffic.respawn(c,p.x,p.z)}}this.policeSpawned=0;this.tankSpawned=false}
  spawnPolice(){const c=new Car(this.scene,0x202a42,'police');this.traffic.respawn(c,this.player.x,this.player.z);this.cars.push(c);this.policeSpawned++;this.sfx.beep(520)}
  killPed(q,by){q.dead=10;this.sfx.beep(90);if(by){if(this.ch&&this.ch.type==='kill')this.ch.n++;this.cash(20+Math.round(Math.random()*120));if(this.wanted<2&&!this.quiet)this.addWanted(1)}}
  cash(n){if(this.rich&&n<0)n=0;this.money+=n;$('money').textContent='$ '+this.money.toLocaleString();if(n>0)this.toast('+$'+n)}
  hurt(n){if(this.dead>0||this.god)return;if(this.armor>0){const a=Math.min(this.armor,n*.7);this.armor-=a;n-=a}this.health-=n;this.hitT=.4;if(this.health<=0){this.health=0;this.die('WASTED','#d4d4d4',Math.min(this.money,500))}}

 xL(a,b){return S.lang==='fa'?b:a}
 xtp(x,z,yaw,zone){const p=this.player;p.x=x;p.z=z;p.y=0;p.vx=p.vz=0;p.face=yaw;this.rig.yaw=yaw;this.rig.init=false;this.zone=zone;this.sfx.beep(520)}
 xnpc(c,x,z,ry,gun,tint){const sc=this.scene,M=k=>new THREE.MeshStandardMaterial({color:k,roughness:.8}),H=mkHuman(M(c),M(tint||0xe0b090),M(0x22252c),M([0x1a1208,0x4a2a14,0xc9a227,0x777777][Math.floor(Math.random()*4)]));
  if(gun){const o=new THREE.Mesh(new THREE.BoxGeometry(.1,.12,.5),M(0x111111));o.position.set(.4,1.15,.35);H.g.add(o)}H.g.position.set(x,0,z);H.g.rotation.y=ry;sc.add(H.g);return{g:H.g,head:H.head,aL:H.aL,aR:H.aR,lL:H.lL,lR:H.lR,t:Math.random()*6,hp:60}}
 xan(n,dt,walk){n.t+=dt;const pl=this.player,gp=n.g.position,dx=pl.x-gp.x,dz=pl.z-gp.z,d=Math.hypot(dx,dz);
  if(!walk&&d<9)n.g.rotation.y=U.lerpA(n.g.rotation.y,Math.atan2(dx,dz),Math.min(1,dt*4));
  const s=walk?Math.sin(n.t*8)*.7:0;n.lL.rotation.x=s;n.lR.rotation.x=-s;n.aL.rotation.x=-s*.8+(walk?0:Math.sin(n.t*1.7)*.06);n.aR.rotation.x=s*.8+(walk?0:Math.cos(n.t*1.9)*.06);
  if(!walk&&!n.nw&&d<6)n.aR.rotation.x=-2.2+Math.sin(n.t*6)*.3;n.head.rotation.y=Math.sin(n.t*.9)*.25;gp.y=walk?Math.abs(Math.sin(n.t*8))*.06:Math.sin(n.t*2)*.015}
 xi(){const G=this,sc=this.scene,W=this.world,L=W.L,M=(c,r=.8,m=0)=>new THREE.MeshStandardMaterial({color:c,roughness:r,metalness:m}),Lg=(a,b)=>G.xL(a,b);
  this.xin=1;this.zone='city';this.xs=[];this.xn=[];this.xcp=[];this.xc=null;this.xj=null;this.xloot=-9999;this.xdoors=[];this.xg=[];this.xback={x:20,z:10};this.xparts=[];this.xneon();
  const bx=(w,h,d,c,x,y,z,sd,em)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),em?new THREE.MeshBasicMaterial({color:c}):M(c));o.position.set(x,y,z);o.castShadow=o.receiveShadow=true;sc.add(o);let q=null;if(sd){q={x0:x-w/2,x1:x+w/2,z0:z-d/2,z1:z+d/2,h:h+y};W.boxes.push(q);W.grid.add(q)}return{o,q}},
  P=(x,z,r,t,fn,cond)=>{const p={x,z,r,t,fn,if:cond};this.xs.push(p);return p},
  room=(cx,w,d,h,fl,wl,lc)=>{bx(w,.2,d,fl,cx,-.1,0);bx(w,.2,d,0x1b1d24,cx,h+.1,0);bx(w+1.2,h,.6,wl,cx,h/2,-d/2-.3,1);bx(w+1.2,h,.6,wl,cx,h/2,d/2+.3,1);bx(.6,h,d,wl,cx-w/2-.3,h/2,0,1);bx(.6,h,d,wl,cx+w/2+.3,h/2,0,1);const l=new THREE.PointLight(lc,1.4,w*1.6);l.position.set(cx,h-1,0);sc.add(l)},
  npc=(c,x,z,ry,gun,tint)=>{const n=this.xnpc(c,x,z,ry,gun,tint);this.xn.push(n);return n};
  const e1=document.createElement('div');e1.id='xp';e1.className='hud';e1.style.cssText='left:50%;bottom:30%;transform:translateX(-50%);display:none;color:#9dffb0;z-index:6';document.body.appendChild(e1);
  const e2=document.createElement('div');e2.id='xo';e2.className='hud';e2.style.cssText='left:16px;top:56px;display:none;color:#ffd24a;z-index:6';document.body.appendChild(e2);
  this.xm=new THREE.Mesh(new THREE.CylinderGeometry(1.6,1.6,80,14,1,true),new THREE.MeshBasicMaterial({color:0xffd24a,transparent:true,opacity:.4,side:THREE.DoubleSide,depthWrite:false,blending:THREE.AdditiveBlending,fog:false}));this.xm.visible=false;sc.add(this.xm);
  /* ---- OFFICE interior (x=1500) ---- */
  room(1500,30,22,6,0x6a5a48,0x8a8f99,0xfff0d0);bx(8,1,2.4,0x5a3a22,1500,.5,-7.6,1);bx(5,.9,2,0x2a4a7a,1489,.45,6,1);bx(5,.9,2,0x2a4a7a,1511,.45,6,1);bx(10,3,.1,0xc03070,1500,3.3,-10.6,0,1);bx(.8,2,.8,0x2a7a3a,1486,1,-9,1);bx(.8,2,.8,0x2a7a3a,1514,1,-9,1);bx(26,.15,.15,0x36f1ff,1500,5.6,0,0,1);
  const fx=npc(0x3a2a5a,1500,-5.4,0,0),ht=npc(0x1a1a1a,1491,-8,0,1,0x8d5a3b),dl=npc(0x4a5a2a,1509,-8,0,0,0xc68c62);
  P(1500,-5.4,3.6,()=>Lg('Press E — talk to Vince (heists)','E — صحبت با وینس (سرقت)'),()=>this.xgive('rob'));
  P(1491,-8,3.4,()=>Lg('Press E — talk to Mako (hits)','E — صحبت با ماکو (ترور)'),()=>this.xgive('kill'));
  P(1509,-8,3.4,()=>Lg('Press E — talk to Dutch (tank job)','E — صحبت با داچ (تانک)'),()=>this.xgive('tank'));
  P(1500,9.2,3,()=>Lg('Press E — leave the building','E — خروج از ساختمان'),()=>{const b=this.xback;this.xtp(b.x,b.z,0,'city')});
  /* ---- PRISON interior (x=1700) ---- */
  room(1700,44,30,6,0x55585f,0x6a6d74,0xcfe0ff);
  const bars=(x0,z0,x1,z1,n)=>{const gr=new THREE.Group();for(let i=0;i<=n;i++){const o=new THREE.Mesh(new THREE.BoxGeometry(.12,3.6,.12),M(0x222226,.4,.7));o.position.set(x0+(x1-x0)*i/n,1.8,z0+(z1-z0)*i/n);gr.add(o)}sc.add(gr);return gr};
  bars(1688,-15,1688,-9,8);bars(1678,-6,1688,-6,12);const dg=bars(1688,-9,1688,-6.4,4),dq=bx(.4,3.6,2.6,0x222226,1688,1.8,-7.7,1).q;this.xdoor={g:dg,q:dq,o:{x0:dq.x0,x1:dq.x1,z0:dq.z0,z1:dq.z1}};bx(.5,3.6,6,0x222226,1688,1.8,-12,1).o.visible=false;bx(10,3.6,.5,0x222226,1683,1.8,-6,1).o.visible=false;
  bx(2.2,.5,1,0x777777,1680.2,.45,-13,1);bx(1.2,.2,.9,0x777777,1679.8,.6,-9.4,1);bx(8,1,2,0x4a4a52,1712,.5,-10,1);bx(.2,3,.6,0x35c27a,1713,1.7,-13.8,0,1);bx(1,2.2,1,0x3a3a42,1720.5,1.1,12,1);bx(.3,4.2,6,0x44ffb0,1721.7,2.1,12,0,1);
  this.xg=[0,1].map(i=>{const n=this.xnpc(0x16264a,1704,i?5:-1,0,1);n.ph=i*3;n.r=i?9:12;n.z0=i?5:-1;n.walk=1;this.xn.push(n);return n});
  P(1680.4,-12,2.6,()=>Lg('Press E — search the loose brick','E — جستجوی آجر شل'),()=>{this.xj.open=1;this.xdoor.g.visible=false;const q=this.xdoor.q;q.x0=q.x1=q.z0=q.z1=9e9;this.toast(Lg('You found a spoon and dug the lock — the cell is open! Avoid the guards','قاشق پیدا کردی و قفل را باز کردی! از نگهبان‌ها دوری کن'))},()=>this.xj&&!this.xj.open);
  P(1712,-12,3.2,()=>Lg('Press E — take the guard keycard','E — برداشتن کارت نگهبان'),()=>{this.xj.key=1;this.toast(Lg('Keycard taken! Now reach the exit gate','کارت را برداشتی! به دروازه خروج برو'))},()=>this.xj&&this.xj.open&&!this.xj.key);
  P(1720,12,3.4,()=>Lg('Press E — exit gate','E — دروازه خروج'),()=>{if(this.xj.key){this.xj=null;this.xtp(14,12,0,'city');this.setWanted(0);this.big(Lg('ESCAPED!','فرار موفق!'),'','#9dffb0',3)}else this.toast(Lg('Gate locked — you need the keycard','دروازه قفل است — کارت لازم داری'))},()=>this.xj);
  /* ---- UNDERGROUND (x=1900) ---- */
  room(1900,60,12,4,0x2a2a30,0x3a3a40,0xff9a50);for(let i=0;i<4;i++){const o=new THREE.Mesh(new THREE.CylinderGeometry(.25,.25,60,8).rotateZ(Math.PI/2),M(0x884422,.6,.5));o.position.set(1900,3.4-i*.0,-5.4+i*.1);sc.add(o)}
  for(let i=0;i<6;i++)bx(1.6,1.6,1.6,i%2?0x6a4a2a:0x4a5a3a,1912+i*3,.8,-3.5+((i*7)%5)*.4,1);bx(2.5,2,2.5,0xd4a017,1926,1,2,1);
  const sm=npc(0x2a2a2a,1900,-3,0,1,0x8d5a3b);P(1900,-3,3.4,()=>Lg('Press E — talk to the Smuggler (heists)','E — صحبت با قاچاقچی (سرقت)'),()=>this.xgive('rob'));
  npc(0x4a1a1a,1890,-3,0,1,0x8d5a3b);P(1890,-3,3.2,()=>Lg('Press E — talk to Mako (hits)','E — صحبت با ماکو (ترور)'),()=>this.xgive('kill'));npc(0x2a4a2a,1908,-3,0,0,0xc68c62);P(1908,-3,3.2,()=>Lg('Press E — talk to Dutch (tank job)','E — صحبت با داچ (تانک)'),()=>this.xgive('tank'));P(1926,2,3.6,()=>Lg('Press E — loot the stash','E — غارت مخفیگاه'),()=>{const n=performance.now()/1000;if(n-this.xloot<600){this.toast(Lg('The stash is empty — come back later','مخفیگاه خالی است — بعداً بیا'));return}this.xloot=n;this.cash(15000);this.big(Lg('SECRET STASH','مخفیگاه مخفی'),'$ 15,000','#ffd24a',3)});
  P(1872.5,0,3,()=>Lg('Press E — climb the ladder','E — بالا رفتن از نردبان'),()=>{const b=this.xmh;this.xtp(b.x,b.z+3,0,'city')});
  bx(.3,4,1,0x888888,1870.4,2,0,0);
  /* manhole (secret entrance) */
  {const mx=L[4],mz=L[5]+30,o=new THREE.Mesh(new THREE.CylinderGeometry(1,1,.06,16),M(0x2a2a2e,.5,.8));o.position.set(mx,.07,mz);sc.add(o);this.xmh={x:mx,z:mz};
   P(mx,mz,2.4,()=>Lg('Press E — secret manhole','E — دریچه مخفی'),()=>this.xtp(1875,0,Math.PI/2,'und'))}
  /* ---- CASINO interior (x=2100) ---- */
  room(2100,44,30,7,0x6a1426,0x2a1030,0xffe2a8);bx(42,.03,28,0x7a1a2a,2100,.01,0,0,1);
  bx(40,.12,.12,0xff2d95,2100,6.6,-8,0,1);bx(40,.12,.12,0x2de2ff,2100,6.6,8,0,1);bx(4,.3,4,0xffe9a0,2100,6.3,0,0,1);
  for(const sx of[-1,1])for(const sz of[-1,1])bx(1,7,1,0xd4a017,2100+sx*20,3.5,sz*13.5,1);
  for(let i=0;i<8;i++){const x=2083+i*4.6;bx(1.4,2.4,1.1,0x22222a,x,1.2,-13.9,1);bx(1.1,.8,.1,[0xff2d95,0x2de2ff,0xffd12d,0x7dff3d][i%4],x,1.7,-13.3,0,1);P(x,-11.8,2.3,()=>Lg('Press E — slot machine ($1,000 · 777 = $50,000)','E — اسلات ($1,000 · 777 = $50,000)'),()=>this.xslot())}
  bx(10,1,6,0x0a5a2a,2108,.5,1,1);bx(9.4,.05,5.4,0x16803a,2108,1.02,1,0,1);bx(1.8,.3,1.8,0xd4a017,2105,1.15,0,0,1);npc(0xaa1133,2108,-2.5,0,0,0xf1cfb0);
  P(2104.3,5.6,1.8,()=>Lg('Press E — roulette: $2,000 on RED','E — رولت: ۲۰۰۰ دلار روی قرمز'),()=>this.xroul('red'));
  P(2108,5.6,1.8,()=>Lg('Press E — roulette: $500 on GREEN (pays 36x)','E — رولت: ۵۰۰ دلار روی سبز (۳۶ برابر)'),()=>this.xroul('green'));
  P(2111.7,5.6,1.8,()=>Lg('Press E — roulette: $2,000 on BLACK','E — رولت: ۲۰۰۰ دلار روی مشکی'),()=>this.xroul('black'));
  bx(8,1,4.5,0x14423a,2090,.5,1.5,1);bx(7.4,.05,3.9,0x1c6b4e,2090,1.02,1.5,0,1);npc(0x111111,2090,-1.2,0,0,0xc68c62);
  P(2090,5.3,2.8,()=>Lg('Press E — blackjack ($3,000 bet)','E — بلک‌جک (شرط ۳۰۰۰ دلار)'),()=>this.xbj());
  npc(0x111111,2096,10,0,0,0xc68c62);npc(0x222233,2105,10,0,0,0x8d5a3b);
  P(2100,12.4,3,()=>Lg('Press E — leave the casino','E — خروج از کازینو'),()=>{const b=this.xback;this.xtp(b.x,b.z,0,'city')});

  /* ---- overpass over the avenue ---- */
  {const ox=L[6],oz=L[7];OV={x:ox,a:oz-90,b:oz-30,c:oz+30,d:oz+90,h:7,hw:7.6};const as=M(0x2e3036,.95),rl=M(0x8a8f99,.5,.4),yl=new THREE.MeshBasicMaterial({color:0xffd24a}),seg=(z0,z1,h0,h1)=>{const dz=z1-z0,dh=h1-h0,len=Math.hypot(dz,dh),g=new THREE.Group(),a=Math.atan2(dh,dz);g.position.set(ox,(h0+h1)/2-.25,(z0+z1)/2);g.rotation.x=-a;
    const m=(w,h,d,mt,x,y,z)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),mt);o.position.set(x,y,z);o.castShadow=o.receiveShadow=true;g.add(o)};m(15.2,.5,len,as,0,0,0);m(.3,.9,len,rl,7.5,.7,0);m(.3,.9,len,rl,-7.5,.7,0);m(.25,.06,len,yl,0,.28,0);sc.add(g)};
   seg(oz-90,oz-30,0,7);seg(oz-30,oz+30,7,7);seg(oz+30,oz+90,7,0);
   for(const sx of[-1,1])for(const sz of[-1,1]){const px=ox+sx*8,pz=oz+sz*16,p=new THREE.Mesh(new THREE.CylinderGeometry(.8,1,6.6,10),M(0x777b84,.8));p.position.set(px,3.3,pz);p.castShadow=true;sc.add(p);const q={x0:px-.9,x1:px+.9,z0:pz-.9,z1:pz+.9,h:7};W.boxes.push(q);W.grid.add(q)}
   bx(18,.3,.3,0xffd24a,ox,7.2,oz-30,0,1);bx(18,.3,.3,0xffd24a,ox,7.2,oz+30,0,1)}
  this.xcity();/* ---- posters ---- */
  this.xpo=[];const saved=ld('gtaelfo_p',{a:[]}).a,pp=[[1,2],[2,5],[4,1],[5,6],[6,3]];
  pp.forEach((q,i)=>{const px=L[q[0]]+10.5,pz=L[q[1]]+60,c=document.createElement('canvas');c.width=512;c.height=256;this.xdef(c);const t=new THREE.CanvasTexture(c),m=new THREE.Mesh(new THREE.PlaneGeometry(10,5),new THREE.MeshBasicMaterial({map:t,side:THREE.DoubleSide}));
   m.position.set(px-.2,9.5,pz);m.rotation.y=-Math.PI/2;sc.add(m);bx(.3,5.4,10.4,0x15181e,px,9.5,pz);bx(.3,7,.3,0x30343c,px,3.5,pz-3.5);bx(.3,7,.3,0x30343c,px,3.5,pz+3.5);this.xpo[i]={c,t};if(saved[i])this.xposter(i,saved[i])})}
 xdef(c){const g=c.getContext('2d'),gr=g.createLinearGradient(0,0,512,256);gr.addColorStop(0,'#1b0b3a');gr.addColorStop(1,'#0b3a4a');g.fillStyle=gr;g.fillRect(0,0,512,256);g.strokeStyle='#36f1ff';g.lineWidth=6;g.strokeRect(8,8,496,240);g.fillStyle='#ff3d8b';g.font='bold 64px sans-serif';g.textAlign='center';g.fillText('YOUR AD',256,125);g.fillStyle='#36f1ff';g.fillText('HERE',256,200)}
 xposter(i,u){const P=this.xpo&&this.xpo[i];if(!P)return;if(!u){this.xdef(P.c);P.t.needsUpdate=true;return}const im=new Image();im.onload=()=>{P.c.getContext('2d').drawImage(im,0,0,512,256);P.t.needsUpdate=true};im.src=u}
 xfile(i,f,clr){const st=ld('gtaelfo_p',{a:[]}).a;if(clr){st[i]=null;sv('gtaelfo_p',{a:st});if(this.xin)this.xposter(i,null);return}if(!f)return;const r=new FileReader();r.onload=()=>{const im=new Image();im.onload=()=>{const c=document.createElement('canvas');c.width=512;c.height=256;const g=c.getContext('2d'),s=Math.max(512/im.width,256/im.height),w=im.width*s,h=im.height*s;g.drawImage(im,(512-w)/2,(256-h)/2,w,h);const u=c.toDataURL('image/jpeg',.82),a=ld('gtaelfo_p',{a:[]}).a;a[i]=u;sv('gtaelfo_p',{a});if(this.xin)this.xposter(i,u);this.toast(this.xL('Poster '+(i+1)+' updated','پوستر '+(i+1)+' به‌روز شد'))};im.src=r.result};r.readAsDataURL(f)}
 xgive(k){if(this.xc){this.toast(this.xL('Finish your current challenge first','اول چالش فعلی را تمام کن'));return}const rw={rob:7000,kill:4000,tank:9000}[k];this.xc={k,t:k==='tank'?300:240,rw,tg:null};
  if(k==='rob'){let j,t=0;do{j=Math.floor(Math.random()*this.xdoors.length)}while(this.xdoors.length>1&&j===this.xcur&&t++<20);this.xc.door=j}
  this.toast({rob:this.xL('Job: rob the marked building (yellow beacon). Leave and go there.','کار: از ساختمان علامت‌خورده سرقت کن (نور زرد).'),kill:this.xL('Hit: a man is marked. Take him out.','ترور: یک نفر علامت‌خورده، او را بزن.'),tank:this.xL('Job: destroy the marked tank!','کار: تانک علامت‌خورده را نابود کن!')}[k]);this.sfx.beep(660)}
 xchal(dt){const c=this.xc,o=$('xo'),m=this.xm;if(!c){o.style.display='none';m.visible=false;return}
  c.t-=dt;if(c.t<=0){this.toast(this.xL('Challenge failed: time is up','چالش شکست خورد: زمان تمام شد'));this.xc=null;return}
  let tx=null,tz=null,txt='';const pl=this.player;
  if(c.k==='rob'){const d=this.xdoors[c.door];if(d){tx=d.x;tz=d.z;txt=this.xL('Rob: ','سرقت: ')+d.n}}
  else if(c.k==='kill'){txt=this.xL('Hit: eliminate the target','ترور: هدف را بزن');if(!c.tg&&this.zone==='city'){let b=1e9;for(const q of this.peds.p){if(q.dead>0||q.free)continue;const d=Math.hypot(q.x-pl.x,q.z-pl.z);if(d>40&&d<220&&d<b){b=d;c.tg=q}}}
   if(c.tg){tx=c.tg.x;tz=c.tg.z;if(c.tg.dead>0)return this.xdone()}}
  else{txt=this.xL('Destroy the tank','تانک را نابود کن');if(!c.tg&&this.zone==='city'){const t=new Car(this.scene,0x536b4a,'tank');t.x=pl.x+80;t.z=pl.z+60;t.h=0;this.cars.push(t);c.tg=t;this.addWanted(1)}
   if(c.tg){if(c.tg.wreck)return this.xdone();if(!this.cars.includes(c.tg))c.tg=null;else{tx=c.tg.x;tz=c.tg.z}}}
  o.style.display='block';o.textContent=txt+' · '+(c.t|0)+'s · $'+c.rw;if(tx!=null){m.visible=true;m.position.set(tx,40,tz)}else m.visible=false}
 xdone(){const c=this.xc;this.cash(c.rw);this.big(this.xL('CHALLENGE COMPLETE','چالش کامل شد'),'$ '+c.rw.toLocaleString(),'#9dffb0',3);this.sfx.beep(880);this.xc=null}
 xguards(dt){if(this.zone!=='pri'||!this.xj)return;const pl=this.player;for(const g of this.xg){g.ph+=dt*.5;const x=1704+Math.sin(g.ph)*g.r;g.g.position.x=x;g.g.position.z=g.z0;g.g.rotation.y=Math.cos(g.ph)>0?Math.PI/2:-Math.PI/2;
   if(!this.driving&&pl.x>1689&&Math.hypot(x-pl.x,g.z0-pl.z)<4.2&&this.dead<=0){this.toast(this.xL('A guard spotted you! Back to the cell','نگهبان تو را دید! بازگشت به سلول'));this.xtp(1684,-10.5,Math.PI/2,'pri');this.xj.t=Math.max(this.xj.t,60);this.xj.key=0;break}}
  this.xj.t-=dt;if(this.xj.t<=0){this.xj=null;this.xtp(14,12,0,'city');this.toast(this.xL('You served your time — released','دوران حبس تمام شد — آزاد شدی'))}}
 xjail(){const q=this.xdoor.q,o=this.xdoor.o;q.x0=o.x0;q.x1=o.x1;q.z0=o.z0;q.z1=o.z1;this.xdoor.g.visible=true;this.xj={t:150,key:0,open:0};this.xtp(1684,-10.5,Math.PI/2,'pri');this.setWanted(0);this.toast(this.xL('PRISON: find a way out before your sentence ends (150s)','زندان: قبل از پایان حکم (۱۵۰ ثانیه) راه فرار پیدا کن'))}
 xcops(dt){const pl=this.player,w=this.wanted,tgt=this.driving||pl;const al=this.xcp.filter(c=>!c.gone);if(al.length!==this.xcp.length){for(const c of this.xcp)if(c.gone)this.scene.remove(c.g);this.xcp=al}
  for(const c of al){if(c.dead){c.dt+=dt;c.g.rotation.x=Math.min(1.5,c.dt*4);if(c.dt>6){c.gone=1;c.g.visible=false}continue}
   if(w<=0||this.zone!=='city'){c.gone=1;c.g.visible=false;continue}
   const gp=c.g.position,dx=tgt.x-gp.x,dz=tgt.z-gp.z,d=Math.hypot(dx,dz);c.g.rotation.y=U.lerpA(c.g.rotation.y,Math.atan2(dx,dz),Math.min(1,dt*6));
   if(d>90){c.gone=1;c.g.visible=false;continue}
   const mv=d>11;if(mv){const nx=gp.x+dx/d*4.6*dt,nz=gp.z+dz/d*4.6*dt;if(this.world.free(nx,gp.z,.5))gp.x=nx;if(this.world.free(gp.x,nz,.5))gp.z=nz}
   for(const k of this.cars){if(k.wreck)continue;const ex=gp.x-k.x,ez=gp.z-k.z,ed=Math.hypot(ex,ez);if(ed<2.5&&ed>.01){if(k===this.driving&&Math.abs(k.sp)>7)c.hp=0;else{gp.x=k.x+ex/ed*2.5;gp.z=k.z+ez/ed*2.5}}}this.xan(c,dt,mv);c.g.rotation.y=U.lerpA(c.g.rotation.y,Math.atan2(dx,dz),1);
   if(!mv&&this.dead<=0){c.cd-=dt;if(c.cd<=0){c.cd=1.1;this.tracer(gp.x,1.4,gp.z,tgt.x+(Math.random()-.5)*2,1.2,tgt.z+(Math.random()-.5)*2);this.sfx.shot(.7);if(Math.random()<.5)this.hurt(5)}}
   if(this.driving&&Math.abs(this.driving.sp)>9&&d<2.6){c.hp=0}
   if(c.hp<=0){c.dead=1;c.dt=0;this.addWanted(0)}}
  if(w>0&&this.zone==='city'&&this.state==='PLAYING'){this.xcT=(this.xcT||0)-dt;if(this.xcT<=0&&al.filter(c=>!c.dead).length<Math.min(6,w*2)){this.xcT=2.5;for(const o of this.cars){if(o.type!=='police'||o.wreck)continue;const d=Math.hypot(o.x-tgt.x,o.z-tgt.z);if(d<45&&d>6&&Math.abs(o.sp)<4){const n=this.xnpc(0x16264a,o.x+Math.cos(o.h)*1.8,o.z-Math.sin(o.h)*1.8,0,1);n.cd=.8;n.dead=0;this.xcp.push(n);break}}}}}
 xshot(){if(this.driving||this.flying||this.weaponCooldown>0||this.dead>0||this.zone!=='city')return;const Wp=WEAP[this.weaponName];if(!Wp||!(this.mag[this.weaponName]>0)||this.rl>0)return;const pl=this.player,y=this.rig.yaw,fx=Math.sin(y),fz=Math.cos(y);
  for(const c of this.xcp){if(c.gone||c.dead)continue;const dx=c.g.position.x-pl.x,dz=c.g.position.z-pl.z,d=Math.hypot(dx,dz);if(d>Wp.rng||d<.5)continue;const f=(dx*fx+dz*fz)/d;if(f>0&&d*Math.sqrt(Math.max(0,1-f*f))<1.3){c.hp-=Wp.dmg*Wp.pel}}}
 xt(dt){if(!this.xin)this.xi();this.xex(dt);if(this.state!=='PLAYING')return;const pl=this.player,on=!this.driving&&!this.flying&&this.dead<=0;
  for(const n of this.xn)this.xan(n,dt,n.walk);this.xguards(dt);this.xcops(dt);this.xchal(dt);this.xentU(dt);this.xcar(dt);
  let b=null,bd=1e9;if(on)for(const p of this.xs){const d=Math.hypot(p.x-pl.x,p.z-pl.z);if(d<p.r&&d<bd&&(!p.if||p.if())){b=p;bd=d}}
  this.xnear=b;const e=$('xp');if(b){e.textContent=typeof b.t==='function'?b.t():b.t;e.style.display='block'}else e.style.display='none'}
  xthug(dt){const pl=this.player,th=this.xth;
  if(!th){const d=this.driving;this.xcd=(this.xcd||0)-dt;if(!d||this.zone!=='city'||d.type==='tank'||d.type==='mytank'||d.wreck||Math.abs(d.sp||0)>5||this.xcd>0)return;this.xtm=(this.xtm||0)+dt;if(this.xtm<4)return;this.xtm=0;if(Math.random()>.3)return;
   const car=d;this.toggleCar();const n=this.xnpc(0x7a1f1f,car.x+Math.cos(car.h)*2.5,car.z-Math.sin(car.h)*2.5,0,0,0x9a6a4a);this.xth={n,car,ph:'run',t:0,hit:0};this.xcd=60;this.toast(this.xL('A thug dragged you out of your car!','یه گردن‌کلفت تو را از ماشین بیرون کشید!'));this.sfx.beep(180);return}
  const n=th.n,gp=n.g.position,car=th.car;th.t+=dt;
  if(th.ph==='run'||th.ph==='beat'){const dx=pl.x-gp.x,dz=pl.z-gp.z,d=Math.hypot(dx,dz);n.g.rotation.y=U.lerpA(n.g.rotation.y,Math.atan2(dx,dz),Math.min(1,dt*8));
   if(d>1.5&&th.ph==='run'){gp.x+=dx/d*5.5*dt;gp.z+=dz/d*5.5*dt;this.xan(n,dt,1);if(th.t>8)th.ph='steal'}
   else{if(th.ph==='run'){th.ph='beat';th.t=0}this.xan(n,dt,0);n.aR.rotation.x=-1.6+Math.sin(th.t*14)*.9;n.aL.rotation.x=-1.6+Math.cos(th.t*14)*.9;th.hit-=dt;if(th.hit<=0){th.hit=.55;this.hurt(6);this.sfx.beep(140);pl.vx+=dx/Math.max(d,.1)*-2;pl.vz+=dz/Math.max(d,.1)*-2}if(th.t>2.6){th.ph='steal';th.t=0}}}
  else if(th.ph==='steal'){const dx=car.x-gp.x,dz=car.z-gp.z,d=Math.hypot(dx,dz);n.g.rotation.y=Math.atan2(dx,dz);if(d>1.8){gp.x+=dx/d*6*dt;gp.z+=dz/d*6*dt;this.xan(n,dt,1)}else{n.g.visible=false;th.ph='drive';th.t=0;this.toast(this.xL('He stole your car!','ماشینت را دزدید!'));car.ai=false}}
  else{car.step(dt,1,Math.sin(th.t*.8)*.35,false,false);if(th.t>9||car.wreck){this.xth=null}}}
 xdim(c){const d=c.model&&CARMODELS[c.model]?CARMODELS[c.model].d:null;return d?{L:d[0],w:d[1],hh:d[3],dh:d[4],z1:d[5],z2:d[6],z3:d[7]}:{L:4.4,w:1.8,hh:.85,dh:.95,z1:.6,z2:-.2,z3:-.7}}
 xdent(c,px,pz,mag){const D=this.xdim(c);if(!c.dg){c.dg={h:0,t:0,l:0,r:0};c.body.geometry=c.body.geometry.clone();c.dg0=c.body.geometry.attributes.position.array.slice()}
  const g=c.body.geometry,pa=g.attributes.position,co=g.attributes.color,a=pa.array,R=1.35,m=Math.min(.6,mag*.07),l=Math.hypot(px,pz)||1,nx=-px/l,nz=-pz/l;
  for(let i=0;i<pa.count;i++){const x=a[i*3],y=a[i*3+1],z=a[i*3+2],d=Math.hypot(x-px,z-pz);if(d<R){const f=Math.pow(1-d/R,1.4)*m,r1=.55+.45*Math.sin(i*12.9),r2=.55+.45*Math.cos(i*7.3);a[i*3]+=nx*f*r1;a[i*3+2]+=nz*f*r2;a[i*3+1]-=f*.22*Math.abs(Math.sin(i*3.1))}}
  const k=mag;if(pz>D.L*.18&&Math.abs(px)<D.w*.45)c.dg.h+=k;else if(pz<-D.L*.18&&Math.abs(px)<D.w*.45)c.dg.t+=k;else if(Math.abs(px)>D.w*.28&&Math.abs(pz)<D.L*.3)c.dg[px>0?'r':'l']+=k;
  const th=18;if(c.dg.h>th&&!c.dgh){c.dgh=1;this.xrip(c,'h',D)}if(c.dg.t>th&&!c.dgt){c.dgt=1;this.xrip(c,'t',D)}if(c.dg.r>th&&!c.dgr){c.dgr=1;this.xrip(c,'r',D)}if(c.dg.l>th&&!c.dgl){c.dgl=1;this.xrip(c,'l',D)}
  pa.needsUpdate=true;g.computeVertexNormals()}
 xrip(c,w,D){const g=c.body.geometry,pa=g.attributes.position,co=g.attributes.color,a=pa.array,o=c.dg0;let sx,sy,sz,px,py,pz;
  if(w==='h'){sx=D.w*.8;sy=.07;sz=D.L*.3;px=0;py=D.hh;pz=D.L/2-sz/2-.1}else if(w==='t'){sx=D.w*.8;sy=.07;sz=D.L*.24;px=0;py=D.dh;pz=-D.L/2+sz/2+.1}else{sx=.07;sy=D.hh*.6;sz=D.L*.24;px=(w==='r'?1:-1)*D.w/2;py=D.hh*.55;pz=(D.z1+D.z3)/2-.2}
  for(let i=0;i<pa.count;i++){const x=o[i*3],y=o[i*3+1],z=o[i*3+2];if(Math.abs(x-px)<=sx/2+.06&&Math.abs(z-pz)<=sz/2+.06&&(w==='r'||w==='l'?(y>.4&&y<D.hh+.1):y>py-.3)){a[i*3+1]-=.1;if(co){co.array[i*3]=.1;co.array[i*3+1]=.1;co.array[i*3+2]=.11}}}
  pa.needsUpdate=true;if(co)co.needsUpdate=true;g.computeVertexNormals();
  const sn=Math.sin(c.h),cs=Math.cos(c.h),wx=c.x+px*cs+pz*sn,wz=c.z-px*sn+pz*cs,mesh=new THREE.Mesh(new THREE.BoxGeometry(sx,sy,sz),new THREE.MeshStandardMaterial({color:c.col,roughness:.4,metalness:.6}));mesh.position.set(wx,(c.y||0)+py,wz);mesh.rotation.y=c.h;mesh.castShadow=true;this.scene.add(mesh);
  const side=(w==='r'?1:w==='l'?-1:0),v=Math.hypot(c.vx||0,c.vz||0);this.xparts.push({m:mesh,vx:(c.vx||0)*.6+cs*side*5+(Math.random()-.5)*3,vz:(c.vz||0)*.6-sn*side*5+(Math.random()-.5)*3,vy:5+Math.random()*4,wx:(Math.random()-.5)*8,wz:(Math.random()-.5)*8,t:0,sy});this.sfx.beep(110);this.toast(this.xL('A part was torn off the car!','یک قطعه از ماشین کنده شد!'))}
 xcar(dt){this.xparts=this.xparts||[];const pl=this.player;
  for(const c of this.cars){if(c.dgR&&!c.wreck){c.body.geometry=c.model?Car.mod(c.model):Car.sg;c.dg=null;c.dgh=c.dgt=c.dgr=c.dgl=0;c.dgR=0}if(c.wreck){if(c.dg)c.dgR=1;continue}if(c.type==='motorcycle'||c.type==='tank'||c.type==='mytank')continue;const d=Math.hypot(c.x-pl.x,c.z-pl.z);if(d>70){c.xv=null;continue}
   const vx=c.vx||0,vz=c.vz||0,p=c.xv;if(p&&c.xhp!=null){const dx=vx-p[0],dz=vz-p[1],dv=Math.hypot(dx,dz);if(dv>4&&c.hp<c.xhp-.5){const wx=-dx,wz=-dz,sn=Math.sin(c.h),cs=Math.cos(c.h),lx=wx*cs-wz*sn,lz=wx*sn+wz*cs,l=Math.hypot(lx,lz)||1,D=this.xdim(c);this.xdent(c,lx/l*D.w*.5,lz/l*D.L*.5,Math.min(12,dv))}}
   c.xv=[vx,vz];c.xhp=c.hp}
  for(let i=this.xparts.length-1;i>=0;i--){const q=this.xparts[i],m=q.m;q.t+=dt;q.vy-=22*dt;m.position.x+=q.vx*dt;m.position.z+=q.vz*dt;m.position.y+=q.vy*dt;if(m.position.y<q.sy/2+.02){m.position.y=q.sy/2+.02;q.vy=-q.vy*.25;q.vx*=.7;q.vz*=.7;q.wx*=.6;q.wz*=.6}m.rotation.x+=q.wx*dt;m.rotation.z+=q.wz*dt;if(q.t>14){this.scene.remove(m);this.xparts.splice(i,1)}}
  for(const c of this.cars){if(c.xdman!=null&&c.xdm){c.xdm.visible=c.xdman>.01;const u=c.xdman;c.xdm.rotation.y=-1.15*(u*u*(3-2*u));continue}const a=c.xd;if(!a)continue;a.t+=dt;const T=a.t,u=T<.4?T/.4:T<.75?1:Math.max(0,1-(T-.75)/.4);if(T>1.2){a.g.visible=false;c.xd=null;continue}a.g.visible=true;a.g.rotation.y=-1.15*(u*u*(3-2*u))}}
 xdoorA(c,mk){if((c.xd&&!mk)||c.wreck)return;const D=this.xdim(c);if(!c.xdm){const g=new THREE.Group(),dm=new THREE.Mesh(new THREE.BoxGeometry(.05,D.hh*.6,1.15),new THREE.MeshStandardMaterial({color:c.col,roughness:.3,metalness:.6})),gl=new THREE.Mesh(new THREE.BoxGeometry(.04,D.hh*.28,.9),new THREE.MeshStandardMaterial({color:0x10151c,roughness:.1,metalness:.8}));dm.position.set(0,D.hh*.3+.35,-.58);gl.position.set(.01,D.hh*.62+.4,-.6);g.add(dm,gl);g.position.set(D.w/2+.03,0,D.z1-.3);g.visible=false;c.m.add(g);c.xdm=g}
  if(!mk)c.xd={g:c.xdm,t:0}}
 xneon(){const W=this.world,sc=this.scene,t=W.boxes.filter(b=>b.h>22&&b.x1-b.x0>8).slice(0,160),n=t.length;if(!n)return;const cl=[0xff2d95,0x2de2ff,0xffd12d,0x7dff3d,0xb04dff],im=new THREE.InstancedMesh(new THREE.BoxGeometry(1,1,1),new THREE.MeshBasicMaterial({color:0xffffff}),n*2),D=new THREE.Object3D(),C=new THREE.Color();
  t.forEach((b,i)=>{const cz=(b.z0+b.z1)/2,cx=(b.x0+b.x1)/2;D.position.set(b.x0-.35,b.h*(.45+W.R()*.3),cz+(W.R()-.5)*(b.z1-b.z0)*.5);D.scale.set(.5,7+W.R()*6,2.2);D.rotation.set(0,0,0);D.updateMatrix();im.setMatrixAt(i*2,D.matrix);C.setHex(cl[Math.floor(W.R()*5)]);im.setColorAt(i*2,C);
   D.position.set(cx,b.h+.8,cz);D.scale.set(1.2,1.6,1.2);D.updateMatrix();im.setMatrixAt(i*2+1,D.matrix);C.setHex(0xff2020);im.setColorAt(i*2+1,C)});im.instanceMatrix.needsUpdate=true;if(im.instanceColor)im.instanceColor.needsUpdate=true;sc.add(im)}
 xslot(){if(!this.pay(1000))return;const S5=['🍒','🍋','🔔','⭐','7'],r=[0,0,0].map(()=>Math.floor(Math.random()*5)),t=r.map(i=>S5[i]).join('  ');let w=0;if(r[0]===r[1]&&r[1]===r[2])w=r[0]===4?50000:10000;this.sfx.beep(w?880:200);if(w){this.cash(w);this.big(t,'+$'+w.toLocaleString(),'#ffd24a',3)}else this.big(t,this.xL('No luck','باختی'),'#ff7a7a',2)}
 xroul(m){const bet=m==='green'?500:2000;if(!this.pay(bet))return;const n=Math.floor(Math.random()*37),isRed=[1,3,5,7,9,12,14,16,18,19,21,23,25,27,30,32,34,36].includes(n),col=n===0?'green':isRed?'red':'black',win=col===m;this.sfx.beep(win?880:200);const t=n+' '+(col==='green'?this.xL('GREEN','سبز'):col==='red'?this.xL('RED','قرمز'):this.xL('BLACK','مشکی'));if(win){const g=m==='green'?bet*36:bet*2;this.cash(g);this.big(t,'+$'+g.toLocaleString(),'#ffd24a',3)}else this.big(t,this.xL('You lost $','باختی $')+bet.toLocaleString(),'#ff7a7a',2)}
 xbj(){if(!this.pay(3000))return;const d=()=>Math.min(10,1+Math.floor(Math.random()*13)),hv=h=>{const s=h.reduce((a,b)=>a+b,0);return h.includes(1)&&s+10<=21?s+10:s},p=[d(),d()],q=[d(),d()];while(hv(p)<17)p.push(d());while(hv(q)<17)q.push(d());const a=hv(p),b=hv(q),r=a>21?-1:b>21?1:a>b?1:a<b?-1:0,t=this.xL('You ','تو ')+a+' - '+this.xL('Dealer ','دیلر ')+b;this.sfx.beep(r>0?880:200);if(r>0){this.cash(6000);this.big(t,'+$6,000','#ffd24a',3)}else if(r===0){this.cash(3000);this.big(t,this.xL('Push - bet returned','مساوی - پول برگشت'),'#ffffff',3)}else this.big(t,this.xL('You lost $3,000','۳۰۰۰ دلار باختی'),'#ff7a7a',2)}
 xentS(c){if(this.xent)return;this.xent={c,ph:0,t:0};c.xdm||this.xdoorA(c,1);}
 xentU(dt){const e=this.xent;if(!e)return;const c=e.c,pl=this.player,k=this.inp.k;for(const n of['KeyW','KeyA','KeyS','KeyD','Space','ShiftLeft'])k[n]=0;
  if(c.wreck||Math.hypot(c.x-pl.x,c.z-pl.z)>14||this.dead>0){this.xent=null;c.xdman=0;return}
  const D=this.xdim(c),sn=Math.sin(c.h),cs=Math.cos(c.h),lx=D.w/2+.8,lz=D.z1-.75,tx=c.x+lx*cs+lz*sn,tz=c.z-lx*sn+lz*cs;e.t+=dt;c.stun=3;
  const ease=u=>u*u*(3-2*u),face=Math.atan2(-cs,sn);
  if(e.ph===0){const dx=tx-pl.x,dz=tz-pl.z,d=Math.hypot(dx,dz);if(d>.3&&e.t<3){pl.x+=dx/d*Math.min(d,3.6*dt);pl.z+=dz/d*Math.min(d,3.6*dt);pl.face=Math.atan2(dx,dz);pl.vx=dx/d*3.6;pl.vz=dz/d*3.6}else{pl.vx=pl.vz=0;pl.face=face;e.ph=1;e.t=0}}
  else if(e.ph===1){pl.face=face;c.xdman=Math.min(1,e.t/.55);if(e.t>.6){e.ph=2;e.t=0;if(c.ai){this.jack(c);c.ai=null;e.drv=1}}}
  else if(e.ph===2){pl.face=face;c.xdman=1;if(e.drv){pl.aimArm=1;const q=Math.sin(Math.min(1,e.t/.5)*Math.PI);pl.x=tx-cs*.25*q;pl.z=tz+sn*.25*q}if(e.t>(e.drv?1.1:.15)){e.ph=3;e.t=0}}
  else if(e.ph===3){const u=Math.min(1,e.t/.55),dx=c.x-tx,dz=c.z-tz;pl.x=tx+dx*ease(u);pl.z=tz+dz*ease(u);pl.face=face;if(u>=1){this.xbyp=1;this.near=c;this.toggleCar();this.xbyp=0;e.ph=4;e.t=0}}
  else{c.xdman=Math.max(0,1-e.t/.4);if(e.t>.45){c.xdman=null;if(c.xdm)c.xdm.visible=false;this.xent=null}}}
 xcity(){const G=this,sc=this.scene,W=this.world,Lg=(a,b)=>G.xL(a,b);G.xtm=[];
  const solid=(x0,x1,z0,z1,h)=>{const q={x0,x1,z0,z1,h};W.boxes.push(q);W.grid.add(q)},
  MS=(c,r=.7,m=0)=>new THREE.MeshStandardMaterial({color:c,roughness:r,metalness:m}),BS=c=>new THREE.MeshBasicMaterial({color:c}),
  mk=(w,h,d,m,x,y,z)=>{const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),m);o.position.set(x,y,z);o.castShadow=o.receiveShadow=true;sc.add(o);return o},
  flat=(w,d,c,x,y,z)=>{const o=new THREE.Mesh(new THREE.PlaneGeometry(w,d).rotateX(-Math.PI/2),MS(c,.9));o.position.set(x,y,z);o.receiveShadow=true;sc.add(o)},
  win=(col,lit)=>{const c=document.createElement('canvas');c.width=c.height=128;const g=c.getContext('2d');g.fillStyle=col;g.fillRect(0,0,128,128);for(let i=0;i<8;i++)for(let j=0;j<8;j++){g.fillStyle=Math.random()<.6?lit:'#10161f';g.fillRect(i*16+3,j*16+4,10,9)}const t=new THREE.CanvasTexture(c);t.wrapS=t.wrapT=THREE.RepeatWrapping;return t},
  tower=(x,z,w,h,col,lit)=>{const t=win(col,lit);t.repeat.set(w/14,h/14);const m=new THREE.MeshStandardMaterial({map:t,emissiveMap:t,emissive:0xffffff,emissiveIntensity:.3,roughness:.25,metalness:.5});G.xtm.push(m);
   mk(w,h,w,m,x,h/2,z);mk(w+2,2,w+2,MS(0x222831,.4,.6),x,h+1,z);mk(w*.5,6,w*.5,MS(0x333a44,.5,.5),x,h+5,z);const a=mk(.6,28,.6,MS(0x999999,.4,.8),x,h+22,z);mk(1.2,1.2,1.2,BS(0xff2020),x,h+36,z);solid(x-w/2,x+w/2,z-w/2,z+w/2,h)},
  sign=(txt,css,w,h,x,y,z,ry)=>{const c=document.createElement('canvas');c.width=512;c.height=Math.round(512*h/w);const g=c.getContext('2d');g.fillStyle='#0b0612';g.fillRect(0,0,c.width,c.height);g.strokeStyle=css;g.lineWidth=10;g.strokeRect(8,8,c.width-16,c.height-16);g.fillStyle=css;g.shadowColor=css;g.shadowBlur=24;g.font='bold '+(c.height*.42|0)+'px Rajdhani,Impact,sans-serif';g.textAlign='center';g.textBaseline='middle';g.fillText(txt,c.width/2,c.height/2);
   const o=new THREE.Mesh(new THREE.PlaneGeometry(w,h),new THREE.MeshBasicMaterial({map:new THREE.CanvasTexture(c)}));o.position.set(x,y,z);o.rotation.y=ry;sc.add(o)};
  // TWIN TOWERS (east-north)
  for(const z of[-540,-490])tower(675,z,30,260,'#9fb4c8','#ffe9a8');mk(10,5,20,MS(0x8a99aa,.3,.6),675,190,-515);mk(10,5,20,MS(0x8a99aa,.3,.6),675,120,-515);
  // CASINO STRIP (east): 3 casinos only, entrance faces the city
  const CN=[['ROYAL CASINO','#ffd24a'],['NEON PALACE','#ff2d95'],['GOLDEN ACE','#2de2ff']];
  CN.forEach((n,k)=>{const z=-380+k*130,x0=632,x1=692,cx=662;mk(60,38,70,MS(0x24122e,.5,.3),cx,19,z);mk(60.4,3,70.4,BS(new THREE.Color(n[1])),cx,39.5,z);
   mk(.4,36,.6,BS(new THREE.Color(n[1])),x0-.1,19,z-34);mk(.4,36,.6,BS(new THREE.Color(n[1])),x0-.1,19,z+34);
   sign(n[0],n[1],40,9,x0-.3,31,z,-Math.PI/2);mk(14,.8,14,MS(0x1a1a22,.4,.6),x0-7,7,z);mk(.7,7,.7,MS(0xd4a017,.3,.9),x0-13,3.5,z-6.5);mk(.7,7,.7,MS(0xd4a017,.3,.9),x0-13,3.5,z+6.5);
   mk(.5,5.5,8,BS(0xffd890),x0-.1,2.8,z);flat(12,8,0xaa0f2a,x0-6,.1,z);flat(12,28,0x2b2d33,x0-6,.05,z);for(let i=-3;i<=3;i++)mk(.8,.8,.8,BS(0xffd24a),x0-12,.6,z+i*2.2);
   solid(x0,x1,z-35,z+35,38);G.xdoors.push({x:x0-4,z,n:n[0]});G.xs.push({x:x0-4,z,r:5,t:()=>{const c=G.xc;return(c&&c.k==='rob'&&c.door===k)?Lg('Press E — ROB '+n[0],'E — سرقت از '+n[0]):Lg('Press E — enter '+n[0],'E — ورود به '+n[0])},fn:()=>{const c=G.xc;if(c&&c.k==='rob'&&c.door===k){G.cash(c.rw);G.big(Lg('HEIST COMPLETE','سرقت موفق'),'$ '+c.rw.toLocaleString(),'#ffd24a',3);G.addWanted(3);G.xc=null;return}G.xback={x:x0-5,z};G.xtp(2100,9,Math.PI,'cas')}})});
  // SKY NEEDLE (north-west)
  {const m=MS(0xcfd6de,.3,.6),x=-660,z=-560;mk(7,160,7,m,x,80,z);const d=mk(30,5,30,MS(0x2de2ff,.3,.4),x,150,z);d.material.emissive=new THREE.Color(0x0b6070);mk(2,35,2,MS(0xaaaaaa),x,178,z);solid(x-3.5,x+3.5,z-3.5,z+3.5,160)}
  // AIRPORTS
  const strip=(x,z0,z1,nm)=>{const len=z1-z0,zc=(z0+z1)/2;flat(26,len,0x2f3238,x,.045,zc);flat(1.2,len,0x2f3238,x,.05,zc);for(let z=z0+15;z<z1-10;z+=24)mk(.8,.04,10,BS(0xf2f2f2),x,.09,z);for(let z=z0+4;z<z1;z+=30){mk(.7,.4,.7,BS(0xffe9a0),x-14,.25,z);mk(.7,.4,.7,BS(0xffe9a0),x+14,.25,z)}
   for(let i=0;i<6;i++){mk(1.4,.04,12,BS(0xffffff),x-9+i*3.6,.09,z0+8);mk(1.4,.04,12,BS(0xffffff),x-9+i*3.6,.09,z1-8)}};
  strip(-700,-480,520);{const x=-650,z=0;flat(40,220,0x3a3d44,x,.04,z);mk(24,16,120,MS(0x9aa6b5,.15,.6),x,8,z);solid(x-12,x+12,z-60,z+60,16);mk(10,32,10,MS(0xcfcfcf,.5),x,16,z+75);mk(12,6,12,MS(0x2a4a6a,.1,.8),x,34,z+75);solid(x-5,x+5,z+70,z+80,34);sign('WEST INTERNATIONAL','#ffffff',50,7,x+12.3,13,z,Math.PI/2)}
  strip(702,40,580);{const x=650,z=310;flat(30,100,0x3a3d44,x,.04,z);mk(16,10,50,MS(0xb9a98a,.7),x,5,z);solid(x-8,x+8,z-25,z+25,10);mk(5,18,5,MS(0xcfcfcf),x,9,z+34);solid(x-2.5,x+2.5,z+31.5,z+36.5,18);sign('EAST AIRFIELD','#ffd24a',30,5,x-8.3,8,z,-Math.PI/2)}
  const put=(k,x,z,h)=>{const a=new Plane(sc,k);a.hx=x;a.hz=z;a.hh=h;a.reset();G.planes.push(a)};
  put('Airbus',-700,-450,0);put('Learjet',-700,-390,0);put('Cessna',-700,-340,0);put('Heli',-650,-240,0);
  put('Cessna',702,560,Math.PI);put('Biplane',702,520,Math.PI);put('Stunt',702,480,Math.PI);{const W1=['Cessna','Cessna2','Cessna3','Biplane','Biplane2','Stunt','Stunt2','Learjet','Learjet2','Boeing','Boeing2','Cargo','Airbus','Airbus2','Concorde','Heli','Heli2','Heli3'],J=['F35','F35b','Sukhoi','Sukhoi2','Raptor','Raptor2','B2','B2b'];let n=0;for(let z=-440;z<=-90;z+=35)put(W1[n++%W1.length],-672,z,0);for(let z=100;z<=480;z+=38)put(W1[n++%W1.length],-672,z,0);for(let z=70;z<=270;z+=40)put(W1[n++%W1.length],672,z,Math.PI);for(let z=380;z<=540;z+=40)put(W1[n++%W1.length],672,z,Math.PI);for(let x=-520;x<=520;x+=52){put(n%3?J[n%J.length]:W1[n%W1.length],x,-690,Math.PI/2);n++}}
  POI.push({x:632,z:-380,c:'#ffd24a',t:'CASINO'},{x:632,z:-250,c:'#ff2d95',t:'CASINO'},{x:632,z:-120,c:'#2de2ff',t:'CASINO'},{x:-650,z:0,c:'#ffffff',t:'AIRPORT'},{x:650,z:310,c:'#ffffff',t:'AIRPORT'});
  G.wp={x:615,z:-250};
  ['RevueltoSV','RevueltoBlack','Ferrari12','JeepCJ','Vario'].forEach((k,i)=>{G.spawnCar(k,622,-310+i*14,Math.PI);G.spawnCar(k,45+i*10,-4.5,Math.PI/2)});
  MAPLBL.push(['WEST INTL AIRPORT',-690,10],['EAST AIRFIELD',700,310],['CASINO STRIP',662,-250],['TWIN TOWERS',675,-515])}
 xex(dt){const W=this.world;if(this.xtm){const e=.12+W.night*1.3;for(const m of this.xtm)m.emissiveIntensity=e}
  for(const c of this.cars){if(!c.rider)continue;if(!c.rider.visible){c.rs=0;continue}c.rs=Math.min(1,(c.rs||0)+dt*3.2);const u=c.rs*c.rs*(3-2*c.rs);c.rider.position.set(0,.5+(1-u)*.7,-.3-(1-u)*.9);c.rider.scale.setScalar(.85*(.5+.5*u))}}

 xe(){const b=this.xnear;if(b&&b.fn)b.fn()}
  die(a,col,fee){if(this.flying){const f=this.flying;f.alive=false;f.dead=15;f.g.visible=false;this.flying=null}this.ch=null;this.dead=3.5;this.fee=fee;this.big(a,'',col,3.5);if(a==='WASTED')$('gl').classList.add('dead');this.jail=a==='BUSTED'}
  big(a,b,col,sec=3){$('ovl').style.display='block';$('ot').textContent=tr(a);$('ot').style.color=col;$('os').textContent=tr(b);this.bigT=sec}
  revive(){const p=this.player;this.zone='city';this.xj=null;this.xent=null;if(this.xth){this.xth.n.g.visible=false;this.xth=null}this.rig.init=false;this.driving=null;this.flying=null;for(const o of this.cars)if(o.rider)o.rider.visible=false;p.g.visible=true;p.x=20;p.z=10;p.y=0;p.vx=p.vz=0;this.health=100;this.armor=0;this.setWanted(0);this.sfx.radio(0);$('gl').classList.remove('dead');this.cash(-this.fee);if(this.jail){this.jail=0;this.xi&&(this.xin||this.xi());this.xjail();return}this.toast('Discharged from Harbor General. -$'+this.fee)}
  nextMission(){const L=this.world.L,f=this.driving||this.player;let x,z,t=0;do{x=L[Math.floor(this.world.R()*11)];z=L[Math.floor(this.world.R()*11)];t++}while(t<30&&Math.hypot(x-f.x,z-f.z)<350);
   const d=Math.hypot(x-f.x,z-f.z);this.mis={x,z,d,time:d/14+25};this.mk.position.set(x,30,z)}
mkRev(){this.rev={};this.dset=new Set(BINDS.map(b=>b[1]));for(const[n,d]of BINDS)this.rev[KB[d]||d]=d}
 kmap(c){return this.rev[c]||(this.dset.has(c)?'None':c)}
 bindKey(c){const d=this.binding;this.binding=null;if(c!=='Escape'){KB[d]=c;this.mkRev();sv('gtaelfo_k',KB)}this.drawSet()}
 cheatKey(e){if(this.state!=='PLAYING'||e.repeat)return;const ch=e.code==='Space'?'_':/^Key/.test(e.code)?e.code[3].toLowerCase():'';if(!ch)return;this.cb=(this.cb+ch).slice(-40);for(const c of CHEATS)if(this.cb.endsWith(c[0])){this.cb='';c[1](this);this.toast('Cheat: '+c[2]);this.sfx.beep(700);break}}
 applyGfx(){const q=S.q;const dp=devicePixelRatio||1;this.r.setPixelRatio(q==='low'?1:q==='med'?Math.min(dp,1.5):q==='high'?dp:Math.min(dp*1.5,3));this.r.setSize(innerWidth,innerHeight,false);this.world.sun.castShadow=q!=='low';C.cam.fov=S.fov;C.cam.fovMax=S.fov+15;this.sens=S.sens;this.showFps=S.fps;$('fps').style.display=S.fps?'block':'none';if(this.sfx.mg)this.sfx.mg.gain.value=S.vol}
 applyLang(){document.body.classList.toggle('fa',S.lang==='fa');$('bSet').textContent=tr('Settings');$('bStart').textContent=tr(this.state==='PAUSED'?'Resume GTA_elfo':'Start GTA_elfo');if(this.state==='PAUSED')$('sub').textContent=tr('Paused')}
 openSet(p){$('set').style.display='flex';$('screen').style.display='none';this.setPage=p||'main';this.drawSet()}
 closeSet(){$('set').style.display='none';$('screen').style.display='flex';sv('gtaelfo_s',S)}
 drawSet(){const G=this,box=document.createElement('div');box.className='sb';const e=$('set');e.innerHTML='';e.appendChild(box);
  const add=(h,fn)=>{const d=document.createElement('div');d.innerHTML=h;const x=d.firstChild;if(fn)fn(x);box.appendChild(x)},
  btn=(l,t,fn)=>add('<div class="r"><span>'+tr(l)+'</span><button></button></div>',x=>{const b=x.lastChild;b.textContent=tr(t);b.onclick=fn}),
  rng=(l,k,mn,mx,st)=>add('<div class="r"><span>'+tr(l)+'</span><input type="range" min="'+mn+'" max="'+mx+'" step="'+st+'" value="'+S[k]+'"></div>',x=>x.lastChild.oninput=ev=>{S[k]=+ev.target.value;G.applyGfx()});
  if(this.setPage==='keys'){add('<h2>'+tr('PC KEYS — click an action, then press the new key')+'</h2>');for(const[n,d]of BINDS)btn(n,this.binding===d?'press a key…':kn(KB[d]||d),()=>{G.binding=d;G.drawSet()});
   btn('Restore defaults','Reset',()=>{for(const k in KB)delete KB[k];G.mkRev();sv('gtaelfo_k',KB);G.drawSet()});btn('','Back',()=>{G.setPage='main';G.drawSet()});return}
  if(this.setPage==='posters'){add('<h2>'+tr('City posters (up to 5, any image size)')+'</h2>');for(let i=0;i<5;i++){add('<div class="r"><span>'+tr('Poster')+' '+(i+1)+'</span><input type="file" accept="image/*" style="max-width:190px"><button>'+tr('Clear')+'</button></div>',x=>{x.children[1].onchange=ev=>G.xfile(i,ev.target.files[0]);x.lastChild.onclick=()=>G.xfile(i,null,1)})}add('<div class="ch">'+tr('Posters appear on billboards along the city roads.')+'</div>');btn('','Back',()=>{G.setPage='main';G.drawSet()});return}
  add('<h2>'+tr('SETTINGS')+'</h2>');btn('City posters','Edit',()=>{G.setPage='posters';G.drawSet()});btn('Control mode',S.mode==='pc'?'PC (default)':'MOBILE',()=>{S.mode=S.mode==='pc'?'mobile':'pc';G.showMob();G.drawSet()});
  btn('Controls',S.mode==='pc'?'Edit keys':'Edit touch layout',()=>{if(S.mode==='pc'){G.setPage='keys';G.drawSet()}else G.editMob()});
  btn('Graphics quality',{low:'Low',med:'Medium',high:'High (native pixels)',ultra:'Ultra (1px, supersampled)'}[S.q],()=>{S.q={low:'med',med:'high',high:'ultra',ultra:'low'}[S.q];G.applyGfx();G.drawSet()});
  btn('Camera view',S.view==='first'?'First person':'Third person',()=>{S.view=S.view==='first'?'third':'first';sv('gtaelfo_s',S);G.drawSet()});rng('Field of view','fov',60,100,1);rng('Master volume','vol',0,1,.05);rng('Mouse / touch sensitivity','sens',.3,2.5,.1);btn('Show FPS',S.fps?'ON':'OFF',()=>{S.fps=!S.fps;G.applyGfx();G.drawSet()});btn('Language',S.lang==='fa'?'فارسی':'English',()=>{S.lang=S.lang==='fa'?'en':'fa';sv('gtaelfo_s',S);G.applyLang();G.drawSet()});
  btn('Fullscreen',document.fullscreenElement?'ON':'OFF',()=>{const d=document,e=d.documentElement;try{if(d.fullscreenElement)d.exitFullscreen();else{(e.requestFullscreen||e.webkitRequestFullscreen).call(e);try{screen.orientation.lock('landscape').catch(()=>{})}catch(x){}}}catch(x){}setTimeout(()=>G.drawSet(),400)});
  add('<h3>'+tr('Cheat codes (type during play)')+'</h3>');for(const c of CHEATS)add('<div class="ch"><b>'+tr(c[2])+'</b>: '+c[0].replace(/_/g,' (space) ')+'</div>');add('<div class="r"><button>'+tr('Back')+'</button></div>',x=>x.lastChild.onclick=()=>G.closeSet())}
 showMob(){$('mob').style.display=(S.mode==='mobile'&&(this.state==='PLAYING'||this.editing))?'block':'none'}
 mc(id){const d=MB.find(b=>b[0]===id);return MBL[id]||(MBL[id]={x:d[2],y:d[3],s:58,o:75})}
 renderMob(){const m=$('mob');m.innerHTML='';for(const[id,code]of MB){const c=this.mc(id),b=document.createElement('div');b.className='mbt'+(this.editing&&this.mobSel===id?' sel':'');b.textContent=id==='JOY'?'':id;
   if(id==='JOY'){const sz=Math.max(110,c.s*2.3),R=sz/2,kn=document.createElement('div');Object.assign(b.style,{left:c.x+'%',top:c.y+'%',width:sz+'px',height:sz+'px',opacity:c.o/100,borderRadius:'50%',border:'2px solid rgba(255,255,255,.55)',background:'radial-gradient(circle,rgba(255,255,255,.12),rgba(255,255,255,.04))',touchAction:'none'});
    Object.assign(kn.style,{position:'absolute',left:'50%',top:'50%',width:sz*.42+'px',height:sz*.42+'px',marginLeft:-sz*.21+'px',marginTop:-sz*.21+'px',borderRadius:'50%',background:'radial-gradient(circle at 35% 30%,#fff,#9ab 70%)',boxShadow:'0 2px 8px #0008',pointerEvents:'none'});b.appendChild(kn);
    const set=(dx,dy)=>{const k=this.inp.k,t=R*.22;k.KeyW=dy<-t?1:0;k.KeyS=dy>t?1:0;k.KeyA=dx<-t?1:0;k.KeyD=dx>t?1:0},mv=e=>{const r=b.getBoundingClientRect();let dx=e.clientX-(r.left+R),dy=e.clientY-(r.top+R);const l=Math.hypot(dx,dy);if(l>R){dx*=R/l;dy*=R/l}kn.style.transform='translate('+dx+'px,'+dy+'px)';set(dx,dy)};
    b.onpointerdown=e=>{e.preventDefault();b.setPointerCapture(e.pointerId);if(this.editing){this.mobSel=id;this.dr={id,ox:e.clientX,oy:e.clientY,x:c.x,y:c.y};this.drawMed();b.classList.add('sel')}else mv(e)};
    b.onpointermove=e=>{if(this.editing){if(this.dr&&this.dr.id===id){c.x=U.clamp(this.dr.x+(e.clientX-this.dr.ox)/innerWidth*100,2,98);c.y=U.clamp(this.dr.y+(e.clientY-this.dr.oy)/innerHeight*100,2,98);b.style.left=c.x+'%';b.style.top=c.y+'%'}}else if(e.buttons||e.pointerType==='touch')mv(e)};
    b.onpointerup=b.onpointercancel=()=>{this.dr=null;kn.style.transform='translate(0,0)';if(!this.editing)set(0,0)};m.appendChild(b);continue}
   Object.assign(b.style,{left:c.x+'%',top:c.y+'%',width:c.s+'px',height:c.s+'px',opacity:c.o/100,lineHeight:c.s+'px',fontSize:c.s*.28+'px'});
   b.onpointerdown=e=>{e.preventDefault();b.setPointerCapture(e.pointerId);if(this.editing){this.mobSel=id;this.dr={id,ox:e.clientX,oy:e.clientY,x:c.x,y:c.y};this.drawMed();b.classList.add('sel')}else{this.inp.k[code]=1;b.classList.add('on');this.onKey(code)}};
   b.onpointermove=e=>{if(this.editing&&this.dr&&this.dr.id===id){c.x=U.clamp(this.dr.x+(e.clientX-this.dr.ox)/innerWidth*100,2,98);c.y=U.clamp(this.dr.y+(e.clientY-this.dr.oy)/innerHeight*100,2,98);b.style.left=c.x+'%';b.style.top=c.y+'%'}};
   b.onpointerup=b.onpointercancel=()=>{this.dr=null;if(!this.editing){this.inp.k[code]=0;b.classList.remove('on')}};m.appendChild(b)}}
 editMob(){this.editing=true;this.mobSel=MB[0][0];$('set').style.display='none';$('med').style.display='flex';this.showMob();this.renderMob();this.drawMed()}
 drawMed(){const G=this,c=this.mc(this.mobSel),e=$('med');e.innerHTML='<div class="sb"><b>'+this.mobSel+'</b> — '+tr(MB.find(b=>b[0]===this.mobSel)[4])+' · '+tr('drag any button to move it')+'<div class="r"><span>'+tr('Size')+'</span><input id="ms" type="range" min="36" max="140" value="'+c.s+'"></div><div class="r"><span>'+tr('Opacity %')+'</span><input id="mo" type="range" min="10" max="100" value="'+c.o+'"></div><div class="r"><button id="mr">'+tr('Reset layout')+'</button><button id="md">'+tr('Done')+'</button></div><div class="lg">'+MB.map(b=>'<span><b>'+b[0]+'</b> = '+tr(b[4])+'</span>').join('')+'</div></div>';
  $('ms').oninput=ev=>{c.s=+ev.target.value;G.renderMob()};$('mo').oninput=ev=>{c.o=+ev.target.value;G.renderMob()};$('mr').onclick=()=>{for(const k in MBL)delete MBL[k];G.renderMob();G.drawMed()};
  $('md').onclick=()=>{G.editing=false;sv('gtaelfo_m',MBL);$('med').style.display='none';G.showMob();G.renderMob();G.openSet('main')}}
 pay(n){if(this.money<n){this.toast('Not enough cash');return false}this.cash(-n);return true}
 eff(n){const r={...WEAP[n]},a=this.att[n]||{};r.mag=MAG[n];r.rl=RL[n];r.sil=!!a.sil;if(a.long){r.rng*=1.35;r.dmg*=1.1;r.spr*=.7}if(a.short){r.rate*=.8;r.spr*=1.4;r.rng*=.75}if(a.stock)r.spr*=.55;if(a.mag){r.mag=Math.round(r.mag*1.8);r.rl+=.25}return r}
 reload(){const n=this.weaponName;if(!WEAP[n]||this.rl>0||this.driving)return;const e=this.eff(n);if((this.mag[n]||0)>=e.mag||!(this.am[n]>0))return;this.rl=this.rlT=e.rl;this.rlW=n;this.sfx.beep(300)}
 puff(x,y,z){const i=this.si++%60;this.sp[i*3]=x+(Math.random()-.5);this.sp[i*3+1]=y;this.sp[i*3+2]=z+(Math.random()-.5);this.sl[i]=1.2}
 dmgCar(c,n){if(c.wreck||n<=0)return;c.hp-=n;if(c.hp<=0)this.explode(c)}
 boom(x,z,r,dmg){const m=new THREE.Mesh(new THREE.SphereGeometry(1,12,8),new THREE.MeshBasicMaterial({color:0xff9a2a,transparent:true,opacity:.9,blending:THREE.AdditiveBlending,depthWrite:false,fog:false}));m.position.set(x,1.5,z);m.life=.7;m.R=r;this.scene.add(m);this.fx.push(m);this.bl.position.set(x,4,z);this.bl.intensity=8;this.sfx.shot(3);
  for(let i=0;i<14;i++)this.puff(x+(Math.random()-.5)*r,1+Math.random()*3,z+(Math.random()-.5)*r);
  for(const c of this.cars){if(c.wreck)continue;const dx=c.x-x,dz=c.z-z,d=Math.hypot(dx,dz);if(d<r*1.6){const k=1-d/(r*1.6);c.vx+=dx/(d||1)*k*12;c.vz+=dz/(d||1)*k*12;c.stun=2;c.vy=Math.max(c.vy,k*5);this.dmgCar(c,dmg*k)}}
  const p=this.driving||this.player,d=Math.hypot(p.x-x,p.z-z);if(d<r*1.4)this.hurt(dmg*(1-d/(r*1.4))*.8);for(const q of this.peds.p)if(q.dead<=0&&Math.hypot(q.x-x,q.z-z)<r*1.5)this.killPed(q,true)}
 explode(c){if(c.wreck)return;c.wreck=true;c.wt=0;c.hp=0;c.ai=null;const dr=c===this.driving,tk=c.type==='tank';this.boom(c.x,c.z,tk?10:6,tk?0:55);
  if(c.type==='police')this.policeSpawned=Math.max(0,this.policeSpawned-1);if(tk){this.tankSpawned=false;c.m.scale.set(1,1,1);c.sc0.set(1,1,1)}if(c.type!=='motorcycle')c.type=null;
  c.vy=12;c.y=.05;c.spin=[(Math.random()-.5)*7,(Math.random()-.5)*7];c.body.material.color.setHex(0x151515);c.body.material.emissive.setHex(0);
  if(dr){this.toggleCar();this.player.vy=8;this.player.vx=(Math.random()-.5)*10;this.player.vz=(Math.random()-.5)*10}}
 cops(){const p=this.player,w=this.wanted;while(this.policeSpawned<Math.min(w+1,4))this.spawnPolice();
  if(w>=5&&!this.tankSpawned){const t=new Car(this.scene,0x536b4a,'tank');t.x=p.x-40;t.z=p.z-30;this.cars.push(t);this.tankSpawned=true;this.toast('5 STARS — TANK DEPLOYED!')}
  if(w>=3&&!this.heli){const h=this.heli=new Heli(this.scene);h.x=p.x+80;h.z=p.z+80;this.toast('3 STARS — POLICE HELICOPTER!')}}
 spawnCar(k,x,z,h){const p=this.player,y=this.rig.yaw,mo=!!MOTOS[k],M=mo?MOTOS[k]:CARMODELS[k],c=new Car(this.scene,M.c,mo?'motorcycle':null,k);c.x=x??p.x+Math.sin(y)*6;c.z=z??p.z+Math.cos(y)*6;c.h=h??y;c.step(0,0,0,true,false);this.cars.push(c);return c}
 chDone(r){this.cash(r);this.big('CHALLENGE COMPLETE!','$ '+r.toLocaleString(),'#ffd24a');this.sfx.beep(880);this.ch=null}
 fireMsl(){const a=this.flying;if(!a||!a.P.jet||this.weaponCooldown>0)return;this.weaponCooldown=.6;const f=[Math.sin(a.h)*Math.cos(a.p),Math.sin(a.p),Math.cos(a.h)*Math.cos(a.p)],sp=a.v+110,m=new THREE.Mesh(new THREE.CylinderGeometry(.12,.12,1.6,6).rotateX(Math.PI/2),new THREE.MeshBasicMaterial({color:0xffe9a0,fog:false}));
  m.position.set(a.x,a.y+a.gy-.6,a.z);m.vel=[f[0]*sp,f[1]*sp,f[2]*sp];m.t=4;m.lookAt(m.position.x+f[0],m.position.y+f[1],m.position.z+f[2]);this.scene.add(m);this.msls.push(m);this.sfx.shot(.8)}
 tick2(dt){this.xt(dt);const pl=this.player,k=this.dead>0?NOKEY:this.inp.k,car=this.driving||this.flying,W=WEAP[this.weaponName];
  {const tr=this.traffic;tr.t+=dt;const s0=tr.st(0),s1=tr.st(1);if(s0!==this.tl0||s1!==this.tl1){this.tl0=s0;this.tl1=s1;const W2=this.world,cc=[new THREE.Color(0x22ff66),new THREE.Color(0xffc21a),new THREE.Color(0xff2a2a)];for(let i=0;i<W2.tla.length;i++)W2.tlb.setColorAt(i,cc[W2.tla[i]?s1:s0]);W2.tlb.instanceColor.needsUpdate=true}}
  for(let i=0;i<2;i++){const m=this.fl[i],d=this.driving,bk=d&&d.type==='motorcycle';if(d&&d.nb&&!(bk&&i)){m.visible=true;const fl=1+Math.random()*(bk?1.4:.8);m.scale.set(bk?.55:1,bk?.55:1,fl*(bk?1.25:1));m.material.color.setHex(bk?(d.fc||0xffa030):0x66b0ff);const sn=Math.sin(d.h),cs=Math.cos(d.h),o=bk?.28:(i?-.5:.5),bz=bk?2.7:3.3;m.position.set(d.x+cs*o-sn*bz,d.y+(bk?.45:.55),d.z-sn*o-cs*bz);m.rotation.set(d.rx||0,d.h,0)}else m.visible=false}
  {const dl=this.dl,d=this.driving;for(let i=0;i<120;i++)if(dl[i]>0){dl[i]-=dt;this.dp[i*3+1]+=dt*.6;this.dp[i*3]+=(Math.random()-.5)*dt*1.5;if(dl[i]<=0)this.dp[i*3+1]=-100}
   if(d&&d.type==='motorcycle'&&d.y<=.05&&Math.abs(d.sp)>6){const sn=Math.sin(d.h),cs=Math.cos(d.h),n=Math.min(3,1+(Math.abs(d.sp)/14|0))*(d.dust>1.5?2:1)+(d.slip?3:0)+(d.nb?2:0);for(let k=0;k<n;k++){const i=this.di++%120;this.dp[i*3]=d.x-sn*1.0+(Math.random()-.5)*.5;this.dp[i*3+1]=.12+Math.random()*.2;this.dp[i*3+2]=d.z-cs*1.0+(Math.random()-.5)*.5;dl[i]=.5+Math.random()*.5*d.dust}}
   this.dg.attributes.position.needsUpdate=true}
  for(const a of this.planes){if(!a.alive){if((a.dead-=dt)<=0)a.reset()}else a.g.visible=a===this.flying||Math.hypot(a.x-pl.x,a.z-pl.z)<480}
  for(let i=this.msls.length-1;i>=0;i--){const m=this.msls[i];m.t-=dt;m.position.x+=m.vel[0]*dt;m.position.y+=m.vel[1]*dt;m.position.z+=m.vel[2]*dt;this.puff(m.position.x,m.position.y,m.position.z);let hit=m.t<=0||m.position.y<=.6;
   if(!hit)for(const b of this.world.grid.at(m.position.x,m.position.z))if(m.position.x>b.x0&&m.position.x<b.x1&&m.position.z>b.z0&&m.position.z<b.z1&&m.position.y<b.h)hit=true;
   if(!hit)for(const c of this.cars)if(!c.wreck&&Math.hypot(c.x-m.position.x,c.z-m.position.z)<3&&m.position.y<4)hit=true;
   if(hit){this.boom(m.position.x,m.position.z,11,95);this.scene.remove(m);this.msls.splice(i,1)}}
  if(this.punchT>0){this.punchT-=dt;const u=Math.sin((1-Math.max(0,this.punchT)/.3)*Math.PI),a1=this.pf?pl.aR:pl.aL,a2=this.pf?pl.aL:pl.aR;a1.rotation.x=-1.9*u;a2.rotation.x=.7*u;pl.g.rotation.x=.2*u}
  {const ch=this.ch;if(ch&&this.dead<=0){if(ch.type==='kill'){ch.t-=dt;ch.txt='BRAWL \u00b7 KO '+ch.n+'/'+ch.need+' \u00b7 '+Math.max(0,ch.t|0)+'s';if(ch.n>=ch.need)this.chDone(ch.r);else if(ch.t<=0){this.toast('Challenge failed');this.ch=null}}
   else if(ch.type==='heat'){ch.t-=dt;ch.txt='SURVIVE THE HEAT \u00b7 '+Math.max(0,ch.t|0)+'s';if(ch.t<=0){this.setWanted(0);this.chDone(ch.r)}}else ch.txt='TIME ATTACK \u00b7 reach the red marker in time'}}
  for(let i=this.fx.length-1;i>=0;i--){const m=this.fx[i];m.life-=dt;const u=Math.max(0,m.life/.7);m.scale.setScalar(m.R*(1-u*u)+.5);m.material.opacity=u;if(m.life<=0){this.scene.remove(m);this.fx.splice(i,1)}}
  this.bl.intensity=Math.max(0,this.bl.intensity-dt*40);
  for(const c of this.cars){if(c.wreck||c.hp>=45)continue;if(Math.random()<.2)this.puff(c.x,1.3,c.z);c.hp-=(c.hp<20?6:1)*dt;if(c.hp<=0)this.explode(c)}
  if(this.rl>0){if(this.rlW!==this.weaponName||car)this.rl=0;else if((this.rl-=dt)<=0){const n=this.weaponName,e=this.eff(n),t=Math.min(e.mag-(this.mag[n]||0),this.am[n]||0);this.mag[n]=(this.mag[n]||0)+t;this.am[n]-=t;this.sfx.beep(420)}}
  this.aiming=!car&&!!W&&!!k.KeyZ;this.fp=!car&&(S.view==='first'||this.aiming);for(const o of pl.g.children){if(o===pl.flashM||o===pl.magM||Object.values(pl.guns).includes(o))continue;o.visible=!this.fp}const a=this.att[this.weaponName]||{};this.scopeFov=a.scp?(this.weaponName==='Sniper'?12:24):this.weaponName==='Sniper'?30:52;$('scope').style.display=this.aiming&&a.scp?'block':'none';if(this.aiming&&a.scp)for(const o of pl.g.children)o.visible=false;
  const g=pl.armed&&pl.guns[this.weaponName];if(g){g.at.sil.visible=!!a.sil;g.at.scp.visible=!!a.scp;g.at.lng.visible=!!a.long;g.at.stk.visible=!!a.stock;
   const p=this.rl>0?1-this.rl/this.rlT:0,s=this.rl>0?Math.sin(p*Math.PI):0;g.rotation.x=s*.8;g.position.set(-.4,1.6-s*.3,.7-(p>.85?.1*Math.sin((p-.85)/.15*Math.PI):0));pl.aL.rotation.z=-1.1*s;if(s)pl.aL.rotation.x=-1.25*s;
   const mm=pl.magM;mm.visible=this.rl>0&&(p<.3||(p>.55&&p<.88));if(mm.visible){if(p<.3)mm.position.set(-.4,1.4-p/.3*.9,.7);else{const u=(p-.55)/.33;mm.position.set(U.lerp(.15,-.4,u),U.lerp(1,1.4,u),.7)}}}else pl.magM.visible=false;
  const h=this.heli;if(h){h.a+=dt*.5;const f=Math.min(1,dt*1.2);h.x+=(pl.x+Math.cos(h.a)*26-h.x)*f;h.z+=(pl.z+Math.sin(h.a)*26-h.z)*f;h.y=24+Math.sin(this.tt)*2;h.g.position.set(h.x,h.y,h.z);h.g.rotation.set(.08,Math.atan2(pl.x-h.x,pl.z-h.z),0);h.rot.rotation.y+=dt*35;h.tr.rotation.x+=dt*40;h.bc.material.color.setHex(((this.tt*5)|0)%2?0xff2020:0x2060ff);
   h.cd-=dt;if(h.cd<=0&&this.dead<=0&&this.zone==='city'){h.cd=.45;const t=car||pl;this.tracer(h.x,h.y-1,h.z,t.x+(Math.random()-.5)*4,1,t.z+(Math.random()-.5)*4);if(Math.random()<.3)this.hurt(4)}}
  if(this.wanted>0&&(this.polT-=dt)<=0){this.polT=3;this.cops()}}
 buildShop(id){const e=$('shop'),G=this,w=this.weaponName,s=this.nearShop||{},R=[],c=this.driving;e.style.display=id==='skin'?'none':'block';$('skin').style.display=id==='skin'?'block':'none';if(id==='skin')return;
  const T={gun:'HARBOR ARMS — weapons',att:'ATTACHMENT LAB',car:'PREMIUM MOTORS — cars',moto:'TWO WHEELS — bikes',garage:'ELFO GARAGE — tuning',arena:'CHALLENGE HALL — win cash',mil:'MILITARY DEPOT — vehicles',air:'AIRCRAFT DEALER — planes'}[id],P={Pistol:300,SMG:900,Shotgun:1200,Rifle:1800,Sniper:2200};let note='';
  if(id==='gun'){for(const n of GUNS)R.push([(this.own.has(n)?'✓ ':'')+n,this.own.has(n)?0:P[n],()=>{if(G.own.has(n)){G.weaponName=n;return}if(G.pay(P[n])){G.own.add(n);G.am[n]=(G.am[n]||0)+WEAP[n].ammo;G.mag[n]=MAG[n];G.weaponName=n}}]);
   R.push(['Ammo (equipped gun)',100,()=>{if(WEAP[w]&&G.pay(100))G.am[w]+=WEAP[w].ammo}],['Armor',700,()=>{if(G.pay(700))G.armor=100}],['Medkit',150,()=>{if(G.pay(150))G.health=100}])}
  else if(id==='att'){for(const n of GUNS)if(this.own.has(n))R.push([(n===w?'» ':'')+n,0,()=>{G.weaponName=n}]);
   if(WEAP[w])for(const[k,l,pr]of ATT){const A=this.att[w]||{},ow=this.attOwn.has(w+k);R.push([(A[k]?'● ':'○ ')+l,ow?0:pr,()=>{if(!ow&&!G.pay(pr))return;G.attOwn.add(w+k);const B=G.att[w]=G.att[w]||{};B[k]=!B[k];if(B[k]){if(k==='long')B.short=false;if(k==='short')B.long=false}}])}else note='Buy and equip a gun first.'}
  else if(id==='car'||id==='moto'){const D=id==='car'?CARMODELS:MOTOS;for(const k in D)R.push([D[k].n,D[k].p,()=>{if(G.pay(D[k].p)){G.spawnCar(k,s.x,s.z-11,Math.PI);G.toast(D[k].n+' delivered outside')}}])}
  else if(id==='mil'){const B=(n,p,fn)=>R.push([n,p,()=>{if(G.pay(p)){fn();G.toast(n+' delivered')}}]),
  air=(k,jet)=>()=>{const a=new Plane(G.scene,k);if(jet){a.hx=-450+Math.random()*350;a.hz=-690;a.hh=Math.PI/2}else{a.hx=s.x+(Math.random()-.5)*8;a.hz=s.z-14;a.hh=0}a.reset();G.planes.push(a);if(jet)G.toast('Parked on the airport taxiway')};
  B('Battle Tank (F: drive, fire: cannon)',45000,()=>{const c=new Car(G.scene,0x536b4a,'tank');c.type='mytank';c.mytank=1;c.f.max*=.4;c.f.acc*=.55;c.hp=1600;c.x=s.x;c.z=s.z-12;c.h=Math.PI;const M=new THREE.MeshStandardMaterial({color:0x3f5a38,roughness:.6,metalness:.4}),t=new THREE.Mesh(new THREE.BoxGeometry(1.6,.5,2.2),M),b=new THREE.Mesh(new THREE.CylinderGeometry(.09,.09,2.6,8).rotateX(Math.PI/2),M);t.position.set(0,1.45,-.1);b.position.set(0,1.5,1.9);c.m.add(t,b);c.step(0,0,0,true,false);G.cars.push(c)});
  B('Attack Helicopter',60000,air('Heli',0));}
  else if(id==='air'){const PR={Cessna:8000,Stunt:15000,Biplane:12000,Learjet:55000,Airbus:70000,Boeing:90000,Concorde:90000,F35:150000,Sukhoi:130000,Raptor:120000,B2:200000,Heli:60000,Cessna2:8000,Cessna3:8000,Stunt2:15000,Biplane2:12000,Learjet2:55000,Boeing2:90000,Cargo:95000,Airbus2:70000,F35b:150000,Sukhoi2:130000,Raptor2:125000,B2b:200000,Heli2:60000,Heli3:60000};for(const k of Object.keys(PLANES)){const p=PR[k]||50000;R.push([PLANES[k].name,p,()=>{if(!G.pay(p))return;const a=new Plane(G.scene,k);if(PLANES[k].heli){a.hx=330;a.hz=-650;a.hh=0}else{a.hx=-450+Math.random()*380;a.hz=-690;a.hh=Math.PI/2}a.reset();G.planes.push(a);G.toast(PLANES[k].name+' delivered to the '+(PLANES[k].heli?'helipad':'taxiway'))}])}note='Delivered to the airport. Hold Shift on the runway to take off.'}
   else if(id==='arena'){const go=(o)=>{G.ch=o;G.toast('Challenge started!');G.closeShop();return true};
   R.push(['Street Brawl: 8 KOs in 60s \u2192 win $2,500',0,()=>go({type:'kill',n:0,need:8,t:60,r:2500,txt:''})],['Time Attack: reach the red marker (drive!) \u2192 +$4,000',0,()=>{G.nextMission();G.mis.time=Math.round(G.mis.time*.6);return go({type:'race',bonus:4000,txt:''})}],
    ['Survive the Heat: 3 stars for 60s \u2192 win $6,000',0,()=>{G.setWanted(0);G.addWanted(3);return go({type:'heat',t:60,r:6000,txt:''})}]);if(G.ch)R.push(['Abandon current challenge',0,()=>{G.ch=null}]);note='Pick a challenge. Fight, race or survive.'}
  else if(c){const o=G.over,cap=o?25:3;c.lv=c.lv||{e:0,h:0,t:0,a:0};const PAL=[0xd10000,0x2c7be5,0xf2c200,0x1fbf3a,0xf4f4f4,0x111111,0x8e44ad,0xff6a00,0xff3d8b,0x00e5ff],
   up=(lab,k,base,fn)=>R.push([lab+' Lv '+c.lv[k]+'/'+cap,c.lv[k]<cap?base*(c.lv[k]+1):0,()=>{if(c.lv[k]<cap&&G.pay(base*(c.lv[k]+1))){c.lv[k]++;fn()}}]),nm=o?9999:300;
   R.push(['Nitro refill +100 ('+(G.nit|0)+'/'+nm+', hold Shift)',500,()=>{if(G.nit<nm&&G.pay(500))G.nit=Math.min(nm,G.nit+100)}]);
   up('Engine / top speed','e',1500,()=>{c.f.max*=1.08;c.f.acc*=1.12});up('Handling / steering','h',1200,()=>{c.f.steer*=1.08;c.f.grip*=1.06});up('Tires & brakes','t',1000,()=>{c.f.brake*=1.1;c.f.grip*=1.05});up('Armor plating','a',1300,()=>{c.hp+=60});
   const lo=o?-.3:-.15,hi=o?1.5:.45;R.push(['Spring height \u25bc lower ('+c.rh.toFixed(2)+')',100,()=>{if(c.rh>lo&&G.pay(100))c.rh=Math.max(lo,c.rh-.1)}],['Spring height \u25b2 raise',100,()=>{if(c.rh<hi&&G.pay(100))c.rh=Math.min(hi,c.rh+.1)}]);
   if(c.wh)R.push(['Wheel size \u25bc smaller ('+c.wsz.toFixed(2)+'x)',150,()=>{if(c.wsz>(o?.5:.8)&&G.pay(150))c.wsz=Math.max(o?.5:.8,c.wsz-.1)}],['Wheel size \u25b2 bigger',150,()=>{if(c.wsz<(o?3:1.4)&&G.pay(150))c.wsz=Math.min(o?3:1.4,c.wsz+.1)}]);
   R.push([c.air?'\u2713 Air suspension (V = hop)':'Air suspension kit',c.air?0:2500,()=>{if(!c.air&&G.pay(2500))c.air=true}],['Repaint (next color)',200,()=>{if(G.pay(200)){c.pi=((c.pi||0)+1)%PAL.length;c.col=PAL[c.pi];c.body.material.color.setHex(c.col)}}]);if(o)note='UNLIMITED mode on'}
  else note='Drive a vehicle into the garage marker to tune it.';
  e.innerHTML='<h2>'+tr(T)+'</h2><p>$ '+this.money.toLocaleString()+' · '+tr('B closes.')+' '+tr(note)+'</p>';const gr=document.createElement('div');gr.className='shopgrid';
  R.forEach(r=>{const b=document.createElement('button');b.textContent=tr(r[0])+(r[1]?' — $'+r[1].toLocaleString():'');b.onclick=()=>{if(r[2]()===true)return;G.buildShop(id)};gr.appendChild(b)});
  const x=document.createElement('button');x.textContent=tr('Close');x.onclick=()=>G.closeShop();gr.appendChild(x);e.appendChild(gr)}
 toggleCar(){const p=this.player;if(this.xent&&!this.xbyp)return;if(!this.driving&&!this.flying&&this.near&&!this.xbyp&&this.xin){const nc=this.near;if(nc.type!=='motorcycle'&&nc.type!=='tank'&&nc.type!=='mytank'&&!nc.wreck&&Math.abs(nc.sp||0)<5){this.xentS(nc);return}}if(this.driving&&!this.flying&&this.driving.type!=='motorcycle'&&this.driving.type!=='tank'&&this.driving.type!=='mytank')this.xdoorA(this.driving);
  if(this.flying){const a=this.flying;if(a.y-(a.gl||0)>.3||a.v>(a.P.heli?6:25)){this.toast(a.P.heli?'Land the helicopter first (hold Space)':'Land and slow below 90 km/h first');return}const ex=a.P.heli?a.P.span*.8:a.P.span+2;p.x=a.x+Math.cos(a.h)*ex;p.z=a.z-Math.sin(a.h)*ex;p.y=a.gl||0;p.vx=p.vz=0;p.g.visible=true;this.flying=null;a.v=0;a.th=0;this.sfx.beep();return}
  if(!this.driving&&!this.near&&this.nearAir){this.flying=this.nearAir;p.g.visible=false;this.sfx.beep();this.toast('Hold Shift: throttle (auto takeoff) \u00b7 Shift: throttle \u00b7 Space: brake \u00b7 W/S: pitch \u00b7 A/D: bank \u00b7 J: missile (jets)');return}
  if(this.driving){const c=this.driving,sn=Math.sin(c.h),cs=Math.cos(c.h),sp=[[c.x+cs*2.6,c.z-sn*2.6],[c.x-cs*2.6,c.z+sn*2.6],[c.x-sn*4,c.z-cs*4]];
   const ok=sp.find(([x,z])=>this.world.free(x,z,.7)&&!this.cars.some(o=>o!==c&&Math.hypot(o.x-x,o.z-z)<2))||sp[0];
   p.x=ok[0];p.z=ok[1];p.y=0;p.vx=p.vz=0;p.g.visible=true;this.driving=null;c.nb=false;if(c.rider)c.rider.visible=false;this.sfx.radio(0)}
  else if(this.near){if(this.near.ai)this.jack(this.near);this.driving=this.near;this.near.ai=null;this.near.stun=0;p.g.visible=false;this.sfx.beep();this.sfx.radio(this.radio);const rm=this.near.rmat;if(rm){rm[0].color.copy(p.mat.sh.color);rm[1].color.copy(p.mat.pn.color);rm[2].color.copy(p.mat.sk.color);this.near.rider.visible=true}}}
 toast(t){const e=$('toast');e.textContent=tr(t);e.style.display='block';this.toastT=2}
 fixed(dt){if(this.dead>0&&(this.dead-=dt)<=0)this.revive();const k=this.dead>0?NOKEY:this.inp.k,car=this.driving,pl=this.player;this.weaponCooldown=Math.max(0,this.weaponCooldown-dt);if(this.flash>0)this.flash-=dt;for(const o of this.trs)if(o.visible&&(o.life-=dt)<=0)o.visible=false;
  if(car){car.nb=!!(k.ShiftLeft&&k.KeyW&&this.nit>0&&!car.wreck);if(car.nb)this.nit=Math.max(0,this.nit-14*dt*(car.type==='motorcycle'?1.25:1));car.step(dt,(k.KeyW?1:0)-(k.KeyS?1:0),(k.KeyA?1:0)-(k.KeyD?1:0),false,!!k.Space);pl.x=car.x;pl.z=car.z}else if(this.flying){const a=this.flying,cr=a.fly(dt,k,this);pl.x=a.x;pl.z=a.z;pl.face=a.h;pl.g.visible=false;if(cr){this.toast('Crashed: '+cr);this.boom(a.x,a.z,14,100);a.alive=false;a.dead=20;a.g.visible=false;this.flying=null;pl.g.visible=true;this.hurt(999)}}else{this.kin.k=k;pl.step(dt,this.kin,this.rig.yaw,this.world)}
  {const W=WEAP[this.weaponName];pl.armed=!car&&!!W;for(const n in pl.guns)pl.guns[n].visible=pl.armed&&n===this.weaponName;pl.flashM.visible=pl.armed&&this.flash>0;
   if(pl.armed){pl.aR.rotation.x=-1.45;if(this.fireT>0){this.fireT-=dt;pl.face=this.rig.yaw;pl.g.rotation.y=pl.face}}
   if(W&&W.auto&&!car&&this.dead<=0&&(k.KeyJ||(this.inp.locked&&this.inp.btn)))this.shoot()}
  const pp=car?null:pl;
  for(const c of this.cars){if(c===car)continue;if(this.xth&&this.xth.car===c&&this.xth.ph==='drive')continue;{const dd=Math.hypot(c.x-pl.x,c.z-pl.z),far=dd>300&&!c.wreck&&c.type!=='police'&&c.type!=='tank';if(far!==c.far){c.far=far;c.m.visible=!far}if(far&&!c.ai)continue}
   if(c.wreck){c.step(dt,0,0,true,false);c.wt+=dt;if(c.wt>7)c.m.scale.copy(c.sc0).multiplyScalar(Math.max(.01,1-(c.wt-7)/2));if(c.wt>9){c.m.scale.copy(c.sc0);c.wreck=false;c.hp=100;c.y=0;c.vy=0;c.body.material.color.setHex(c.col);this.traffic.respawn(c,pl.x,pl.z)}continue}if(c.type==='police'||c.type==='tank'){const dx=pl.x-c.x,dz=pl.z-c.z;const d=Math.hypot(dx,dz);if(c.type==='tank'&&d<55&&this.dead<=0){c.sk2=(c.sk2||0)-dt;if(c.sk2<=0){c.sk2=3.2;this.tracer(c.x,2.6,c.z,pl.x,1,pl.z);this.boom(pl.x+(Math.random()-.5)*10,pl.z+(Math.random()-.5)*10,5,30)}}if(d>4){c.h=U.lerpA(c.h,Math.atan2(dx,dz),dt*1.5);c.step(dt,c.type==='tank'?.35:.5,U.clamp(U.wrap(Math.atan2(dx,dz)-c.h)*2,-1,1),false,false)}else c.step(dt,0,0,true,false);
   c.sk=Math.abs(c.sp)<2&&d>8?c.sk+dt:0;if(c.sk>2.5||d>C.npc.cull){c.sk=0;if(c.type==='tank'){c.x=pl.x-40;c.z=pl.z}else this.traffic.respawn(c,pl.x,pl.z)}continue}if(c.ai){this.traffic.drive(c,dt,this.cars,pp);if(Math.hypot(c.x-pl.x,c.z-pl.z)>C.npc.cull)this.traffic.respawn(c,pl.x,pl.z)}else c.step(dt,0,0,true,false)}
  for(const c of this.cars)c.collide(this.world);crash(this.cars);if(car&&car.hit>9)this.hurt((car.hit-9)*2.2);for(const c of this.cars)if(c.hit>9)this.dmgCar(c,(c.hit-9)*4);this.tt+=dt;this.peds.update(dt,pl.x,pl.z,this.tt,this);
  for(const q of this.peds.p){if(q.dead>0||q.down>0)continue;for(const c of this.cars)if(Math.abs(c.sp)>5&&Math.hypot(c.x-q.x,c.z-q.z)<C.ped.hit){this.killPed(q,c===car);break}}
  let pn=0,pc=0;for(const c of this.cars)if(c.type==='police'||c.type==='tank'){const d=Math.hypot(c.x-pl.x,c.z-pl.z);if(d<22)pn++;if(d<6)pc++;if(c.type==='tank'&&d<30)pn+=3}this.pn=pn;
  if(this.wanted>0&&this.dead<=0){if(pn)this.hurt(1.2*this.wanted*pn*dt);const slow=car?Math.abs(car.sp)<3:Math.hypot(pl.vx,pl.vz)<1.5;this.bust=pc&&slow?this.bust+dt:Math.max(0,this.bust-dt);
   if(this.bust>2.5){this.bust=0;this.die('BUSTED','#6fa8ff',Math.min(this.money,300))}this.evade=pn?0:this.evade+dt;if(this.evade>12)this.setWanted(this.wanted-1)}
  const m=this.mis;if(car&&this.dead<=0){m.time-=dt;if(Math.hypot(car.x-m.x,car.z-m.z)<C.mis.r){const r=Math.round(C.mis.reward+m.d*1.5);if(this.ch&&this.ch.type==='race'){this.cash(this.ch.bonus);this.ch=null}this.cash(r);this.big('MISSION PASSED!','$ '+r.toLocaleString(),'#ffd24a');this.sfx.beep(880);this.nextMission()}else if(m.time<=0){if(this.ch&&this.ch.type==='race')this.ch=null;this.toast('Mission failed: out of time');this.nextMission()}}
  const a=this.sl;for(let i=0;i<60;i++)if(a[i]>0){a[i]-=dt;this.sp[i*3+1]+=dt*1.2;if(a[i]<=0)this.sp[i*3+1]=-100}
  if(car&&car.slip&&Math.abs(car.sp)>5){const sn=Math.sin(car.h),cs=Math.cos(car.h);for(const s of[1,-1]){const i=this.si++%60;this.sp[i*3]=car.x+cs*s-sn*1.4;this.sp[i*3+1]=.4;this.sp[i*3+2]=car.z-sn*s-cs*1.4;a[i]=.8}}
  this.tick2(dt);this.sg.attributes.position.needsUpdate=true}
 mini(x,z,h){const g=this.mg,yaw=this.rig.yaw,th=yaw+Math.PI;g.clearRect(0,0,200,200);g.save();g.beginPath();g.arc(100,100,98,0,7);g.clip();g.translate(100,100);g.rotate(th);
  g.drawImage(this.world.mm,-(x+1300)*.5,-(z+1300)*.5);g.restore();
  const c=Math.cos(th),s=Math.sin(th);g.fillStyle='#ff3d8b';
  for(const o of this.cars){if(!o.ai&&o.type!=='tank')continue;g.fillStyle=o.type==='police'?'#4da3ff':o.type==='tank'?'#9bd15a':'#ff3d8b';const dx=(o.x-x)*.5,dz=(o.z-z)*.5,X=100+dx*c-dz*s,Y=100+dx*s+dz*c;if((X-100)**2+(Y-100)**2<9000)g.fillRect(X-1.5,Y-1.5,3,3)}
  {const pt=(wx,wz,col,r)=>{const dx=(wx-x)*.5,dz=(wz-z)*.5;let X=dx*c-dz*s,Y=dx*s+dz*c;const d=Math.hypot(X,Y);if(d>88){X*=88/d;Y*=88/d}g.fillStyle=col;g.beginPath();g.arc(100+X,100+Y,r,0,7);g.fill()};
  for(const q of SHOPS)pt(q.x,q.mz,q.css,4);for(const o of POI)pt(o.x,o.z,o.c,4);pt(0,-641,'#ffffff',5);if(this.wp)pt(this.wp.x,this.wp.z,'#ff4bd8',4);pt(this.mis.x,this.mis.z,'#ff3030',5)}
  g.save();g.translate(100,100);g.rotate(yaw-h);g.fillStyle='#36f1ff';g.beginPath();g.moveTo(0,-10);g.lineTo(-6,8);g.lineTo(6,8);g.fill();g.restore()}
 hud(){const w=this.world,c=this.driving,pl=this.player,x=c?c.x:pl.x,z=c?c.z:pl.z,h=Math.floor(w.hour),m=Math.floor(w.hour%1*60);
  $('clock').textContent=String(h).padStart(2,'0')+':'+String(m).padStart(2,'0');
  const loc=x>1400?'Interior':(Math.abs(x)>760||z<-760)?'Outskirts':z<-610?'Airport':z>480?'Harbor Docks':(x>240&&x<480&&z>-480&&z<-120)?'Greenfield Park':Math.hypot(x,z)<90?'Central Plaza':Math.hypot(x,z)<300?'Downtown':x<0?'Westgate':'Eastside';
  if(loc!==this.loc){this.loc=loc;$('loc').textContent=loc;const e=$('zone');e.textContent=loc;e.style.animation='none';void e.offsetWidth;e.style.animation='zn 4s forwards'}
  $('speed').style.display=c?'block':'none';if(c){const k=Math.abs(c.sp);$('spd').textContent=Math.round(k*3.6);$('arc').style.strokeDashoffset=226.2*(1-Math.min(1,k/C.car.max))}
  this.near=null;if(!c){let best=C.enter;for(const o of this.cars){if(o.wreck)continue;const d=Math.hypot(o.x-pl.x,o.z-pl.z);if(d<best){best=d;this.near=o}}}
  let ns=null;for(const q of SHOPS)if((!c||q.id==='garage')&&Math.hypot(x-q.x,z-q.mz)<4)ns=q;this.nearShop=ns;if(this.wp&&Math.hypot(x-this.wp.x,z-this.wp.z)<12)this.wp=null;
  this.nearAir=null;if(!c&&!this.flying)for(const a of this.planes)if(a.alive&&Math.hypot(a.x-pl.x,a.z-pl.z)<a.P.span+5)this.nearAir=a;$('prompt').textContent=tr(this.flying?'Press F to exit (when landed)':ns?'Press B — '+ns.name:(!this.near&&this.nearAir)?'Press F to board '+this.nearAir.P.name:'Press F to enter vehicle');$('prompt').style.display=(this.near||ns||this.nearAir||this.flying)?'block':'none';this.mini(x,z,c?c.h:pl.face);
  $('hbi').style.width=Math.max(0,this.health)+'%';$('abi').style.width=this.armor+'%';$('wp').textContent=this.weaponName.toUpperCase()+(WEAP[this.weaponName]?' \u00b7 '+(this.mag[this.weaponName]||0)+'/'+(this.am[this.weaponName]||0)+(this.rl>0?' RELOAD':''):'')+(c?' \u00b7 NOS '+(this.nit|0):'');$('hit').style.opacity=Math.min(1,this.hitT*2);$('xh').style.display=(pl.armed&&!c)?'block':'none';
  const mi=this.mis;let ob='Get in a vehicle';if(c){const t=Math.max(0,mi.time|0);ob='Drive to the red marker \u00b7 '+Math.round(Math.hypot(c.x-mi.x,c.z-mi.z))+' m \u00b7 '+(t/60|0)+':'+String(t%60).padStart(2,'0')}if(this.flying){const a=this.flying;ob=a.P.name+' \u00b7 '+Math.round(a.v*3.6)+' km/h \u00b7 ALT '+Math.round(a.y)+' m \u00b7 THR '+Math.round(a.th*100)+'%'}else if(this.ch)ob=this.ch.txt;$('obj').textContent=tr(ob)}
 loop(t){requestAnimationFrame(t2=>this.loop(t2));document.body.classList.toggle('nc',this.state==='PLAYING'&&!this.shopOpen&&!this.mapOpen&&!this.editing);const dt=Math.min(.1,(t-this.last)/1000);this.last=t;
  if(this.state==='PLAYING'&&!this.shopOpen&&!this.mapOpen){this.acc+=dt;while(this.acc>=1/60){this.fixed(1/60);this.acc-=1/60}
   const c=this.driving;this.sfx.update(c?Math.min(1,Math.abs(c.sp)/C.car.max):0,!!c,c&&this.inp.k.KeyH,c&&c.slip&&Math.abs(c.sp)>5,this.pn>0&&this.wanted>0);
   if(this.world.edge){this.toast('Turn back: edge of the city');this.world.edge=false}
   if(this.toastT>0&&(this.toastT-=dt)<=0)$('toast').style.display='none';
   if(this.bigT>0&&(this.bigT-=dt)<=0)$('ovl').style.display='none';this.hitT=Math.max(0,this.hitT-dt);this.mk.rotation.y=t/700;
   {const ei=.15+.7*(1-this.world.night);for(const o of this.cars){o.body.material.envMapIntensity=ei;if(o.type==='police')o.body.material.emissive.setHex(((t/160)|0)%2?0xff0000:0x0000ff)}}
   {const c=this.driving,I=c?this.world.night*2.4:0;for(let i=0;i<2;i++){const l=this.hl[i];l.intensity=I;if(c){const sn=Math.sin(c.h),cs=Math.cos(c.h),o=i?-.7:.7;l.position.set(c.x+sn*2.1+cs*o,.9,c.z+cs*2.1-sn*o);l.target.position.set(c.x+sn*30+cs*o,0,c.z+cs*30-sn*o)}}}
   this.rig.update(dt,this);this.hud();
   this.fc++;this.ft+=dt;if(this.ft>.5){$('fps').textContent=Math.round(this.fc/this.ft)+' FPS';this.fc=0;this.ft=0}}
  else if(this.state==='MENU')this.rig.update(dt,this);
  if(this.state!=='PAUSED'){const f=this.driving||this.player;this.world.tick(dt,f.x,f.z,t/1000)}
  if(this.mapOpen)this.drawMap();this.world.dome.position.copy(this.cam.position);this.r.render(this.scene,this.cam)}}
Game=new GameCls();window.Game=Game;
})();
</script></body></html>
