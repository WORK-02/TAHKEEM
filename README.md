<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>لوحة التحكيم — مسابقة الثقلين</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap');
:root{
  --bg:#0f1923;--bg2:#162030;--bg3:#1e2d3d;--bg4:#253545;
  --border:rgba(255,255,255,0.07);--border2:rgba(255,255,255,0.16);
  --gold:#c9a84c;--gold2:#f0d080;--gold-bg:rgba(201,168,76,0.1);
  --text:#e8edf2;--text2:#8fa3b8;--text3:#4a6070;
  --green:#2ecc71;--green-bg:rgba(46,204,113,0.08);--green-border:rgba(46,204,113,0.25);
  --blue:#3498db;--blue-bg:rgba(52,152,219,0.08);
  --red:#e74c3c;--orange:#e67e22;--yellow:#f1c40f;
  --purple:#9b59b6;--purple-bg:rgba(155,89,182,0.1);
  --teal:#1abc9c;--teal-bg:rgba(26,188,156,0.1);
  --r:14px;--rs:8px;--r-lg:18px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Tajawal',sans-serif;background:var(--bg);color:var(--text);min-height:100vh}

/* ── LOGIN ── */
#login{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:2rem}
.lbox{background:var(--bg2);border:1px solid var(--border2);border-radius:var(--r-lg);padding:3rem 2.5rem;width:100%;max-width:420px;text-align:center}
.diamond{width:58px;height:58px;background:var(--gold);margin:0 auto 1.5rem;transform:rotate(45deg);border-radius:10px;display:flex;align-items:center;justify-content:center}
.diamond span{transform:rotate(-45deg);font-size:22px;font-weight:800;color:#0f1923}
.lbox h1{font-size:22px;font-weight:800;margin-bottom:6px}
.lbox p{font-size:14px;color:var(--text2);margin-bottom:2rem}
.lbox input{width:100%;padding:13px 16px;background:var(--bg3);border:1px solid var(--border2);border-radius:var(--rs);color:var(--text);font-size:16px;font-family:'Tajawal',sans-serif;text-align:right;outline:none;margin-bottom:1rem;transition:border-color .2s}
.lbox input:focus{border-color:var(--gold)}
.btn-primary{width:100%;padding:13px;background:var(--gold);border:none;border-radius:var(--rs);color:#0f1923;font-size:16px;font-weight:700;font-family:'Tajawal',sans-serif;cursor:pointer;transition:background .2s}
.btn-primary:hover{background:var(--gold2)}

/* ── TOP BAR ── */
#main{display:none}
.topbar{background:var(--bg2);border-bottom:1px solid var(--border);padding:.85rem 1.5rem;display:flex;align-items:center;justify-content:space-between;gap:1rem;flex-wrap:wrap;position:sticky;top:0;z-index:200}
.tb-left h2{font-size:15px;font-weight:800;color:var(--gold)}
.tb-left p{font-size:12px;color:var(--text3);margin-top:2px}
.tb-stats{display:flex;gap:1.5rem;font-size:13px;color:var(--text2)}
.tb-stats b{color:var(--text);font-weight:700}
.tb-btns{display:flex;gap:8px}
.btn-xs{padding:6px 14px;border-radius:var(--rs);border:1px solid var(--border2);background:transparent;color:var(--text2);font-size:13px;font-family:'Tajawal',sans-serif;cursor:pointer;transition:all .15s}
.btn-xs:hover{background:var(--bg3);color:var(--text)}
.btn-xs.gold{background:var(--gold);border-color:var(--gold);color:#0f1923;font-weight:700}
.btn-xs.gold:hover{background:var(--gold2)}

/* ── CONTENT ── */
.content{padding:1.5rem;max-width:920px;margin:0 auto}

/* ── SECTION HEADER ── */
.sec-hdr{display:flex;align-items:center;gap:12px;margin:2rem 0 1rem}
.sec-badge{background:var(--gold);color:#0f1923;font-size:13px;font-weight:800;padding:5px 16px;border-radius:20px;white-space:nowrap}
.sec-line{flex:1;height:1px;background:var(--border2)}

/* ── QUESTION CARD ── */
.qcard{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r);padding:1.5rem;margin-bottom:1rem;transition:border-color .2s}
.qcard.scored{border-color:rgba(201,168,76,.3)}

.qhead{display:flex;align-items:flex-start;gap:10px;margin-bottom:1.1rem}
.qnum{background:var(--bg4);border:1px solid var(--border2);border-radius:6px;padding:3px 11px;font-size:12px;font-weight:800;color:var(--gold);white-space:nowrap;flex-shrink:0}
.qtype-tag{background:var(--blue-bg);border:1px solid rgba(52,152,219,.2);border-radius:6px;padding:3px 11px;font-size:11px;color:var(--blue);white-space:nowrap;flex-shrink:0}
.qtext{font-size:15px;line-height:1.85;color:var(--text);flex:1}

/* ── REVEAL BOXES ── */
.ans-box{background:var(--green-bg);border:1px solid var(--green-border);border-radius:var(--rs);padding:14px 16px;font-size:14px;color:var(--text);line-height:1.9;margin-bottom:10px;display:none}
.ans-box.show{display:block}
.ans-box .ans-label{font-size:11px;font-weight:800;color:var(--green);margin-bottom:8px;letter-spacing:.05em}
.ans-box .ans-detail{color:var(--text2);font-size:13px;margin-top:8px;padding-top:8px;border-top:1px solid var(--green-border);line-height:1.8}

/* ── CARDS ROW ── */
.cards-section{margin-bottom:1rem}
.cards-label{font-size:11px;font-weight:800;color:var(--text3);letter-spacing:.05em;margin-bottom:8px}
.cards-grid{display:flex;flex-wrap:wrap;gap:7px}

.card-btn{
  display:flex;align-items:center;gap:6px;
  padding:7px 13px;border-radius:8px;
  border:1px solid var(--border2);background:transparent;
  color:var(--text2);font-size:12px;font-family:'Tajawal',sans-serif;
  cursor:pointer;transition:all .15s;white-space:nowrap
}
.card-btn:hover{background:var(--bg3);color:var(--text)}
.card-btn.active{color:var(--text)}
.card-btn .ci{font-size:13px}

.card-btn.c-ans{border-color:var(--green-border);color:var(--green)}
.card-btn.c-ans.active{background:var(--green-bg)}
.card-btn.c-hint{border-color:rgba(241,196,15,.25);color:var(--yellow)}
.card-btn.c-hint.active{background:rgba(241,196,15,.08)}
.card-btn.c-choices{border-color:rgba(52,152,219,.25);color:var(--blue)}
.card-btn.c-choices.active{background:var(--blue-bg)}
.card-btn.c-change{border-color:rgba(230,126,34,.25);color:var(--orange)}
.card-btn.c-change.active{background:rgba(230,126,34,.08)}
.card-btn.c-transfer{border-color:rgba(231,76,60,.25);color:var(--red)}
.card-btn.c-transfer.active{background:rgba(231,76,60,.08)}
.card-btn.c-double{border-color:rgba(155,89,182,.25);color:var(--purple)}
.card-btn.c-double.active{background:var(--purple-bg)}
.card-btn.c-audience{border-color:rgba(26,188,156,.25);color:var(--teal)}
.card-btn.c-audience.active{background:var(--teal-bg)}
.card-btn.c-time{border-color:rgba(46,204,113,.25);color:var(--green)}
.card-btn.c-time.active{background:var(--green-bg)}

.reveal{background:var(--bg3);border:1px solid var(--border);border-radius:var(--rs);padding:12px 15px;font-size:13px;color:var(--text2);margin-bottom:8px;display:none;line-height:1.85}
.reveal.show{display:block}
.reveal .rlbl{font-size:11px;font-weight:800;margin-bottom:6px;letter-spacing:.04em}

/* TIMER */
.timer-box{display:none;align-items:center;gap:12px;padding:10px 16px;background:var(--bg3);border:1px solid rgba(46,204,113,.25);border-radius:var(--rs);margin-bottom:8px}
.timer-box.show{display:flex}
.timer-num{font-size:26px;font-weight:800;color:var(--green);min-width:40px;text-align:center}
.timer-bar-bg{flex:1;height:5px;background:var(--bg4);border-radius:4px;overflow:hidden}
.timer-bar{height:100%;background:var(--green);border-radius:4px;transition:width 1s linear,background .3s}
.timer-stop{padding:5px 12px;border-radius:6px;border:1px solid rgba(46,204,113,.3);background:transparent;color:var(--green);font-size:12px;font-family:'Tajawal',sans-serif;cursor:pointer}

/* DOUBLE BADGE */
.double-badge{display:none;background:var(--purple-bg);border:1px solid rgba(155,89,182,.3);border-radius:6px;padding:5px 12px;font-size:12px;color:var(--purple);margin-bottom:8px;text-align:center}
.double-badge.show{display:block}

/* ── CONTROLS ── */
.controls{display:flex;gap:1.2rem;flex-wrap:wrap;align-items:flex-start;padding-top:1rem;border-top:1px solid var(--border);margin-top:.5rem}
.cg{display:flex;flex-direction:column;gap:6px}
.clbl{font-size:11px;color:var(--text3);font-weight:800;letter-spacing:.05em}
.grp-row{display:flex;gap:6px}
.grp-btn{padding:5px 14px;border-radius:6px;border:1px solid var(--border2);background:transparent;color:var(--text2);font-size:13px;font-family:'Tajawal',sans-serif;cursor:pointer;transition:all .15s}
.grp-btn:hover{background:var(--bg3)}
.grp-btn.on{background:var(--gold-bg);border-color:rgba(201,168,76,.4);color:var(--gold);font-weight:700}
.dots-row{display:flex;gap:5px}
.dot{width:32px;height:32px;border-radius:50%;border:1px solid var(--border2);background:transparent;color:var(--text2);font-size:13px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .15s;font-family:'Tajawal',sans-serif}
.dot:hover{background:var(--bg3)}
.dot[data-v="1"].on{background:rgba(231,76,60,.12);border-color:var(--red);color:var(--red)}
.dot[data-v="2"].on{background:rgba(230,126,34,.1);border-color:var(--orange);color:var(--orange)}
.dot[data-v="3"].on{background:rgba(241,196,15,.1);border-color:var(--yellow);color:var(--yellow)}
.dot[data-v="4"].on{background:rgba(46,204,113,.1);border-color:#27ae60;color:#27ae60}
.dot[data-v="5"].on{background:var(--gold-bg);border-color:var(--gold);color:var(--gold)}
.nt-area{flex:1;min-width:190px;display:flex;flex-direction:column;gap:5px}
.nt-area textarea{padding:9px 12px;background:var(--bg3);border:1px solid var(--border);border-radius:var(--rs);color:var(--text);font-size:13px;font-family:'Tajawal',sans-serif;resize:vertical;min-height:60px;outline:none;transition:border-color .15s;text-align:right}
.nt-area textarea:focus{border-color:var(--border2)}

/* ── RESULT SECTION ── */
.result-wrap{text-align:center;margin:1rem 0 1.5rem}
.btn-result{padding:9px 22px;border-radius:20px;border:1px solid var(--gold);background:var(--gold-bg);color:var(--gold);font-size:14px;font-weight:700;font-family:'Tajawal',sans-serif;cursor:pointer;transition:all .2s}
.btn-result:hover{background:var(--gold);color:#0f1923}
.result-panel{display:none;margin-top:1rem;background:var(--bg2);border:1px solid var(--border2);border-radius:var(--r);padding:1.5rem}
.result-panel.show{display:block}
.res-title{font-size:17px;font-weight:800;color:var(--text);text-align:center;margin-bottom:1.2rem}
.res-cards{display:grid;grid-template-columns:1fr 1fr;gap:1rem;margin-bottom:1.2rem}
.res-card{background:var(--bg3);border:1px solid var(--border);border-radius:var(--rs);padding:1.2rem;text-align:center}
.res-card-lbl{font-size:12px;color:var(--text3);font-weight:800;margin-bottom:.5rem;letter-spacing:.04em}
.res-card-val{font-size:30px;font-weight:800;color:var(--gold);line-height:1}
.res-card-sub{font-size:13px;color:var(--text2);margin-top:5px}
.pbar-bg{height:5px;background:var(--bg3);border-radius:4px;overflow:hidden;margin:1rem 0 .4rem}
.pbar-fill{height:100%;background:var(--gold);border-radius:4px;transition:width .5s ease}
.pbar-lbl{font-size:13px;color:var(--text2);text-align:center}
.res-list{margin-top:1rem}
.res-row{display:flex;align-items:center;gap:8px;padding:7px 12px;background:var(--bg3);border-radius:var(--rs);margin-bottom:5px;font-size:13px}
.res-row .rq{flex:1;color:var(--text2);padding-left:8px}
.res-row .rg{font-size:11px;color:var(--text3)}
.res-row .rs{font-weight:700;font-size:14px;min-width:32px;text-align:center}
.rs.v5{color:var(--gold)}.rs.v4{color:#27ae60}.rs.v3{color:var(--yellow)}.rs.v2{color:var(--orange)}.rs.v1{color:var(--red)}.rs.v0{color:var(--text3)}
.res-note{font-size:12px;color:var(--text3);text-align:center;margin-top:.5rem}

/* ── HISTORY ── */
.hist-wrap{margin-top:2rem;padding-top:2rem;border-top:1px solid var(--border)}
.hist-title{font-size:15px;font-weight:700;color:var(--text);margin-bottom:1rem;display:flex;align-items:center;gap:10px}
.hist-title::after{content:'';flex:1;height:1px;background:var(--border)}
.hcard{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r);padding:1.1rem;margin-bottom:8px;transition:border-color .15s}
.hcard:hover{border-color:var(--border2)}
.hcard-top{display:flex;align-items:center;justify-content:space-between;gap:1rem;flex-wrap:wrap;margin-bottom:6px}
.hcard-name{font-size:14px;font-weight:700;color:var(--text)}
.hcard-date{font-size:12px;color:var(--text3)}
.hcard-meta{font-size:13px;color:var(--text2);display:flex;gap:1.5rem;flex-wrap:wrap}
.hcard-meta b{color:var(--gold)}
.hdel{padding:3px 10px;border-radius:6px;border:1px solid rgba(231,76,60,.2);background:transparent;color:rgba(231,76,60,.5);font-size:12px;font-family:'Tajawal',sans-serif;cursor:pointer;transition:all .15s}
.hdel:hover{background:rgba(231,76,60,.08);color:var(--red);border-color:var(--red)}
.empty{text-align:center;padding:2rem;color:var(--text3);font-size:14px;border:1px dashed var(--border);border-radius:var(--r)}
</style>
</head>
<body>

<!-- LOGIN -->
<div id="login">
  <div class="lbox">
    <div class="diamond"><span>ث</span></div>
    <h1>مسابقة الثقلين</h1>
    <p>لوحة التحكيم — المجموعة الثالثة</p>
    <input type="text" id="jname" placeholder="اسم المحكم..." />
    <button class="btn-primary" onclick="start()">بدء التحكيم</button>
  </div>
</div>

<!-- MAIN -->
<div id="main">
  <div class="topbar">
    <div class="tb-left">
      <h2>مسابقة الثقلين — تحكيم</h2>
      <p id="jdisp"></p>
    </div>
    <div class="tb-stats">
      <div>مقيَّم: <b id="s-done">0</b>/<b id="s-tot">0</b></div>
      <div>المجموع: <b id="s-sum">0</b></div>
    </div>
    <div class="tb-btns">
      <button class="btn-xs" onclick="resetAll()">إعادة تعيين</button>
      <button class="btn-xs gold" onclick="saveSession()">حفظ التحكيم</button>
    </div>
  </div>
  <div class="content" id="content"></div>
</div>

<script>
/* ═══════════════════════════════════════
   DATA
═══════════════════════════════════════ */
var SECTIONS = [
{
  title:"المفردات", icon:"📖",
  questions:[
    {
      q:"معنى كلمة <b>أزِفَت</b> في قوله تعالى: ﴿أَزِفَتِ الْآزِفَةُ﴾ (النجم 57)",
      ans:"اقتربت ودنت",
      detail:"الآزفة: من أسماء القيامة، ومعناها الداهية القريبة.\nقال الطباطبائي في الميزان: أزفت أي دنت ولم يبق حتى تقوم إلا قليل.\nوالفعل أزِف يأزف: قرُب وضاق الوقت.",
      hint:"الفعل من مادة (أ-ز-ف) ويفيد القُرب الشديد",
      choices:"أ) بعُدت وتأخرت\nب) اقتربت ودنت ✓\nج) هلكت وانتهت\nد) اشتدت وعظُمت",
      type:"مفردات"
    },
    {
      q:"معنى كلمة <b>فَحَدِّث</b> في قوله تعالى: ﴿وَأَمَّا بِنِعْمَةِ رَبِّكَ فَحَدِّثْ﴾ (الضحى 11)",
      ans:"فأخبر وتكلم بالنعمة شكراً لله",
      detail:"التحديث بالنعمة: إظهارها والكلام عنها حمداً وشكراً.\nليس مجرد الإخبار، بل القصد: أن تُعلن نعم الله عليك.\nوفيه دلالة على أن إظهار النعمة عبادة وشكر لا فخر.",
      hint:"فعل أمر من التحديث — اذكر نعمة الله ولا تكتمها",
      choices:"أ) فاكتم وأخفِ النعمة\nب) فاشكر بالقلب فقط\nج) فأخبر وتكلم بالنعمة ✓\nد) فتصدق وأنفق",
      type:"مفردات"
    },
    {
      q:"معنى كلمة <b>دُسُر</b> في قوله تعالى: ﴿وَحَمَلْنَاهُ عَلَى ذَاتِ أَلْوَاحٍ وَدُسُرٍ﴾ (القمر 13)",
      ans:"المسامير والأوتاد التي تُثبَّت بها ألواح السفينة",
      detail:"الدُّسُر جمع دِسار: وهي المسامير الضخمة أو الحبال المبرومة التي تُشدّ بها ألواح السفينة.\nمجمع البيان للطبرسي: الدسر كل ما شُدّ وأحكم من مسمار أو خيط.\nوهي تدل على إحكام بناء سفينة نوح (ع).",
      hint:"تتعلق ببناء سفينة نوح وتثبيت ألواحها",
      choices:"أ) أشرعة السفينة\nب) مجاذيف السفينة\nج) المسامير التي تثبّت الألواح ✓\nد) قاع السفينة المتين",
      type:"مفردات"
    },
    {
      q:"معنى كلمة <b>ثَجَّاجًا</b> في قوله تعالى: ﴿وَأَنزَلْنَا مِنَ الْمُعْصِرَاتِ مَاءً ثَجَّاجًا﴾ (النبأ 14)",
      ans:"الماء الغزير الكثير المنصبّ بشدة وتدفق",
      detail:"ثجّاج: من ثجّ يثجّ أي سال بغزارة.\nوالمعصرات: السحب المثقلة بالماء على وشك المطر.\nأي ماء غزيراً متدفقاً لا ينقطع — وهو دليل على كمال النعمة الإلهية.",
      hint:"تصف كمية المطر وشدة تدفقه",
      choices:"أ) الماء الصافي النقي\nب) الماء الغزير المنصبّ بشدة ✓\nج) الماء البارد المثلّج\nد) الماء الملح المر",
      type:"مفردات"
    },
    {
      q:"معنى كلمة <b>كنود</b> في قوله تعالى: ﴿إِنَّ الْإِنسَانَ لِرَبِّهِ لَكَنُودٌ﴾ (العاديات 6)",
      ans:"الجحود الكفور لنعم الله — شديد الكفران",
      detail:"الكنود: صيغة مبالغة من الكنود أي الكفور بالنعمة المبالغ فيه.\nروي عن الإمام علي (ع): الكنود الذي يأكل وحده ويمنع رفده.\nوقيل: هو الذي يذكر المصائب وينسى النعم.",
      hint:"صفة ذم تتعلق بعدم الشكر على النعم",
      choices:"أ) الشاكر المخلص\nب) الظالم الغاشم\nج) الجاهل الغافل\nد) الجحود الكفور بالنعمة ✓",
      type:"مفردات"
    },
    {
      q:"معنى كلمة <b>رهواً</b> في قوله تعالى: ﴿وَاتْرُكِ الْبَحْرَ رَهْوًا﴾ (الدخان 24)",
      ans:"ساكناً ثابتاً منبسطاً — أي اتركه منفرجاً كما هو",
      detail:"رهواً: أي ساكناً هادئاً منفرجاً.\nأُمر موسى (ع) بعد عبوره البحر أن لا يُعيده بل يتركه مفتوحاً ليدخله فرعون وجنوده فيغرقوا.\nوفيه معنى الاطمئنان وعدم التعجل.",
      hint:"أمر لموسى بعد عبور البحر — اتركه كما هو",
      choices:"أ) متلاطماً عاصفاً\nب) ساكناً منبسطاً منفرجاً ✓\nج) عميقاً مظلماً\nد) باردة مياهه",
      type:"مفردات"
    },
    {
      q:"معنى كلمة <b>حنيفاً</b> في قوله تعالى: ﴿حَنِيفًا مُسْلِمًا﴾ (آل عمران 67)",
      ans:"مائلاً عن الشرك والباطل إلى التوحيد الخالص",
      detail:"الحنيف: من حنَف أي مال — والمقصود المائل عن الأديان الباطلة إلى الإسلام الخالص.\nوصف الله إبراهيم (ع) بأنه حنيف في مواضع عدة لأنه مال عن دين قومه إلى التوحيد.\nوالحنيفية هي الملة المستقيمة الخالصة من الشرك.",
      hint:"تصف إبراهيم (ع) — مائل عن الشرك نحو التوحيد",
      choices:"أ) مائلاً نحو الشرك\nب) شاكاً في عقيدته\nج) مائلاً عن الشرك إلى التوحيد ✓\nد) متشدداً في العبادة فقط",
      type:"مفردات"
    },
    {
      q:"معنى كلمة <b>ضِيزَى</b> في قوله تعالى: ﴿تِلْكَ إِذًا قِسْمَةٌ ضِيزَى﴾ (النجم 22)",
      ans:"جائرة ظالمة غير عادلة",
      detail:"ضيزى: صفة للمؤنث تعني الجور والظلم وعدم العدل.\nالسياق: ردٌّ على المشركين الذين ادّعوا أن لله البنات وهم يفضّلون البنين — فهذه قسمة ظالمة.\nوهي إدانة لمنطقهم المتناقض.",
      hint:"صفة تدل على الظلم — وردت رداً على منطق المشركين",
      choices:"أ) عادلة منصفة\nب) جائرة ظالمة ✓\nج) غريبة عجيبة\nد) قديمة موروثة",
      type:"مفردات"
    }
  ]
},
{
  title:"القصص", icon:"📚",
  questions:[
    {
      q:"قصة <b>أصحاب السبت</b>: من هم؟ وماذا فعلوا؟ وما عقوبتهم؟",
      ans:"قوم من بني إسرائيل حُرّم عليهم صيد السمك يوم السبت، فاحتالوا بوضع الشباك يوم الجمعة وأخذ السمك يوم الأحد، فمسخهم الله قردة خاسئين",
      detail:"القصة في سورة البقرة (65) والأعراف (163-166).\nكانوا في قرية على شاطئ البحر — قيل هي أيلة.\nحيلتهم: استغلال الثغرة الزمنية دون أن يمسّوا الحظر مباشرة.\nمنهم من نهى عن المنكر ومنهم من أقرّه ومنهم من ارتكبه — فنُجّي الناهون وعُوقب المعتدون.",
      hint:"قصة في البقرة والأعراف — احتيال على حكم الله",
      choices:"أ) مسخوا خنازير\nب) أُغرقوا في البحر\nج) ابتُلوا بالطاعون\nد) مسخوا قردة خاسئين ✓",
      type:"قصص"
    },
    {
      q:"في قوله تعالى: ﴿فَاسْتَغَاثَهُ الَّذِي مِن شِيعَتِهِ عَلَى الَّذِي مِن عَدُوِّهِ﴾ — من المقصود؟ وما الحادثة؟",
      ans:"رجل من بني إسرائيل طلب نصرة موسى على رجل قبطي، فضربه موسى فمات",
      detail:"السياق في سورة القصص (15): موسى دخل المدينة على حين غفلة من أهلها.\nرجل إسرائيلي يستغيث موسى ضد رجل قبطي (من قوم فرعون).\nموسى ضربه بقبضته ففاضت روحه — لم يقصد القتل.\nفكان ذلك سبب خروج موسى من مصر خوفاً.",
      hint:"القصص آية 15 — قبل رحلة موسى إلى مدين",
      choices:"أ) رجل طلب نصرة داوود على عدوه\nب) رجل طلب نصرة موسى فقتل القبطي ✓\nج) رجل طلب نصرة سليمان من الجن\nد) رجل طلب نصرة النبي من المنافقين",
      type:"قصص"
    },
    {
      q:"كيف بنى النبي إبراهيم (ع) الكعبة؟ ومن ساعده؟ وما الدعاء الذي رفعه أثناء البناء؟",
      ans:"بنى إبراهيم الكعبة مع ابنه إسماعيل بأمر الله — ورفعا الدعاء: ﴿رَبَّنَا تَقَبَّلْ مِنَّا إِنَّكَ أَنتَ السَّمِيعُ الْعَلِيمُ﴾",
      detail:"الآية: ﴿وَإِذْ يَرْفَعُ إِبْرَاهِيمُ الْقَوَاعِدَ مِنَ الْبَيْتِ وَإِسْمَاعِيلُ﴾ (البقرة 127).\nكان إبراهيم يضع الحجارة وإسماعيل يناوله إياها — دلالة على التعاون في طاعة الله.\nوأمر الله إبراهيم بأذان الحج بعد الفراغ من البناء.",
      hint:"البقرة 127 — أب وابنه يبنيان أقدس بيت",
      choices:"أ) بناها إبراهيم وحده بأمر الله\nب) بناها إبراهيم مع إسحاق\nج) بناها الملائكة وأشرف عليها إبراهيم\nد) بناها إبراهيم مع إسماعيل ✓",
      type:"قصص"
    },
    {
      q:"ما قصة لقاء موسى (ع) بشعيب (ع)؟ وكيف انتهت؟",
      ans:"هرب موسى إلى مدين بعد قتل القبطي، فسقى لابنتي شعيب من البئر، فدعاه شعيب وزوّجه إحدى ابنتيه على أن يرعى غنمه ثماني سنوات أو عشراً",
      detail:"القصص آيات 22-28.\nلقاء البئر: بنتان لا تستطيعان السقاية بسبب الرعاة — فتطوّع موسى وسقى لهما.\nالأب (شعيب) دعاه جزاءً على معروفه.\nالعقد: ﴿إِنِّي أُرِيدُ أَنْ أُنكِحَكَ إِحْدَى ابْنَتَيَّ عَلَى أَن تَأْجُرَنِي ثَمَانِيَ حِجَجٍ﴾.",
      hint:"القصص — بعد فرار موسى من مصر مباشرة",
      choices:"أ) موسى وصل وقاتل مع شعيب\nب) موسى علّم شعيب النبوة\nج) موسى سقى وتزوج ابنة شعيب ✓\nد) موسى رفض دعوة شعيب وعاد لمصر",
      type:"قصص"
    },
    {
      q:"ما قصة سليمان (ع) مع ملكة سبأ؟ وكيف أسلمت؟",
      ans:"أخبر الهدهد سليمان عن ملكة سبأ (بلقيس) وقومها يعبدون الشمس، فأرسل رسالة يدعوها للتوحيد، فأرسلت هدية فردّها، فجاءت وأسلمت",
      detail:"سورة النمل (20-44).\nمعجزات القصة: الهدهد رسولاً، نقل عرش بلقيس قبل أن ترتدّ إليها طرفة عين.\nعند رؤيتها العرش منقولاً قالت: ﴿إِنَّهُ عَرْشِي﴾.\nإسلامها: ﴿قَالَتْ رَبِّ إِنِّي ظَلَمْتُ نَفْسِي وَأَسْلَمْتُ مَعَ سُلَيْمَانَ لِلَّهِ رَبِّ الْعَالَمِينَ﴾.",
      hint:"النمل — الهدهد رسولاً وعرش بلقيس ينتقل",
      choices:"أ) سليمان حارب سبأ وهزمها عسكرياً\nب) بلقيس رفضت الإسلام وبقيت على دينها\nج) بلقيس أسلمت بعد رسالة سليمان ومعجزاته ✓\nد) سليمان تزوج بلقيس ثم أسلمت",
      type:"قصص"
    },
    {
      q:"كيف تسلّم الإمام الرضا (ع) ولاية العهد؟ وما الشروط التي اشترطها؟ وما موقفه الحقيقي منها؟",
      ans:"فرضها عليه المأمون العباسي سنة 201هـ مكرهاً، وقبلها بشرط ألا يعيّن ولا يعزل ولا يتدخل في الحكم، وأعلن أنه قبلها اضطراراً لا رغبة",
      detail:"المصدر: الإرشاد للمفيد، عيون أخبار الرضا.\nسبب قبوله: التهديد الضمني بالقتل لو رفض.\nقوله (ع) بعد القبول: 'اللهم إنك تعلم أنني أُكرهت، فلا تؤاخذني كما لم تؤاخذ يوسف ونبيك على ما أُكرها عليه'.\nكان القبول فيه مصلحة للشيعة: اكتساب شرعية وسعة للحركة.",
      hint:"الإرشاد للمفيد — قبول مكره بشروط واضحة",
      choices:"أ) طلب الإمام الولاية من المأمون\nب) رفض الإمام الولاية رفضاً تاماً\nج) قبلها مكرهاً بشروط عدم التدخل ✓\nد) قبلها بسرور لأنها تخدم الإسلام",
      type:"قصص"
    },
    {
      q:"ما قصة شعب أبي طالب؟ وكم امتدت؟ وما أثرها على النبي (ص) وأهل بيته؟",
      ans:"حاصرت قريش بني هاشم والنبي (ص) ثلاث سنوات، منعوا عنهم الطعام والتجارة وكتبوا صحيفة المقاطعة، حتى كانوا يأكلون أوراق الشجر ويسمع بكاء الأطفال من الجوع",
      detail:"المصدر: بحار الأنوار للمجلسي، السيرة النبوية.\nالمدة: 3 سنوات من سنة 7 إلى 10 من البعثة تقريباً.\nالصحيفة: علّقوها في الكعبة — وقيل أن الأرَضة أكلت كل بنودها إلا اسم الله.\nالأثر: وفاة السيدة خديجة وأبي طالب في هذه الفترة أو بعدها — وسُمّيت تلك السنة 'عام الحزن'.",
      hint:"بحار الأنوار — الحصار الاقتصادي ثلاث سنوات",
      choices:"أ) استمر سنة واحدة فقط\nب) استمر خمس سنوات\nج) استمر ثلاث سنوات ✓\nد) استمر سبع سنوات",
      type:"قصص"
    },
    {
      q:"ما قصة إخراج النبي آدم (ع) من الجنة؟ ومن تسبب في ذلك؟ وما موقف آدم بعدها؟",
      ans:"وسوس إبليس لآدم وحواء فأكلا من الشجرة المنهي عنها، فأُهبطا إلى الأرض — ثم تاب آدم فتاب الله عليه: ﴿فَتَلَقَّى آدَمُ مِن رَّبِّهِ كَلِمَاتٍ فَتَابَ عَلَيْهِ﴾",
      detail:"البقرة 35-37، الأعراف 19-25.\nالشجرة: لم يُحدَّد نوعها في القرآن — والتخمينات لا تستند لنص.\nالهبوط ليس عقوبة فحسب بل هو تحقيق لقوله تعالى: ﴿إِنِّي جَاعِلٌ فِي الْأَرْضِ خَلِيفَةً﴾.\nتوبة آدم: تعلّم كلمات من الله فتاب — وهذا يدل على أن باب التوبة مفتوح دائماً.",
      hint:"البقرة 36 — وسوسة إبليس ثم توبة آدم",
      choices:"أ) آدم خرج طوعاً من الجنة بطلبه\nب) ملائكة أخرجته تنفيذاً للأمر الإلهي\nج) إبليس وسوس فأكل من الشجرة ثم تاب ✓\nد) حواء وحدها هي التي أخطأت وآدم بريء",
      type:"قصص"
    }
  ]
},
{
  title:"عدّد", icon:"🔢",
  questions:[
    {
      q:"عدّد <b>مناسبات أهل البيت (ع) في شهر صفر</b> بتواريخها",
      ans:"1 صفر: دخول السبايا للشام\n7 صفر: شهادة الإمام الحسن (ع)\n20 صفر: زيارة الأربعين\n28 صفر: وفاة النبي (ص)\n29 صفر: شهادة الإمام الرضا (ع)",
      detail:"دخول السبايا: بعد وقعة كربلاء بأيام — السيدة زينب وآل البيت أسرى.\nشهادة الإمام الحسن: سنة 50هـ — مسموماً بتدبير معاوية.\nالأربعين: أول زيارة للإمام الحسين بعد أربعين يوماً من شهادته.\nوفاة النبي وشهادة الإمام الحسن: يتزامنان في 28 صفر.",
      hint:"ابدأ من أول الشهر — الشهر الذي يبدأ بالحزن",
      choices:"أ) مناسبتان فقط\nب) ثلاث مناسبات\nج) خمس مناسبات ✓\nد) سبع مناسبات",
      type:"عدّد"
    },
    {
      q:"عدّد <b>مناسبات أهل البيت (ع) في شهر شعبان</b> بتواريخها",
      ans:"3 شعبان: ولادة الإمام الحسين (ع)\n4 شعبان: ولادة العباس بن علي (ع)\n5 شعبان: ولادة الإمام زين العابدين (ع)\n11 شعبان: ولادة علي الأكبر (ع)\n15 شعبان: ولادة الإمام المهدي (عج)",
      detail:"شعبان شهر النور والمواليد المباركة.\nولادة الإمام الحسين: 3 شعبان 4هـ.\nولادة الإمام المهدي: 15 شعبان 255هـ بسامراء.\nيُعظَّم هذا الشهر خاصةً بصلوات الليالي البيض.",
      hint:"شعبان شهر المواليد المباركة — خمسة موالد عظام",
      choices:"أ) مولد الإمام الحسين فقط\nب) مولدان: الحسين والمهدي\nج) أربعة موالد\nد) خمسة موالد ✓",
      type:"عدّد"
    },
    {
      q:"عدّد <b>فروع الدين العشرة</b> عند الإمامية",
      ans:"1- الصلاة\n2- الصوم\n3- الحج\n4- الزكاة\n5- الخمس\n6- الجهاد\n7- الأمر بالمعروف\n8- النهي عن المنكر\n9- التولي\n10- التبري",
      detail:"الفرق بينها وبين أركان الإسلام عند السنة: إضافة الخمس والتولي والتبري.\nالتولي: محبة أهل البيت (ع) والتقرب إليهم.\nالتبري: التبرؤ من أعداء الله وأعداء أهل البيت.\nوهي واجبات عملية تُبنى على أصول الدين الخمسة.",
      hint:"تبدأ بالصلاة وتنتهي بالتولي والتبري",
      choices:"أ) خمسة فروع فقط\nب) سبعة فروع\nج) ثمانية فروع\nد) عشرة فروع ✓",
      type:"عدّد"
    },
    {
      q:"عدّد <b>عشر غزوات</b> من غزوات النبي (ص)",
      ans:"بدر — أحد — الخندق — بني قريظة — بني المصطلق — خيبر — الحديبية — حنين — تبوك — فتح مكة",
      detail:"إجمالي غزوات النبي (ص): قيل 27 غزوة، وقيل أكثر.\nالغزوة التي قاتل فيها النبي فعلياً: ابتداءً من بدر.\nتبوك: آخر الغزوات الكبرى ولم يقع فيها قتال.\nخرج النبي (ص) في الحديبية صلحاً ويُعدّ فتحاً مبيناً بنص القرآن.",
      hint:"ابدأ ببدر — أول الغزوات الكبرى",
      choices:"أ) ثلاث غزوات كبرى فقط\nب) خمس غزوات\nج) سبع غزوات\nد) عشر غزوات أو أكثر ✓",
      type:"عدّد"
    },
    {
      q:"عدّد <b>عشرة من أصحاب الإمام الحسين (ع)</b> في كربلاء",
      ans:"العباس بن علي — علي الأكبر — حبيب بن مظاهر — مسلم بن عوسجة — زهير بن القين — جون مولى أبي ذر — نافع بن هلال — الحر الرياحي — وهب الكلبي — عابس بن شبيب",
      detail:"الأصحاب كانوا نحو 72 رجلاً وفق أغلب الروايات.\nالحر الرياحي: كان قائداً في جيش يزيد ثم انضم للحسين (ع) فجراً — رمز التوبة.\nجون: مولى أبي ذر — وهو من الموالي الذين نالوا شرف الاستشهاد.\nمسلم بن عوسجة: أول من سقط في المعركة من الأصحاب.",
      hint:"ابدأ بأبرزهم: العباس وعلي الأكبر",
      choices:"أ) ثلاثة أصحاب مشهورين فقط\nب) خمسة أصحاب\nج) سبعة أصحاب\nد) عشرة أصحاب أو أكثر ✓",
      type:"عدّد"
    },
    {
      q:"عدّد <b>النساء المذكورات في القرآن الكريم</b> بأسمائهن أو أوصافهن",
      ans:"مريم — آسيا امرأة فرعون — أم موسى — امرأة العزيز — بلقيس — امرأة نوح — امرأة لوط — أم يحيى (إليصابات)",
      detail:"مريم: الوحيدة المذكورة باسمها صريحاً — وسورة كاملة باسمها.\nآسيا: ﴿وَضَرَبَ اللَّهُ مَثَلًا لِّلَّذِينَ آمَنُوا امْرَأَتَ فِرْعَوْنَ﴾.\nامرأة العزيز: تعلّقت بيوسف — ﴿وَرَاوَدَتْهُ الَّتِي هُوَ فِي بَيْتِهَا﴾.\nامرأتا نوح ولوط: ضُربتا مثلاً للكافرة في بيت نبي.",
      hint:"مريم باسمها صريح — والباقيات بوصفهن",
      choices:"أ) امرأة واحدة فقط (مريم)\nب) ثلاث نساء\nج) خمس نساء\nد) ثماني نساء أو أكثر ✓",
      type:"عدّد"
    },
    {
      q:"عدّد <b>المدن المذكورة في القرآن الكريم</b>",
      ans:"مكة (بكة) — المدينة — مصر — بابل — مدين — سبأ — إرم — سدوم",
      detail:"مكة: ذُكرت باسمها في الفتح (24) وباسم 'بكة' في آل عمران (96).\nإرم: ﴿إِرَمَ ذَاتِ الْعِمَادِ﴾ — مدينة عاد المشهورة بالعظمة.\nسبأ: مملكة بلقيس في اليمن — ﴿لَقَدْ كَانَ لِسَبَإٍ فِي مَسْكَنِهِمْ آيَةٌ﴾.\nبابل: ﴿وَمَا أُنزِلَ عَلَى الْمَلَكَيْنِ بِبَابِلَ﴾.",
      hint:"ابدأ بمكة المكرمة — ثم المدن الأخرى",
      choices:"أ) مكة والمدينة فقط\nب) أربع مدن\nج) ست مدن\nد) ثماني مدن أو أكثر ✓",
      type:"عدّد"
    },
    {
      q:"عدّد <b>عشرة من أسماء جهنم أو عذاباتها</b> كما وردت في القرآن الكريم",
      ans:"جهنم — السعير — الحطمة — النار — لظى — الجحيم — الهاوية — سقر — السموم — الغاشية",
      detail:"جهنم: الاسم الأكثر ذكراً في القرآن.\nالحطمة: ﴿وَمَا أَدْرَاكَ مَا الْحُطَمَةُ﴾ — تحطم كل شيء يُلقى فيها.\nالهاوية: ﴿فَأُمُّهُ هَاوِيَةٌ﴾ — تدل على السقوط البعيد.\nومن عذاباتها: الحميم والزقوم والغسلين والصديد.",
      hint:"الأسماء السبعة المشهورة: جهنم — السعير — الحطمة — لظى — الجحيم — الهاوية — سقر",
      choices:"أ) اسم واحد فقط\nب) ثلاثة أسماء\nج) خمسة أسماء\nد) سبعة أسماء وأكثر ✓",
      type:"عدّد"
    }
  ]
},
{
  title:"آيات الولاية", icon:"🌟",
  questions:[
    {
      q:"اذكر <b>آية الولاية</b> كاملةً — فيمن نزلت؟ وما القرينة الداخلية التي تخصّصها بشخص واحد؟",
      ans:"﴿إِنَّمَا وَلِيُّكُمُ اللَّهُ وَرَسُولُهُ وَالَّذِينَ آمَنُوا الَّذِينَ يُقِيمُونَ الصَّلَاةَ وَيُؤْتُونَ الزَّكَاةَ وَهُمْ رَاكِعُونَ﴾\nنزلت في الإمام علي (ع) حين تصدّق بخاتمه في الصلاة\nالقرينة: (وهم راكعون) لا تنطبق إلا على من تصدّق أثناء الصلاة",
      detail:"المائدة 55 — رواه الكافي والميزان وتفسير القمي.\nالحادثة: دخل سائل المسجد يطلب الصدقة، فأشار الإمام علي (ع) وهو راكع إلى خاتمه فأخذه السائل.\nإنما: أداة حصر تُضيّق الولاية وتُثبتها لأولياء بعينهم.\n(وهم راكعون): حال من المتصدق — وهو وصف لا ينطبق على جمع في آنٍ واحد، بل على فعل يوسف حدث مرة.",
      hint:"المائدة 55 — (إنما) أداة حصر + الركوع أثناء التصدق",
      choices:"أ) نزلت في عموم المؤمنين\nب) نزلت في يوم بدر\nج) نزلت في الإمام علي حين تصدق بخاتمه راكعاً ✓\nد) نزلت في أصحاب النبي العشرة",
      type:"آيات الولاية"
    },
    {
      q:"اذكر <b>آية المباهلة</b> — من خرج مع النبي (ص)؟ وما دلالة كلمة (أنفسنا) فيها؟",
      ans:"﴿فَقُلْ تَعَالَوْا نَدْعُ أَبْنَاءَنَا وَأَبْنَاءَكُمْ وَنِسَاءَنَا وَنِسَاءَكُمْ وَأَنفُسَنَا وَأَنفُسَكُمْ﴾\nخرج: علي وفاطمة والحسن والحسين\n(أنفسنا) تعني الإمام علي — فهو نفس النبي",
      detail:"آل عمران 61 — مباهلة نصارى نجران.\nنصارى نجران رفضوا الإسلام وتحدّوا النبي فنزلت الآية.\nخروج الأربعة وحدهم دليل على خصوصيتهم عند الله.\n(أنفسنا): من المستحيل أن يكون النبي نفسه المقصود — فلزم أن المراد نفسه من غيره، وهو علي (ع) باتفاق المفسرين.\nانسحب نصارى نجران دون مباهلة خوفاً.",
      hint:"آل عمران 61 — (أنفسنا) أي الأقرب لنفس النبي",
      choices:"أ) خرج النبي مع عشرة من الصحابة\nب) خرج النبي وحده\nج) خرج النبي مع أبي بكر وعمر\nد) خرج مع علي وفاطمة والحسن والحسين ✓",
      type:"آيات الولاية"
    },
    {
      q:"اذكر <b>آية التبليغ</b> — متى نزلت؟ وما الذي أُمر النبي (ص) بتبليغه؟ وما المقطع الذي يدل على خطورة الأمر؟",
      ans:"﴿يَا أَيُّهَا الرَّسُولُ بَلِّغْ مَا أُنزِلَ إِلَيْكَ مِن رَّبِّكَ وَإِن لَّمْ تَفْعَلْ فَمَا بَلَّغْتَ رِسَالَتَهُ﴾\nنزلت في غدير خم — يوم 18 ذي الحجة سنة 10هـ\nالمُبلَّغ: ولاية الإمام علي (ع)",
      detail:"المائدة 67 — رواه أغلب المفسرين في سبب النزول.\n(وإن لم تفعل فما بلّغت رسالته): يعني أن هذا الأمر بمثابة الرسالة كلها — وهذا يدل على عِظَمه.\n(والله يعصمك من الناس): تطمين للنبي من التبعات.\nغدير خم: واحة بين مكة والمدينة — تجمّع فيها مئة ألف حاج.",
      hint:"المائدة 67 — غدير خم — وإن لم تفعل فما بلّغت",
      choices:"أ) نزلت في تبليغ أحكام الزكاة\nب) نزلت في الهجرة إلى المدينة\nج) نزلت في تبليغ ولاية الإمام علي في غدير خم ✓\nد) نزلت في موقعة بدر",
      type:"آيات الولاية"
    },
    {
      q:"اذكر <b>آية التطهير</b> — فيمن نزلت؟ ولماذا يستدل بها أهل البيت (ع) على عصمتهم؟",
      ans:"﴿إِنَّمَا يُرِيدُ اللَّهُ لِيُذْهِبَ عَنكُمُ الرِّجْسَ أَهْلَ الْبَيْتِ وَيُطَهِّرَكُمْ تَطْهِيرًا﴾\nنزلت في أهل الكساء الخمسة: النبي وعلي وفاطمة والحسن والحسين\nإنما: حصر الإرادة الإلهية في إذهاب الرجس عنهم",
      detail:"الأحزاب 33 — حديث الكساء رواه أهل السنة والشيعة.\nالرجس: الذنب والنجاسة المعنوية — (إذهابه) يعني العصمة.\n(تطهيراً): مصدر مؤكد يدل على الكمال والتمام.\nحادثة الكساء: جمع النبي (ص) أهله تحت الكساء ودعا: 'اللهم هؤلاء أهل بيتي'.\nبناء على الآية: الأئمة مرجع معصوم لتفسير الدين.",
      hint:"الأحزاب 33 — (إنما) حصر + (إذهاب الرجس) = العصمة",
      choices:"أ) نزلت في نساء النبي فقط\nب) نزلت في عموم المسلمين\nج) نزلت في أهل الكساء الخمسة ✓\nد) نزلت في آل إبراهيم",
      type:"آيات الولاية"
    }
  ]
},
{
  title:"ما الفرق بين؟", icon:"⚖️",
  questions:[
    {
      q:"ما الفرق بين <b>الكتاب</b> و<b>القرآن</b> حين يُذكران معاً في القرآن الكريم؟",
      ans:"الكتاب: يشير إلى الوحي من حيث كونه مدوَّناً ومحفوظاً — الجانب التشريعي\nالقرآن: يشير إليه من حيث كونه مقروءاً ومتلوّاً — الجانب الأدائي",
      detail:"﴿وَنَزَّلْنَا عَلَيْكَ الْكِتَابَ تِبْيَاناً لِّكُلِّ شَيْءٍ﴾ — الكتاب للشمول والتفصيل.\n﴿إِنَّ هَذَا الْقُرْآنَ يَهْدِي لِلَّتِي هِيَ أَقْوَمُ﴾ — القرآن للهداية والتلاوة.\nويمكن القول: كل قرآن كتاب وليس العكس — إذ الكتاب أشمل يشمل سائر الكتب المنزلة.",
      hint:"أحدهما مكتوب تشريعي والآخر متلو أدائي",
      choices:"أ) لا فرق — هما اسمان لشيء واحد\nب) القرآن أقدم من الكتاب\nج) الكتاب التشريع المدوَّن والقرآن التلاوة ✓\nد) الكتاب أشمل ويتضمن القرآن وغيره",
      type:"ما الفرق؟"
    },
    {
      q:"ما الفرق بين <b>الغفران</b> و<b>العفو</b> في القرآن الكريم؟",
      ans:"الغفران: ستر الذنب مع عدم المؤاخذة — من الغفر بمعنى التغطية\nالعفو: محو الذنب وإسقاط أثره كلياً — والعفو أشمل وأعلى درجة",
      detail:"الغفران مأخوذ من (المغفر) وهو ما يُغطّى به الرأس — أي ستر الذنب بحيث لا يُرى.\nالعفو من (عفا الأثر) إذا زال — أي محو الذنب من السجل كلياً.\nلذلك يُعدّ العفو أعلى درجة: يمحو الذنب، والغفران يستره.\n﴿عَفَا اللَّهُ عَنكَ﴾ (التوبة 43) — محو وإسقاط.",
      hint:"الغفران ستر — العفو محو — أيهما أعلى؟",
      choices:"أ) هما بمعنى واحد تماماً\nب) الغفران أعلى من العفو\nج) الغفران ستر والعفو محو والعفو أعلى ✓\nد) العفو خاص بالدنيا والغفران بالآخرة",
      type:"ما الفرق؟"
    },
    {
      q:"ما الفرق بين <b>الظن</b> و<b>الشك</b> في القرآن الكريم؟",
      ans:"الظن: ترجيح أحد الاحتمالين على الآخر مع بقاء احتمال ضعيف للثاني\nالشك: تساوي الاحتمالين دون ترجيح لأيٍّ منهما",
      detail:"﴿إِن يَتَّبِعُونَ إِلَّا الظَّنَّ﴾ — الظن المذموم هو ما يُعتمد عليه بلا دليل.\nالشك: عدم الجزم في أي الجهتين — وهو مذموم في العقائد.\nوعند المنطقيين: اليقين > الظن > الشك.\nالظن قد يكون محموداً في الفقه (الظن الاطمئناني).",
      hint:"أيهما فيه ترجيح؟ وأيهما فيه تساوٍ؟",
      choices:"أ) هما بمعنى واحد\nب) الشك أقوى من الظن\nج) الظن ترجيح والشك تساوٍ ✓\nد) الظن خاص بالأمور الدينية فقط",
      type:"ما الفرق؟"
    },
    {
      q:"ما الفرق بين <b>الإنفاق</b> و<b>الصدقة</b> في القرآن الكريم؟",
      ans:"الإنفاق: أشمل — يشمل الواجب (كالنفقة على الأهل) والمستحب في كل وجوه الخير\nالصدقة: أخص — غالباً تطوعية تُعطى للفقراء تقرباً لله",
      detail:"﴿أَنفِقُوا مِمَّا رَزَقْنَاكُم﴾ — الإنفاق بمعناه الشامل.\n﴿وَأَقِيمُوا الصَّلَاةَ وَآتُوا الزَّكَاةَ﴾ — الزكاة من الإنفاق لكن بمعناه الواجب.\nالصدقة: من التطهر — ﴿خُذْ مِنْ أَمْوَالِهِمْ صَدَقَةً تُطَهِّرُهُمْ﴾ (التوبة 103).\nالصدقة تُطلق أحياناً على الزكاة الواجبة أيضاً في القرآن.",
      hint:"أيهما أشمل؟ وأيهما أخص بالفقراء؟",
      choices:"أ) الصدقة أشمل من الإنفاق\nب) لا فرق — هما متطابقان\nج) الإنفاق أشمل ويشمل الواجب والمستحب ✓\nد) الإنفاق خاص بالجهاد فقط",
      type:"ما الفرق؟"
    },
    {
      q:"ما الفرق بين <b>الذنب</b> و<b>المعصية</b> في القرآن الكريم؟",
      ans:"الذنب: ما يترتب عليه الذنب والعقاب — وصف للفعل من جهة أثره\nالمعصية: مخالفة أمر الله أو نهيه — وصف للفعل من جهة مصدره",
      detail:"الذنب مأخوذ من الذَّنَب أي الأثر والعاقبة — كأن صاحبه يجرّ وراءه عقوبة.\nالمعصية من العصيان أي الامتناع عن الطاعة.\nكل ذنب معصية وليس العكس دائماً — إذ بعض المعاصي قد تُكفَّر بلا عقاب.\nوالمعصية أعم لأنها تشمل الصغائر والكبائر.",
      hint:"الذنب من جهة العقاب — المعصية من جهة مخالفة الأمر",
      choices:"أ) هما مترادفان تماماً\nب) الذنب أشد من المعصية دائماً\nج) الذنب يرتبط بالعقاب والمعصية بمخالفة الأمر ✓\nد) المعصية خاصة بالكبائر",
      type:"ما الفرق؟"
    },
    {
      q:"ما الفرق بين <b>الخوف</b> و<b>الخشية</b> في القرآن الكريم؟ واذكر الآية الدالة",
      ans:"الخوف: توقع الضرر — يعتري أي شخص حتى بلا معرفة\nالخشية: خوف مقرون بالمعرفة والتعظيم — لا تكون إلا لمن عرف\n﴿إِنَّمَا يَخْشَى اللَّهَ مِنْ عِبَادِهِ الْعُلَمَاءُ﴾",
      detail:"فاطر 28 — الآية تربط الخشية بالعلم ربطاً مباشراً.\nالخوف من الأسد خوف — لكن خشية الله معرفة بعظمته وعلمٌ بحقيقته.\nلذلك: الخشية أرقى مرتبة — وخشية العالم لله أعلى من خوف الجاهل منه.\nوفيها إشارة إلى أن العلم يزيد الخشية لا العكس.",
      hint:"أيهما مقترن بالعلم؟ فاطر 28",
      choices:"أ) هما بمعنى واحد\nب) الخوف أشد دائماً\nج) الخشية أخص وتقترن بالعلم والتعظيم ✓\nد) الخوف خاص بعذاب الآخرة",
      type:"ما الفرق؟"
    }
  ]
},
{
  title:"قارن", icon:"↔️",
  questions:[
    {
      q:"قارن بين موقف <b>الإمام الحسن (ع)</b> و<b>الإمام الحسين (ع)</b> من السلطة الأموية — لماذا اختلف موقفهما رغم أن كليهما كان يرفع الباطل؟",
      ans:"الإمام الحسن: الصلح لحفظ الشيعة وحقن الدماء — الجيش تفكّك وأُعدّت المؤامرات\nالإمام الحسين: الثورة لأن الموافقة على يزيد تعني إضفاء الشرعية على الفسق\nكلاهما فعل تكليفه الزماني",
      detail:"فرق الظروف:\n• الحسن (ع) واجه جيشاً تفكّك وأُقيمت المؤامرات لاغتياله — الصلح هو الخيار الأهون.\n• الحسين (ع) واجه مطالبةً صريحةً بالبيعة ليزيد — بشاربٍ للخمر راتك الحرمات.\nكلمة الحسين الشهيرة: 'هيهات منّا الذلة' — الذل هو بيعة الفاسق.\nالصلح لم يكن استسلاماً بل تكتيكاً لحفظ البنية الشيعية.",
      hint:"الفرق في الظروف لا في القيم — كلاهما رفض الباطل",
      choices:"أ) كلاهما اختار الثورة لكن الحسن فشل\nب) الحسن اختار الصلح والحسين الثورة لأن الظروف اختلفت ✓\nج) كلاهما اختار الصلح\nد) الحسين عصى أخاه الحسن بقيامه",
      type:"قارن"
    },
    {
      q:"قارن بين أسلوب <b>الإمام الصادق (ع)</b> و<b>الإمام الكاظم (ع)</b> في نشر العلم — وما السبب؟",
      ans:"الإمام الصادق: نشر العلم علناً — المدرسة الجعفرية — أكثر من 4000 تلميذ\nالإمام الكاظم: نشر العلم سراً عبر الوكلاء — بسبب القمع العباسي وسنوات السجن",
      detail:"الصادق (ع): استغل الفترة الانتقالية بين الأمويين والعباسيين — فنشر علوم الفقه والكيمياء والكلام.\nمن تلاميذه: جابر بن حيان (أبو الكيمياء)، هشام بن الحكم، مؤمن الطاق.\nالكاظم (ع): اعتُقل في سجن هارون الرشيد سنوات — ومع ذلك واصل التعليم عبر رسائل الوكلاء.\nقوله (ع) وهو في السجن: 'اللهم إنك تعلم أنني كنت أسألك أن تفرّغني لعبادتك — اللهم قد فعلت'.",
      hint:"الصادق بالانفتاح السياسي — الكاظم بالصبر على القمع",
      choices:"أ) كلاهما نشرا العلم سراً فقط\nب) كلاهما نشرا علناً وبنفس الأسلوب\nج) الصادق علناً بالمدرسة الجعفرية والكاظم سراً ✓\nد) الكاظم نشر أكثر من الصادق رغم السجن",
      type:"قارن"
    }
  ]
}
];

/* ═══════════════════════════════════════
   STATE
═══════════════════════════════════════ */
var scores={}, groups={}, notes={}, doubled={}, judgeName="", sessions=[];
var timerIntervals={};
try{sessions=JSON.parse(localStorage.getItem('tq3v3')||'[]');}catch(e){sessions=[];}

var allQ=[];
SECTIONS.forEach(function(s,si){s.questions.forEach(function(q,qi){allQ.push({si:si,qi:qi});});});

/* ═══════════════════════════════════════
   START
═══════════════════════════════════════ */
function start(){
  var n=document.getElementById('jname').value.trim();
  if(!n){alert('الرجاء إدخال اسم المحكم');return;}
  judgeName=n;
  document.getElementById('login').style.display='none';
  document.getElementById('main').style.display='block';
  document.getElementById('jdisp').textContent='المحكم: '+judgeName;
  document.getElementById('s-tot').textContent=allQ.length;
  buildAll();renderHist();
}

/* ═══════════════════════════════════════
   BUILD
═══════════════════════════════════════ */
function buildAll(){
  var c=document.getElementById('content');c.innerHTML='';
  var idx=0;
  SECTIONS.forEach(function(sec,si){
    var sh=document.createElement('div');sh.className='sec-hdr';
    sh.innerHTML='<span class="sec-badge">'+sec.icon+' '+sec.title+'</span><div class="sec-line"></div>';
    c.appendChild(sh);

    sec.questions.forEach(function(q,qi){
      c.appendChild(buildCard(q,idx,si));idx++;
    });

    // Result button
    var rw=document.createElement('div');rw.className='result-wrap';
    rw.innerHTML=
      '<button class="btn-result" onclick="toggleResult(\'rp-'+si+'\')">◆ عرض نتيجة قسم '+sec.title+'</button>'+
      '<div class="result-panel" id="rp-'+si+'"></div>';
    c.appendChild(rw);
  });

  var hw=document.createElement('div');hw.className='hist-wrap';
  hw.innerHTML='<div class="hist-title">النسخ المحفوظة</div><div id="hlist"></div>';
  c.appendChild(hw);
}

function buildCard(q,idx,si){
  var card=document.createElement('div');
  card.className='qcard';card.id='qc-'+idx;

  var dotsH=[1,2,3,4,5].map(function(n){
    return '<div class="dot" data-v="'+n+'" onclick="setScore('+idx+','+n+',this)">'+n+'</div>';
  }).join('');

  card.innerHTML=
    '<div class="qhead">'+
      '<span class="qnum">س'+(idx+1)+'</span>'+
      '<div class="qtext">'+q.q+'</div>'+
      '<span class="qtype-tag">'+q.type+'</span>'+
    '</div>'+

    /* ANSWER */
    '<div class="ans-box" id="ab-'+idx+'">'+
      '<div class="ans-label">الجواب</div>'+
      q.ans.replace(/\n/g,'<br>')+
      '<div class="ans-detail">'+q.detail.replace(/\n/g,'<br>')+'</div>'+
    '</div>'+

    /* DOUBLE BADGE */
    '<div class="double-badge" id="db-'+idx+'">◆ مضاعفة النقاط مفعّلة</div>'+

    /* TIMER */
    '<div class="timer-box" id="tb-'+idx+'">'+
      '<span style="font-size:12px;color:var(--text2)">وقت إضافي</span>'+
      '<div class="timer-num" id="tn-'+idx+'">60</div>'+
      '<div class="timer-bar-bg"><div class="timer-bar" id="tbar-'+idx+'" style="width:100%"></div></div>'+
      '<button class="timer-stop" onclick="stopTimer('+idx+')">إيقاف</button>'+
    '</div>'+

    /* CARDS */
    '<div class="cards-section">'+
      '<div class="cards-label">البطاقات</div>'+
      '<div class="cards-grid">'+
        '<button class="card-btn c-ans" id="cb-ans-'+idx+'" onclick="togRev(\'ab-'+idx+'\',\'cb-ans-'+idx+'\')"><span class="ci">✅</span>إظهار الجواب</button>'+
        '<button class="card-btn c-hint" id="cb-hint-'+idx+'" onclick="togRev(\'rev-h-'+idx+'\',\'cb-hint-'+idx+'\')"><span class="ci">💡</span>تلميح بسيط</button>'+
        '<button class="card-btn c-choices" id="cb-cho-'+idx+'" onclick="togRev(\'rev-c-'+idx+'\',\'cb-cho-'+idx+'\')"><span class="ci">🔠</span>طلب الخيارات</button>'+
        '<button class="card-btn c-change" onclick="markUsed(this,\'تغيير السؤال\')"><span class="ci">🔄</span>تغيير السؤال</button>'+
        '<button class="card-btn c-transfer" onclick="markUsed(this,\'تحويل للفريق\')"><span class="ci">↩️</span>تحويل للفريق الآخر</button>'+
        '<button class="card-btn c-double" id="cb-dbl-'+idx+'" onclick="toggleDouble('+idx+')"><span class="ci">✖️</span>مضاعفة النقاط</button>'+
        '<button class="card-btn c-audience" onclick="markUsed(this,\'مساعدة الجمهور\')"><span class="ci">👥</span>مساعدة الجمهور</button>'+
        '<button class="card-btn c-time" onclick="startTimer('+idx+')"><span class="ci">⏱</span>وقت إضافي</button>'+
      '</div>'+
    '</div>'+

    /* REVEALS */
    '<div class="reveal" id="rev-h-'+idx+'"><div class="rlbl" style="color:var(--yellow)">تلميح</div>'+q.hint+'</div>'+
    '<div class="reveal" id="rev-c-'+idx+'"><div class="rlbl" style="color:var(--blue)">الخيارات</div>'+q.choices.replace(/\n/g,'<br>')+'</div>'+

    /* CONTROLS */
    '<div class="controls">'+
      '<div class="cg">'+
        '<div class="clbl">المجموعة</div>'+
        '<div class="grp-row" id="gr-'+idx+'">'+
          '<button class="grp-btn" onclick="setGrp('+idx+',\'1\')">الأولى</button>'+
          '<button class="grp-btn" onclick="setGrp('+idx+',\'2\')">الثانية</button>'+
        '</div>'+
      '</div>'+
      '<div class="cg">'+
        '<div class="clbl">الدرجة من 5</div>'+
        '<div class="dots-row" id="dt-'+idx+'">'+dotsH+'</div>'+
      '</div>'+
      '<div class="nt-area cg">'+
        '<div class="clbl">ملاحظات</div>'+
        '<textarea id="nt-'+idx+'" placeholder="ملاحظة اختيارية..." oninput="notes['+idx+']=this.value"></textarea>'+
      '</div>'+
    '</div>';

  return card;
}

/* ═══════════════════════════════════════
   INTERACTIONS
═══════════════════════════════════════ */
function togRev(revId,btnId){
  var el=document.getElementById(revId);
  var btn=document.getElementById(btnId);
  if(!el)return;
  var on=el.classList.toggle('show');
  if(btn)btn.classList.toggle('active',on);
}

function markUsed(btn,lbl){
  btn.classList.toggle('active');
  if(btn.classList.contains('active')){
    btn.style.opacity='.5';
    btn.title='تم استخدام: '+lbl;
  } else {
    btn.style.opacity='';
    btn.title='';
  }
}

function toggleDouble(idx){
  doubled[idx]=!doubled[idx];
  var btn=document.getElementById('cb-dbl-'+idx);
  var badge=document.getElementById('db-'+idx);
  if(btn)btn.classList.toggle('active',doubled[idx]);
  if(badge)badge.classList.toggle('show',doubled[idx]);
  updateStats();
}

function startTimer(idx){
  if(timerIntervals[idx])return;
  var box=document.getElementById('tb-'+idx);
  var num=document.getElementById('tn-'+idx);
  var bar=document.getElementById('tbar-'+idx);
  if(box)box.classList.add('show');
  var secs=60;
  timerIntervals[idx]=setInterval(function(){
    secs--;
    if(num)num.textContent=secs;
    if(bar)bar.style.width=(secs/60*100)+'%';
    if(secs<=10&&bar){bar.style.background='var(--red)';}
    if(secs<=0){stopTimer(idx);}
  },1000);
}

function stopTimer(idx){
  if(timerIntervals[idx]){clearInterval(timerIntervals[idx]);delete timerIntervals[idx];}
  var box=document.getElementById('tb-'+idx);
  var num=document.getElementById('tn-'+idx);
  var bar=document.getElementById('tbar-'+idx);
  if(box)box.classList.remove('show');
  if(num)num.textContent='60';
  if(bar){bar.style.width='100%';bar.style.background='var(--green)';}
}

function setScore(idx,n,el){
  scores[idx]=n;
  var card=document.getElementById('qc-'+idx);
  if(card)card.classList.add('scored');
  var row=document.getElementById('dt-'+idx);
  if(row)row.querySelectorAll('.dot').forEach(function(d){d.classList.toggle('on',parseInt(d.dataset.v)===n);});
  updateStats();
}

function setGrp(idx,g){
  groups[idx]=g;
  var row=document.getElementById('gr-'+idx);
  if(row)row.querySelectorAll('.grp-btn').forEach(function(b,j){b.classList.toggle('on',String(j+1)===g);});
}

function updateStats(){
  var done=Object.keys(scores).length;
  var sum=0;
  Object.keys(scores).forEach(function(k){
    var s=scores[k];
    sum+=doubled[k]?s*2:s;
  });
  document.getElementById('s-done').textContent=done;
  document.getElementById('s-sum').textContent=sum+' / '+(done*5);
}

/* ═══════════════════════════════════════
   RESULT
═══════════════════════════════════════ */
function toggleResult(panelId){
  var panel=document.getElementById(panelId);
  var si=parseInt(panelId.replace('rp-',''));
  if(panel.classList.contains('show')){panel.classList.remove('show');panel.innerHTML='';return;}

  var offset=0;
  for(var i=0;i<si;i++)offset+=SECTIONS[i].questions.length;

  var g1t=0,g1m=0,g2t=0,g2m=0,unscore=0;
  var rows='';

  SECTIONS[si].questions.forEach(function(q,qi){
    var idx=offset+qi;
    var sc=scores[idx];
    var gr=groups[idx];
    var nt=notes[idx]||'';
    var isDbl=doubled[idx];
    var dispSc=sc!==undefined?(isDbl?sc+'×2='+(sc*2):sc+'/5'):'—';
    var cls=sc!==undefined?'v'+sc:'v0';
    if(sc===undefined){unscore++;}
    else{
      var effective=isDbl?sc*2:sc;
      var maxEff=isDbl?10:5;
      if(gr==='1'){g1t+=effective;g1m+=maxEff;}
      else if(gr==='2'){g2t+=effective;g2m+=maxEff;}
    }
    rows+='<div class="res-row">'+
      '<span class="qnum" style="flex-shrink:0">س'+(idx+1)+'</span>'+
      '<span class="rq">'+q.q.replace(/<[^>]+>/g,'').substring(0,55)+'...</span>'+
      '<span class="rg">'+(gr?'مج'+gr:'—')+'</span>'+
      (isDbl?'<span style="font-size:11px;color:var(--purple)">×2</span>':'')+
      '<span class="rs '+cls+'">'+dispSc+'</span>'+
    '</div>';
  });

  var totalT=g1t+g2t,totalM=g1m+g2m;
  var pct=totalM?Math.round(totalT/totalM*100):0;
  var p1=g1m?Math.round(g1t/g1m*100):0;
  var p2=g2m?Math.round(g2t/g2m*100):0;

  panel.innerHTML=
    '<div class="res-title">نتيجة: '+SECTIONS[si].icon+' '+SECTIONS[si].title+'</div>'+
    '<div class="res-cards">'+
      '<div class="res-card">'+
        '<div class="res-card-lbl">المجموعة الأولى</div>'+
        '<div class="res-card-val">'+g1t+'<span style="font-size:14px;color:var(--text2)">/'+g1m+'</span></div>'+
        '<div class="res-card-sub">'+g1m/5+' سؤال — '+p1+'%</div>'+
      '</div>'+
      '<div class="res-card">'+
        '<div class="res-card-lbl">المجموعة الثانية</div>'+
        '<div class="res-card-val">'+g2t+'<span style="font-size:14px;color:var(--text2)">/'+g2m+'</span></div>'+
        '<div class="res-card-sub">'+g2m/5+' سؤال — '+p2+'%</div>'+
      '</div>'+
    '</div>'+
    '<div class="pbar-bg"><div class="pbar-fill" id="pfill-'+si+'" style="width:0"></div></div>'+
    '<div class="pbar-lbl">الإجمالي: '+totalT+' / '+totalM+' ('+pct+'%)</div>'+
    (unscore?'<div class="res-note">⚠ '+unscore+' سؤال لم يُقيَّم</div>':'')+
    '<div class="res-list">'+rows+'</div>';

  panel.classList.add('show');
  setTimeout(function(){
    var pf=document.getElementById('pfill-'+si);
    if(pf)pf.style.width=pct+'%';
  },100);
}

/* ═══════════════════════════════════════
   SAVE / HISTORY
═══════════════════════════════════════ */
function saveSession(){
  var done=Object.keys(scores).length;
  if(!done){alert('لم يتم تقييم أي سؤال');return;}
  var sum=0;
  Object.keys(scores).forEach(function(k){sum+=doubled[k]?scores[k]*2:scores[k];});
  var s={
    judge:judgeName,
    date:new Date().toLocaleString('ar-SA'),
    scores:Object.assign({},scores),
    groups:Object.assign({},groups),
    notes:Object.assign({},notes),
    doubled:Object.assign({},doubled),
    total:sum,done:done,max:done*5
  };
  sessions.unshift(s);
  try{localStorage.setItem('tq3v3',JSON.stringify(sessions));}catch(e){}
  renderHist();alert('تم الحفظ ✓');
}

function resetAll(){
  if(!confirm('إعادة تعيين جميع الدرجات؟'))return;
  scores={};groups={};notes={};doubled={};
  Object.keys(timerIntervals).forEach(stopTimer);
  buildAll();updateStats();renderHist();
}

function delSession(i){
  if(!confirm('حذف هذه النسخة؟'))return;
  sessions.splice(i,1);
  try{localStorage.setItem('tq3v3',JSON.stringify(sessions));}catch(e){}
  renderHist();
}

function renderHist(){
  var el=document.getElementById('hlist');if(!el)return;
  if(!sessions.length){el.innerHTML='<div class="empty">لا توجد نسخ محفوظة بعد</div>';return;}
  el.innerHTML=sessions.map(function(s,i){
    var pct=s.max?Math.round(s.total/s.max*100):0;
    var nts=Object.entries(s.notes||{}).filter(function(x){return x[1];}).map(function(x){return '<span style="font-size:12px;color:var(--text3);display:block;margin-top:2px">س'+(+x[0]+1)+': '+x[1]+'</span>';}).join('');
    return '<div class="hcard">'+
      '<div class="hcard-top">'+
        '<span class="hcard-name">◆ '+s.judge+'</span>'+
        '<div style="display:flex;gap:8px;align-items:center">'+
          '<span class="hcard-date">'+s.date+'</span>'+
          '<button class="hdel" onclick="delSession('+i+')">حذف</button>'+
        '</div>'+
      '</div>'+
      '<div class="hcard-meta">'+
        '<div>مقيَّم: <b>'+s.done+'</b> سؤال</div>'+
        '<div>المجموع: <b>'+s.total+'</b>/'+s.max+'</div>'+
        '<div>النسبة: <b>'+pct+'%</b></div>'+
      '</div>'+
      (nts?'<div style="margin-top:6px">'+nts+'</div>':'')+
    '</div>';
  }).join('');
}

document.addEventListener('DOMContentLoaded',function(){
  renderHist();
  document.getElementById('jname').addEventListener('keydown',function(e){if(e.key==='Enter')start();});
});
</script>
</body>
</html>
