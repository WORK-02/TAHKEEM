<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>منصة المسابقات</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&family=Tajawal:wght@400;700;900&display=swap" rel="stylesheet">
<style>
/* ══════════════════ TOKENS ══════════════════ */
:root {
  --bg:#f0f2f8; --s1:#fff; --s2:#f4f5fb; --s3:#eceef6;
  --a1:#4f46e5; --a2:#7c3aed; --a3:#06b6d4;
  --green:#10b981; --orange:#f97316; --red:#ef4444; --gold:#d97706;
  --text:#1a1a2e; --text2:#3d3d5c; --muted:#8888aa;
  --border:rgba(79,70,229,.13); --sh:0 2px 14px rgba(79,70,229,.08);
  --sh2:0 6px 32px rgba(79,70,229,.14); --r:16px;
}
[data-theme=dark]{
  --bg:#0d0d14; --s1:#17172a; --s2:#1e1e32; --s3:#26263e;
  --border:rgba(99,102,241,.16); --text:#eef0ff; --text2:#b0b0d0; --muted:#6060a0;
  --sh:0 2px 14px rgba(0,0,0,.4); --sh2:0 6px 32px rgba(0,0,0,.5);
}
*{margin:0;padding:0;box-sizing:border-box;}
html,body{width:100%;min-height:100vh;}
body{font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);transition:background .3s,color .3s;}

/* ══ SCREENS ══ */
.screen{display:none;width:100%;min-height:100vh;}
.screen.active{display:flex;flex-direction:column;}
.page-fade{position:fixed;inset:0;background:var(--bg);z-index:9999;opacity:0;pointer-events:none;transition:opacity .22s;}
.page-fade.show{opacity:1;pointer-events:all;}

