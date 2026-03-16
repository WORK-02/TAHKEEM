<!DOCTYPE html>
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

/* ── screens ── */
.scr{display:none;width:100%;min-height:100vh;flex-direction:column;}
.scr.on{display:flex;}
.pfade{position:fixed;inset:0;background:var(--bg);z-index:9999;opacity:0;pointer-events:none;transition:opacity .22s;}
.pfade.show{opacity:1;pointer-events:all;}

/* ── base ── */
.card{background:var(--s1);border:1px solid var(--border);border-radius:16px;padding:20px;margin-bottom:14px;box-shadow:var(--sh);}
.lbl{font-size:.74rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1.2px;margin-bottom:8px;}
input,textarea,select{width:100%;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;padding:10px 14px;color:var(--text);font-family:'Cairo',sans-serif;font-size:.93rem;transition:border-color .2s;}
textarea{resize:vertical;min-height:70px;}
input:focus,textarea:focus,select:focus{outline:none;border-color:var(--a1);box-shadow:0 0 0 3px rgba(79,70,229,.12);}
input[type=radio]{width:auto;padding:0;}
.btn{padding:10px 20px;border:none;border-radius:11px;font-family:'Cairo',sans-serif;font-size:.92rem;font-weight:700;cursor:pointer;transition:all .15s;white-space:nowrap;}
.b-ind{background:var(--a1);color:#fff;} .b-ind:hover{background:#4338ca;}
.b-grad{background:linear-gradient(135deg,var(--a1),var(--a2));color:#fff;} .b-grad:hover{filter:brightness(1.07);}
.b-grn{background:var(--green);color:#fff;} .b-grn:hover{filter:brightness(1.1);}
.b-gh{background:var(--s2);color:var(--text2);border:1.5px solid var(--border);} .b-gh:hover{border-color:var(--a1);color:var(--a1);}
.b-rg{background:rgba(239,68,68,.1);color:var(--red);border:1px solid rgba(239,68,68,.2);} .b-rg:hover{background:rgba(239,68,68,.2);}
.b-sm{padding:5px 10px;font-size:.8rem;border-radius:8px;}
.row{display:flex;gap:9px;} .row input{flex:1;}
.empty{color:var(--muted);font-size:.85rem;text-align:center;padding:20px 0;}
.divider{border:none;border-top:1px solid var(--border);margin:14px 0;}

/* ── nav ── */
.nav{display:flex;align-items:center;justify-content:space-between;padding:12px 20px;background:var(--s1);border-bottom:1px solid var(--border);flex-wrap:wrap;gap:9px;position:sticky;top:0;z-index:100;box-shadow:0 1px 6px rgba(79,70,229,.06);}
.nav-brand{font-family:'Tajawal',sans-serif;font-size:1rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.nav-acts{display:flex;gap:6px;align-items:center;}
.iBtn{width:34px;height:34px;border:1.5px solid var(--border);border-radius:9px;background:var(--s2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:.9rem;transition:all .15s;color:var(--text2);}
.iBtn:hover{border-color:var(--a1);color:var(--a1);}
.pill{background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:4px 13px;font-size:.8rem;font-weight:700;color:var(--a1);}

/* ── modal ── */
.mbg{position:fixed;inset:0;background:rgba(0,0,0,.45);backdrop-filter:blur(6px);z-index:5000;display:none;align-items:center;justify-content:center;padding:20px;}
.mbg.on{display:flex;}
.mbox{background:var(--s1);border:1px solid var(--border);border-radius:20px;padding:24px;width:100%;max-width:480px;box-shadow:var(--sh2);max-height:90vh;overflow-y:auto;}
.mtitle{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:900;margin-bottom:14px;}
.macts{display:flex;gap:8px;margin-top:16px;justify-content:flex-end;}
.tabbar{display:flex;background:var(--s2);border-radius:12px;padding:4px;margin-bottom:14px;}
.tabbtn{flex:1;padding:7px 8px;border:none;border-radius:9px;font-family:'Cairo',sans-serif;font-size:.8rem;font-weight:700;cursor:pointer;background:transparent;color:var(--muted);transition:all .15s;}
.tabbtn.on{background:var(--s1);color:var(--a1);box-shadow:var(--sh);}

/* ── theme chips ── */
.tchips{display:flex;gap:7px;justify-content:center;}
.tchip{padding:6px 15px;border-radius:999px;font-size:.81rem;font-weight:700;border:1.5px solid var(--border);background:var(--s1);color:var(--muted);cursor:pointer;transition:all .15s;}
.tchip.on{background:var(--a1);color:#fff;border-color:var(--a1);}

/* ════════════════════════════════
   HOME
════════════════════════════════ */
.hero{width:100%;padding:46px 20px 30px;text-align:center;background:linear-gradient(160deg,rgba(79,70,229,.09) 0%,rgba(124,58,237,.05) 50%,transparent 100%);border-bottom:1px solid var(--border);}
.site-nm{font-family:'Tajawal',sans-serif;font-size:2.5rem;font-weight:900;background:linear-gradient(135deg,var(--a1) 20%,var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:6px;line-height:1.1;}
.site-sub{color:var(--muted);font-size:.88rem;margin-bottom:22px;}
.portals{display:grid;grid-template-columns:repeat(2,1fr);gap:11px;padding:22px 18px;max-width:740px;margin:0 auto;width:100%;}
@media(max-width:500px){.portals{grid-template-columns:1fr;}}
.pcrd{background:var(--s1);border:1.5px solid var(--border);border-radius:18px;padding:20px;cursor:pointer;transition:all .2s;box-shadow:var(--sh);display:flex;flex-direction:column;gap:8px;}
.pcrd:hover{border-color:var(--a1);box-shadow:var(--sh2);transform:translateY(-2px);}
.pico{width:46px;height:46px;border-radius:13px;display:flex;align-items:center;justify-content:center;font-size:1.3rem;}
.pi-j{background:linear-gradient(135deg,var(--a1),var(--a2));}
.pi-p{background:linear-gradient(135deg,var(--green),#059669);}
.pi-d{background:linear-gradient(135deg,var(--orange),#ea580c);}
.pi-b{background:linear-gradient(135deg,var(--a3),#0284c7);}
.pi-a{background:linear-gradient(135deg,#6366f1,#4338ca);}
.ptitle{font-family:'Tajawal',sans-serif;font-size:1rem;font-weight:900;}
.pdesc{font-size:.76rem;color:var(--muted);line-height:1.5;}
.hstats{display:flex;gap:9px;padding:0 18px 20px;max-width:740px;width:100%;margin:0 auto;flex-wrap:wrap;}
.sc{flex:1;min-width:80px;background:var(--s1);border:1px solid var(--border);border-radius:13px;padding:11px;text-align:center;box-shadow:var(--sh);}
.sn{font-family:'Tajawal',sans-serif;font-size:1.6rem;font-weight:900;color:var(--a1);}
.sl{font-size:.68rem;color:var(--muted);font-weight:700;}

/* ════════════════════════════════
   PIN
════════════════════════════════ */
.pin-wrap{display:flex;align-items:center;justify-content:center;flex:1;padding:20px;}
.pin-box{background:var(--s1);border:1px solid var(--border);border-radius:22px;padding:30px;width:100%;max-width:340px;text-align:center;box-shadow:var(--sh2);}
.pin-ico{font-size:2.6rem;margin-bottom:9px;}
.pin-ttl{font-family:'Tajawal',sans-serif;font-size:1.15rem;font-weight:900;margin-bottom:3px;}
.pin-sub{color:var(--muted);font-size:.82rem;margin-bottom:18px;}
.pin-dots{display:flex;gap:9px;justify-content:center;margin-bottom:14px;}
.pdot{width:13px;height:13px;border-radius:50%;border:2px solid var(--border);background:transparent;transition:all .2s;}
.pdot.on{background:var(--a1);border-color:var(--a1);}
.pin-err{color:var(--red);font-size:.81rem;min-height:17px;margin-bottom:9px;}
.pkpad{display:grid;grid-template-columns:repeat(3,1fr);gap:7px;max-width:200px;margin:0 auto 13px;}
.pk{padding:13px;background:var(--s2);border:1.5px solid var(--border);border-radius:11px;font-family:'Tajawal',sans-serif;font-size:1.15rem;font-weight:700;cursor:pointer;transition:all .13s;color:var(--text);}
.pk:hover{background:var(--a1);color:#fff;border-color:var(--a1);}
.pk:active{transform:scale(.94);}
.pk.del{background:rgba(239,68,68,.07);color:var(--red);border-color:rgba(239,68,68,.14);}

/* ════════════════════════════════
   SETUP WIZARD
════════════════════════════════ */
.wbody{flex:1;padding:18px 20px;max-width:580px;width:100%;margin:0 auto;}
.wsteps{display:flex;margin-bottom:20px;position:relative;}
.wsteps::before{content:'';position:absolute;top:12px;right:24px;left:24px;height:2px;background:var(--border);z-index:0;}
.ws{flex:1;text-align:center;position:relative;z-index:1;}
.wd{width:24px;height:24px;border-radius:50%;border:2px solid var(--border);background:var(--s1);display:flex;align-items:center;justify-content:center;margin:0 auto 3px;font-size:.73rem;font-weight:700;color:var(--muted);transition:all .3s;}
.ws.act .wd{background:var(--a1);border-color:var(--a1);color:#fff;}
.ws.done .wd{background:var(--green);border-color:var(--green);color:#fff;}
.wlbl{font-size:.67rem;color:var(--muted);font-weight:700;}
.ws.act .wlbl{color:var(--a1);}
.wp{display:none;} .wp.on{display:block;}
.wnav{display:flex;gap:9px;margin-top:13px;} .wnav .btn{flex:1;padding:11px;}
.pts-tags{display:flex;flex-wrap:wrap;gap:6px;margin-top:8px;}
.ptag{display:flex;align-items:center;gap:4px;background:rgba(79,70,229,.1);border:1.5px solid rgba(79,70,229,.2);border-radius:999px;padding:4px 11px;font-size:.84rem;font-weight:700;color:var(--a1);}
.ptag button{background:none;border:none;color:var(--muted);cursor:pointer;font-size:.84rem;}
.ptag button:hover{color:var(--red);}

/* ════════════════════════════════
   JUDGE
════════════════════════════════ */
.jbody{flex:1;padding:14px 18px;max-width:680px;width:100%;margin:0 auto;}
/* timer */
.tbox{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:9px;background:var(--s1);border:1px solid var(--border);border-radius:13px;padding:11px 15px;margin-bottom:12px;box-shadow:var(--sh);}
.tdisp{font-family:'Tajawal',sans-serif;font-size:2.1rem;font-weight:900;color:var(--a1);min-width:84px;text-align:center;letter-spacing:2px;transition:color .3s;}
.tdisp.urg{color:var(--red);animation:blk .6s ease-in-out infinite;}
@keyframes blk{0%,100%{opacity:1;}50%{opacity:.5;}}
.tpre-row{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:5px;}
.tpre{padding:4px 9px;background:var(--s2);border:1.5px solid var(--border);border-radius:7px;font-size:.77rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .12s;}
.tpre:hover{border-color:var(--a3);color:var(--a3);}
.tctrl{display:flex;gap:5px;}
.tbtn{width:31px;height:31px;border:1.5px solid var(--border);border-radius:8px;background:var(--s2);font-size:.86rem;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .12s;color:var(--text2);}
.tbtn:hover{border-color:var(--a1);color:var(--a1);}
.tbtn.on{background:var(--green);border-color:var(--green);color:#fff;}
/* active q */
.aqbox{background:var(--s1);border:1px solid var(--border);border-radius:13px;padding:12px 16px;margin-bottom:12px;box-shadow:var(--sh);}
.aqlbl{font-size:.69rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:4px;}
.aqtxt{font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:700;line-height:1.6;}
.aqans{font-size:.84rem;color:var(--green);font-weight:700;margin-top:4px;display:none;}
.aqans.on{display:block;}
.aqpts{font-size:.75rem;color:var(--muted);margin-top:2px;}
.aqacts{display:flex;gap:6px;margin-top:7px;flex-wrap:wrap;}
/* pts chips */
.pchips{display:flex;flex-wrap:wrap;gap:6px;margin:7px 0 13px;}
.pc{padding:6px 13px;background:var(--s1);border:1.5px solid var(--border);border-radius:8px;font-size:.87rem;font-weight:700;color:var(--muted);cursor:pointer;transition:all .12s;box-shadow:var(--sh);}
.pc:hover{border-color:var(--a1);color:var(--a1);}
.pc.on{background:var(--a1);border-color:var(--a1);color:#fff;}
/* team rows */
.trow{display:flex;align-items:center;justify-content:space-between;background:var(--s1);border:1.5px solid var(--border);border-radius:12px;padding:11px 14px;margin-bottom:8px;cursor:pointer;transition:all .17s;gap:10px;box-shadow:var(--sh);}
.trow:hover{border-color:var(--a1);box-shadow:var(--sh2);}
.trow.win{border-color:var(--green);background:rgba(16,185,129,.06);box-shadow:0 4px 18px rgba(16,185,129,.13);}
.trnm{font-family:'Tajawal',sans-serif;font-size:.97rem;font-weight:700;flex:1;}
.trsc{font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:900;color:var(--gold);}
.awbdg{padding:3px 9px;background:var(--green);color:#fff;border-radius:7px;font-size:.76rem;font-weight:700;opacity:0;transition:opacity .2s;}
.trow.win .awbdg{opacity:1;}
.actbar{margin-top:10px;padding:11px 14px;background:var(--s1);border:1px solid var(--border);border-radius:12px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px;box-shadow:var(--sh);}
.logwrap{max-height:140px;overflow-y:auto;margin-top:9px;}
.logitem{display:flex;align-items:center;justify-content:space-between;padding:5px 10px;background:var(--s2);border-radius:8px;margin-bottom:4px;font-size:.79rem;}
.logq{color:var(--muted);}.logw{font-weight:700;}.logp{color:var(--green);font-weight:900;}

/* ════════════════════════════════
   SHARED BOARD (rankings)
════════════════════════════════ */
.bwrap{flex:1;display:flex;flex-direction:column;align-items:center;padding:22px 16px 36px;}
.bname{font-family:'Tajawal',sans-serif;font-size:1.9rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-align:center;margin-bottom:6px;}
.bmeta{display:inline-flex;gap:7px;align-items:center;background:var(--s1);border:1.5px solid var(--border);border-radius:999px;padding:6px 16px;font-size:.83rem;font-weight:700;color:var(--muted);box-shadow:var(--sh);margin-bottom:18px;}
.bmeta b{color:var(--a1);}
.qshowbox{background:var(--s1);border:2px solid rgba(79,70,229,.14);border-radius:15px;padding:17px 20px;margin-bottom:18px;box-shadow:var(--sh2);text-align:center;display:none;width:100%;max-width:700px;}
.qshowbox.on{display:block;}
.qshowtext{font-family:'Tajawal',sans-serif;font-size:1.2rem;font-weight:700;line-height:1.6;}
.qshowtimer{font-family:'Tajawal',sans-serif;font-size:2.8rem;font-weight:900;color:var(--a1);margin-top:7px;transition:color .3s;}
.qshowtimer.urg{color:var(--red);}
.rwrap{width:100%;max-width:700px;position:relative;}

/* rank cards */
.rcard{position:absolute;left:0;width:100%;display:flex;align-items:center;gap:12px;background:var(--s1);border:1.5px solid var(--border);border-radius:15px;padding:13px 17px;overflow:hidden;box-shadow:var(--sh);transition:top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s;}
.rcard.r1{border-color:rgba(217,119,6,.38);background:linear-gradient(135deg,#fffbeb,#fef3c7 60%,var(--s1));}
.rcard.r2{border-color:rgba(107,114,128,.22);}
.rcard.r3{border-color:rgba(146,64,14,.22);}
.rcard.hot{border-color:var(--green)!important;box-shadow:0 0 0 3px rgba(16,185,129,.13),var(--sh2)!important;}
.rmed{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Tajawal',sans-serif;font-size:1.1rem;font-weight:900;flex-shrink:0;}
.r1 .rmed{background:linear-gradient(135deg,#fde68a,#d97706);color:#fff;}
.r2 .rmed{background:linear-gradient(135deg,#e5e7eb,#9ca3af);color:#fff;}
.r3 .rmed{background:linear-gradient(135deg,#fcd34d,#92400e);color:#fff;}
.ro .rmed{background:var(--s3);color:var(--muted);font-size:.93rem;}
.rnm{flex:1;font-family:'Tajawal',sans-serif;font-size:1.05rem;font-weight:700;}
.rsc{font-family:'Tajawal',sans-serif;font-size:1.4rem;font-weight:900;color:var(--a1);min-width:74px;text-align:left;}
.r1 .rsc{color:var(--gold);}
.sbt{position:absolute;bottom:0;right:0;left:0;height:4px;background:rgba(79,70,229,.05);}
.sbf{height:100%;background:linear-gradient(90deg,var(--a3),var(--a1),var(--a2));transition:width .85s cubic-bezier(.4,0,.2,1);border-radius:0 0 0 15px;}
.fpts{position:absolute;font-family:'Tajawal',sans-serif;font-size:1.35rem;font-weight:900;color:var(--green);pointer-events:none;text-shadow:0 2px 8px rgba(16,185,129,.28);animation:fpu 1.2s ease-out forwards;right:86px;top:4px;z-index:20;}
@keyframes fpu{0%{opacity:1;transform:translateY(0) scale(.9);}30%{opacity:1;transform:translateY(-12px) scale(1.2);}100%{opacity:0;transform:translateY(-48px) scale(.85);}}

/* display big */
.disp-name{font-family:'Tajawal',sans-serif;font-size:2.8rem;font-weight:900;background:linear-gradient(135deg,var(--a1),var(--a2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-align:center;margin-bottom:8px;}
.disp-qbox{background:var(--s1);border:2px solid rgba(79,70,229,.16);border-radius:18px;padding:20px 26px;margin-bottom:20px;box-shadow:var(--sh2);text-align:center;display:none;width:100%;max-width:860px;}
.disp-qbox.on{display:block;}
.disp-qtxt{font-family:'Tajawal',sans-serif;font-size:1.6rem;font-weight:700;line-height:1.6;}
.disp-timer{font-family:'Tajawal',sans-serif;font-size:4.5rem;font-weight:900;color:var(--a1);margin-top:7px;transition:color .3s;line-height:1;}
.disp-timer.urg{color:var(--red);animation:blk .6s ease-in-out infinite;}

/* live footer */
.lfooter{width:100%;max-width:700px;margin-top:18px;display:flex;gap:8px;flex-wrap:wrap;}
.lfooter .btn{flex:1;padding:11px;font-size:.93rem;}

/* player q history */
.qhi{background:var(--s1);border:1px solid var(--border);border-radius:12px;padding:11px 14px;margin-bottom:7px;box-shadow:var(--sh);}
.qhi-q{font-size:.88rem;font-weight:700;margin-bottom:3px;}
.qhi-m{font-size:.75rem;color:var(--muted);}
.qhi-w{color:var(--green);font-weight:700;}

/* ════════════════════════════════
   BANK
════════════════════════════════ */
.bankbody{flex:1;padding:14px 18px;max-width:800px;width:100%;margin:0 auto;}
.catbox{background:var(--s1);border:1px solid var(--border);border-radius:14px;margin-bottom:11px;box-shadow:var(--sh);overflow:hidden;}
.cathdr{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;cursor:pointer;gap:8px;transition:background .14s;}
.cathdr:hover{background:var(--s2);}
.cattl{font-family:'Tajawal',sans-serif;font-size:.95rem;font-weight:900;flex:1;}
.catmt{font-size:.73rem;color:var(--muted);}
.catarr{transition:transform .25s;color:var(--muted);font-size:.83rem;}
.catbox.open .catarr{transform:rotate(90deg);}
.catbody{display:none;padding:0 14px 12px;}
.catbox.open .catbody{display:block;}
.qitem{display:flex;align-items:flex-start;gap:8px;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:8px 11px;margin-bottom:6px;}
.qitxt{flex:1;}
.qitext{font-size:.87rem;font-weight:600;line-height:1.5;}
.qians{font-size:.76rem;color:var(--green);margin-top:2px;font-weight:700;}
.qipts{font-size:.71rem;color:var(--muted);margin-top:2px;}
.qused{opacity:.4;}
.qpend{border-color:rgba(249,115,22,.3);background:rgba(249,115,22,.04);}
.addrow{display:flex;gap:6px;margin-top:8px;flex-wrap:wrap;}
.addrow input{flex:1;min-width:100px;}
.addrow select{width:auto;flex:none;}

/* ════════════════════════════════
   FINALE
════════════════════════════════ */
.fw{width:100%;max-width:600px;text-align:center;padding:10px 0;}
.ftro{font-size:4rem;margin-bottom:9px;animation:tB .8s ease-out;}
@keyframes tB{0%{transform:scale(.5) translateY(28px);opacity:0;}70%{transform:scale(1.12) translateY(-8px);}100%{transform:scale(1) translateY(0);opacity:1;}}
.fwn{font-family:'Tajawal',sans-serif;font-size:2.3rem;font-weight:900;background:linear-gradient(135deg,var(--gold),var(--orange));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:18px;}
.podium{display:flex;align-items:flex-end;justify-content:center;gap:9px;margin:18px 0 24px;}
.pi{display:flex;flex-direction:column;align-items:center;gap:4px;}
.pb{width:66px;border-radius:7px 7px 0 0;display:flex;align-items:center;justify-content:center;font-size:1.3rem;}
.p1 .pb{height:84px;background:linear-gradient(180deg,#fde68a,#d97706);}
.p2 .pb{height:56px;background:linear-gradient(180deg,#e5e7eb,#9ca3af);}
.p3 .pb{height:42px;background:linear-gradient(180deg,#fcd34d,#92400e);}
.pn{font-family:'Tajawal',sans-serif;font-weight:700;font-size:.84rem;max-width:80px;text-align:center;}
.ps{font-size:.77rem;color:var(--gold);font-weight:900;}
.facts{display:flex;gap:8px;justify-content:center;flex-wrap:wrap;}
.smtbl{width:100%;border-collapse:collapse;margin-top:14px;text-align:right;}
.smtbl th{font-size:.72rem;font-weight:700;color:var(--muted);padding:7px 10px;border-bottom:1px solid var(--border);text-transform:uppercase;}
.smtbl td{padding:7px 10px;border-bottom:1px solid var(--border);font-size:.83rem;}
.smtbl tr:last-child td{border:none;}

/* particles / flash */
.parts{position:fixed;inset:0;pointer-events:none;z-index:999;}
.prt{position:absolute;border-radius:3px;animation:pfall linear forwards;}
@keyframes pfall{0%{transform:translateY(-10px) rotate(0deg);opacity:1;}100%{transform:translateY(110vh) rotate(700deg);opacity:0;}}
.flash{position:fixed;inset:0;pointer-events:none;z-index:998;opacity:0;background:rgba(16,185,129,.07);transition:opacity .15s;}
.flash.on{opacity:1;}
::-webkit-scrollbar{width:5px;height:5px;}::-webkit-scrollbar-thumb{background:var(--border);border-radius:3px;}
@media(max-width:580px){.disp-name,.bname{font-size:1.6rem;}.rnm{font-size:.92rem;}.rsc{font-size:1.2rem;}.jbody,.bankbody,.wbody{padding:12px;}}
</style>
</head>
<body>
<div class="parts" id="parts"></div>
<div class="flash" id="flash"></div>
<div class="pfade" id="pfade"></div>

<!-- ════ HOME ════ -->
<div class="scr on" id="S_home">
  <div class="hero">
    <div class="site-nm" id="siteNm">منصة المسابقات</div>
    <div class="site-sub">اختر القسم المناسب</div>
    <div class="tchips">
      <div class="tchip" data-m="light" onclick="setTheme('light')">فاتح</div>
      <div class="tchip" data-m="auto" onclick="setTheme('auto')">تلقائي</div>
      <div class="tchip" data-m="dark" onclick="setTheme('dark')">داكن</div>
    </div>
  </div>
  <div class="hstats" id="hstats"></div>
  <div class="portals">
    <div class="pcrd" onclick="portal('judge')"><div class="pico pi-j">⚖️</div><div class="ptitle">قسم المحكمين</div><div class="pdesc">إدارة كاملة — نتائج، مؤقت، أسئلة</div></div>
    <div class="pcrd" onclick="portal('player')"><div class="pico pi-p">🏅</div><div class="ptitle">قسم المتسابقين</div><div class="pdesc">أدخل رقم المسابقة لمتابعة النتائج</div></div>
    <div class="pcrd" onclick="portal('display')"><div class="pico pi-d">📺</div><div class="ptitle">شاشة العرض</div><div class="pdesc">للشاشة الكبيرة — ترتيب ومؤقت وسؤال</div></div>
    <div class="pcrd" onclick="portal('bank')"><div class="pico pi-b">📚</div><div class="ptitle">بنك الأسئلة</div><div class="pdesc">استعراض واقتراح أسئلة (تحتاج موافقة)</div></div>
    <div class="pcrd" onclick="portal('admin')"><div class="pico pi-a">🛡️</div><div class="ptitle">لوحة المشرف</div><div class="pdesc">إعدادات الموقع، الرموز، المحفوظات</div></div>
  </div>
</div>

<!-- ════ PIN ════ -->
<div class="scr" id="S_pin">
  <div class="nav"><div class="nav-brand" id="pinBrand">رمز سري</div><div class="nav-acts"><div class="iBtn" onclick="goS('S_home')">← رجوع</div></div></div>
  <div class="pin-wrap">
    <div class="pin-box">
      <div class="pin-ico" id="pinIco">🔐</div>
      <div class="pin-ttl" id="pinTtl">أدخل الرمز</div>
      <div class="pin-sub" id="pinSub">هذا القسم محمي</div>
      <div class="pin-dots">
        <div class="pdot" id="pd0"></div><div class="pdot" id="pd1"></div><div class="pdot" id="pd2"></div>
        <div class="pdot" id="pd3"></div><div class="pdot" id="pd4"></div><div class="pdot" id="pd5"></div>
      </div>
      <div class="pin-err" id="pinErr"></div>
      <div class="pkpad">
        <div class="pk" onclick="pk('1')">1</div><div class="pk" onclick="pk('2')">2</div><div class="pk" onclick="pk('3')">3</div>
        <div class="pk" onclick="pk('4')">4</div><div class="pk" onclick="pk('5')">5</div><div class="pk" onclick="pk('6')">6</div>
        <div class="pk" onclick="pk('7')">7</div><div class="pk" onclick="pk('8')">8</div><div class="pk" onclick="pk('9')">9</div>
        <div class="pk" onclick="pk('0')" style="grid-column:2;">0</div><div class="pk del" onclick="pk('del')">⌫</div>
      </div>
      <button class="btn b-grad" style="width:100%;" onclick="checkPin()">دخول</button>
    </div>
  </div>
</div>

<!-- ════ PLAYER PIN ════ -->
<div class="scr" id="S_playerPin">
  <div class="nav"><div class="nav-brand">قسم المتسابقين</div><div class="nav-acts"><div class="iBtn" onclick="goS('S_home')">⌂</div></div></div>
  <div class="pin-wrap">
    <div class="pin-box">
      <div class="pin-ico">🏅</div>
      <div class="pin-ttl">رقم المسابقة</div>
      <div class="pin-sub">احصل على الرقم من المحكم</div>
      <input type="number" id="playerPinInp" placeholder="أدخل الرقم" style="text-align:center;font-size:1.4rem;letter-spacing:4px;margin-bottom:10px;" autocomplete="off">
      <div class="pin-err" id="playerPinErr"></div>
      <button class="btn b-grad" style="width:100%;" onclick="playerLogin()">دخول</button>
    </div>
  </div>
</div>

<!-- ════ SETUP ════ -->
<div class="scr" id="S_setup">
  <div class="nav"><div class="nav-brand" id="setupBrand">مسابقة جديدة</div><div class="nav-acts"><div class="iBtn" onclick="goS('S_home')">✕</div></div></div>
  <div class="wbody">
    <div class="wsteps">
      <div class="ws act" id="ws0"><div class="wd">1</div><div class="wlbl">الهوية</div></div>
      <div class="ws" id="ws1"><div class="wd">2</div><div class="wlbl">الفرق</div></div>
      <div class="ws" id="ws2"><div class="wd">3</div><div class="wlbl">النقاط</div></div>
      <div class="ws" id="ws3"><div class="wd">4</div><div class="wlbl">الرمز</div></div>
    </div>
    <div class="wp on" id="wp0">
      <div class="card">
        <div class="lbl">اسم المسابقة</div>
        <input type="text" id="setupTitle" placeholder="مثال: مسابقة الثقافة العامة" style="margin-bottom:10px;">
        <div class="lbl">اسم المجموعة (اختياري)</div>
        <input type="text" id="setupGroup" placeholder="مثال: طلاب الفصل" style="margin-bottom:10px;">
        <div class="lbl">ترتيب الأسئلة</div>
        <div style="display:flex;gap:8px;">
          <label style="flex:1;display:flex;align-items:center;gap:7px;background:var(--s2);border:1.5px solid var(--border);border-radius:10px;padding:9px 12px;cursor:pointer;font-size:.9rem;"><input type="radio" name="qord" value="ordered" checked> مرتب</label>
          <label style="flex:1;display:flex;align-items:center;gap:7px;background:var(--s2);border:1.5px solid var(--border);border-radius:10px;padding:9px 12px;cursor:pointer;font-size:.9rem;"><input type="radio" name="qord" value="random"> عشوائي</label>
        </div>
      </div>
      <div class="wnav"><button class="btn b-gh" onclick="goS('S_home')">إلغاء</button><button class="btn b-grad" onclick="wNext(0)">التالي ←</button></div>
    </div>
    <div class="wp" id="wp1">
      <div class="card">
        <div class="lbl">اضافة فريق</div>
        <div class="row"><input type="text" id="teamInp" placeholder="اسم الفريق" onkeydown="if(event.key==='Enter')addTeam()"><button class="btn b-ind" onclick="addTeam()">اضافة</button></div>
        <div id="teamsList" style="margin-top:9px;"><div class="empty">لا توجد فرق</div></div>
      </div>
      <div class="wnav"><button class="btn b-gh" onclick="wPrev(1)">→ السابق</button><button class="btn b-grad" onclick="wNext(1)">التالي ←</button></div>
    </div>
    <div class="wp" id="wp2">
      <div class="card">
        <div class="lbl">فئات النقاط</div>
        <div class="pts-tags" id="ptsTagWrap"></div>
        <div class="row" style="margin-top:8px;">
          <input type="number" id="ptsAddInp" placeholder="فئة جديدة" min="10" step="50" style="max-width:160px;">
          <button class="btn b-gh b-sm" onclick="addPtsTag()" style="padding:10px 13px;">اضافة</button>
          <button class="btn b-gh b-sm" onclick="resetPts()" style="padding:10px 11px;">افتراضي</button>
        </div>
      </div>
      <div class="wnav"><button class="btn b-gh" onclick="wPrev(2)">→ السابق</button><button class="btn b-grad" onclick="wNext(2)">التالي ←</button></div>
    </div>
    <div class="wp" id="wp3">
      <div class="card">
        <div class="lbl">رمز سري (4-6 أرقام)</div>
        <p style="font-size:.81rem;color:var(--muted);margin-bottom:10px;">يُستخدم للدخول كمحكم وكرقم مسابقة للمتسابقين.</p>
        <input type="number" id="compPin1" placeholder="أدخل الرمز" maxlength="6" style="text-align:center;font-size:1.3rem;letter-spacing:5px;margin-bottom:8px;" autocomplete="off">
        <input type="number" id="compPin2" placeholder="أعد الرمز" maxlength="6" style="text-align:center;font-size:1.3rem;letter-spacing:5px;" autocomplete="off">
        <div style="font-size:.77rem;color:var(--muted);margin-top:7px;">اترك فارغاً للدخول بدون رمز</div>
      </div>
      <div class="wnav"><button class="btn b-gh" onclick="wPrev(3)">→ السابق</button><button class="btn b-grad" onclick="setupDone()">بدء المسابقة ✓</button></div>
    </div>
  </div>
</div>

<!-- ════ JUDGE ════ -->
<div class="scr" id="S_judge">
  <div class="nav">
    <div class="nav-brand" id="judgeBrand">المسابقة</div>
    <div class="nav-acts">
      <div class="pill">س <span id="qNum">1</span></div>
      <div class="iBtn" onclick="openBankJ()" title="بنك الأسئلة">📚</div>
      <div class="iBtn" onclick="openJSettings()" title="إعدادات">⚙</div>
      <div class="iBtn" onclick="gHome()">⌂</div>
    </div>
  </div>
  <div class="jbody">
    <div class="tbox">
      <div class="tdisp" id="tdisp">00:30</div>
      <div>
        <div class="tpre-row">
          <div class="tpre" onclick="setT(10)">10ث</div><div class="tpre" onclick="setT(15)">15ث</div><div class="tpre" onclick="setT(30)">30ث</div><div class="tpre" onclick="setT(60)">1د</div><div class="tpre" onclick="setT(90)">90ث</div><div class="tpre" onclick="setT(120)">2د</div>
        </div>
        <div class="tctrl">
          <div class="tbtn" id="tplayBtn" onclick="toggleT()">▶</div>
          <div class="tbtn" onclick="resetT()">↺</div>
          <div class="tbtn" onclick="pushBoards()" title="تحديث الشاشات">↑</div>
        </div>
      </div>
    </div>
    <div class="aqbox">
      <div class="aqlbl">السؤال الحالي</div>
      <div class="aqtxt" id="aqtxt">اختر سؤالاً أو تجاوز</div>
      <div class="aqans" id="aqans"></div>
      <div class="aqpts" id="aqpts"></div>
      <div class="aqacts">
        <button class="btn b-gh b-sm" onclick="toggleAns()">إظهار الإجابة</button>
        <button class="btn b-gh b-sm" onclick="pickQ()">سؤال من البنك</button>
        <button class="btn b-gh b-sm" id="sendQBtn" onclick="toggleSendQ()">إرسال للشاشة</button>
      </div>
    </div>
    <div class="lbl">النقاط</div>
    <div class="pchips" id="pchips"></div>
    <div class="lbl">الفريق الفائز</div>
    <div id="teamBtns"></div>
    <div class="actbar">
      <button class="btn b-gh b-sm" id="undoBtn" onclick="undoLast()" disabled>↩ تراجع</button>
      <div style="display:flex;gap:7px;flex-wrap:wrap;">
        <button class="btn b-gh b-sm" onclick="doFinale()">إنهاء</button>
        <button class="btn b-grad" onclick="confirmNext()">تسجيل وعرض اللوحة</button>
      </div>
    </div>
    <div style="margin-top:12px;"><div class="lbl">سجل الأسئلة</div><div class="logwrap" id="histLog"><div class="empty">لا يوجد بعد</div></div></div>
  </div>
</div>

<!-- ════ PLAYER ════ -->
<div class="scr" id="S_player">
  <div class="nav">
    <div class="nav-brand" id="playerBrand">المتسابقون</div>
    <div class="nav-acts">
      <div class="pill">س <span id="playerQ">—</span></div>
      <div class="iBtn" onclick="goS('S_playerPin')">↩ رجوع</div>
      <div class="iBtn" onclick="goS('S_home')">⌂</div>
    </div>
  </div>
  <div class="bwrap" style="background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.08) 0%,transparent 58%),var(--bg);">
    <div class="bname" id="playerName">—</div>
    <div class="bmeta" id="playerMeta">السؤال <b>—</b></div>
    <div class="qshowbox" id="playerQBox">
      <div class="qshowtext" id="playerQTxt">—</div>
      <div class="qshowtimer" id="playerTimer">—</div>
    </div>
    <div class="rwrap" id="playerRankings"></div>
    <div id="playerHistory" style="display:none;margin-top:22px;width:100%;max-width:700px;">
      <div class="lbl" style="margin-bottom:9px;">سجل الأسئلة</div>
      <div id="playerHistList"></div>
    </div>
  </div>
</div>

<!-- ════ DISPLAY ════ -->
<div class="scr" id="S_display">
  <div class="nav">
    <div class="nav-brand" id="dispBrand">شاشة العرض</div>
    <div class="nav-acts"><div class="iBtn" onclick="goS('S_home')">⌂</div></div>
  </div>
  <div class="bwrap" style="background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.11) 0%,transparent 58%),var(--bg);">
    <div class="disp-name" id="dispName">—</div>
    <div class="bmeta" style="margin-bottom:16px;">السؤال <b id="dispQ">—</b></div>
    <div class="disp-qbox" id="dispQBox">
      <div class="disp-qtxt" id="dispQTxt">—</div>
      <div class="disp-timer" id="dispTimer">—</div>
    </div>
    <div class="rwrap" id="dispRankings" style="max-width:860px;"></div>
  </div>
</div>

<!-- ════ BANK ════ -->
<div class="scr" id="S_bank">
  <div class="nav">
    <div class="nav-brand">بنك الأسئلة</div>
    <div class="nav-acts">
      <div class="iBtn" id="bankCatBtn" onclick="addCat()" style="display:none;">+</div>
      <div class="iBtn" id="bankAIBtn" onclick="openAI(null)" style="display:none;">✦</div>
      <div class="iBtn" onclick="returnBank()">← رجوع</div>
    </div>
  </div>
  <div class="bankbody">
    <div id="pendingSec" style="display:none;">
      <div class="lbl" style="color:var(--orange);">بانتظار موافقة المشرف <span id="pendCnt" style="background:rgba(249,115,22,.12);color:var(--orange);padding:2px 8px;border-radius:999px;font-size:.75rem;font-weight:700;"></span></div>
      <div id="pendList" style="margin-bottom:14px;"></div>
    </div>
    <div id="bankCats"><div class="empty">لا توجد تصنيفات</div></div>
  </div>
</div>

<!-- ════ LIVE ════ -->
<div class="scr" id="S_live">
  <div class="nav">
    <div class="nav-brand" id="liveBrand">النتائج</div>
    <div class="nav-acts">
      <div class="iBtn" onclick="goS('S_judge')">← رجوع</div>
      <div class="iBtn" onclick="gHome()">⌂</div>
    </div>
  </div>
  <div class="bwrap" style="background:radial-gradient(ellipse 80% 55% at 50% -5%,rgba(79,70,229,.1) 0%,transparent 58%),var(--bg);">
    <div class="bname" id="liveNm">—</div>
    <div class="bmeta">السؤال <b id="liveQ">—</b></div>
    <div class="rwrap" id="liveRankings"></div>
    <div class="lfooter" id="liveFooter"></div>
  </div>
</div>

<!-- ════ FINALE ════ -->
<div class="scr" id="S_finale">
  <div class="nav">
    <div class="nav-brand">نهاية المسابقة</div>
    <div class="nav-acts">
      <div class="iBtn" onclick="goS('S_judge')">← رجوع</div>
      <div class="iBtn" onclick="gHome()">⌂</div>
    </div>
  </div>
  <div class="bwrap" style="background:radial-gradient(ellipse 90% 60% at 50% 0%,rgba(79,70,229,.13) 0%,transparent 65%),var(--bg);justify-content:center;">
    <div class="fw">
      <div class="ftro">🏆</div>
      <div style="color:var(--muted);font-size:.97rem;font-weight:700;margin-bottom:3px;">الفائز</div>
      <div class="fwn" id="finaleW">—</div>
      <div class="podium" id="finalePodium"></div>
      <div class="facts">
        <button class="btn b-grad" onclick="gHome()">الرئيسية</button>
        <button class="btn b-gh" onclick="toggleSummary()">ملخص</button>
      </div>
      <div id="summSec" style="display:none;margin-top:16px;text-align:right;width:100%;">
        <table class="smtbl" id="summTbl"></table>
      </div>
    </div>
  </div>
</div>

<!-- ════ MODALS ════ -->
<!-- Admin -->
<div class="mbg" id="M_admin">
  <div class="mbox">
    <div class="mtitle">🛡️ لوحة المشرف</div>
    <div class="tabbar">
      <button class="tabbtn on" onclick="admTab(0)">الموقع</button>
      <button class="tabbtn" onclick="admTab(1)">المسابقات</button>
      <button class="tabbtn" onclick="admTab(2)">الرمز</button>
    </div>
    <div id="adm0">
      <div class="lbl">اسم الموقع</div>
      <input type="text" id="admNm" style="margin-bottom:10px;" placeholder="منصة المسابقات">
    </div>
    <div id="adm1" style="display:none;"><div id="admHistList"><div class="empty">لا توجد مسابقات</div></div></div>
    <div id="adm2" style="display:none;">
      <p style="font-size:.84rem;color:var(--text2);margin-bottom:10px;">الرمز الافتراضي: <b>1234</b></p>
      <div class="lbl">رمز المشرف الجديد (4-6 أرقام)</div>
      <input type="number" id="admNewPin" placeholder="أدخل الرمز الجديد" autocomplete="off">
    </div>
    <div class="macts"><button class="btn b-grad" onclick="saveAdmin()">حفظ</button><button class="btn b-gh" onclick="closeM('M_admin')">إغلاق</button></div>
  </div>
</div>
<!-- Judge Settings -->
<div class="mbg" id="M_js">
  <div class="mbox">
    <div class="mtitle">⚙ إعدادات المسابقة</div>
    <div class="tabbar">
      <button class="tabbtn on" onclick="jsTab(0)">الفرق</button>
      <button class="tabbtn" onclick="jsTab(1)">النقاط</button>
      <button class="tabbtn" onclick="jsTab(2)">المسابقة</button>
    </div>
    <div id="js0">
      <div class="row" style="margin-bottom:8px;"><input type="text" id="jsTeamInp" placeholder="فريق جديد" onkeydown="if(event.key==='Enter')jsAddTeam()"><button class="btn b-ind" onclick="jsAddTeam()">اضافة</button></div>
      <div id="jsTeamList"></div>
      <div class="divider"></div>
      <div class="lbl">تعديل النقاط يدوياً</div>
      <div id="jsScoreEdit"></div>
    </div>
    <div id="js1" style="display:none;">
      <div class="pts-tags" id="jsPtsTags"></div>
      <div class="row" style="margin-top:8px;"><input type="number" id="jsPtsInp" placeholder="فئة جديدة" min="10" step="50" style="max-width:150px;"><button class="btn b-gh b-sm" onclick="jsAddPts()" style="padding:10px 12px;">اضافة</button></div>
    </div>
    <div id="js2" style="display:none;">
      <div class="lbl">اسم المسابقة</div><input type="text" id="jsTitleInp" style="margin-bottom:9px;">
      <div class="lbl">اسم المجموعة</div><input type="text" id="jsGroupInp">
    </div>
    <div class="macts"><button class="btn b-grad" onclick="saveJS()">حفظ</button><button class="btn b-gh" onclick="closeM('M_js')">إغلاق</button></div>
  </div>
</div>
<!-- Edit Score -->
<div class="mbg" id="M_es">
  <div class="mbox" style="max-width:300px;">
    <div class="mtitle">تعديل نقاط: <span id="esNm"></span></div>
    <input type="number" id="esVal" min="0" style="text-align:center;font-size:1.3rem;">
    <div class="macts"><button class="btn b-grad" onclick="saveES()">حفظ</button><button class="btn b-gh" onclick="closeM('M_es')">إلغاء</button></div>
  </div>
</div>
<!-- AI -->
<div class="mbg" id="M_ai">
  <div class="mbox" style="max-width:500px;">
    <div class="mtitle">✦ توليد أسئلة بالذكاء الاصطناعي</div>
    <div class="lbl">مزود AI</div>
    <select id="aiProv" style="margin-bottom:8px;" onchange="aiProvChanged()">
      <option value="gemini">Gemini (Google) — مجاني</option>
      <option value="openai">OpenAI (ChatGPT)</option>
    </select>
    <div class="lbl">API Key <small id="aiKeyHint" style="color:var(--muted);font-weight:400;"></small></div>
    <input type="password" id="aiKey" placeholder="الصق المفتاح هنا" style="margin-bottom:8px;" autocomplete="off">
    <div class="lbl">الموضوع</div>
    <input type="text" id="aiTopic" placeholder="مثال: جغرافيا المملكة" style="margin-bottom:8px;">
    <div style="display:flex;gap:8px;margin-bottom:10px;">
      <select id="aiCnt"><option value="3">3</option><option value="5" selected>5</option><option value="10">10</option></select>
      <select id="aiLang"><option value="ar">عربي</option><option value="en">English</option></select>
    </div>
    <button class="btn b-grad" onclick="genAI()" id="aiGenBtn" style="width:100%;margin-bottom:10px;">توليد الأسئلة</button>
    <div id="aiRes"></div>
    <div class="macts"><button class="btn b-gh" onclick="closeM('M_ai')">إغلاق</button></div>
  </div>
</div>
<!-- Resume -->
<div class="mbg" id="M_resume">
  <div class="mbox" style="max-width:360px;">
    <div class="mtitle">مسابقة محفوظة</div>
    <div id="resumeTxt" style="font-size:.88rem;color:var(--text2);margin-bottom:4px;"></div>
    <div class="macts">
      <button class="btn b-grad" onclick="doResume()">استئناف</button>
      <button class="btn b-gh" onclick="closeM('M_resume');startNew()">جديدة</button>
      <button class="btn b-gh" onclick="closeM('M_resume')">إلغاء</button>
    </div>
  </div>
</div>

<script>
/* ══════════════════════════════════════════
   AUDIO
══════════════════════════════════════════ */
let AC;
function getAC(){if(!AC)AC=new(window.AudioContext||window.webkitAudioContext)();if(AC.state==='suspended')AC.resume();return AC;}
function tone(f,t,type='sine',v=0.4,d=0){try{const ac=getAC(),o=ac.createOscillator(),g=ac.createGain();o.connect(g);g.connect(ac.destination);o.type=type;o.frequency.value=f;g.gain.setValueAtTime(0,ac.currentTime+d);g.gain.linearRampToValueAtTime(v,ac.currentTime+d+.01);g.gain.exponentialRampToValueAtTime(.001,ac.currentTime+d+t);o.start(ac.currentTime+d);o.stop(ac.currentTime+d+t+.05);}catch(e){}}
function sndStart(){[0,.3,.6].forEach((d,i)=>tone(440+i*110,'sine',.18,.5,d));}
function sndTick(){tone(800,'square',.05,.12);}
function sndUrg(){tone(660,'sawtooth',.07,.22);}
function sndEnd(){tone(600,'sine',.14,.45,0);tone(400,'sine',.14,.45,.16);tone(200,'sawtooth',.28,.38,.32);}
function sndWin(){[523,659,784,1047].forEach((f,i)=>tone(f,'sine',.22,.5,i*.11));}

/* ══════════════════════════════════════════
   STORAGE
══════════════════════════════════════════ */
const LS={g:k=>{try{return JSON.parse(localStorage.getItem(k));}catch{return null;}},s:(k,v)=>localStorage.setItem(k,JSON.stringify(v))};

/* ══════════════════════════════════════════
   BUILTIN BANK
══════════════════════════════════════════ */
const BANK0=[
  {name:'ثقافة عامة',qs:[{t:'ما عاصمة المملكة العربية السعودية؟',a:'الرياض',p:100},{t:'كم عدد أيام الأسبوع؟',a:'7 أيام',p:100},{t:'ما أكبر كوكب في المجموعة الشمسية؟',a:'المشتري',p:200},{t:'ما أطول نهر في العالم؟',a:'نيل',p:200},{t:'في أي سنة تأسست المملكة؟',a:'1932م',p:300},{t:'ما الرمز الكيميائي للذهب؟',a:'Au',p:400},{t:'كم عدد الدول المعترف بها دولياً؟',a:'195 دولة',p:500}]},
  {name:'علوم وتكنولوجيا',qs:[{t:'ما الوحدة الأساسية للمعلومات في الحاسوب؟',a:'البت',p:100},{t:'من اخترع الهاتف؟',a:'غراهام بيل',p:200},{t:'ما الغاز الأوفر في الغلاف الجوي؟',a:'النيتروجين 78%',p:200},{t:'ما سرعة الضوء؟',a:'300,000 كم/ث',p:300},{t:'ما معنى HTTP؟',a:'HyperText Transfer Protocol',p:400}]},
  {name:'جغرافيا',qs:[{t:'ما أكبر قارة مساحةً؟',a:'آسيا',p:100},{t:'ما أعلى جبل في العالم؟',a:'إيفرست',p:100},{t:'ما أصغر دولة في العالم؟',a:'الفاتيكان',p:200},{t:'ما أكبر صحراء في العالم؟',a:'الصحراء الكبرى',p:300},{t:'أي دولة أكبر سكاناً؟',a:'الهند',p:200}]},
  {name:'تاريخ',qs:[{t:'متى انتهت الحرب العالمية الثانية؟',a:'1945م',p:100},{t:'من أول إنسان على القمر؟',a:'نيل أرمسترونغ',p:200},{t:'في أي عام اكتشف كولومبوس أمريكا؟',a:'1492م',p:300},{t:'متى سقط جدار برلين؟',a:'1989م',p:300}]},
];

/* ══════════════════════════════════════════
   STATE
══════════════════════════════════════════ */
let G={id:null,title:'',group:'',qOrder:'ordered',teams:[],pts:[100,200,300,400,500],cats:[],curQ:1,selPts:100,selTeam:-1,lastWin:-1,lastPts:0,log:[],activeQ:null,showQ:false,tSecs:30,tLeft:30,tRun:false,pin:'',done:false};
const RCELS={live:{},player:{},display:{}};
const CH=76,CG=11;
let tInt=null,pinVal='',pinTarget='',bankJ=false,aiCatId=null,esIdx=-1,jsTabI=0,admTabI=0;

/* ══════════════════════════════════════════
   THEME
══════════════════════════════════════════ */
let thM=LS.g('thM')||'auto';
function applyTheme(){const dk=thM==='dark'||(thM==='auto'&&matchMedia('(prefers-color-scheme: dark)').matches);document.documentElement.setAttribute('data-theme',dk?'dark':'light');document.querySelectorAll('.tchip').forEach(c=>c.classList.toggle('on',c.dataset.m===thM));}
function setTheme(m){thM=m;LS.s('thM',m);applyTheme();}
matchMedia('(prefers-color-scheme: dark)').addEventListener('change',applyTheme);
applyTheme();

/* ══════════════════════════════════════════
   SITE
══════════════════════════════════════════ */
function getSite(){return LS.g('site')||'منصة المسابقات';}
function getAdmPin(){return LS.g('admPin')||'1234';}
function renderSite(){const n=getSite();document.getElementById('siteNm').textContent=n;document.title=n;}

/* ══════════════════════════════════════════
   HISTORY
══════════════════════════════════════════ */
function getH(){return LS.g('hist')||[];}
function saveH(){
  if(!G.title||!G.teams.length)return;
  let h=getH();
  const r={id:G.id||Date.now(),title:G.title,group:G.group,qOrder:G.qOrder,teams:JSON.parse(JSON.stringify(G.teams)),pts:[...G.pts],cats:JSON.parse(JSON.stringify(G.cats)),log:[...G.log],curQ:G.curQ,selPts:G.selPts,pin:G.pin,done:G.done,saved:Date.now()};
  G.id=r.id;const i=h.findIndex(x=>x.id===r.id);if(i>=0)h[i]=r;else h.unshift(r);h=h.slice(0,20);LS.s('hist',h);
}
function delH(id){if(!confirm('حذف هذه المسابقة؟'))return;LS.s('hist',getH().filter(x=>x.id!==id));renderStats();renderAdmHist();}

function renderStats(){
  const h=getH();const tq=h.reduce((a,b)=>a+(b.cats?.reduce((x,c)=>x+(c.questions?.length||0),0)||0),0);
  document.getElementById('hstats').innerHTML=`<div class="sc"><div class="sn">${h.length}</div><div class="sl">مسابقة</div></div><div class="sc"><div class="sn">${h.reduce((a,b)=>a+(b.teams?.length||0),0)}</div><div class="sl">فريق</div></div><div class="sc"><div class="sn">${h.reduce((a,b)=>a+(b.log?.length||0),0)}</div><div class="sl">سؤال مجاب</div></div><div class="sc"><div class="sn">${tq}</div><div class="sl">في البنك</div></div>`;
}

/* ══════════════════════════════════════════
   NAV
══════════════════════════════════════════ */
function goS(id){
  const f=document.getElementById('pfade');f.classList.add('show');
  setTimeout(()=>{document.querySelectorAll('.scr').forEach(s=>s.classList.remove('on'));document.getElementById(id).classList.add('on');f.classList.remove('show');},220);
}
function gHome(){stopT();saveH();renderStats();goS('S_home');}
function openM(id){document.getElementById(id).classList.add('on');}
function closeM(id){document.getElementById(id).classList.remove('on');}

/* ══════════════════════════════════════════
   PORTALS
══════════════════════════════════════════ */
function portal(type){
  if(AC)AC.resume();
  if(type==='judge'){
    if(G.id){renderJudge();goS('S_judge');return;}
    const h=getH();
    if(h.length){document.getElementById('resumeTxt').innerHTML=`<b>${h[0].title}</b> — السؤال ${h[0].curQ} · ${h[0].teams?.length} فرق`;document.getElementById('M_resume')._id=h[0].id;openM('M_resume');}
    else startNew();
    return;
  }
  if(type==='player'){goS('S_playerPin');return;}
  if(type==='display'){
    const h=getH();if(!G.id&&!h.length){alert('لا توجد مسابقة');return;}
    if(!G.id&&h.length){loadComp(h[0].id);}
    goS('S_display');setTimeout(()=>renderDisplay(),260);
    return;
  }
  if(type==='bank'){bankJ=false;document.getElementById('bankCatBtn').style.display='none';document.getElementById('bankAIBtn').style.display='none';renderBank(false);goS('S_bank');return;}
  if(type==='admin'){pinVal='';updateDots();document.getElementById('pinErr').textContent='';document.getElementById('pinIco').textContent='🛡️';document.getElementById('pinTtl').textContent='لوحة المشرف';document.getElementById('pinSub').textContent='أدخل رمز المشرف';pinTarget='admin';goS('S_pin');return;}
}

function doResume(){
  closeM('M_resume');
  const id=document.getElementById('M_resume')._id;
  const rec=getH().find(x=>x.id===id);if(!rec)return;
  if(rec.pin){
    pinVal='';updateDots();document.getElementById('pinErr').textContent='';
    document.getElementById('pinIco').textContent='⚖️';
    document.getElementById('pinTtl').textContent='رمز: '+rec.title;
    document.getElementById('pinSub').textContent='أدخل الرمز السري';
    document.getElementById('M_resume')._resumeId=id;
    pinTarget='judgeResume';goS('S_pin');
  }else{loadComp(id);renderJudge();goS('S_judge');}
}

function loadComp(id){
  const r=getH().find(x=>x.id===id);if(!r)return;
  G={...G,...r,teams:JSON.parse(JSON.stringify(r.teams)),cats:JSON.parse(JSON.stringify(r.cats||[])),log:[...(r.log||[])],pts:[...r.pts],selTeam:-1,lastWin:-1,lastPts:0,tSecs:30,tLeft:30,tRun:false,activeQ:null,showQ:false};
  clearCels();initBank();
}
function clearCels(){Object.keys(RCELS).forEach(k=>{Object.keys(RCELS[k]).forEach(x=>delete RCELS[k][x]);});}
function initBank(){
  if(!G.cats||!G.cats.length){
    G.cats=BANK0.map(b=>({id:'b_'+b.name,name:b.name,questions:b.qs.map((q,i)=>({id:'bq'+i,text:q.t,answer:q.a,pts:q.p,used:false,approved:true}))}));
  }
}

/* ══════════════════════════════════════════
   PIN
══════════════════════════════════════════ */
function pk(v){
  if(!AC){try{AC=new(window.AudioContext||window.webkitAudioContext)();}catch(e){}}
  if(AC&&AC.state==='suspended')AC.resume();
  tone(660,'sine',.05,.12);
  if(v==='del')pinVal=pinVal.slice(0,-1);
  else if(pinVal.length<6)pinVal+=v;
  updateDots();
  if(pinVal.length>0)document.getElementById('pinErr').textContent='';
}
function updateDots(){for(let i=0;i<6;i++)document.getElementById('pd'+i).classList.toggle('on',i<pinVal.length);}
function checkPin(){
  const e=document.getElementById('pinErr');
  if(pinTarget==='admin'){
    if(pinVal===getAdmPin()){document.getElementById('admNm').value=getSite();renderAdmHist();goS('S_home');setTimeout(()=>{admTab(0);openM('M_admin');},300);}
    else{e.textContent='رمز خاطئ';tone(220,'sawtooth',.2,.3);}
    return;
  }
  if(pinTarget==='judgeResume'){
    const id=document.getElementById('M_resume')._resumeId;const r=getH().find(x=>x.id===id);
    if(r&&String(r.pin)===pinVal){loadComp(id);renderJudge();goS('S_judge');}
    else{e.textContent='رمز خاطئ';tone(220,'sawtooth',.2,.3);}
    return;
  }
}

/* player login */
function playerLogin(){
  const v=document.getElementById('playerPinInp').value.trim();
  const e=document.getElementById('playerPinErr');e.textContent='';
  const h=getH();if(!h.length){e.textContent='لا توجد مسابقات محفوظة';return;}
  let found=null;
  if(v===''||v==='0'){found=h.find(x=>!x.pin||x.pin==='')||h[0];}
  else{found=h.find(x=>String(x.pin)===String(v))||null;}
  if(!found){e.textContent='لم يُعثر على مسابقة بهذا الرقم';return;}
  loadComp(found.id);
  renderPlayer();goS('S_player');
  if(G.done)showPlayerHistory();
}

/* ══════════════════════════════════════════
   SETUP
══════════════════════════════════════════ */
function startNew(){
  G={id:null,title:'',group:'',qOrder:'ordered',teams:[],pts:[100,200,300,400,500],cats:[],curQ:1,selPts:100,selTeam:-1,lastWin:-1,lastPts:0,log:[],activeQ:null,showQ:false,tSecs:30,tLeft:30,tRun:false,pin:'',done:false};
  clearCels();renderWiz(0);goS('S_setup');
}
function renderWiz(s){
  for(let i=0;i<4;i++){document.getElementById('wp'+i).classList.toggle('on',i===s);const ws=document.getElementById('ws'+i);ws.classList.remove('act','done');if(i===s)ws.classList.add('act');else if(i<s)ws.classList.add('done');}
  if(s===1)renderSetupTeams();if(s===2)renderPtsTags();
}
function wNext(s){
  if(s===0){const t=document.getElementById('setupTitle').value.trim();if(!t){alert('اكتب اسم المسابقة');return;}G.title=t;G.group=document.getElementById('setupGroup').value.trim();G.qOrder=document.querySelector('input[name=qord]:checked').value;}
  if(s===1&&!G.teams.length){alert('اضف فريقاً');return;}
  renderWiz(s+1);
}
function wPrev(s){renderWiz(s-1);}
function renderSetupTeams(){const el=document.getElementById('teamsList');if(!G.teams.length){el.innerHTML='<div class="empty">لا توجد فرق</div>';return;}el.innerHTML=G.teams.map((t,i)=>`<div style="display:flex;align-items:center;justify-content:space-between;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:8px 11px;margin-bottom:5px;"><span style="font-weight:700;">${t.name}</span><button class="btn b-rg b-sm" onclick="rmTeam(${i})">حذف</button></div>`).join('');}
function addTeam(){const inp=document.getElementById('teamInp');const n=inp.value.trim();if(!n)return;if(G.teams.find(t=>t.name===n)){inp.select();return;}G.teams.push({name:n,score:0});inp.value='';inp.focus();renderSetupTeams();}
function rmTeam(i){G.teams.splice(i,1);renderSetupTeams();}
function renderPtsTags(){document.getElementById('ptsTagWrap').innerHTML=G.pts.map((p,i)=>`<div class="ptag">${p}<button onclick="rmPtsTag(${i})">✕</button></div>`).join('');}
function addPtsTag(){const v=parseInt(document.getElementById('ptsAddInp').value);if(!v||v<10)return;if(!G.pts.includes(v)){G.pts.push(v);G.pts.sort((a,b)=>a-b);}document.getElementById('ptsAddInp').value='';renderPtsTags();}
function rmPtsTag(i){if(G.pts.length<=1)return;G.pts.splice(i,1);renderPtsTags();}
function resetPts(){G.pts=[100,200,300,400,500];renderPtsTags();}
function setupDone(){
  const p1=String(document.getElementById('compPin1').value).trim();
  const p2=String(document.getElementById('compPin2').value).trim();
  if(p1&&p1!==p2){alert('الرمزان غير متطابقان');return;}
  if(p1&&(p1.length<4||p1.length>6)){alert('الرمز 4-6 أرقام');return;}
  G.pin=p1;initBank();G.selPts=G.pts[0];saveH();renderJudge();goS('S_judge');
}

/* ══════════════════════════════════════════
   TIMER
══════════════════════════════════════════ */
function fmt(s){return String(Math.floor(s/60)).padStart(2,'0')+':'+String(s%60).padStart(2,'0');}
function updateTimerUI(){
  const v=fmt(G.tLeft),urg=G.tLeft<=5&&G.tLeft>0&&G.tRun;
  const ids=['tdisp','dispTimer','playerTimer'];
  ids.forEach(id=>{const el=document.getElementById(id);if(el){el.textContent=v;el.classList.toggle('urg',urg);}});
}
function setT(s){stopT();G.tSecs=s;G.tLeft=s;updateTimerUI();}
function toggleT(){G.tRun?stopT():startT();}
function startT(){
  if(!AC){try{AC=new(window.AudioContext||window.webkitAudioContext)();}catch(e){}}
  if(AC.state==='suspended')AC.resume();
  if(G.tLeft<=0)G.tLeft=G.tSecs;
  G.tRun=true;document.getElementById('tplayBtn').textContent='⏸';document.getElementById('tplayBtn').classList.add('on');
  sndStart();
  tInt=setInterval(()=>{G.tLeft--;updateTimerUI();if(G.tLeft>5)sndTick();else if(G.tLeft>0)sndUrg();else{stopT();sndEnd();}},1000);
}
function stopT(){clearInterval(tInt);tInt=null;G.tRun=false;const b=document.getElementById('tplayBtn');if(b){b.textContent='▶';b.classList.remove('on');}}
function resetT(){stopT();G.tLeft=G.tSecs;updateTimerUI();}

// auto-sync timer to display/player screens
setInterval(()=>{updateTimerUI();},1000);

/* ══════════════════════════════════════════
   JUDGE
══════════════════════════════════════════ */
function renderJudge(){
  document.getElementById('judgeBrand').textContent=G.title;
  document.getElementById('qNum').textContent=G.curQ;
  updateTimerUI();
  document.getElementById('pchips').innerHTML=G.pts.map(p=>`<div class="pc${p===G.selPts?' on':''}" onclick="selPts(${p})">${p}</div>`).join('');
  renderTRows();renderLog();updateAQ();
  document.getElementById('undoBtn').disabled=!G.log.length;
}
function selPts(p){G.selPts=p;document.querySelectorAll('.pc').forEach(c=>c.classList.toggle('on',parseInt(c.textContent)===p));renderTRows();}
function selTeam(i){G.selTeam=G.selTeam===i?-1:i;renderTRows();}
function renderTRows(){document.getElementById('teamBtns').innerHTML=G.teams.map((t,i)=>`<div class="trow${i===G.selTeam?' win':''}" onclick="selTeam(${i})"><div class="trnm">${t.name}</div><div class="trsc">${t.score.toLocaleString()}</div><div class="awbdg">فائز +${G.selPts}</div></div>`).join('');}
function updateAQ(){
  const q=G.activeQ;
  document.getElementById('aqtxt').textContent=q?q.text:'اختر سؤالاً أو تجاوز';
  const a=document.getElementById('aqans');a.textContent=q?.answer?'الإجابة: '+q.answer:'';a.classList.remove('on');
  document.getElementById('aqpts').textContent=q?q.pts+' نقطة':'';
  document.getElementById('sendQBtn').textContent=G.showQ?'إخفاء من الشاشة':'إرسال للشاشة';
}
function toggleAns(){document.getElementById('aqans').classList.toggle('on');}
function pickQ(){
  const pool=[];G.cats.forEach(cat=>cat.questions.forEach((q,qi)=>{if(!q.used&&q.approved!==false)pool.push({catId:cat.id,qIdx:qi,...q});}));
  if(!pool.length){alert('لا توجد أسئلة غير مستخدمة');return;}
  const q=G.qOrder==='random'?pool[~~(Math.random()*pool.length)]:pool[0];
  G.activeQ={...q};updateAQ();pushBoards();
}
function toggleSendQ(){G.showQ=!G.showQ;document.getElementById('sendQBtn').textContent=G.showQ?'إخفاء من الشاشة':'إرسال للشاشة';pushBoards();}
function confirmNext(){
  if(G.selTeam<0){alert('اختر الفريق الفائز');return;}
  if(!AC){try{AC=new(window.AudioContext||window.webkitAudioContext)();}catch(e){}}
  if(AC.state==='suspended')AC.resume();
  stopT();
  const snap={ti:G.selTeam,pts:G.selPts,q:G.curQ,score:G.teams[G.selTeam].score,aq:G.activeQ?{...G.activeQ}:null};
  G.teams[G.selTeam].score+=G.selPts;G.lastWin=G.selTeam;G.lastPts=G.selPts;
  G.log.push({q:G.curQ,team:G.teams[G.selTeam].name,pts:G.selPts,_s:snap});
  if(G.activeQ){const cat=G.cats.find(c=>c.id===G.activeQ.catId);if(cat&&cat.questions[G.activeQ.qIdx])cat.questions[G.activeQ.qIdx].used=true;G.activeQ=null;G.showQ=false;}
  saveH();pushBoards();
  document.getElementById('flash').classList.add('on');setTimeout(()=>document.getElementById('flash').classList.remove('on'),380);
  sndWin();confetti();
  renderLive();goS('S_live');
}
function undoLast(){
  if(!G.log.length)return;
  const last=G.log.pop();const s=last._s;
  G.teams[s.ti].score=s.score;G.curQ=s.q;G.selTeam=-1;G.lastWin=-1;G.lastPts=0;
  if(s.aq){const cat=G.cats.find(c=>c.id===s.aq.catId);if(cat&&cat.questions[s.aq.qIdx])cat.questions[s.aq.qIdx].used=false;}
  clearCels();saveH();renderJudge();
}
function renderLog(){const el=document.getElementById('histLog');if(!G.log.length){el.innerHTML='<div class="empty">لا يوجد بعد</div>';return;}el.innerHTML=[...G.log].reverse().map(r=>`<div class="logitem"><span class="logq">س${r.q}</span><span class="logw">${r.team}</span><span class="logp">+${r.pts}</span></div>`).join('');}

/* ══════════════════════════════════════════
   PUSH BOARDS
══════════════════════════════════════════ */
function pushBoards(){
  if(document.getElementById('S_player').classList.contains('on'))renderPlayer();
  if(document.getElementById('S_display').classList.contains('on'))renderDisplay();
}

/* ══════════════════════════════════════════
   RANKINGS (FLIP)
══════════════════════════════════════════ */
function drawRankings(wrapId,ckey){
  const wrap=document.getElementById(wrapId);if(!wrap)return;
  const cels=RCELS[ckey];
  const sorted=[...G.teams].map((t,i)=>({...t,oi:i})).sort((a,b)=>b.score-a.score);
  const max=Math.max(...sorted.map(t=>t.score),1);
  wrap.style.height=(sorted.length*(CH+CG)-CG)+'px';
  const first=Object.keys(cels).length!==G.teams.length;
  if(first){
    wrap.innerHTML='';Object.keys(cels).forEach(k=>delete cels[k]);
    sorted.forEach((t,r)=>{const el=mkCard(t,r,max);el.style.top=(r*(CH+CG))+'px';wrap.appendChild(el);cels[t.oi]=el;});
    return;
  }
  const prev={};sorted.forEach(t=>{const el=cels[t.oi];if(el)prev[t.oi]=parseInt(el.style.top)||0;});
  sorted.forEach((t,r)=>{const el=cels[t.oi];if(el)updCard(el,t,r,max);});
  sorted.forEach(t=>{const el=cels[t.oi];if(!el)return;el.style.transition='none';el.style.top=(prev[t.oi]??0)+'px';});
  requestAnimationFrame(()=>requestAnimationFrame(()=>{
    sorted.forEach((t,r)=>{const el=cels[t.oi];if(!el)return;el.style.transition='top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s';el.style.top=(r*(CH+CG))+'px';});
  }));
  if(G.lastWin>=0&&cels[G.lastWin]){
    const el=cels[G.lastWin];el.querySelector('.fpts')?.remove();
    const fp=document.createElement('div');fp.className='fpts';fp.textContent='+'+G.lastPts;
    el.appendChild(fp);setTimeout(()=>fp.remove(),1300);
  }
}
function mkCard(t,r,max){const el=document.createElement('div');el.style.transition='top .85s cubic-bezier(.34,1.15,.64,1),box-shadow .35s,border-color .35s';updCard(el,t,r,max);return el;}
function updCard(el,t,r,max){
  const rc=r===0?'r1':r===1?'r2':r===2?'r3':'ro';
  el.className='rcard '+rc+(t.oi===G.lastWin?' hot':'');
  const pct=(t.score/max*100).toFixed(1);
  el.innerHTML=`<div class="rmed">${r+1}</div><div class="rnm">${t.name}</div><div class="rsc">${t.score.toLocaleString()}</div><div class="sbt"><div class="sbf" style="width:${pct}%"></div></div>`;
}

/* ══════════════════════════════════════════
   PLAYER
══════════════════════════════════════════ */
function renderPlayer(){
  document.getElementById('playerBrand').textContent=G.title;
  document.getElementById('playerName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('playerQ').textContent=G.curQ;
  document.getElementById('playerMeta').innerHTML=`السؤال <b>${G.curQ}</b>${G.group?' · '+G.group:''}`;
  const qb=document.getElementById('playerQBox');
  if(G.showQ&&G.activeQ){qb.classList.add('on');document.getElementById('playerQTxt').textContent=G.activeQ.text;}
  else{qb.classList.remove('on');}
  drawRankings('playerRankings','player');
  updateTimerUI();
}
function showPlayerHistory(){
  document.getElementById('playerHistory').style.display='block';
  document.getElementById('playerHistList').innerHTML=G.log.map(r=>`<div class="qhi"><div class="qhi-q">س${r.q}: ${r._s?.aq?.text||'—'}</div><div class="qhi-m">الفائز: <span class="qhi-w">${r.team}</span> · +${r.pts}</div></div>`).join('');
}

/* ══════════════════════════════════════════
   DISPLAY
══════════════════════════════════════════ */
function renderDisplay(){
  if(!G.id&&!getH().length)return;
  const h=getH();if(!G.id&&h.length)loadComp(h[0].id);
  document.getElementById('dispBrand').textContent=G.title||'شاشة العرض';
  document.getElementById('dispName').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('dispQ').textContent=G.curQ;
  const qb=document.getElementById('dispQBox');
  if(G.showQ&&G.activeQ){qb.classList.add('on');document.getElementById('dispQTxt').textContent=G.activeQ.text;}
  else{qb.classList.remove('on');}
  document.getElementById('dispTimer').textContent=fmt(G.tLeft);
  drawRankings('dispRankings','display');
}

/* ══════════════════════════════════════════
   LIVE
══════════════════════════════════════════ */
function renderLive(){
  document.getElementById('liveBrand').textContent=G.title;
  document.getElementById('liveNm').textContent=G.title+(G.group?' — '+G.group:'');
  document.getElementById('liveQ').textContent=G.curQ;
  document.getElementById('liveFooter').innerHTML=`<button class="btn b-grad" onclick="nextQ()">السؤال التالي →</button><button class="btn b-gh" onclick="doFinale()">إنهاء المسابقة</button>`;
  drawRankings('liveRankings','live');
}
function nextQ(){G.curQ++;G.selTeam=-1;G.lastWin=-1;G.lastPts=0;G.tLeft=G.tSecs;G.activeQ=null;G.showQ=false;renderJudge();goS('S_judge');}

/* ══════════════════════════════════════════
   FINALE
══════════════════════════════════════════ */
function doFinale(){
  G.done=true;saveH();
  const sorted=[...G.teams].sort((a,b)=>b.score-a.score);
  document.getElementById('finaleW').textContent=sorted[0]?.name||'—';
  const p3=sorted.slice(0,3);const ord=[1,0,2];
  document.getElementById('finalePodium').innerHTML=ord.map(i=>{if(!p3[i])return'';const cls=['p2','p1','p3'][i];const m=['🥈','🥇','🥉'][i];return`<div class="pi ${cls}"><div class="pb">${m}</div><div class="pn">${p3[i].name}</div><div class="ps">${p3[i].score.toLocaleString()}</div></div>`;}).join('');
  sndWin();confetti();setTimeout(confetti,800);
  goS('S_finale');
}
function toggleSummary(){
  const el=document.getElementById('summSec');el.style.display=el.style.display==='none'?'block':'none';
  document.getElementById('summTbl').innerHTML=`<tr>${['المرتبة','الفريق','النقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>${[...G.teams].sort((a,b)=>b.score-a.score).map((t,i)=>`<tr><td>${i+1}</td><td>${t.name}</td><td>${t.score.toLocaleString()}</td></tr>`).join('')}<tr><th colspan="3" style="padding-top:10px;">سجل الأسئلة</th></tr><tr>${['سؤال','الفائز','نقاط'].map(h=>`<th>${h}</th>`).join('')}</tr>${G.log.map(r=>`<tr><td>س${r.q}</td><td>${r.team}</td><td>+${r.pts}</td></tr>`).join('')}`;
}

/* ══════════════════════════════════════════
   BANK
══════════════════════════════════════════ */
function renderBank(judgeMode){
  document.getElementById('bankCatBtn').style.display=judgeMode?'flex':'none';
  document.getElementById('bankAIBtn').style.display=judgeMode?'flex':'none';
  // pending
  const pending=[];G.cats.forEach(cat=>cat.questions.forEach((q,qi)=>{if(q.approved===false)pending.push({catId:cat.id,qi,q});}));
  const ps=document.getElementById('pendingSec');
  if(judgeMode&&pending.length){
    ps.style.display='block';document.getElementById('pendCnt').textContent=pending.length;
    document.getElementById('pendList').innerHTML=pending.map(({catId,qi,q})=>`<div class="qitem qpend"><div class="qitxt"><div class="qitext">${q.text}</div>${q.answer?`<div class="qians">الإجابة: ${q.answer}</div>`:''}<div class="qipts">${q.pts} نقطة</div></div><div style="display:flex;flex-direction:column;gap:4px;"><button class="btn b-grn b-sm" onclick="approveQ('${catId}',${qi})">موافقة ✓</button><button class="btn b-rg b-sm" onclick="rejectQ('${catId}',${qi})">رفض</button></div></div>`).join('');
  }else ps.style.display='none';
  const el=document.getElementById('bankCats');
  if(!G.cats.length){el.innerHTML='<div class="empty">لا توجد تصنيفات</div>';return;}
  el.innerHTML=G.cats.map(cat=>{
    const appr=cat.questions.filter(q=>q.approved!==false);
    return `<div class="catbox" id="cb-${cat.id}"><div class="cathdr" onclick="togCat('${cat.id}')"><div class="cattl">${cat.name}</div><div class="catmt">${appr.length} سؤال · ${cat.questions.filter(q=>q.used).length} مستخدم</div>${judgeMode?`<div style="display:flex;gap:5px;"><button class="btn b-sm" style="background:rgba(79,70,229,.1);color:var(--a1);border:none;padding:4px 9px;" onclick="event.stopPropagation();openAI('${cat.id}')">✦ AI</button><button class="btn b-rg b-sm" onclick="event.stopPropagation();delCat('${cat.id}')">حذف</button></div>`:''}<div class="catarr">›</div></div><div class="catbody">${appr.map((q,qi)=>`<div class="qitem${q.used?' qused':''}"><div class="qitxt"><div class="qitext">${q.text}</div>${q.answer&&judgeMode?`<div class="qians">الإجابة: ${q.answer}</div>`:''}<div class="qipts">${q.pts} نقطة</div></div>${judgeMode?`<div style="display:flex;gap:3px;"><button class="btn b-gh b-sm" onclick="editQ('${cat.id}',${qi})">✎</button><button class="btn b-rg b-sm" onclick="delQ('${cat.id}',${qi})">✕</button></div>`:''}</div>`).join('')}${judgeMode?`<div class="addrow"><input type="text" placeholder="نص السؤال" id="qt-${cat.id}"><input type="text" placeholder="الإجابة" id="qa-${cat.id}" style="max-width:140px;"><select id="qp-${cat.id}">${G.pts.map(p=>`<option value="${p}">${p}</option>`).join('')}</select><button class="btn b-ind b-sm" onclick="addQ('${cat.id}')">اضافة</button></div>`:`<div class="addrow"><input type="text" placeholder="اقتراح سؤال" id="sqt-${cat.id}"><input type="text" placeholder="الإجابة" id="sqa-${cat.id}" style="max-width:130px;"><select id="sqp-${cat.id}">${G.pts.map(p=>`<option value="${p}">${p}</option>`).join('')}</select><button class="btn b-gh b-sm" onclick="suggestQ('${cat.id}')" style="padding:8px 9px;">اقتراح ↑</button></div>`}</div></div>`;
  }).join('');
  G.cats.forEach(c=>document.getElementById('cb-'+c.id)?.classList.add('open'));
}
function togCat(id){document.getElementById('cb-'+id)?.classList.toggle('open');}
function addCat(){const n=prompt('اسم التصنيف:');if(!n?.trim())return;G.cats.push({id:'c_'+Date.now(),name:n.trim(),questions:[]});renderBank(true);saveH();}
function delCat(id){if(!confirm('حذف التصنيف وأسئلته؟'))return;G.cats=G.cats.filter(c=>c.id!==id);renderBank(true);saveH();}
function addQ(cid){
  const cat=G.cats.find(c=>c.id===cid);if(!cat)return;
  const t=document.getElementById('qt-'+cid)?.value.trim();if(!t)return;
  const a=document.getElementById('qa-'+cid)?.value.trim();const p=parseInt(document.getElementById('qp-'+cid)?.value)||G.pts[0];
  cat.questions.push({id:'q_'+Date.now(),text:t,answer:a,pts:p,used:false,approved:true});
  document.getElementById('qt-'+cid).value='';document.getElementById('qa-'+cid).value='';
  renderBank(true);saveH();
}
function suggestQ(cid){
  const cat=G.cats.find(c=>c.id===cid);if(!cat)return;
  const t=document.getElementById('sqt-'+cid)?.value.trim();if(!t)return;
  const a=document.getElementById('sqa-'+cid)?.value.trim();const p=parseInt(document.getElementById('sqp-'+cid)?.value)||G.pts[0];
  cat.questions.push({id:'q_'+Date.now(),text:t,answer:a,pts:p,used:false,approved:false});
  document.getElementById('sqt-'+cid).value='';document.getElementById('sqa-'+cid).value='';
  alert('تم إرسال اقتراحك للمشرف للموافقة ✓');saveH();renderBank(false);
}
function approveQ(cid,qi){
  const cat=G.cats.find(c=>c.id===cid);if(!cat)return;
  const pending=cat.questions.filter(q=>q.approved===false);if(pending[qi])pending[qi].approved=true;
  renderBank(true);saveH();
}
function rejectQ(cid,qi){
  const cat=G.cats.find(c=>c.id===cid);if(!cat)return;
  const pending=cat.questions.filter(q=>q.approved===false);
  if(pending[qi]){const idx=cat.questions.indexOf(pending[qi]);cat.questions.splice(idx,1);}
  renderBank(true);saveH();
}
function delQ(cid,qi){const cat=G.cats.find(c=>c.id===cid);if(!cat)return;const appr=cat.questions.filter(q=>q.approved!==false);const real=cat.questions.indexOf(appr[qi]);if(real>=0)cat.questions.splice(real,1);renderBank(true);saveH();}
function editQ(cid,qi){const cat=G.cats.find(c=>c.id===cid);if(!cat)return;const appr=cat.questions.filter(q=>q.approved!==false);const q=appr[qi];if(!q)return;const nt=prompt('نص السؤال:',q.text);if(nt===null)return;const na=prompt('الإجابة:',q.answer||'');const np=parseInt(prompt('النقاط:',q.pts));q.text=nt||q.text;q.answer=na;if(!isNaN(np))q.pts=np;renderBank(true);saveH();}
function openBankJ(){bankJ=true;document.getElementById('bankCatBtn').style.display='flex';document.getElementById('bankAIBtn').style.display='flex';renderBank(true);goS('S_bank');}
function returnBank(){saveH();if(bankJ){renderJudge();goS('S_judge');}else goS('S_home');}

/* ══════════════════════════════════════════
   AI — Gemini 2.0 flash (free) or OpenAI
══════════════════════════════════════════ */
function aiProvChanged(){
  const p=document.getElementById('aiProv').value;
  document.getElementById('aiKeyHint').textContent=p==='gemini'?'(aistudio.google.com — مجاني)':'(platform.openai.com)';
  const saved=LS.g('aikey_'+p)||'';document.getElementById('aiKey').value=saved;
}
function openAI(cid){
  aiCatId=cid;const cat=cid?G.cats.find(c=>c.id===cid):null;
  document.getElementById('aiTopic').value=cat?cat.name:'';
  document.getElementById('aiRes').innerHTML='';
  aiProvChanged();openM('M_ai');
}
async function genAI(){
  const topic=document.getElementById('aiTopic').value.trim();if(!topic){alert('اكتب موضوعاً');return;}
  const cnt=document.getElementById('aiCnt').value;const lang=document.getElementById('aiLang').value;
  const prov=document.getElementById('aiProv').value;const key=document.getElementById('aiKey').value.trim();
  if(!key){alert('أدخل API Key');return;}
  LS.s('aikey_'+prov,key);
  const btn=document.getElementById('aiGenBtn');btn.textContent='جاري...';btn.disabled=true;
  document.getElementById('aiRes').innerHTML='<div class="empty">جاري التوليد...</div>';
  const ptsStr=G.pts.join(lang==='ar'?'،':',');
  const prompt=lang==='ar'
    ?`أنشئ ${cnt} أسئلة مسابقة عن "${topic}" باللغة العربية. أجب بـ JSON فقط، بدون أي نص إضافي، الشكل: [{"text":"...","answer":"...","pts":100}]. تنوع النقاط بين: ${ptsStr}`
    :`Create ${cnt} quiz questions about "${topic}". Reply ONLY with a JSON array, no markdown or extra text: [{"text":"...","answer":"...","pts":100}]. Vary points among: ${ptsStr}`;
  try{
    let qs;
    if(prov==='openai'){
      const r=await fetch('https://api.openai.com/v1/chat/completions',{method:'POST',headers:{'Content-Type':'application/json','Authorization':'Bearer '+key},body:JSON.stringify({model:'gpt-4o-mini',messages:[{role:'user',content:prompt}],temperature:.7})});
      const d=await r.json();if(!r.ok)throw new Error(d.error?.message||'OpenAI error');
      qs=JSON.parse(d.choices[0].message.content.replace(/```json|```/g,'').trim());
    }else{
      // Try Gemini models in order until one works
      const MODELS=['gemini-1.5-flash-latest','gemini-1.5-flash','gemini-1.5-pro','gemini-2.0-flash','gemini-pro'];
      let raw='',usedModel='',lastErr='';
      for(const m of MODELS){
        try{
          const r=await fetch(`https://generativelanguage.googleapis.com/v1beta/models/${m}:generateContent?key=${key}`,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({contents:[{parts:[{text:prompt}]}]})});
          const d=await r.json();
          if(!r.ok){lastErr=(d.error?.message||'error')+' ('+m+')';continue;}
          const t=d.candidates?.[0]?.content?.parts?.[0]?.text||'';
          if(t){raw=t;usedModel=m;break;}
        }catch(e){lastErr=e.message+' ('+m+')';continue;}
      }
      if(!raw)throw new Error(lastErr||'فشلت كل نماذج Gemini');
      document.getElementById('aiRes').insertAdjacentHTML('beforeend',`<div style="font-size:.71rem;color:var(--muted);padding:4px 0;">النموذج: ${usedModel}</div>`);
      qs=JSON.parse(raw.replace(/```json|```/g,'').trim());
    }
    if(!Array.isArray(qs))throw new Error('تنسيق غير صحيح');
    document.getElementById('aiRes').innerHTML=`<div style="background:rgba(79,70,229,.06);border:1.5px solid rgba(79,70,229,.18);border-radius:11px;padding:12px;"><div style="font-size:.8rem;font-weight:700;color:var(--a1);margin-bottom:8px;">✦ ${qs.length} أسئلة جاهزة</div>${qs.map((q,i)=>`<div style="display:flex;align-items:flex-start;gap:7px;background:var(--s1);border:1px solid var(--border);border-radius:8px;padding:8px 10px;margin-bottom:5px;"><div style="flex:1;"><div style="font-size:.85rem;line-height:1.5;">${q.text}</div>${q.answer?`<div style="font-size:.75rem;color:var(--green);font-weight:700;margin-top:2px;">الإجابة: ${q.answer}</div>`:''}</div><button class="btn b-grn b-sm" onclick="addAIQ(${i})">+ اضافة</button></div>`).join('')}<button class="btn b-ind b-sm" onclick="addAllAIQ()" style="width:100%;margin-top:5px;">إضافة الكل</button></div>`;
    document.getElementById('aiRes')._qs=qs;
  }catch(e){document.getElementById('aiRes').innerHTML=`<div class="empty" style="color:var(--red);">خطأ: ${e.message}</div>`;}
  btn.textContent='توليد الأسئلة';btn.disabled=false;
}
function addAIQ(i){
  const qs=document.getElementById('aiRes')._qs;if(!qs)return;const q=qs[i];
  const cat=aiCatId?G.cats.find(c=>c.id===aiCatId):G.cats[0];
  if(!cat){alert('أنشئ تصنيفاً أولاً');return;}
  const pts=G.pts.includes(q.pts)?q.pts:G.pts[0];
  cat.questions.push({id:'ai_'+Date.now()+'_'+i,text:q.text,answer:q.answer||'',pts,used:false,approved:true});
  renderBank(bankJ);saveH();
}
function addAllAIQ(){const qs=document.getElementById('aiRes')._qs;if(!qs)return;qs.forEach((_,i)=>addAIQ(i));}

/* ══════════════════════════════════════════
   JUDGE SETTINGS
══════════════════════════════════════════ */
function openJSettings(){jsTabI=0;jsTab(0);document.getElementById('jsTitleInp').value=G.title;document.getElementById('jsGroupInp').value=G.group;renderJSTeams();renderJSPts();openM('M_js');}
function jsTab(t){jsTabI=t;[0,1,2].forEach(i=>{document.getElementById('js'+i).style.display=i===t?'block':'none';});document.querySelectorAll('#M_js .tabbtn').forEach((b,i)=>b.classList.toggle('on',i===t));}
function renderJSTeams(){document.getElementById('jsTeamList').innerHTML=G.teams.map((t,i)=>`<div style="display:flex;align-items:center;gap:7px;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:7px 11px;margin-bottom:5px;"><span style="flex:1;font-weight:700;">${t.name}</span><span style="color:var(--gold);font-weight:900;font-size:.9rem;">${t.score}</span><button class="btn b-gh b-sm" onclick="openES(${i})">تعديل</button><button class="btn b-rg b-sm" onclick="jsDel(${i})">حذف</button></div>`).join('');}
function jsAddTeam(){const inp=document.getElementById('jsTeamInp');const n=inp.value.trim();if(!n)return;G.teams.push({name:n,score:0});inp.value='';clearCels();renderJSTeams();}
function jsDel(i){G.teams.splice(i,1);clearCels();renderJSTeams();}
function openES(i){esIdx=i;document.getElementById('esNm').textContent=G.teams[i].name;document.getElementById('esVal').value=G.teams[i].score;openM('M_es');}
function saveES(){const v=parseInt(document.getElementById('esVal').value);if(!isNaN(v)&&v>=0){G.teams[esIdx].score=v;clearCels();}closeM('M_es');renderJSTeams();}
function renderJSPts(){document.getElementById('jsPtsTags').innerHTML=G.pts.map((p,i)=>`<div class="ptag">${p}<button onclick="jsDelvPts(${i})">✕</button></div>`).join('');}
function jsAddPts(){const v=parseInt(document.getElementById('jsPtsInp').value);if(!v||v<10)return;if(!G.pts.includes(v)){G.pts.push(v);G.pts.sort((a,b)=>a-b);}document.getElementById('jsPtsInp').value='';renderJSPts();}
function jsDelvPts(i){if(G.pts.length<=1)return;G.pts.splice(i,1);renderJSPts();}
function saveJS(){const t=document.getElementById('jsTitleInp').value.trim();if(t)G.title=t;G.group=document.getElementById('jsGroupInp').value.trim();saveH();closeM('M_js');renderJudge();}

/* ══════════════════════════════════════════
   ADMIN
══════════════════════════════════════════ */
function admTab(t){admTabI=t;[0,1,2].forEach(i=>{document.getElementById('adm'+i).style.display=i===t?'block':'none';});document.querySelectorAll('#M_admin .tabbtn').forEach((b,i)=>b.classList.toggle('on',i===t));if(t===1)renderAdmHist();}
function renderAdmHist(){
  const h=getH();
  document.getElementById('admHistList').innerHTML=h.length
    ?h.map(r=>`<div style="display:flex;align-items:center;gap:8px;background:var(--s2);border:1px solid var(--border);border-radius:9px;padding:8px 11px;margin-bottom:5px;"><div style="flex:1;"><div style="font-weight:700;font-size:.87rem;">${r.title}</div><div style="font-size:.72rem;color:var(--muted);">س${r.curQ} · ${r.teams?.length} فرق${r.pin?' · رقم: '+r.pin:''} · ${new Date(r.saved).toLocaleDateString('ar-SA')}</div></div><button class="btn b-rg b-sm" onclick="delH(${r.id})">حذف</button></div>`).join('')
    :'<div class="empty">لا توجد مسابقات</div>';
}
function saveAdmin(){
  const n=document.getElementById('admNm').value.trim();if(n){LS.s('site',n);renderSite();}
  const np=String(document.getElementById('admNewPin').value).trim();if(np&&np.length>=4&&np.length<=6){LS.s('admPin',np);alert('تم تغيير رمز المشرف ✓');}
  closeM('M_admin');
}

/* ══════════════════════════════════════════
   CONFETTI
══════════════════════════════════════════ */
function confetti(){
  const cols=['#4f46e5','#7c3aed','#06b6d4','#10b981','#f97316','#d97706','#ec4899'];
  const c=document.getElementById('parts');
  for(let i=0;i<50;i++){const p=document.createElement('div');p.className='prt';const sz=5+Math.random()*9;p.style.cssText=`left:${Math.random()*100}vw;top:-12px;width:${sz}px;height:${sz}px;background:${cols[~~(Math.random()*cols.length)]};animation-duration:${.9+Math.random()*1.5}s;animation-delay:${Math.random()*.5}s;`;c.appendChild(p);setTimeout(()=>p.remove(),3200);}
}

/* ══════════════════════════════════════════
   INIT
══════════════════════════════════════════ */
renderSite();renderStats();
</script>
</body>
</html>
