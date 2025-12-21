<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>دليل زيوت السيارات</title>
<style>
body{font-family:tahoma;direction:rtl;background:#f4f4f4;padding:20px}
h1{color:#003366}
input,select,button{padding:8px;margin:5px}
table{width:100%;background:#fff;border-collapse:collapse;margin-top:20px}
th,td{border:1px solid #aaa;padding:8px;text-align:center}
</style>
</head>
<body>

<h1>دليل زيوت السيارات</h1>

<!-- بحث سريع -->
<input id="search" placeholder="ابحث عن سيارة..." onkeyup="searchCars()">

<br><br>

<!-- اختيار السيارة -->
<select id="car" onchange="setOil()">
<option value="">اختر السيارة</option>
<option value="تويوتا كورولا">تويوتا كورولا</option>
<option value="تويوتا كامري">تويوتا كامري</option>
<option value="نيسان التيما">نيسان التيما</option>
<option value="هيونداي إلنترا">هيونداي إلنترا</option>
<option value="كيا سيراتو">كيا سيراتو</option>
</select>

<!-- سنة الصنع -->
<select id="year" onchange="setOil()">
<option value="">سنة الصنع</option>
</select>

<!-- نوع الزيت -->
<input id="oil" readonly placeholder="نوع الزيت">

<button onclick="add()">إضافة</button>

<table>
<tr>
<th>السيارة</th>
<th>سنة الصنع</th>
<th>نوع الزيت</th>
</tr>
<tbody id="rows"></tbody>
</table>

<script>
// توليد السنوات
for(let y=2005;y<=2025;y++){
 year.add(new Option(y,y));
}

// قاعدة البيانات
const oils = {
 "تويوتا كورولا":{
  "2018":"5W-30","2019":"5W-30","2020":"5W-30"
 },
 "تويوتا كامري":{
  "2019":"5W-30","2020":"5W-30"
 },
 "نيسان التيما":{
  "2018":"5W-30","2019":"5W-30"
 },
 "هيونداي إلنترا":{
  "2020":"5W-30","2021":"5W-30"
 },
 "كيا سيراتو":{
  "2019":"5W-30","2020":"5W-30"
 }
};

function setOil(){
 oil.value = oils[car.value]?.[year.value] || "";
}

let data=[];

function add(){
 if(!car.value||!year.value) return;
 data.push([car.value,year.value,oil.value||"—"]);
 render();
}

function render(){
 rows.innerHTML="";
 data.forEach(r=>{
  rows.innerHTML+=`<tr>
   <td>${r[0]}</td>
   <td>${r[1]}</td>
   <td>${r[2]}</td>
  </tr>`;
 });
}

// البحث السريع
function searchCars(){
 let q = search.value.toLowerCase();
 for(let i=0;i<car.options.length;i++){
  let opt = car.options[i];
  opt.style.display = opt.text.toLowerCase().includes(q) ? "" : "none";
 }
}
</script>

</body>
</html>
