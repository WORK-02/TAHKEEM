
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>منصة المسابقات</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&family=Tajawal:wght@400;700;900&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#f0f2f8;--s1:#fff;--s2:#f4f5fb;--s3:#eceef6;
  --a1:#4f46e5;--a2:#7c3aed;--a3:#06b6d4;
  --green:#10b981;--orange:#f97316;--red:#ef4444;--gold:#d97706;
  --text:#1a1a2e;--text2:#3d3d5c;--muted:#8888aa;
  --border:rgba(79,70,229,.13);--sh:0 2px 14px rgba(79,70,229,.08);--sh2:0 6px 32px rgba(79,70,229,.14);
}
[data-theme=dark]{
  --bg:#0d0d14;--s1:#17172a;--s2:#1e1e32;--s3:#26263e;
  --border:rgba(99,102,241,.16);--text:#eef0ff;--text2:#b0b0d0;--muted:#6060a0;
  --sh:0 2px 14px rgba(0,0,0,.4);--sh2:0 6px 32px rgba(0,0,0,.5);
}
*{margin:0;padding:0;box-sizing:border-box;}
html,body{width:100%;min-height:100vh;}
body{font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);transition:background .3s,color .3s;}
.screen{display:none;width:100%;min-height:100vh;}
.screen.active{display:flex;flex-direction:column;}
.page-fade{position:fixed;inset:0;background:var(--bg);z-index:9999;opacity:0;pointer-events:none;transition:opacity .22s;}
.page-fade.show{opacity:1;pointer-events:all;}

