
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#07051b">
<title>GJ Python Studio</title>

<script src="https://telegram.org/js/telegram-web-app.js"></script>
<script src="https://cdn.jsdelivr.net/pyodide/v0.27.7/full/pyodide.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/python/python.min.js"></script>

<style>
:root{
  --bg:#07051b;
  --panel:#0c0b28;
  --panel2:#111039;
  --line:#30216c;
  --purple:#a855f7;
  --blue:#397bff;
  --cyan:#55e7ff;
  --text:#f4f1ff;
  --muted:#9695c7;
  --green:#43f5b0;
}
*{box-sizing:border-box}
body{
  margin:0;min-height:100vh;color:var(--text);
  font-family:Tahoma,Arial,sans-serif;
  background:
    radial-gradient(ellipse at 15% 0%,#45208055,transparent 35%),
    radial-gradient(ellipse at 90% 10%,#1742a555,transparent 34%),
    radial-gradient(ellipse at 50% 100%,#34116b30,transparent 40%),
    var(--bg);
}
button{font:inherit;cursor:pointer}
button:disabled{opacity:.55;cursor:wait}
.topbar{
  position:relative;overflow:hidden;
  display:flex;align-items:center;justify-content:space-between;
  gap:14px;padding:18px 27px;
  background:linear-gradient(100deg,#110a30,#0b1540,#160c38);
  border-bottom:1px solid #4831a0;
}
.topbar:before{
  content:"";position:absolute;left:10%;right:10%;bottom:-2px;height:3px;
  background:linear-gradient(90deg,transparent,#a855f7,#387dff,#e84dff,transparent);
  filter:blur(3px);
}
.brand{display:flex;align-items:center;gap:13px;position:relative}
.logo{
  width:48px;height:48px;display:grid;place-items:center;
  border-radius:15px;font-size:21px;font-weight:900;
  background:linear-gradient(140deg,#b54cff,#544cff 60%,#27cfff);
  box-shadow:0 0 28px #7845ff75;
}
.brand h1{margin:0;font-size:clamp(17px,3vw,25px)}
.brand h1 span{
  background:linear-gradient(90deg,#65a7ff,#bd83ff,#f08bff);
  color:transparent;background-clip:text;
}
.brand p{margin:5px 0 0;font-size:10px;letter-spacing:3px;color:#858bda}
.header-right{display:flex;gap:10px;align-items:center}
.pill{
  border:1px solid #433786;background:#11102f;padding:10px 13px;
  border-radius:30px;color:#bfb7ff;font-size:11px;white-space:nowrap;
}
.online-dot{
  display:inline-block;width:7px;height:7px;border-radius:50%;
  background:var(--green);box-shadow:0 0 10px var(--green);margin-left:7px;
}
.layout{
  width:min(1600px,100%);margin:auto;padding:22px;
  display:grid;grid-template-columns:225px minmax(0,1fr);gap:17px;
}
.panel{
  background:linear-gradient(145deg,#11102ff5,#090a21f5);
  border:1px solid #30256a;border-radius:17px;
  box-shadow:0 15px 45px #0005,0 0 25px #4824aa0a;
}
.sidebar{padding:15px;align-self:stretch}
.label{
  margin:5px 0 13px;font-size:11px;font-weight:bold;
  color:#a9a0e8;letter-spacing:.4px;
}
.nav{
  display:flex;align-items:center;gap:10px;width:100%;
  text-align:right;padding:12px 10px;margin-bottom:8px;
  color:#c6c5ec;background:#11112f;border:1px solid #272657;
  border-radius:12px;transition:.2s;font-size:12px;
}
.nav .ico{
  display:grid;place-items:center;flex-shrink:0;
  width:34px;height:34px;border-radius:10px;
  background:#21164e;color:#bba0ff;font-size:17px;
}
.nav:hover,.nav.active{
  color:#fff;border-color:#7960ff;
  background:linear-gradient(110deg,#5422a9,#173eaa);
  box-shadow:0 0 20px #6040ff28;transform:translateY(-1px);
}
.nav small{display:block;color:#9996ce;font-size:10px;margin-top:5px}
.nav.active small{color:#d5d1ff}
.quote{
  position:relative;overflow:hidden;margin-top:19px;padding:17px 13px;
  border:1px solid #5132a6;border-radius:14px;
  background:radial-gradient(ellipse at 80% 0%,#7539bf55,transparent 55%),
  linear-gradient(140deg,#171039,#0d1b46);
}
.quote .star{font-size:22px;color:#c49aff}
.quote h3{font-size:12px;margin:9px 0;color:#e6d7ff}
.quote p{font-size:11px;line-height:2;color:#a7a8d9;margin:0}
.quote .quote-glow{
  position:absolute;left:-25px;bottom:-40px;width:120px;height:90px;
  border-radius:50%;background:#7546ff55;filter:blur(30px);
}
.main{min-width:0}
.hero{
  display:flex;justify-content:space-between;align-items:center;gap:14px;
  padding:20px;margin-bottom:15px;position:relative;overflow:hidden;
  background:
    radial-gradient(ellipse at 85% 30%,#5143db45,transparent 40%),
    linear-gradient(110deg,#171039,#101947 70%,#130e36);
  border:1px solid #42358e;border-radius:17px;
}
.hero:after{
  content:"</>";position:absolute;left:24px;top:-15px;
  font-size:95px;font-weight:900;color:#9c83ff0b;pointer-events:none;
}
.hero h2{font-size:clamp(17px,2.4vw,24px);margin:0 0 9px}
.hero h2 span{color:#8bafff}
.hero p{font-size:11px;line-height:1.9;color:#aaa8d7;margin:0}
.hero-tag{
  z-index:1;white-space:nowrap;border:1px solid #5844a0;
  color:#d0baff;background:#201849;padding:10px 12px;
  border-radius:12px;font-size:11px;
}
.editor-panel{padding:15px;overflow:hidden}
.editor-head{
  display:flex;justify-content:space-between;align-items:center;
  flex-wrap:wrap;gap:12px;margin-bottom:14px;
}
.file-info{display:flex;align-items:center;gap:10px}
.file-icon{
  width:39px;height:39px;display:grid;place-items:center;
  border-radius:12px;background:linear-gradient(135deg,#5628a5,#174ba7);
  color:#d8caff;font-weight:bold;box-shadow:0 0 17px #6147ff26;
}
.file-info strong{font-size:12px}
.file-info small{display:block;color:#8588c2;font-size:10px;margin-top:5px}
.actions{display:flex;gap:8px;flex-wrap:wrap}
.btn{
  padding:10px 12px;color:#d8d5ff;border:1px solid #39346f;
  background:#151538;border-radius:10px;font-size:11px;transition:.2s;
}
.btn:hover:not(:disabled){border-color:#9e7aff;filter:brightness(1.2)}
.btn.run{
  color:white;font-weight:bold;border-color:#8e79ff;
  background:linear-gradient(110deg,#9637ed,#4c4bff,#167fe9);
  box-shadow:0 0 20px #6849ff50;
}
.btn.run:hover:not(:disabled){box-shadow:0 0 28px #7c59ff90}
.editor-shell{
  border:1px solid #3c3c91;border-radius:13px;overflow:hidden;
  box-shadow:0 0 25px #302bff16;
}
.editor-strip{
  height:37px;display:flex;align-items:center;gap:7px;padding:0 12px;
  background:#10112d;border-bottom:1px solid #282957;
  direction:ltr;font-size:10px;color:#8e91c8;
}
.traffic{width:7px;height:7px;border-radius:50%;background:#a855f7}
.traffic:nth-child(2){background:#4d86ff}
.traffic:nth-child(3){background:#55e7ff}
.editor-strip span:last-child{margin-left:auto}
.CodeMirror{
  height:340px!important;background:#080b20!important;color:#e3e6ff;
  direction:ltr;text-align:left;font:14px/1.9 Consolas,Monaco,monospace;
}
.CodeMirror-gutters{background:#0b0d26!important;border-right:1px solid #25264d!important}
.CodeMirror-linenumber{color:#666eae!important}
.CodeMirror-cursor{border-left:2px solid #c6a1ff!important}
.CodeMirror-selected{background:#38316c!important}
.cm-s-default .cm-keyword{color:#c792ff!important}
.cm-s-default .cm-def{color:#66d9ff!important}
.cm-s-default .cm-string{color:#8ee8c0!important}
.cm-s-default .cm-number{color:#ffbf86!important}
.cm-s-default .cm-comment{color:#727bb4!important}
.cm-s-default .cm-builtin{color:#63caff!important}
.cm-s-default .cm-operator{color:#ff8bd4!important}
.console{
  margin-top:14px;border:1px solid #33377c;border-radius:13px;
  overflow:hidden;background:#070b1d;
}
.console-head{
  padding:13px 15px;display:flex;align-items:center;justify-content:space-between;
  gap:10px;flex-wrap:wrap;background:linear-gradient(100deg,#161035,#101b3c);
  border-bottom:1px solid #292c5d;
}
.console-title{font-size:12px;color:#c1a7ff;font-weight:bold}
.status{
  font-size:10px;padding:7px 10px;border-radius:30px;
  background:#10342e;color:#5bf1bd;border:1px solid #1a6555;
}
#output{
  margin:0;min-height:120px;max-height:320px;overflow:auto;padding:15px;
  white-space:pre-wrap;overflow-wrap:anywhere;direction:ltr;text-align:left;
  font:13px/1.9 Consolas,Monaco,monospace;color:#8ff3ce;
  background:repeating-linear-gradient(0deg,#0a102600,#0a102600 25px,#18204422 26px),#070b1d;
}
#output.error{color:#ff9dbd}
.footer{
  width:min(1600px,100%);margin:auto;padding:0 22px 22px;
  display:flex;justify-content:space-between;gap:12px;
  font-size:10px;color:#777cae;
}
.footer b{color:#a68cff}
@media(max-width:850px){
  .layout{grid-template-columns:1fr;padding:12px;gap:12px}
  .sidebar{order:2}
  .nav-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:7px}
  .nav{margin:0;padding:9px}
  .quote{margin-top:13px}
  .editor-panel{padding:10px}
  .CodeMirror{height:290px!important}
  .pill:last-child{display:none}
  .hero{padding:16px}
}
@media(max-width:480px){
  .topbar{padding:13px}
  .logo{width:40px;height:40px}
  .brand p{letter-spacing:1px}
  .header-right .pill{font-size:0;padding:10px}
  .hero-tag{display:none}
  .actions{width:100%}
  .actions .btn{flex:1}
  .editor-head{align-items:flex-start}
  .CodeMirror{font-size:12px!important;height:270px!important}
  .footer{padding:5px 13px 18px;flex-wrap:wrap}
}
</style>
</head>

<body>
<header class="topbar">
  <div class="brand">
    <div class="logo">Py</div>
    <div>
      <h1>GJ <span>Python Studio</span></h1>
      <p>CODE · LEARN · CREATE</p>
    </div>
  </div>
  <div class="header-right">
    <div class="pill"><span class="online-dot"></span><span id="topStatus">در حال آماده‌سازی</span></div>
    <div class="pill">✦ Python Pro Academy</div>
  </div>
</header>

<div class="layout">
  <aside class="sidebar panel">
    <div class="label">✦ کتابخانه کد</div>
    <div class="nav-grid">
      <button class="nav active" data-example="hello">
        <span class="ico">⌘</span><span>سلام دنیا<small>شروعی ساده</small></span>
      </button>
      <button class="nav" data-example="variables">
        <span class="ico">∑</span><span>متغیرها<small>داده و محاسبات</small></span>
      </button>
      <button class="nav" data-example="condition">
        <span class="ico">◇</span><span>شرط if<small>تصمیم‌گیری</small></span>
      </button>
      <button class="nav" data-example="loop">
        <span class="ico">↻</span><span>حلقه for<small>تکرار هوشمند</small></span>
      </button>
      <button class="nav" data-example="function">
        <span class="ico">ƒ</span><span>توابع<small>کد قابل استفاده مجدد</small></span>
      </button>
      <button class="nav" data-example="list">
        <span class="ico">▤</span><span>لیست‌ها<small>مجموعه داده‌ها</small></span>
      </button>
    </div>
    <div class="quote">
      <div class="star">✧</div>
      <h3>هر خط کد، یک قدم جلوتر</h3>
      <p>ایده‌های بزرگ از تمرین‌های کوچک شروع می‌شوند. امروز چیزی بساز که دیروز بلد نبودی.</p>
      <div class="quote-glow"></div>
    </div>
  </aside>

  <main class="main">
    <section class="hero">
      <div>
        <h2>ایده‌ات را به <span>کد تبدیل کن.</span></h2>
        <p>فضای اختصاصی تو برای یادگیری، آزمایش و ساختن با پایتون.</p>
      </div>
      <div class="hero-tag">✦ YOUR CREATIVE SPACE</div>
    </section>

    <section class="editor-panel panel">
      <div class="editor-head">
        <div class="file-info">
          <div class="file-icon">Py</div>
          <div><strong>main.py</strong><small>PYTHON SOURCE FILE</small></div>
        </div>
        <div class="actions">
          <button class="btn run" id="run" disabled>▶ بارگذاری پایتون...</button>
          <button class="btn" id="clearCode">⌫ پاک کردن کد</button>
          <button class="btn" id="clearOutput">⌑ پاک کردن خروجی</button>
        </div>
      </div>

      <div class="editor-shell">
        <div class="editor-strip">
          <i class="traffic"></i><i class="traffic"></i><i class="traffic"></i>
          <span>main.py</span>
          <span>Python 3 · Editor</span>
        </div>
        <textarea id="code"># Welcome to GJ Python Studio
name = "Python"

print("Hello", name)
print("Welcome to Python!")
print(10 + 20)</textarea>
      </div>

      <section class="console">
        <div class="console-head">
          <div class="console-title">▸ خروجی برنامه / TERMINAL</div>
          <div class="status" id="status">در حال آماده‌سازی</div>
        </div>
        <pre id="output">در حال بارگذاری موتور پایتون...</pre>
      </section>
    </section>
  </main>
</div>

<footer class="footer">
  <span>♡ آموزش پایتون · ساختن آینده با کد</span>
  <b>GJ PYTHON STUDIO ✦</b>
</footer>

<script>
const tg = window.Telegram?.WebApp;
if (tg) {
  tg.ready();
  tg.expand();
  tg.setHeaderColor("#07051b");
  tg.setBackgroundColor("#07051b");
}

const editor = CodeMirror.fromTextArea(document.getElementById("code"), {
  mode:"python",
  lineNumbers:true,
  indentUnit:4,
  tabSize:4,
  lineWrapping:true,
  autofocus:false
});

const runButton = document.getElementById("run");
const output = document.getElementById("output");
const status = document.getElementById("status");
const topStatus = document.getElementById("topStatus");

let python = null;
let running = false;

const examples = {
  hello: '# Welcome to GJ Python Studio\nname = "Python"\n\nprint("Hello", name)\nprint("Welcome to Python!")\nprint(10 + 20)',
  variables: 'name = "Python"\na = 10\nb = 20\n\nprint("Language:", name)\nprint("Sum:", a + b)\nprint("Product:", a * b)',
  condition: 'number = 12\n\nif number > 10:\n    print("Number is greater than 10")\nelse:\n    print("Number is 10 or less")',
  loop: 'for number in range(1, 6):\n    print(number)',
  function: 'def square(number):\n    return number * number\n\nprint(square(5))\nprint(square(12))',
  list: 'fruits = ["apple", "banana", "orange"]\n\nfor fruit in fruits:\n    print(fruit)'
};

document.querySelectorAll("[data-example]").forEach(button => {
  button.addEventListener("click", () => {
    editor.setValue(examples[button.dataset.example]);
    document.querySelectorAll("[data-example]").forEach(item => {
      item.classList.toggle("active", item === button);
    });
    output.textContent = "نمونه‌کد بارگذاری شد؛ برای اجرا روی دکمه کلیک کن.";
    output.classList.remove("error");
  });
});

document.getElementById("clearCode").addEventListener("click", () => {
  editor.setValue("");
  editor.focus();
});

document.getElementById("clearOutput").addEventListener("click", () => {
  output.textContent = "";
  output.classList.remove("error");
});

async function initializePython() {
  try {
    python = await loadPyodide();
    runButton.disabled = false;
    runButton.textContent = "▶ اجرای کد";
    status.textContent = "● پایتون آماده است";
    topStatus.textContent = "آماده برای اجرا";
    output.textContent = "Python آماده است.\nکدت را بنویس و اجرا کن.";
  } catch (error) {
    status.textContent = "بارگذاری ناموفق";
    topStatus.textContent = "خطای اتصال";
    output.textContent =
      "موتور پایتون بارگذاری نشد.\nاتصال اینترنت را بررسی و صفحه را تازه‌سازی کن.\n\n" + String(error);
    output.classList.add("error");
  }
}

runButton.addEventListener("click", async () => {
  if (!python || running) return;

  running = true;
  runButton.disabled = true;
  runButton.textContent = "در حال اجرا...";
  status.textContent = "● در حال اجرا";
  output.textContent = "";
  output.classList.remove("error");

  let result = "";
  python.setStdout({batched: text => { result += text + "\n"; }});
  python.setStderr({batched: text => { result += text + "\n"; }});

  try {
    await python.runPythonAsync(editor.getValue());
    output.textContent = result || "برنامه اجرا شد؛ خروجی‌ای نداشت.";
    status.textContent = "● اجرا کامل شد";
  } catch (error) {
    output.textContent = String(error);
    output.classList.add("error");
    status.textContent = "● خطای برنامه";
  } finally {
    running = false;
    runButton.disabled = false;
    runButton.textContent = "▶ اجرای کد";
  }
});

initializePython();
</script>
</body>
</html>
