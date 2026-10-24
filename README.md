
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#101820">
<title>GJ Python Lab | محیط برنامه‌نویسی</title>

<style>
:root {
  --bg: #101820;
  --surface: #17232d;
  --surface2: #1d2c38;
  --border: #2c404d;
  --text: #eef5f7;
  --muted: #9aafb9;
  --cyan: #54e6d0;
  --blue: #80aaff;
  --orange: #ffbd69;
  --red: #ff7885;
  --green: #a8f0b0;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: Tahoma, Arial, sans-serif;
  min-height: 100vh;
}
button, textarea { font: inherit; }
button { cursor: pointer; }
button:disabled { opacity: .55; cursor: wait; }
button:focus-visible, textarea:focus-visible {
  outline: 2px solid var(--cyan);
  outline-offset: 2px;
}
.app { max-width: 1600px; margin: auto; padding: 20px; }

.topbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 16px 20px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
}
.logo { display: flex; align-items: center; gap: 13px; }
.logo-icon {
  width: 48px; height: 48px;
  display: grid; place-items: center;
  background: var(--cyan); color: #10222a;
  font: bold 15px Consolas, monospace;
  border-radius: 13px;
}
.logo h2 { margin: 0; font-size: 16px; }
.logo small {
  display: block; color: var(--muted);
  font-size: 10px; margin-top: 6px;
  direction: ltr; text-align: right;
}
.connection {
  display: flex; align-items: center; gap: 8px;
  color: var(--muted); font-size: 11px;
}
.connection-dot {
  width: 9px; height: 9px; border-radius: 50%;
  background: var(--orange);
}
.hero {
  display: flex; justify-content: space-between;
  align-items: center; gap: 24px;
  padding: 35px 4px 25px;
}
.eyebrow {
  color: var(--cyan); font-size: 11px;
  letter-spacing: 2px; direction: ltr;
  text-align: right;
}
h1 { font-size: clamp(26px, 4vw, 43px); margin: 12px 0; }
.hero p { color: var(--muted); font-size: 12px; line-height: 2; margin: 0; }
.hero-chip {
  flex-shrink: 0; padding: 12px 15px;
  border: 1px solid var(--border); border-radius: 12px;
  color: var(--cyan); font: 11px Consolas, monospace;
  direction: ltr;
}

