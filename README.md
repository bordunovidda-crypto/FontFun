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
}
.style:hover{background:#242437}
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

<div class="tabs">
  <div class="tab active" onclick="switchLang('en')">EN</div>
  <div class="tab" onclick="switchLang('ru')">RU</div>
</div>

<textarea id="input" placeholder="Введите текст / Enter text..."></textarea>
<input id="search" placeholder="Поиск стиля..." oninput="render()">

<div class="grid" id="grid"></div>

<div class="footer">
Нажми на стиль — текст скопируется!
</div>
</div>

<script>
let lang="en";

const fontsEN=[
["𝐄𝐱𝐚𝐦𝐩𝐥𝐞", mapEN("𝐀")],
["𝘌𝘹𝘢𝘮𝘱𝘭𝘦", mapEN("𝘈")],
["𝙀𝙭𝙖𝙢𝙥𝙡𝙚", mapEN("𝘼")],
["𝖤𝗑𝖺𝗆𝗉𝗅𝖾", mapEN("𝖠")],
["𝓔𝔁𝓪𝓶𝓹𝓵𝓮", mapEN("𝓐")],
["Ｅｘａｍｐｌｅ", mapEN("Ａ")],
["𝕰𝖝𝖆𝖒𝖕𝖑𝖊", mapEN("𝕬")],
["ᴇxᴀᴍᴘʟᴇ", mapEN("ᴀ")],
["ｅхａｍｐｌｅ", mapEN("ｅ")],
["EXAMPLE", t=>t.toUpperCase()],
["example", t=>t.toLowerCase()]
];

const fontsRU=[
["ТеКсТ", mapRU("Т")],
["𝘛𝘦𝘬𝘴𝘵", mapRU("𝘛")],
["𝙏𝙚𝙠𝙨𝙩", mapRU("𝙏")],
["𝓣𝓮𝓴𝓼𝓽", mapRU("𝓣")],
["𝕿𝖊𝖐𝖘𝖙", mapRU("𝕿")],
["ТЕКСТ", t=>t.toUpperCase()],
["текст", t=>t.toLowerCase()],
["Т е к с т", t=>t.split("").join(" ")]
];

function mapEN(start){
  const base="abcdefghijklmnopqrstuvwxyz";
  const code=start.codePointAt(0);
  return t=>t.split("").map(c=>{
    let i=base.indexOf(c.toLowerCase());
    if(i==-1)return c;
    let ch=String.fromCodePoint(code+i);
    return c===c.toUpperCase()?ch:ch;
  }).join("");
}

function mapRU(start){
  const base="абвгдеёжзийклмнопрстуфхцчшщъыьэюя";
  const code=start.codePointAt(0);
  return t=>t.split("").map(c=>{
    let i=base.indexOf(c.toLowerCase());
    if(i==-1)return c;
    return String.fromCodePoint(code+i);
  }).join("");
}

function switchLang(l){
  lang=l;
  document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
  document.querySelectorAll(".tab")[l==="en"?0:1].classList.add("active");
  render();
}

function render(){
  const grid=document.getElementById("grid");
  const q=document.getElementById("search").value.toLowerCase();
  grid.innerHTML="";
  const list=lang==="en"?fontsEN:fontsRU;
  list.forEach(([name,fn])=>{
    if(!name.toLowerCase().includes(q))return;
    const d=document.createElement("div");
    d.className="style";
    d.textContent=name;
    d.onclick=()=>navigator.clipboard.writeText(fn(input.value));
    grid.appendChild(d);
  });
}

render();
</script>

</body>
</html>
