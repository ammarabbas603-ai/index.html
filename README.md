<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>سما بغداد - تسجيل الزيارات</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<style>
body{
 font-family:Tahoma;
 direction:rtl;
 background:#f2f4f7;
 padding:15px;
}
.container{
 max-width:420px;
 margin:auto;
 background:#fff;
 padding:20px;
 border-radius:10px;
 box-shadow:0 5px 15px rgba(0,0,0,.15);
}
h2{text-align:center;color:#0a7}
input,textarea,button{
 width:100%;
 padding:12px;
 margin:6px 0;
 border-radius:6px;
 font-size:15px;
}
button{
 background:#0a7;
 color:#fff;
 border:none;
}
#status{margin-top:10px;color:#555}
#pdf{
 display:none;
 font-size:14px;
}
</style>
</head>
<body>

<div class="container">
<h2>سما بغداد</h2>

<input id="shop" placeholder="اسم المحل">
<input id="phone" placeholder="رقم الهاتف">
<textarea id="notes" placeholder="ملاحظات"></textarea>

<button onclick="getLocation()">📍 أخذ الموقع</button>
<button onclick="createPDF()">📄 حفظ PDF</button>

<div id="status"></div>
</div>

<!-- محتوى PDF -->
<div id="pdf">
<h3>سما بغداد</h3>
<p><b>اسم المحل:</b> <span id="pShop"></span></p>
<p><b>رقم الهاتف:</b> <span id="pPhone"></span></p>
<p><b>التاريخ:</b> <span id="pDate"></span></p>
<p><b>الموقع:</b> <span id="pLocation"></span></p>
<p><b>ملاحظات:</b> <span id="pNotes"></span></p>
</div>

<script>
let locationLink="";

function getLocation(){
 navigator.geolocation.getCurrentPosition(pos=>{
  locationLink=`https://maps.google.com/?q=${pos.coords.latitude},${pos.coords.longitude}`;
  document.getElementById("status").innerHTML="📍 تم تحديد الموقع";
 });
}

function createPDF(){
 document.getElementById("pShop").innerText=shop.value;
 document.getElementById("pPhone").innerText=phone.value;
 document.getElementById("pDate").innerText=new Date().toLocaleString();
 document.getElementById("pLocation").innerText=locationLink;
 document.getElementById("pNotes").innerText=notes.value;

 html2pdf().from(document.getElementById("pdf"))
 .save("زيارة-"+Date.now()+".pdf");

 document.getElementById("status").innerHTML="✅ تم إنشاء ملف PDF";
}
</script>

</body>
</html>

