<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>اختبار الرخصة المهنية – 20 سؤال</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    margin: 0;
    padding: 20px;
}
.card {
    background: #fff;
    padding: 15px;
    margin-bottom: 20px;
    border-radius: 10px;
    box-shadow: 0 0 7px #ccc;
}
.choice {
    padding: 10px;
    background: #eee;
    margin: 6px 0;
    border-radius: 6px;
    cursor: pointer;
    transition: .3s;
}
.choice.correct {
    background: #8de38d !important;
}
.choice.wrong {
    background: #ff8c8c !important;
}
.choice.disabled {
    pointer-events: none;
    opacity: .6;
}
.popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 12px #0008;
    z-index: 9999;
}
.popup button {
    margin-top: 10px;
}
.summary {
    position: fixed;
    right: 10px;
    bottom: 10px;
    background: #fff;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 0 10px #ccc;
}
button {
    padding: 10px 15px;
}
</style>
</head>
<body>

<h1>اختبار الرخصة المهنية – 20 سؤالًا</h1>

<div id="container"></div>

<div class="summary">
    <div>عدد الإجابات الصحيحة: <span id="correct">0</span> / 20</div>
    <button onclick="resetExam()">إعادة الاختبار</button>
</div>

<script>

// ==========================
// 20 سؤال مع توزيع إجابات ملخبط
// ==========================

