<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kalkulator Kece Ultra 5.0</title>
<style>
body { margin:0; font-family:Arial,sans-serif; transition:0.3s; overflow-x:hidden; color:white; background: linear-gradient(270deg,#ff6a00,#ee0979,#00c3ff,#f5f7fa,#ff6a00); background-size:1000% 1000%; animation: gradientBG 20s ease infinite; }

@keyframes gradientBG {
  0%{background-position:0% 50%;}
  50%{background-position:100% 50%;}
  100%{background-position:0% 50%;}
}

button { cursor:pointer; border:none; border-radius:8px; padding:10px; margin:4px; font-size:1.2rem; font-weight:bold; transition:0.2s; }
button:hover { transform:scale(1.05); box-shadow:0 0 15px #0ff; }
button:active { animation: bounce 0.3s; }
@keyframes bounce {0%{transform:scale(1);}50%{transform:scale(0.9);}100%{transform:scale(1);}}

/* CALCULATOR */
#calcPage, #aboutPage { display:block; padding-top:20px; min-height:100vh; text-align:center; position:relative; transition:0.5s; }
#clock { font-size:1.5rem; margin-bottom:10px; color:#0ff; text-shadow:0 0 5px #0ff; }
.display { color:#0f0; font-size:2.2rem; background:black; padding:12px; width:280px; margin:auto; border-radius:10px; text-align:right; box-shadow:0 0 15px #0f0; }
.buttons { width:300px; display:grid; grid-template-columns:repeat(4,1fr); gap:10px; margin:20px auto; }
.btn { background:#333; color:white; box-shadow:0 0 5px #fff; border-radius:12px; font-weight:bold; font-size:1.1rem; }
.history-box { background:white; color:black; width:280px; margin:auto; font-size:0.9rem; padding:8px; border-radius:8px; height:120px; overflow-y:auto; text-align:left; }

/* PANELS FIXED DI ATAS */
.panel { display:none; position:fixed; top:50%; left:50%; transform:translate(-50%,-50%); width:300px; background:rgba(0,0,0,0.85); border-radius:16px; padding:15px; text-align:center; z-index:9999; }
.panel button { width:70px; margin:4px; background:#444; color:#0f0; box-shadow:0 0 5px #0f0; }
.panel button:hover { box-shadow:0 0 12px #0ff; }

/* ABOUT PAGE */
#aboutPage { background:linear-gradient(135deg,#6a11cb,#2575fc); color:white; margin-top:20px; }
#aboutPage h2 { margin-top:20px; }
#aboutPage p { width:80%; margin:auto; font-size:1.1rem; line-height:1.5; background:rgba(0,0,0,0.25); padding:15px; border-radius:12px; }

/* FOOTER NAVIGATION */
#footerNav { display:block; background:rgba(0,0,0,0.5); padding:10px; text-align:center; position:fixed; bottom:0; width:100%; z-index:10; }
#footerNav button { margin:2px; padding:8px 12px; font-size:1rem; }
</style>
</head>
<body>

<!-- CALCULATOR -->
<div id="calcPage">
    <h2 id="calcTitle">Kalkulator Kece Ultra 5.0 😎</h2>
    <div id="clock"></div>
    <div class="display" id="display">0</div>

    <div class="buttons">
        <button class="btn" onclick="press('7')">7</button>
        <button class="btn" onclick="press('8')">8</button>
        <button class="btn" onclick="press('9')">9</button>
        <button class="btn" onclick="press('/')">÷</button>

        <button class="btn" onclick="press('4')">4</button>
        <button class="btn" onclick="press('5')">5</button>
        <button class="btn" onclick="press('6')">6</button>
        <button class="btn" onclick="press('*')">×</button>

        <button class="btn" onclick="press('1')">1</button>
        <button class="btn" onclick="press('2')">2</button>
        <button class="btn" onclick="press('3')">3</button>
        <button class="btn" onclick="press('-')">−</button>

        <button class="btn" onclick="press('0')">0</button>
        <button class="btn" onclick="press('.')">.</button>
        <button class="btn" onclick="calculate()">=</button>
        <button class="btn" onclick="press('+')">+</button>

        <button class="btn" onclick="backspace()">⌫</button>
        <button class="btn" onclick="clearAll()">C</button>
        <button class="btn" style="grid-column: span 2;" onclick="saveHistory()">Save History</button>
    </div>

    <div class="history-box" id="history"></div>

    <!-- PREMIUM PANELS -->
    <div id="scientificPanel" class="panel">
        <button onclick="press('Math.sin(')">sin</button>
        <button onclick="press('Math.cos(')">cos</button>
        <button onclick="press('Math.tan(')">tan</button>
        <button onclick="press('Math.log(')">ln</button>
        <button onclick="press('Math.log10(')">log</button>
        <button onclick="press('Math.sqrt(')">√</button>
        <button onclick="press('**2')">x²</button>
        <button onclick="press('Math.PI')">π</button>
        <button onclick="press('Math.E')">e</button>
    </div>

    <div id="programmerPanel" class="panel">
        <button onclick="toBase(2)">Bin</button>
        <button onclick="toBase(8)">Oct</button>
        <button onclick="toBase(10)">Dec</button>
        <button onclick="toBase(16)">Hex</button>
    </div>

    <div id="graphPanel" class="panel">
        <input id="graphInput" placeholder="x*x" style="width:100px;">
        <button onclick="plotGraph()">Plot</button>
        <canvas id="graphCanvas" width="260" height="200" style="background:white;margin-top:10px;"></canvas>
    </div>

    <div id="themePanel" class="panel">
        <button onclick="setTheme('gradient')">Gradient</button>
        <button onclick="setTheme('dark')">Dark</button>
        <button onclick="setTheme('neon')">Neon</button>
        <button onclick="setTheme('glass')">Glass</button>
        <button onclick="setTheme('retro')">Retro</button>
    </div>

    <div id="langPanel" class="panel">
        <button onclick="setLang('id')">Indonesia</button>
        <button onclick="setLang('en')">English</button>
    </div>
</div>

<!-- ABOUT PAGE -->
<div id="aboutPage">
    <h2>Tentang Saya</h2>
    <p>
        Halo! Saya adalah pembuat aplikasi kalkulator ini. 
        Tujuan saya adalah membuat kalkulator yang keren, interaktif, dan mudah digunakan, 
        lengkap dengan fitur premium seperti kalkulator ilmiah, programmer, graph, theme, dan language.
    </p>
</div>

<!-- FOOTER NAVIGATION -->
<div id="footerNav">
    <button onclick="showCalc()">Kalkulator</button>
    <button onclick="showAbout()">Tentang Saya</button>
    <button onclick="toggleThemePanel()">Theme</button>
    <button onclick="toggleLang()">Language</button>
    <button onclick="toggleScientific()">Scientific</button>
    <button onclick="toggleProgrammer()">Programmer</button>
    <button onclick="toggleGraph()">Graph</button>
</div>

<audio id="clickSound" src="https://freesound.org/data/previews/256/256113_3263906-lq.mp3"></audio>

<script>
let result="0";
const clickSound=document.getElementById("clickSound");

// CALCULATOR
function press(val){ clickSound.currentTime=0; clickSound.play(); if(result==="0") result=""; result+=val; document.getElementById("display").innerText=result; if(navigator.vibrate)navigator.vibrate(10);}
function calculate(){ clickSound.play(); try{ let out=eval(result); document.getElementById("history").innerHTML+=result+" = "+out+"<br>"; result=out.toString(); document.getElementById("display").innerText=result;}catch{document.getElementById("display").innerText="Error";}}
function clearAll(){ clickSound.play(); result="0"; document.getElementById("display").innerText=result;}
function backspace(){ clickSound.play(); result=result.slice(0,-1); if(result==="") result="0"; document.getElementById("display").innerText=result;}
function saveHistory(){ clickSound.play(); let text=document.getElementById("history").innerText; let blob=new Blob([text],{type:"text/plain"}); let link=document.createElement("a"); link.href=URL.createObjectURL(blob); link.download="history.txt"; link.click();}

// PREMIUM PANELS
function toggleScientific(){ clickSound.play(); let s=document.getElementById("scientificPanel"); s.style.display=(s.style.display==="none"?"block":"none");}
function toggleProgrammer(){ clickSound.play(); let s=document.getElementById("programmerPanel"); s.style.display=(s.style.display==="none"?"block":"none");}
function toggleGraph(){ clickSound.play(); let s=document.getElementById("graphPanel"); s.style.display=(s.style.display==="none"?"block":"none");}
function toggleThemePanel(){ clickSound.play(); let s=document.getElementById("themePanel"); s.style.display=(s.style.display==="none"?"block":"none");}
function toggleLang(){ clickSound.play(); let s=document.getElementById("langPanel"); s.style.display=(s.style.display==="none"?"block":"none");}

// PROGRAMMER
function toBase(base){ clickSound.play(); let num=parseInt(result); if(isNaN(num))return; result=num.toString(base).toUpperCase(); document.getElementById("display").innerText=result;}

// GRAPH
function plotGraph(){ clickSound.play(); let input=document.getElementById("graphInput").value; let canvas=document.getElementById("graphCanvas"); let ctx=canvas.getContext("2d"); ctx.clearRect(0,0,260,200); ctx.beginPath(); for(let x=-130;x<130;x++){ try{ let y=eval(input.replace(/x/g,(x/20))); ctx.lineTo(x+130,100-y*20);}catch(e){} } ctx.stroke();}

// THEME
function setTheme(t){
    clickSound.play();
    const page=document.getElementById("calcPage");
    const buttons=document.querySelectorAll(".btn");
    if(t==="gradient"){ page.style.background="linear-gradient(135deg,#121212,#1f1f1f)"; buttons.forEach(b=>b.style.background="#333"); }
    if(t==="dark"){ page.style.background="#222"; buttons.forEach(b=>b.style.background="#444"); }
    if(t==="neon"){ page.style.background="linear-gradient(45deg, #0ff, #f0f)"; buttons.forEach(b=>b.style.background="#0ff"); }
    if(t==="glass"){ page.style.background="rgba(255,255,255,0.1)"; buttons.forEach(b=>b.style.background="rgba(255,255,255,0.2)"); }
    if(t==="retro"){ page.style.background="linear-gradient(135deg,#f06,#f79)"; buttons.forEach(b=>b.style.background="#f06"); }
}

// LANGUAGE
function setLang(lang){
    clickSound.play();
    const title=document.getElementById("calcTitle");
    if(lang==="id"){ title.innerText="Kalkulator Kece Ultra 5.0 😎"; alert("Bahasa diubah ke Indonesia"); }
    if(lang==="en"){ title.innerText="Cool Calculator Ultra 5.0 😎"; alert("Language switched to English"); }
}

// NAVIGATION
function showAbout(){ clickSound.play(); document.getElementById("calcPage").style.display="none"; document.getElementById("aboutPage").style.display="block";}
function showCalc(){ clickSound.play(); document.getElementById("aboutPage").style.display="none"; document.getElementById("calcPage").style.display="block";}

// JAM REAL-TIME
function updateClock(){
    const now = new Date();
    let h = now.getHours().toString().padStart(2,'0');
    let m = now.getMinutes().toString().padStart(2,'0');
    let s = now.getSeconds().toString().padStart(2,'0');
    document.getElementById("clock").innerText = h+":"+m+":"+s;
}
setInterval(updateClock,1000);
updateClock();
</script>

</body>
</html>