.workspace {
  display: grid;
  grid-template-columns: minmax(0, 1.35fr) minmax(300px, .8fr);
  gap: 16px;
}
.panel {
  min-width: 0; overflow: hidden;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
}
.panel-header {
  display: flex; align-items: center;
  justify-content: space-between; gap: 10px;
  padding: 15px 17px;
  border-bottom: 1px solid var(--border);
}
.panel-title { font-size: 12px; font-weight: bold; }
.panel-subtitle {
  display: block; color: var(--muted);
  font-size: 10px; font-weight: normal; margin-top: 5px;
}
.file-tag {
  color: var(--cyan); background: #203b40;
  border-radius: 6px; padding: 7px 10px;
  direction: ltr; font: 11px Consolas, monospace;
}
.editor-toolbar {
  display: flex; justify-content: space-between;
  gap: 8px; padding: 10px 15px;
  background: #131e27; color: var(--muted);
  font: 10px Consolas, monospace; direction: ltr;
}
.editor-wrap { position: relative; background: #111a22; }
#code {
  display: block; width: 100%; height: 420px;
  resize: vertical; border: 0; border-radius: 0;
  outline: none; padding: 18px;
  color: #d9f5ee; background: #111a22;
  font: 14px/1.85 Consolas, "Courier New", monospace;
  direction: ltr; text-align: left; tab-size: 4;
  white-space: pre; overflow: auto;
}
.CodeMirror {
  height: 420px;
  font: 14px/1.8 Consolas, monospace;
  direction: ltr; text-align: left;
}
.editor-footer {
  display: flex; justify-content: space-between;
  gap: 10px; padding: 9px 14px;
  color: var(--muted); font-size: 10px;
  border-top: 1px solid var(--border);
}
.toolbar {
  display: grid; grid-template-columns: 1.3fr 1fr 1fr;
  gap: 8px; padding: 13px;
}
.btn {
  min-height: 42px; border: 1px solid var(--border);
  border-radius: 8px; padding: 10px;
  color: var(--text); background: var(--surface2);
  font-size: 11px;
}
.btn:hover { border-color: var(--cyan); }
.btn-run {
  background: var(--cyan); border-color: var(--cyan);
  color: #10252b; font-weight: bold;
}
.btn-run { grid-column: 1 / -1; min-height: 49px; font-size: 13px; }
.btn-danger { color: #ffb5bc; }
.console-panel { display: flex; flex-direction: column; }
.console-tabs {
  display: flex; align-items: center;
  justify-content: space-between;
  gap: 8px; padding: 11px 14px;
  background: #131e27; border-bottom: 1px solid var(--border);
}
.console-tabs strong { font-size: 11px; }
.console-label { color: var(--muted); font-size: 10px; }
.console-body {
  min-height: 340px; flex: 1; padding: 17px;
  background: #0e171e;
}
#output {
  margin: 0; color: var(--green);
  font: 13px/1.9 Consolas, monospace;
  direction: ltr; text-align: left;
  white-space: pre-wrap; overflow-wrap: anywhere;
  min-height: 280px; max-height: 550px; overflow: auto;
}
#output.error-output { color: #ff9da6; }
.console-bottom {
  display: flex; align-items: flex-start; gap: 9px;
  padding: 14px; border-top: 1px solid var(--border);
}
.mini-dot {
  flex-shrink: 0; width: 8px; height: 8px;
  margin-top: 4px; border-radius: 50%; background: var(--cyan);
}
#status { color: var(--muted); font-size: 11px; line-height: 1.9; }
#diagnostics {
  display: none; margin: 12px; padding: 12px;
  color: #ffb5bc; background: #301d25;
  border: 1px solid #693744; border-radius: 8px;
  font-size: 11px; line-height: 1.9;
  white-space: pre-wrap; overflow-wrap: anywhere;
}
#diagnostics.visible { display: block; }
.diagnostic-actions { display: flex; gap: 8px; margin-top: 10px; }
.diagnostic-actions button {
  padding: 9px; border: 1px solid #693744;
  border-radius: 6px; color: var(--text); background: #472631;
}
.tips {
  display: grid; grid-template-columns: repeat(3,1fr);
  gap: 12px; margin-top: 16px;
}
.tip {
  padding: 18px; background: var(--surface);
  border: 1px solid var(--border); border-radius: 12px;
}
.tip-number { color: var(--cyan); font: 11px Consolas, monospace; }
.tip h3 { font-size: 12px; margin: 12px 0 7px; }
.tip p { color: var(--muted); font-size: 11px; line-height: 2; margin: 0; }
footer { padding: 25px 0 8px; text-align: center; color: var(--muted); font-size: 10px; }

@media(max-width:900px) {
  .app { padding: 13px; }
  .workspace { grid-template-columns: 1fr; }
  #code, .CodeMirror { height: 340px; }
  .console-body { min-height: 220px; }
  #output { min-height: 170px; }
}
@media(max-width:540px) {
  .app { padding: 9px; }
  .topbar { padding: 12px; }
  .logo-icon { width: 40px; height: 40px; }
  .logo h2 { font-size: 13px; }
  .logo small { font-size: 9px; }
  .connection { max-width: 105px; font-size: 10px; }
  .hero { padding: 25px 3px 20px; }
  h1 { font-size: 28px; }
  .hero-chip { display: none; }
  .panel-header { padding: 12px; }
  #code, .CodeMirror { height: 285px; font-size: 12px; }
  .toolbar { grid-template-columns: 1fr 1fr; padding: 9px; }
  .btn-run { grid-column: 1 / -1; }
  .tips { grid-template-columns: 1fr; }
  .tip { padding: 14px; }
  .console-body { padding: 12px; }
  #output { font-size: 12px; }
}
</style>
</head>
<body>
<main class="app">

<header class="topbar">
  <div class="logo">
    <div class="logo-icon">GJ.py</div>
    <div>
      <h2>GJ PYTHON LAB</h2>
      <small>CODE · TEST · LEARN</small>
    </div>
  </div>
  <div class="connection">
    <span class="connection-dot" id="connectionDot"></span>
    <span id="connectionText">در حال بررسی اتصال</span>
  </div>
</header>

<section class="hero">
  <div>
    <div class="eyebrow">YOUR PERSONAL CODING WORKSPACE</div>
    <h1>ایده‌ات را به <span style="color:var(--cyan)">کد</span> تبدیل کن.</h1>
    <p>کد بنویس، اجرا کن و نتیجه را در کنسول ببین.<br>بدون نصب پایتون روی دستگاه.</p>
  </div>
  <div class="hero-chip">PYTHON 3 / WEB</div>
</section>

