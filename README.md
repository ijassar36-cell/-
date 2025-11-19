# -<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>اختبار — أسئلة 1 إلى 10 (رخصة مهنية — مستوى متقدم)</title>
<style>
:root{ --bg:#f4f7fb; --card:#ffffff; --primary:#2563eb; --accent:#06b6d4; --success:#16a34a; --danger:#ef4444; --muted:#6b7280; --radius:14px; }
*{box-sizing:border-box}
body{ margin:0; font-family: "Noto Kufi Arabic", "Segoe UI", Tahoma, system-ui, -apple-system; background:linear-gradient(180deg,#fbfdff, #eef6ff); color:#0b1220; direction:rtl; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale; }
.container{max-width:1050px;margin:28px auto;padding:20px}
.header{ background:var(--card); border-radius:var(--radius); padding:18px 20px; box-shadow:0 10px 30px rgba(2,6,23,0.06); display:flex; flex-direction:column; gap:8px; align-items:center; text-align:center; }
.h-title{font-size:1.4rem;font-weight:800;color:var(--primary)}
.h-sub{color:var(--muted);font-weight:600}
.grid{margin-top:18px;display:grid;grid-template-columns:1fr;gap:14px}
.card{ background:var(--card); border-radius:12px;padding:14px 16px; box-shadow:0 8px 26px rgba(2,6,23,0.06); transition:transform .22s, box-shadow .22s; overflow:visible; }
.card:hover{transform:translateY(-4px)}
.q-head{display:flex;align-items:center;gap:12px;justify-content:space-between}
.q-num{background:linear-gradient(135deg,var(--accent),var(--primary));color:#fff;padding:6px 12px;border-radius:10px;font-weight:800}
.sentence{margin:12px 0 14px;font-size:1.05rem;color:#0b1220;line-height:1.5}
/* خيارات */ .choices{display:flex;flex-wrap:wrap;gap:10px} .choice{ flex:1 1 240px; padding:12px 14px;border-radius:10px; border:1px solid rgba(15,23,42,0.06); background:#fbfdff;color:#08203a;font-weight:700; cursor:pointer;text-align:center;transition:all .18s; user-select:none; } .choice:hover{transform:translateY(-6px);box-shadow:0 12px 30px rgba(2,6,23,0.06)} .choice.correct{background:linear-gradient(90deg,#4ade80,#16a34a);color:#04200a;box-shadow:0 10px 30px rgba(16,185,129,0.12)} .choice.wrong{background:linear-gradient(90deg,#fda4af,#ef4444);color:#3b0a0a;box-shadow:0 10px 30px rgba(239,68,68,0.12)} .choice.disabled{opacity:.86;cursor:default;transform:none;box-shadow:none}
/* شرح منبثق */ .pop{ margin-top:12px;padding:12px;border-radius:10px;background:#ffffff;border:1px solid #e6eef8; box-shadow:0 10px 30px rgba(2,6,23,0.04); animation:pop .36s ease forwards; direction:rtl;color:#0b1220; } .pop strong{display:block;margin-bottom:6px;} @keyframes pop{from{opacity:0;transform:translateY(-8px)}to{opacity:1;transform:none}}
/* شريط التحكم */ .controls{ display:flex;gap:12px;align-items:center;justify-content:space-between;margin-top:18px; flex-wrap:wrap; } .btn{ background:var(--primary);color:#fff;padding:10px 14px;border-radius:12px;border:0;font-weight:800;cursor:pointer; box-shadow:0 8px 22px rgba(37,99,235,0.12); } .btn.secondary{background:#fff;color:var(--primary);border:1px solid rgba(37,99,235,0.12)} .results{font-weight:800;color:#0b1220} .footer{margin-top:22px;text-align:center;color:var(--muted);font-size:0.98rem;padding-bottom:30px}
/* شاشة النتيجة الكبرى */ .overlay{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(2,6,23,0.46);z-index:9999} .panel{background:#fff;padding:20px;border-radius:14px;max-width:520px;width:92%;text-align:center;box-shadow:0 20px 50px rgba(2,6,23,0.3)} .panel h2{margin:6px 0 10px;color:var(--primary)} .panel .score{font-size:2.6rem;font-weight:900;color:var(--success)} .panel .break{margin-top:10px;color:var(--muted)} .panel button{margin-top:14px}
/* responsive */ @media (min-width:900px){ .grid{grid-template-columns:1fr 1fr} .choice{flex:1 1 48%} }
</style>
</head>
<body>
<div class="container">
  <div class="header">
    <div class="h-title">اختبار — أسئلة 1 إلى 10 (رخصة مهنية — مستوى متقدم)</div>
    <div class="h-sub">مجال: مواقف تربوية، تقويم، إدارة صف، ممارسات مهنية</div>
    <div id="summary" class="h-sub">إجابات صحيحة: 0 من 10</div>
  </div>

  <div class="controls">
    <div class="results">النتيجة النهائية: <span id="finalScore">0 / 10</span></div>
    <div style="display:flex;gap:10px;">
      <button id="showAll" class="btn">عرض النتيجة</button>
      <button id="resetBtn" class="btn secondary">إعادة الاختبار</button>
    </div>
  </div>

  <div id="grid" class="grid" style="margin-top:18px;"></div>

  <div class="footer">إعداد: نموذج مخصَّص — بالتوفيق للجميع</div>
</div>

<!-- Overlay النتيجة -->
<div id="overlay" class="overlay">
  <div class="panel">
    <h2>النتيجة النهائية</h2>
    <div class="score" id="finalScoreBig">0 / 10</div>
    <div class="break" id="finalBreak">لم يتم الإجابة بعد.</div>
    <button id="closeOverlay" class="btn secondary">حسناً</button>
  </div>
</div>

<script>
/* مصفوفة الأسئلة (1-10) — كل سؤال: q, choices, correct (index 0..3), explanation */
const questions = [
/* 1 */
{ q:"أثناء درس تعاوني، لاحظ المعلم أن مجموعة من الطلاب تعتمد على طالب واحد لإنجاز المهمة بينما الآخرون يراقبون فقط. ما الإجراء التربوي الأكثر فاعلية لضمان المشاركة المتوازنة؟",
  choices:[
    "إعادة توزيع الأدوار داخل المجموعة بشكل محدد وواضح",
    "زيادة وقت المهمة دون أي تعديل في البنية",
    "تغيير الطالب المتفوق إلى مجموعة أخرى",
    "تقليل حجم المهمة لتبدو أسهل على الجميع"
  ],
  correct:0,
  explanation:"إعادة توزيع الأدوار يسهم في ضمان المشاركة النشطة لجميع أفراد المجموعة ويمنع الاتكالية."
},
/* 2 */
{ q:"أجرى المعلم اختبارًا تشخيصيًا في بداية الوحدة، ولاحظ أن معظم الطلاب يمتلكون مفاهيم خاطئة متشابهة حول المحتوى. ما الخطوة الأكثر دقة قبل بدء التدريس؟",
  choices:[
    "معالجة المفاهيم الخاطئة بشكل صريح قبل تقديم المحتوى الجديد",
    "الانتقال مباشرة إلى المحتوى مع إعطاء أمثلة إضافية فقط",
    "تأجيل معالجة الأخطاء إلى نهاية الوحدة",
    "تقليل مستوى الأسئلة لتناسب فهم الطلاب الحالي"
  ],
  correct:0,
  explanation:"معالجة المفاهيم الخاطئة قبل بداية التدريس تمنع ترسيخ التصورات الخاطئة أثناء التعلم."
},
/* 3 */
{ q:"لاحظ المعلم أن طالبًا يشارك بفعالية في الأنشطة الشفوية، لكنه يُظهر ضعفًا واضحًا في المهام الكتابية. ما التفسير التربوي الأكثر احتمالًا؟",
  choices:[
    "وجود فروق فردية بين أنماط التعبير لدى الطالب",
    "ضعف في الدافعية العامة لدى الطالب",
    "عدم مناسبة مستوى المحتوى للطلاب",
    "قلة وضوح التعليمات في الحصة"
  ],
  correct:0,
  explanation:"تفاوت الأداء بين التعبير الشفوي والكتابي مؤشر على فروق فردية في أنماط التعبير والقدرات."
},
/* 4 */
{ q:"أثناء نقاش صفّي، لاحظ المعلم أن الطلاب يقدمون إجابات سطحية على الرغم من معرفتهم بالمحتوى. ما النوع الأنسب من الأسئلة لرفع مستوى التفكير؟",
  choices:[
    "أسئلة تحليلية تتطلب تبرير الأدلة",
    "أسئلة تذكر مباشرة",
    "أسئلة نعم/لا لتسريع المشاركة",
    "أسئلة مطابقة بسيطة"
  ],
  correct:0,
  explanation:"الأسئلة التحليلية ترفع مستوى التفكير من السطحي إلى العميق عبر طلب تبرير الأدلة."
},
/* 5 */
{ q:"أظهر الطلاب قدرة على تطبيق مهارة معينة داخل الدرس، لكنهم فشلوا في استخدامها في مهمة حياتية مشابهة. ما المفهوم الأصح لتفسير ذلك؟",
  choices:[
    "ضعف في الانتقال المعرفي",
    "قصور في مهارات التذكر الأولي",
    "عدم مناسبة الاستراتيجية المستخدمة",
    "انخفاض الدافعية داخل الصف"
  ],
  correct:0,
  explanation:"عدم القدرة على نقل المهارة إلى سياق جديد يشير إلى ضعف في القدرة على الانتقال المعرفي (transfer)."
},
/* 6 */
{ q:"في أثناء تنفيذ نشاط جماعي، لاحظ المعلم أن مهمات الطلاب تتداخل ولا توجد أدوار واضحة. ما الحل الأكثر فاعلية؟",
  choices:[
    "تصميم أدوار محدّدة لكل طالب مرتبطة بمكونات المهمة",
    "توفير وقت أطول لنفس النشاط دون تغيير البنية",
    "تقليل عدد الطلاب في المجموعات فقط",
    "الاعتماد على الطلاب لتوزيع الأعمال بأنفسهم"
  ],
  correct:0,
  explanation:"تحديد أدوار واضحة لكل عضو يقلل التداخل ويجعل التقييم والمسؤولية أوضح."
},
/* 7 */
{ q:"أثناء الملاحظة الصفية، لاحظ المشرف أن المعلم يستخدم استراتيجية واحدة في جميع الحصص دون تغيير. ما العيب التربوي الأكثر احتمالًا لهذا الأسلوب؟",
  choices:[
    "انخفاض تباين المثيرات مما يقلل مشاركة الطلاب",
    "زيادة الوقت الضائع أثناء الدرس",
    "ارتفاع عبء التخطيط على المعلم",
    "صعوبة تقييم أداء الطلاب"
  ],
  correct:0,
  explanation:"استخدام استراتيجية واحدة يسبب رتابة ويقلل من تباين المحفزات الضروري للحفاظ على انتباه الطلاب."
},
/* 8 */
{ q:"إذا كان معامل الثبات لاختبار معيّن منخفضًا، ما النتيجة الأكثر دقة؟",
  choices:[
    "نتائج الاختبار لا يمكن الاعتماد عليها لاتخاذ قرارات تربوية",
    "الاختبار صعب جدًا ولا يناسب مستوى الطلاب",
    "الأسئلة غير شاملة لجميع النواتج",
    "الاختبار يقيس مهارات مرتفعة"
  ],
  correct:0,
  explanation:"الثبات المنخفض يعني أن النتائج غير مستقرة بين مرات القياس وبالتالي غير موثوقة للاعتماد عليها."
},
/* 9 */
{ q:"أثناء حل المشكلات، يقف الطلاب عند خطوة واحدة ولا ينتقلون للتي تليها رغم معرفتهم بالإجراء. ما الاستراتيجية الأنسب لمعالجة ذلك؟",
  choices:[
    "التسقيل التدريجي مع تقليل التلميحات بمرور الوقت",
    "زيادة عدد الأمثلة المحلولة فقط",
    "إعطاء الحل النهائي للطلاب لنسخه",
    "تقليل مستوى التعقيد في الأنشطة"
  ],
  correct:0,
  explanation:"التسقيل (scaffolding) يمنح دعمًا مرحليًا ثم يسحبه تدريجيًا لتطوير الاستقلالية."
},
/* 10 */
{ q:"لاحظ المعلم أثناء النقاش أن الطلاب يقدمون إجابات صحيحة لكن بلا تفسير. ما الإجراءات التي تعزز التفكير العميق؟",
  choices:[
    "طلب تبرير الإجابة وشرح كيفية الوصول إليها",
    "زيادة عدد الأسئلة لإشغال الطلاب",
    "تقليل وقت التفكير حتى يتجاوزوا الإجابات الخاطئة",
    "إعطاء درجات فقط للإجابة الصحيحة دون الاهتمام بالتفسير"
  ],
  correct:0,
  explanation:"طلب التبرير يحفز الطالب على التفكير في خطوات حل المسألة وما وراء المعرفة."
}
];

/* إنشاء البطاقات */
const grid = document.getElementById('grid');

questions.forEach((Q, idx) => {
  const card = document.createElement('div');
  card.className = 'card';
  card.innerHTML = `
    <div class="q-head">
      <div class="q-num">س ${idx+1}</div>
      <div style="font-weight:700;color:var(--muted)">سؤال ${idx+1}</div>
    </div>
    <div class="sentence">${Q.q}</div>
    <div class="choices"></div>
  `;
  const choicesDiv = card.querySelector('.choices');
  Q.choices.forEach((c, i) => {
    const btn = document.createElement('button');
    btn.className = 'choice';
    const label = ['أ','ب','ج','د'][i] || (i+1);
    btn.innerText = label + ' — ' + c;
    btn.addEventListener('click', () => {
      if (btn.classList.contains('disabled')) return;
      // تعطيل الخيارات بعد الاختيار
      Array.from(choicesDiv.children).forEach(x => x.classList.add('disabled'));
      if (i === Q.correct) {
        btn.classList.add('correct');
        showPop(card, '<strong>إجابة صحيحة</strong>' + '<div>' + Q.explanation + '</div>');
      } else {
        btn.classList.add('wrong');
        const correctBtn = choicesDiv.children[Q.correct];
        if (correctBtn) correctBtn.classList.add('correct');
        showPop(card, '<strong>إجابة خاطئة</strong>' + '<div>' + Q.explanation + '</div>');
      }
      updateSummary();
    });
    choicesDiv.appendChild(btn);
  });
  grid.appendChild(card);
});

function showPop(card, html) {
  const old = card.querySelector('.pop');
  if (old) old.remove();
  const p = document.createElement('div');
  p.className = 'pop';
  p.innerHTML = html;
  card.appendChild(p);
}

function updateSummary() {
  const total = questions.length;
  let correctCount = 0;
  document.querySelectorAll('.card').forEach((card, idx) => {
    if (card.querySelector('.choice.correct')) correctCount++;
  });
  document.getElementById('summary').innerText = `إجابات صحيحة: ${correctCount} من ${total}`;
  document.getElementById('finalScore').innerText = `${correctCount} / ${total}`;
  document.getElementById('finalScoreBig').innerText = `${correctCount} / ${total}`;
}

/* عرض النتائج */
document.getElementById('showAll').addEventListener('click', () => {
  updateSummary();
  document.getElementById('overlay').style.display = 'flex';
  const scoreText = document.getElementById('finalScore').innerText;
  const scoreNum = Number(scoreText.split('/')[0].trim());
  const total = questions.length;
  const panelBreak = document.getElementById('finalBreak');
  if (scoreNum === total) panelBreak.innerText = 'ممتاز — إجابات جميعها صحيحة!';
  else if (scoreNum >= Math.ceil(total * 0.75)) panelBreak.innerText = 'جيد جدًا — استمر بالمراجعة!';
  else if (scoreNum >= Math.ceil(total * 0.5)) panelBreak.innerText = 'متوسط — يحتاج مراجعة.';
  else panelBreak.innerText = 'ضعيف — أنصح بمراجعة الأساسيات.';
});

/* إغلاق overlay */
document.getElementById('closeOverlay').addEventListener('click', () => {
  document.getElementById('overlay').style.display = 'none';
});

/* إعادة الاختبار */
document.getElementById('resetBtn').addEventListener('click', () => {
  document.querySelectorAll('.card').forEach((card, idx) => {
    card.querySelectorAll('.choice').forEach(btn => {
      btn.classList.remove('disabled', 'correct', 'wrong');
    });
    const pop = card.querySelector('.pop');
    if (pop) pop.remove();
  });
  updateSummary();
});

/* تهيئة النتيجة الابتدائية */
updateSummary();
</script>
</body>
</html>
