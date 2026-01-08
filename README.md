<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Красивые шрифты</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>
body{
  margin:0;
  background:#0a0a0e;
  font-family:system-ui,-apple-system;
  color:#f2f2f5;
}
.wrapper{
  max-width:420px;
  margin:auto;
  padding:16px;
}
h1{
  text-align:center;
  font-size:22px;
  margin-bottom:10px;
}
.tabs{
  display:flex;
  gap:8px;
  margin-bottom:10px;
}
.tab{
  flex:1;
  padding:10px;
  border-radius:12px;
  background:#1a1a25;
  text-align:center;
  cursor:pointer;
  opacity:.6;
}
.tab.active{
  opacity:1;
  background:#232337;
}
textarea,input{
  width:100%;
  background:#15151d;
  border:none;
  border-radius:14px;
  padding:12px;
  color:#fff;
  font-size:15px;
}
input{margin-top:10px}
.hint{
  margin-top:8px;
  font-size:13px;
  opacity:.6;
  text-align:center;
}
.grid{
  margin-top:14px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
}
.style{
  background:#1a1a25;
  border-radius:14px;
  padding:14px;
  text-align:center;
  cursor:pointer;
  font-size:14px;
  user-select:none;
  transition:.15s;
}
.style:active{
  transform:scale(.96);
  background:#2a2a40;
}
.toast{
  position:fixed;
  bottom:20px;
  left:50%;
  transform:translateX(-50%);
  background:#232337;
  padding:10px 16px;
  border-radius:12px;
  font-size:13px;
  opacity:0;
  pointer-events:none;
  transition:.3s;
}
.toast.show{opacity:1}
</style>
</head>

<body>
<div class="wrapper">

<h1>Красивые шрифты ✒️</h1>

<div class="tabs">
  <div class="tab active" onclick="switchLang('en')">EN</div>
  <div class="tab" onclick="switchLang('ru')">RU</div>
</div>

<textarea id="input" placeholder="Введите текст / Enter text..."></textarea>
<div class="hint" id="hint">Введите текст и нажмите на стиль ниже</div>

<input id="search" placeholder="Поиск стиля..." oninput="render()">
<div class="grid" id="grid"></div>

</div>

<div class="toast" id="toast">Скопировано ✅</div>

<script>
let lang="en";

/* ===== TRANSLIT (как в Telegram) ===== */
const translitMap = {
  yo:"ё", zh:"ж", ch:"ч", sh:"ш", sch:"щ", yu:"ю", ya:"я",
  a:"а",b:"б",v:"в",g:"г",d:"д",e:"е",z:"з",
  i:"и",j:"й",k:"к",l:"л",m:"м",n:"н",
  o:"о",p:"п",r:"р",s:"с",t:"т",u:"у",
  f:"ф",h:"х",c:"ц",y:"ы"
};

function translit(t){
  if(/[а-яё]/i.test(t)) return t;
  let s=t.toLowerCase();
  Object.keys(translitMap).sort((a,b)=>b.length-a.length)
    .forEach(k=>s=s.replaceAll(k,translitMap[k]));
  return s;
}

/* ===== helpers ===== */
function combine(mark){
  return t=>t.split("").map(c=>c===" "?c:c+mark).join("");
}
function wide(t){return t.split("").join(" ")}
function extraWide(t){return t.split("").join("  ")}
function glitch(t){
  const m=["\u0307","\u0301","\u0308","\u0303"];
  return t.split("").map(c=>c===" "?c:c+m[Math.random()*m.length|0]).join("");
}

/* ===== fonts ===== */
const commonStyles=[
 ["Подчёркнутый", combine("\u0332")],
 ["Зачёркнутый", combine("\u0336")],
 ["Точки", combine("\u0323")],
 ["Волны", combine("\u0330")],
 ["Wide", wide],
 ["Extra Wide", extraWide],
 ["Glitch", glitch],
 ["ВЕРХНИЙ РЕГИСТР", t=>t.toUpperCase()],
 ["нижний регистр", t=>t.toLowerCase()]
];

const fontsEN=[
 ["𝐄𝐱𝐚𝐦𝐩𝐥𝐞", t=>t],
 ...commonStyles
];

const fontsRU=[
 ["ТеКсТ", t=>t],
 ...commonStyles
];

/* ===== UI ===== */
function switchLang(l){
  lang=l;
  document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
  document.querySelectorAll(".tab")[l==="en"?0:1].classList.add("active");
  hint.textContent = l==="ru"
    ? "Можно писать латиницей — текст сам станет русским"
    : "Введите текст и нажмите на стиль";
  render();
}

function showToast(){
  toast.classList.add("show");
  setTimeout(()=>toast.classList.remove("show"),1200);
}

function render(){
  const grid=document.getElementById("grid");
  grid.innerHTML="";
  let text=input.value;
  if(lang==="ru") text=translit(text);

  const list=lang==="en"?fontsEN:fontsRU;
  list.forEach(([name,fn])=>{
    const d=document.createElement("div");
    d.className="style";
    d.textContent=fn(text||name);
    d.onclick=()=>{
      navigator.clipboard.writeText(fn(text));
      showToast();
    };
    grid.appendChild(d);
  });
}

input.oninput=render;
render();
</script>
</body>
</html>
