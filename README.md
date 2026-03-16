<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>منصة المسابقات</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&family=Tajawal:wght@400;700;900&display=swap" rel="stylesheet">
<style>
/* ══════════════════════════════════════════
   DESIGN TOKENS
══════════════════════════════════════════ */
:root {
  --bg:      #f0f2f8;
  --s1:      #ffffff;
  --s2:      #f4f5fb;
  --s3:      #eceef6;
  --a1:      #4f46e5;
  --a2:      #7c3aed;
  --a3:      #06b6d4;
  --green:   #10b981;
  --orange:  #f97316;
  --red:     #ef4444;
  --gold:    #d97706;
  --text:    #1a1a2e;
  --text2:   #3d3d5c;
  --muted:   #8888aa;
  --border:  rgba(79,70,229,0.13);
  --sh:      0 2px 14px rgba(79,70,229,0.08);
  --sh2:     0 6px 32px rgba(79,70,229,0.14);
}
[data-theme=dark]{
  --bg:#0d0d14; --s1:#17172a; --s2:#1e1e32; --s3:#26263e;
  --border:rgba(99,102,241,0.16); --text:#eef0ff; --text2:#b0b0d0; --muted:#6060a0;
  --sh:0 2px 14px rgba(0,0,0,0.4); --sh2:0 6px 32px rgba(0,0,0,0.5);
}
*{margin:0;padding:0;box-sizing:border-box;}
html,body{width:100%;min-height:100vh;}
body{font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);transition:background .3s,color .3s;}

/* ══════════════════════════════════════════
   LAYOUT
══════════════════════════════════════════ */
.screen{display:none;width:100%;min-height:100vh;}
.screen.active{display:flex;flex-direction:column;}

.page-fade{position:fixed;inset:0;background:var(--bg);z-index:9999;opacity:0;pointer-events:none;transition:opacity .22s;}
.page-fade.show{opacity:1;pointer-events:all;}

/* ══════════════════════════════════════════
   COMPONENTS
══════════════════════════════════════════ */
.card{background:var(--s1);border:1px solid var(--border);border-radius:16px;padding:20px;margin-bottom:14px;box-shadow:var(--sh);}
.lbl{font-size:.74rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1.2px;margin-bottom:8px;}
input[type=text],input[type=number],textarea,select{
  width:100%;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;
  padding:10px 14px;color:var(--text);font-family:'Cairo',sans-serif;font-size:.93rem;transition:border-color .2s,box-shadow .2s;
}
textarea{resize:vertical;min-height:80px;}
select{cursor:pointer;}
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
.row{display:flex;gap:9px;}
.row input{flex:1;}
.empty{color:var(--muted);font-size:.86rem;text-align:center;padding:20px 0;}
.divider{border:none;border-top:1px solid var(--border);margin:16px 0;}
.badge{display:inline-flex;align-items:center;padding:3px 10px;border-radius:999px;font-size:.75rem;font-weight:700;}
.badge-a1{background:rgba(79,70,229,.12);color:var(--a1);}
.badge-green{background:rgba(16,185,129,.12);color:var(--green);}
.badge-orange{background:rgba(249,115,22,.12);color:var(--orange);}

/* TOP NAV */
.top-nav{display:flex;align-items:center;justify-content:space-between;padding:13px 24px;background:var(--s1);border-bottom:1px solid var(--border);box-shadow:0 1px 8px rgba(79,70,229,.06);flex-wrap:wrap;gap:10px;position:sticky;top:0;z-index:100;}
.nav-brand{font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.nav-acts{display:flex;gap:7px;align-items:center;}
.icon-btn{width:34px;height:34px;border:1.5px solid var(--border);border-radius:9px;background:var(--s2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:.95rem;transition:all .15s;color:var(--text2);}
.icon-btn:hover{border-color:var(--a1);color:var(--a1);}
.pill{background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:4px 14px;font-size:.82rem;font-weight:700;color:var(--a1);}

/* MODAL */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.4);backdrop-filter:blur(5px);z-index:5000;display:none;align-items:center;justify-content:center;padding:20px;}
.modal-bg.open{display:flex;}
.modal-box{background:var(--s1);border:1px solid var(--border);border-radius:20px;padding:24px;width:100%;max-width:480px;box-shadow:var(--sh2);}
.modal-title{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:900;margin-bottom:14px;}
.modal-acts{display:flex;gap:8px;margin-top:16px;justify-content:flex-end;}

/* TABS */
.tab-bar{display:flex;gap:0;background:var(--s2);border-radius:12px;padding:4px;margin-bottom:18px;}
.tab-btn{flex:1;padding:8px 12px;border:none;border-radius:9px;font-family:'Cairo',sans-serif;font-size:.85rem;font-weight:700;cursor:pointer;background:transparent;color:var(--muted);transition:all .15s;}
.tab-btn.active{background:var(--s1);color:var(--a1);box-shadow:var(--sh);}

/* ══════════════════════════════════════════
   HOME
══════════════════════════════════════════ */
#homeScreen{
  align-items:center;padding:0 0 48px;
  background:var(--bg);
}
.home-hero{
  width:100%;padding:60px 20px 40px;text-align:center;
  background:linear-gradient(160deg,rgba(79,70,229,.08) 0%,rgba(124,58,237,.05) 50%,transparent 100%);
  border-bottom:1px solid var(--border);
  margin-bottom:32px;
}
.site-name-display{
  font-family:'Tajawal',sans-serif;font-size:3rem;font-weight:900;
  background:linear-gradient(135deg,var(--a1) 20%,var(--a2));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
  margin-bottom:8px;line-height:1.1;
}
.home-sub{color:var(--muted);font-size:.95rem;margin-bottom:28px;}
.home-ctas{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;}
.home-ctas .btn{padding:13px 28px;font-size:1rem;}

.home-body{width:100%;max-width:680px;padding:0 20px;}

/* stats bar */
.stats-bar{display:flex;gap:10px;margin-bottom:24px;flex-wrap:wrap;}
.stat-card{flex:1;min-width:120px;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:14px 16px;box-shadow:var(--sh);text-align:center;}
.stat-num{font-family:'Tajawal',sans-serif;font-size:1.8rem;font-weight:900;color:var(--a1);}
.stat-lbl{font-size:.75rem;color:var(--muted);font-weight:700;margin-top:2px;}

