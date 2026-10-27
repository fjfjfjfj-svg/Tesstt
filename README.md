<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Тест: Упаковка и маркировка. Спецслучаи</title>
<style>
:root{--bg:#0b1220;--panel:#121d30;--panel2:#18263d;--text:#f3f6fc;--muted:#a8b5ca;--accent:#56d6b0;--accent2:#32b994;--bad:#ff7777;--border:#2b3b55}
*{box-sizing:border-box}
body{margin:0;min-height:100vh;background:radial-gradient(circle at top,#172b48 0,#0b1220 55%);color:var(--text);font-family:Arial,Helvetica,sans-serif;padding:22px}
.wrap{max-width:820px;margin:0 auto}
header{text-align:center;margin:18px 0 24px}
.logo{display:inline-grid;place-items:center;width:58px;height:58px;border-radius:18px;background:#193c4a;color:var(--accent);font-size:28px;margin-bottom:12px}
h1{font-size:clamp(26px,5vw,38px);margin:0 0 10px}
.subtitle{color:var(--muted);line-height:1.5;margin:0}
.card{background:rgba(18,29,48,.96);border:1px solid var(--border);border-radius:22px;padding:clamp(20px,4vw,32px);box-shadow:0 18px 50px #0003}
.hidden{display:none!important}
.stats{display:flex;gap:10px;flex-wrap:wrap;margin:20px 0}
.pill{background:var(--panel2);border:1px solid var(--border);padding:9px 12px;border-radius:999px;color:var(--muted);font-size:13px}
button{font:inherit;cursor:pointer;border:0;transition:.15s}
.primary{background:var(--accent);color:#06241d;font-weight:800;padding:14px 20px;border-radius:12px}
.primary:hover{background:var(--accent2);transform:translateY(-1px)}
.secondary{background:var(--panel2);color:var(--text);border:1px solid var(--border);padding:12px 16px;border-radius:12px}
.secondary:hover{border-color:var(--accent)}
button:disabled{opacity:.35;cursor:not-allowed;transform:none}
.topline{display:flex;justify-content:space-between;gap:12px;color:var(--muted);font-size:14px;margin-bottom:12px}
.progress{height:8px;background:#25334a;border-radius:99px;overflow:hidden;margin-bottom:25px}
.progressbar{height:100%;width:0;background:var(--accent);transition:width .25s}
.question{font-size:clamp(20px,3.5vw,26px);line-height:1.4;margin:0 0 22px}
.answers{display:grid;gap:11px}
.answer{display:flex;align-items:flex-start;gap:12px;text-align:left;width:100%;background:var(--panel2);color:var(--text);border:1px solid var(--border);padding:15px;border-radius:13px;line-height:1.45}
.answer:hover{border-color:#6c89ad}
.answer .letter{flex:0 0 28px;height:28px;display:grid;place-items:center;border:1px solid #51637e;border-radius:8px;color:var(--muted);font-weight:bold;font-size:13px}
.answer.selected{border-color:var(--accent);background:#173a3a}
.answer.selected .letter{background:var(--accent);color:#06241d;border-color:var(--accent)}
.answer.correct{border-color:var(--accent);background:#12372f}
.answer.wrong{border-color:var(--bad);background:#40242d}
.controls{display:flex;justify-content:space-between;gap:10px;margin-top:24px}
.controls button{min-width:115px}
.note{color:var(--muted);font-size:13px;line-height:1.5;margin-top:18px}
.score{font-size:56px;font-weight:800;color:var(--accent);margin:8px 0}
.review{border-top:1px solid var(--border);padding:18px 0}
.review h3{font-size:16px;line-height:1.45;margin:0 0 8px}
.review p{margin:6px 0;color:var(--muted);line-height:1.5}
.good{color:var(--accent)!important}.bad{color:var(--bad)!important}
footer{text-align:center;color:#75859e;font-size:12px;margin:18px 0}
@media(max-width:520px){body{padding:12px}.card{border-radius:17px}.controls button{min-width:0;flex:1}.topline{font-size:12px}}
</style>
</head>
<body>
<div class="wrap">
<header>
  <div class="logo">▣</div>
  <h1>Упаковка и маркировка</h1>
  <p class="subtitle">Спецслучаи • Проверь свои знания</p>
</header>

<section id="start" class="card">
  <h2>Готов к проверке знаний?</h2>
  <p class="subtitle">Тест содержит 15 вопросов. В каждом вопросе выбери один правильный ответ. В конце увидишь результат и сможешь разобрать ошибки.</p>
  <div class="stats">
    <span class="pill">📋 15 вопросов</span>
    <span class="pill">🎯 1 балл за ответ</span>
    <span class="pill">📱 Для телефона и компьютера</span>
  </div>
  <button class="primary" id="startBtn">Начать тест →</button>
  <p class="note">Тест составлен по общим правилам упаковки и маркировки. Для учебного или официального использования сверяй требования с материалами своей дисциплины.</p>
</section>

<section id="quiz" class="card hidden">
  <div class="topline"><span id="counter">Вопрос 1 из 15</span><span id="answered">Отвечено: 0/15</span></div>
  <div class="progress"><div class="progressbar" id="progressbar"></div></div>
  <h2 class="question" id="question"></h2>
  <div class="answers" id="answers"></div>
  <div class="controls">
    <button class="secondary" id="prevBtn">← Назад</button>
    <button class="primary" id="nextBtn">Далее →</button>
  </div>
  <p class="note">Можно вернуться к предыдущему вопросу и изменить ответ до завершения теста.</p>
</section>

<section id="result" class="card hidden">
  <h2>Тест завершён</h2>
  <p class="subtitle" id="resultMessage"></p>
  <div class="score" id="score">0/15</div>
  <p id="percent"></p>
  <div class="progress"><div class="progressbar" id="resultbar"></div></div>
  <div class="controls">
    <button class="secondary" id="reviewBtn">Разобрать ответы</button>
    <button class="primary" id="restartBtn">Пройти заново ↻</button>
  </div>
  <div id="review" class="hidden" style="margin-top:22px"></div>
</section>
<footer>Учебный тест • Упаковка и маркировка</footer>
</div>

<script>
const questions = [
{q:"Что такое упаковка товара?",c:"Средство для защиты товара при хранении и транспортировке",w:["Документ, подтверждающий стоимость товара","Способ определения качества товара","Рекламный текст о производителе"]},
{q:"Для чего предназначена маркировка товара?",c:"Для предоставления информации о товаре",w:["Только для украшения упаковки","Только для увеличения стоимости товара","Для замены сопроводительных документов"]},
{q:"Какая информация обычно указывается на маркировке товара?",c:"Наименование товара, изготовитель и основные характеристики",w:["Личные данные всех покупателей","Пароли сотрудников предприятия","Только цена товара"]},
{q:"Что означает штрихкод на упаковке?",c:"Графическое обозначение, позволяющее идентифицировать товар",w:["Подтверждение отсутствия дефектов товара","Гарантию бесплатной доставки","Информацию исключительно о сроке годности"]},
{q:"Что необходимо учитывать при выборе упаковки?",c:"Свойства товара, условия хранения и транспортировки",w:["Только её цвет","Только её стоимость","Только название производителя"]},
{q:"Что означает маркировка «Хрупкое»?",c:"С грузом необходимо обращаться осторожно",w:["Товар запрещено хранить на складе","Товар нельзя перевозить автомобильным транспортом","Товар обязательно должен храниться в морозильнике"]},
{q:"Как следует упаковывать товары, чувствительные к влаге?",c:"В герметичную или влагозащитную упаковку, подходящую для данного товара",w:["В открытую картонную коробку","В упаковку с отверстиями без дополнительной защиты","В любую бумажную упаковку"]},
{q:"Что следует сделать, если маркировка товара повреждена и не читается?",c:"Проверить информацию и восстановить маркировку установленным способом",w:["Игнорировать повреждение","Самостоятельно придумать недостающие сведения","Удалить все сведения о производителе"]},
{q:"Как маркируют опасные грузы?",c:"Знаками опасности и другими предусмотренными обозначениями",w:["Только названием транспортной компании","Исключительно цветом упаковки","Без специальных обозначений, если груз небольшой"]},
{q:"Что такое специальная упаковка?",c:"Упаковка, предназначенная для определённых свойств товара или особых условий обращения",w:["Упаковка, используемая исключительно для рекламы","Любая упаковка повышенной стоимости","Упаковка без маркировки"]},
{q:"Как следует маркировать товар с ограниченным сроком годности?",c:"Указывать срок годности или дату окончания срока годности в соответствии с требованиями",w:["Указывать только дату продажи","Указывать только фамилию продавца","Не указывать даты, если упаковка герметичная"]},
{q:"Как поступить с товаром, упаковка которого нарушена?",c:"Проверить состояние товара и принять решение согласно установленным требованиям",w:["Всегда продавать его без проверки","Переклеить маркировку без осмотра","Скрыть повреждение дополнительной этикеткой"]},
{q:"Для чего применяется вакуумная упаковка?",c:"Для удаления воздуха из упаковки и замедления некоторых процессов порчи",w:["Для увеличения массы товара","Для полного уничтожения всех микроорганизмов в любом продукте","Только для придания товару привлекательного вида"]},
{q:"Что необходимо учитывать при маркировке импортного товара?",c:"Требования законодательства страны ввоза, включая язык и обязательные сведения",w:["Только язык страны отправления","Только фирменный знак продавца","Только адрес транспортной компании"]},
{q:"Что следует сделать, если сведения на этикетке не соответствуют фактическому содержимому упаковки?",c:"Приостановить реализацию до проверки и устранить несоответствие установленным способом",w:["Оставить этикетку без изменений","Продолжить реализацию без проверки","Удалить упаковку и продавать товар без информации"]}
];

let order=[],answers=[],current=0,reviewShown=false;
const $=id=>document.getElementById(id);
function shuffle(arr){const a=[...arr];for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]];}return a;}
function startQuiz(){
  order=questions.map((q,i)=>({q,i,opts:shuffle([{text:q.c,correct:true},...q.w.map(text=>({text,correct:false}))])}));
  answers=Array(questions.length).fill(null);current=0;reviewShown=false;
  $("start").classList.add("hidden");$("result").classList.add("hidden");$("quiz").classList.remove("hidden");
  $("review").classList.add("hidden");$("reviewBtn").textContent="Разобрать ответы";
  renderQuestion();
}
function renderQuestion(){
  const item=order[current];
  $("counter").textContent=`Вопрос ${current+1} из ${order.length}`;
  $("answered").textContent=`Отвечено: ${answers.filter(x=>x!==null).length}/${order.length}`;
  $("progressbar").style.width=`${((current+1)/order.length)*100}%`;
  $("question").textContent=item.q.q;
  $("answers").innerHTML="";
  item.opts.forEach((opt,i)=>{
    const b=document.createElement("button");b.className="answer"+(answers[current]===i?" selected":"");b.type="button";
    const letter=document.createElement("span");letter.className="letter";letter.textContent=String.fromCharCode(65+i);
    const text=document.createElement("span");text.textContent=opt.text;
    b.append(letter,text);b.addEventListener("click",()=>{answers[current]=i;renderQuestion();});$("answers").appendChild(b);
  });
  $("prevBtn").disabled=current===0;
  $("nextBtn").textContent=current===order.length-1?"Завершить тест ✓":"Далее →";
}
function finishQuiz(){
  const score=answers.reduce((sum,ans,i)=>sum+(ans!==null&&order[i].opts[ans].correct?1:0),0);
  const pct=Math.round(score/questions.length*100);
  $("quiz").classList.add("hidden");$("result").classList.remove("hidden");
  $("score").textContent=`${score}/${questions.length}`;
  $("percent").textContent=`Правильных ответов: ${pct}%`;
  $("resultbar").style.width=pct+"%";
  $("resultMessage").textContent=pct>=90?"Отличный результат! Ты хорошо знаешь материал.":pct>=70?"Хороший результат! Повтори вопросы, в которых ошибся.":pct>=50?"Неплохо, но стоит повторить материал и попробовать ещё раз.":"Повтори материал и пройди тест ещё раз.";
  buildReview();
}
function buildReview(){
  const box=$("review");box.innerHTML="";
  order.forEach((item,i)=>{
    const chosen=answers[i]===null?null:item.opts[answers[i]];
    const correct=item.opts.find(x=>x.correct);
    const div=document.createElement("div");div.className="review";
    const h=document.createElement("h3");h.textContent=`${i+1}. ${item.q.q}`;div.appendChild(h);
    const p1=document.createElement("p");p1.className=chosen&&chosen.correct?"good":"bad";p1.textContent="Твой ответ: "+(chosen?chosen.text:"Ответ не выбран");div.appendChild(p1);
    const p2=document.createElement("p");p2.className="good";p2.textContent="Правильный ответ: "+correct.text;div.appendChild(p2);
    box.appendChild(div);
  });
}
$("startBtn").addEventListener("click",startQuiz);
$("prevBtn").addEventListener("click",()=>{if(current>0){current--;renderQuestion();}});
$("nextBtn").addEventListener("click",()=>{
  if(current<order.length-1){current++;renderQuestion();}
  else if(answers.some(a=>a===null)){const missing=answers.filter(a=>a===null).length;if(confirm(`Осталось вопросов без ответа: ${missing}. Завершить тест?`))finishQuiz();}
  else finishQuiz();
});
$("restartBtn").addEventListener("click",startQuiz);
$("reviewBtn").addEventListener("click",()=>{reviewShown=!reviewShown;$("review").classList.toggle("hidden",!reviewShown);$("reviewBtn").textContent=reviewShown?"Скрыть разбор":"Разобрать ответы";if(reviewShown)$("review").scrollIntoView({behavior:"smooth",block:"start"});});
</script>
</body>
</html>