const QUESTIONS = [
{
q: "أثناء درس تعلّم قائم على المشكلات، لاحظ المعلم أن الطلاب يقترحون حلولًا جاهزة دون تحليل الأسباب. ما الإجراء الأدق لرفع مستوى thinking؟",
choices: ["إعطاء مزيد من الوقت فقط", "تحويل الدرس لأسئلة مباشرة", "طلب تحديد الفرضيات ومبرراتها", "تقليل صعوبة المهمة"],
correct: 2, // ج
explanation: "تحليل الفرضيات يجبر الطالب على التفكير العميق وليس الاكتفاء بالحلول السطحية."
},

{
q: "يستخدم معلم طريقة المحاضرة دائمًا لشرح المفاهيم المجردة، مما أدى لانخفاض فهم الطلاب. ما الحل الأنسب تربويًا؟",
choices: ["دمج النماذج والمحاكاة في الشرح", "إطالة زمن الحصة", "زيادة عدد الواجبات", "الاكتفاء بالشرح اللفظي"],
correct: 0, // أ
explanation: "المفاهيم المجردة تحتاج تمثيلًا بصريًا أو نماذج لتوضيحها."
},

{
q: "لاحظ المعلم أن طالبًا يعيد نفس الخطأ في كل مهمة رغم حصوله على التغذية الراجعة. ما السبب الأكثر احتمالاً؟",
choices: ["قلة الوقت التدريبي", "الطالب غير مهتم بالتعلم", "ضعف في التغذية الراجعة", "صعوبة المحتوى"],
correct: 2, // د
explanation: "التغذية الراجعة يجب أن تكون دقيقة ومباشرة لتغيير الأداء."
},

{
q: "عند تحليل نتائج الاختبار، وجد المعلم تباينًا كبيرًا بين أجزاء الاختبار. ما المؤشر التربوي المحتمل؟",
choices: ["زيادة دافعية الطلاب", "ضعف في صدق البناء", "ارتفاع الثبات", "مناسبة شاملة للمحتوى"],
correct: 1, // ب
explanation: "التباين الكبير يشير لخلل في الاتساق الداخلي وضعف صدق البناء."
},

{
q: "إذا كان الطالب ينجح في تطبيق المهارة داخل الصف ويفشل خارجها، فما السبب التربوي؟",
choices: ["ضعف في النقل المعرفي", "قلة الواجبات", "عدم مناسبة الأهداف", "انخفاض الدافعية"],
correct: 0, // ج
explanation: "النقل المعرفي يعني استخدام المهارة في سياقات جديدة، وهو ما لم يتحقق."
},

{
q: "عند استخدام التعلم التعاوني، لاحظ المعلم أن بعض الطلاب لا يقدمون حججًا منطقية. كيف يعالج ذلك؟",
choices: ["تدريب الطلاب على مهارات المناقشة", "نقل الطلاب لمجموعات أخرى", "إلغاء الطريقة", "زيادة الوقت"],
correct: 0, // أ
explanation: "تعليم مهارات الحوار شرط لنجاح التعلم التعاوني."
},

{
q: "أثناء تنفيذ استراتيجية العصف الذهني، بدأ الطلاب في نقد أفكار بعضهم. كيف يعالج المعلم الموقف؟",
choices: ["تقليل عدد الأفكار", "منح وقت إضافي", "نقل الطلاب", "التأكيد على قاعدة تعليق النقد"],
correct: 3, // د
explanation: "العصف الذهني يعتمد على حرية الطرح بدون نقد."
},

{
q: "إذا أظهر الطلاب قدرة على الفهم لكنهّم يفشلون في التحليل، فما الاستراتيجية الأنسب؟",
choices: ["الاكتفاء بالأمثلة", "طرح أسئلة عليا موجهة", "تقليل متطلبات الدرس", "زيادة الحفظ"],
correct: 1, // ب
explanation: "الأسئلة العليا تدفع المتعلم للتحليل والتفسير."
},

{
q: "في موقف تعلّم فردي، يواجه الطالب صعوبة في تنظيم خطوات النشاط. ما الدعم المناسب؟",
choices: ["زيادة العمل الفردي", "التسقيل التدريجي", "تغيير المحتوى", "تقليل الأنشطة"],
correct: 1, // ج
explanation: "التسقيل يساعد في تنظيم الخطوات حتى يصل الطالب للاستقلالية."
},

{
q: "لاحظ المعلم أن الطلاب يتذكرون المفهوم داخل الدرس وينسونه بعد أيام. ما السبب المحتمل؟",
choices: ["ضعف في الترميز العميق", "قلة الأمثلة", "عدم وجود دافعية", "الاختبار صعب"],
correct: 0, // أ
explanation: "الترميز السطحي يؤدي لنسيان سريع، ويلزم ربط المعنى والتطبيق."
},

{
q: "إذا أراد المعلم التأكد من صدق المحك لاختبار ما، فماذا يفعل؟",
choices: ["زيادة عدد الأسئلة", "مقارنة النتائج بأداء الطلاب الفعلي", "تغيير طريقة التصحيح", "إطالة زمن الاختبار"],
correct: 1, // د
explanation: "صدق المحك يعتمد على مقارنة نتائج الاختبار بمؤشر خارجي موثوق."
},

{
q: "استخدم المعلم التعلم المعكوس، لكن الطلاب لم يشاهدوا المحتوى قبل الدرس. ما الحل الأنسب؟",
choices: ["تقليل طول الفيديو فقط", "تصميم نشاط تحفيزي يسبق الفيديو", "تغيير الطريقة بالكامل", "زيادة الواجبات"],
correct: 1, // ب
explanation: "النشاط التحفيزي يرفع مشاركة الطلاب قبل الدرس."
},

{
q: "طالب يرفض المشاركة في الأنشطة الجماعية رغم قدرته، ما التفسير الأنسب؟",
choices: ["قلة الثقة بالنفس", "قلة الذكاء الاجتماعي", "ضعف التحصيل", "صعوبة المحتوى"],
correct: 0, // ج
explanation: "الثقة بالنفس تؤثر مباشرة على المشاركة."
},

{
q: "أثناء التقويم البديل، قدم الطالب منتجًا عامًا دون عمق. ما السبب المحتمل؟",
choices: ["زيادة الوقت", "عدم وضوح معايير التقييم", "ضعف القدرات", "اختيار استراتيجية خاطئة"],
correct: 1, // أ
explanation: "غياب معايير دقيقة يؤدي لمنتج غير ذي جودة."
},

{
q: "أراد المعلم تطوير مهارة حل المشكلات، فما النشاط الأدق؟",
choices: ["تكرار الأمثلة", "تقليل الخطوات", "تقديم مشكلات غير روتينية", "زيادة التمارين التقليدية"],
correct: 2, // د
explanation: "المشكلات غير الروتينية تنمّي التفكير العالي."
},

{
q: "في اختبار موضوعي، وجد المعلم أن جميع الطلاب اختاروا نفس الخيار الخاطئ. ما الفرضية الأقرب؟",
choices: ["ضعف الوقت", "وجود خطأ في صياغة السؤال", "انخفاض الذكاء", "صعوبة المحتوى"],
correct: 1, // ب
explanation: "الإجماع على خطأ معين يدل غالبًا على مشكلة في السؤال نفسه."
},

{
q: "لاحظ المعلم أن طالبًا لديه معرفة جيدة لكنه يفشل في التعبير الشفهي. ما التفسير الأقرب؟",
choices: ["قلة الواجبات", "ضعف المحتوى", "ضعف مهارات التواصل", "عدم وجود استراتيجيات"],
correct: 2, // ج
explanation: "التواصل الشفهي مهارة مستقلة عن المعرفة."
},

{
q: "أثناء تقييم الأداء العملي، وجد المعلم تفاوتًا بين المحكمين. ما السبب؟",
choices: ["قلة الوقت", "ضعف في ثبات المحكمين", "جودة عالية", "اختبار صعب"],
correct: 1, // أ
explanation: "تفاوت الأحكام يعني انخفاض ثبات المحكمين."
},

{
q: "إذا أراد المعلم دعم مهارات ما وراء المعرفة، فما أفضل إجراء؟",
choices: ["زيادة أمثلة الحفظ", "تشجيع الطالب على التفكير بصوت مسموع", "تقليل الأنشطة", "تقديم الإجابات مباشرة"],
correct: 1, // د
explanation: "التفكير بصوت مسموع يعزز الوعي بعمليات التفكير."
},

{
q: "عند تنفيذ التعلم الذاتي، وجد المعلم أن الطلاب يحتاجون توجيهًا مستمرًا. ما السبب؟",
choices: ["وقت غير كاف", "قلة الدافعية", "ضعف مهارات التنظيم الذاتي", "صعوبة المحتوى"],
correct: 2, // ب
explanation: "التنظيم الذاتي عنصر أساسي في التعلم الذاتي."
}

];