/* REUSE */
.card{background:var(--s1);border:1px solid var(--border);border-radius:16px;padding:20px;margin-bottom:14px;box-shadow:var(--sh);}
.lbl{font-size:.74rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1.2px;margin-bottom:8px;}
input[type=text],input[type=number],input[type=password],textarea,select{width:100%;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;padding:10px 14px;color:var(--text);font-family:'Cairo',sans-serif;font-size:.93rem;transition:border-color .2s,box-shadow .2s;}
textarea{resize:vertical;min-height:70px;}
input:focus,textarea:focus,select:focus{outline:none;border-color:var(--a1);box-shadow:0 0 0 3px rgba(79,70,229,.12);}
.btn{padding:10px 20px;border:none;border-radius:11px;font-family:'Cairo',sans-serif;font-size:.92rem;font-weight:700;cursor:pointer;transition:all .15s;white-space:nowrap;}
.btn-a1{background:var(--a1);color:#fff;}
.btn-a1:hover{background:#4338ca;}
.btn-grad{background:linear-gradient(135deg,var(--a1),var(--a2));color:#fff;}
.btn-grad:hover{filter:brightness(1.07);}
.btn-green{background:var(--green);color:#fff;}
.btn-green:hover{filter:brightness(1.1);}
.btn-ghost{background:var(--s2);color:var(--text2);border:1.5px solid var(--border);}
.btn-ghost:hover{border-color:var(--a1);color:var(--a1);}
.btn-rg{background:rgba(239,68,68,.1);color:var(--red);border:1px solid rgba(239,68,68,.2);}
.btn-rg:hover{background:rgba(239,68,68,.2);}
.btn-orange{background:var(--orange);color:#fff;}
.btn-sm{padding:5px 11px;font-size:.8rem;border-radius:8px;}
.row{display:flex;gap:9px;}
.row input{flex:1;}
.empty{color:var(--muted);font-size:.86rem;text-align:center;padding:20px 0;}
.divider{border:none;border-top:1px solid var(--border);margin:14px 0;}
.badge{display:inline-flex;align-items:center;padding:3px 10px;border-radius:999px;font-size:.75rem;font-weight:700;}
.badge-orange{background:rgba(249,115,22,.12);color:var(--orange);}

/* NAV */
.top-nav{display:flex;align-items:center;justify-content:space-between;padding:13px 22px;background:var(--s1);border-bottom:1px solid var(--border);flex-wrap:wrap;gap:10px;position:sticky;top:0;z-index:100;box-shadow:0 1px 6px rgba(79,70,229,.06);}
.nav-brand{font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.nav-acts{display:flex;gap:7px;align-items:center;}
.icon-btn{width:34px;height:34px;border:1.5px solid var(--border);border-radius:9px;background:var(--s2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:.95rem;transition:all .15s;color:var(--text2);}
.icon-btn:hover{border-color:var(--a1);color:var(--a1);}
.pill{background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:4px 14px;font-size:.82rem;font-weight:700;color:var(--a1);}

/* MODAL */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.45);backdrop-filter:blur(6px);z-index:5000;display:none;align-items:center;justify-content:center;padding:20px;}
.modal-bg.open{display:flex;}
.modal-box{background:var(--s1);border:1px solid var(--border);border-radius:20px;padding:24px;width:100%;max-width:480px;box-shadow:var(--sh2);max-height:90vh;overflow-y:auto;}
.modal-title{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:900;margin-bottom:14px;}
.modal-acts{display:flex;gap:8px;margin-top:16px;justify-content:flex-end;}
.tab-bar{display:flex;background:var(--s2);border-radius:12px;padding:4px;margin-bottom:14px;}
.tab-btn{flex:1;padding:7px 10px;border:none;border-radius:9px;font-family:'Cairo',sans-serif;font-size:.82rem;font-weight:700;cursor:pointer;background:transparent;color:var(--muted);transition:all .15s;}
.tab-btn.active{background:var(--s1);color:var(--a1);box-shadow:var(--sh);}
.theme-row{display:flex;gap:7px;justify-content:center;}
.theme-chip{padding:6px 16px;border-radius:999px;font-size:.82rem;font-weight:700;border:1.5px solid var(--border);background:var(--s1);color:var(--muted);cursor:pointer;transition:all .15s;}
.theme-chip.active{background:var(--a1);color:#fff;border-color:var(--a1);}

/* ══ HOME ══ */
#homeScreen{background:var(--bg);}
.home-hero{width:100%;padding:48px 20px 32px;text-align:center;background:linear-gradient(160deg,rgba(79,70,229,.09) 0%,rgba(124,58,237,.05) 50%,transparent 100%);border-bottom:1px solid var(--border);}
.site-name{font-family:'Tajawal',sans-serif;font-size:2.6rem;font-weight:900;background:linear-gradient(135deg,var(--a1) 20%,var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:6px;line-height:1.1;}
.site-sub{color:var(--muted);font-size:.9rem;margin-bottom:24px;}
.portals{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;padding:24px 20px;max-width:760px;margin:0 auto;width:100%;}
@media(max-width:520px){.portals{grid-template-columns:1fr;}}
.portal-card{background:var(--s1);border:1.5px solid var(--border);border-radius:20px;padding:22px;cursor:pointer;transition:all .2s;box-shadow:var(--sh);display:flex;flex-direction:column;gap:9px;}
.portal-card:hover{border-color:var(--a1);box-shadow:var(--sh2);transform:translateY(-2px);}
.portal-icon{width:50px;height:50px;border-radius:14px;display:flex;align-items:center;justify-content:center;font-size:1.4rem;}
.pi-j{background:linear-gradient(135deg,var(--a1),var(--a2));}
.pi-p{background:linear-gradient(135deg,var(--green),#059669);}
.pi-d{background:linear-gradient(135deg,var(--orange),#ea580c);}
.pi-b{background:linear-gradient(135deg,var(--a3),#0284c7);}
.pi-a{background:linear-gradient(135deg,#6366f1,#4338ca);}
.portal-title{font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:900;}
.portal-desc{font-size:.78rem;color:var(--muted);line-height:1.5;}
.home-stats{display:flex;gap:10px;padding:0 20px 20px;max-width:760px;width:100%;margin:0 auto;flex-wrap:wrap;}
.stat-c{flex:1;min-width:90px;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:12px;text-align:center;box-shadow:var(--sh);}
.stat-n{font-family:'Tajawal',sans-serif;font-size:1.7rem;font-weight:900;color:var(--a1);}
.stat-l{font-size:.7rem;color:var(--muted);font-weight:700;}

/* ══ PIN ══ */
#pinScreen{align-items:center;justify-content:center;background:var(--bg);}
.pin-box{background:var(--s1);border:1px solid var(--border);border-radius:24px;padding:34px;width:100%;max-width:360px;text-align:center;box-shadow:var(--sh2);}
.pin-icon{font-size:2.8rem;margin-bottom:10px;}
.pin-title{font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:900;margin-bottom:4px;}
.pin-sub{color:var(--muted);font-size:.84rem;margin-bottom:20px;}
.pin-dots{display:flex;gap:10px;justify-content:center;margin-bottom:16px;}
.pin-dot{width:14px;height:14px;border-radius:50%;border:2px solid var(--border);background:transparent;transition:all .2s;}
.pin-dot.on{background:var(--a1);border-color:var(--a1);}
.pin-err{color:var(--red);font-size:.83rem;min-height:18px;margin-bottom:10px;}
.pkpad{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;max-width:210px;margin:0 auto 14px;}
.pk{padding:14px;background:var(--s2);border:1.5px solid var(--border);border-radius:12px;font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:700;cursor:pointer;transition:all .13s;color:var(--text);}
.pk:hover{background:var(--a1);color:#fff;border-color:var(--a1);}
.pk.del{background:rgba(239,68,68,.07);color:var(--red);border-color:rgba(239,68,68,.15);}
.pk:active{transform:scale(.95);}

/* ══ SETUP ══ */
#setupScreen{background:var(--bg);}
.setup-body{flex:1;padding:18px 22px;max-width:600px;width:100%;margin:0 auto;}
.wsteps{display:flex;gap:0;margin-bottom:20px;position:relative;}
.wsteps::before{content:'';position:absolute;top:13px;right:26px;left:26px;height:2px;background:var(--border);z-index:0;}
.ws{flex:1;text-align:center;position:relative;z-index:1;}
.wdot{width:26px;height:26px;border-radius:50%;border:2px solid var(--border);background:var(--s1);display:flex;align-items:center;justify-content:center;margin:0 auto 3px;font-size:.76rem;font-weight:700;color:var(--muted);transition:all .3s;}
.ws.active .wdot{background:var(--a1);border-color:var(--a1);color:#fff;}
.ws.done .wdot{background:var(--green);border-color:var(--green);color:#fff;}
.wlbl{font-size:.68rem;color:var(--muted);font-weight:700;}
.ws.active .wlbl{color:var(--a1);}
.wp{display:none;}
.wp.active{display:block;}
.wn{display:flex;gap:9px;margin-top:14px;}
.wn .btn{flex:1;padding:12px;}
.pts-tags{display:flex;flex-wrap:wrap;gap:7px;margin-top:8px;}
.pts-tag{display:flex;align-items:center;gap:5px;background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:5px 12px;font-size:.86rem;font-weight:700;color:var(--a1);}
.pts-tag button{background:none;border:none;color:var(--muted);cursor:pointer;font-size:.86rem;}
.pts-tag button:hover{color:var(--red);}

/* ══ JUDGE ══ */
#judgeScreen{background:var(--bg);}
.jbody{flex:1;padding:16px 20px;max-width:700px;width:100%;margin:0 auto;}
/* timer */
.tbox{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:12px 16px;margin-bottom:13px;box-shadow:var(--sh);}
.tdisp{font-family:'Tajawal',sans-serif;font-size:2.2rem;font-weight:900;color:var(--a1);min-width:88px;text-align:center;letter-spacing:2px;transition:color .3s;}
.tdisp.urgent{color:var(--red);animation:blink .6s ease-in-out infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:.5;}}
.tpres{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:6px;}
.tpre{padding:5px 10px;background:var(--s2);border:1.5px solid var(--border);border-radius:7px;font-size:.78rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .13s;}
.tpre:hover{border-color:var(--a3);color:var(--a3);}
.tctrls{display:flex;gap:5px;}
.tbtn{width:32px;height:32px;border:1.5px solid var(--border);border-radius:8px;background:var(--s2);font-size:.88rem;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .13s;color:var(--text2);}
.tbtn:hover{border-color:var(--a1);color:var(--a1);}
.tbtn.on{background:var(--green);border-color:var(--green);color:#fff;}
/* active q */
.aqbox{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:13px 17px;margin-bottom:13px;box-shadow:var(--sh);}
.aqlbl{font-size:.7rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:4px;}
.aqtext{font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:700;line-height:1.6;}
.aqans{font-size:.86rem;color:var(--green);font-weight:700;margin-top:4px;display:none;}
.aqans.show{display:block;}
.aqpts{font-size:.76rem;color:var(--muted);margin-top:3px;}
.aqacts{display:flex;gap:6px;margin-top:8px;flex-wrap:wrap;}
/* pts chips */
.ptschips{display:flex;flex-wrap:wrap;gap:6px;margin:8px 0 14px;}
.ptsc{padding:6px 14px;background:var(--s1);border:1.5px solid var(--border);border-radius:9px;font-size:.88rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .13s;box-shadow:var(--sh);}
.ptsc:hover{border-color:var(--a1);color:var(--a1);}
.ptsc.sel{background:var(--a1);border-color:var(--a1);color:#fff;}
/* team rows */
.trow{display:flex;align-items:center;justify-content:space-between;background:var(--s1);border:1.5px solid var(--border);border-radius:13px;padding:11px 15px;margin-bottom:8px;cursor:pointer;transition:all .18s;gap:11px;box-shadow:var(--sh);}
.trow:hover{border-color:var(--a1);box-shadow:var(--sh2);}
.trow.winner{border-color:var(--green);background:rgba(16,185,129,.06);box-shadow:0 4px 18px rgba(16,185,129,.14);}
.trname{font-family:'Tajawal',sans-serif;font-size:1rem;font-weight:700;flex:1;}
.trscore{font-family:'Tajawal',sans-serif;font-size:1.15rem;font-weight:900;color:var(--gold);}
.awbadge{padding:4px 10px;background:var(--green);color:#fff;border-radius:7px;font-size:.78rem;font-weight:700;opacity:0;transition:opacity .2s;}
.trow.winner .awbadge{opacity:1;}
.actbar{margin-top:11px;padding:12px 15px;background:var(--s1);border:1px solid var(--border);border-radius:13px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:9px;box-shadow:var(--sh);}
.logwrap{max-height:150px;overflow-y:auto;margin-top:10px;}
.logitem{display:flex;align-items:center;justify-content:space-between;padding:6px 11px;background:var(--s2);border-radius:8px;margin-bottom:5px;font-size:.8rem;}
.logq{color:var(--muted);}
.logw{font-weight:700;}
.logp{color:var(--green);font-weight:900;}

/* ══ PLAYER & DISPLAY shared board ══ */
.comp-name-big{font-family:'Tajawal',sans-serif;font-size:2rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-align:center;margin-bottom:6px;}
.meta-pill{display:inline-flex;gap:7px;align-items:center;background:var(--s1);border:1.5px solid var(--border);border-radius:999px;padding:6px 18px;font-size:.85rem;font-weight:700;color:var(--muted);box-shadow:var(--sh);}
.meta-pill b{color:var(--a1);}
.qshowbox{background:var(--s1);border:2px solid rgba(79,70,229,.15);border-radius:16px;padding:18px 22px;margin-bottom:20px;box-shadow:var(--sh2);text-align:center;display:none;}
.qshowbox.show{display:block;}
.qshowtext{font-family:'Tajawal',sans-serif;font-size:1.25rem;font-weight:700;line-height:1.6;}
.qshowtimer{font-family:'Tajawal',sans-serif;font-size:3rem;font-weight:900;color:var(--a1);margin-top:8px;transition:color .3s;}
.qshowtimer.urgent{color:var(--red);}
.rwrap{width:100%;position:relative;}
.rank-card{position:absolute;left:0;width:100%;display:flex;align-items:center;gap:13px;background:var(--s1);border:1.5px solid var(--border);border-radius:16px;padding:14px 18px;overflow:hidden;box-shadow:var(--sh);transition:top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s;}
.rank-card.rank-1{border-color:rgba(217,119,6,.4);background:linear-gradient(135deg,#fffbeb,#fef3c7 60%,var(--s1));}
.rank-card.rank-2{border-color:rgba(107,114,128,.25);}
.rank-card.rank-3{border-color:rgba(146,64,14,.25);}
.rank-card.just-scored{border-color:var(--green)!important;box-shadow:0 0 0 3px rgba(16,185,129,.14),var(--sh2)!important;}
.rmed{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Tajawal',sans-serif;font-size:1.15rem;font-weight:900;flex-shrink:0;}
.rank-1 .rmed{background:linear-gradient(135deg,#fde68a,#d97706);color:#fff;}
.rank-2 .rmed{background:linear-gradient(135deg,#e5e7eb,#9ca3af);color:#fff;}
.rank-3 .rmed{background:linear-gradient(135deg,#fcd34d,#92400e);color:#fff;}
.rank-other .rmed{background:var(--s3);color:var(--muted);font-size:.95rem;}
.rname{flex:1;font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:700;}
.rscore{font-family:'Tajawal',sans-serif;font-size:1.5rem;font-weight:900;color:var(--a1);min-width:78px;text-align:left;}
.rank-1 .rscore{color:var(--gold);}
.sbt{position:absolute;bottom:0;right:0;left:0;height:4px;background:rgba(79,70,229,.06);}
.sbf{height:100%;background:linear-gradient(90deg,var(--a3),var(--a1),var(--a2));transition:width .85s cubic-bezier(.4,0,.2,1);border-radius:0 0 0 16px;}
.fpts{position:absolute;font-family:'Tajawal',sans-serif;font-size:1.4rem;font-weight:900;color:var(--green);pointer-events:none;text-shadow:0 2px 8px rgba(16,185,129,.3);animation:fpu 1.2s ease-out forwards;right:88px;top:5px;z-index:20;}
@keyframes fpu{0%{opacity:1;transform:translateY(0) scale(.9);}30%{opacity:1;transform:translateY(-12px) scale(1.2);}100%{opacity:0;transform:translateY(-50px) scale(.85);}}

/* ══ PLAYER SCREEN ══ */
#playerScreen{background:var(--bg);align-items:center;}
.player-body{width:100%;max-width:720px;padding:24px 18px 40px;}
/* question history for player */
.qhist-item{background:var(--s1);border:1px solid var(--border);border-radius:12px;padding:12px 16px;margin-bottom:8px;box-shadow:var(--sh);}
.qhist-q{font-size:.9rem;font-weight:700;margin-bottom:4px;}
.qhist-meta{font-size:.76rem;color:var(--muted);}
.qhist-winner{color:var(--green);font-weight:700;}

/* ══ DISPLAY SCREEN (big) ══ */
#displayScreen{
  background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.12) 0%,transparent 58%),var(--bg);
  align-items:center;
  padding:24px 20px 36px;
}
.disp-wrap{width:100%;max-width:900px;display:flex;flex-direction:column;align-items:center;}
.disp-name{font-family:'Tajawal',sans-serif;font-size:3rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-align:center;margin-bottom:10px;}
.disp-qbox{background:var(--s1);border:2px solid rgba(79,70,229,.18);border-radius:20px;padding:22px 28px;margin-bottom:22px;box-shadow:var(--sh2);text-align:center;display:none;width:100%;}
.disp-qbox.show{display:block;}
.disp-qtext{font-family:'Tajawal',sans-serif;font-size:1.7rem;font-weight:700;line-height:1.6;}
.disp-timer{font-family:'Tajawal',sans-serif;font-size:5rem;font-weight:900;color:var(--a1);margin-top:8px;transition:color .3s;line-height:1;}
.disp-timer.urgent{color:var(--red);animation:blink .6s ease-in-out infinite;}
.disp-rwrap{width:100%;position:relative;}

/* ══ BANK ══ */
#bankScreen{background:var(--bg);}
.bankbody{flex:1;padding:16px 20px;max-width:820px;width:100%;margin:0 auto;}
.catbox{background:var(--s1);border:1px solid var(--border);border-radius:15px;margin-bottom:11px;box-shadow:var(--sh);overflow:hidden;}
.cathdr{display:flex;align-items:center;justify-content:space-between;padding:13px 17px;cursor:pointer;gap:9px;transition:background .15s;}
.cathdr:hover{background:var(--s2);}
.cattitle{font-family:'Tajawal',sans-serif;font-size:.97rem;font-weight:900;flex:1;}
.catmeta{font-size:.74rem;color:var(--muted);}
.catarrow{transition:transform .25s;color:var(--muted);font-size:.85rem;}
.catbox.open .catarrow{transform:rotate(90deg);}
.catbody{display:none;padding:0 15px 13px;}
.catbox.open .catbody{display:block;}
.qitem{display:flex;align-items:flex-start;gap:9px;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:9px 12px;margin-bottom:6px;}
.qitxt{flex:1;}
.qitext{font-size:.88rem;font-weight:600;line-height:1.5;}
.qians{font-size:.77rem;color:var(--green);margin-top:2px;font-weight:700;}
.qipts{font-size:.72rem;color:var(--muted);margin-top:2px;}
.qused{opacity:.42;}
.qpending{border-color:rgba(249,115,22,.3);background:rgba(249,115,22,.04);}
.addrow{display:flex;gap:7px;margin-top:9px;flex-wrap:wrap;}
.addrow input{flex:1;min-width:110px;}

/* ══ LIVE / FINALE ══ */
#liveScreen{align-items:center;padding:26px 18px 40px;background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.1) 0%,transparent 58%),var(--bg);}
.live-head{width:100%;max-width:720px;text-align:center;margin-bottom:24px;}
.live-name{font-family:'Tajawal',sans-serif;font-size:2.2rem;font-weight:900;background:linear-gradient(135deg,var(--a1) 20%,var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:8px;line-height:1.2;}
.live-rw{width:100%;max-width:720px;position:relative;}
.live-footer{width:100%;max-width:720px;margin-top:20px;display:flex;gap:8px;flex-wrap:wrap;}
.live-footer .btn{flex:1;padding:11px;font-size:.94rem;}
#finaleScreen{align-items:center;justify-content:center;padding:36px 18px;background:radial-gradient(ellipse 90% 60% at 50% 0%,rgba(79,70,229,.14) 0%,transparent 65%),var(--bg);}
.fwrap{width:100%;max-width:620px;text-align:center;}
.ftrophy{font-size:4.5rem;margin-bottom:10px;animation:tB .8s ease-out;}
@keyframes tB{0%{transform:scale(.5) translateY(30px);opacity:0;}70%{transform:scale(1.15) translateY(-10px);}100%{transform:scale(1) translateY(0);opacity:1;}}
.fwinner{font-family:'Tajawal',sans-serif;font-size:2.4rem;font-weight:900;background:linear-gradient(135deg,var(--gold),var(--orange));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:20px;}
.podium{display:flex;align-items:flex-end;justify-content:center;gap:9px;margin:20px 0 26px;}
.podium-item{display:flex;flex-direction:column;align-items:center;gap:4px;}
.pbar{width:68px;border-radius:7px 7px 0 0;display:flex;align-items:center;justify-content:center;font-size:1.4rem;}
.p1 .pbar{height:86px;background:linear-gradient(180deg,#fde68a,#d97706);}
.p2 .pbar{height:58px;background:linear-gradient(180deg,#e5e7eb,#9ca3af);}
.p3 .pbar{height:43px;background:linear-gradient(180deg,#fcd34d,#92400e);}
.pname{font-family:'Tajawal',sans-serif;font-weight:700;font-size:.86rem;max-width:82px;text-align:center;}
.pscore{font-size:.79rem;color:var(--gold);font-weight:900;}
.facts{display:flex;gap:9px;justify-content:center;flex-wrap:wrap;}
.smtable{width:100%;border-collapse:collapse;margin-top:14px;text-align:right;}
.smtable th{font-size:.73rem;font-weight:700;color:var(--muted);padding:7px 11px;border-bottom:1px solid var(--border);text-transform:uppercase;}
.smtable td{padding:7px 11px;border-bottom:1px solid var(--border);font-size:.85rem;}
.smtable tr:last-child td{border:none;}

/* PARTICLES / FLASH */
.particles{position:fixed;inset:0;pointer-events:none;z-index:999;}
.prt{position:absolute;border-radius:3px;animation:pfall linear forwards;}
@keyframes pfall{0%{transform:translateY(-10px) rotate(0deg);opacity:1;}100%{transform:translateY(110vh) rotate(700deg);opacity:0;}}
.flash-el{position:fixed;inset:0;pointer-events:none;z-index:998;opacity:0;background:rgba(16,185,129,.08);transition:opacity .15s;}
.flash-el.on{opacity:1;}
::-webkit-scrollbar{width:5px;height:5px;}
::-webkit-scrollbar-thumb{background:var(--border);border-radius:3px;}
@media(max-width:600px){
  .live-name,.disp-name{font-size:1.7rem;}.rname{font-size:.95rem;}.rscore{font-size:1.25rem;}
  .jbody,.bankbody,.setup-body{padding:12px;}
}
</style>
</head>
<body>
<div class="particles" id="particles"></div>
<div class="flash-el" id="flash"></div>
<div class="page-fade" id="pageFade"></div>

<!-- ══ HOME ══ -->
<div class="screen active" id="homeScreen">
  <div class="home-hero">
    <div class="site-name" id="siteNameEl">منصة المسابقات</div>
    <div class="site-sub">اختر القسم المناسب</div>
    <div class="theme-row">
      <div class="theme-chip" data-mode="light" onclick="setTheme('light')">فاتح</div>
      <div class="theme-chip" data-mode="auto" onclick="setTheme('auto')">تلقائي</div>
      <div class="theme-chip" data-mode="dark" onclick="setTheme('dark')">داكن</div>
    </div>
  </div>
  <div class="home-stats" id="homeStats"></div>
  <div class="portals">
    <div class="portal-card" onclick="enterPortal('judge')">
      <div class="portal-icon pi-j">⚖️</div>
      <div class="portal-title">قسم المحكمين</div>
      <div class="portal-desc">إدارة كاملة — تسجيل النتائج، المؤقت، التحكم الكامل</div>
    </div>
    <div class="portal-card" onclick="enterPortal('player')">
      <div class="portal-icon pi-p">🏅</div>
      <div class="portal-title">قسم المتسابقين</div>
      <div class="portal-desc">أدخل رقم المسابقة لمتابعة النتائج الحية والأسئلة</div>
    </div>
    <div class="portal-card" onclick="enterPortal('display')">
      <div class="portal-icon pi-d">📺</div>
      <div class="portal-title">شاشة العرض</div>
      <div class="portal-desc">للشاشة الكبيرة — ترتيب ومؤقت وسؤال بخط كبير</div>
    </div>
    <div class="portal-card" onclick="enterPortal('bank')">
      <div class="portal-icon pi-b">📚</div>
      <div class="portal-title">بنك الأسئلة العام</div>
      <div class="portal-desc">استعراض الأسئلة واقتراح أسئلة جديدة للمحكم</div>
    </div>
    <div class="portal-card" onclick="enterPortal('admin')">
      <div class="portal-icon pi-a">🛡️</div>
      <div class="portal-title">لوحة المشرف</div>
      <div class="portal-desc">إعدادات الموقع، الرموز السرية، المسابقات المحفوظة</div>
    </div>
  </div>
</div>

<!-- ══ PIN ══ -->
<div class="screen" id="pinScreen">
  <div style="position:absolute;top:16px;right:16px;">
    <button class="btn btn-ghost btn-sm" onclick="goHome()">رجوع</button>
  </div>
  <div class="pin-box">
    <div class="pin-icon" id="pinIcon">🔐</div>
    <div class="pin-title" id="pinTitle">أدخل الرمز السري</div>
    <div class="pin-sub" id="pinSub">هذا القسم محمي برمز سري</div>
    <div class="pin-dots" id="pinDots">
      <div class="pin-dot" id="pd0"></div><div class="pin-dot" id="pd1"></div>
      <div class="pin-dot" id="pd2"></div><div class="pin-dot" id="pd3"></div>
      <div class="pin-dot" id="pd4"></div><div class="pin-dot" id="pd5"></div>
    </div>
    <div class="pin-err" id="pinErr"></div>
    <div class="pkpad">
      <div class="pk" onclick="pinKey('1')">1</div><div class="pk" onclick="pinKey('2')">2</div><div class="pk" onclick="pinKey('3')">3</div>
      <div class="pk" onclick="pinKey('4')">4</div><div class="pk" onclick="pinKey('5')">5</div><div class="pk" onclick="pinKey('6')">6</div>
      <div class="pk" onclick="pinKey('7')">7</div><div class="pk" onclick="pinKey('8')">8</div><div class="pk" onclick="pinKey('9')">9</div>
      <div class="pk" onclick="pinKey('0')" style="grid-column:2;">0</div><div class="pk del" onclick="pinKey('del')">⌫</div>
    </div>
    <button class="btn btn-grad" style="width:100%;" onclick="checkPin()">دخول</button>
  </div>
</div>

<!-- ══ PLAYER PIN ENTRY ══ -->
<div class="screen" id="playerPinScreen">
  <div class="top-nav">
    <div class="nav-brand">قسم المتسابقين</div>
    <div class="nav-acts"><div class="icon-btn" onclick="goHome()">⌂</div></div>
  </div>
  <div style="flex:1;display:flex;align-items:center;justify-content:center;padding:20px;">
    <div style="width:100%;max-width:400px;">
      <div class="card" style="text-align:center;">
        <div style="font-size:2.2rem;margin-bottom:10px;">🏅</div>
        <div class="pin-title" style="font-size:1.2rem;margin-bottom:6px;">أدخل رقم المسابقة</div>
        <div style="color:var(--muted);font-size:.86rem;margin-bottom:18px;">احصل على الرقم من المحكم</div>
        <input type="password" id="playerCompPin" placeholder="رقم المسابقة" maxlength="6" style="text-align:center;font-size:1.4rem;letter-spacing:6px;margin-bottom:12px;" autocomplete="off">
        <div style="color:var(--red);font-size:.83rem;min-height:18px;margin-bottom:10px;" id="playerPinErr"></div>
        <button class="btn btn-grad" style="width:100%;" onclick="playerLogin()">دخول</button>
      </div>
    </div>
  </div>
</div>

<!-- ══ SETUP ══ -->
<div class="screen" id="setupScreen">
  <div class="top-nav">
    <div class="nav-brand" id="setupBrand">مسابقة جديدة</div>
    <div class="nav-acts"><div class="icon-btn" onclick="goHome()">✕</div></div>
  </div>
  <div class="setup-body">
    <div class="wsteps">
      <div class="ws active" id="ws0"><div class="wdot">1</div><div class="wlbl">الهوية</div></div>
      <div class="ws" id="ws1"><div class="wdot">2</div><div class="wlbl">الفرق</div></div>
      <div class="ws" id="ws2"><div class="wdot">3</div><div class="wlbl">النقاط</div></div>
      <div class="ws" id="ws3"><div class="wdot">4</div><div class="wlbl">الرمز</div></div>
    </div>
    <!-- step 0 -->
    <div class="wp active" id="wp0">
      <div class="card">
        <div class="lbl">اسم المسابقة</div>
        <input type="text" id="setupTitle" placeholder="مثال: مسابقة الثقافة العامة" style="margin-bottom:10px;">
        <div class="lbl">اسم المجموعة (اختياري)</div>
        <input type="text" id="setupGroup" placeholder="مثال: طلاب الفصل الثالث" style="margin-bottom:10px;">
        <div class="lbl">ترتيب الأسئلة</div>
        <div style="display:flex;gap:8px;">
          <label style="flex:1;display:flex;align-items:center;gap:7px;background:var(--s2);border:1.5px solid var(--border);border-radius:10px;padding:10px 12px;cursor:pointer;"><input type="radio" name="qord" value="ordered" checked style="width:auto;"> مرتب</label>
          <label style="flex:1;display:flex;align-items:center;gap:7px;background:var(--s2);border:1.5px solid var(--border);border-radius:10px;padding:10px 12px;cursor:pointer;"><input type="radio" name="qord" value="random" style="width:auto;"> عشوائي</label>
        </div>
      </div>
      <div class="wn"><button class="btn btn-ghost" onclick="goHome()">إلغاء</button><button class="btn btn-grad" onclick="wizNext(0)">التالي ←</button></div>
    </div>
    <!-- step 1 -->
    <div class="wp" id="wp1">
      <div class="card">
        <div class="lbl">اضافة فريق</div>
        <div class="row"><input type="text" id="teamInp" placeholder="اسم الفريق" onkeydown="if(event.key==='Enter')addTeam()"><button class="btn btn-a1" onclick="addTeam()">اضافة</button></div>
        <div id="teamsList" style="margin-top:10px;"><div class="empty">لا توجد فرق</div></div>
      </div>
      <div class="wn"><button class="btn btn-ghost" onclick="wizPrev(1)">→ السابق</button><button class="btn btn-grad" onclick="wizNext(1)">التالي ←</button></div>
    </div>
    <!-- step 2 -->
    <div class="wp" id="wp2">
      <div class="card">
        <div class="lbl">فئات النقاط</div>
        <div class="pts-tags" id="ptsTagWrap"></div>
        <div class="row" style="margin-top:9px;">
          <input type="number" id="ptsAddInp" placeholder="فئة جديدة" min="10" step="50" style="max-width:170px;">
          <button class="btn btn-ghost btn-sm" onclick="addPtsTag()" style="padding:10px 14px;">اضافة</button>
          <button class="btn btn-ghost btn-sm" onclick="resetPts()" style="padding:10px 12px;">افتراضي</button>
        </div>
      </div>
      <div class="wn"><button class="btn btn-ghost" onclick="wizPrev(2)">→ السابق</button><button class="btn btn-grad" onclick="wizNext(2)">التالي ←</button></div>
    </div>
    <!-- step 3 PIN -->
    <div class="wp" id="wp3">
      <div class="card">
        <div class="lbl">رمز سري للمسابقة (4-6 أرقام)</div>
        <p style="font-size:.83rem;color:var(--muted);margin-bottom:10px;">يُستخدم للدخول كمحكم ويُعطى للمتسابقين لمتابعة النتائج.</p>
        <input type="password" id="compPinInp" maxlength="6" placeholder="أدخل الرمز" style="text-align:center;font-size:1.3rem;letter-spacing:6px;margin-bottom:9px;" autocomplete="off">
        <input type="password" id="compPinConf" maxlength="6" placeholder="أعد الرمز" style="text-align:center;font-size:1.3rem;letter-spacing:6px;" autocomplete="off">
        <div style="font-size:.78rem;color:var(--muted);margin-top:7px;">اترك فارغاً للدخول بدون رمز</div>
      </div>
      <div class="wn"><button class="btn btn-ghost" onclick="wizPrev(3)">→ السابق</button><button class="btn btn-grad" onclick="setupDone()">بدء المسابقة ✓</button></div>
    </div>
  </div>
</div>

<!-- ══ JUDGE ══ -->
<div class="screen" id="judgeScreen">
  <div class="top-nav">
    <div class="nav-brand" id="judgeBrand">المسابقة</div>
    <div class="nav-acts">
      <div class="pill">س <span id="qNum">1</span></div>
      <div class="icon-btn" onclick="openBankFromJudge()" title="بنك الأسئلة">📚</div>
      <div class="icon-btn" onclick="openJudgeSettings()" title="الإعدادات">⚙</div>
      <div class="icon-btn" onclick="goHome()">⌂</div>
    </div>
  </div>
  <div class="jbody">
    <div class="tbox">
      <div class="tdisp" id="tdisp">00:30</div>
      <div>
        <div class="tpres">
          <div class="tpre" onclick="setTimer(10)">10ث</div><div class="tpre" onclick="setTimer(15)">15ث</div>
          <div class="tpre" onclick="setTimer(30)">30ث</div><div class="tpre" onclick="setTimer(60)">1د</div>
          <div class="tpre" onclick="setTimer(90)">90ث</div><div class="tpre" onclick="setTimer(120)">2د</div>
        </div>
        <div class="tctrls">
          <div class="tbtn" id="tplayBtn" onclick="toggleTimer()">▶</div>
          <div class="tbtn" onclick="resetTimer()">↺</div>
          <div class="tbtn" onclick="sendStateToBoards()" title="تحديث الشاشات">↑</div>
        </div>
      </div>
    </div>
    <div class="aqbox">
      <div class="aqlbl">السؤال الحالي</div>
      <div class="aqtext" id="aqtext">اختر سؤالاً أو تجاوز</div>
      <div class="aqans" id="aqans"></div>
      <div class="aqpts" id="aqpts"></div>
      <div class="aqacts">
        <button class="btn btn-ghost btn-sm" onclick="toggleAns()">إظهار الإجابة</button>
        <button class="btn btn-ghost btn-sm" onclick="pickQ()">سؤال من البنك</button>
        <button class="btn btn-ghost btn-sm" id="sendQBtn" onclick="toggleSendQ()">إرسال للشاشة</button>
      </div>
    </div>
    <div class="lbl">النقاط</div>
    <div class="ptschips" id="ptschips"></div>
    <div class="lbl">الفريق الفائز</div>
    <div id="teamBtns"></div>
    <div class="actbar">
      <button class="btn btn-ghost btn-sm" id="undoBtn" onclick="undoLast()" disabled>↩ تراجع</button>
      <div style="display:flex;gap:7px;flex-wrap:wrap;">
        <button class="btn btn-ghost btn-sm" onclick="showFinale()">إنهاء</button>
        <button class="btn btn-grad" onclick="confirmAndNext()">تسجيل وعرض اللوحة</button>
      </div>
    </div>
    <div style="margin-top:13px;"><div class="lbl">سجل الأسئلة</div><div class="logwrap" id="histLog"><div class="empty">لا يوجد بعد</div></div></div>
  </div>
</div>

<!-- ══ PLAYER (contestant board) ══ -->
<div class="screen" id="playerScreen">
  <div class="top-nav">
    <div class="nav-brand" id="playerBrand">المتسابقون</div>
    <div class="nav-acts">
      <div class="pill">س <span id="playerQNum">—</span></div>
      <div class="icon-btn" onclick="goTo('playerPinScreen')">↩</div>
      <div class="icon-btn" onclick="goHome()">⌂</div>
    </div>
  </div>
  <div class="player-body">
    <div class="comp-name-big" id="playerCompName">—</div>
    <div style="text-align:center;margin-bottom:16px;"><span class="meta-pill" id="playerMeta">—</span></div>
    <div class="qshowbox" id="playerQBox">
      <div class="qshowtext" id="playerQText"></div>
      <div class="qshowtimer" id="playerTimer">—</div>
    </div>
    <div class="rwrap" id="playerRankings"></div>
    <!-- question history shown after comp ends -->
    <div id="playerQHistory" style="margin-top:24px;display:none;">
      <div class="lbl" style="margin-bottom:10px;">سجل الأسئلة</div>
      <div id="playerQHistList"></div>
    </div>
  </div>
</div>

<!-- ══ DISPLAY (big screen) ══ -->
<div class="screen" id="displayScreen">
  <div class="top-nav" style="background:var(--s1);border-bottom:1px solid var(--border);">
    <div class="nav-brand" id="dispBrand">شاشة العرض</div>
    <div class="nav-acts">
      <div class="icon-btn" onclick="goHome()">⌂</div>
    </div>
  </div>
  <div style="flex:1;display:flex;align-items:center;justify-content:center;padding:20px 16px 32px;background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.12) 0%,transparent 58%),var(--bg);">
    <div class="disp-wrap">
      <div class="disp-name" id="dispName">—</div>
      <div style="text-align:center;margin-bottom:16px;"><span class="meta-pill">السؤال <b id="dispQ">—</b></span></div>
      <div class="disp-qbox" id="dispQBox">
        <div class="disp-qtext" id="dispQText">—</div>
        <div class="disp-timer" id="dispTimer">—</div>
      </div>
      <div class="disp-rwrap" id="dispRankings"></div>
    </div>
  </div>
</div>

<!-- ══ BANK ══ -->
<div class="screen" id="bankScreen">
  <div class="top-nav">
    <div class="nav-brand">بنك الأسئلة</div>
    <div class="nav-acts">
      <div class="icon-btn" id="bankAddCatBtn" onclick="addCategory()" style="display:none;" title="+تصنيف">+</div>
      <div class="icon-btn" id="bankAIBtn" onclick="openAIModal(null)" style="display:none;" title="AI">✦</div>
      <div class="icon-btn" onclick="returnFromBank()">←</div>
    </div>
  </div>
  <div class="bankbody">
    <div id="bankPending" style="display:none;">
      <div class="lbl" style="color:var(--orange);">بانتظار موافقة المشرف <span class="badge badge-orange" id="pendingCnt"></span></div>
      <div id="pendingList" style="margin-bottom:16px;"></div>
    </div>
    <div id="bankCats"><div class="empty">لا توجد تصنيفات</div></div>
  </div>
</div>

<!-- ══ LIVE ══ -->
<div class="screen" id="liveScreen">
  <div class="top-nav">
    <div class="nav-brand" id="liveBrand">النتائج</div>
    <div class="nav-acts">
      <div class="icon-btn" onclick="goTo('judgeScreen')" title="رجوع للمحكم">←</div>
      <div class="icon-btn" onclick="goHome()">⌂</div>
    </div>
  </div>
  <div style="flex:1;display:flex;flex-direction:column;align-items:center;padding:24px 18px 40px;background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.1) 0%,transparent 58%),var(--bg);">
    <div class="live-head">
      <div class="live-name" id="liveName">—</div>
      <div style="text-align:center;"><span class="meta-pill">السؤال <b id="liveQ">—</b></span></div>
    </div>
    <div class="live-rw" id="liveRankings"></div>
    <div class="live-footer" id="liveFooter"></div>
  </div>
</div>

<!-- ══ FINALE ══ -->
<div class="screen" id="finaleScreen">
  <div class="top-nav">
    <div class="nav-brand">نهاية المسابقة</div>
    <div class="nav-acts">
      <div class="icon-btn" onclick="goTo('judgeScreen');renderJudge();" title="رجوع للمحكم">←</div>
      <div class="icon-btn" onclick="goHome()">⌂</div>
    </div>
  </div>
  <div style="flex:1;display:flex;align-items:center;justify-content:center;padding:28px 18px 40px;background:radial-gradient(ellipse 90% 60% at 50% 0%,rgba(79,70,229,.14) 0%,transparent 65%),var(--bg);overflow-y:auto;">
  <div class="fwrap">
    <div class="ftrophy">🏆</div>
    <div style="color:var(--muted);font-size:1rem;font-weight:700;margin-bottom:3px;">الفائز</div>
    <div class="fwinner" id="finaleWinner">—</div>
    <div class="podium" id="finalePodium"></div>
    <div class="facts">
      <button class="btn btn-grad" onclick="goHome()">الرئيسية</button>
      <button class="btn btn-ghost" onclick="toggleSummary()">ملخص المسابقة</button>
    </div>
    <div id="summarySection" style="display:none;margin-top:18px;text-align:right;">
      <table class="smtable" id="summaryTable"></table>
    </div>
  </div>
</div>

<!-- ══ MODALS ══ -->
<!-- Admin -->
<div class="modal-bg" id="adminModal">
  <div class="modal-box">
    <div class="modal-title">🛡️ لوحة المشرف</div>
    <div class="tab-bar">
      <button class="tab-btn active" onclick="admTab(0)">الموقع</button>
      <button class="tab-btn" onclick="admTab(1)">المسابقات</button>
      <button class="tab-btn" onclick="admTab(2)">الرمز</button>
    </div>
    <div id="adm0">
      <div class="lbl">اسم الموقع</div>
      <input type="text" id="admSiteName" style="margin-bottom:10px;">
    </div>
    <div id="adm1" style="display:none;"><div id="admHistList"></div></div>
    <div id="adm2" style="display:none;">
      <p style="font-size:.86rem;color:var(--text2);margin-bottom:10px;">الرمز الافتراضي للمشرف: <b>1234</b></p>
      <div class="lbl">رمز المشرف الجديد (4-6 أرقام)</div>
      <input type="password" id="admNewPin" autocomplete="off">
    </div>
    <div class="modal-acts">
      <button class="btn btn-grad" onclick="saveAdmin()">حفظ</button>
      <button class="btn btn-ghost" onclick="closeModal('adminModal')">إغلاق</button>
    </div>
  </div>
</div>
<!-- Judge Settings -->
<div class="modal-bg" id="jsModal">
  <div class="modal-box">
    <div class="modal-title">⚙ إعدادات المسابقة</div>
    <div class="tab-bar">
      <button class="tab-btn active" onclick="jsTab(0)">الفرق</button>
      <button class="tab-btn" onclick="jsTab(1)">النقاط</button>
      <button class="tab-btn" onclick="jsTab(2)">المسابقة</button>
    </div>
    <div id="js0">
      <div class="row" style="margin-bottom:9px;"><input type="text" id="jsTeamInp" placeholder="فريق جديد" onkeydown="if(event.key==='Enter')jsAddTeam()"><button class="btn btn-a1" onclick="jsAddTeam()">اضافة</button></div>
      <div id="jsTeamsList"></div>
      <div class="divider"></div>
      <div class="lbl">تعديل النقاط</div>
      <div id="jsScoreEdit"></div>
    </div>
    <div id="js1" style="display:none;">
      <div class="pts-tags" id="jsPtsTags"></div>
      <div class="row" style="margin-top:9px;"><input type="number" id="jsPtsInp" placeholder="فئة جديدة" min="10" step="50" style="max-width:150px;"><button class="btn btn-ghost btn-sm" onclick="jsAddPts()" style="padding:10px 13px;">اضافة</button></div>
    </div>
    <div id="js2" style="display:none;">
      <div class="lbl">اسم المسابقة</div><input type="text" id="jsTitle" style="margin-bottom:9px;">
      <div class="lbl">اسم المجموعة</div><input type="text" id="jsGroup">
    </div>
    <div class="modal-acts"><button class="btn btn-grad" onclick="saveJS()">حفظ</button><button class="btn btn-ghost" onclick="closeModal('jsModal')">إغلاق</button></div>
  </div>
</div>
<!-- Edit Score -->
<div class="modal-bg" id="esModal">
  <div class="modal-box" style="max-width:320px;">
    <div class="modal-title">تعديل نقاط: <span id="esName"></span></div>
    <input type="number" id="esScore" min="0" style="text-align:center;font-size:1.3rem;">
    <div class="modal-acts"><button class="btn btn-grad" onclick="saveEditScore()">حفظ</button><button class="btn btn-ghost" onclick="closeModal('esModal')">إلغاء</button></div>
  </div>
</div>
<!-- AI -->
<div class="modal-bg" id="aiModal">
  <div class="modal-box" style="max-width:520px;">
    <div class="modal-title">✦ توليد أسئلة بالذكاء الاصطناعي</div>
    <div class="lbl">مزود AI</div>
    <select id="aiProv" style="margin-bottom:9px;" onchange="updateAIKeyHint()">
      <option value="gemini">Gemini (Google) — مجاني</option>
      <option value="openai">OpenAI (ChatGPT)</option>
    </select>
    <div class="lbl">API Key <span id="aiKeyHint" style="font-size:.73rem;color:var(--muted);"></span></div>
    <input type="password" id="aiKey" placeholder="الصق المفتاح هنا" style="margin-bottom:9px;" autocomplete="off">
    <div class="lbl">الموضوع</div>
    <input type="text" id="aiTopic" placeholder="مثال: تاريخ المملكة العربية السعودية" style="margin-bottom:9px;">
    <div style="display:flex;gap:8px;margin-bottom:10px;">
      <select id="aiCnt"><option value="3">3 أسئلة</option><option value="5" selected>5</option><option value="10">10</option></select>
      <select id="aiLang"><option value="ar">عربي</option><option value="en">English</option></select>
    </div>
    <button class="btn btn-grad" onclick="genAI()" id="aiGenBtn" style="width:100%;margin-bottom:10px;">توليد الأسئلة</button>
    <div id="aiResults"></div>
    <div class="modal-acts"><button class="btn btn-ghost" onclick="closeModal('aiModal')">إغلاق</button></div>
  </div>
</div>
<!-- Resume -->
<div class="modal-bg" id="resumeModal">
  <div class="modal-box" style="max-width:360px;">
    <div class="modal-title">استئناف مسابقة؟</div>
    <div id="resumeText" style="font-size:.9rem;color:var(--text2);"></div>
    <div class="modal-acts"><button class="btn btn-grad" onclick="doResume()">استئناف</button><button class="btn btn-ghost" onclick="closeModal('resumeModal');startNew()">مسابقة جديدة</button><button class="btn btn-ghost" onclick="closeModal('resumeModal')">إلغاء</button></div>
  </div>
</div>

<script>
/* ═══════════════ AUDIO ENGINE ═══════════════ */
const AC = new (window.AudioContext || window.webkitAudioContext)();
function playTone(freq, type, dur, vol=0.4, delay=0){
  const o=AC.createOscillator(), g=AC.createGain();
  o.connect(g); g.connect(AC.destination);
  o.type=type; o.frequency.setValueAtTime(freq, AC.currentTime+delay);
  g.gain.setValueAtTime(0, AC.currentTime+delay);
  g.gain.linearRampToValueAtTime(vol, AC.currentTime+delay+0.01);
  g.gain.exponentialRampToValueAtTime(0.001, AC.currentTime+delay+dur);
  o.start(AC.currentTime+delay); o.stop(AC.currentTime+delay+dur+0.05);
}
function soundStart(){
  // 3 rising beeps — "get ready"
  [0,0.35,0.7].forEach((d,i)=>playTone(440+i*110,'sine',0.18,0.5,d));
}
function soundTick(){playTone(880,'square',0.06,0.18);}
function soundUrgent(){playTone(660,'sawtooth',0.08,0.25);}
function soundEnd(){
  // descending + buzz
  playTone(600,'sine',0.15,0.5,0);
  playTone(400,'sine',0.15,0.5,0.18);
  playTone(200,'sawtooth',0.3,0.4,0.36);
}
function soundWin(){
  // fanfare
  [0,0.12,0.24,0.36].forEach((d,i)=>playTone([523,659,784,1047][i],'sine',0.22,0.5,d));
}
function resumeAC(){if(AC.state==='suspended')AC.resume();}

/* ═══════════════ STORAGE ═══════════════ */
const S={
  get:(k)=>{try{return JSON.parse(localStorage.getItem(k));}catch{return null;}},
  set:(k,v)=>localStorage.setItem(k,JSON.stringify(v))
};

/* ═══════════════ BUILTIN BANK ═══════════════ */
const BUILTIN=[
  {name:'ثقافة عامة',qs:[
    {t:'ما عاصمة المملكة العربية السعودية؟',a:'الرياض',p:100},
    {t:'كم عدد أيام الأسبوع؟',a:'7 أيام',p:100},
    {t:'ما أكبر كوكب في المجموعة الشمسية؟',a:'المشتري',p:200},
    {t:'ما أطول نهر في العالم؟',a:'نهر النيل',p:200},
    {t:'في أي سنة تأسست المملكة العربية السعودية؟',a:'1932م',p:300},
    {t:'ما الرمز الكيميائي للذهب؟',a:'Au',p:400},
    {t:'كم عدد الدول المعترف بها دولياً؟',a:'195 دولة',p:500},
  ]},
  {name:'علوم وتكنولوجيا',qs:[
    {t:'ما الوحدة الأساسية للمعلومات في الحاسوب؟',a:'البت (Bit)',p:100},
    {t:'من اخترع الهاتف؟',a:'ألكسندر غراهام بيل',p:200},
    {t:'ما الغاز الأكثر وفرة في الغلاف الجوي؟',a:'النيتروجين 78%',p:200},
    {t:'ما سرعة الضوء تقريباً؟',a:'300,000 كم/ثانية',p:300},
    {t:'ما معنى HTTP؟',a:'HyperText Transfer Protocol',p:400},
  ]},
  {name:'جغرافيا',qs:[
    {t:'ما أكبر قارة مساحةً؟',a:'آسيا',p:100},
    {t:'ما أعلى جبل في العالم؟',a:'إيفرست',p:100},
    {t:'ما أصغر دولة في العالم؟',a:'الفاتيكان',p:200},
    {t:'ما أكبر صحراء في العالم؟',a:'الصحراء الكبرى',p:300},
    {t:'أي دولة أكبر سكاناً؟',a:'الهند',p:200},
  ]},
  {name:'تاريخ',qs:[
    {t:'متى انتهت الحرب العالمية الثانية؟',a:'1945م',p:100},
    {t:'من أول إنسان على القمر؟',a:'نيل أرمسترونغ',p:200},
    {t:'في أي عام اكتشف كولومبوس أمريكا؟',a:'1492م',p:300},
    {t:'متى سقط جدار برلين؟',a:'1989م',p:300},
  ]},
];

/* ═══════════════ STATE ═══════════════ */
let G={
  id:null,title:'',group:'',qOrder:'ordered',
  teams:[],ptsOptions:[100,200,300,400,500],
  categories:[],
  currentQ:1,selPts:100,selTeamIdx:-1,
  lastWinner:-1,lastPts:0,
  questionLog:[],
  activeQuestion:null,showQOnDisplay:false,
  timerSecs:30,timerLeft:30,timerRunning:false,
  pin:'',finished:false,
};
const CELS={live:{},player:{},display:{}};
const CARD_H=76,CARD_GAP=11;
let timerInt=null;
let pinTarget='';
let pinEnteredVal='';
let bankFromJudge=false;
let aiTargetCatId=null;
let esIdx=-1;
let jsTabI=0;
let admTabI=0;

/* ═══════════════ THEME ═══════════════ */
let themeMode=S.get('themeMode')||'auto';
function applyTheme(){
  const dark=themeMode==='dark'||(themeMode==='auto'&&window.matchMedia('(prefers-color-scheme: dark)').matches);
  document.documentElement.setAttribute('data-theme',dark?'dark':'light');
  document.querySelectorAll('.theme-chip').forEach(c=>c.classList.toggle('active',c.dataset.mode===themeMode));
}
function setTheme(m){themeMode=m;S.set('themeMode',m);applyTheme();}
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change',applyTheme);
applyTheme();

/* ═══════════════ SITE NAME ═══════════════ */
function getSiteName(){return S.get('siteName')||'منصة المسابقات';}
function getAdminPin(){return S.get('adminPin')||'1234';}
function renderSiteName(){const n=getSiteName();document.getElementById('siteNameEl').textContent=n;document.title=n;}

/* ═══════════════ HISTORY ═══════════════ */
function getHistory(){return S.get('compHistory')||[];}
function saveHistory(){
  if(!G.title||!G.teams.length)return;
  let h=getHistory();
  const rec={id:G.id||Date.now(),title:G.title,group:G.group,qOrder:G.qOrder,
    teams:JSON.parse(JSON.stringify(G.teams)),ptsOptions:[...G.ptsOptions],
    categories:JSON.parse(JSON.stringify(G.categories)),
    questionLog:[...G.questionLog],
    currentQ:G.currentQ,selPts:G.selPts,pin:G.pin,finished:G.finished,savedAt:Date.now()};
  G.id=rec.id;
  const idx=h.findIndex(x=>x.id===rec.id);
  if(idx>=0)h[idx]=rec;else h.unshift(rec);
  h=h.slice(0,20);S.set('compHistory',h);
}
function delHistory(id){if(!confirm('حذف؟'))return;S.set('compHistory',getHistory().filter(x=>x.id!==id));renderHomeStats();renderAdmHist();}

function renderHomeStats(){
  const h=getHistory();
  const tqs=h.reduce((a,b)=>a+(b.categories?.reduce((x,c)=>x+c.questions.length,0)||0),0);
  document.getElementById('homeStats').innerHTML=`
    <div class="stat-c"><div class="stat-n">${h.length}</div><div class="stat-l">مسابقة</div></div>
    <div class="stat-c"><div class="stat-n">${h.reduce((a,b)=>a+(b.teams?.length||0),0)}</div><div class="stat-l">فريق</div></div>
    <div class="stat-c"><div class="stat-n">${h.reduce((a,b)=>a+(b.questionLog?.length||0),0)}</div><div class="stat-l">سؤال مجاب</div></div>
    <div class="stat-c"><div class="stat-n">${tqs}</div><div class="stat-l">في البنك</div></div>`;
}

/* ═══════════════ PORTAL ENTRY ═══════════════ */
function enterPortal(type){
  resumeAC();
  if(type==='judge'){
    const h=getHistory();
    if(G.id){renderJudge();goTo('judgeScreen');return;}
    if(h.length){
      const last=h[0];
      document.getElementById('resumeText').innerHTML=`<b>${last.title}</b><br>السؤال ${last.currentQ} · ${last.teams?.length} فرق`;
      document.getElementById('resumeModal')._lastId=last.id;
      openModal('resumeModal');
    }else{startNew();}
    return;
  }
  if(type==='player'){goTo('playerPinScreen');return;}
  if(type==='display'){
    if(!G.id&&!getHistory().length){alert('لا توجد مسابقة جارية');return;}
    if(!G.id){const h=getHistory();loadCompById(h[0].id);}
    goTo('displayScreen');
    setTimeout(()=>{renderDisplayBoard();},250);
    return;
  }
  if(type==='bank'){
    bankFromJudge=false;
    renderBank(false);
    document.getElementById('bankAddCatBtn').style.display='none';
    document.getElementById('bankAIBtn').style.display='none';
    goTo('bankScreen');return;
  }
  if(type==='admin'){
    pinTarget='admin';
    document.getElementById('pinIcon').textContent='🛡️';
    document.getElementById('pinTitle').textContent='لوحة المشرف';
    document.getElementById('pinSub').textContent='أدخل رمز المشرف';
    pinEnteredVal='';updatePinDots();
    document.getElementById('pinErr').textContent='';
    goTo('pinScreen');return;
  }
}

function doResume(){
  closeModal('resumeModal');
  const id=document.getElementById('resumeModal')._lastId;
  const rec=getHistory().find(x=>x.id===id);
  if(!rec)return;
  if(rec.pin){
    pinTarget='judgeResume';
    document.getElementById('pinIcon').textContent='⚖️';
    document.getElementById('pinTitle').textContent='رمز مسابقة: '+rec.title;
    document.getElementById('pinSub').textContent='أدخل الرمز للمتابعة';
    document.getElementById('resumeModal')._lastId=id;
    pinEnteredVal='';updatePinDots();
    document.getElementById('pinErr').textContent='';
    goTo('pinScreen');
  }else{
    loadCompById(id);renderJudge();goTo('judgeScreen');
  }
}

function loadCompById(id){
  const rec=getHistory().find(x=>x.id===id);if(!rec)return;
  G={...G,...rec,
    teams:JSON.parse(JSON.stringify(rec.teams)),
    categories:JSON.parse(JSON.stringify(rec.categories||[])),
    questionLog:[...(rec.questionLog||[])],
    ptsOptions:[...rec.ptsOptions],
    selTeamIdx:-1,lastWinner:-1,lastPts:0,
    timerSecs:30,timerLeft:30,timerRunning:false,
    activeQuestion:null,showQOnDisplay:false};
  Object.keys(CELS).forEach(k=>{Object.keys(CELS[k]).forEach(x=>delete CELS[k][x]);});
  initBank();
}

function initBank(){
  if(!G.categories||!G.categories.length){
    G.categories=BUILTIN.map(b=>({
      id:'b_'+b.name,name:b.name,
      questions:b.qs.map((q,i)=>({id:'bq'+i+'_'+b.name,text:q.t,answer:q.a,pts:q.p,used:false,approved:true}))
    }));
  }
}

/* ═══════════════ PIN SCREEN ═══════════════ */
function pinKey(v){
  resumeAC();
  playTone(660,'sine',0.05,0.15);
  if(v==='del'){pinEnteredVal=pinEnteredVal.slice(0,-1);}
  else if(pinEnteredVal.length<6){pinEnteredVal+=v;}
  updatePinDots();
  if(pinEnteredVal.length>=4)document.getElementById('pinErr').textContent='';
}
function updatePinDots(){
  for(let i=0;i<6;i++){
    document.getElementById('pd'+i).classList.toggle('on',i<pinEnteredVal.length);
  }
}
function checkPin(){
  const v=pinEnteredVal;
  const err=document.getElementById('pinErr');
  if(pinTarget==='admin'){
    if(v===getAdminPin()){
      document.getElementById('admSiteName').value=getSiteName();
      renderAdmHist();
      goTo('homeScreen');setTimeout(()=>openModal('adminModal'),300);
    }else{err.textContent='رمز خاطئ';playTone(200,'sawtooth',0.2,0.3);}
    return;
  }
  if(pinTarget==='judgeResume'){
    const id=document.getElementById('resumeModal')._lastId;
    const rec=getHistory().find(x=>x.id===id);
    if(rec&&rec.pin===v){loadCompById(id);renderJudge();goTo('judgeScreen');}
    else{err.textContent='رمز خاطئ';playTone(200,'sawtooth',0.2,0.3);}
    return;
  }
}

/* player PIN */
function playerLogin(){
  const v=document.getElementById('playerCompPin').value.trim();
  const err=document.getElementById('playerPinErr');
  err.textContent='';
  const h=getHistory();
  if(!h.length){err.textContent='لا توجد مسابقات محفوظة';return;}
  // find by pin match, or if no pin set use first comp
  let found=null;
  if(v===''){found=h.find(x=>!x.pin)||null;}
  else{found=h.find(x=>x.pin===v)||null;}
  if(!found){err.textContent='لم يتم العثور على مسابقة بهذا الرقم';return;}
  loadCompById(found.id);
  renderPlayerBoard();
  goTo('playerScreen');
  if(G.finished){showPlayerHistory();}
}

/* ═══════════════ SETUP ═══════════════ */
function startNew(){
  G={id:null,title:'',group:'',qOrder:'ordered',teams:[],ptsOptions:[100,200,300,400,500],categories:[],currentQ:1,selPts:100,selTeamIdx:-1,lastWinner:-1,lastPts:0,questionLog:[],activeQuestion:null,showQOnDisplay:false,timerSecs:30,timerLeft:30,timerRunning:false,pin:'',finished:false};
  Object.keys(CELS).forEach(k=>{Object.keys(CELS[k]).forEach(x=>delete CELS[k][x]);});
  renderWizard(0);goTo('setupScreen');
}
function renderWizard(s){
  for(let i=0;i<4;i++){
    document.getElementById('wp'+i).classList.toggle('active',i===s);
    const ws=document.getElementById('ws'+i);
    ws.classList.remove('active','done');
    if(i===s)ws.classList.add('active');else if(i<s)ws.classList.add('done');
  }
  if(s===1)renderSetupTeams();
  if(s===2)renderPtsTags();
}
function wizNext(s){
  if(s===0){const t=document.getElementById('setupTitle').value.trim();if(!t){alert('اكتب اسم المسابقة');return;}G.title=t;G.group=document.getElementById('setupGroup').value.trim();G.qOrder=document.querySelector('input[name=qord]:checked').value;}
  if(s===1&&!G.teams.length){alert('اضف فريقاً');return;}
  renderWizard(s+1);
}
function wizPrev(s){renderWizard(s-1);}
function renderSetupTeams(){
  const el=document.getElementById('teamsList');
  if(!G.teams.length){el.innerHTML='<div class="empty">لا توجد فرق</div>';return;}
  el.innerHTML=G.teams.map((t,i)=>`
    <div style="display:flex;align-items:center;justify-content:space-between;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:8px 12px;margin-bottom:6px;">
      <span style="font-weight:700;">${t.name}</span>
      <button class="btn btn-sm btn-rg" onclick="removeTeam(${i})">حذف</button>
    </div>`).join('');
}
function addTeam(){const inp=document.getElementById('teamInp');const n=inp.value.trim();if(!n)return;if(G.teams.find(t=>t.name===n)){inp.select();return;}G.teams.push({name:n,score:0});inp.value='';inp.focus();renderSetupTeams();}
function removeTeam(i){G.teams.splice(i,1);renderSetupTeams();}
function renderPtsTags(){document.getElementById('ptsTagWrap').innerHTML=G.ptsOptions.map((p,i)=>`<div class="pts-tag">${p}<button onclick="removePtsTag(${i})">✕</button></div>`).join('');}
function addPtsTag(){const v=parseInt(document.getElementById('ptsAddInp').value);if(!v||v<10)return;if(!G.ptsOptions.includes(v)){G.ptsOptions.push(v);G.ptsOptions.sort((a,b)=>a-b);}document.getElementById('ptsAddInp').value='';renderPtsTags();}
function removePtsTag(i){if(G.ptsOptions.length<=1)return;G.ptsOptions.splice(i,1);renderPtsTags();}
function resetPts(){G.ptsOptions=[100,200,300,400,500];renderPtsTags();}
function setupDone(){
  const p1=document.getElementById('compPinInp').value;const p2=document.getElementById('compPinConf').value;
  if(p1&&p1!==p2){alert('الرمزان غير متطابقان');return;}
  if(p1&&(p1.length<4||p1.length>6)){alert('الرمز 4-6 أرقام');return;}
  G.pin=p1;initBank();G.selPts=G.ptsOptions[0];
  saveHistory();renderJudge();goTo('judgeScreen');
}

/* ═══════════════ TIMER ═══════════════ */
let lastTickSec=-1;
function fmt(s){return String(Math.floor(s/60)).padStart(2,'0')+':'+String(s%60).padStart(2,'0');}
function updateTimerUI(){
  const el=document.getElementById('tdisp');if(!el)return;
  el.textContent=fmt(G.timerLeft);
  const urg=G.timerLeft<=5&&G.timerLeft>0&&G.timerRunning;
  el.classList.toggle('urgent',urg);
  // sync display/player timer text
  ['dispTimer','playerTimer'].forEach(id=>{
    const e=document.getElementById(id);if(e){e.textContent=fmt(G.timerLeft);e.classList.toggle('urgent',urg);}
  });
}
function setTimer(s){stopTimer();G.timerSecs=s;G.timerLeft=s;updateTimerUI();}
function toggleTimer(){G.timerRunning?stopTimer():startTimerRun();}
function startTimerRun(){
  resumeAC();
  if(G.timerLeft<=0)G.timerLeft=G.timerSecs;
  G.timerRunning=true;
  document.getElementById('tplayBtn').textContent='⏸';
  document.getElementById('tplayBtn').classList.add('on');
  soundStart();
  timerInt=setInterval(()=>{
    G.timerLeft--;
    updateTimerUI();
    // tick every second
    if(G.timerLeft>5)soundTick();
    else if(G.timerLeft>0)soundUrgent();
    else{stopTimer();soundEnd();}
  },1000);
}
function stopTimer(){
  clearInterval(timerInt);timerInt=null;G.timerRunning=false;
  const b=document.getElementById('tplayBtn');if(b){b.textContent='▶';b.classList.remove('on');}
}
function resetTimer(){stopTimer();G.timerLeft=G.timerSecs;updateTimerUI();}

/* ═══════════════ JUDGE ═══════════════ */
function renderJudge(){
  document.getElementById('judgeBrand').textContent=G.title;
  document.getElementById('qNum').textContent=G.currentQ;
  updateTimerUI();
  document.getElementById('ptschips').innerHTML=G.ptsOptions.map(p=>`<div class="ptsc ${p===G.selPts?'sel':''}" onclick="selPts(${p})">${p}</div>`).join('');
  renderTeamBtns();renderLog();updateAQBox();
  document.getElementById('undoBtn').disabled=!G.questionLog.length;
}
function selPts(p){G.selPts=p;document.querySelectorAll('.ptsc').forEach(c=>c.classList.toggle('sel',parseInt(c.textContent)===p));renderTeamBtns();}
function selectTeam(i){G.selTeamIdx=G.selTeamIdx===i?-1:i;renderTeamBtns();}
function renderTeamBtns(){
  document.getElementById('teamBtns').innerHTML=G.teams.map((t,i)=>`
    <div class="trow ${i===G.selTeamIdx?'winner':''}" onclick="selectTeam(${i})">
      <div class="trname">${t.name}</div>
      <div class="trscore">${t.score.toLocaleString()}</div>
      <div class="awbadge">فائز +${G.selPts}</div>
    </div>`).join('');
}
function updateAQBox(){
  const q=G.activeQuestion;
  document.getElementById('aqtext').textContent=q?q.text:'اختر سؤالاً أو تجاوز';
  const a=document.getElementById('aqans');a.textContent=q?.answer?'الإجابة: '+q.answer:'';a.classList.remove('show');
  document.getElementById('aqpts').textContent=q?q.pts+' نقطة':'';
  document.getElementById('sendQBtn').textContent=G.showQOnDisplay?'إخفاء من الشاشة':'إرسال للشاشة';
}
function toggleAns(){document.getElementById('aqans').classList.toggle('show');}
function pickQ(){
  const pool=[];
  G.categories.forEach(cat=>cat.questions.forEach((q,qi)=>{if(!q.used&&q.approved!==false)pool.push({catId:cat.id,qIdx:qi,...q});}));
  if(!pool.length){alert('لا توجد أسئلة غير مستخدمة');return;}
  const q=G.qOrder==='random'?pool[Math.floor(Math.random()*pool.length)]:pool[0];
  G.activeQuestion={...q};updateAQBox();sendStateToBoards();
}
function toggleSendQ(){G.showQOnDisplay=!G.showQOnDisplay;document.getElementById('sendQBtn').textContent=G.showQOnDisplay?'إخفاء من الشاشة':'إرسال للشاشة';sendStateToBoards();}
function confirmAndNext(){
  if(G.selTeamIdx<0){alert('اختر الفريق الفائز');return;}
  resumeAC();stopTimer();
  const snap={teamIdx:G.selTeamIdx,pts:G.selPts,q:G.currentQ,score:G.teams[G.selTeamIdx].score,aq:G.activeQuestion?{...G.activeQuestion}:null};
  G.teams[G.selTeamIdx].score+=G.selPts;G.lastWinner=G.selTeamIdx;G.lastPts=G.selPts;
  G.questionLog.push({q:G.currentQ,teamName:G.teams[G.selTeamIdx].name,pts:G.selPts,_snap:snap});
  if(G.activeQuestion){const cat=G.categories.find(c=>c.id===G.activeQuestion.catId);if(cat&&cat.questions[G.activeQuestion.qIdx])cat.questions[G.activeQuestion.qIdx].used=true;G.activeQuestion=null;G.showQOnDisplay=false;}
  saveHistory();sendStateToBoards();
  document.getElementById('flash').classList.add('on');setTimeout(()=>document.getElementById('flash').classList.remove('on'),400);
  soundWin();spawnConfetti();
  renderLive();goTo('liveScreen');
}
function undoLast(){
  if(!G.questionLog.length)return;
  const last=G.questionLog.pop();const s=last._snap;
  G.teams[s.teamIdx].score=s.score;G.currentQ=s.q;G.selTeamIdx=-1;G.lastWinner=-1;G.lastPts=0;
  if(s.aq){const cat=G.categories.find(c=>c.id===s.aq.catId);if(cat&&cat.questions[s.aq.qIdx])cat.questions[s.aq.qIdx].used=false;}
  Object.keys(CELS).forEach(k=>{Object.keys(CELS[k]).forEach(x=>delete CELS[k][x]);});
  saveHistory();renderJudge();
}
function renderLog(){
  const el=document.getElementById('histLog');
  if(!G.questionLog.length){el.innerHTML='<div class="empty">لا يوجد بعد</div>';return;}
  el.innerHTML=[...G.questionLog].reverse().map(r=>`<div class="logitem"><span class="logq">س${r.q}</span><span class="logw">${r.teamName}</span><span class="logp">+${r.pts}</span></div>`).join('');
}

/* ═══════════════ STATE SYNC (player + display) ═══════════════ */
function sendStateToBoards(){
  renderPlayerBoard();
  renderDisplayBoard();
}

// Auto-refresh display and player every second for timer sync
setInterval(()=>{
  if(document.getElementById('displayScreen').classList.contains('active')){
    // just update timer text, no full re-render needed
    const dt=document.getElementById('dispTimer');if(dt)dt.textContent=fmt(G.timerLeft);
    const urg=G.timerLeft<=5&&G.timerLeft>0&&G.timerRunning;
    if(dt)dt.classList.toggle('urgent',urg);
  }
  if(document.getElementById('playerScreen').classList.contains('active')){
    const pt=document.getElementById('playerTimer');if(pt)pt.textContent=fmt(G.timerLeft);
    const urg=G.timerLeft<=5&&G.timerLeft>0&&G.timerRunning;
    if(pt)pt.classList.toggle('urgent',urg);
  }
},1000);

/* ═══════════════ RANKINGS RENDERER (shared FLIP) ═══════════════ */
function renderRankings(wrapId,celsKey){
  const wrap=document.getElementById(wrapId);if(!wrap)return;
  const cels=CELS[celsKey];
  const sorted=[...G.teams].map((t,i)=>({...t,origIdx:i})).sort((a,b)=>b.score-a.score);
  const maxScore=Math.max(...sorted.map(t=>t.score),1);
  wrap.style.height=(sorted.length*(CARD_H+CARD_GAP)-CARD_GAP)+'px';
  const isFirst=Object.keys(cels).length!==G.teams.length;
  if(isFirst){
    wrap.innerHTML='';Object.keys(cels).forEach(k=>delete cels[k]);
    sorted.forEach((t,rank)=>{
      const el=buildCard(t,rank,maxScore);el.style.top=(rank*(CARD_H+CARD_GAP))+'px';
      wrap.appendChild(el);cels[t.origIdx]=el;
    });return;
  }
  const prevTops={};sorted.forEach(t=>{const el=cels[t.origIdx];if(el)prevTops[t.origIdx]=parseInt(el.style.top)||0;});
  sorted.forEach((t,rank)=>{const el=cels[t.origIdx];if(el)updateCard(el,t,rank,maxScore);});
  sorted.forEach(t=>{const el=cels[t.origIdx];if(!el)return;el.style.transition='none';el.style.top=(prevTops[t.origIdx]??0)+'px';});
  requestAnimationFrame(()=>requestAnimationFrame(()=>{
    sorted.forEach((t,rank)=>{const el=cels[t.origIdx];if(!el)return;el.style.transition='top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s';el.style.top=(rank*(CARD_H+CARD_GAP))+'px';});
  }));
  if(G.lastWinner>=0&&cels[G.lastWinner]){
    const el=cels[G.lastWinner];el.querySelector('.fpts')?.remove();
    const fp=document.createElement('div');fp.className='fpts';fp.textContent='+'+G.lastPts;
    el.appendChild(fp);setTimeout(()=>fp.remove(),1300);
  }
}
function buildCard(t,rank,maxScore){const el=document.createElement('div');el.style.transition='top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s';updateCard(el,t,rank,maxScore);return el;}
function updateCard(el,t,rank,maxScore){
  const rc=rank===0?'rank-1':rank===1?'rank-2':rank===2?'rank-3':'rank-other';
  el.className='rank-card '+rc+(t.origIdx===G.lastWinner?' just-scored':'');
  const pct=(t.score/maxScore*100).toFixed(1);
  el.innerHTML=`<div class="rmed">${rank+1}</div><div class="rname">${t.name}</div><div class="rscore">${t.score.toLocaleString()}</div><div class="sbt"><div class="sbf" style="width:${pct}%"></div></div>`;
}

/* ═══════════════ PLAYER BOARD ═══════════════ */
function renderPlayerBoard(){
  document.getElementById('playerBrand').textContent=G.title;
  document.getElementById('playerCompName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('playerQNum').textContent=G.currentQ;
  document.getElementById('playerMeta').innerHTML=`السؤال <b>${G.currentQ}</b>${G.group?' · '+G.group:''}`;
  const qb=document.getElementById('playerQBox');
  if(G.showQOnDisplay&&G.activeQuestion){qb.classList.add('show');document.getElementById('playerQText').textContent=G.activeQuestion.text;}
  else{qb.classList.remove('show');}
  renderRankings('playerRankings','player');
  updateTimerUI();
}
function showPlayerHistory(){
  document.getElementById('playerQHistory').style.display='block';
  document.getElementById('playerQHistList').innerHTML=G.questionLog.map(r=>`
    <div class="qhist-item">
      <div class="qhist-q">س${r.q}: ${r._snap?.aq?.text||'—'}</div>
      <div class="qhist-meta">الفائز: <span class="qhist-winner">${r.teamName}</span> · +${r.pts} نقطة</div>
    </div>`).join('');
}

/* ═══════════════ DISPLAY BOARD (big screen) ═══════════════ */
function renderDisplayBoard(){
  if(!G.id&&!getHistory().length)return;
  document.getElementById('dispBrand').textContent=G.title||'شاشة العرض';
  document.getElementById('dispName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('dispQ').textContent=G.currentQ;
  const qb=document.getElementById('dispQBox');
  if(G.showQOnDisplay&&G.activeQuestion){
    qb.classList.add('show');
    document.getElementById('dispQText').textContent=G.activeQuestion.text;
  }else{qb.classList.remove('show');}
  document.getElementById('dispTimer').textContent=fmt(G.timerLeft);
  renderRankings('dispRankings','display');
}

/* ═══════════════ LIVE BOARD ═══════════════ */
function renderLive(){
  document.getElementById('liveBrand').textContent=G.title;
  document.getElementById('liveName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('liveQ').textContent=G.currentQ;
  document.getElementById('liveFooter').innerHTML=`
    <button class="btn btn-grad" onclick="goNextFromLive()">السؤال التالي →</button>
    <button class="btn btn-ghost" onclick="showFinale()">إنهاء المسابقة</button>`;
  renderRankings('liveRankings','live');
}
function goNextFromLive(){
  G.currentQ++;G.selTeamIdx=-1;G.lastWinner=-1;G.lastPts=0;
  G.timerLeft=G.timerSecs;G.activeQuestion=null;G.showQOnDisplay=false;
  renderJudge();goTo('judgeScreen');
}

/* ═══════════════ FINALE ═══════════════ */
function showFinale(){
  G.finished=true;saveHistory();
  const sorted=[...G.teams].sort((a,b)=>b.score-a.score);
  document.getElementById('finaleWinner').textContent=sorted[0]?.name||'—';
  const p3=sorted.slice(0,3);const ord=[1,0,2];
  document.getElementById('finalePodium').innerHTML=ord.map(i=>{
    if(!p3[i])return'';const cls=['p2','p1','p3'][i];const m=['🥈','🥇','🥉'][i];
    return `<div class="podium-item ${cls}"><div class="pbar">${m}</div><div class="pname">${p3[i].name}</div><div class="pscore">${p3[i].score.toLocaleString()}</div></div>`;
  }).join('');
  soundWin();spawnConfetti();setTimeout(()=>{spawnConfetti();},800);
  goTo('finaleScreen');
}
function toggleSummary(){
  const el=document.getElementById('summarySection');el.style.display=el.style.display==='none'?'block':'none';
  document.getElementById('summaryTable').innerHTML=`
    <tr>${['المرتبة','الفريق','النقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>
    ${[...G.teams].sort((a,b)=>b.score-a.score).map((t,i)=>`<tr><td>${i+1}</td><td>${t.name}</td><td>${t.score.toLocaleString()}</td></tr>`).join('')}
    <tr><th colspan="3" style="padding-top:10px;">سجل الأسئلة</th></tr>
    <tr>${['سؤال','الفائز','نقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>
    ${G.questionLog.map(r=>`<tr><td>س${r.q}</td><td>${r.teamName}</td><td>+${r.pts}</td></tr>`).join('')}`;
}

/* ═══════════════ BANK ═══════════════ */
function renderBank(judgeMode){
  document.getElementById('bankAddCatBtn').style.display=judgeMode?'flex':'none';
  document.getElementById('bankAIBtn').style.display=judgeMode?'flex':'none';

  // pending for judge
  const allPending=[];
  G.categories.forEach(cat=>cat.questions.forEach((q,qi)=>{if(q.approved===false)allPending.push({catId:cat.id,qi,q});}));
  const ps=document.getElementById('bankPending');
  if(judgeMode&&allPending.length){
    ps.style.display='block';
    document.getElementById('pendingCnt').textContent=allPending.length;
    document.getElementById('pendingList').innerHTML=allPending.map(({catId,qi,q})=>`
      <div class="qitem qpending">
        <div class="qitxt"><div class="qitext">${q.text}</div>${q.answer?`<div class="qians">الإجابة: ${q.answer}</div>`:''}<div class="qipts">${q.pts} نقطة</div></div>
        <div style="display:flex;flex-direction:column;gap:4px;">
          <button class="btn btn-sm btn-green" onclick="approveQ('${catId}',${qi})">موافقة ✓</button>
          <button class="btn btn-sm btn-rg" onclick="rejectQ('${catId}',${qi})">رفض</button>
        </div>
      </div>`).join('');
  }else{ps.style.display='none';}

  const el=document.getElementById('bankCats');
  if(!G.categories.length){el.innerHTML='<div class="empty">لا توجد تصنيفات</div>';return;}
  el.innerHTML=G.categories.map(cat=>{
    const appr=cat.questions.filter(q=>q.approved!==false);
    return `<div class="catbox" id="cat-${cat.id}">
      <div class="cathdr" onclick="toggleCat('${cat.id}')">
        <div class="cattitle">${cat.name}</div>
        <div class="catmeta">${appr.length} سؤال · ${cat.questions.filter(q=>q.used).length} مستخدم</div>
        ${judgeMode?`<div style="display:flex;gap:5px;">
          <button class="btn btn-sm" style="background:rgba(79,70,229,.1);color:var(--a1);border:none;padding:4px 9px;" onclick="event.stopPropagation();openAIModal('${cat.id}')">✦ AI</button>
          <button class="btn btn-sm btn-rg" onclick="event.stopPropagation();deleteCat('${cat.id}')">حذف</button>
        </div>`:''}
        <div class="catarrow">›</div>
      </div>
      <div class="catbody">
        ${appr.map((q,qi)=>`
          <div class="qitem ${q.used?'qused':''}">
            <div class="qitxt">
              <div class="qitext">${q.text}</div>
              ${q.answer&&judgeMode?`<div class="qians">الإجابة: ${q.answer}</div>`:''}
              <div class="qipts">${q.pts} نقطة</div>
            </div>
            ${judgeMode?`<div style="display:flex;gap:4px;">
              <button class="btn btn-sm btn-ghost" onclick="editQ('${cat.id}',${qi})">✎</button>
              <button class="btn btn-sm btn-rg" onclick="delQ('${cat.id}',${qi})">✕</button>
            </div>`:''}
          </div>`).join('')}
        ${judgeMode?`<div class="addrow">
          <input type="text" placeholder="نص السؤال" id="qt-${cat.id}">
          <input type="text" placeholder="الإجابة" id="qa-${cat.id}" style="max-width:140px;">
          <select id="qp-${cat.id}" style="width:auto;flex:none;">${G.ptsOptions.map(p=>`<option value="${p}">${p}</option>`).join('')}</select>
          <button class="btn btn-a1 btn-sm" onclick="addQ('${cat.id}')">اضافة</button>
        </div>`:
        `<div class="addrow">
          <input type="text" placeholder="اقتراح سؤال" id="sqt-${cat.id}">
          <input type="text" placeholder="الإجابة" id="sqa-${cat.id}" style="max-width:130px;">
          <select id="sqp-${cat.id}" style="width:auto;flex:none;">${G.ptsOptions.map(p=>`<option value="${p}">${p}</option>`).join('')}</select>
          <button class="btn btn-ghost btn-sm" onclick="suggestQ('${cat.id}')" style="padding:8px 10px;">اقتراح ↑</button>
        </div>`}
      </div>
    </div>`;
  }).join('');
  G.categories.forEach(c=>document.getElementById('cat-'+c.id)?.classList.add('open'));
}
function toggleCat(id){document.getElementById('cat-'+id)?.classList.toggle('open');}
function addCategory(){const n=prompt('اسم التصنيف:');if(!n?.trim())return;G.categories.push({id:'cat_'+Date.now(),name:n.trim(),questions:[]});renderBank(true);saveHistory();}
function deleteCat(id){if(!confirm('حذف التصنيف وكل أسئلته؟'))return;G.categories=G.categories.filter(c=>c.id!==id);renderBank(true);saveHistory();}
function addQ(catId){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const t=document.getElementById('qt-'+catId)?.value.trim();if(!t)return;
  const a=document.getElementById('qa-'+catId)?.value.trim();
  const p=parseInt(document.getElementById('qp-'+catId)?.value)||G.ptsOptions[0];
  cat.questions.push({id:'q_'+Date.now(),text:t,answer:a,pts:p,used:false,approved:true});
  document.getElementById('qt-'+catId).value='';document.getElementById('qa-'+catId).value='';
  renderBank(true);saveHistory();
}
function suggestQ(catId){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const t=document.getElementById('sqt-'+catId)?.value.trim();if(!t)return;
  const a=document.getElementById('sqa-'+catId)?.value.trim();
  const p=parseInt(document.getElementById('sqp-'+catId)?.value)||G.ptsOptions[0];
  cat.questions.push({id:'q_'+Date.now(),text:t,answer:a,pts:p,used:false,approved:false});
  document.getElementById('sqt-'+catId).value='';document.getElementById('sqa-'+catId).value='';
  alert('تم إرسال اقتراحك للمشرف للموافقة ✓');
  saveHistory();renderBank(false);
}
function approveQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const pending=cat.questions.filter(q=>q.approved===false);
  if(pending[qi])pending[qi].approved=true;
  renderBank(true);saveHistory();
}
function rejectQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const pending=cat.questions.filter(q=>q.approved===false);
  if(pending[qi]){const idx=cat.questions.indexOf(pending[qi]);cat.questions.splice(idx,1);}
  renderBank(true);saveHistory();
}
function delQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const appr=cat.questions.filter(q=>q.approved!==false);
  const real=cat.questions.indexOf(appr[qi]);if(real>=0)cat.questions.splice(real,1);
  renderBank(true);saveHistory();
}
function editQ(catId,qi){
  const cat=G.categories.find(c=>c.id===catId);if(!cat)return;
  const appr=cat.questions.filter(q=>q.approved!==false);const q=appr[qi];if(!q)return;
  const nt=prompt('نص السؤال:',q.text);if(nt===null)return;
  const na=prompt('الإجابة:',q.answer||'');const np=parseInt(prompt('النقاط:',q.pts));
  q.text=nt||q.text;q.answer=na;if(!isNaN(np))q.pts=np;
  renderBank(true);saveHistory();
}
function openBankFromJudge(){bankFromJudge=true;renderBank(true);document.getElementById('bankAddCatBtn').style.display='flex';document.getElementById('bankAIBtn').style.display='flex';goTo('bankScreen');}
function returnFromBank(){saveHistory();if(bankFromJudge){renderJudge();goTo('judgeScreen');}else{goHome();}}

/* ═══════════════ AI ═══════════════ */
function updateAIKeyHint(){
  const p=document.getElementById('aiProv').value;
  document.getElementById('aiKeyHint').textContent=p==='gemini'?'(aistudio.google.com)':'(platform.openai.com)';
  const saved=S.get('aiKey_'+p)||'';document.getElementById('aiKey').value=saved;
}
function openAIModal(catId){
  aiTargetCatId=catId;
  const cat=catId?G.categories.find(c=>c.id===catId):null;
  document.getElementById('aiTopic').value=cat?cat.name:'';
  document.getElementById('aiResults').innerHTML='';
  updateAIKeyHint();
  openModal('aiModal');
}
async function genAI(){
  const topic=document.getElementById('aiTopic').value.trim();if(!topic){alert('اكتب موضوعاً');return;}
  const count=document.getElementById('aiCnt').value;const lang=document.getElementById('aiLang').value;
  const provider=document.getElementById('aiProv').value;const key=document.getElementById('aiKey').value.trim();
  if(!key){alert('أدخل API Key');return;}
  S.set('aiKey_'+provider,key);
  const btn=document.getElementById('aiGenBtn');btn.textContent='جاري...';btn.disabled=true;
  document.getElementById('aiResults').innerHTML='<div class="empty">جاري التوليد...</div>';
  const pts=G.ptsOptions.join(lang==='ar'?'، ':',');
  const prompt=lang==='ar'
    ?`أنشئ ${count} أسئلة مسابقة عن "${topic}" باللغة العربية. أجب بـ JSON فقط بدون أي نص: [{"text":"...","answer":"...","pts":100}]. تنوع النقاط بين: ${pts}`
    :`Create ${count} quiz questions about "${topic}" in English. Reply ONLY with JSON array, no markdown: [{"text":"...","answer":"...","pts":100}]. Vary points among: ${pts}`;
  try{
    let qs;
    if(provider==='openai'){
      const r=await fetch('https://api.openai.com/v1/chat/completions',{method:'POST',headers:{'Content-Type':'application/json','Authorization':'Bearer '+key},body:JSON.stringify({model:'gpt-4o-mini',messages:[{role:'user',content:prompt}],temperature:.7})});
      const d=await r.json();if(!r.ok)throw new Error(d.error?.message||'خطأ');
      qs=JSON.parse(d.choices[0].message.content.replace(/```json|```/g,'').trim());
    }else{
      const r=await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${key}`,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({contents:[{parts:[{text:prompt}]}]})});
      const d=await r.json();if(!r.ok)throw new Error(d.error?.message||'خطأ');
      qs=JSON.parse(d.candidates[0].content.parts[0].text.replace(/```json|```/g,'').trim());
    }
    if(!Array.isArray(qs))throw new Error();
    document.getElementById('aiResults').innerHTML=`
      <div style="background:linear-gradient(135deg,rgba(79,70,229,.06),rgba(124,58,237,.06));border:1.5px solid rgba(79,70,229,.18);border-radius:11px;padding:13px;">
        <div style="font-size:.81rem;font-weight:700;color:var(--a1);margin-bottom:9px;">✦ الأسئلة المقترحة (${qs.length})</div>
        ${qs.map((q,i)=>`<div style="display:flex;align-items:flex-start;gap:8px;background:var(--s1);border:1px solid var(--border);border-radius:9px;padding:9px 11px;margin-bottom:6px;">
          <div style="flex:1;"><div style="font-size:.87rem;line-height:1.5;">${q.text}</div>${q.answer?`<div style="font-size:.77rem;color:var(--green);font-weight:700;margin-top:2px;">الإجابة: ${q.answer}</div>`:''}</div>
          <button class="btn btn-green btn-sm" onclick="addAIQ(${i})">+ اضافة</button>
        </div>`).join('')}
        <button class="btn btn-a1 btn-sm" onclick="addAllAIQ()" style="width:100%;margin-top:5px;">إضافة الكل</button>
      </div>`;
    document.getElementById('aiResults')._qs=qs;
  }catch(e){document.getElementById('aiResults').innerHTML=`<div class="empty" style="color:var(--red);">فشل: ${e.message}</div>`;}
  btn.textContent='توليد الأسئلة';btn.disabled=false;
}
function addAIQ(i){
  const qs=document.getElementById('aiResults')._qs;if(!qs)return;const q=qs[i];
  const cat=aiTargetCatId?G.categories.find(c=>c.id===aiTargetCatId):G.categories[0];
  if(!cat){alert('أنشئ تصنيفاً أولاً');return;}
  const pts=G.ptsOptions.includes(q.pts)?q.pts:G.ptsOptions[0];
  cat.questions.push({id:'ai_'+Date.now()+'_'+i,text:q.text,answer:q.answer||'',pts,used:false,approved:true});
  renderBank(bankFromJudge);saveHistory();
}
function addAllAIQ(){const qs=document.getElementById('aiResults')._qs;if(!qs)return;qs.forEach((_,i)=>addAIQ(i));}

/* ═══════════════ JUDGE SETTINGS ═══════════════ */
function openJudgeSettings(){jsTabI=0;jsTab(0);document.getElementById('jsTitle').value=G.title;document.getElementById('jsGroup').value=G.group;renderJSTeams();renderJSPts();openModal('jsModal');}
function jsTab(t){jsTabI=t;[0,1,2].forEach(i=>{document.getElementById('js'+i).style.display=i===t?'block':'none';});document.querySelectorAll('#jsModal .tab-btn').forEach((b,i)=>b.classList.toggle('active',i===t));}
function renderJSTeams(){
  document.getElementById('jsTeamsList').innerHTML=G.teams.map((t,i)=>`
    <div style="display:flex;align-items:center;gap:7px;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:8px 11px;margin-bottom:6px;">
      <span style="flex:1;font-weight:700;">${t.name}</span>
      <span style="color:var(--gold);font-weight:900;font-size:.93rem;">${t.score}</span>
      <button class="btn btn-sm btn-ghost" onclick="openEditScore(${i})">تعديل</button>
      <button class="btn btn-sm btn-rg" onclick="jsDelTeam(${i})">حذف</button>
    </div>`).join('');
}
function jsAddTeam(){const inp=document.getElementById('jsTeamInp');const n=inp.value.trim();if(!n)return;G.teams.push({name:n,score:0});inp.value='';Object.keys(CELS).forEach(k=>{Object.keys(CELS[k]).forEach(x=>delete CELS[k][x]);});renderJSTeams();}
function jsDelTeam(i){G.teams.splice(i,1);Object.keys(CELS).forEach(k=>{Object.keys(CELS[k]).forEach(x=>delete CELS[k][x]);});renderJSTeams();}
function openEditScore(i){esIdx=i;document.getElementById('esName').textContent=G.teams[i].name;document.getElementById('esScore').value=G.teams[i].score;openModal('esModal');}
function saveEditScore(){const v=parseInt(document.getElementById('esScore').value);if(!isNaN(v)&&v>=0){G.teams[esIdx].score=v;Object.keys(CELS).forEach(k=>{Object.keys(CELS[k]).forEach(x=>delete CELS[k][x]);});}closeModal('esModal');renderJSTeams();}
function renderJSPts(){document.getElementById('jsPtsTags').innerHTML=G.ptsOptions.map((p,i)=>`<div class="pts-tag">${p}<button onclick="jsRemovePts(${i})">✕</button></div>`).join('');}
function jsAddPts(){const v=parseInt(document.getElementById('jsPtsInp').value);if(!v||v<10)return;if(!G.ptsOptions.includes(v)){G.ptsOptions.push(v);G.ptsOptions.sort((a,b)=>a-b);}document.getElementById('jsPtsInp').value='';renderJSPts();}
function jsRemovePts(i){if(G.ptsOptions.length<=1)return;G.ptsOptions.splice(i,1);renderJSPts();}
function saveJS(){const t=document.getElementById('jsTitle').value.trim();if(t)G.title=t;G.group=document.getElementById('jsGroup').value.trim();saveHistory();closeModal('jsModal');renderJudge();}

/* ═══════════════ ADMIN ═══════════════ */
function admTab(t){admTabI=t;[0,1,2].forEach(i=>{document.getElementById('adm'+i).style.display=i===t?'block':'none';});document.querySelectorAll('#adminModal .tab-btn').forEach((b,i)=>b.classList.toggle('active',i===t));if(t===1)renderAdmHist();}
function renderAdmHist(){
  const h=getHistory();
  document.getElementById('admHistList').innerHTML=h.length
    ?h.map(r=>`<div style="display:flex;align-items:center;gap:9px;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:8px 11px;margin-bottom:6px;">
      <div style="flex:1;"><div style="font-weight:700;font-size:.88rem;">${r.title}</div><div style="font-size:.73rem;color:var(--muted);">س${r.currentQ} · ${r.teams?.length} فرق · ${r.pin?'رمز: '+r.pin:''} · ${new Date(r.savedAt).toLocaleDateString('ar-SA')}</div></div>
      <button class="btn btn-sm btn-rg" onclick="delHistory(${r.id})">حذف</button>
    </div>`).join('')
    :'<div class="empty">لا توجد مسابقات</div>';
}
function saveAdmin(){
  const name=document.getElementById('admSiteName').value.trim();if(name){S.set('siteName',name);renderSiteName();}
  const np=document.getElementById('admNewPin').value.trim();if(np&&np.length>=4&&np.length<=6){S.set('adminPin',np);alert('تم تغيير رمز المشرف ✓');}
  closeModal('adminModal');
}

/* ═══════════════ NAV ═══════════════ */
function goHome(){stopTimer();saveHistory();renderHomeStats();goTo('homeScreen');}
function goTo(id){
  const f=document.getElementById('pageFade');f.classList.add('show');
  setTimeout(()=>{document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));document.getElementById(id).classList.add('active');f.classList.remove('show');},220);
}
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}

/* ═══════════════ CONFETTI ═══════════════ */
function spawnConfetti(){
  const cols=['#4f46e5','#7c3aed','#06b6d4','#10b981','#f97316','#d97706','#ec4899'];
  const c=document.getElementById('particles');
  for(let i=0;i<50;i++){
    const p=document.createElement('div');p.className='prt';const sz=5+Math.random()*9;
    p.style.cssText=`left:${Math.random()*100}vw;top:-12px;width:${sz}px;height:${sz}px;background:${cols[~~(Math.random()*cols.length)]};animation-duration:${.9+Math.random()*1.5}s;animation-delay:${Math.random()*.5}s;`;
    c.appendChild(p);setTimeout(()=>p.remove(),3200);
  }
}

/* ═══════════════ INIT ═══════════════ */
renderSiteName();renderHomeStats();
</script>
</body>
</html>
