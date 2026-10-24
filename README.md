
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>محیط تمرین پایتون</title>
<style>
body {
    margin: 0;
    padding: 20px;
    background: #101827;
    color: white;
    font-family: Tahoma, Arial, sans-serif;
}
h2 { color: #60a5fa; }
textarea {
    width: 100%;
    height: 220px;
    box-sizing: border-box;
    background: #080e18;
    color: #e2e8f0;
    padding: 12px;
    border: 1px solid #475569;
    border-radius: 8px;
    direction: ltr;
    font: 15px/1.6 Consolas, monospace;
}
button {
    margin: 12px 0;
    padding: 12px 20px;
    border: 0;
    border-radius: 8px;
    background: #16a34a;
    color: white;
    font-size: 15px;
}
pre {
    min-height: 80px;
    padding: 12px;
    background: #080e18;
    color: #86efac;
    white-space: pre-wrap;
    overflow-wrap: anywhere;
    direction: ltr;
    text-align: left;
}
</style>
</head>
<body>

<h2>محیط تمرین پایتون</h2>
<p>کدت را بنویس و روی اجرای کد بزن.</p>

<textarea id="code">print("Hello, Python!")
print(10 + 20)</textarea>

<br>
<button id="run" disabled>در حال بارگذاری پایتون...</button>

<h3>خروجی برنامه</h3>
<pre id="output">در انتظار اجرا...</pre>

<script src="https://cdn.jsdelivr.net/pyodide/v0.27.7/full/pyodide.js"></script>
<script>
const codeBox = document.getElementById("code");
const output = document.getElementById("output");
const runButton = document.getElementById("run");
let python = null;

async function startPython() {
    try {
        python = await loadPyodide();
        runButton.disabled = false;
        runButton.textContent = "▶ اجرای کد";
        output.textContent = "پایتون آماده است.";
    } catch (error) {
        output.textContent = "خطا در بارگذاری پایتون:\n" + error;
        runButton.textContent = "بارگذاری ناموفق";
    }
}

runButton.addEventListener("click", async () => {
    if (!python) return;

    runButton.disabled = true;
    output.textContent = "";

    let result = "";

    python.setStdout({
        batched: text => { result += text + "\n"; }
    });
    python.setStderr({
        batched: text => { result += text + "\n"; }
    });

    try {
        await python.runPythonAsync(codeBox.value);
        output.textContent = result || "برنامه اجرا شد؛ خروجی‌ای نداشت.";
    } catch (error) {
        output.textContent = String(error);
    } finally {
        runButton.disabled = false;
    }
});

startPython();
</script>

</body>
</html>
