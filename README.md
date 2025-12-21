<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>نظام قياسات زيوت السيارات</title>
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

<select id="brand" onchange="loadModels()">
<option value="">الشركة</option>
</select>

<select id="model" onchange="loadYears()">
<option value="">الموديل</option>
</select>

<select id="year" onchange="loadEngines()">
<option value="">السنة</option>
</select>

<select id="engine" onchange="setOil()">
<option value="">المحرك</option>
</select>

<input id="oil" readonly placeholder="نوع الزيت">
<input id="oxi" type="number" placeholder="الأكسدة (%)">

<button onclick="add()">إضافة</button>

<table>
<tr>
<th>الشركة</th><th>الموديل</th><th>السنة</th><th>المحرك</th>
<th>الزيت</th><th>الأكسدة</th><th>الحالة</th>
</tr>
<tbody id="rows"></tbody>
</table>

<script>
// قاعدة بيانات قابلة للتوسعة
const db = {
 "تويوتا":{
  "كورولا":{
   "2020":{
    "1.6L":"5W-30",
    "2.0L":"5W-30"
   },
   "2022":{
    "1.6L":"5W-30"
   }
  },
  "كامري":{
   "2019":{
    "2.5L":"5W-30"
   }
  }
 },
 "نيسان":{
  "التيما":{
   "2020":{
    "2.5L":"5W-30"
   }
  }
 },
 "هيونداي":{
  "إلنترا":{
   "2021":{
    "1.6L":"5W-30"
   }
  }
 }
};

// تحميل الشركات
Object.keys(db).forEach(b=>{
 let o=new Option(b,b);
 brand.add(o);
});

function loadModels(){
 model.length=1; year.length=1; engine.length=1; oil.value="";
 if(!brand.value) return;
 Object.keys(db[brand.value]).forEach(m=>{
  model.add(new Option(m,m));
 });
}

function loadYears(){
 year.length=1; engine.length=1; oil.value="";
 if(!model.value) return;
 Object.keys(db[brand.value][model.value]).forEach(y=>{
  year.add(new Option(y,y));
 });
}

function loadEngines(){
 engine.length=1; oil.value="";
 if(!year.value) return;
 Object.keys(db[brand.value][model.value][year.value]).forEach(e=>{
  engine.add(new Option(e,e));
 });
}

function setOil(){
 oil.value=db[brand.value][model.value][year.value][engine.value]||"";
}

function status(o){
 if(o<20) return "جيد";
 if(o<35) return "متوسط";
 return "تغيير الزيت";
}

let data=[];
function add(){
 if(!engine.value||!oxi.value) return;
 data.push([
  brand.value,model.value,year.value,engine.value,
  oil.value,oxi.value,status(oxi.value)
 ]);
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