// =======================================================
// إنشاء البطاقات
// =======================================================

const container = document.getElementById("container");

QUESTIONS.forEach((Q, idx) => {
    const card = document.createElement("div");
    card.className = "card";
    card.dataset.answered = "";

    const qEl = document.createElement("h3");
    qEl.textContent = `${idx + 1}. ${Q.q}`;
    card.appendChild(qEl);

    const choicesDiv = document.createElement("div");

    Q.choices.forEach((ch, i) => {
        const btn = document.createElement("div");
        btn.className = "choice";
        btn.textContent = ch;

        btn.addEventListener("click", () => {

            if (btn.classList.contains("disabled")) return;

            Array.from(choicesDiv.children).forEach(x => x.classList.add("disabled"));

            if (i === Q.correct) {
                btn.classList.add("correct");
                card.dataset.answered = "correct";

                showPop(card,
                    `<strong>إجابة صحيحة ✔</strong><div>${Q.explanation}</div>`
                );

            } else {
                btn.classList.add("wrong");
                choicesDiv.children[Q.correct].classList.add("correct");
                card.dataset.answered = "wrong";

                showPop(card,
                    `<strong>إجابة خاطئة ✘</strong><div>${Q.explanation}</div>`
                );
            }

            updateSummary();
        });

        choicesDiv.appendChild(btn);
    });

    card.appendChild(choicesDiv);
    container.appendChild(card);
});

// =======================================================
// نافذة الشرح
// =======================================================

function showPop(card, msg) {
    const pop = document.createElement("div");
    pop.className = "popup";
    pop.innerHTML = msg + `<br><button onclick="this.parentElement.remove()">إغلاق</button>`;
    document.body.appendChild(pop);
}

// =======================================================
// حساب الدرجات الصحيح 100%
// =======================================================

function updateSummary() {
    let correct = 0;
    document.querySelectorAll(".card").forEach(c => {
        if (c.dataset.answered === "correct") correct++;
    });
    document.getElementById("correct").textContent = correct;
}

// =======================================================
// إعادة الاختبار
// =======================================================

function resetExam() {
    document.querySelectorAll(".popup").forEach(p => p.remove());

    document.querySelectorAll(".card").forEach(card => {
        card.dataset.answered = "";
        card.querySelectorAll(".choice").forEach(btn => {
            btn.classList.remove("disabled", "correct", "wrong");
        });
    });

    updateSummary();
}

</script>

</body>
</html>
