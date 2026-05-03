<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>❤️</title>

<style>
body{
margin:0;
font-family:'Cairo', sans-serif;
background:#0b0b0f;
color:#ddd;
overflow:hidden;
}

/* 🎬 Loading */
#loading{
position:fixed;
width:100%;
height:100%;
background:black;
display:flex;
justify-content:center;
align-items:center;
flex-direction:column;
z-index:999;
}

.dot{
width:10px;height:10px;
background:#ff4d6d;
border-radius:50%;
animation:grow 2s forwards;
}

@keyframes grow{
to{transform:scale(40);opacity:0;}
}

/* 📱 */
.section{
position:absolute;
width:100%;
height:100%;
display:none;
justify-content:center;
align-items:center;
flex-direction:column;
animation:fade .6s;
}

@keyframes fade{
from{opacity:0;transform:translateY(20px)}
to{opacity:1}
}

/* 🔐 */
.keys{
display:grid;
grid-template-columns:repeat(3,70px);
gap:10px;
}

.key{
padding:15px;
background:#222;
border-radius:15px;
text-align:center;
cursor:pointer;
}

.key:active{background:#ff4d6d}

/* 😏 */
.btn{
background:rgba(255,255,255,0.1);
backdrop-filter:blur(10px);
padding:12px 25px;
border-radius:25px;
border:1px solid rgba(255,255,255,0.2);
color:white;
margin:5px;
cursor:pointer;
transition:.3s;
}

.btn:hover{
transform:scale(1.1);
background:#ff4d6d;
}

/* ❤️ */
.heart{
position:absolute;
color:#ff4d6d;
animation:float 2s linear;
}

@keyframes float{
to{transform:translateY(-500px);opacity:0;}
}
</style>
</head>

<body>

<!-- 🎬 Loading -->
<div id="loading">
<div class="dot"></div>
<p>في حكاية بدأت من غير ما ناخد بالنا… ❤️</p>
</div>

<!-- 🔐 -->
<div id="lock" class="section">
<p>المكان ده لينا بس 🤍</p>
<div id="display"></div>

<div class="keys">
<div class="key">1</div><div class="key">2</div><div class="key">3</div>
<div class="key">4</div><div class="key">5</div><div class="key">6</div>
<div class="key">7</div><div class="key">8</div><div class="key">9</div>
<div class="key">0</div>
</div>

<p id="error"></p>
</div>

<!-- 💌 -->
<div id="message" class="section"></div>

<!-- 😏 -->
<div id="kiss" class="section">
<p id="kissText">مش هتعدي غير لما تديني بوسة 😏</p>
<button class="btn" onclick="kiss()">امواااه 💋</button>
<button class="btn" onclick="noKiss()">لا 😕</button>
</div>

<!-- 🎵 -->
<div id="audioSection" class="section">
<p>دوسي هنا 🎧</p>
<button class="btn" onclick="playSong()">تشغيل</button>
<audio id="song" src="song.mp3"></audio>
</div>

<!-- 🖼️ -->
<div id="gallery" class="section">
<img id="img" src="img1.jpg" width="80%">
</div>

<!-- 📖 -->
<div id="book" class="section">
<p id="page">بداية</p>
<button class="btn" onclick="nextPage()">اقلب الصفحة</button>
</div>

<!-- ⏳ -->
<div id="counter" class="section">
<p id="time"></p>
<button class="btn" onclick="love()">بتحبني قد اي</button>
<p id="loveCount"></p>
</div>

<script>

// 🎬 loading
setTimeout(()=>{
loading.style.display="none";
show(lock);
},2500);

// 🎬 show sections
function show(sec){
document.querySelectorAll(".section").forEach(s=>s.style.display="none");
sec.style.display="flex";
}

// 🔐
let pass="2024326",input="";
document.querySelectorAll(".key").forEach(k=>{
k.onclick=()=>{
input+=k.innerText;
display.innerText=input;

if(input.length==pass.length){
if(input==pass){
show(message);
startMsg();
}else{
error.innerText="غلط 😏";
input="";display.innerText="";
}
}
}
});

// 💌 (fix lag)
let msgs=[
"فاكرة أول مرة؟",
"أنا بحبك بجد ❤️",
"كملي…"
];
function startMsg(){
message.innerHTML="";
let i=0;
let interval=setInterval(()=>{
if(i<msgs.length){
let p=document.createElement("p");
p.innerText=msgs[i++];
message.appendChild(p);
}else{
clearInterval(interval);
setTimeout(()=>show(kiss),2000);
}
},1500);
}

// 😏
let k=0;
function kiss(){
k++;
for(let i=0;i<10;i++){
let h=document.createElement("div");
h.className="heart";
h.innerText="❤️";
h.style.left=Math.random()*100+"%";
document.body.appendChild(h);
setTimeout(()=>h.remove(),2000);
}
if(k==3) show(audioSection);
}
function noKiss(){alert("غصب 😂");}

// 🎵
function playSong(){
song.play().catch(()=>{});
show(gallery);
startGallery();
}

// 🖼️ (fix intervals)
let imgs=[
"img1.jpg","img2.jpg","img3.jpg","img4.jpg","img5.jpg",
"img6.jpg","img7.jpg","img8.jpg","img9.jpg","img10.jpg"
];
let galleryInterval;
function startGallery(){
clearInterval(galleryInterval);
galleryInterval=setInterval(()=>{
img.src=imgs[Math.floor(Math.random()*imgs.length)];
},3000);

setTimeout(()=>{
clearInterval(galleryInterval);
show(book);
},15000);
}

// 📖
let pages=["بداية","حب","أنا","وانتي","سوا ❤️"];
let p=0;
function nextPage(){
page.innerText=pages[p++]||"❤️";
if(p>pages.length) show(counter);
}

// ⏳ (full time)
let start=new Date("2024-03-26");
setInterval(()=>{
let now=new Date();
let diff=now-start;

let d=Math.floor(diff/1000/60/60/24);
let h=Math.floor(diff/1000/60/60)%24;
let m=Math.floor(diff/1000/60)%60;
let s=Math.floor(diff/1000)%60;

time.innerText=`${d} يوم ${h} ساعة ${m} دقيقة ${s} ثانية ❤️`;
},1000);

// ❤️
let count=localStorage.getItem("love")||0;
function love(){
count++;
localStorage.setItem("love",count);
loveCount.innerText=count;
if(count%10==0) alert("بس كده؟ 😏");
}

// 👀 رجوع
if(localStorage.getItem("visited")){
alert("رجعتي تاني؟ 😏 وحشتيني ❤️");
}
localStorage.setItem("visited",true);

</script>

</body>
</html>