<section class="workspace">
  <section class="panel">
    <div class="panel-header">
      <div class="panel-title">محیط ویرایش کد
        <span class="panel-subtitle">کد پایتون خودت را اینجا بنویس</span>
      </div>
      <span class="file-tag">main.py</span>
    </div>
    <div class="editor-toolbar">
      <span>PYTHON</span>
      <span id="editorMode">EDITOR STARTING</span>
    </div>
    <div class="editor-wrap">
      <textarea id="code" spellcheck="false" autocapitalize="off" autocomplete="off" autocorrect="off">name = input("اسمت چیست؟ ")
print("سلام", name)
print("به آزمایشگاه پایتون خوش آمدی!")</textarea>
    </div>
    <div class="editor-footer">
      <span id="lineInfo">LINE 1</span>
      <span>UTF-8 · SPACES: 4</span>
    </div>
    <div class="toolbar">
      <button class="btn btn-run" id="runButton" disabled>در حال بارگذاری پایتون...</button>
      <button class="btn" id="exampleButton">نمونه کد</button>
      <button class="btn" id="downloadButton">ذخیره فایل</button>
      <button class="btn btn-danger" id="clearButton">پاک‌کردن خروجی</button>
    </div>
    <div id="diagnostics">
      <div id="diagnosticText"></div>
      <div class="diagnostic-actions">
        <button id="retryButton">تلاش مجدد</button>
        <button id="copyErrorButton">کپی خطا</button>
      </div>
    </div>
  </section>

  <section class="panel console-panel">
    <div class="panel-header">
      <div class="panel-title">کنسول اجرا
        <span class="panel-subtitle">نتیجه و خطاهای برنامه</span>
      </div>
      <span class="file-tag">OUTPUT</span>
    </div>
    <div class="console-tabs">
      <strong>خروجی برنامه</strong>
      <span class="console-label" id="runTime">READY</span>
    </div>
    <div class="console-body">
      <pre id="output">در حال آماده‌سازی موتور پایتون...</pre>
    </div>
    <div class="console-bottom">
      <span class="mini-dot" id="statusDot"></span>
      <div id="status">در حال بررسی فایل‌های موردنیاز...</div>
    </div>
  </section>
</section>

<section class="tips">
  <article class="tip">
    <span class="tip-number">01 / WRITE</span>
    <h3>کدنویسی</h3>
    <p>کد را در ویرایشگر بنویس یا نمونهٔ آماده را تغییر بده.</p>
  </article>
  <article class="tip">
    <span class="tip-number">02 / EXECUTE</span>
    <h3>اجرا و آزمایش</h3>
    <p>با دکمهٔ اجرای کد، برنامه را در مرورگر اجرا کن.</p>
  </article>
  <article class="tip">
    <span class="tip-number">03 / IMPROVE</span>
    <h3>یادگیری</h3>
    <p>خروجی و خطاها را بررسی کن و کدت را بهتر کن.</p>
  </article>
</section>

<footer>GJ PYTHON LAB · LEARN BY BUILDING</footer>
</main>

<script>
"use strict";

