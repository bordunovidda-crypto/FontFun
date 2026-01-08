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
h1{text-align:center;font-size:22px;margin-bottom:10px}
.tabs{display:flex;gap:8px;margin-bottom:10px}
.tab{
  flex:1;padding:10px;border-radius:12px;
  background:#1a1a25;text-align:center;
  cursor:pointer;opacity:.6
}
.tab.active{opacity:1;background:#232337}
textarea,input{
  width:100%;background:#15151d;border:none;
  border-radius:14px;padding:12px;color:#fff;font-size:15px
}
input{margin-top:10px}
.hint{text-align:center;font-size:13px;opacity:.6;margin-top:8px}
.grid{
  margin-top:14px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px
}
.style{
  background:#1a1a25;border-radius:14px;
  padding:14px;text-align:center;
  cursor:pointer;font-size:14px;
  user-select:none;transition:.15s
}
.style:active{transform:scale(.96);background:#2a2a40}
.toast{
  position:fixed;bottom:20px;left:50%;
  transform:translateX(-50%);
  background:#232337;padding:10px 16px;
  border-radius:12px;font-size:13px;
  opacity:0;transition:.3s;pointer-events:none
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

/* ===== Unicode maps ===== */
function mapEN(start){
  const base="abcdefghijklmnopqrstuvwxyz";
  const code=start.codePointAt(0);
  return t=>t.split("").map(c=>{
    let i=base.indexOf(c.toLowerCase());
    return i==-1?c:String.fromCodePoint(code+i);
  }).join("");
}

function mapRU(start){
  const base="абвгдеёжзийклмнопрстуфхцчшщъыьэюя";
  const code=start.codePointAt(0);
  return t=>t.split("").map(c=>{
    let i=base.indexOf(c.toLowerCase());
    return i==-1?c:String.fromCodePoint(code+i);
  }).join("");
}

/* ===== Decor styles ===== */
function combine(m){return t=>t.split("").map(c=>c===" "?c:c+m).join("")}
const decor=[
 ["Underline",combine("\u0332")],
 ["Strike",combine("\u0336")],
 ["Dots",combine("\u0323")],
 ["Waves",combine("\u0330")],
 ["Wide",t=>t.split("").join(" ")],
 ["Glitch",t=>t.split("").map(c=>c===" "?c:c+["\u0307","\u0301","\u0308"][Math.random()*3|0]).join("")]
];

/* ===== Transliteration RU ===== */
const tr={
 yo:"ё",zh:"ж",ch:"ч",sh:"ш",sch:"щ",yu:"ю",ya:"я",
 a:"а",b:"б",v:"в",g:"г",d:"д",e:"е",z:"з",
 i:"и",j:"й",k:"к",l:"л",m:"м",n:"н",
 o:"о",p:"п",r:"р",s:"с",t:"т",u:"у",
 f:"ф",h:"х",c:"ц",y:"ы"
};
function translit(t){
  if(/[а-яё]/i.test(t)) return t;
  let s=t.toLowerCase();
  Object.keys(tr).sort((a,b)=>b.length-a.length)
    .forEach(k=>s=s.replaceAll(k,tr[k]));
  return s;
}

/* ===== Fonts ===== */
const fontsEN=[
 ["𝐄𝐱𝐚𝐦𝐩𝐥𝐞",mapEN("𝐀")],
 ["𝘌𝘹𝘢𝘮𝘱𝘭𝘦",mapEN("𝘈")],
 ["𝙀𝙭𝙖𝙢𝙥𝙡𝙚",mapEN("𝘼")],
 ["𝓔𝔁𝓪𝓶𝓹𝓵𝓮",mapEN("𝓐")],
 ["𝖤𝗑𝖺𝗆𝗉𝗅𝖾",mapEN("𝖠")],
 ["Ｅｘａｍｐｌｅ",mapEN("Ａ")],
 ...decor
];

const fontsRU=[
 ["ТеКсТ",mapRU("Т")],
 ["𝓣𝓮𝓴𝓼𝓽",mapRU("𝓣")],
 ["𝕿𝖊𝖐𝖘𝖙",mapRU("𝕿")],
 ...decor
];

/* ===== UI ===== */
function switchLang(l){
  lang=l;
  document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
  document.querySelectorAll(".tab")[l==="en"?0:1].classList.add("active");
  hint.textContent = l==="ru"
   ? "Можно писать латиницей — текст станет русским"
   : "Введите текст и нажмите на стиль";
  render();
}
function toastShow(){
  toast.classList.add("show");
  setTimeout(()=>toast.classList.remove("show"),1200);
}
function render(){
  grid.innerHTML="";
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
h1{text-align:center;font-size:22px;margin-bottom:10px}
.tabs{display:flex;gap:8px;margin-bottom:10px}
.tab{
  flex:1;padding:10px;border-radius:12px;
  background:#1a1a25;text-align:center;
  cursor:pointer;opacity:.6
}
.tab.active{opacity:1;background:#232337}
textarea,input{
  width:100%;background:#15151d;border:none;
  border-radius:14px;padding:12px;color:#fff;font-size:15px
}
input{margin-top:10px}
.hint{text-align:center;font-size:13px;opacity:.6;margin-top:8px}
.grid{
  margin-top:14px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px
}
.style{
  background:#1a1a25;border-radius:14px;
  padding:14px;text-align:center;
  cursor:pointer;font-size:14px;
  user-select:none;transition:.15s
}
.style:active{transform:scale(.96);background:#2a2a40}
.toast{
  position:fixed;bottom:20px;left:50%;
  transform:translateX(-50%);
  background:#232337;padding:10px 16px;
  border-radius:12px;font-size:13px;
  opacity:0;transition:.3s;pointer-events:none
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

/* ===== Unicode maps ===== */
function mapEN(start){
  const base="abcdefghijklmnopqrstuvwxyz";
  const code=start.codePointAt(0);
  return t=>t.split("").map(c=>{
    let i=base.indexOf(c.toLowerCase());
    return i==-1?c:String.fromCodePoint(code+i);
  }).join("");
}

function mapRU(start){
  const base="абвгдеёжзийклмнопрстуфхцчшщъыьэюя";
  const code=start.codePointAt(0);
  return t=>t.split("").map(c=>{
    let i=base.indexOf(c.toLowerCase());
    return i==-1?c:String.fromCodePoint(code+i);
  }).join("");
}

/* ===== Decor styles ===== */
function combine(m){return t=>t.split("").map(c=>c===" "?c:c+m).join("")}
const decor=[
 ["Underline",combine("\u0332")],
 ["Strike",combine("\u0336")],
 ["Dots",combine("\u0323")],
 ["Waves",combine("\u0330")],
 ["Wide",t=>t.split("").join(" ")],
 ["Glitch",t=>t.split("").map(c=>c===" "?c:c+["\u0307","\u0301","\u0308"][Math.random()*3|0]).join("")]
];

/* ===== Transliteration RU ===== */
const tr={
 yo:"ё",zh:"ж",ch:"ч",sh:"ш",sch:"щ",yu:"ю",ya:"я",
 a:"а",b:"б",v:"в",g:"г",d:"д",e:"е",z:"з",
 i:"и",j:"й",k:"к",l:"л",m:"м",n:"н",
 o:"о",p:"п",r:"р",s:"с",t:"т",u:"у",
 f:"ф",h:"х",c:"ц",y:"ы"
};
function translit(t){
  if(/[а-яё]/i.test(t)) return t;
  let s=t.toLowerCase();
  Object.keys(tr).sort((a,b)=>b.length-a.length)
    .forEach(k=>s=s.replaceAll(k,tr[k]));
  return s;
}

/* ===== Fonts ===== */
const fontsEN=[
 ["𝐄𝐱𝐚𝐦𝐩𝐥𝐞",mapEN("𝐀")],
 ["𝘌𝘹𝘢𝘮𝘱𝘭𝘦",mapEN("𝘈")],
 ["𝙀𝙭𝙖𝙢𝙥𝙡𝙚",mapEN("𝘼")],
 ["𝓔𝔁𝓪𝓶𝓹𝓵𝓮",mapEN("𝓐")],
 ["𝖤𝗑𝖺𝗆𝗉𝗅𝖾",mapEN("𝖠")],
 ["Ｅｘａｍｐｌｅ",mapEN("Ａ")],
 ...decor
];

const fontsRU=[
 ["ТеКсТ",mapRU("Т")],
 ["𝓣𝓮𝓴𝓼𝓽",mapRU("𝓣")],
 ["𝕿𝖊𝖐𝖘𝖙",mapRU("𝕿")],
 ...decor
];

/* ===== UI ===== */
function switchLang(l){
  lang=l;
  document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
  document.querySelectorAll(".tab")[l==="en"?0:1].classList.add("active");
  hint.textContent = l==="ru"
   ? "Можно писать латиницей — текст станет русским"
   : "Введите текст и нажмите на стиль";
  render();
}
function toastShow(){
  toast.classList.add("show");
  setTimeout(()=>toast.classList.remove("show"),1200);
}
function render(){
  grid.innerHTML="";
