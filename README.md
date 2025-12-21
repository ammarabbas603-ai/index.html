<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>قياسات زيوت السيارات</title>
<style>
body{font-family:tahoma;direction:rtl;background:#f4f4f4;padding:20px}
h1{color:#003366}
select,input,button{padding:8px;margin:5px}
table{width:100%;background:#fff;border-collapse:collapse;margin-top:20px}
th,td{border:1px solid #aaa;padding:8px;text-align:center}
</style>
</head>
<body>

<h1>نظام قياسات زيوت السيارات</h1>

<!-- اختيار السيارة -->
<select id="car" onchange="setOil()">
<option value="">اختر السيارة</option>
<option value="تويوتا كورولا">تويوتا كورولا</option>
<option value="تويوتا كامري">تويوتا كامري</option>
<option value="نيسان التيما">نيسان التيما</option>
<option value="هيونداي إلنترا">هيونداي إلنترا</option>
</select>

<!-- سنة الصنع -->
<select id="year" onchange="setOil()">
<option value="">سنة الصنع</option>
</select>

<!-- نوع الزيت -->
<input id="oil" readonly placeholder="نوع الزيت">

<input id="oxi" type="number" placeholder="الأكسدة (%)">
<button onclick="add()">إضافة</button>

<table>
<tr>
<th>السيارة</th>
<th>سنة الصنع</th>
<th>نوع الزيت</th>
<th>الأكسدة</th>
<th>الحالة</th>
</tr>
<tbody id="rows"></tbody>
</table>

<script>
// توليد سنوات الصنع تلقائيًا
for(let y=2005;y<=2025;y++){
 year.add(new Option(y,y));
}

// قاعدة بيانات السيارة + السنة + الزيت
const oils = {
 "تويوتا كورولا":{
  "2018":"5W-30",
  "2019":"5W-30",
  "2020":"5W-30"
 },
 "تويوتا كامري":{
  "2019":"5W-30",
  "2020":"5W-30"
 },
 "نيسان التيما":{
  "2018":"5W-30",
  "2019":"5W-30"
 },
 "هيونداي إلنترا":{
  "2020":"5W-30",
  "2021":"5W-30"
 }
};

function setOil(){
 oil.value = oils[car.value]?.[year.value] || "";
}

function status(o){
 if(o<20) return "جيد";
 if(o<35) return "متوسط";
 return "تغيير الزيت";
}

let data=[];
function add(){
 if(!car.value||!year.value||!oxi.value) return;
 data.push([car.value,year.value,oil.value,oxi.value,status(oxi.value)]);
 oxi.value="";
 render();
}

function render(){
 rows.innerHTML="";
 data.forEach(r=>{
  rows.innerHTML+=`<tr>${r.map(c=>`<td>${c}</td>`).join("")}</tr>`;
 });
}
</script>

</body>
</html>