/* ══ REUSE ══ */
.card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:20px;margin-bottom:14px;box-shadow:var(--sh);}
.lbl{font-size:.74rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1.2px;margin-bottom:8px;}
input[type=text],input[type=number],input[type=password],textarea,select{
  width:100%;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;
  padding:10px 14px;color:var(--text);font-family:'Cairo',sans-serif;font-size:.93rem;transition:border-color .2s,box-shadow .2s;
}
textarea{resize:vertical;min-height:70px;}
input:focus,textarea:focus,select:focus{outline:none;border-color:var(--a1);box-shadow:0 0 0 3px rgba(79,70,229,.12);}
.btn{padding:10px 20px;border:none;border-radius:11px;font-family:'Cairo',sans-serif;font-size:.92rem;font-weight:700;cursor:pointer;transition:all .15s;white-space:nowrap;}
.btn-a1{background:var(--a1);color:#fff;box-shadow:0 2px 10px rgba(79,70,229,.28);}
.btn-a1:hover{background:#4338ca;}
.btn-grad{background:linear-gradient(135deg,var(--a1),var(--a2));color:#fff;box-shadow:0 2px 14px rgba(124,58,237,.28);}
.btn-grad:hover{filter:brightness(1.07);}
.btn-green{background:var(--green);color:#fff;}
.btn-green:hover{filter:brightness(1.1);}
.btn-ghost{background:var(--s2);color:var(--text2);border:1.5px solid var(--border);}
.btn-ghost:hover{border-color:var(--a1);color:var(--a1);}
.btn-rg{background:rgba(239,68,68,.1);color:var(--red);border:1px solid rgba(239,68,68,.2);}
.btn-rg:hover{background:rgba(239,68,68,.18);}
.btn-sm{padding:5px 11px;font-size:.8rem;border-radius:8px;}
.btn-orange{background:var(--orange);color:#fff;}
.row{display:flex;gap:9px;}
.row input{flex:1;}
.empty{color:var(--muted);font-size:.86rem;text-align:center;padding:20px 0;}
.divider{border:none;border-top:1px solid var(--border);margin:16px 0;}
.badge{display:inline-flex;align-items:center;padding:3px 10px;border-radius:999px;font-size:.75rem;font-weight:700;}
.badge-a1{background:rgba(79,70,229,.12);color:var(--a1);}
.badge-green{background:rgba(16,185,129,.12);color:var(--green);}
.badge-orange{background:rgba(249,115,22,.12);color:var(--orange);}
.badge-red{background:rgba(239,68,68,.12);color:var(--red);}

/* TOP NAV */
.top-nav{display:flex;align-items:center;justify-content:space-between;padding:13px 24px;background:var(--s1);border-bottom:1px solid var(--border);box-shadow:0 1px 8px rgba(79,70,229,.06);flex-wrap:wrap;gap:10px;position:sticky;top:0;z-index:100;}
.nav-brand{font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.nav-acts{display:flex;gap:7px;align-items:center;}
.icon-btn{width:34px;height:34px;border:1.5px solid var(--border);border-radius:9px;background:var(--s2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:.95rem;transition:all .15s;color:var(--text2);}
.icon-btn:hover{border-color:var(--a1);color:var(--a1);}
.pill{background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:4px 14px;font-size:.82rem;font-weight:700;color:var(--a1);}

/* MODAL */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.45);backdrop-filter:blur(6px);z-index:5000;display:none;align-items:center;justify-content:center;padding:20px;}
.modal-bg.open{display:flex;}
.modal-box{background:var(--s1);border:1px solid var(--border);border-radius:20px;padding:26px;width:100%;max-width:480px;box-shadow:var(--sh2);}
.modal-title{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:900;margin-bottom:14px;}
.modal-acts{display:flex;gap:8px;margin-top:16px;justify-content:flex-end;}

/* TABS */
.tab-bar{display:flex;gap:0;background:var(--s2);border-radius:12px;padding:4px;margin-bottom:16px;}
.tab-btn{flex:1;padding:8px 10px;border:none;border-radius:9px;font-family:'Cairo',sans-serif;font-size:.82rem;font-weight:700;cursor:pointer;background:transparent;color:var(--muted);transition:all .15s;}
.tab-btn.active{background:var(--s1);color:var(--a1);box-shadow:var(--sh);}

/* THEME */
.theme-row{display:flex;gap:7px;justify-content:center;}
.theme-chip{padding:6px 16px;border-radius:999px;font-size:.82rem;font-weight:700;border:1.5px solid var(--border);background:var(--s1);color:var(--muted);cursor:pointer;transition:all .15s;}
.theme-chip.active{background:var(--a1);color:#fff;border-color:var(--a1);}

/* ══════════════════════════════════════
   HOME SCREEN
══════════════════════════════════════ */
#homeScreen{background:var(--bg);}
.home-hero{
  width:100%;padding:52px 20px 36px;text-align:center;
  background:linear-gradient(160deg,rgba(79,70,229,.09) 0%,rgba(124,58,237,.06) 50%,transparent 100%);
  border-bottom:1px solid var(--border);
}
.site-name{font-family:'Tajawal',sans-serif;font-size:2.8rem;font-weight:900;background:linear-gradient(135deg,var(--a1) 20%,var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:6px;line-height:1.1;}
.site-sub{color:var(--muted);font-size:.9rem;margin-bottom:30px;}
.theme-row{margin-top:0;}

/* 4 portal cards */
.portals{display:grid;grid-template-columns:repeat(2,1fr);gap:14px;padding:28px 20px;max-width:760px;margin:0 auto;width:100%;}
@media(max-width:540px){.portals{grid-template-columns:1fr;}}
.portal-card{
  background:var(--s1);border:1.5px solid var(--border);border-radius:20px;
  padding:24px;cursor:pointer;transition:all .2s;box-shadow:var(--sh);
  display:flex;flex-direction:column;align-items:flex-start;gap:10px;
}
.portal-card:hover{border-color:var(--a1);box-shadow:var(--sh2);transform:translateY(-2px);}
.portal-icon{width:52px;height:52px;border-radius:14px;display:flex;align-items:center;justify-content:center;font-size:1.5rem;}
.pi-judge{background:linear-gradient(135deg,var(--a1),var(--a2));}
.pi-player{background:linear-gradient(135deg,var(--green),#059669);}
.pi-display{background:linear-gradient(135deg,var(--orange),#ea580c);}
.pi-bank{background:linear-gradient(135deg,var(--a3),#0284c7);}
.pi-admin{background:linear-gradient(135deg,#6366f1,#4338ca);}
.portal-title{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:900;color:var(--text);}
.portal-desc{font-size:.8rem;color:var(--muted);line-height:1.5;}
.portal-arrow{font-size:1.1rem;color:var(--muted);margin-top:auto;align-self:flex-end;}

/* home stats */
.home-stats{display:flex;gap:10px;padding:0 20px 24px;max-width:760px;width:100%;margin:0 auto;flex-wrap:wrap;}
.stat-c{flex:1;min-width:100px;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:12px 14px;text-align:center;box-shadow:var(--sh);}
.stat-n{font-family:'Tajawal',sans-serif;font-size:1.7rem;font-weight:900;color:var(--a1);}
.stat-l{font-size:.72rem;color:var(--muted);font-weight:700;}

/* ══════════════════════════════════════
   PIN SCREEN
══════════════════════════════════════ */
#pinScreen{align-items:center;justify-content:center;background:var(--bg);}
.pin-box{background:var(--s1);border:1px solid var(--border);border-radius:24px;padding:36px;width:100%;max-width:380px;text-align:center;box-shadow:var(--sh2);}
.pin-icon{font-size:3rem;margin-bottom:12px;}
.pin-title{font-family:'Tajawal',sans-serif;font-size:1.3rem;font-weight:900;margin-bottom:6px;}
.pin-sub{color:var(--muted);font-size:.86rem;margin-bottom:22px;}
.pin-input-wrap{display:flex;gap:10px;justify-content:center;margin-bottom:18px;}
.pin-digit{width:52px;height:60px;text-align:center;font-size:1.6rem;font-weight:900;font-family:'Tajawal',sans-serif;letter-spacing:2px;border-radius:14px;}
.pin-error{color:var(--red);font-size:.84rem;min-height:20px;margin-bottom:10px;}
.pin-keypad{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;max-width:200px;margin:0 auto;}
.pk-btn{padding:14px;background:var(--s2);border:1.5px solid var(--border);border-radius:12px;font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:700;cursor:pointer;transition:all .13s;color:var(--text);}
.pk-btn:hover{background:var(--a1);color:#fff;border-color:var(--a1);}
.pk-btn.del{background:rgba(239,68,68,.08);color:var(--red);border-color:rgba(239,68,68,.2);}

/* ══════════════════════════════════════
   SETUP WIZARD
══════════════════════════════════════ */
#setupScreen{background:var(--bg);}
.setup-body{flex:1;padding:20px 24px;max-width:620px;width:100%;margin:0 auto;}
.wiz-steps{display:flex;gap:0;margin-bottom:22px;position:relative;}
.wiz-steps::before{content:'';position:absolute;top:14px;right:28px;left:28px;height:2px;background:var(--border);z-index:0;}
.w-step{flex:1;text-align:center;position:relative;z-index:1;}
.w-dot{width:28px;height:28px;border-radius:50%;border:2px solid var(--border);background:var(--s1);display:flex;align-items:center;justify-content:center;margin:0 auto 4px;font-size:.78rem;font-weight:700;color:var(--muted);transition:all .3s;}
.w-step.active .w-dot{background:var(--a1);border-color:var(--a1);color:#fff;}
.w-step.done .w-dot{background:var(--green);border-color:var(--green);color:#fff;}
.w-label{font-size:.7rem;color:var(--muted);font-weight:700;}
.w-step.active .w-label{color:var(--a1);}
.wiz-panel{display:none;}
.wiz-panel.active{display:block;}
.wiz-nav{display:flex;gap:9px;margin-top:16px;}
.wiz-nav .btn{flex:1;padding:12px;}
.pts-tags{display:flex;flex-wrap:wrap;gap:7px;margin-top:10px;}
.pts-tag{display:flex;align-items:center;gap:5px;background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:5px 12px;font-size:.87rem;font-weight:700;color:var(--a1);}
.pts-tag button{background:none;border:none;color:var(--muted);cursor:pointer;font-size:.88rem;}
.pts-tag button:hover{color:var(--red);}

/* PIN setup */
.pin-setup-display{display:flex;gap:8px;justify-content:center;margin:12px 0;}
.psd-dot{width:14px;height:14px;border-radius:50%;border:2px solid var(--border);background:transparent;transition:background .2s;}
.psd-dot.filled{background:var(--a1);border-color:var(--a1);}
.pin-keypad-sm{display:grid;grid-template-columns:repeat(3,1fr);gap:7px;max-width:180px;margin:0 auto;}
.pk-sm{padding:11px;background:var(--s2);border:1.5px solid var(--border);border-radius:10px;font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:700;cursor:pointer;transition:all .13s;color:var(--text);text-align:center;}
.pk-sm:hover{background:var(--a1);color:#fff;border-color:var(--a1);}
.pk-sm.del{color:var(--red);}

/* ══════════════════════════════════════
   JUDGE SCREEN
══════════════════════════════════════ */
#judgeScreen{background:var(--bg);}
.judge-body{flex:1;padding:18px 22px;max-width:700px;width:100%;margin:0 auto;}

/* timer */
.timer-box{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:13px 18px;margin-bottom:14px;box-shadow:var(--sh);}
.timer-disp{font-family:'Tajawal',sans-serif;font-size:2.3rem;font-weight:900;color:var(--a1);min-width:90px;text-align:center;letter-spacing:2px;transition:color .3s;}
.timer-disp.urgent{color:var(--red);animation:blink .6s ease-in-out infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:.5;}}
.t-pres{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:6px;}
.t-pre{padding:5px 11px;background:var(--s2);border:1.5px solid var(--border);border-radius:8px;font-size:.79rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .13s;}
.t-pre:hover{border-color:var(--a3);color:var(--a3);}
.t-ctrls{display:flex;gap:6px;}
.t-btn{width:33px;height:33px;border:1.5px solid var(--border);border-radius:9px;background:var(--s2);font-size:.9rem;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .13s;color:var(--text2);}
.t-btn:hover{border-color:var(--a1);color:var(--a1);}
.t-btn.on{background:var(--green);border-color:var(--green);color:#fff;}

/* active q */
.aq-box{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:14px 18px;margin-bottom:14px;box-shadow:var(--sh);}
.aq-lbl{font-size:.72rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:5px;}
.aq-text{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:700;line-height:1.6;}
.aq-ans{font-size:.87rem;color:var(--green);font-weight:700;margin-top:5px;display:none;}
.aq-ans.show{display:block;}
.aq-pts{font-size:.78rem;color:var(--muted);margin-top:3px;}
.aq-acts{display:flex;gap:7px;margin-top:10px;flex-wrap:wrap;}

/* pts */
.pts-chips{display:flex;flex-wrap:wrap;gap:7px;margin:10px 0 16px;}
.pts-chip{padding:6px 15px;background:var(--s1);border:1.5px solid var(--border);border-radius:9px;font-size:.9rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .13s;box-shadow:var(--sh);}
.pts-chip:hover{border-color:var(--a1);color:var(--a1);}
.pts-chip.sel{background:var(--a1);border-color:var(--a1);color:#fff;}

/* teams */
.team-row{display:flex;align-items:center;justify-content:space-between;background:var(--s1);border:1.5px solid var(--border);border-radius:14px;padding:12px 16px;margin-bottom:9px;cursor:pointer;transition:all .18s;gap:12px;box-shadow:var(--sh);}
.team-row:hover{border-color:var(--a1);box-shadow:var(--sh2);}
.team-row.winner{border-color:var(--green);background:rgba(16,185,129,.06);box-shadow:0 4px 20px rgba(16,185,129,.15);}
.tr-name{font-family:'Tajawal',sans-serif;font-size:1rem;font-weight:700;flex:1;}
.tr-score{font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:900;color:var(--gold);}
.award-badge{padding:4px 10px;background:var(--green);color:#fff;border-radius:7px;font-size:.78rem;font-weight:700;opacity:0;transition:opacity .2s;}
.team-row.winner .award-badge{opacity:1;}

.action-bar{margin-top:12px;padding:13px 16px;background:var(--s1);border:1px solid var(--border);border-radius:14px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;box-shadow:var(--sh);}

/* log */
.log-wrap{max-height:160px;overflow-y:auto;margin-top:10px;}
.log-item{display:flex;align-items:center;justify-content:space-between;padding:6px 11px;background:var(--s2);border-radius:9px;margin-bottom:5px;font-size:.81rem;}
.log-q{color:var(--muted);}
.log-w{font-weight:700;}
.log-p{color:var(--green);font-weight:900;}

/* ══════════════════════════════════════
   PLAYER SCREEN (contestants view)
══════════════════════════════════════ */
#playerScreen{background:var(--bg);align-items:center;}
.player-body{width:100%;max-width:720px;padding:28px 20px 44px;}
.player-comp-name{font-family:'Tajawal',sans-serif;font-size:2rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-align:center;margin-bottom:6px;}
.player-meta{text-align:center;color:var(--muted);font-size:.86rem;margin-bottom:24px;}
/* rankings same as live */
.rankings-wrap{width:100%;position:relative;}
.rank-card{position:absolute;left:0;width:100%;display:flex;align-items:center;gap:14px;background:var(--s1);border:1.5px solid var(--border);border-radius:18px;padding:15px 20px;overflow:hidden;box-shadow:var(--sh);transition:top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s;}
.rank-card.rank-1{border-color:rgba(217,119,6,.4);background:linear-gradient(135deg,#fffbeb,#fef3c7 60%,var(--s1));}
.rank-card.rank-2{border-color:rgba(107,114,128,.25);}
.rank-card.rank-3{border-color:rgba(146,64,14,.25);}
.rank-card.just-scored{border-color:var(--green)!important;box-shadow:0 0 0 3px rgba(16,185,129,.14),var(--sh2)!important;}
.rank-medal{width:40px;height:40px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:900;flex-shrink:0;}
.rank-1 .rank-medal{background:linear-gradient(135deg,#fde68a,#d97706);color:#fff;box-shadow:0 2px 10px rgba(217,119,6,.38);}
.rank-2 .rank-medal{background:linear-gradient(135deg,#e5e7eb,#9ca3af);color:#fff;}
.rank-3 .rank-medal{background:linear-gradient(135deg,#fcd34d,#92400e);color:#fff;}
.rank-other .rank-medal{background:var(--s3);color:var(--muted);font-size:1rem;}
.rank-name{flex:1;font-family:'Tajawal',sans-serif;font-size:1.15rem;font-weight:700;}
.rank-score{font-family:'Tajawal',sans-serif;font-size:1.5rem;font-weight:900;color:var(--a1);min-width:80px;text-align:left;}
.rank-1 .rank-score{color:var(--gold);}
.score-bar-track{position:absolute;bottom:0;right:0;left:0;height:4px;background:rgba(79,70,229,.06);}
.score-bar-fill{height:100%;background:linear-gradient(90deg,var(--a3),var(--a1),var(--a2));transition:width .85s cubic-bezier(.4,0,.2,1);border-radius:0 0 0 18px;}
.float-pts{position:absolute;font-family:'Tajawal',sans-serif;font-size:1.5rem;font-weight:900;color:var(--green);pointer-events:none;text-shadow:0 2px 10px rgba(16,185,129,.3);animation:floatUp 1.2s ease-out forwards;right:90px;top:6px;z-index:20;}
@keyframes floatUp{0%{opacity:1;transform:translateY(0) scale(.9);}30%{opacity:1;transform:translateY(-14px) scale(1.2);}100%{opacity:0;transform:translateY(-52px) scale(.85);}}

/* question box for player */
.player-q-box{background:var(--s1);border:2px solid rgba(79,70,229,.15);border-radius:18px;padding:20px 24px;margin-bottom:24px;box-shadow:var(--sh2);text-align:center;display:none;}
.player-q-box.show{display:block;}
.player-q-text{font-family:'Tajawal',sans-serif;font-size:1.3rem;font-weight:700;line-height:1.6;}
.player-timer{font-family:'Tajawal',sans-serif;font-size:3.5rem;font-weight:900;color:var(--a1);margin-top:10px;transition:color .3s;}
.player-timer.urgent{color:var(--red);}

/* ══════════════════════════════════════
   DISPLAY SCREEN (big screen)
══════════════════════════════════════ */
#displayScreen{
  align-items:center;justify-content:center;
  background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.12) 0%,transparent 58%),var(--bg);
  padding:24px 20px 40px;
}
.disp-wrap{width:100%;max-width:900px;}
.disp-comp-name{font-family:'Tajawal',sans-serif;font-size:3rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-align:center;margin-bottom:8px;}
.disp-meta{text-align:center;margin-bottom:20px;}
.disp-q-box{background:var(--s1);border:2px solid rgba(79,70,229,.18);border-radius:20px;padding:22px 30px;margin-bottom:24px;box-shadow:var(--sh2);text-align:center;display:none;}
.disp-q-box.show{display:block;}
.disp-q-text{font-family:'Tajawal',sans-serif;font-size:1.6rem;font-weight:700;line-height:1.6;}
.disp-timer{font-family:'Tajawal',sans-serif;font-size:4rem;font-weight:900;color:var(--a1);margin-top:10px;transition:color .3s;}
.disp-timer.urgent{color:var(--red);animation:blink .6s ease-in-out infinite;}

/* ══════════════════════════════════════
   QUESTION BANK
══════════════════════════════════════ */
#bankScreen{background:var(--bg);}
.bank-body{flex:1;padding:18px 22px;max-width:820px;width:100%;margin:0 auto;}
.cat-box{background:var(--s1);border:1px solid var(--border);border-radius:16px;margin-bottom:12px;box-shadow:var(--sh);overflow:hidden;}
.cat-header{display:flex;align-items:center;justify-content:space-between;padding:14px 18px;cursor:pointer;gap:10px;transition:background .15s;}
.cat-header:hover{background:var(--s2);}
.cat-title{font-family:'Tajawal',sans-serif;font-size:1rem;font-weight:900;flex:1;}
.cat-meta{font-size:.76rem;color:var(--muted);}
.cat-arrow{transition:transform .25s;color:var(--muted);}
.cat-box.open .cat-arrow{transform:rotate(90deg);}
.cat-body{display:none;padding:0 16px 14px;}
.cat-box.open .cat-body{display:block;}
.q-item{display:flex;align-items:flex-start;gap:10px;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:10px 13px;margin-bottom:7px;}
.q-item-txt{flex:1;}
.q-text{font-size:.9rem;font-weight:600;line-height:1.5;}
.q-answer{font-size:.79rem;color:var(--green);margin-top:3px;font-weight:700;}
.q-pts-badge{font-size:.73rem;color:var(--muted);margin-top:2px;}
.q-used{opacity:.42;}
.q-pending{border-color:rgba(249,115,22,.3);background:rgba(249,115,22,.04);}
.cat-add-row{display:flex;gap:7px;margin-top:10px;flex-wrap:wrap;}
.cat-add-row input{flex:1;min-width:120px;}

/* AI panel */
.ai-panel{background:linear-gradient(135deg,rgba(79,70,229,.06),rgba(124,58,237,.06));border:1.5px solid rgba(79,70,229,.18);border-radius:12px;padding:14px;margin-top:10px;}
.ai-panel-title{font-size:.82rem;font-weight:700;color:var(--a1);margin-bottom:10px;display:flex;align-items:center;gap:6px;}
.ai-q-chip{display:flex;align-items:flex-start;gap:9px;background:var(--s1);border:1px solid var(--border);border-radius:9px;padding:10px 12px;margin-bottom:7px;}
.ai-q-text{flex:1;font-size:.87rem;line-height:1.5;}
.ai-q-ans{font-size:.78rem;color:var(--green);font-weight:700;margin-top:2px;}

/* ══════════════════════════════════════
   LIVE / FINALE
══════════════════════════════════════ */
#liveScreen{align-items:center;padding:28px 20px 44px;background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.1) 0%,transparent 58%),radial-gradient(ellipse 50% 40% at 100% 100%,rgba(6,182,212,.07) 0%,transparent 55%),var(--bg);}
.live-head{width:100%;max-width:720px;text-align:center;margin-bottom:28px;}
.live-comp-name{font-family:'Tajawal',sans-serif;font-size:2.3rem;font-weight:900;background:linear-gradient(135deg,var(--a1) 20%,var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:8px;line-height:1.2;}
.live-meta-pill{display:inline-flex;gap:8px;align-items:center;background:var(--s1);border:1.5px solid var(--border);border-radius:999px;padding:7px 20px;font-size:.87rem;font-weight:700;color:var(--muted);box-shadow:var(--sh);}
.live-meta-pill b{color:var(--a1);}
.live-rw{width:100%;max-width:720px;position:relative;}
.live-footer{width:100%;max-width:720px;margin-top:22px;display:flex;gap:9px;flex-wrap:wrap;}
.live-footer .btn{flex:1;padding:12px;font-size:.96rem;}

/* finale */
#finaleScreen{align-items:center;justify-content:center;padding:40px 20px;background:radial-gradient(ellipse 90% 60% at 50% 0%,rgba(79,70,229,.14) 0%,transparent 65%),var(--bg);}
.finale-wrap{width:100%;max-width:640px;text-align:center;}
.finale-trophy{font-size:5rem;margin-bottom:12px;animation:tBounce .8s ease-out;}
@keyframes tBounce{0%{transform:scale(.5) translateY(30px);opacity:0;}70%{transform:scale(1.15) translateY(-10px);}100%{transform:scale(1) translateY(0);opacity:1;}}
.finale-winner-name{font-family:'Tajawal',sans-serif;font-size:2.6rem;font-weight:900;background:linear-gradient(135deg,var(--gold),var(--orange));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:24px;}
.podium{display:flex;align-items:flex-end;justify-content:center;gap:10px;margin:24px 0 30px;}
.podium-item{display:flex;flex-direction:column;align-items:center;gap:5px;}
.podium-bar{width:72px;border-radius:8px 8px 0 0;display:flex;align-items:center;justify-content:center;font-size:1.5rem;}
.p1 .podium-bar{height:90px;background:linear-gradient(180deg,#fde68a,#d97706);}
.p2 .podium-bar{height:60px;background:linear-gradient(180deg,#e5e7eb,#9ca3af);}
.p3 .podium-bar{height:45px;background:linear-gradient(180deg,#fcd34d,#92400e);}
.podium-name{font-family:'Tajawal',sans-serif;font-weight:700;font-size:.88rem;max-width:86px;text-align:center;}
.podium-score{font-size:.8rem;color:var(--gold);font-weight:900;}
.finale-acts{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;}
.summary-t{width:100%;border-collapse:collapse;margin-top:16px;text-align:right;}
.summary-t th{font-size:.74rem;font-weight:700;color:var(--muted);padding:8px 12px;border-bottom:1px solid var(--border);text-transform:uppercase;}
.summary-t td{padding:8px 12px;border-bottom:1px solid var(--border);font-size:.86rem;}
.summary-t tr:last-child td{border:none;}

/* PARTICLES / FLASH */
.particles{position:fixed;inset:0;pointer-events:none;z-index:999;}
.prt{position:absolute;border-radius:3px;animation:prtFall linear forwards;}
@keyframes prtFall{0%{transform:translateY(-10px) rotate(0deg);opacity:1;}100%{transform:translateY(110vh) rotate(700deg);opacity:0;}}
.flash-el{position:fixed;inset:0;pointer-events:none;z-index:998;opacity:0;background:rgba(16,185,129,.08);transition:opacity .15s;}
.flash-el.on{opacity:1;}

/* SCROLLBAR */
::-webkit-scrollbar{width:6px;height:6px;}
::-webkit-scrollbar-thumb{background:var(--border);border-radius:3px;}

@media(max-width:600px){
  .live-comp-name,.disp-comp-name{font-size:1.7rem;}
  .rank-name{font-size:1rem;}.rank-score{font-size:1.3rem;}
  .judge-body,.bank-body{padding:12px;}
  .top-nav{padding:12px 14px;}
}
</style>
</head>
<body>
<div class="particles" id="particles"></div>
<div class="flash-el" id="flash"></div>
<div class="page-fade" id="pageFade"></div>

<!-- ══════════ HOME ══════════ -->
<div class="screen active" id="homeScreen">
  <div class="home-hero">
    <div class="site-name" id="siteNameEl">منصة المسابقات</div>
    <div class="site-sub">اختر القسم المناسب للمتابعة</div>
    <div class="theme-row">
      <div class="theme-chip" data-mode="light" onclick="setTheme('light')">فاتح</div>
      <div class="theme-chip" data-mode="auto" onclick="setTheme('auto')">تلقائي</div>
      <div class="theme-chip" data-mode="dark" onclick="setTheme('dark')">داكن</div>
    </div>
  </div>

  <div class="home-stats" id="homeStats"></div>

  <div class="portals">
    <div class="portal-card" onclick="enterJudge()">
      <div class="portal-icon pi-judge">⚖️</div>
      <div class="portal-title">قسم المحكمين</div>
      <div class="portal-desc">إدارة كاملة — تسجيل النتائج، المؤقت، بنك الأسئلة، التحكم الكامل</div>
      <div class="portal-arrow">←</div>
    </div>
    <div class="portal-card" onclick="enterPlayer()">
      <div class="portal-icon pi-player">🏅</div>
      <div class="portal-title">قسم المتسابقين</div>
      <div class="portal-desc">عرض الترتيب والنتائج الحية فقط — بدون صلاحيات تعديل</div>
      <div class="portal-arrow">←</div>
    </div>
    <div class="portal-card" onclick="enterDisplay()">
      <div class="portal-icon pi-display">📺</div>
      <div class="portal-title">شاشة العرض</div>
      <div class="portal-desc">للشاشة الكبيرة — الترتيب والمؤقت والسؤال بخط كبير واضح</div>
      <div class="portal-arrow">←</div>
    </div>
    <div class="portal-card" onclick="enterBank()">
      <div class="portal-icon pi-bank">📚</div>
      <div class="portal-title">بنك الأسئلة</div>
      <div class="portal-desc">استعراض الأسئلة واقتراح أسئلة جديدة (تحتاج موافقة المحكم)</div>
      <div class="portal-arrow">←</div>
    </div>
    <div class="portal-card" onclick="enterAdmin()">
      <div class="portal-icon pi-admin">🛡️</div>
      <div class="portal-title">لوحة المشرف</div>
      <div class="portal-desc">إعدادات الموقع، الرموز السرية، المسابقات المحفوظة</div>
      <div class="portal-arrow">←</div>
    </div>
  </div>
</div>

<!-- ══════════ PIN SCREEN ══════════ -->
<div class="screen" id="pinScreen">
  <div class="pin-box">
    <div class="pin-icon" id="pinIcon">🔐</div>
    <div class="pin-title" id="pinTitle">أدخل الرمز السري</div>
    <div class="pin-sub" id="pinSub">هذا القسم محمي برمز سري</div>
    <div class="pin-input-wrap">
      <input type="password" id="pinInput" maxlength="6" style="text-align:center;font-size:1.6rem;letter-spacing:8px;max-width:200px;" placeholder="••••" autocomplete="off" oninput="onPinInput(this.value)" onkeydown="if(event.key==='Enter')checkPin()">
    </div>
    <div class="pin-error" id="pinError"></div>
    <div style="display:flex;gap:9px;justify-content:center;">
      <button class="btn btn-grad" onclick="checkPin()">دخول</button>
      <button class="btn btn-ghost" onclick="goTo('homeScreen')">رجوع</button>
    </div>
  </div>
</div>

<!-- ══════════ SETUP WIZARD ══════════ -->
<div class="screen" id="setupScreen">
  <div class="top-nav">
    <div class="nav-brand" id="setupBrand">مسابقة جديدة</div>
    <div class="nav-acts">
      <div class="icon-btn" onclick="goHome()">✕</div>
    </div>
  </div>
  <div class="setup-body">
    <div class="wiz-steps">
      <div class="w-step active" id="ws0"><div class="w-dot">1</div><div class="w-label">الهوية</div></div>
      <div class="w-step" id="ws1"><div class="w-dot">2</div><div class="w-label">الفرق</div></div>
      <div class="w-step" id="ws2"><div class="w-dot">3</div><div class="w-label">النقاط</div></div>
      <div class="w-step" id="ws3"><div class="w-dot">4</div><div class="w-label">الرمز</div></div>
    </div>

    <!-- step 0 -->
    <div class="wiz-panel active" id="wp0">
      <div class="card">
        <div class="lbl">اسم المسابقة</div>
        <input type="text" id="setupTitle" placeholder="مثال: مسابقة الثقافة العامة" style="margin-bottom:10px;">
        <div class="lbl">اسم المجموعة (اختياري)</div>
        <input type="text" id="setupGroup" placeholder="مثال: طلاب الفصل الثالث" style="margin-bottom:10px;">
        <div class="lbl">ترتيب الأسئلة</div>
        <div style="display:flex;gap:9px;">
          <label style="flex:1;display:flex;align-items:center;gap:8px;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;padding:10px 13px;cursor:pointer;"><input type="radio" name="qord" value="ordered" checked style="width:auto;"> مرتب</label>
          <label style="flex:1;display:flex;align-items:center;gap:8px;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;padding:10px 13px;cursor:pointer;"><input type="radio" name="qord" value="random" style="width:auto;"> عشوائي</label>
        </div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-ghost" onclick="goHome()">إلغاء</button>
        <button class="btn btn-grad" onclick="wizNext(0)">التالي ←</button>
      </div>
    </div>

    <!-- step 1 -->
    <div class="wiz-panel" id="wp1">
      <div class="card">
        <div class="lbl">اضافة فريق</div>
        <div class="row">
          <input type="text" id="teamInp" placeholder="اسم الفريق" onkeydown="if(event.key==='Enter')addTeam()">
          <button class="btn btn-a1" onclick="addTeam()">اضافة</button>
        </div>
        <div id="teamsList" style="margin-top:10px;"><div class="empty">لا توجد فرق بعد</div></div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-ghost" onclick="wizPrev(1)">→ السابق</button>
        <button class="btn btn-grad" onclick="wizNext(1)">التالي ←</button>
      </div>
    </div>

    <!-- step 2 -->
    <div class="wiz-panel" id="wp2">
      <div class="card">
        <div class="lbl">فئات النقاط</div>
        <div class="pts-tags" id="ptsTagWrap"></div>
        <div class="row" style="margin-top:10px;">
          <input type="number" id="ptsAddInp" placeholder="فئة جديدة" min="10" step="50" style="max-width:180px;">
          <button class="btn btn-ghost btn-sm" onclick="addPtsTag()" style="padding:10px 16px;">اضافة</button>
          <button class="btn btn-ghost btn-sm" onclick="resetPts()" style="padding:10px 12px;">افتراضي</button>
        </div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-ghost" onclick="wizPrev(2)">→ السابق</button>
        <button class="btn btn-grad" onclick="wizNext(2)">التالي ←</button>
      </div>
    </div>

    <!-- step 3: PIN -->
    <div class="wiz-panel" id="wp3">
      <div class="card">
        <div class="lbl">رمز سري لهذه المسابقة (4-6 أرقام)</div>
        <p style="font-size:.84rem;color:var(--muted);margin-bottom:12px;">هذا الرمز يحمي نتائج المسابقة ويسمح للمحكم بالدخول. احفظه جيداً.</p>
        <input type="password" id="compPinInp" maxlength="6" placeholder="أدخل الرمز" style="text-align:center;font-size:1.4rem;letter-spacing:6px;margin-bottom:10px;" autocomplete="off">
        <input type="password" id="compPinConf" maxlength="6" placeholder="أعد الرمز للتأكيد" style="text-align:center;font-size:1.4rem;letter-spacing:6px;" autocomplete="off">
        <div style="font-size:.8rem;color:var(--muted);margin-top:8px;">أو اترك فارغاً للدخول بدون رمز</div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-ghost" onclick="wizPrev(3)">→ السابق</button>
        <button class="btn btn-grad" onclick="setupDone()">بدء المسابقة ✓</button>
      </div>
    </div>
  </div>
</div>

<!-- ══════════ JUDGE ══════════ -->
<div class="screen" id="judgeScreen">
  <div class="top-nav">
    <div class="nav-brand" id="judgeBrand">المسابقة</div>
    <div class="nav-acts">
      <div class="pill">س <span id="qNum">1</span></div>
      <div class="icon-btn" onclick="goTo('bankScreen')" title="بنك الأسئلة">📚</div>
      <div class="icon-btn" onclick="openJudgeSettings()" title="الاعدادات">⚙</div>
      <div class="icon-btn" onclick="goHome()" title="الرئيسية">⌂</div>
    </div>
  </div>
  <div class="judge-body">
    <!-- timer -->
    <div class="timer-box">
      <div class="timer-disp" id="timerDisp">00:30</div>
      <div>
        <div class="t-pres">
          <div class="t-pre" onclick="setTimer(10)">10ث</div>
          <div class="t-pre" onclick="setTimer(15)">15ث</div>
          <div class="t-pre" onclick="setTimer(30)">30ث</div>
          <div class="t-pre" onclick="setTimer(60)">1د</div>
          <div class="t-pre" onclick="setTimer(90)">90ث</div>
          <div class="t-pre" onclick="setTimer(120)">2د</div>
        </div>
        <div class="t-ctrls">
          <div class="t-btn" id="tPlayBtn" onclick="toggleTimer()">▶</div>
          <div class="t-btn" onclick="resetTimer()">↺</div>
          <div class="t-btn" onclick="pushState()" title="تحديث شاشة المتسابقين">↑</div>
        </div>
      </div>
    </div>

    <!-- active question -->
    <div class="aq-box">
      <div class="aq-lbl">السؤال الحالي</div>
      <div class="aq-text" id="aqText">اختر سؤالاً من البنك أو تجاوز مباشرة</div>
      <div class="aq-ans" id="aqAns"></div>
      <div class="aq-pts" id="aqPts"></div>
      <div class="aq-acts">
        <button class="btn btn-ghost btn-sm" onclick="toggleAns()">إظهار الإجابة</button>
        <button class="btn btn-ghost btn-sm" onclick="pickQ()">سؤال آخر من البنك</button>
        <button class="btn btn-ghost btn-sm" id="sendQBtn" onclick="toggleSendQ()">إرسال للشاشة</button>
      </div>
    </div>

    <div class="lbl">النقاط لهذا السؤال</div>
    <div class="pts-chips" id="ptsChips"></div>

    <div class="lbl">الفريق الفائز بهذا السؤال</div>
    <div id="teamBtns"></div>

    <div class="action-bar">
      <button class="btn btn-ghost btn-sm" id="undoBtn" onclick="undoLast()" disabled>↩ تراجع</button>
      <div style="display:flex;gap:8px;flex-wrap:wrap;">
        <button class="btn btn-ghost btn-sm" onclick="showFinale()">إنهاء</button>
        <button class="btn btn-grad" onclick="confirmAndNext()">تسجيل وعرض اللوحة</button>
      </div>
    </div>

    <div style="margin-top:14px;">
      <div class="lbl">سجل الأسئلة</div>
      <div class="log-wrap" id="histLog"><div class="empty">لا يوجد سجل بعد</div></div>
    </div>
  </div>
</div>

<!-- ══════════ PLAYER ══════════ -->
<div class="screen" id="playerScreen">
  <div class="top-nav">
    <div class="nav-brand" id="playerBrand">المتسابقون</div>
    <div class="nav-acts">
      <div class="pill">س <span id="playerQ">—</span></div>
      <div class="icon-btn" onclick="goHome()">⌂</div>
    </div>
  </div>
  <div class="player-body">
    <div class="player-comp-name" id="playerCompName">—</div>
    <div class="player-meta" id="playerMeta"></div>
    <div class="player-q-box" id="playerQBox">
      <div class="player-q-text" id="playerQText"></div>
      <div class="player-timer" id="playerTimer">—</div>
    </div>
    <div class="rankings-wrap" id="playerRankings" style="position:relative;"></div>
  </div>
</div>

<!-- ══════════ DISPLAY (big screen) ══════════ -->
<div class="screen" id="displayScreen">
  <div style="display:flex;justify-content:flex-end;padding:12px 18px;position:absolute;top:0;right:0;z-index:10;">
    <div class="icon-btn" onclick="goHome()">⌂</div>
  </div>
  <div class="disp-wrap">
    <div class="disp-comp-name" id="dispCompName">—</div>
    <div class="disp-meta">
      <span class="live-meta-pill" id="dispMeta">السؤال <b id="dispQ">—</b></span>
    </div>
    <div class="disp-q-box" id="dispQBox">
      <div class="disp-q-text" id="dispQText"></div>
      <div class="disp-timer" id="dispTimer">—</div>
    </div>
    <div class="rankings-wrap" id="dispRankings" style="position:relative;"></div>
  </div>
</div>

<!-- ══════════ BANK ══════════ -->
<div class="screen" id="bankScreen">
  <div class="top-nav">
    <div class="nav-brand">بنك الأسئلة</div>
    <div class="nav-acts">
      <div class="icon-btn" id="bankAddCatBtn" onclick="addCategory()" title="تصنيف جديد" style="display:none;">+</div>
      <div class="icon-btn" id="bankAIBtn" onclick="openAIModal(null)" title="توليد أسئلة" style="display:none;">✦</div>
      <div class="icon-btn" onclick="returnFromBank()">←</div>
    </div>
  </div>
  <div class="bank-body">
    <div id="bankPendingSection" style="display:none;">
      <div class="lbl" style="color:var(--orange);">أسئلة بانتظار الموافقة <span id="pendingCount" class="badge badge-orange"></span></div>
      <div id="pendingList" style="margin-bottom:18px;"></div>
    </div>
    <div id="bankCats"><div class="empty">لا توجد تصنيفات</div></div>
  </div>
</div>

<!-- ══════════ LIVE ══════════ -->
<div class="screen" id="liveScreen">
  <div class="live-head">
    <div class="live-comp-name" id="liveName">—</div>
    <div class="live-meta-pill" id="liveMeta">السؤال <b id="liveQ">—</b></div>
  </div>
  <div class="live-rw" id="liveRankings"></div>
  <div class="live-footer" id="liveFooter"></div>
</div>

<!-- ══════════ FINALE ══════════ -->
<div class="screen" id="finaleScreen">
  <div class="finale-wrap">
    <div class="finale-trophy">🏆</div>
    <div style="color:var(--muted);font-size:1rem;font-weight:700;margin-bottom:4px;">الفائز</div>
    <div class="finale-winner-name" id="finaleWinner">—</div>
    <div class="podium" id="finalePodium"></div>
    <div class="finale-acts">
      <button class="btn btn-grad" onclick="goHome()">الرئيسية</button>
      <button class="btn btn-ghost" onclick="toggleSummary()">ملخص المسابقة</button>
    </div>
    <div id="summarySection" style="display:none;margin-top:20px;text-align:right;">
      <table class="summary-t" id="summaryTable"></table>
    </div>
  </div>
</div>

<!-- ══════════ ADMIN MODAL ══════════ -->
<div class="modal-bg" id="adminModal">
  <div class="modal-box" style="max-width:520px;">
    <div class="modal-title">🛡️ لوحة المشرف</div>
    <div class="tab-bar">
      <button class="tab-btn active" onclick="adminTab(0)">الموقع</button>
      <button class="tab-btn" onclick="adminTab(1)">المسابقات</button>
      <button class="tab-btn" onclick="adminTab(2)">الرمز</button>
    </div>
    <div id="adm0">
      <div class="lbl">اسم الموقع</div>
      <input type="text" id="admSiteName" placeholder="منصة المسابقات" style="margin-bottom:10px;">
      <div class="lbl">رمز المشرف الحالي</div>
      <input type="password" id="admPinChange" placeholder="رمز جديد (4-6 أرقام)" autocomplete="off">
      <div style="font-size:.8rem;color:var(--muted);margin-top:6px;">الرمز الافتراضي: 1234</div>
    </div>
    <div id="adm1" style="display:none;">
      <div id="admHistList"><div class="empty">لا توجد مسابقات</div></div>
    </div>
    <div id="adm2" style="display:none;">
      <p style="font-size:.88rem;color:var(--text2);margin-bottom:12px;">رمز المشرف يمنح الوصول الكامل للوحة الإدارة وبنك الأسئلة بصلاحيات كاملة.</p>
      <div class="lbl">رمز المشرف الجديد</div>
      <input type="password" id="admNewPin" placeholder="4-6 أرقام" autocomplete="off">
    </div>
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="saveAdmin()">حفظ</button>
      <button class="btn btn-ghost" onclick="closeModal('adminModal')">إغلاق</button>
    </div>
  </div>
</div>

<!-- Judge Settings Modal -->
<div class="modal-bg" id="judgeSettingsModal">
  <div class="modal-box">
    <div class="modal-title">⚙ إعدادات المسابقة</div>
    <div class="tab-bar">
      <button class="tab-btn active" onclick="jsTab(0)">الفرق</button>
      <button class="tab-btn" onclick="jsTab(1)">النقاط</button>
      <button class="tab-btn" onclick="jsTab(2)">المسابقة</button>
    </div>
    <div id="js0">
      <div class="row" style="margin-bottom:10px;">
        <input type="text" id="jsTeamInp" placeholder="فريق جديد" onkeydown="if(event.key==='Enter')jsAddTeam()">
        <button class="btn btn-a1" onclick="jsAddTeam()">اضافة</button>
      </div>
      <div id="jsTeamsList"></div>
      <div class="divider"></div>
      <div class="lbl">تعديل النقاط</div>
      <div id="jsScoreEdit"></div>
    </div>
    <div id="js1" style="display:none;">
      <div class="pts-tags" id="jsPtsTags"></div>
      <div class="row" style="margin-top:10px;">
        <input type="number" id="jsPtsInp" placeholder="فئة جديدة" min="10" step="50" style="max-width:160px;">
        <button class="btn btn-ghost btn-sm" onclick="jsAddPts()" style="padding:10px 14px;">اضافة</button>
      </div>
    </div>
    <div id="js2" style="display:none;">
      <div class="lbl">اسم المسابقة</div>
      <input type="text" id="jsTitle" style="margin-bottom:10px;">
      <div class="lbl">اسم المجموعة</div>
      <input type="text" id="jsGroup">
    </div>
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="saveJudgeSettings()">حفظ</button>
      <button class="btn btn-ghost" onclick="closeModal('judgeSettingsModal')">إغلاق</button>
    </div>
  </div>
</div>

<!-- AI Modal -->
<div class="modal-bg" id="aiModal">
  <div class="modal-box" style="max-width:540px;">
    <div class="modal-title">✦ توليد أسئلة بالذكاء الاصطناعي</div>
    <div class="lbl">مزود AI</div>
    <select id="aiProvider" style="margin-bottom:10px;">
      <option value="gemini">Gemini (Google) — مجاني</option>
      <option value="openai">OpenAI (ChatGPT)</option>
    </select>
    <div class="lbl">API Key <span style="font-size:.75rem;color:var(--muted);">(يُحفظ محلياً فقط)</span></div>
    <input type="password" id="aiKey" placeholder="الصق المفتاح هنا" style="margin-bottom:10px;" autocomplete="off">
    <div class="lbl">الموضوع</div>
    <input type="text" id="aiTopic" placeholder="مثال: تاريخ المملكة العربية السعودية" style="margin-bottom:10px;">
    <div style="display:flex;gap:9px;margin-bottom:12px;">
      <select id="aiCount"><option value="3">3 أسئلة</option><option value="5" selected>5 أسئلة</option><option value="10">10 أسئلة</option></select>
      <select id="aiLang"><option value="ar">عربي</option><option value="en">English</option></select>
    </div>
    <button class="btn btn-grad" onclick="genAI()" id="aiGenBtn" style="width:100%;margin-bottom:12px;">توليد الأسئلة</button>
    <div id="aiResults"></div>
    <div class="modal-acts">
      <button class="btn btn-ghost" onclick="closeModal('aiModal')">إغلاق</button>
    </div>
  </div>
</div>

<!-- Edit Score Modal -->
<div class="modal-bg" id="editScoreModal">
  <div class="modal-box" style="max-width:340px;">
    <div class="modal-title">تعديل نقاط: <span id="esName"></span></div>
    <input type="number" id="esScore" min="0" style="text-align:center;font-size:1.3rem;">
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="saveEditScore()">حفظ</button>
      <button class="btn btn-ghost" onclick="closeModal('editScoreModal')">إلغاء</button>
    </div>
  </div>
</div>

<!-- Resume Modal -->
<div class="modal-bg" id="resumeModal">
  <div class="modal-box" style="max-width:380px;">
    <div class="modal-title">استئناف المسابقة؟</div>
    <div id="resumeText" style="font-size:.9rem;color:var(--text2);"></div>
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="resumeComp()">استئناف</button>
      <button class="btn btn-ghost" onclick="closeModal('resumeModal')">إلغاء</button>
    </div>
  </div>
</div>

<script>
/* ═══════════════════════════════════
   STORAGE
═══════════════════════════════════ */
const S={
  get:(k)=>{try{return JSON.parse(localStorage.getItem(k));}catch{return null;}},
  set:(k,v)=>localStorage.setItem(k,JSON.stringify(v)),
  del:(k)=>localStorage.removeItem(k)
};

/* ═══════════════════════════════════
   BUILT-IN QUESTION BANK
═══════════════════════════════════ */
const BUILTIN_BANK=[
  {name:'ثقافة عامة',questions:[
    {text:'ما هي عاصمة المملكة العربية السعودية؟',answer:'الرياض',pts:100},
    {text:'كم عدد أيام الأسبوع؟',answer:'7 أيام',pts:100},
    {text:'ما هو أكبر كوكب في المجموعة الشمسية؟',answer:'المشتري',pts:200},
    {text:'من هو مؤلف رواية "ألف ليلة وليلة"؟',answer:'مجهول / تراث شعبي',pts:200},
    {text:'ما هي أطول نهر في العالم؟',answer:'نهر النيل',pts:300},
    {text:'في أي سنة تأسست المملكة العربية السعودية؟',answer:'1932م',pts:300},
    {text:'ما هو الرمز الكيميائي للذهب؟',answer:'Au',pts:400},
    {text:'كم عدد دول العالم المعترف بها دولياً تقريباً؟',answer:'195 دولة',pts:500},
  ]},
  {name:'علوم وتكنولوجيا',questions:[
    {text:'ما هي الوحدة الأساسية للمعلومات في الحاسوب؟',answer:'البت (Bit)',pts:100},
    {text:'من اخترع الهاتف؟',answer:'ألكسندر غراهام بيل',pts:200},
    {text:'ما هو الغاز الأكثر وفرة في الغلاف الجوي؟',answer:'النيتروجين (78%)',pts:200},
    {text:'ما هي سرعة الضوء تقريباً؟',answer:'300,000 كم/ثانية',pts:300},
    {text:'ما معنى اختصار HTTP؟',answer:'HyperText Transfer Protocol',pts:400},
    {text:'ما هو عدد بايتات في الكيلوبايت؟',answer:'1024 بايت',pts:400},
  ]},
  {name:'جغرافيا',questions:[
    {text:'ما هي أكبر قارة مساحةً؟',answer:'آسيا',pts:100},
    {text:'ما هو أعلى جبل في العالم؟',answer:'جبل إيفرست',pts:100},
    {text:'ما هي أصغر دولة في العالم مساحةً؟',answer:'الفاتيكان',pts:200},
    {text:'ما هي أكبر صحراء في العالم؟',answer:'الصحراء الكبرى في أفريقيا',pts:300},
    {text:'أي دولة تمتلك أكبر عدد سكان؟',answer:'الهند',pts:200},
  ]},
  {name:'تاريخ',questions:[
    {text:'متى انتهت الحرب العالمية الثانية؟',answer:'1945م',pts:100},
    {text:'من هو أول إنسان وطأت قدمه القمر؟',answer:'نيل أرمسترونغ',pts:200},
    {text:'في أي عام اكتشف كريستوفر كولومبوس أمريكا؟',answer:'1492م',pts:300},
    {text:'ما هو أقدم حضارة في التاريخ؟',answer:'الحضارة السومرية',pts:400},
    {text:'متى سقط جدار برلين؟',answer:'1989م',pts:300},
  ]},
];

/* ═══════════════════════════════════
   STATE
═══════════════════════════════════ */
let G={
  id:null,title:'',group:'',qOrder:'ordered',
  teams:[],ptsOptions:[100,200,300,400,500],
  categories:[],
  currentQ:1,selPts:100,selTeamIdx:-1,
  lastWinner:-1,lastPts:0,
  questionLog:[],
  activeQuestion:null,showQOnDisplay:false,
  timerSecs:30,timerLeft:30,timerRunning:false,
  pin:'',
};
let cardEls={},playerCardEls={},dispCardEls={};
const CARD_H=78,CARD_GAP=12;
let timerInt=null;
let pinTarget=''; // which screen after pin
let aiTargetCatId=null;
let editScoreIdx=-1;
let bankFromJudge=false;
let adminTabIdx=0;
let jsTabIdx=0;
let isAdmin=false;

/* ═══════════════════════════════════
   THEME
═══════════════════════════════════ */
let themeMode=S.get('themeMode')||'auto';
function applyTheme(){
  const dark=themeMode==='dark'||(themeMode==='auto'&&window.matchMedia('(prefers-color-scheme: dark)').matches);
  document.documentElement.setAttribute('data-theme',dark?'dark':'light');
  document.querySelectorAll('.theme-chip').forEach(c=>c.classList.toggle('active',c.dataset.mode===themeMode));
}
function setTheme(m){themeMode=m;S.set('themeMode',m);applyTheme();}
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change',applyTheme);
applyTheme();

/* ═══════════════════════════════════
   SITE NAME / ADMIN PIN
═══════════════════════════════════ */
function getSiteName(){return S.get('siteName')||'منصة المسابقات';}
function getAdminPin(){return S.get('adminPin')||'1234';}
function renderSiteName(){
  const n=getSiteName();
  document.getElementById('siteNameEl').textContent=n;
  document.title=n;
}

/* ═══════════════════════════════════
   HISTORY
═══════════════════════════════════ */
function getHistory(){return S.get('compHistory')||[];}
function saveHistory(){
  if(!G.title||!G.teams.length)return;
  let h=getHistory();
  const rec={
    id:G.id||Date.now(),title:G.title,group:G.group,qOrder:G.qOrder,
    teams:JSON.parse(JSON.stringify(G.teams)),
    ptsOptions:[...G.ptsOptions],
    categories:JSON.parse(JSON.stringify(G.categories)),
    questionLog:[...G.questionLog],
    currentQ:G.currentQ,selPts:G.selPts,
    pin:G.pin, savedAt:Date.now()
  };
  G.id=rec.id;
  const idx=h.findIndex(x=>x.id===rec.id);
  if(idx>=0)h[idx]=rec;else h.unshift(rec);
  h=h.slice(0,20);
  S.set('compHistory',h);
}
function delHistory(id){
  if(!confirm('حذف هذه المسابقة؟'))return;
  S.set('compHistory',getHistory().filter(x=>x.id!==id));
  renderHomeStats();renderAdmHist();
}

function renderHomeStats(){
  const h=getHistory();
  const totalQs=h.reduce((a,b)=>a+(b.categories?.reduce((x,c)=>x+c.questions.length,0)||0),0);
  document.getElementById('homeStats').innerHTML=`
    <div class="stat-c"><div class="stat-n">${h.length}</div><div class="stat-l">مسابقة</div></div>
    <div class="stat-c"><div class="stat-n">${h.reduce((a,b)=>a+(b.teams?.length||0),0)}</div><div class="stat-l">فريق</div></div>
    <div class="stat-c"><div class="stat-n">${h.reduce((a,b)=>a+(b.questionLog?.length||0),0)}</div><div class="stat-l">سؤال مجاب</div></div>
    <div class="stat-c"><div class="stat-n">${totalQs}</div><div class="stat-l">سؤال في البنك</div></div>`;
}

/* ═══════════════════════════════════
   HOME / PORTALS
═══════════════════════════════════ */
function goHome(){stopTimer();saveHistory();renderHomeStats();goTo('homeScreen');}

function enterJudge(){
  // judge needs pin — either start new or resume
  const h=getHistory();
  if(!G.id&&!h.length){startNew();return;}
  if(G.id){
    // already loaded
    renderJudge();goTo('judgeScreen');return;
  }
  // show resume or new options
  showJudgeEntry();
}

function showJudgeEntry(){
  const h=getHistory();
  if(!h.length){startNew();return;}
  // ask: resume last or new
  const last=h[0];
  document.getElementById('resumeText').innerHTML=`آخر مسابقة: <b>${last.title}</b> — السؤال ${last.currentQ}<br>هل تريد استئنافها أم بدء جديدة؟`;
  document.getElementById('resumeModal')._action='judge';
  openModal('resumeModal');
}

function resumeComp(){
  closeModal('resumeModal');
  const act=document.getElementById('resumeModal')._action;
  if(act==='judge'){
    // ask PIN for last comp
    const h=getHistory();
    const last=h[0];
    if(last.pin){
      pinTarget='judgeResume';
      document.getElementById('pinTitle').textContent='رمز مسابقة: '+last.title;
      document.getElementById('pinSub').textContent='أدخل الرمز السري للمسابقة';
      document.getElementById('pinInput').value='';
      document.getElementById('pinError').textContent='';
      document.getElementById('resumeModal')._lastId=last.id;
      goTo('pinScreen');
    } else {
      loadCompById(last.id);renderJudge();goTo('judgeScreen');
    }
  }
}

function loadCompById(id){
  const rec=getHistory().find(x=>x.id===id);
  if(!rec)return;
  G={...G,...rec,teams:JSON.parse(JSON.stringify(rec.teams)),categories:JSON.parse(JSON.stringify(rec.categories||[])),questionLog:[...(rec.questionLog||[])],ptsOptions:[...rec.ptsOptions],selTeamIdx:-1,lastWinner:-1,lastPts:0,timerSecs:30,timerLeft:30,timerRunning:false,activeQuestion:null,showQOnDisplay:false};
  cardEls={};playerCardEls={};dispCardEls={};
  initCategoriesIfEmpty();
}

function initCategoriesIfEmpty(){
  if(!G.categories||!G.categories.length){
    G.categories=BUILTIN_BANK.map(b=>({
      id:'builtin_'+b.name,name:b.name,
      questions:b.questions.map((q,i)=>({id:'bq_'+i+'_'+b.name,text:q.text,answer:q.answer,pts:q.pts,used:false,approved:true}))
    }));
  }
}

function enterPlayer(){
  if(!G.id&&!getHistory().length){alert('لا توجد مسابقة جارية');return;}
  if(!G.id){const h=getHistory();if(h.length)loadCompById(h[0].id);}
  renderPlayerBoard();goTo('playerScreen');
  startPlayerRefresh();
}

function enterDisplay(){
  if(!G.id&&!getHistory().length){alert('لا توجد مسابقة جارية');return;}
  if(!G.id){const h=getHistory();if(h.length)loadCompById(h[0].id);}
  renderDisplayBoard();goTo('displayScreen');
}

function enterBank(){
  bankFromJudge=false;
  renderBank(false);
  document.getElementById('bankAddCatBtn').style.display='none';
  document.getElementById('bankAIBtn').style.display='none';
  goTo('bankScreen');
}

function enterAdmin(){
  pinTarget='admin';
  document.getElementById('pinTitle').textContent='لوحة المشرف';
  document.getElementById('pinSub').textContent='أدخل رمز المشرف';
  document.getElementById('pinIcon').textContent='🛡️';
  document.getElementById('pinInput').value='';
  document.getElementById('pinError').textContent='';
  goTo('pinScreen');
}

/* ═══════════════════════════════════
   PIN SCREEN
═══════════════════════════════════ */
function onPinInput(v){}
function checkPin(){
  const v=document.getElementById('pinInput').value.trim();
  const errEl=document.getElementById('pinError');

  if(pinTarget==='admin'){
    if(v===getAdminPin()){
      isAdmin=true;
      document.getElementById('admSiteName').value=getSiteName();
      renderAdmHist();
      goTo('homeScreen');
      setTimeout(()=>openModal('adminModal'),300);
    }else{errEl.textContent='رمز خاطئ، حاول مرة أخرى';}
    return;
  }
  if(pinTarget==='judgeResume'){
    const id=document.getElementById('resumeModal')._lastId;
    const rec=getHistory().find(x=>x.id===id);
    if(rec&&rec.pin===v){loadCompById(id);renderJudge();goTo('judgeScreen');}
    else{errEl.textContent='رمز خاطئ';}
    return;
  }
  if(pinTarget==='judgeNew'){
    if(v===G.pin||!G.pin){renderJudge();goTo('judgeScreen');}
    else{errEl.textContent='رمز خاطئ';}
    return;
  }
}

/* ═══════════════════════════════════
   SETUP WIZARD
═══════════════════════════════════ */
function startNew(){
  G={id:null,title:'',group:'',qOrder:'ordered',teams:[],ptsOptions:[100,200,300,400,500],categories:[],currentQ:1,selPts:100,selTeamIdx:-1,lastWinner:-1,lastPts:0,questionLog:[],activeQuestion:null,showQOnDisplay:false,timerSecs:30,timerLeft:30,timerRunning:false,pin:''};
  cardEls={};playerCardEls={};dispCardEls={};
  renderWizard(0);
  goTo('setupScreen');
}

function renderWizard(step){
  for(let i=0;i<4;i++){
    document.getElementById('wp'+i).classList.toggle('active',i===step);
    const ws=document.getElementById('ws'+i);
    ws.classList.remove('active','done');
    if(i===step)ws.classList.add('active');
    else if(i<step)ws.classList.add('done');
  }
  if(step===1)renderSetupTeams();
  if(step===2)renderPtsTags();
}

function wizNext(s){
  if(s===0){
    const t=document.getElementById('setupTitle').value.trim();
    if(!t){alert('اكتب اسم المسابقة');return;}
    G.title=t;G.group=document.getElementById('setupGroup').value.trim();
    G.qOrder=document.querySelector('input[name=qord]:checked').value;
  }
  if(s===1&&!G.teams.length){alert('اضف فريقاً على الأقل');return;}
  renderWizard(s+1);
}
function wizPrev(s){renderWizard(s-1);}

function renderSetupTeams(){
  const el=document.getElementById('teamsList');
  if(!G.teams.length){el.innerHTML='<div class="empty">لا توجد فرق بعد</div>';return;}
  el.innerHTML=G.teams.map((t,i)=>`
    <div style="display:flex;align-items:center;justify-content:space-between;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:8px 12px;margin-bottom:6px;">
      <span style="font-weight:700;">${t.name}</span>
      <button class="btn btn-sm btn-rg" onclick="removeTeam(${i})">حذف</button>
    </div>`).join('');
}
function addTeam(){
  const inp=document.getElementById('teamInp');const n=inp.value.trim();
  if(!n)return;if(G.teams.find(t=>t.name===n)){inp.select();return;}
  G.teams.push({name:n,score:0});inp.value='';inp.focus();renderSetupTeams();
}
function removeTeam(i){G.teams.splice(i,1);renderSetupTeams();}

function renderPtsTags(){
  document.getElementById('ptsTagWrap').innerHTML=G.ptsOptions.map((p,i)=>`
    <div class="pts-tag">${p}<button onclick="removePtsTag(${i})">✕</button></div>`).join('');
}
function addPtsTag(){
  const v=parseInt(document.getElementById('ptsAddInp').value);
  if(!v||v<10)return;
  if(!G.ptsOptions.includes(v)){G.ptsOptions.push(v);G.ptsOptions.sort((a,b)=>a-b);}
  document.getElementById('ptsAddInp').value='';renderPtsTags();
}
function removePtsTag(i){if(G.ptsOptions.length<=1)return;G.ptsOptions.splice(i,1);renderPtsTags();}
function resetPts(){G.ptsOptions=[100,200,300,400,500];renderPtsTags();}

function setupDone(){
  const p1=document.getElementById('compPinInp').value;
  const p2=document.getElementById('compPinConf').value;
  if(p1&&p1!==p2){alert('الرمزان غير متطابقان');return;}
  if(p1&&(p1.length<4||p1.length>6)){alert('الرمز يجب أن يكون 4-6 أرقام');return;}
  G.pin=p1;
  initCategoriesIfEmpty();
  G.selPts=G.ptsOptions[0];
  saveHistory();
  renderJudge();
  goTo('judgeScreen');
}

/* ═══════════════════════════════════
   JUDGE SCREEN
═══════════════════════════════════ */
function renderJudge(){
  document.getElementById('judgeBrand').textContent=G.title;
  document.getElementById('qNum').textContent=G.currentQ;
  updateTimerUI();
  document.getElementById('ptsChips').innerHTML=G.ptsOptions.map(p=>`
    <div class="pts-chip ${p===G.selPts?'sel':''}" onclick="selPts(${p})">${p}</div>`).join('');
  renderTeamBtns();
  renderLog();
  updateAQBox();
  document.getElementById('undoBtn').disabled=!G.questionLog.length;
}

function selPts(p){G.selPts=p;document.querySelectorAll('.pts-chip').forEach(c=>c.classList.toggle('sel',parseInt(c.textContent)===p));renderTeamBtns();}
function selectTeam(i){G.selTeamIdx=G.selTeamIdx===i?-1:i;renderTeamBtns();}

function renderTeamBtns(){
  document.getElementById('teamBtns').innerHTML=G.teams.map((t,i)=>`
    <div class="team-row ${i===G.selTeamIdx?'winner':''}" onclick="selectTeam(${i})">
      <div class="tr-name">${t.name}</div>
      <div class="tr-score">${t.score.toLocaleString()}</div>
      <div class="award-badge">فائز +${G.selPts}</div>
    </div>`).join('');
}

function updateAQBox(){
  const q=G.activeQuestion;
  document.getElementById('aqText').textContent=q?q.text:'اختر سؤالاً من البنك أو تجاوز';
  const a=document.getElementById('aqAns');
  a.textContent=q?.answer?'الإجابة: '+q.answer:'';a.classList.remove('show');
  document.getElementById('aqPts').textContent=q?q.pts+' نقطة':'';
  document.getElementById('sendQBtn').textContent=G.showQOnDisplay?'إخفاء من الشاشة':'إرسال للشاشة';
}
function toggleAns(){document.getElementById('aqAns').classList.toggle('show');}

function pickQ(){
  const pool=[];
  G.categories.forEach(cat=>cat.questions.forEach((q,qi)=>{
    if(!q.used&&q.approved!==false)pool.push({catId:cat.id,qIdx:qi,...q});
  }));
  if(!pool.length){alert('لا توجد أسئلة غير مستخدمة');return;}
  const q=G.qOrder==='random'?pool[Math.floor(Math.random()*pool.length)]:pool[0];
  G.activeQuestion={...q};
  updateAQBox();pushState();
}

function toggleSendQ(){
  G.showQOnDisplay=!G.showQOnDisplay;
  document.getElementById('sendQBtn').textContent=G.showQOnDisplay?'إخفاء من الشاشة':'إرسال للشاشة';
  pushState();
}

function confirmAndNext(){
  if(G.selTeamIdx<0){alert('اختر الفريق الفائز');return;}
  stopTimer();
  const snap={teamIdx:G.selTeamIdx,pts:G.selPts,q:G.currentQ,score:G.teams[G.selTeamIdx].score,aq:G.activeQuestion?{...G.activeQuestion}:null};
  G.teams[G.selTeamIdx].score+=G.selPts;
  G.lastWinner=G.selTeamIdx;G.lastPts=G.selPts;
  G.questionLog.push({q:G.currentQ,teamName:G.teams[G.selTeamIdx].name,pts:G.selPts,_snap:snap});
  if(G.activeQuestion){
    const cat=G.categories.find(c=>c.id===G.activeQuestion.catId);
    if(cat&&cat.questions[G.activeQuestion.qIdx])cat.questions[G.activeQuestion.qIdx].used=true;
    G.activeQuestion=null;G.showQOnDisplay=false;
  }
  saveHistory();pushState();
  document.getElementById('flash').classList.add('on');setTimeout(()=>document.getElementById('flash').classList.remove('on'),400);
  spawnConfetti();
  renderLive();goTo('liveScreen');
}

function undoLast(){
  if(!G.questionLog.length)return;
  const last=G.questionLog.pop();const s=last._snap;
  G.teams[s.teamIdx].score=s.score;
  G.currentQ=s.q;G.selTeamIdx=-1;G.lastWinner=-1;G.lastPts=0;
  if(s.aq){const cat=G.categories.find(c=>c.id===s.aq.catId);if(cat&&cat.questions[s.aq.qIdx])cat.questions[s.aq.qIdx].used=false;}
  cardEls={};saveHistory();renderJudge();
}

function renderLog(){
  const el=document.getElementById('histLog');
  if(!G.questionLog.length){el.innerHTML='<div class="empty">لا يوجد سجل</div>';return;}
  el.innerHTML=[...G.questionLog].reverse().map(r=>`
    <div class="log-item">
      <span class="log-q">س${r.q}</span>
      <span class="log-w">${r.teamName}</span>
      <span class="log-p">+${r.pts}</span>
    </div>`).join('');
}

/* ═══════════════════════════════════
   TIMER
═══════════════════════════════════ */
function fmt(s){return String(Math.floor(s/60)).padStart(2,'0')+':'+String(s%60).padStart(2,'0');}
function updateTimerUI(){
  const el=document.getElementById('timerDisp');if(!el)return;
  el.textContent=fmt(G.timerLeft);
  el.classList.toggle('urgent',G.timerLeft<=5&&G.timerLeft>0);
  // update player / display
  const pd=document.getElementById('playerTimer');if(pd)pd.textContent=fmt(G.timerLeft),pd.classList.toggle('urgent',G.timerLeft<=5&&G.timerLeft>0);
  const dd=document.getElementById('dispTimer');if(dd)dd.textContent=fmt(G.timerLeft),dd.classList.toggle('urgent',G.timerLeft<=5&&G.timerLeft>0);
}
function setTimer(s){stopTimer();G.timerSecs=s;G.timerLeft=s;updateTimerUI();}
function toggleTimer(){G.timerRunning?stopTimer():startTimerRun();}
function startTimerRun(){
  if(G.timerLeft<=0)G.timerLeft=G.timerSecs;
  G.timerRunning=true;
  document.getElementById('tPlayBtn').textContent='⏸';
  document.getElementById('tPlayBtn').classList.add('on');
  timerInt=setInterval(()=>{G.timerLeft--;updateTimerUI();if(G.timerLeft<=0)stopTimer();},1000);
}
function stopTimer(){
  clearInterval(timerInt);timerInt=null;G.timerRunning=false;
  const b=document.getElementById('tPlayBtn');if(b){b.textContent='▶';b.classList.remove('on');}
}
function resetTimer(){stopTimer();G.timerLeft=G.timerSecs;updateTimerUI();}

/* ═══════════════════════════════════
   PUSH STATE (sync player/display)
═══════════════════════════════════ */
function pushState(){
  renderPlayerBoard();
  renderDisplayBoard();
}

/* ═══════════════════════════════════
   PLAYER BOARD
═══════════════════════════════════ */
let playerRefInt=null;
function startPlayerRefresh(){clearInterval(playerRefInt);playerRefInt=setInterval(()=>{updateTimerUI();},1000);}

function renderPlayerBoard(){
  if(!document.getElementById('playerScreen').classList.contains('active'))return;
  document.getElementById('playerBrand').textContent=G.title;
  document.getElementById('playerCompName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('playerQ').textContent=G.currentQ;
  document.getElementById('playerMeta').textContent=G.group||'';

  const qBox=document.getElementById('playerQBox');
  if(G.showQOnDisplay&&G.activeQuestion){
    qBox.classList.add('show');
    document.getElementById('playerQText').textContent=G.activeQuestion.text;
  }else{qBox.classList.remove('show');}

  renderRankings('playerRankings',playerCardEls,'player');
}

/* ═══════════════════════════════════
   DISPLAY BOARD
═══════════════════════════════════ */
function renderDisplayBoard(){
  if(!document.getElementById('displayScreen').classList.contains('active'))return;
  document.getElementById('dispCompName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('dispQ').textContent=G.currentQ;

  const qb=document.getElementById('dispQBox');
  if(G.showQOnDisplay&&G.activeQuestion){
    qb.classList.add('show');
    document.getElementById('dispQText').textContent=G.activeQuestion.text;
  }else{qb.classList.remove('show');}

  renderRankings('dispRankings',dispCardEls,'display');
}

/* ═══════════════════════════════════
   LIVE BOARD (after scoring)
═══════════════════════════════════ */
function renderLive(){
  document.getElementById('liveName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('liveQ').textContent=G.currentQ;
  document.getElementById('liveFooter').innerHTML=`
    <button class="btn btn-grad" onclick="goNextFromLive()">السؤال التالي</button>
    <button class="btn btn-ghost" onclick="showFinale()">إنهاء المسابقة</button>
    <button class="btn btn-ghost" onclick="goHome()">الرئيسية</button>`;
  renderRankings('liveRankings',cardEls,'live');
}

function goNextFromLive(){
  G.currentQ++;G.selTeamIdx=-1;G.lastWinner=-1;G.lastPts=0;
  G.timerLeft=G.timerSecs;G.activeQuestion=null;G.showQOnDisplay=false;
  renderJudge();goTo('judgeScreen');
}

/* ═══════════════════════════════════
   GENERIC RANKINGS RENDERER (FLIP)
═══════════════════════════════════ */
function renderRankings(wrapId,cels,mode){
  const wrap=document.getElementById(wrapId);if(!wrap)return;
  const sorted=[...G.teams].map((t,i)=>({...t,origIdx:i})).sort((a,b)=>b.score-a.score);
  const maxScore=Math.max(...sorted.map(t=>t.score),1);
  wrap.style.height=(sorted.length*(CARD_H+CARD_GAP)-CARD_GAP)+'px';

  const isFirst=Object.keys(cels).length!==G.teams.length;
  if(isFirst){
    wrap.innerHTML='';
    // clear cels
    Object.keys(cels).forEach(k=>delete cels[k]);
    sorted.forEach((t,rank)=>{
      const el=buildCard(t,rank,maxScore);
      el.style.top=(rank*(CARD_H+CARD_GAP))+'px';
      wrap.appendChild(el);cels[t.origIdx]=el;
    });return;
  }
  const prevTops={};
  sorted.forEach(t=>{const el=cels[t.origIdx];if(el)prevTops[t.origIdx]=parseInt(el.style.top)||0;});
  sorted.forEach((t,rank)=>{const el=cels[t.origIdx];if(el)updateCard(el,t,rank,maxScore);});
  sorted.forEach(t=>{const el=cels[t.origIdx];if(!el)return;el.style.transition='none';el.style.top=(prevTops[t.origIdx]??0)+'px';});
  requestAnimationFrame(()=>requestAnimationFrame(()=>{
    sorted.forEach((t,rank)=>{
      const el=cels[t.origIdx];if(!el)return;
      el.style.transition='top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s';
      el.style.top=(rank*(CARD_H+CARD_GAP))+'px';
    });
  }));
  if(G.lastWinner>=0&&cels[G.lastWinner]){
    const el=cels[G.lastWinner];
    el.querySelector('.float-pts')?.remove();
    const fp=document.createElement('div');fp.className='float-pts';fp.textContent='+'+G.lastPts;
    el.appendChild(fp);setTimeout(()=>fp.remove(),1300);
  }
}

function buildCard(t,rank,maxScore){
  const el=document.createElement('div');
  el.style.transition='top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s';
  updateCard(el,t,rank,maxScore);return el;
}
function updateCard(el,t,rank,maxScore){
  const rc=rank===0?'rank-1':rank===1?'rank-2':rank===2?'rank-3':'rank-other';
  el.className='rank-card '+rc+(t.origIdx===G.lastWinner?' just-scored':'');
  const pct=(t.score/maxScore*100).toFixed(1);
  el.innerHTML=`<div class="rank-medal">${rank+1}</div><div class="rank-name">${t.name}</div><div class="rank-score">${t.score.toLocaleString()}</div><div class="score-bar-track"><div class="score-bar-fill" style="width:${pct}%"></div></div>`;
}

/* ═══════════════════════════════════
   FINALE
═══════════════════════════════════ */
function showFinale(){
  const sorted=[...G.teams].sort((a,b)=>b.score-a.score);
  document.getElementById('finaleWinner').textContent=sorted[0]?.name||'—';
  const p3=sorted.slice(0,3);
  const ord=[1,0,2];
  document.getElementById('finalePodium').innerHTML=ord.map(i=>{
    if(!p3[i])return'';
    const cls=['p2','p1','p3'][i];const m=['🥈','🥇','🥉'][i];
    return `<div class="podium-item ${cls}"><div class="podium-bar">${m}</div><div class="podium-name">${p3[i].name}</div><div class="podium-score">${p3[i].score.toLocaleString()}</div></div>`;
  }).join('');
  saveHistory();spawnConfetti();goTo('finaleScreen');
}
function toggleSummary(){
  const el=document.getElementById('summarySection');
  el.style.display=el.style.display==='none'?'block':'none';
  document.getElementById('summaryTable').innerHTML=`
    <tr>${['المرتبة','الفريق','النقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>
    ${[...G.teams].sort((a,b)=>b.score-a.score).map((t,i)=>`<tr><td>${i+1}</td><td>${t.name}</td><td>${t.score.toLocaleString()}</td></tr>`).join('')}
    <tr><th colspan="3" style="padding-top:12px;">سجل الأسئلة</th></tr>
    <tr>${['سؤال','الفائز','نقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>
    ${G.questionLog.map(r=>`<tr><td>س${r.q}</td><td>${r.teamName}</td><td>+${r.pts}</td></tr>`).join('')}`;
}

/* ═══════════════════════════════════
   QUESTION BANK
═══════════════════════════════════ */
function renderBank(judgeMode){
  document.getElementById('bankAddCatBtn').style.display=judgeMode?'flex':'none';
  document.getElementById('bankAIBtn').style.display=judgeMode?'flex':'none';

  // pending section (judge only)
  const pending=[];
  G.categories.forEach(cat=>cat.questions.forEach((q,qi)=>{if(q.approved===false)pending.push({catId:cat.id,qi,q});}));
  const ps=document.getElementById('bankPendingSection');
  if(judgeMode&&pending.length){
    ps.style.display='block';
    document.getElementById('pendingCount').textContent=pending.length;
    document.getElementById('pendingList').innerHTML=pending.map(({catId,qi,q})=>`
      <div class="q-item q-pending">
        <div class="q-item-txt">
          <div class="q-text">${q.text}</div>
          ${q.answer?`<div class="q-answer">الإجابة: ${q.answer}</div>`:''}
          <div class="q-pts-badge">${q.pts} نقطة</div>
        </div>
        <div style="display:flex;flex-direction:column;gap:5px;">
          <button class="btn btn-sm btn-green" onclick="approveQ('${catId}',${qi})">موافقة ✓</button>
          <button class="btn btn-sm btn-rg" onclick="rejectQ('${catId}',${qi})">رفض</button>
        </div>
      </div>`).join('');
  }else{ps.style.display='none';}

  const el=document.getElementById('bankCats');
  if(!G.categories.length){el.innerHTML='<div class="empty">لا توجد تصنيفات</div>';return;}
  el.innerHTML=G.categories.map(cat=>{
    const approved=cat.questions.filter(q=>q.approved!==false);
    return `<div class="cat-box" id="cat-${cat.id}">
      <div class="cat-header" onclick="toggleCat('${cat.id}')">
        <div class="cat-title">${cat.name}</div>
        <div class="cat-meta">${approved.length} سؤال · ${cat.questions.filter(q=>q.used).length} مستخدم</div>
        ${judgeMode?`<div style="display:flex;gap:5px;">
          <button class="btn btn-sm" style="background:rgba(79,70,229,.1);color:var(--a1);border:none;padding:4px 10px;" onclick="event.stopPropagation();openAIModal('${cat.id}')">✦ AI</button>
          <button class="btn btn-sm btn-rg" onclick="event.stopPropagation();deleteCat('${cat.id}')">حذف</button>
        </div>`:''}
        <div class="cat-arrow">›</div>
      </div>
      <div class="cat-body">
        ${approved.map((q,qi)=>`
          <div class="q-item ${q.used?'q-used':''}">
            <div class="q-item-txt">
              <div class="q-text">${q.text}</div>
              ${q.answer&&judgeMode?`<div class="q-answer">الإجابة: ${q.answer}</div>`:''}
              <div class="q-pts-badge">${q.pts} نقطة</div>
            </div>
            ${judgeMode?`<div style="display:flex;gap:4px;">
              <button class="btn btn-sm btn-ghost" onclick="editQ('${cat.id}',${qi})">✎</button>
              <button class="btn btn-sm btn-rg" onclick="delQ('${cat.id}',${qi})">✕</button>
            </div>`:''}
          </div>`).join('')}
        ${judgeMode?`<div class="cat-add-row">
          <input type="text" placeholder="نص السؤال" id="qt-${cat.id}">
          <input type="text" placeholder="الإجابة" id="qa-${cat.id}" style="max-width:150px;">
          <select id="qp-${cat.id}" style="width:auto;flex:none;">${G.ptsOptions.map(p=>`<option value="${p}">${p}</option>`).join('')}</select>
          <button class="btn btn-a1 btn-sm" onclick="addQ('${cat.id}')">اضافة</button>
        </div>`:`<div class="cat-add-row">
          <input type="text" placeholder="اقتراح سؤال" id="sqt-${cat.id}">
          <input type="text" placeholder="الإجابة" id="sqa-${cat.id}" style="max-width:140px;">
          <select id="sqp-${cat.id}" style="width:auto;flex:none;">${G.ptsOptions.map(p=>`<option value="${p}">${p}</option>`).join('')}</select>
          <button class="btn btn-ghost btn-sm" onclick="suggestQ('${cat.id}')" style="padding:8px 12px;">اقتراح ←</button>
        </div>`}
      </div>
    </div>`;
  }).join('');
  G.categories.forEach(c=>document.getElementById('cat-'+c.id)?.classList.add('open'));
}

function toggleCat(id){document.getElementById('cat-'+id)?.classList.toggle('open');}

function addCategory(){
  const n=prompt('اسم التصنيف:');if(!n?.trim())return;
  G.categories.push({id:'cat_'+Date.now(),name:n.trim(),questions:[]});
  renderBank(true);saveHistory();
}
function deleteCat(id){
  if(!confirm('حذف التصنيف وكل أسئلته؟'))return;
  G.categories=G.categories.filter(c=>c.id!==id);
  renderBank(true);saveHistory();
}
function addQ(catId){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const t=document.getElementById('qt-'+catId)?.value.trim();if(!t)return;
  const a=document.getElementById('qa-'+catId)?.value.trim();
  const p=parseInt(document.getElementById('qp-'+catId)?.value)||G.ptsOptions[0];
  cat.questions.push({id:'q_'+Date.now(),text:t,answer:a,pts:p,used:false,approved:true});
  document.getElementById('qt-'+catId).value='';
  document.getElementById('qa-'+catId).value='';
  renderBank(true);saveHistory();
}
function suggestQ(catId){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const t=document.getElementById('sqt-'+catId)?.value.trim();if(!t)return;
  const a=document.getElementById('sqa-'+catId)?.value.trim();
  const p=parseInt(document.getElementById('sqp-'+catId)?.value)||G.ptsOptions[0];
  cat.questions.push({id:'q_'+Date.now(),text:t,answer:a,pts:p,used:false,approved:false});
  document.getElementById('sqt-'+catId).value='';
  document.getElementById('sqa-'+catId).value='';
  alert('تم إرسال اقتراحك للمحكم للمراجعة ✓');
  renderBank(false);saveHistory();
}
function approveQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);
  const approved=cat.questions.filter(q=>q.approved!==false);
  cat.questions[qi+(cat.questions.length-approved.length)].approved=true;
  // re-find by position in all questions
  const pending=cat.questions.filter(q=>q.approved===false);
  if(pending[qi])pending[qi].approved=true;
  else{// find first pending
    const first=cat.questions.find(q=>q.approved===false);if(first)first.approved=true;}
  renderBank(true);saveHistory();
}
function rejectQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);
  const pending=cat.questions.filter(q=>q.approved===false);
  if(pending[qi]){const idx=cat.questions.indexOf(pending[qi]);cat.questions.splice(idx,1);}
  renderBank(true);saveHistory();
}
function delQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);
  const approved=cat.questions.filter(q=>q.approved!==false);
  const real=cat.questions.indexOf(approved[qi]);
  if(real>=0)cat.questions.splice(real,1);
  renderBank(true);saveHistory();
}
function editQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);
  const approved=cat.questions.filter(q=>q.approved!==false);
  const q=approved[qi];if(!q)return;
  const nt=prompt('نص السؤال:',q.text);if(nt===null)return;
  const na=prompt('الإجابة:',q.answer||'');
  const np=parseInt(prompt('النقاط:',q.pts));
  q.text=nt||q.text;q.answer=na;if(!isNaN(np))q.pts=np;
  renderBank(true);saveHistory();
}

function returnFromBank(){
  saveHistory();
  if(bankFromJudge){renderJudge();goTo('judgeScreen');}
  else{goHome();}
}

/* ═══════════════════════════════════
   AI QUESTIONS
═══════════════════════════════════ */
function openAIModal(catId){
  aiTargetCatId=catId;
  const cat=catId?G.categories.find(c=>c.id===catId):null;
  document.getElementById('aiTopic').value=cat?cat.name:'';
  document.getElementById('aiResults').innerHTML='';
  const savedKey=S.get('aiKey_'+document.getElementById('aiProvider').value)||'';
  document.getElementById('aiKey').value=savedKey;
  openModal('aiModal');
}

async function genAI(){
  const topic=document.getElementById('aiTopic').value.trim();
  if(!topic){alert('اكتب موضوعاً');return;}
  const count=document.getElementById('aiCount').value;
  const lang=document.getElementById('aiLang').value;
  const provider=document.getElementById('aiProvider').value;
  const key=document.getElementById('aiKey').value.trim();
  if(!key){alert('أدخل API Key');return;}
  S.set('aiKey_'+provider,key);
  const btn=document.getElementById('aiGenBtn');
  btn.textContent='جاري التوليد...';btn.disabled=true;
  document.getElementById('aiResults').innerHTML='<div class="empty">جاري التوليد...</div>';

  const sysPrompt=lang==='ar'
    ?`أنت مساعد لإنشاء أسئلة مسابقات. أنشئ ${count} أسئلة عن "${topic}" باللغة العربية. أجب بـ JSON فقط (مصفوفة): [{"text":"...","answer":"...","pts":100}]. تنوع النقاط بين: ${G.ptsOptions.join('، ')}`
    :`Create ${count} quiz questions about "${topic}". Reply ONLY with JSON array: [{"text":"...","answer":"...","pts":100}]. Vary points among: ${G.ptsOptions.join(', ')}`;

  try{
    let questions;
    if(provider==='openai'){
      const res=await fetch('https://api.openai.com/v1/chat/completions',{
        method:'POST',
        headers:{'Content-Type':'application/json','Authorization':'Bearer '+key},
        body:JSON.stringify({model:'gpt-4o-mini',messages:[{role:'user',content:sysPrompt}],temperature:.7})
      });
      const d=await res.json();
      if(!res.ok)throw new Error(d.error?.message||'OpenAI error');
      questions=JSON.parse(d.choices[0].message.content.replace(/```json|```/g,'').trim());
    }else{
      // Gemini
      const res=await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${key}`,{
        method:'POST',
        headers:{'Content-Type':'application/json'},
        body:JSON.stringify({contents:[{parts:[{text:sysPrompt}]}]})
      });
      const d=await res.json();
      if(!res.ok)throw new Error(d.error?.message||'Gemini error');
      const raw=d.candidates[0].content.parts[0].text;
      questions=JSON.parse(raw.replace(/```json|```/g,'').trim());
    }
    if(!Array.isArray(questions))throw new Error();
    document.getElementById('aiResults').innerHTML=`
      <div class="ai-panel">
        <div class="ai-panel-title">✦ الأسئلة المقترحة</div>
        ${questions.map((q,i)=>`
          <div class="ai-q-chip">
            <div style="flex:1;"><div class="ai-q-text">${q.text}</div>${q.answer?`<div class="ai-q-ans">الإجابة: ${q.answer}</div>`:''}</div>
            <button class="btn btn-green btn-sm" onclick="addAIQ(${i})">+ اضافة</button>
          </div>`).join('')}
        <button class="btn btn-a1 btn-sm" onclick="addAllAIQ()" style="width:100%;margin-top:6px;">إضافة الكل</button>
      </div>`;
    document.getElementById('aiResults')._qs=questions;
  }catch(e){
    document.getElementById('aiResults').innerHTML=`<div class="empty" style="color:var(--red);">فشل التوليد: ${e.message||'تحقق من API Key والاتصال'}</div>`;
  }
  btn.textContent='توليد الأسئلة';btn.disabled=false;
}

function addAIQ(i){
  const qs=document.getElementById('aiResults')._qs;if(!qs)return;
  const q=qs[i];
  // if no target cat, add to first
  const cat=aiTargetCatId?G.categories.find(c=>c.id===aiTargetCatId):G.categories[0];
  if(!cat){alert('أنشئ تصنيفاً أولاً');return;}
  const pts=G.ptsOptions.includes(q.pts)?q.pts:G.ptsOptions[0];
  cat.questions.push({id:'ai_'+Date.now()+'_'+i,text:q.text,answer:q.answer||'',pts,used:false,approved:true});
  renderBank(bankFromJudge);saveHistory();
}
function addAllAIQ(){
  const qs=document.getElementById('aiResults')._qs;if(!qs)return;
  qs.forEach((_,i)=>addAIQ(i));
}

/* ═══════════════════════════════════
   JUDGE SETTINGS
═══════════════════════════════════ */
function openJudgeSettings(){
  jsTabIdx=0;jsTab(0);
  document.getElementById('jsTitle').value=G.title;
  document.getElementById('jsGroup').value=G.group;
  renderJSTeams();renderJSPts();
  openModal('judgeSettingsModal');
}
function jsTab(t){
  jsTabIdx=t;
  [0,1,2].forEach(i=>{document.getElementById('js'+i).style.display=i===t?'block':'none';});
  document.querySelectorAll('#judgeSettingsModal .tab-btn').forEach((b,i)=>b.classList.toggle('active',i===t));
}
function renderJSTeams(){
  document.getElementById('jsTeamsList').innerHTML=G.teams.map((t,i)=>`
    <div style="display:flex;align-items:center;gap:8px;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:8px 12px;margin-bottom:6px;">
      <span style="flex:1;font-weight:700;">${t.name}</span>
      <span style="color:var(--gold);font-weight:900;font-size:.95rem;">${t.score}</span>
      <button class="btn btn-sm btn-ghost" onclick="openEditScore(${i})">تعديل النقاط</button>
      <button class="btn btn-sm btn-rg" onclick="jsDelTeam(${i})">حذف</button>
    </div>`).join('');
}
function jsAddTeam(){
  const inp=document.getElementById('jsTeamInp');const n=inp.value.trim();
  if(!n)return;G.teams.push({name:n,score:0});inp.value='';
  cardEls={};playerCardEls={};dispCardEls={};renderJSTeams();
}
function jsDelTeam(i){G.teams.splice(i,1);cardEls={};playerCardEls={};dispCardEls={};renderJSTeams();}
function openEditScore(i){
  editScoreIdx=i;
  document.getElementById('esName').textContent=G.teams[i].name;
  document.getElementById('esScore').value=G.teams[i].score;
  openModal('editScoreModal');
}
function saveEditScore(){
  const v=parseInt(document.getElementById('esScore').value);
  if(!isNaN(v)&&v>=0){G.teams[editScoreIdx].score=v;cardEls={};playerCardEls={};dispCardEls={};}
  closeModal('editScoreModal');renderJSTeams();
}
function renderJSPts(){
  document.getElementById('jsPtsTags').innerHTML=G.ptsOptions.map((p,i)=>`
    <div class="pts-tag">${p}<button onclick="jsRemovePts(${i})">✕</button></div>`).join('');
}
function jsAddPts(){
  const v=parseInt(document.getElementById('jsPtsInp').value);
  if(!v||v<10)return;
  if(!G.ptsOptions.includes(v)){G.ptsOptions.push(v);G.ptsOptions.sort((a,b)=>a-b);}
  document.getElementById('jsPtsInp').value='';renderJSPts();
}
function jsRemovePts(i){if(G.ptsOptions.length<=1)return;G.ptsOptions.splice(i,1);renderJSPts();}
function saveJudgeSettings(){
  const t=document.getElementById('jsTitle').value.trim();if(t)G.title=t;
  G.group=document.getElementById('jsGroup').value.trim();
  saveHistory();closeModal('judgeSettingsModal');renderJudge();
}

/* ═══════════════════════════════════
   ADMIN
═══════════════════════════════════ */
function adminTab(t){
  adminTabIdx=t;
  [0,1,2].forEach(i=>{document.getElementById('adm'+i).style.display=i===t?'block':'none';});
  document.querySelectorAll('#adminModal .tab-btn').forEach((b,i)=>b.classList.toggle('active',i===t));
  if(t===1)renderAdmHist();
}
function renderAdmHist(){
  const h=getHistory();
  document.getElementById('admHistList').innerHTML=h.length
    ?h.map(r=>`<div style="display:flex;align-items:center;gap:10px;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:9px 12px;margin-bottom:7px;">
      <div style="flex:1;"><div style="font-weight:700;font-size:.9rem;">${r.title}</div><div style="font-size:.74rem;color:var(--muted);">السؤال ${r.currentQ} · ${r.teams?.length} فرق · ${new Date(r.savedAt).toLocaleDateString('ar-SA')}</div></div>
      <button class="btn btn-sm btn-rg" onclick="delHistory(${r.id})">حذف</button>
    </div>`).join('')
    :'<div class="empty">لا توجد مسابقات</div>';
}
function saveAdmin(){
  const name=document.getElementById('admSiteName').value.trim();
  if(name){S.set('siteName',name);renderSiteName();}
  const newPin=document.getElementById('admNewPin').value.trim()||document.getElementById('admPinChange').value.trim();
  if(newPin&&newPin.length>=4&&newPin.length<=6){S.set('adminPin',newPin);alert('تم تغيير رمز المشرف ✓');}
  closeModal('adminModal');
}

/* ═══════════════════════════════════
   NAVIGATION / MODAL
═══════════════════════════════════ */
function goTo(id){
  const f=document.getElementById('pageFade');f.classList.add('show');
  setTimeout(()=>{document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));document.getElementById(id).classList.add('active');f.classList.remove('show');},220);
}
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}

/* ═══════════════════════════════════
   CONFETTI
═══════════════════════════════════ */
function spawnConfetti(){
  const colors=['#4f46e5','#7c3aed','#06b6d4','#10b981','#f97316','#d97706','#ec4899'];
  const c=document.getElementById('particles');
  for(let i=0;i<50;i++){
    const p=document.createElement('div');p.className='prt';
    const sz=5+Math.random()*9;
    p.style.cssText=`left:${Math.random()*100}vw;top:-12px;width:${sz}px;height:${sz}px;background:${colors[~~(Math.random()*colors.length)]};animation-duration:${.9+Math.random()*1.5}s;animation-delay:${Math.random()*.5}s;`;
    c.appendChild(p);setTimeout(()=>p.remove(),3200);
  }
}

/* ═══════════════════════════════════
   INIT
═══════════════════════════════════ */
renderSiteName();renderHomeStats();
</script>
</body>
</html>
