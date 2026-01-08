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
  margin-bottom:6px;
}
.hint{
  text-align:center;
  font-size:14px;
  margin-bottom:12px;
  opacity:.75;
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
.footer{
  margin:16px 0;
  font-size:12px;
  text-align:center;
  opacity:.4;
}
</style>
</head>
<body>

<div class="wrapper">
<h1>Красивые шрифты ✒️</h1>
<div class="hint">Нажми на стиль — скопируется текст (EN / RU)</div>

<textarea id="input" placeholder="Введите текст латиницей или кириллицей"></textarea>
<input id="search" placeholder="Поиск стиля..." oninput="render()">

<div class="grid" id="grid"></div>

<div class="footer">
Example / Текст
</div>
</div>

<script>
/* ===== translit EN → RU (без багов) ===== */
const tr=[
["sch","щ"],["yo","ё"],["zh","ж"],["ch","ч"],["sh","ш"],
["yu","ю"],["ya","я"],["je","э"],["ye","е"],
["a","а"],["b","б"],["v","в"],["g","г"],["d","д"],
["e","е"],["z","з"],["i","и"],["j","й"],["k","к"],
["l","л"],["m","м"],["n","н"],["o","о"],["p","п"],
["r","р"],["s","с"],["t","т"],["u","у"],["f","ф"],
["h","х"],["c","ц"],["y","ы"]
];
function toRU(t){
  if(/[а-яё]/i.test(t)) return t;
  let s=t.toLowerCase();
  tr.forEach(([a,b])=>s=s.replaceAll(a,b));
  return s;
}

/* ===== RU → EN (простая, стабильная) ===== */
const rtl={
а:"a",б:"b",в:"v",г:"g",д:"d",е:"e",ё:"yo",ж:"zh",
з:"z",и:"i",й:"y",к:"k",л:"l",м:"m",н:"n",о:"o",
п:"p",р:"r",с:"s",т:"t",у:"u",ф:"f",х:"h",
ц:"c",ч:"ch",ш:"sh",щ:"sch",ы:"y",э:"e",ю:"yu",я:"ya"
};
function toEN(t){
  return t.toLowerCase().split("").map(c=>rtl[c]||c).join("");
}

/* ===== dual text ===== */
function dualText(text){
  if(!text) return "";
  if(/[а-яё]/i.test(text)){
    return text + " / " + toEN(text);
  }else{
    return text + " / " + toRU(text);
  }
}

/* ===== helpers ===== */
function mapEN(start){
  const base="abcdefghijklmnopqrstuvwxyz";
  const code=start.codePointAt(0);
  return t=>t.split("").map(c=>{
    let i=base.indexOf(c.toLowerCase());
    return i==-1?c:String.fromCodePoint(code+i);
  }).join("");
}
function combine(mark){
  return t=>t.split("").map(c=>c===" "?c:c+mark).join("");
}
function glitch(t){
  const m=["\u0301","\u0307","\u0308"];
  return t.split("").map(c=>c===" "?c:c+m[Math.random()*m.length|0]).join("");
}

/* ===== fonts ===== */
const fonts=[
["𝐄𝐱𝐚𝐦𝐩𝐥𝐞",mapEN("𝐀")],
["𝘌𝘹𝘢𝘮𝘱𝘭𝘦",mapEN("𝘈")],
["𝓔𝔁𝓪𝓶𝓹𝓵𝓮",mapEN("𝓐")],
["𝖤𝗑𝖺𝗆𝗉𝗅𝖾",mapEN("𝖠")],
["Ｅｘａｍｐｌｅ",mapEN("Ａ")],

["Underline",combine("\u0332")],
["Double underline",combine("\u0333")],
["Strike",combine("\u0336")],
["Waves",combine("\u0330")],

["Wide",t=>t.split("").join(" ")],
["Glitch",glitch],

["UPPERCASE",t=>t.toUpperCase()],
["lowercase",t=>t.toLowerCase()]
];

/* ===== render ===== */
function render(){
  const q=search.value.toLowerCase();
  const raw=input.value;
  const text=dualText(raw);
  grid.innerHTML="";
  fonts.forEach(([name,fn])=>{
    if(!name.toLowerCase().includes(q))return;
    const d=document.createElement("div");
    d.className="style";
    d.textContent=fn(text||name);
    d.onclick=()=>navigator.clipboard.writeText(fn(text));
    grid.appendChild(d);
  });
}
input.oninput=render;
render();
</script>

</body>
</html>