(() => {
  const $ = id => document.getElementById(id);
  const editorFallback = $("code");
  const PYODIDE_VERSION = "0.27.7";

  const sources = [
    {
      script: `https://cdn.jsdelivr.net/pyodide/v${PYODIDE_VERSION}/full/pyodide.js`,
      base: `https://cdn.jsdelivr.net/pyodide/v${PYODIDE_VERSION}/full/`
    },
    {
      script: `https://unpkg.com/pyodide@${PYODIDE_VERSION}/ pyodide.js`.replace(" ", ""),
      base: `https://unpkg.com/pyodide@${PYODIDE_VERSION}/`
    }
  ];

  let pyodide = null;
  let editor = null;
  let loading = false;
  let running = false;
  let lastError = "";

  function setStatus(message, type = "normal") {
    $("status").textContent = message;
    $("connectionText").textContent =
      type === "error" ? "خطای اتصال" :
      pyodide ? "پایتون آماده است" : "در حال آماده‌سازی";

    const color = type === "error" ? "var(--red)" :
      type === "success" ? "var(--cyan)" : "var(--orange)";

    $("connectionDot").style.background = color;
    $("statusDot").style.background = color;
  }

  function setOutput(text, error = false) {
    $("output").textContent = text;
    $("output").classList.toggle("error-output", error);
  }

  function setButtons(enabled) {
    $("runButton").disabled = !enabled;
    $("runButton").textContent = enabled ? "▶ اجرای کد" : "در حال بارگذاری پایتون...";
  }

  function showDiagnostic(message) {
    lastError = message;
    $("diagnosticText").textContent = message;
    $("diagnostics").classList.add("visible");
  }

  function hideDiagnostic() {
    $("diagnostics").classList.remove("visible");
  }

  function formatError(error) {
    if (error && error.stack) return String(error.stack);
    if (error && error.message) return String(error.message);
    try { return JSON.stringify(error, null, 2); }
    catch (_) { return String(error); }
  }

  function loadScript(url) {
    return new Promise((resolve, reject) => {
      const script = document.createElement("script");
      script.src = url;
      script.async = true;
      script.onload = () => resolve();
      script.onerror = () => {
        script.remove();
        reject(new Error("فایل کتابخانه دریافت نشد:\n" + url));
      };
      document.head.appendChild(script);
    });
  }

  async function loadCodeMirror() {
    if (window.CodeMirror) return true;

    const cssUrls = [
      "https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.css",
      "https://unpkg.com/codemirror@5.65.16/lib/codemirror.css"
    ];

    const scriptUrls = [
      "https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.js",
      "https://unpkg.com/codemirror@5.65.16/lib/codemirror.js"
    ];

    for (const url of cssUrls) {
      const link = document.createElement("link");
      link.rel = "stylesheet";
      link.href = url;
      document.head.appendChild(link);
    }

    let loaded = false;
    for (const url of scriptUrls) {
      try {
        await loadScript(url);
        if (window.CodeMirror) {
          loaded = true;
          break;
        }
      } catch (_) {}
    }

    if (!loaded) return false;

    try {
      await loadScript(
        "https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/python/python.min.js"
      );
    } catch (_) {
      try {
        await loadScript("https://unpkg.com/codemirror@5.65.16/mode/python/python.js");
      } catch (_) {}
    }

    return true;
  }

  async function initEditor() {
    const hasCodeMirror = await loadCodeMirror();

    if (!hasCodeMirror || !window.CodeMirror) {
      $("editorMode").textContent = "BASIC EDITOR";
      editor = null;
      return;
    }

    if (!editor) {
      editor = window.CodeMirror.fromTextArea(editorFallback, {
        mode: window.CodeMirror.modes && window.CodeMirror.modes.python
          ? "python" : null,
        lineNumbers: true,
        indentUnit: 4,
        tabSize: 4,
        lineWrapping: false,
        autofocus: false,
        extraKeys: {
          "Tab": cm => cm.replaceSelection("    ", "end"),
          "Ctrl-Enter": runCode,
          "Cmd-Enter": runCode
        }
      });

      editor.on("cursorActivity", updateLineInfo);
      editor.on("change", updateLineInfo);
    }

    $("editorMode").textContent = "CODEMIRROR";
    editor.refresh();
  }

  function updateLineInfo() {
    let line = 1;
    if (editor) line = editor.getCursor().line + 1;
    else {
      const value = editorFallback.value;
      const pos = editorFallback.selectionStart;
      line = value.slice(0, pos).split("\n").length;
    }
    $("lineInfo").textContent = "LINE " + line;
  }

  function getCode() {
    return editor ? editor.getValue() : editorFallback.value;
  }

  function setCode(value) {
    if (editor) editor.setValue(value);
    else editorFallback.value = value;
    updateLineInfo();
  }

  async function initPython() {
    if (pyodide || loading) return;

    loading = true;
    hideDiagnostic();
    setButtons(false);
    setStatus("در حال بارگذاری موتور پایتون...");
    setOutput("در حال دریافت موتور پایتون. ممکن است بار اول کمی طول بکشد.");

    try {
      await initEditor();

      let loaded = false;
      const failures = [];

      for (const source of sources) {
        try {
          setStatus("در حال امتحان یک منبع برای موتور پایتون...");
          if (typeof window.loadPyodide !== "function") {
            await loadScript(source.script);
          }

          if (typeof window.loadPyodide !== "function") {
            throw new Error("فایل دریافت شد، اما loadPyodide در دسترس نیست.");
          }

          pyodide = await window.loadPyodide({
            indexURL: source.base
          });

          loaded = true;
          break;
        } catch (error) {
          failures.push(source.base + "\n" + formatError(error));
          pyodide = null;
        }
      }

      if (!loaded || !pyodide) {
        throw new Error(
          "موتور پایتون از هیچ‌کدام از منابع بارگذاری نشد.\n\n" +
          failures.join("\n\n----------------\n\n") +
          "\n\nاتصال اینترنت، دسترسی به CDNها یا تنظیمات مرورگر را بررسی کن."
        );
      }

      pyodide.runPython(`
import builtins
import contextlib
import io
import traceback

def run_practice_code(code):
    output = io.StringIO()
    errors = io.StringIO()
    original_input = builtins.input

    def browser_input(message=""):
        from js import prompt
        answer = prompt(str(message))
        if answer is None:
            raise EOFError("ورودی توسط کاربر لغو شد.")
        return str(answer)

    builtins.input = browser_input
    try:
        with contextlib.redirect_stdout(output), contextlib.redirect_stderr(errors):
            exec(compile(code, "main.py", "exec"), {"__name__": "__main__"})
    except BaseException as exc:
        if isinstance(exc, (KeyboardInterrupt, SystemExit)):
            errors.write(type(exc).__name__ + ": اجرای برنامه متوقف شد.\\n")
        else:
            traceback.print_exc(file=errors)
    finally:
        builtins.input = original_input

    return output.getvalue() + errors.getvalue()
      `);

      setButtons(true);
      setStatus("موتور پایتون با موفقیت آماده شد.", "success");
      $("runTime").textContent = "READY";
      setOutput("آماده‌ای!\nکدت را بنویس و روی «اجرای کد» بزن.");
      if (editor) editor.refresh();
    } catch (error) {
      pyodide = null;
      setButtons(false);
      setStatus("بارگذاری موتور پایتون ناموفق بود.", "error");
      const details = formatError(error);
      setOutput("موتور پایتون بارگذاری نشد.\n\n" + details, true);
      showDiagnostic(details);
    } finally {
      loading = false;
    }
  }

  async function runCode() {
    if (!pyodide || running) return;

    running = true;
    setButtons(false);
    hideDiagnostic();
    setStatus("در حال اجرای برنامه...");
    $("runTime").textContent = "RUNNING";
    setOutput("");

    const start = performance.now();

    try {
      pyodide.globals.set("practice_code_from_editor", getCode());
      const result = await pyodide.runPythonAsync(
        "run_practice_code(practice_code_from_editor)"
      );

      const output = String(result || "");
      setOutput(output || "برنامه اجرا شد؛ خروجی چاپ‌شده‌ای ندارد.");
      setStatus("اجرای برنامه تمام شد.", "success");
    } catch (error) {
      const details = formatError(error);
      setOutput("خطای اجرای برنامه:\n\n" + details, true);
      setStatus("برنامه با خطا مواجه شد.", "error");
    } finally {
      const elapsed = ((performance.now() - start) / 1000).toFixed(2);
      $("runTime").textContent = elapsed + " SEC";
      running = false;
      setButtons(Boolean(pyodide));
    }
  }

  $("runButton").addEventListener("click", runCode);

  $("exampleButton").addEventListener("click", () => {
    setCode(
`numbers = [2, 4, 6, 8, 10]

total = sum(numbers)
average = total / len(numbers)

print("Numbers:", numbers)
print("Total:", total)
print("Average:", average)

for number in numbers:
    if number > 5:
        print(number, "is greater than 5")`
    );
    if (editor) editor.focus();
    else editorFallback.focus();
  });

  $("clearButton").addEventListener("click", () => {
    setOutput("خروجی پاک شد.");
    $("runTime").textContent = "READY";
  });

  $("downloadButton").addEventListener("click", () => {
    const blob = new Blob([getCode()], {
      type: "text/x-python;charset=utf-8"
    });
    const url = URL.createObjectURL(blob);
    const link = document.createElement("a");
    link.href = url;
    link.download = "main.py";
    document.body.appendChild(link);
    link.click();
    link.remove();
    setTimeout(() => URL.revokeObjectURL(url), 1000);
  });

  $("retryButton").addEventListener("click", () => {
    if (!loading) initPython();
  });

  $("copyErrorButton").addEventListener("click", async () => {
    try {
      await navigator.clipboard.writeText(lastError);
      $("copyErrorButton").textContent = "کپی شد";
    } catch (_) {
      $("diagnosticText").textContent =
        lastError + "\n\nکپی خودکار در این مرورگر در دسترس نیست.";
    }
  });

  editorFallback.addEventListener("keyup", updateLineInfo);
  editorFallback.addEventListener("click", updateLineInfo);
  editorFallback.addEventListener("input", updateLineInfo);

  editorFallback.addEventListener("keydown", event => {
    if (event.key === "Tab") {
      event.preventDefault();
      const start = editorFallback.selectionStart;
      const end = editorFallback.selectionEnd;
      const value = editorFallback.value;
      editorFallback.value = value.slice(0, start) + "    " + value.slice(end);
      editorFallback.selectionStart = editorFallback.selectionEnd = start + 4;
      updateLineInfo();
    }
    if ((event.ctrlKey || event.metaKey) && event.key === "Enter") {
      event.preventDefault();
      runCode();
    }
  });

  window.addEventListener("resize", () => {
    if (editor) editor.refresh();
  });

  initPython();
})();
</script>
</body>
</html>
