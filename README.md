# index.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>ข่าวประชาสัมพันธ์</title>

<style>

body{
font-family:Tahoma;
margin:0;
background:#f2f2f2;
}

.container{
max-width:900px;
margin:auto;
background:white;
padding:20px;
border-radius:12px;
box-shadow:0 3px 10px rgba(0,0,0,0.1);
}

.title{
font-size:24px;
font-weight:bold;
margin-bottom:15px;
color:#003366;
}

.news{
display:flex;
gap:12px;
margin-bottom:15px;
padding-bottom:12px;
border-bottom:1px solid #ddd;
}

.news img{
width:140px;
height:90px;
object-fit:cover;
border-radius:8px;
}

.news a{
text-decoration:none;
color:#222;
font-size:16px;
}

.news a:hover{
color:#0066cc;
}

@media(max-width:600px){

.news{
flex-direction:column;
}

.news img{
width:100%;
height:auto;
}

}

</style>

</head>

<body>

<div class="container">

<div class="title">
ข่าวประชาสัมพันธ์ล่าสุด
</div>

<div id="newslist">
กำลังโหลดข่าว...
</div>

</div>

<script>

fetch("https://system.sesaorb.go.th/news/news_archive.php?type=image&group=school")
.then(res => res.text())
.then(data => {

let parser = new DOMParser();
let doc = parser.parseFromString(data,"text/html");

let links = doc.querySelectorAll("a");
let imgs = doc.querySelectorAll("img");

let html="";

for(let i=0;i<5;i++){

let link = links[i]?.href;
let img = imgs[i]?.src;
let title = links[i]?.innerText;

html += `
<div class="news">

<img src="${img}">

<div>
<a href="${link}" target="_blank">
${title}
</a>
</div>

</div>
`;

}

document.getElementById("newslist").innerHTML = html;

});

</script>

</body>
</html>
