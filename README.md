<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>دليل زيوت السيارات</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{
  font-family:Tahoma;
  direction:rtl;
  background:#f1f3f6;
  padding:20px;
}
.container{
  max-width:420px;
  margin:auto;
  background:#fff;
  padding:20px;
  border-radius:12px;
  box-shadow:0 5px 15px rgba(0,0,0,.15);
}
h2{text-align:center;color:#333}
select{
  width:100%;
  padding:12px;
  margin:8px 0;
  border-radius:8px;
  font-size:15px;
}
.result{
  background:#f9fafb;
  padding:15px;
  border-radius:8px;
  margin-top:10px;
}
.label{color:#555}
.value{font-weight:bold;color:#0a7}
</style>
</head>
<body>

<div class="container">
<h2>دليل زيوت السيارات</h2>

<select id="brand" onchange="loadModels()">
<option value="">اختر الشركة</option>
</select>

<select id="model" onchange="loadYears()">
<option value="">اختر الموديل</option>
</select>

<select id="year" onchange="showOil()">
<option value="">اختر سنة الصنع</option>
</select>

<div class="result" id="result">اختر البيانات</div>
</div>

<script>
// قاعدة البيانات
const cars = {
"تويوتا":{"كورولا":{"oil":"5W-30","cap":"4 لتر","engine":"4 سلندر"},
          "كامري":{"oil":"5W-30","cap":"4.5 لتر","engine":"4 سلندر"},
          "لاندكروزر":{"oil":"10W-40","cap":"6.5 لتر","engine":"6 سلندر"}},
"نيسان":{"صني":{"oil":"5W-30","cap":"3.8 لتر","engine":"4 سلندر"},
         "التيما":{"oil":"5W-30","cap":"4.2 لتر","engine":"4 سلندر"},
         "باترول":{"oil":"10W-40","cap":"6.5 لتر","engine":"6 سلندر"}},
"هيونداي":{"إلنترا":{"oil":"5W-30","cap":"4 لتر","engine":"4 سلندر"},
           "سوناتا":{"oil":"5W-30","cap":"4.8 لتر","engine":"4 سلندر"}},
"كيا":{"سيراتو":{"oil":"5W-30","cap":"4 لتر","engine":"4 سلندر"},
       "سبورتاج":{"oil":"5W-30","cap":"4.6 لتر","engine":"4 سلندر"}},
"هوندا":{"سيفيك":{"oil":"5W-30","cap":"3.7 لتر","engine":"4 سلندر"},
         "أكورد":{"oil":"5W-30","cap":"4.2 لتر","engine":"4 سلندر"}},
"مازدا":{"6":{"oil":"5W-30","cap":"4.5 لتر","engine":"4 سلندر"},
         "CX-5":{"oil":"5W-30","cap":"4.8 لتر","engine":"4 سلندر"}},
"فورد":{"فوكس":{"oil":"5W-30","cap":"4.3 لتر","engine":"4 سلندر"},
        "إكسبلورر":{"oil":"5W-30","cap":"5.7 لتر","engine":"6 سلندر"}},
"شيفروليه":{"ماليبو":{"oil":"5W-30","cap":"4.7 لتر","engine":"4 سلندر"},
            "تاهو":{"oil":"5W-30","cap":"7 لتر","engine":"6 سلندر"}},
"BMW":{"320":{"oil":"5W-30","cap":"5 لتر","engine":"4 سلندر"},
       "520":{"oil":"5W-30","cap":"5.5 لتر","engine":"6 سلندر"}},
"مرسيدس":{"C200":{"oil":"5W-40","cap":"5 لتر","engine":"4 سلندر"},
          "E300":{"oil":"5W-40","cap":"5.5 لتر","engine":"6 سلندر"}}
};

// تعبئة الشركات
const brand = document.getElementById("brand");
const model = document.getElementById("model");
const year = document.getElementById("year");
const result = document.getElementById("result");

Object.keys(cars).forEach(b=>{
  brand.add(new Option(b,b));
});

// تحميل الموديلات
function loadModels(){
  model.length = 1;
  year.length = 1;
  Object.keys(cars[brand.value]).forEach(m=>{
    model.add(new Option(m,m));
  });
  result.innerHTML="اختر الموديل";
}

// تحميل السنوات 2000-2025
function loadYears(){
  year.length = 1;
  for(let y=2000;y<=2025;y++){
    year.add(new Option(y,y));
  }
  result.innerHTML="اختر السنة";
}

// عرض النتائج
function showOil(){
  const o = cars[brand.value][model.value];
  result.innerHTML = `
   <div><span class="label">نوع الزيت:</span> <span class="value">${o.oil}</span></div>
   <div><span class="label">سعة الزيت:</span> <span class="value">${o.cap}</span></div>
   <div><span class="label">نوع المحرك:</span> <span class="value">${o.engine}</span></div>
  `;
}
</script>

</body>
</html>