/* history */
.hist-item{display:flex;align-items:center;gap:12px;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:13px 16px;margin-bottom:9px;cursor:pointer;transition:all .18s;box-shadow:var(--sh);}
.hist-item:hover{border-color:var(--a1);box-shadow:var(--sh2);}
.hist-ico{width:40px;height:40px;border-radius:10px;background:linear-gradient(135deg,var(--a1),var(--a2));display:flex;align-items:center;justify-content:center;font-size:1rem;color:#fff;flex-shrink:0;}
.hist-info{flex:1;}
.hist-name{font-family:'Tajawal',sans-serif;font-size:.97rem;font-weight:700;}
.hist-meta{font-size:.75rem;color:var(--muted);margin-top:2px;}
.hist-del{opacity:0;transition:opacity .15s;}
.hist-item:hover .hist-del{opacity:1;}

/* theme chips */
.theme-row{display:flex;gap:7px;justify-content:center;margin-top:18px;}
.theme-chip{padding:6px 16px;border-radius:999px;font-size:.82rem;font-weight:700;border:1.5px solid var(--border);background:var(--s1);color:var(--muted);cursor:pointer;transition:all .15s;}
.theme-chip.active{background:var(--a1);color:#fff;border-color:var(--a1);}

/* ══════════════════════════════════════════
   SETUP WIZARD
══════════════════════════════════════════ */
#setupScreen{background:var(--bg);}
.setup-body{flex:1;padding:20px 24px;max-width:620px;width:100%;margin:0 auto;}
.wizard-steps{display:flex;gap:0;margin-bottom:24px;position:relative;}
.wizard-steps::before{content:'';position:absolute;top:14px;right:28px;left:28px;height:2px;background:var(--border);z-index:0;}
.w-step{flex:1;text-align:center;position:relative;z-index:1;}
.w-dot{width:28px;height:28px;border-radius:50%;border:2px solid var(--border);background:var(--s1);display:flex;align-items:center;justify-content:center;margin:0 auto 4px;font-size:.78rem;font-weight:700;color:var(--muted);transition:all .3s;}
.w-step.active .w-dot{background:var(--a1);border-color:var(--a1);color:#fff;}
.w-step.done .w-dot{background:var(--green);border-color:var(--green);color:#fff;}
.w-label{font-size:.72rem;color:var(--muted);font-weight:700;}
.w-step.active .w-label{color:var(--a1);}

.wizard-panel{display:none;}
.wizard-panel.active{display:block;}
.wiz-nav{display:flex;gap:9px;margin-top:18px;}
.wiz-nav .btn{flex:1;padding:12px;}

/* pts tags */
.pts-tags{display:flex;flex-wrap:wrap;gap:7px;margin-top:10px;}
.pts-tag{display:flex;align-items:center;gap:5px;background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:5px 12px;font-size:.87rem;font-weight:700;color:var(--a1);}
.pts-tag button{background:none;border:none;color:var(--muted);cursor:pointer;font-size:.88rem;padding:0 2px;}
.pts-tag button:hover{color:var(--red);}

/* ══════════════════════════════════════════
   QUESTION BANK
══════════════════════════════════════════ */
#bankScreen{background:var(--bg);}
.bank-body{flex:1;padding:18px 22px;max-width:800px;width:100%;margin:0 auto;}
.cat-box{background:var(--s1);border:1px solid var(--border);border-radius:16px;margin-bottom:14px;box-shadow:var(--sh);overflow:hidden;}
.cat-header{display:flex;align-items:center;justify-content:space-between;padding:14px 18px;cursor:pointer;gap:10px;transition:background .15s;}
.cat-header:hover{background:var(--s2);}
.cat-title{font-family:'Tajawal',sans-serif;font-size:1rem;font-weight:900;flex:1;}
.cat-meta{font-size:.78rem;color:var(--muted);}
.cat-arrow{transition:transform .25s;font-size:.85rem;color:var(--muted);}
.cat-box.open .cat-arrow{transform:rotate(90deg);}
.cat-body{display:none;padding:0 18px 14px;}
.cat-box.open .cat-body{display:block;}
.q-item{display:flex;align-items:flex-start;gap:10px;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:11px 13px;margin-bottom:8px;}
.q-item-txt{flex:1;}
.q-text{font-size:.9rem;font-weight:600;line-height:1.5;}
.q-answer{font-size:.8rem;color:var(--green);margin-top:3px;font-weight:700;}
.q-pts-badge{font-size:.75rem;color:var(--muted);margin-top:2px;}
.q-actions{display:flex;gap:5px;flex-shrink:0;}
.q-used{opacity:.45;}

.cat-add-row{display:flex;gap:8px;margin-top:10px;flex-wrap:wrap;}
.cat-add-row input{flex:1;min-width:140px;}

/* AI suggestion panel */
.ai-panel{background:linear-gradient(135deg,rgba(79,70,229,.06),rgba(124,58,237,.06));border:1.5px solid rgba(79,70,229,.18);border-radius:12px;padding:14px;margin-top:10px;}
.ai-panel-title{font-size:.82rem;font-weight:700;color:var(--a1);margin-bottom:10px;display:flex;align-items:center;gap:6px;}
.ai-q-chip{display:flex;align-items:flex-start;gap:9px;background:var(--s1);border:1px solid var(--border);border-radius:9px;padding:10px 12px;margin-bottom:7px;}
.ai-q-text{flex:1;font-size:.87rem;line-height:1.5;}
.ai-q-ans{font-size:.78rem;color:var(--green);font-weight:700;margin-top:2px;}

/* ══════════════════════════════════════════
   SCORING (JUDGE VIEW)
══════════════════════════════════════════ */
#scoringScreen{background:var(--bg);}
.sc-body{flex:1;padding:18px 22px;max-width:700px;width:100%;margin:0 auto;}

/* timer */
.timer-box{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:13px 18px;margin-bottom:16px;box-shadow:var(--sh);}
.timer-disp{font-family:'Tajawal',sans-serif;font-size:2.4rem;font-weight:900;color:var(--a1);min-width:90px;text-align:center;letter-spacing:2px;transition:color .3s;}
.timer-disp.urgent{color:var(--red);animation:blink .6s ease-in-out infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:.55;}}
.t-presets{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:6px;}
.t-pre{padding:5px 12px;background:var(--s2);border:1.5px solid var(--border);border-radius:8px;font-family:'Cairo',sans-serif;font-size:.8rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .13s;}
.t-pre:hover{border-color:var(--a3);color:var(--a3);}
.t-ctrls{display:flex;gap:6px;}
.t-btn{width:34px;height:34px;border:1.5px solid var(--border);border-radius:9px;background:var(--s2);font-size:.95rem;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .13s;color:var(--text2);}
.t-btn:hover{border-color:var(--a1);color:var(--a1);}
.t-btn.on{background:var(--green);border-color:var(--green);color:#fff;}

/* active question display */
.active-q-box{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:14px 18px;margin-bottom:16px;box-shadow:var(--sh);}
.aq-label{font-size:.75rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:6px;}
.aq-text{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:700;line-height:1.6;}
.aq-answer{font-size:.88rem;color:var(--green);font-weight:700;margin-top:6px;display:none;}
.aq-answer.show{display:block;}
.aq-pts{font-size:.8rem;color:var(--muted);margin-top:4px;}
.aq-actions{display:flex;gap:7px;margin-top:10px;flex-wrap:wrap;}

/* pts chips */
.pts-chips{display:flex;flex-wrap:wrap;gap:7px;margin:10px 0 18px;}
.pts-chip{padding:7px 16px;background:var(--s1);border:1.5px solid var(--border);border-radius:9px;font-family:'Cairo',sans-serif;font-size:.9rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .13s;box-shadow:var(--sh);}
.pts-chip:hover{border-color:var(--a1);color:var(--a1);}
.pts-chip.sel{background:var(--a1);border-color:var(--a1);color:#fff;}

/* team rows */
.team-btn-row{display:flex;align-items:center;justify-content:space-between;background:var(--s1);border:1.5px solid var(--border);border-radius:14px;padding:12px 16px;margin-bottom:9px;cursor:pointer;transition:all .18s;gap:12px;box-shadow:var(--sh);}
.team-btn-row:hover{border-color:var(--a1);box-shadow:var(--sh2);}
.team-btn-row.winner{border-color:var(--green);background:rgba(16,185,129,.06);box-shadow:0 4px 20px rgba(16,185,129,.15);}
.tbr-name{font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:700;flex:1;}
.tbr-score{font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:900;color:var(--gold);}
.award-badge{padding:4px 10px;background:var(--green);color:#fff;border-radius:7px;font-size:.8rem;font-weight:700;opacity:0;transition:opacity .2s;}
.team-btn-row.winner .award-badge{opacity:1;}

.action-bar{margin-top:14px;padding:13px 16px;background:var(--s1);border:1px solid var(--border);border-radius:14px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;box-shadow:var(--sh);}

/* undo history */
.history-log{max-height:180px;overflow-y:auto;margin-top:10px;}
.log-item{display:flex;align-items:center;justify-content:space-between;padding:7px 12px;background:var(--s2);border-radius:9px;margin-bottom:6px;font-size:.82rem;}
.log-q{color:var(--muted);}
.log-winner{font-weight:700;color:var(--text);}
.log-pts{color:var(--green);font-weight:900;}

/* ══════════════════════════════════════════
   LIVE BOARD
══════════════════════════════════════════ */
#liveScreen{
  align-items:center;padding:28px 20px 44px;
  background:
    radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.1) 0%,transparent 58%),
    radial-gradient(ellipse 50% 40% at 100% 100%,rgba(6,182,212,.07) 0%,transparent 55%),
    var(--bg);
}
.live-head{width:100%;max-width:720px;text-align:center;margin-bottom:28px;}
.live-comp-name{font-family:'Tajawal',sans-serif;font-size:2.3rem;font-weight:900;background:linear-gradient(135deg,var(--a1) 20%,var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:8px;line-height:1.2;}
.live-meta-pill{display:inline-flex;gap:8px;align-items:center;background:var(--s1);border:1.5px solid var(--border);border-radius:999px;padding:7px 20px;font-size:.87rem;font-weight:700;color:var(--muted);box-shadow:var(--sh);}
.live-meta-pill b{color:var(--a1);}

.rankings-wrap{width:100%;max-width:720px;position:relative;}
.rank-card{position:absolute;left:0;width:100%;display:flex;align-items:center;gap:14px;background:var(--s1);border:1.5px solid var(--border);border-radius:18px;padding:15px 20px;overflow:hidden;box-shadow:var(--sh);
  transition:top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s;}
.rank-card.rank-1{border-color:rgba(217,119,6,.4);background:linear-gradient(135deg,#fffbeb,#fef3c7 60%,var(--s1));}
.rank-card.rank-2{border-color:rgba(107,114,128,.25);}
.rank-card.rank-3{border-color:rgba(146,64,14,.25);}
.rank-card.just-scored{border-color:var(--green)!important;box-shadow:0 0 0 3px rgba(16,185,129,.14),var(--sh2)!important;}
.rank-medal{width:40px;height:40px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:900;flex-shrink:0;}
.rank-1 .rank-medal{background:linear-gradient(135deg,#fde68a,#d97706);color:#fff;box-shadow:0 2px 10px rgba(217,119,6,.38);}
.rank-2 .rank-medal{background:linear-gradient(135deg,#e5e7eb,#9ca3af);color:#fff;}
.rank-3 .rank-medal{background:linear-gradient(135deg,#fcd34d,#92400e);color:#fff;}
.rank-other .rank-medal{background:var(--s3);color:var(--muted);font-size:1rem;}
.rank-name{flex:1;font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:700;}
.rank-score{font-family:'Tajawal',sans-serif;font-size:1.6rem;font-weight:900;color:var(--a1);min-width:85px;text-align:left;}
.rank-1 .rank-score{color:var(--gold);}
.score-bar-track{position:absolute;bottom:0;right:0;left:0;height:4px;background:rgba(79,70,229,.06);}
.score-bar-fill{height:100%;background:linear-gradient(90deg,var(--a3),var(--a1),var(--a2));transition:width .85s cubic-bezier(.4,0,.2,1);border-radius:0 0 0 18px;}
.float-pts{position:absolute;font-family:'Tajawal',sans-serif;font-size:1.5rem;font-weight:900;color:var(--green);pointer-events:none;text-shadow:0 2px 10px rgba(16,185,129,.3);animation:floatUp 1.2s ease-out forwards;right:100px;top:6px;z-index:20;}
@keyframes floatUp{0%{opacity:1;transform:translateY(0) scale(.9);}30%{opacity:1;transform:translateY(-14px) scale(1.2);}100%{opacity:0;transform:translateY(-52px) scale(.85);}}
.live-footer{width:100%;max-width:720px;margin-top:22px;display:flex;gap:9px;flex-wrap:wrap;}
.live-footer .btn{flex:1;padding:12px;font-size:.96rem;}

/* ══════════════════════════════════════════
   AUDIENCE SCREEN (popup window)
══════════════════════════════════════════ */
/* This content is injected into a new window */

/* ══════════════════════════════════════════
   FINALE SCREEN
══════════════════════════════════════════ */
#finaleScreen{
  align-items:center;justify-content:center;padding:40px 20px;
  background:
    radial-gradient(ellipse 90% 60% at 50% 0%,rgba(79,70,229,.14) 0%,transparent 65%),
    var(--bg);
}
.finale-wrap{width:100%;max-width:640px;text-align:center;}
.finale-trophy{font-size:5rem;margin-bottom:12px;animation:trophyBounce .8s ease-out;}
@keyframes trophyBounce{0%{transform:scale(.5) translateY(30px);opacity:0;}70%{transform:scale(1.15) translateY(-10px);}100%{transform:scale(1) translateY(0);opacity:1;}}
.finale-title{font-family:'Tajawal',sans-serif;font-size:1.5rem;font-weight:900;color:var(--muted);margin-bottom:6px;}
.finale-winner{font-family:'Tajawal',sans-serif;font-size:2.8rem;font-weight:900;background:linear-gradient(135deg,var(--gold),var(--orange));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:24px;}
.finale-podium{display:flex;align-items:flex-end;justify-content:center;gap:10px;margin:24px 0 32px;}
.podium-item{display:flex;flex-direction:column;align-items:center;gap:6px;}
.podium-rank{font-family:'Tajawal',sans-serif;font-weight:900;font-size:.9rem;color:var(--muted);}
.podium-name{font-family:'Tajawal',sans-serif;font-weight:700;font-size:.9rem;max-width:90px;text-align:center;}
.podium-score{font-size:.82rem;color:var(--gold);font-weight:900;}
.podium-bar{width:70px;border-radius:8px 8px 0 0;display:flex;align-items:center;justify-content:center;font-size:1.5rem;}
.podium-1 .podium-bar{height:90px;background:linear-gradient(180deg,#fde68a,#d97706);}
.podium-2 .podium-bar{height:60px;background:linear-gradient(180deg,#e5e7eb,#9ca3af);}
.podium-3 .podium-bar{height:45px;background:linear-gradient(180deg,#fcd34d,#92400e);}
.finale-acts{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;}
.finale-acts .btn{padding:12px 24px;}

/* summary */
.summary-table{width:100%;border-collapse:collapse;margin-top:16px;text-align:right;}
.summary-table th{font-size:.75rem;font-weight:700;color:var(--muted);padding:8px 12px;border-bottom:1px solid var(--border);text-transform:uppercase;}
.summary-table td{padding:9px 12px;border-bottom:1px solid var(--border);font-size:.87rem;}
.summary-table tr:last-child td{border:none;}

/* ══════════════════════════════════════════
   PARTICLES / FLASH
══════════════════════════════════════════ */
.particles{position:fixed;inset:0;pointer-events:none;z-index:999;}
.prt{position:absolute;border-radius:3px;animation:prtFall linear forwards;}
@keyframes prtFall{0%{transform:translateY(-10px) rotate(0deg);opacity:1;}100%{transform:translateY(110vh) rotate(700deg);opacity:0;}}
.flash-el{position:fixed;inset:0;pointer-events:none;z-index:998;opacity:0;background:rgba(16,185,129,.08);transition:opacity .15s;}
.flash-el.on{opacity:1;}

/* scrollbar */
::-webkit-scrollbar{width:6px;height:6px;}
::-webkit-scrollbar-track{background:transparent;}
::-webkit-scrollbar-thumb{background:var(--border);border-radius:3px;}

@media(max-width:600px){
  .live-comp-name{font-size:1.7rem;}.rank-name{font-size:1rem;}.rank-score{font-size:1.3rem;}
  .sc-body,.setup-body,.bank-body{padding:12px;}
  .home-hero{padding:40px 16px 28px;}
  .site-name-display{font-size:2.2rem;}
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
    <div class="site-name-display" id="siteNameDisplay">منصة المسابقات</div>
    <div class="home-sub" id="homeSub">إدارة مسابقاتك باحترافية</div>
    <div class="home-ctas">
      <button class="btn btn-grad" onclick="startNew()">+ مسابقة جديدة</button>
      <button class="btn btn-ghost" onclick="editSiteName()">تعديل الاسم</button>
    </div>
    <div class="theme-row" style="margin-top:22px;">
      <div class="theme-chip" data-mode="light" onclick="setTheme('light')">فاتح</div>
      <div class="theme-chip" data-mode="auto"  onclick="setTheme('auto')">تلقائي</div>
      <div class="theme-chip" data-mode="dark"  onclick="setTheme('dark')">داكن</div>
    </div>
  </div>
  <div class="home-body">
    <div class="stats-bar" id="statsBar"></div>
    <div class="lbl">المسابقات السابقة</div>
    <div id="histList"><div class="empty">لا توجد مسابقات سابقة</div></div>
  </div>
</div>

<!-- ══════════ SETUP WIZARD ══════════ -->
<div class="screen" id="setupScreen">
  <div class="top-nav">
    <div class="nav-brand" id="setupNavBrand">مسابقة جديدة</div>
    <div class="nav-acts">
      <div class="icon-btn" onclick="confirmLeaveSetup()">✕</div>
    </div>
  </div>
  <div class="setup-body">
    <div class="wizard-steps">
      <div class="w-step active" id="ws0"><div class="w-dot">1</div><div class="w-label">الهوية</div></div>
      <div class="w-step" id="ws1"><div class="w-dot">2</div><div class="w-label">الفرق</div></div>
      <div class="w-step" id="ws2"><div class="w-dot">3</div><div class="w-label">النقاط</div></div>
      <div class="w-step" id="ws3"><div class="w-dot">4</div><div class="w-label">الأسئلة</div></div>
    </div>

    <!-- STEP 0: identity -->
    <div class="wizard-panel active" id="wp0">
      <div class="card">
        <div class="lbl">اسم المسابقة</div>
        <input type="text" id="compTitle" placeholder="مثال: مسابقة الثقافة العامة">
      </div>
      <div class="card">
        <div class="lbl">اسم المجموعة المتسابقة (اختياري)</div>
        <input type="text" id="compGroup" placeholder="مثال: طلاب الفصل الثالث">
      </div>
      <div class="card">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;">
          <div class="lbl" style="margin:0;">ترتيب الأسئلة</div>
        </div>
        <div style="display:flex;gap:9px;">
          <label style="flex:1;display:flex;align-items:center;gap:8px;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;padding:11px 14px;cursor:pointer;">
            <input type="radio" name="qorder" value="ordered" checked style="width:auto;"> مرتب بالتسلسل
          </label>
          <label style="flex:1;display:flex;align-items:center;gap:8px;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;padding:11px 14px;cursor:pointer;">
            <input type="radio" name="qorder" value="random" style="width:auto;"> عشوائي
          </label>
        </div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-grad" onclick="wizNext(0)">التالي ←</button>
      </div>
    </div>

    <!-- STEP 1: teams -->
    <div class="wizard-panel" id="wp1">
      <div class="card">
        <div class="lbl">اضافة فريق</div>
        <div class="row">
          <input type="text" id="teamInput" placeholder="اسم الفريق" onkeydown="if(event.key==='Enter')addTeam()">
          <button class="btn btn-a1" onclick="addTeam()">اضافة</button>
        </div>
        <div id="setupTeamsList" style="margin-top:10px;"><div class="empty">لا توجد فرق بعد</div></div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-ghost" onclick="wizPrev(1)">→ السابق</button>
        <button class="btn btn-grad" onclick="wizNext(1)">التالي ←</button>
      </div>
    </div>

    <!-- STEP 2: points -->
    <div class="wizard-panel" id="wp2">
      <div class="card">
        <div class="lbl">فئات النقاط</div>
        <div class="pts-tags" id="ptsTagWrap"></div>
        <div class="row" style="margin-top:10px;">
          <input type="number" id="ptsAddInput" placeholder="أضف فئة (مثال: 300)" min="10" step="50" style="max-width:200px;">
          <button class="btn btn-ghost btn-sm" onclick="addPtsTag()" style="padding:10px 16px;">اضافة</button>
          <button class="btn btn-ghost btn-sm" onclick="resetPts()" style="padding:10px 14px;">افتراضي</button>
        </div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-ghost" onclick="wizPrev(2)">→ السابق</button>
        <button class="btn btn-grad" onclick="wizNext(2)">التالي ←</button>
      </div>
    </div>

    <!-- STEP 3: questions -->
    <div class="wizard-panel" id="wp3">
      <div class="card">
        <p style="color:var(--text2);font-size:.9rem;margin-bottom:12px;">يمكنك البدء بدون أسئلة وإدارة بنك الأسئلة لاحقاً، أو الذهاب لإضافة الأسئلة الآن.</p>
        <div style="display:flex;gap:9px;flex-wrap:wrap;">
          <button class="btn btn-a1" onclick="goToBankFromSetup()">+ اضافة أسئلة الآن</button>
          <button class="btn btn-ghost" onclick="setupDone()">بدء بدون أسئلة</button>
        </div>
      </div>
      <div class="wiz-nav">
        <button class="btn btn-ghost" onclick="wizPrev(3)">→ السابق</button>
        <button class="btn btn-grad" onclick="setupDone()">بدء المسابقة</button>
      </div>
    </div>
  </div>
</div>

<!-- ══════════ QUESTION BANK ══════════ -->
<div class="screen" id="bankScreen">
  <div class="top-nav">
    <div class="nav-brand">بنك الأسئلة</div>
    <div class="nav-acts">
      <div class="icon-btn" onclick="addCategory()" title="تصنيف جديد">+</div>
      <div class="icon-btn" onclick="returnFromBank()" title="رجوع">←</div>
    </div>
  </div>
  <div class="bank-body">
    <div id="bankCats"><div class="empty">اضغط + لإضافة تصنيف</div></div>
  </div>
</div>

<!-- ══════════ SCORING (JUDGE) ══════════ -->
<div class="screen" id="scoringScreen">
  <div class="top-nav">
    <div class="nav-brand" id="scBrand">المسابقة</div>
    <div class="nav-acts">
      <div class="pill">السؤال <span id="qNum">1</span></div>
      <div class="icon-btn" onclick="openDisplayWindow()" title="شاشة المتسابقين">📺</div>
      <div class="icon-btn" onclick="openSettingsModal()" title="الاعدادات">⚙</div>
      <div class="icon-btn" onclick="goHome()" title="الرئيسية">⌂</div>
    </div>
  </div>
  <div class="sc-body">
    <!-- TIMER -->
    <div class="timer-box">
      <div class="timer-disp" id="timerDisp">00:30</div>
      <div>
        <div class="t-presets">
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
        </div>
      </div>
    </div>

    <!-- ACTIVE QUESTION -->
    <div class="active-q-box" id="activeQBox">
      <div class="aq-label">السؤال الحالي</div>
      <div class="aq-text" id="aqText">لا يوجد سؤال محدد</div>
      <div class="aq-answer" id="aqAnswer"></div>
      <div class="aq-pts" id="aqPts"></div>
      <div class="aq-actions">
        <button class="btn btn-ghost btn-sm" onclick="toggleAnswer()">إظهار الإجابة</button>
        <button class="btn btn-ghost btn-sm" onclick="pickNextQuestion()">← سؤال آخر</button>
        <button class="btn btn-ghost btn-sm" onclick="toggleDisplayQ()" id="displayQBtn">إرسال للشاشة</button>
      </div>
    </div>

    <div class="lbl">النقاط</div>
    <div class="pts-chips" id="ptsChips"></div>

    <div class="lbl">المجموعة الفائزة بهذا السؤال</div>
    <div id="teamBtns"></div>

    <div class="action-bar">
      <button class="btn btn-ghost btn-sm" onclick="undoLast()" id="undoBtn" disabled>↩ تراجع</button>
      <div style="display:flex;gap:8px;flex-wrap:wrap;">
        <button class="btn btn-grad" onclick="confirmAndNext()">تسجيل وعرض اللوحة</button>
      </div>
    </div>

    <!-- log -->
    <div style="margin-top:16px;">
      <div class="lbl">سجل الأسئلة</div>
      <div class="history-log" id="historyLog"><div class="empty">لا يوجد سجل بعد</div></div>
    </div>
  </div>
</div>

<!-- ══════════ LIVE BOARD ══════════ -->
<div class="screen" id="liveScreen">
  <div class="live-head">
    <div class="live-comp-name" id="liveName">المسابقة</div>
    <div class="live-meta-pill" id="liveMeta">السؤال <b id="liveQ">—</b></div>
  </div>
  <div class="rankings-wrap" id="rankingsWrap"></div>
  <div class="live-footer" id="liveFooter"></div>
</div>

<!-- ══════════ FINALE ══════════ -->
<div class="screen" id="finaleScreen">
  <div class="finale-wrap">
    <div class="finale-trophy">🏆</div>
    <div class="finale-title">الفائز بالمسابقة</div>
    <div class="finale-winner" id="finaleWinner">—</div>
    <div class="finale-podium" id="finalePodium"></div>
    <div class="finale-acts">
      <button class="btn btn-grad" onclick="goHome()">الرئيسية</button>
      <button class="btn btn-ghost" onclick="showSummary()">ملخص المسابقة</button>
    </div>
    <div id="summarySection" style="display:none;margin-top:20px;text-align:right;">
      <table class="summary-table" id="summaryTable"></table>
    </div>
  </div>
</div>

<!-- ══════════ MODALS ══════════ -->
<!-- Site name modal -->
<div class="modal-bg" id="siteNameModal">
  <div class="modal-box">
    <div class="modal-title">اسم الموقع</div>
    <input type="text" id="siteNameInput" placeholder="منصة المسابقات">
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="saveSiteName()">حفظ</button>
      <button class="btn btn-ghost" onclick="closeModal('siteNameModal')">إلغاء</button>
    </div>
  </div>
</div>

<!-- Settings modal (mid-game) -->
<div class="modal-bg" id="settingsModal">
  <div class="modal-box">
    <div class="modal-title">الاعدادات</div>
    <div class="tab-bar" style="margin-bottom:14px;">
      <button class="tab-btn active" onclick="settingsTab(0)">الفرق</button>
      <button class="tab-btn" onclick="settingsTab(1)">النقاط</button>
      <button class="tab-btn" onclick="settingsTab(2)">المسابقة</button>
    </div>
    <div id="stPanel0">
      <div class="lbl">اضافة فريق</div>
      <div class="row" style="margin-bottom:10px;">
        <input type="text" id="stTeamInput" placeholder="اسم الفريق" onkeydown="if(event.key==='Enter')stAddTeam()">
        <button class="btn btn-a1" onclick="stAddTeam()">اضافة</button>
      </div>
      <div id="stTeamsList"></div>
      <div class="lbl" style="margin-top:14px;">تعديل النقاط يدوياً</div>
      <div id="stScoreEdit"></div>
    </div>
    <div id="stPanel1" style="display:none;">
      <div class="pts-tags" id="stPtsTags"></div>
      <div class="row" style="margin-top:10px;">
        <input type="number" id="stPtsInput" placeholder="فئة جديدة" min="10" step="50" style="max-width:180px;">
        <button class="btn btn-ghost btn-sm" onclick="stAddPts()" style="padding:10px 16px;">اضافة</button>
        <button class="btn btn-ghost btn-sm" onclick="stResetPts()" style="padding:10px 14px;">افتراضي</button>
      </div>
    </div>
    <div id="stPanel2" style="display:none;">
      <div class="lbl">اسم المسابقة</div>
      <input type="text" id="stCompTitle" style="margin-bottom:10px;">
      <div class="lbl">اسم المجموعة</div>
      <input type="text" id="stCompGroup">
    </div>
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="saveSettings()">حفظ</button>
      <button class="btn btn-ghost" onclick="closeModal('settingsModal')">إغلاق</button>
    </div>
  </div>
</div>

<!-- Edit score modal -->
<div class="modal-bg" id="editScoreModal">
  <div class="modal-box">
    <div class="modal-title">تعديل نقاط: <span id="esTeamName"></span></div>
    <input type="number" id="esNewScore" min="0">
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="saveEditScore()">حفظ</button>
      <button class="btn btn-ghost" onclick="closeModal('editScoreModal')">إلغاء</button>
    </div>
  </div>
</div>

<!-- Resume modal -->
<div class="modal-bg" id="resumeModal">
  <div class="modal-box">
    <div class="modal-title">استئناف المسابقة؟</div>
    <div style="color:var(--text2);font-size:.9rem;" id="resumeText"></div>
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="resumeComp()">استئناف</button>
      <button class="btn btn-ghost" onclick="closeModal('resumeModal')">إلغاء</button>
    </div>
  </div>
</div>

<!-- AI Questions modal -->
<div class="modal-bg" id="aiModal">
  <div class="modal-box" style="max-width:540px;">
    <div class="modal-title">اقتراح أسئلة بالذكاء الاصطناعي</div>
    <div class="lbl">الموضوع / التصنيف</div>
    <input type="text" id="aiTopic" placeholder="مثال: جغرافيا العالم العربي" style="margin-bottom:10px;">
    <div style="display:flex;gap:9px;margin-bottom:10px;">
      <select id="aiCount" style="width:auto;flex:none;">
        <option value="3">3 أسئلة</option>
        <option value="5" selected>5 أسئلة</option>
        <option value="10">10 أسئلة</option>
      </select>
      <select id="aiLang" style="width:auto;flex:none;">
        <option value="ar">عربي</option>
        <option value="en">English</option>
      </select>
    </div>
    <button class="btn btn-grad" onclick="generateAIQuestions()" id="aiGenBtn" style="width:100%;margin-bottom:12px;">توليد الأسئلة</button>
    <div id="aiResults"></div>
    <div class="modal-acts">
      <button class="btn btn-ghost" onclick="closeModal('aiModal')">إغلاق</button>
    </div>
  </div>
</div>

<script>
/* ═══════════════════════════════════════════
   STORAGE
═══════════════════════════════════════════ */
const S = {
  get:(k)=>{try{return JSON.parse(localStorage.getItem(k));}catch{return null;}},
  set:(k,v)=>localStorage.setItem(k,JSON.stringify(v))
};

/* ═══════════════════════════════════════════
   STATE
═══════════════════════════════════════════ */
let G = {
  id:null, title:'', group:'', qOrder:'ordered',
  teams:[], ptsOptions:[100,200,300,400,500],
  categories:[], // [{id,name,questions:[{id,text,answer,pts,used}]}]
  currentQ:1, selPts:100, selTeamIdx:-1,
  lastWinner:-1, lastPts:0,
  questionLog:[], // [{q,teamName,pts}]
  activeQuestion:null, // {text,answer,pts,catId,qId}
  showQOnDisplay:false,
  timerSecs:30, timerLeft:30, timerRunning:false,
};
let cardEls={};
const CARD_H=78, CARD_GAP=12;
let timerInt=null;
let displayWindow=null;
let bankReturnScreen='setupScreen';
let aiTargetCatId=null;
let editScoreTeamIdx=-1;

/* ═══════════════════════════════════════════
   THEME
═══════════════════════════════════════════ */
let themeMode=S.get('themeMode')||'auto';
function applyTheme(){
  const dark=themeMode==='dark'||(themeMode==='auto'&&window.matchMedia('(prefers-color-scheme: dark)').matches);
  document.documentElement.setAttribute('data-theme',dark?'dark':'light');
  document.querySelectorAll('.theme-chip').forEach(c=>c.classList.toggle('active',c.dataset.mode===themeMode));
  pushToDisplay();
}
function setTheme(m){themeMode=m;S.set('themeMode',m);applyTheme();}
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change',applyTheme);
applyTheme();

/* ═══════════════════════════════════════════
   SITE NAME
═══════════════════════════════════════════ */
let siteName=S.get('siteName')||'منصة المسابقات';
function renderSiteName(){
  document.getElementById('siteNameDisplay').textContent=siteName;
  document.title=siteName;
}
function editSiteName(){document.getElementById('siteNameInput').value=siteName;openModal('siteNameModal');}
function saveSiteName(){const v=document.getElementById('siteNameInput').value.trim();if(v){siteName=v;S.set('siteName',v);renderSiteName();}closeModal('siteNameModal');}

/* ═══════════════════════════════════════════
   HISTORY
═══════════════════════════════════════════ */
function getHistory(){return S.get('compHistory')||[];}
function saveHistory(){
  if(!G.title||!G.teams.length) return;
  let h=getHistory();
  const rec={
    id:G.id||Date.now(),title:G.title,group:G.group,
    teams:JSON.parse(JSON.stringify(G.teams)),
    ptsOptions:[...G.ptsOptions],
    categories:JSON.parse(JSON.stringify(G.categories)),
    questionLog:[...G.questionLog],
    currentQ:G.currentQ,selPts:G.selPts,
    qOrder:G.qOrder, savedAt:Date.now()
  };
  G.id=rec.id;
  const idx=h.findIndex(x=>x.id===rec.id);
  if(idx>=0)h[idx]=rec; else h.unshift(rec);
  h=h.slice(0,15);
  S.set('compHistory',h);
}
function delHistory(id){S.set('compHistory',getHistory().filter(x=>x.id!==id));renderHistList();}
function renderHistList(){
  const h=getHistory();
  const statsEl=document.getElementById('statsBar');
  statsEl.innerHTML=`
    <div class="stat-card"><div class="stat-num">${h.length}</div><div class="stat-lbl">مسابقة</div></div>
    <div class="stat-card"><div class="stat-num">${h.reduce((a,b)=>a+(b.teams?.length||0),0)}</div><div class="stat-lbl">فريق إجمالي</div></div>
    <div class="stat-card"><div class="stat-num">${h.reduce((a,b)=>a+(b.questionLog?.length||0),0)}</div><div class="stat-lbl">سؤال مجاب</div></div>`;

  const el=document.getElementById('histList');
  if(!h.length){el.innerHTML='<div class="empty">لا توجد مسابقات سابقة</div>';return;}
  el.innerHTML=h.map(r=>{
    const d=new Date(r.savedAt);
    const ds=d.toLocaleDateString('ar-SA',{month:'short',day:'numeric',hour:'2-digit',minute:'2-digit'});
    const leader=r.teams?.slice().sort((a,b)=>b.score-a.score)[0];
    const qs=r.categories?.reduce((a,c)=>a+c.questions.length,0)||0;
    return `<div class="hist-item" onclick="loadComp(${r.id})">
      <div class="hist-ico">🏆</div>
      <div class="hist-info">
        <div class="hist-name">${r.title}${r.group?` — ${r.group}`:''}</div>
        <div class="hist-meta">${r.teams?.length||0} فرق · سؤال ${r.currentQ} · ${qs} سؤال في البنك${leader?' · المتصدر: '+leader.name:''} · ${ds}</div>
      </div>
      <button class="btn btn-sm btn-rg hist-del" onclick="event.stopPropagation();delHistory(${r.id})">حذف</button>
    </div>`;
  }).join('');
}
function loadComp(id){
  const rec=getHistory().find(x=>x.id===id);
  if(!rec)return;
  document.getElementById('resumeText').innerHTML=`<b>${rec.title}</b><br>السؤال ${rec.currentQ} · ${rec.teams?.length} فرق · هل تريد استئنافها؟`;
  document.getElementById('resumeModal')._id=id;
  openModal('resumeModal');
}
function resumeComp(){
  const id=document.getElementById('resumeModal')._id;
  const rec=getHistory().find(x=>x.id===id);
  closeModal('resumeModal');
  if(!rec)return;
  G={...G,...rec,teams:JSON.parse(JSON.stringify(rec.teams)),categories:JSON.parse(JSON.stringify(rec.categories||[])),questionLog:[...(rec.questionLog||[])],ptsOptions:[...rec.ptsOptions],selTeamIdx:-1,lastWinner:-1,lastPts:0,timerSecs:30,timerLeft:30,timerRunning:false,activeQuestion:null,showQOnDisplay:false};
  cardEls={};
  renderScoring();
  goTo('scoringScreen');
}

/* ═══════════════════════════════════════════
   HOME
═══════════════════════════════════════════ */
function goHome(){
  stopTimer();saveHistory();renderHistList();goTo('homeScreen');
}
function startNew(){
  G={id:null,title:'',group:'',qOrder:'ordered',teams:[],ptsOptions:[100,200,300,400,500],categories:[],currentQ:1,selPts:100,selTeamIdx:-1,lastWinner:-1,lastPts:0,questionLog:[],activeQuestion:null,showQOnDisplay:false,timerSecs:30,timerLeft:30,timerRunning:false};
  cardEls={};
  renderSetupWizard(0);
  goTo('setupScreen');
}
function confirmLeaveSetup(){if(confirm('هل تريد الخروج؟'))goTo('homeScreen');}

/* ═══════════════════════════════════════════
   SETUP WIZARD
═══════════════════════════════════════════ */
function renderSetupWizard(step){
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
function wizNext(step){
  if(step===0){
    const t=document.getElementById('compTitle').value.trim();
    if(!t){alert('اكتب اسم المسابقة');return;}
    G.title=t;G.group=document.getElementById('compGroup').value.trim();
    G.qOrder=document.querySelector('input[name=qorder]:checked').value;
  }
  if(step===1&&!G.teams.length){alert('اضف فريقاً واحداً على الأقل');return;}
  renderSetupWizard(step+1);
}
function wizPrev(step){renderSetupWizard(step-1);}

function renderSetupTeams(){
  const el=document.getElementById('setupTeamsList');
  if(!G.teams.length){el.innerHTML='<div class="empty">لا توجد فرق بعد</div>';return;}
  el.innerHTML=G.teams.map((t,i)=>`
    <div style="display:flex;align-items:center;justify-content:space-between;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:9px 13px;margin-bottom:7px;">
      <span style="font-weight:700;">${t.name}</span>
      <button class="btn btn-sm btn-rg" onclick="removeTeam(${i})">حذف</button>
    </div>`).join('');
}
function addTeam(){
  const inp=document.getElementById('teamInput');const n=inp.value.trim();
  if(!n)return;if(G.teams.find(t=>t.name===n)){inp.select();return;}
  G.teams.push({name:n,score:0});inp.value='';inp.focus();renderSetupTeams();
}
function removeTeam(i){G.teams.splice(i,1);renderSetupTeams();}

function renderPtsTags(){
  document.getElementById('ptsTagWrap').innerHTML=G.ptsOptions.map((p,i)=>`
    <div class="pts-tag">${p}<button onclick="removePtsTag(${i})">✕</button></div>`).join('');
}
function addPtsTag(){
  const v=parseInt(document.getElementById('ptsAddInput').value);
  if(!v||v<10)return;
  if(!G.ptsOptions.includes(v)){G.ptsOptions.push(v);G.ptsOptions.sort((a,b)=>a-b);}
  document.getElementById('ptsAddInput').value='';renderPtsTags();
}
function removePtsTag(i){if(G.ptsOptions.length<=1)return;G.ptsOptions.splice(i,1);renderPtsTags();}
function resetPts(){G.ptsOptions=[100,200,300,400,500];renderPtsTags();}

function goToBankFromSetup(){bankReturnScreen='setupScreen';renderBank();goTo('bankScreen');}
function setupDone(){
  const t=document.getElementById('compTitle').value.trim()||G.title;
  if(!t){alert('اكتب اسم المسابقة');return;}
  if(!G.teams.length){alert('اضف فريقاً واحداً على الأقل');return;}
  G.title=t;G.group=document.getElementById('compGroup').value.trim()||G.group;
  G.selPts=G.ptsOptions[0];
  cardEls={};
  renderScoring();goTo('scoringScreen');
}

/* ═══════════════════════════════════════════
   QUESTION BANK
═══════════════════════════════════════════ */
function renderBank(){
  const el=document.getElementById('bankCats');
  if(!G.categories.length){el.innerHTML='<div class="empty">اضغط + لإضافة تصنيف</div>';return;}
  el.innerHTML=G.categories.map((cat,ci)=>`
    <div class="cat-box" id="cat-${cat.id}">
      <div class="cat-header" onclick="toggleCat('${cat.id}')">
        <div class="cat-title">${cat.name}</div>
        <div class="cat-meta">${cat.questions.length} سؤال · ${cat.questions.filter(q=>q.used).length} مستخدم</div>
        <div style="display:flex;gap:6px;align-items:center;">
          <button class="btn btn-sm" style="background:rgba(79,70,229,.1);color:var(--a1);border:none;" onclick="event.stopPropagation();openAI('${cat.id}')">✦ AI</button>
          <button class="btn btn-sm btn-rg" onclick="event.stopPropagation();deleteCat('${cat.id}')">حذف</button>
        </div>
        <div class="cat-arrow">›</div>
      </div>
      <div class="cat-body">
        ${cat.questions.map((q,qi)=>`
          <div class="q-item ${q.used?'q-used':''}">
            <div class="q-item-txt">
              <div class="q-text">${q.text}</div>
              ${q.answer?`<div class="q-answer">الإجابة: ${q.answer}</div>`:''}
              <div class="q-pts-badge">${q.pts||'—'} نقطة</div>
            </div>
            <div class="q-actions">
              <button class="btn btn-sm btn-ghost" onclick="editQuestion('${cat.id}',${qi})">✎</button>
              <button class="btn btn-sm btn-rg" onclick="deleteQuestion('${cat.id}',${qi})">✕</button>
            </div>
          </div>`).join('')}
        <div class="cat-add-row">
          <input type="text" placeholder="نص السؤال" id="qt-${cat.id}">
          <input type="text" placeholder="الإجابة" id="qa-${cat.id}" style="max-width:160px;">
          <select id="qp-${cat.id}" style="width:auto;flex:none;">
            ${G.ptsOptions.map(p=>`<option value="${p}">${p}</option>`).join('')}
          </select>
          <button class="btn btn-a1 btn-sm" onclick="addQuestion('${cat.id}')">اضافة</button>
        </div>
      </div>
    </div>`).join('');
  // open all by default
  G.categories.forEach(c=>document.getElementById('cat-'+c.id)?.classList.add('open'));
}
function toggleCat(id){document.getElementById('cat-'+id)?.classList.toggle('open');}
function addCategory(){
  const n=prompt('اسم التصنيف:');if(!n)return;
  G.categories.push({id:Date.now().toString(),name:n,questions:[]});
  renderBank();
}
function deleteCat(id){if(!confirm('حذف التصنيف وكل أسئلته؟'))return;G.categories=G.categories.filter(c=>c.id!==id);renderBank();}
function addQuestion(catId){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const t=document.getElementById('qt-'+catId).value.trim();if(!t)return;
  const a=document.getElementById('qa-'+catId).value.trim();
  const p=parseInt(document.getElementById('qp-'+catId).value)||G.ptsOptions[0];
  cat.questions.push({id:Date.now().toString(),text:t,answer:a,pts:p,used:false});
  document.getElementById('qt-'+catId).value='';
  document.getElementById('qa-'+catId).value='';
  renderBank();saveHistory();
}
function deleteQuestion(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  cat.questions.splice(qi,1);renderBank();
}
function editQuestion(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const q=cat.questions[qi];
  const nt=prompt('نص السؤال:',q.text);if(nt===null)return;
  const na=prompt('الإجابة:',q.answer||'');
  const np=parseInt(prompt('النقاط:',q.pts||G.ptsOptions[0]));
  cat.questions[qi]={...q,text:nt||q.text,answer:na,pts:isNaN(np)?q.pts:np};
  renderBank();saveHistory();
}
function returnFromBank(){
  saveHistory();
  if(bankReturnScreen==='setupScreen'){renderSetupWizard(3);goTo('setupScreen');}
  else{renderScoring();goTo('scoringScreen');}
}

/* ═══════════════════════════════════════════
   AI QUESTIONS
═══════════════════════════════════════════ */
function openAI(catId){
  aiTargetCatId=catId;
  const cat=G.categories.find(c=>c.id===catId);
  document.getElementById('aiTopic').value=cat?cat.name:'';
  document.getElementById('aiResults').innerHTML='';
  openModal('aiModal');
}
async function generateAIQuestions(){
  const topic=document.getElementById('aiTopic').value.trim();
  if(!topic){alert('اكتب موضوعاً');return;}
  const count=document.getElementById('aiCount').value;
  const lang=document.getElementById('aiLang').value;
  const btn=document.getElementById('aiGenBtn');
  btn.textContent='جاري التوليد...';btn.disabled=true;
  document.getElementById('aiResults').innerHTML='<div class="empty">جاري توليد الأسئلة...</div>';
  const prompt=lang==='ar'
    ?`أنت مساعد لإنشاء أسئلة مسابقات. أنشئ ${count} أسئلة عن "${topic}" باللغة العربية. أجب بـ JSON فقط بدون أي نص إضافي أو Markdown، بالشكل: [{"text":"...","answer":"...","pts":100}] وتنوع النقاط بين ${G.ptsOptions.join('، ')}`
    :`Create ${count} quiz questions about "${topic}" in English. Reply ONLY with JSON array, no markdown: [{"text":"...","answer":"...","pts":100}] vary points among ${G.ptsOptions.join(', ')}`;
  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',headers:{'Content-Type':'application/json'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,messages:[{role:'user',content:prompt}]})
    });
    const data=await res.json();
    const raw=data.content?.map(b=>b.text||'').join('');
    const cleaned=raw.replace(/```json|```/g,'').trim();
    const questions=JSON.parse(cleaned);
    if(!Array.isArray(questions))throw new Error('bad format');
    document.getElementById('aiResults').innerHTML=`
      <div class="ai-panel">
        <div class="ai-panel-title">✦ الأسئلة المقترحة</div>
        ${questions.map((q,i)=>`
          <div class="ai-q-chip">
            <div style="flex:1;">
              <div class="ai-q-text">${q.text}</div>
              ${q.answer?`<div class="ai-q-ans">الإجابة: ${q.answer}</div>`:''}
            </div>
            <button class="btn btn-green btn-sm" onclick="addAIQuestion(${i})">+ اضافة</button>
          </div>`).join('')}
        <button class="btn btn-a1 btn-sm" onclick="addAllAIQuestions()" style="width:100%;margin-top:6px;">إضافة الكل</button>
      </div>`;
    document.getElementById('aiResults')._questions=questions;
  }catch(e){document.getElementById('aiResults').innerHTML='<div class="empty" style="color:var(--red)">فشل التوليد. تأكد من الاتصال وحاول مرة أخرى.</div>';}
  btn.textContent='توليد الأسئلة';btn.disabled=false;
}
function addAIQuestion(i){
  const qs=document.getElementById('aiResults')._questions;if(!qs)return;
  const q=qs[i];const cat=G.categories.find(c=>c.id===aiTargetCatId);if(!cat)return;
  const pts=G.ptsOptions.includes(q.pts)?q.pts:G.ptsOptions[0];
  cat.questions.push({id:Date.now().toString(),text:q.text,answer:q.answer||'',pts,used:false});
  renderBank();saveHistory();
}
function addAllAIQuestions(){
  const qs=document.getElementById('aiResults')._questions;if(!qs)return;
  qs.forEach((_,i)=>addAIQuestion(i));
}

/* ═══════════════════════════════════════════
   TIMER
═══════════════════════════════════════════ */
function fmt(s){return String(Math.floor(s/60)).padStart(2,'0')+':'+String(s%60).padStart(2,'0');}
function updateTimerUI(){
  const el=document.getElementById('timerDisp');if(!el)return;
  el.textContent=fmt(G.timerLeft);
  el.classList.toggle('urgent',G.timerLeft<=5&&G.timerLeft>0);
  pushToDisplay();
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
  const b=document.getElementById('tPlayBtn');
  if(b){b.textContent='▶';b.classList.remove('on');}
}
function resetTimer(){stopTimer();G.timerLeft=G.timerSecs;updateTimerUI();}

/* ═══════════════════════════════════════════
   SCORING
═══════════════════════════════════════════ */
function renderScoring(){
  document.getElementById('scBrand').textContent=G.title;
  document.getElementById('qNum').textContent=G.currentQ;
  updateTimerUI();

  // pts chips
  document.getElementById('ptsChips').innerHTML=G.ptsOptions.map(p=>`
    <div class="pts-chip ${p===G.selPts?'sel':''}" onclick="selPts(${p})">${p}</div>`).join('');

  renderTeamBtns();
  renderLog();
  updateActiveQBox();
  document.getElementById('undoBtn').disabled=!G.questionLog.length;
}
function selPts(p){G.selPts=p;document.querySelectorAll('.pts-chip').forEach(c=>c.classList.toggle('sel',parseInt(c.textContent)===p));renderTeamBtns();}
function selectTeam(i){G.selTeamIdx=G.selTeamIdx===i?-1:i;renderTeamBtns();}
function renderTeamBtns(){
  document.getElementById('teamBtns').innerHTML=G.teams.map((t,i)=>`
    <div class="team-btn-row ${i===G.selTeamIdx?'winner':''}" onclick="selectTeam(${i})">
      <div class="tbr-name">${t.name}</div>
      <div class="tbr-score">${t.score.toLocaleString()}</div>
      <div class="award-badge">فائز +${G.selPts}</div>
    </div>`).join('');
}

function updateActiveQBox(){
  const q=G.activeQuestion;
  document.getElementById('aqText').textContent=q?q.text:'اختر سؤالاً من بنك الأسئلة أو تجاوز';
  const ansEl=document.getElementById('aqAnswer');
  ansEl.textContent=q?.answer?`الإجابة: ${q.answer}`:'';
  ansEl.classList.remove('show');
  document.getElementById('aqPts').textContent=q?`${q.pts} نقطة`:'';
  document.getElementById('displayQBtn').textContent=G.showQOnDisplay?'إخفاء من الشاشة':'إرسال للشاشة';
}
function toggleAnswer(){document.getElementById('aqAnswer').classList.toggle('show');}
function pickNextQuestion(){
  // gather all unused questions
  const pool=[];
  G.categories.forEach(cat=>cat.questions.forEach((q,qi)=>{if(!q.used)pool.push({catId:cat.id,qIdx:qi,...q});}));
  if(!pool.length){alert('لا توجد أسئلة غير مستخدمة');return;}
  const q=G.qOrder==='random'?pool[Math.floor(Math.random()*pool.length)]:pool[0];
  G.activeQuestion={...q};updateActiveQBox();pushToDisplay();
}
function toggleDisplayQ(){
  G.showQOnDisplay=!G.showQOnDisplay;
  document.getElementById('displayQBtn').textContent=G.showQOnDisplay?'إخفاء من الشاشة':'إرسال للشاشة';
  pushToDisplay();
}

function confirmAndNext(){
  if(G.selTeamIdx<0){alert('اختر الفريق الفائز بهذا السؤال');return;}
  stopTimer();
  // save for undo
  const snapshot={teamIdx:G.selTeamIdx,pts:G.selPts,q:G.currentQ,teamScore:G.teams[G.selTeamIdx].score,activeQ:G.activeQuestion?{...G.activeQuestion}:null};
  G.teams[G.selTeamIdx].score+=G.selPts;
  G.lastWinner=G.selTeamIdx;G.lastPts=G.selPts;
  G.questionLog.push({q:G.currentQ,teamName:G.teams[G.selTeamIdx].name,pts:G.selPts,_snap:snapshot});
  // mark question as used
  if(G.activeQuestion){
    const cat=G.categories.find(c=>c.id===G.activeQuestion.catId);
    if(cat&&cat.questions[G.activeQuestion.qIdx])cat.questions[G.activeQuestion.qIdx].used=true;
    G.activeQuestion=null;G.showQOnDisplay=false;
  }
  saveHistory();
  document.getElementById('flash').classList.add('on');setTimeout(()=>document.getElementById('flash').classList.remove('on'),400);
  spawnConfetti();
  goTo('liveScreen');setTimeout(renderLive,240);
}

function undoLast(){
  if(!G.questionLog.length)return;
  const last=G.questionLog.pop();
  const s=last._snap;
  G.teams[s.teamIdx].score=s.teamScore;
  G.currentQ=s.q;G.selTeamIdx=-1;G.lastWinner=-1;G.lastPts=0;
  if(s.activeQ){const cat=G.categories.find(c=>c.id===s.activeQ.catId);if(cat&&cat.questions[s.activeQ.qIdx])cat.questions[s.activeQ.qIdx].used=false;}
  cardEls={};renderScoring();saveHistory();
}

function renderLog(){
  const el=document.getElementById('historyLog');
  if(!G.questionLog.length){el.innerHTML='<div class="empty">لا يوجد سجل بعد</div>';return;}
  el.innerHTML=[...G.questionLog].reverse().map(r=>`
    <div class="log-item">
      <span class="log-q">س ${r.q}</span>
      <span class="log-winner">${r.teamName}</span>
      <span class="log-pts">+${r.pts}</span>
    </div>`).join('');
}

/* ═══════════════════════════════════════════
   LIVE BOARD (FLIP animation)
═══════════════════════════════════════════ */
function renderLive(){
  document.getElementById('liveName').textContent=G.title+(G.group?` — ${G.group}`:'');
  document.getElementById('liveMeta').innerHTML=`السؤال <b>${G.currentQ}</b>`;
  document.getElementById('liveFooter').innerHTML=`
    <button class="btn btn-grad" onclick="goNextFromLive()">السؤال التالي</button>
    <button class="btn btn-ghost" onclick="goHome()">الرئيسية</button>
    <button class="btn btn-ghost" onclick="showFinale()">إنهاء المسابقة</button>`;

  const sorted=[...G.teams].map((t,i)=>({...t,origIdx:i})).sort((a,b)=>b.score-a.score);
  const maxScore=Math.max(...sorted.map(t=>t.score),1);
  const wrap=document.getElementById('rankingsWrap');
  wrap.style.height=(sorted.length*(CARD_H+CARD_GAP)-CARD_GAP)+'px';

  const isFirst=Object.keys(cardEls).length!==G.teams.length;
  if(isFirst){
    wrap.innerHTML='';cardEls={};
    sorted.forEach((t,rank)=>{
      const el=buildCard(t,rank,maxScore);el.style.top=(rank*(CARD_H+CARD_GAP))+'px';
      wrap.appendChild(el);cardEls[t.origIdx]=el;
    });return;
  }
  const prevTops={};
  sorted.forEach(t=>{const el=cardEls[t.origIdx];if(el)prevTops[t.origIdx]=parseInt(el.style.top)||0;});
  sorted.forEach((t,rank)=>{const el=cardEls[t.origIdx];if(el)updateCard(el,t,rank,maxScore);});
  sorted.forEach(t=>{const el=cardEls[t.origIdx];if(!el)return;el.style.transition='none';el.style.top=(prevTops[t.origIdx]??0)+'px';});
  requestAnimationFrame(()=>requestAnimationFrame(()=>{
    sorted.forEach((t,rank)=>{
      const el=cardEls[t.origIdx];if(!el)return;
      el.style.transition='top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s';
      el.style.top=(rank*(CARD_H+CARD_GAP))+'px';
    });
  }));
  if(G.lastWinner>=0&&cardEls[G.lastWinner]){
    const el=cardEls[G.lastWinner];
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
function goNextFromLive(){
  G.currentQ++;G.selTeamIdx=-1;G.lastWinner=-1;G.lastPts=0;G.timerLeft=G.timerSecs;G.activeQuestion=null;G.showQOnDisplay=false;
  renderScoring();goTo('scoringScreen');
}

/* ═══════════════════════════════════════════
   FINALE
═══════════════════════════════════════════ */
function showFinale(){
  const sorted=[...G.teams].sort((a,b)=>b.score-a.score);
  document.getElementById('finaleWinner').textContent=sorted[0]?.name||'—';
  const p3=sorted.slice(0,3);
  const order=[1,0,2]; // silver,gold,bronze visual order
  document.getElementById('finalePodium').innerHTML=order.map(i=>{
    if(!p3[i])return '';
    const cls=['podium-2','podium-1','podium-3'][i];
    const medals=['🥈','🥇','🥉'][i];
    return `<div class="podium-item ${cls}"><div class="podium-rank">${i+1}</div><div class="podium-bar">${medals}</div><div class="podium-name">${p3[i].name}</div><div class="podium-score">${p3[i].score.toLocaleString()}</div></div>`;
  }).join('');
  saveHistory();spawnConfetti();goTo('finaleScreen');
}
function showSummary(){
  const el=document.getElementById('summarySection');
  el.style.display=el.style.display==='none'?'block':'none';
  document.getElementById('summaryTable').innerHTML=`
    <tr>${['المرتبة','الفريق','النقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>
    ${[...G.teams].sort((a,b)=>b.score-a.score).map((t,i)=>`<tr><td>${i+1}</td><td>${t.name}</td><td>${t.score.toLocaleString()}</td></tr>`).join('')}
    <tr><th colspan="3" style="padding-top:12px;">سجل الأسئلة</th></tr>
    <tr>${['رقم','الفائز','النقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>
    ${G.questionLog.map(r=>`<tr><td>س${r.q}</td><td>${r.teamName}</td><td>+${r.pts}</td></tr>`).join('')}`;
}

/* ═══════════════════════════════════════════
   SETTINGS MODAL (mid-game)
═══════════════════════════════════════════ */
let stTab=0;
function openSettingsModal(){
  stTab=0;settingsTab(0);
  document.getElementById('stCompTitle').value=G.title;
  document.getElementById('stCompGroup').value=G.group;
  renderStTeams();renderStPts();
  openModal('settingsModal');
}
function settingsTab(t){
  stTab=t;
  [0,1,2].forEach(i=>{document.getElementById('stPanel'+i).style.display=i===t?'block':'none';});
  document.querySelectorAll('.tab-btn').forEach((b,i)=>b.classList.toggle('active',i===t));
}
function renderStTeams(){
  document.getElementById('stTeamsList').innerHTML=G.teams.map((t,i)=>`
    <div style="display:flex;align-items:center;gap:8px;margin-bottom:7px;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:8px 12px;">
      <span style="flex:1;font-weight:700;">${t.name}</span>
      <span style="color:var(--gold);font-weight:900;">${t.score}</span>
      <button class="btn btn-sm btn-ghost" onclick="openEditScore(${i})">تعديل</button>
      <button class="btn btn-sm btn-rg" onclick="stDelTeam(${i})">حذف</button>
    </div>`).join('');
}
function stAddTeam(){
  const inp=document.getElementById('stTeamInput');const n=inp.value.trim();
  if(!n)return;G.teams.push({name:n,score:0});inp.value='';cardEls={};renderStTeams();
}
function stDelTeam(i){G.teams.splice(i,1);cardEls={};renderStTeams();}
function openEditScore(i){
  editScoreTeamIdx=i;
  document.getElementById('esTeamName').textContent=G.teams[i].name;
  document.getElementById('esNewScore').value=G.teams[i].score;
  openModal('editScoreModal');
}
function saveEditScore(){
  const v=parseInt(document.getElementById('esNewScore').value);
  if(!isNaN(v)&&v>=0){G.teams[editScoreTeamIdx].score=v;cardEls={};}
  closeModal('editScoreModal');renderStTeams();
}
function renderStPts(){
  document.getElementById('stPtsTags').innerHTML=G.ptsOptions.map((p,i)=>`
    <div class="pts-tag">${p}<button onclick="stRemovePts(${i})">✕</button></div>`).join('');
}
function stAddPts(){const v=parseInt(document.getElementById('stPtsInput').value);if(!v||v<10)return;if(!G.ptsOptions.includes(v)){G.ptsOptions.push(v);G.ptsOptions.sort((a,b)=>a-b);}document.getElementById('stPtsInput').value='';renderStPts();}
function stRemovePts(i){if(G.ptsOptions.length<=1)return;G.ptsOptions.splice(i,1);renderStPts();}
function stResetPts(){G.ptsOptions=[100,200,300,400,500];renderStPts();}
function saveSettings(){
  const t=document.getElementById('stCompTitle').value.trim();
  if(t)G.title=t;G.group=document.getElementById('stCompGroup').value.trim();
  saveHistory();closeModal('settingsModal');renderScoring();
}

/* ═══════════════════════════════════════════
   AUDIENCE DISPLAY WINDOW
═══════════════════════════════════════════ */
function openDisplayWindow(){
  displayWindow=window.open('','_blank','width=1280,height=720');
  if(!displayWindow){alert('السماح بالنوافذ المنبثقة في المتصفح');return;}
  const dark=document.documentElement.getAttribute('data-theme')==='dark';
  writeDisplayWindow(dark);
}
function writeDisplayWindow(dark){
  if(!displayWindow||displayWindow.closed)return;
  const html=buildDisplayHTML(dark);
  displayWindow.document.open();displayWindow.document.write(html);displayWindow.document.close();
}
function buildDisplayHTML(dark){
  const sorted=[...G.teams].map((t,i)=>({...t,origIdx:i})).sort((a,b)=>b.score-a.score);
  const maxScore=Math.max(...sorted.map(t=>t.score),1);
  const bg=dark?'#0d0d14':'#f0f2f8';const s1=dark?'#17172a':'#ffffff';const textc=dark?'#eef0ff':'#1a1a2e';
  const q=G.showQOnDisplay&&G.activeQuestion?G.activeQuestion:null;
  return `<!DOCTYPE html><html dir="rtl"><head><meta charset="UTF-8"><link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@700;900&family=Cairo:wght@700&display=swap" rel="stylesheet"><style>
*{margin:0;padding:0;box-sizing:border-box;}body{font-family:'Cairo',sans-serif;background:${bg};color:${textc};min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:30px;}
h1{font-family:'Tajawal',sans-serif;font-size:2.8rem;font-weight:900;background:linear-gradient(135deg,#4f46e5,#7c3aed);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:8px;}
.meta{color:#8888aa;font-size:1rem;margin-bottom:30px;}
.q-box{background:${s1};border:2px solid rgba(79,70,229,.2);border-radius:20px;padding:24px 32px;max-width:800px;width:100%;text-align:center;margin-bottom:28px;box-shadow:0 4px 24px rgba(79,70,229,.12);}
.q-txt{font-family:'Tajawal',sans-serif;font-size:1.7rem;font-weight:700;line-height:1.6;}
.timer{font-family:'Tajawal',sans-serif;font-size:4rem;font-weight:900;color:#4f46e5;margin-bottom:28px;}
.ranks{width:100%;max-width:760px;display:flex;flex-direction:column;gap:10px;}
.rc{display:flex;align-items:center;gap:14px;background:${s1};border:1.5px solid rgba(79,70,229,.12);border-radius:16px;padding:14px 20px;position:relative;overflow:hidden;}
.rc-1{border-color:rgba(217,119,6,.4);background:${dark?'rgba(245,200,66,.06)':'#fffbeb'};}
.med{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:900;flex-shrink:0;}
.m1{background:linear-gradient(135deg,#fde68a,#d97706);color:#fff;}.m2{background:linear-gradient(135deg,#e5e7eb,#9ca3af);color:#fff;}.m3{background:linear-gradient(135deg,#fcd34d,#92400e);color:#fff;}.mo{background:#e5e7eb;color:#888;}
.rn{flex:1;font-family:'Tajawal',sans-serif;font-size:1.3rem;font-weight:700;}.rs{font-family:'Tajawal',sans-serif;font-size:1.6rem;font-weight:900;color:#4f46e5;}
.rc-1 .rs{color:#d97706;}
.bar{position:absolute;bottom:0;right:0;left:0;height:4px;background:rgba(79,70,229,.06);}
.barf{height:100%;background:linear-gradient(90deg,#06b6d4,#4f46e5,#7c3aed);}
</style></head><body>
<h1>${G.title}</h1>
<div class="meta">${G.group?G.group+' · ':''} السؤال ${G.currentQ} · المؤقت: ${fmt(G.timerLeft)}</div>
${q?`<div class="q-box"><div class="q-txt">${q.text}</div></div>`:''}
<div class="ranks">
${sorted.map((t,r)=>{const mc=['m1','m2','m3','mo'][Math.min(r,3)];const rc=r<3?'rc-'+( r+1):'';const pct=(t.score/maxScore*100).toFixed(1);return`<div class="rc ${rc}"><div class="med ${mc}">${r+1}</div><div class="rn">${t.name}</div><div class="rs">${t.score.toLocaleString()}</div><div class="bar"><div class="barf" style="width:${pct}%"></div></div></div>`}).join('')}
</div></body></html>`;
}
function pushToDisplay(){
  if(!displayWindow||displayWindow.closed)return;
  const dark=document.documentElement.getAttribute('data-theme')==='dark';
  writeDisplayWindow(dark);
}

/* ═══════════════════════════════════════════
   NAVIGATION / MODALS
═══════════════════════════════════════════ */
function goTo(id){
  const f=document.getElementById('pageFade');f.classList.add('show');
  setTimeout(()=>{document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));document.getElementById(id).classList.add('active');f.classList.remove('show');},220);
}
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}

/* ═══════════════════════════════════════════
   CONFETTI
═══════════════════════════════════════════ */
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

/* ═══════════════════════════════════════════
   INIT
═══════════════════════════════════════════ */
renderSiteName();renderHistList();
</script>
</body>
</html>
