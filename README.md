<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>سما بغداد - تسجيل الزيارات</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
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
h2{text-align:center}
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
#status{
 margin-top:10px;
 font-size:14px;
 color:#555;
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
<button onclick="addImage()">📸 إضافة صورة</button>
<button onclick="saveVisit()">💾 حفظ الزيارة</button>

<div id="status"></div>
</div>

<script>
let locationData="";
let images=[];

function getLocation(){
 navigator.geolocation.getCurrentPosition(pos=>{
  locationData=`https://maps.google.com/?q=${pos.coords.latitude},${pos.coords.longitude}`;
  document.getElementById("status").innerHTML="📍 تم أخذ الموقع";
 });
}

function addImage(){
 let input=document.createElement("input");
 input.type="file";
 input.accept="image/*";
 input.onchange=e=>images.push(URL.createObjectURL(e.target.files[0]));
 input.click();
}

function saveVisit(){
 let data={
  shop:shop.value,
  phone:phone.value,
  notes:notes.value,
  location:locationData,
  date:new Date().toLocaleString(),
  images:images
 };
 localStorage.setItem(Date.now(),JSON.stringify(data));
 document.getElementById("status").innerHTML="✅ تم حفظ الزيارة";
}
</script>

</body>
</html>

