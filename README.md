<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>دليل زيوت السيارات</title>
<style>
body{font-family:tahoma;direction:rtl;background:#f2f2f2;padding:20px}
h1{color:#003366}
select{padding:8px;margin:5px}
input{padding:8px;margin:5px}
table{width:100%;background:#fff;border-collapse:collapse;margin-top:20px}
th,td{border:1px solid #aaa;padding:10px;text-align:center}
</style>
</head>
<body>

<h1>دليل زيوت السيارات</h1>

<select id="brand" onchange="loadModels()">
<option value="">اختر الشركة</option>
</select>

<select id="model" onchange="loadYears()">
<option value="">اختر الموديل</option>
</select>

<select id="year" onchange="setOil()">
<option value="">سنة الصنع</option>
</select>

<input id="oil" readonly placeholder="نوع الزيت يظهر تلقائيًا">

<table>
<tr>
<th>الشركة</th>
<th>الموديل</th>
<th>سنة الصنع</th>
<th>نوع الزيت</th>
</tr>
<tbody id="rows"></tbody>
</table>

<script>
// قاعدة بيانات أكبر (قابلة للتوسعة)
const db = {
 "تويوتا":{
  "كورولا":{"2018":"5W-30","2019":"5W-30","2020":"5W-30","2021":"5W-30"},
  "كامري":{"2019":"5W-30","2020":"5W-30","2021":"5W-30"},
  "راف4":{"2020":"5W-30","2021":"5W-30"}
 },
 "نيسان":{
  "التيما":{"2018":"5W-30","2019":"5W-30","2020":"5W-30"},
  "باترول":{"2019":"10W-40","2020":"10W-40"},
  "صني":{"2020":"5W-30","2021":"5W-30"}
 },
 "هيونداي":{
  "إلنترا":{"2019":"5W-30","2020":"5W-30","2021":"5W-30"},
  "سوناتا":{"2020":"5W-30","2021":"5W-30"}
 },
 "كيا":{
  "سيراتو":{"2019":"5W-30","2020":"5W-30"},
  "سبورتاج":{"2020":"5W-30","2021":"5W-30"}
 },
 "فورد":{
  "إكسبلورر":{"2019":"5W-30","2020":"5W-30"},
  "فوكس":{"2018":"5W-30","2019":"5W-30"}
 },
 "مرسيدس":{
  "C200":{"2019":"5W-40","2020":"5W-40"},
  "E300":{"2020":"5W-40","2021":"5W-40"}
 },
 "BMW":{
  "320":{"2019":"5W-30","2020":"5W-30"},
  "520":{"2020":"5W-30","2021":"5W-30"}
 }
};

// تحميل الشركات
Object.keys(db).forEach(b=>{
 brand.add(new Option(b,b));
});

function loadModels(){
 model.length=1; year.length=1; oil.value="";
 if(!brand.value) return;
 Object.keys(db[brand.value]).forEach(m=>{
  model.add(new Option(m,m));
 });
}

function loadYears(){
 year.length=1; oil.value="";
 if(!model.value) return;
 Object.keys(db[brand.value][model.value]).forEach(y=>{
  year.add(new Option(y,y));
 });
}

function setOil(){
 if(!year.value) return;
 oil.value = db[brand.value][model.value][year.value];
 rows.innerHTML = `
 <tr>
  <td>${brand.value}</td>
  <td>${model.value}</td>
  <td>${year.value}</td>
  <td>${oil.value}</td>
 </tr>`;
}
</script>

</body>
</html>

