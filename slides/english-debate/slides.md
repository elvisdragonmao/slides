---
theme: ../_shared/theme-em
title: "Under Pressure | Intro to Debate"
titleTemplate: "%s — Mr. Mao"
author: Elvis Dragon Mao
htmlAttrs:
  lang: en
fonts:
  provider: none
  sans: "Avenir Next, Segoe UI, sans-serif"
  mono: "Menlo, Consolas, monospace"
layout: full
class: intro-profile
---

<div class="profile-main">
  <div>
    <h1>Elvis Dragon Mao</h1>
    <p class="full-name">You can call me Mr. Mao.</p>
    <ol class="timeline" aria-label="My path">
      <li><span>Home</span> Born in Taichung</li>
      <li v-click="1"><span>Elementary</span> Wagor Bilingual Elementary School 葳格雙語國小</li>
      <li v-click="2"><span>Junior high</span> St. Viator Catholic High School 天主教衛道國中</li>
      <li v-click="3"><span>Senior high</span> Taichung Municipal Shi-Yuan Senior High School 西苑高中</li>
      <li v-click="4"><span>University</span> National Yang Ming Chiao Tung University 陽明交大<small>BS in Computer Science · HCI research</small></li>
    </ol>
    <div v-click="5" class="profile-roles">Web developer · Designer · Debater</div>
    <p v-click="5" class="profile-debate">Public Forum instructor &amp; judge · Policy · WS · BP · Extemp</p>
    <p v-click="6" class="profile-story">I'm a <strong>furry</strong>, we love anthropomorphic animal characters.</p>
  </div>
  <figure v-click="7" class="fursona">
    <img src="./img/fursona.webp" alt="Mr. Mao’s blue and white fursona, raising a paw" />
    <figcaption>This is my <strong>fursona</strong>.</figcaption>
  </figure>
</div>

<!--
課前破冰。約 5 分鐘自介，之後留 Q&A 時間，按人數調整。先說 “Listen for one thing you’d like to ask me about.” 自介以你自己的故事為主，下面是可直接接的句子。

0:00–0:30 “My full name is Elvis Dragon Mao, but you can call me Mr. Mao. I was born in Taichung.”

[click:1] 0:30–1:00 “I went to Wagor Bilingual Elementary School.” 可以補一句你小學時的真實回憶。問 “What’s your favourite part of elementary school?”

[click:2] 1:00–1:30 “After that, I went to St. Viator Catholic High School.”

[click:3] 1:30–2:00 “Then I went to Taichung Municipal Shi-Yuan Senior High School.” 講一個真實的轉折，或把選校原因留給學生問。

[click:4] 2:00–3:00 “Now I’m working on a bachelor’s degree in computer science at NYCU. I study how people use computers and how we can make them easier to use. That’s called human-computer interaction, or HCI.” 可以請全班想一個很好用或很難用的網站。

[click:5] 3:00–3:35 “I build and design websites. I also teach and judge Public Forum debate. I’ve tried Policy, World Schools, British Parliamentary, and Extemp speaking.” 可用一句解釋評審工作 “I listen to both teams and decide who made the stronger case.” 不用逐個介紹賽制。

[click:6] 3:35–4:10 “When I was in high school, I competed in English debate.” 可以講一次印象深的比賽，或用 2025 年高中英語 PF 中區賽和隊友獲勝的經驗開頭。留一個細節讓學生問，例如那次辯什麼、跟隊友怎麼準備。經歷出自 [About](https://elvismao.com/about/)。

[click:7] 4:10–5:00 “I’m also a furry. I like animal characters that can talk and act like people. A fursona is an animal character someone uses to represent themselves. This one is mine.” 可以先等學生問，再細講角色。插圖取自你的 Eden 個人網站封面圖。

Q&A。“You can ask me anything about myself. Everyone gets to ask one question in English.” 留 20–30 秒想題，可先跟同桌試說。有人卡住時口頭給例句 “Why did you choose that high school?” / “What is a furry?” / “How did you start debating?” 依座位輪流，每人至少開口問一次。人多時，回答控制在一兩句。問完接 “You asked me to explain my story. Today we’ll ask questions to see how an argument works.”
-->

---
layout: cover
class: debate-cover
---

<div class="cover-grid">
  <div>
    <div class="eyebrow">Intro to Debate · Week 7 / Module 1</div>
    <h1>Under<br />Pressure</h1>
    <p>Find the <strong>weak point</strong><br />before your opponent does.</p>
  </div>
  <div class="cover-art" aria-hidden="true">
    <div class="cover-bubble"><ph-quotes /></div>
    <div class="cover-bubble cover-bubble-question" v-click><ph-question /></div>
  </div>
</div>

<!--
正課共 55 分鐘。六段依序為 Starter 5′、Argument X-Ray 10′、Pressure Ladder 10′、Assumption Hunt 10′、Targeted Defence 15′、Priority + Exit Ticket 5′。兩項加碼各 5′，有時間才繼續。準備白板、筆、學生筆記本和計時器。用空白鍵逐步揭示，按 O 看全頁總覽，從左下工具列開啟 Presenter Mode。投影給學生看一般簡報頁。

第一段 · 5 分鐘，含這頁到午餐因果鏈。用一句帶過舊知識 “You already know how to build arguments, explain impacts, use evidence and test reasoning.”
[click] “Today we’ll find the exact part of an argument an opponent might question.” 不用停在封面太久。
-->

---
layout: statement
class: big-question
---

<div class="eyebrow">Today’s big question</div>

# Which part of an argument<br />needs defending most?

<div v-click class="route">
  <span>Clarify</span><i>→</i><span>Unpack</span><i>→</i><span>Locate</span><i>→</i><span>Test</span><i>→</i><span>Defend</span><i>→</i><span>Prioritise</span>
</div>

<!--
把大問題寫在白板上，收尾會再回來回答。
[click] 簡單指過流程。用口語說 “First we ask what it means. Then we look inside it, find a weak spot, test it, answer the question and decide what to answer first.”
-->

---

<div class="eyebrow">Pressure starter</div>

## What do you mean?

<div class="speech">“Schools should have longer lunch breaks because it would be <strong>better</strong> for students.”</div>

<div class="grid grid-cols-2 gap-3 mt-6">
  <div v-click class="prompt-card">What do you mean?</div>
  <div v-click class="prompt-card">Better for whom?</div>
  <div v-click class="prompt-card">What actually changes?</div>
  <div v-click class="prompt-card">Why does that matter?</div>
</div>

<!--
先問 “Does this sound like an argument?” 接住直覺，請學生用下一步的問題來追問你的原句，保持節奏。
[click] “Better in what way?”
[click] “Which students would get the biggest benefit?”
[click] “What happens when lunch is longer?”
[click] “Why should the school care?” 若只說 “It needs more detail”，追問 “Which detail?” 先收問題，把解釋留到下一頁。
-->

---

<div class="eyebrow">Pressure starter</div>

## What did we add?

<div class="speech compact-speech">“Longer lunch is better because <strong>students like it</strong>.”</div>

<div class="flow lunch-flow" aria-label="Developed lunch argument">
  <div v-click="1" class="flow-card"><span>Longer lunch</span><b>More time after waiting for food</b></div>
  <span v-click="2" class="arrow" aria-hidden="true">→</span>
  <div v-click="2" class="flow-card"><span>What changes?</span><b>Students can eat without rushing</b></div>
  <span v-click="3" class="arrow" aria-hidden="true">→</span>
  <div v-click="3" class="flow-card"><span>Why it matters</span><b>Students may feel calmer and focus in class</b></div>
</div>

<p v-click class="takeaway">Which <strong>arrow</strong> would you question?</p>

<!--
先請學生指出薄弱版本缺什麼。參考 “It says students like it, but it doesn’t tell us what changes or why that matters.”
[click] 問多出的午餐時間發生在哪裡。
[click] 問這樣吃飯會有什麼差。
[click] 把三格讀成完整的因果推論。使用 may，因為不是必然。
[click] 示範可問 “Does eating more slowly really help students focus?” 或 “What if the lunch line gets longer too?” 接到 X-Ray，不用解完每個攻擊。
-->

---

<div class="eyebrow">Argument X-Ray</div>

## See what’s inside an argument

<div class="flow map-flow">
  <div class="flow-card"><span>Claim</span><b>What should we do?</b></div>
  <span v-click="1" class="arrow" aria-hidden="true">→</span>
  <div v-click="1" class="flow-card"><span>Starting reason</span><b>What’s the problem now?</b></div>
  <span v-click="2" class="arrow" aria-hidden="true">→</span>
  <div v-click="2" class="flow-card"><span>Mechanism</span><b>How does the change help?</b></div>
  <span v-click="3" class="arrow" aria-hidden="true">→</span>
  <div v-click="3" class="flow-card"><span>Impact</span><b>Why does it matter?</b></div>
</div>

<div v-click class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Copy this</div>
  <p>Claim → Starting Reason → Mechanism → Impact</p>
</div>

<!--
第二段 · 10 分鐘，含示範、找箭頭和小組練習。可以在白板畫這四格。先問誰記得 claim。
[click] Starting reason 是推理起點，也可能是一個現況或事實。
[click] Mechanism 是中間怎麼發生的，可以有兩步以上。
[click] Impact 是最後為什麼值得在意。
[click] 留 20–30 秒抄四格和箭頭。每一個箭頭是一個要解釋的連接。
-->

---
clicks: 5
---

<div class="eyebrow">Argument X-Ray · Teacher model</div>

## Would a later start help?

<div class="speech compact-speech">“Schools should start later because students need more sleep.”</div>

<div class="claim-tag">Claim <b>Schools should start later.</b></div>

<div class="flow sleep-flow">
  <div v-click="1" class="flow-card"><span>Starting reason</span><b>Many teens need more sleep</b></div>
  <span v-click="2" class="arrow" aria-hidden="true">→</span>
  <div v-click="2" class="flow-card" :class="{ 'weak-step': $clicks >= 5 }"><span>Mechanism 1</span><b>A later start may give them more sleep</b></div>
  <span v-click="3" class="arrow" aria-hidden="true">→</span>
  <div v-click="3" class="flow-card"><span>Mechanism 2</span><b>They may feel more awake</b></div>
  <span v-click="4" class="arrow" aria-hidden="true">→</span>
  <div v-click="4" class="flow-card"><span>Impact</span><b>They may focus better in early classes</b></div>
</div>

<p v-click="5" class="takeaway"><strong>Test this step.</strong> What if students go to bed later too?</p>

<!--
把 claim 放在推理鏈上方。它是結論；下面的理由、過程和影響串起來支持它。
[click:1] 示範現況。問 “What has to happen next for a later start to help?”
[click:2] 等到有人提到能睡比較久，再揭示 Mechanism 1。
[click:3] 問 “What changes when they get more sleep?”
[click:4] 問 “How might that help them in class?” 讀完這個鏈，請學生先指出自己想挑戰的箭頭。
[click:5] 揭示一個可能的弱點。問 “Does a later start guarantee more sleep?” 可以同意這條很弱，也可以選 alertness 到 focus。這是推理示範，若要在比賽主張實際成效，需要再找證據。
-->

---

<div class="eyebrow">Argument X-Ray · Pairs</div>

## Circle the weakest link

<div class="link-steps"><span>Later start</span><b>→</b><span>More sleep</span><b>→</b><span>More awake</span><b>→</b><span>Better focus</span></div>

<div class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Write one sentence</div>
  <p>The weakest link is <b>______</b> because an opponent could ask, “<b>______</b>?”</p>
</div>

<p class="action-line">Draw the chain. Circle <strong>one arrow</strong>. Compare with a partner.</p>

<!--
給約 45–60 秒。先在筆記本圈一條箭頭，再填句型。請兩組分享不同答案，重點是講清楚從哪一步到哪一步。
參考 “The weakest link is later start → more sleep because an opponent could ask, ‘What if students stay up later?’”
也可接受 “more awake → better focus” 搭配 “What if students are awake but still distracted?” 可口頭問交通或放學時間等成本，並請學生說它是在挑戰方案能否執行，或是某條因果箭頭。
-->

---

<div class="eyebrow">Argument X-Ray · Pairs</div>

## Give group projects an X-ray

<div class="speech">“Schools should give us more <strong>group projects</strong> because teamwork prepares us for the future.”</div>

<div class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Draw and fill in</div>
  <p>Claim → Starting Reason → Mechanism → Impact</p>
  <p class="small">Fill in the four parts. Circle one weak arrow and write a question about it.</p>
</div>

<!--
給兩人約 2 分鐘寫，再挑一組分享。每組至少寫一個中間步驟。
參考：Claim “Schools should give us more group projects.” Starting reason “We’ll often need to work with others in the future.” Mechanism “Students practise sharing jobs and listening to teammates.” Impact “They may be better at working in teams later.”
可能的弱箭頭 “group projects → practising teamwork”。問題 “What if one student does all the work?” 若同學從理由直接跳到影響，指著中間問 “What happens in between?”
-->

---

<div class="eyebrow">Pressure Ladder</div>

## Make your questions harder

<div class="ladder">
  <div class="ladder-rung" style="--level: 0; --accent: var(--cyan)"><b>1</b><div><span>Clarify</span><p>What exactly do you mean?</p></div></div>
  <div v-click class="ladder-rung" style="--level: 1; --accent: var(--green)"><b>2</b><div><span>Mechanism</span><p>How does that actually happen?</p></div></div>
  <div v-click class="ladder-rung" style="--level: 2; --accent: var(--orange)"><b>3</b><div><span>Assumption</span><p>What has to be true for that to work?</p></div></div>
  <div v-click class="ladder-rung" style="--level: 3; --accent: var(--pink)"><b>4</b><div><span>Significance</span><p>Even if it happens, why does it matter?</p></div></div>
</div>

<p v-click class="action-line"><ph-pencil-simple /> Copy the <strong>four questions</strong> into your notebook.</p>

<!--
第三段 · 10 分鐘，含手機示範、兩輪練習和快速回顧。用手勢一階一階往上。Level 1 問意思。
[click] Level 2 問中間怎麼發生，可用 how 當線索。
[click] Level 3 測試推理依賴的條件，可用 what if。
[click] Level 4 先暫時接受效果，再問這個效果值不值得在意。
[click] 留約 45 秒抄四個問題。需要支援可先抄 “What? / How? / What if …? / Why does it matter?”
-->

---

<div class="eyebrow">Pressure Ladder · Teacher model</div>

## Phones at lunch

<div class="speech compact-speech">“Students should be allowed to use phones during lunch.”</div>

<div class="question-stack">
  <div v-click><b>1 Clarify</b><span>What would students be allowed to do?</span></div>
  <div v-click><b>2 Mechanism</b><span>How could phones help students relax?</span></div>
  <div v-click><b>3 Assumption</b><span>What if they spend the whole break on their phones?</span></div>
  <div v-click><b>4 Significance</b><span>If they relax a little, why does it matter?</span></div>
</div>

<!--
讓學生先想一個可能的好處。示範用 “It could help students relax.” 每按一次讀新問題，示範不同種類的回答。
[click] “They could use phones after eating, in the lunch area.” 交代允許什麼。
[click] “Some could listen to music and take a quiet break after a busy morning.” 補過程。
[click] “The school could set a ten-minute phone window, so everyone still has time to eat and talk.” 處理會不會整段時間都用的疑問。
[click] “A short break could help tired students come back ready to pay attention.” 解釋這個好處的重要性。每次回答只用一兩句。
-->

---

<div class="eyebrow">Pressure Ladder · Round 1</div>

## No homework on weekends?

<div class="role-grid">
  <div class="panel"><div class="eyebrow"><ph-microphone /> Speaker A</div><p>Give a <strong>20–30 second</strong> argument for no weekend homework.</p><p class="small">Add a new detail in every answer.</p></div>
  <div class="panel"><div class="eyebrow"><ph-chats-circle /> Questioner B</div><p>Ask one question at each level. Wait for each answer.</p><p class="small">Clarify → Mechanism → Assumption → Significance</p></div>
</div>

<p class="action-line"><ph-pencil-simple /> Write the question that was <strong>hardest to answer</strong>.</p>

<!--
給 2–3 分鐘。逐級問與答，Questioner 先測試，這裡練問句。Speaker 有需要可用 “My reason is …” 起頭。
參考：1 “Does this include a project due on Monday?” 2 “How would a free weekend help students focus?” 3 “What if weekday homework just gets longer?” 4 “If students get a little extra free time, why should the school care?”
結尾請他們寫下一題最難回答的，問一組是第幾級、為什麼。
-->

---

<div class="eyebrow">Pressure Ladder · Round 2</div>

## AI for homework?

<div class="speech">“Students should be allowed to use <strong>AI for homework</strong>.”</div>

<div class="role-grid two-small">
  <div class="panel"><div class="eyebrow"><ph-microphone /> Speaker B</div><p>Give a 20–30 second argument. Add a new detail each time.</p></div>
  <div class="panel"><div class="eyebrow"><ph-chats-circle /> Questioner A</div><p>Climb all four levels. Ask, listen, then ask again.</p><p class="small">Clarify → Mechanism → Assumption → Significance</p></div>
</div>

<!--
先交換角色，給約 2–3 分鐘。如果學生卡住，可從「AI 可以給小提示」出發，試著問 1 “Can it give you the final answer?” 2 “How would a hint help you learn?” 3 “What if the hint is wrong?” 4 “If it saves five minutes, why does that matter?”
聽學生的回答是否補上新資訊。對重複答案問 “Can you tell me one new thing?”
-->

---

<div class="eyebrow">Pressure Ladder · Debrief</div>

## Which question made you think hardest?

<p class="takeaway">“Level <strong>______</strong> was hardest because <strong>______</strong>.”</p>

<div v-click class="panel quick-prompt">
  <div class="eyebrow">Quick round if we have time</div>
  <p>“Schools should give students more PE classes.”</p>
  <p class="small">Pick one level. Ask your partner a question.</p>
</div>

<!--
用學生筆記裡寫的問題做收束。請一兩組說哪一級最難，理由要具體。例 “Level 3 was hardest because I had to explain what happens if AI makes a mistake.”
[click] 時間夠才加一題 PE，可請學生只做一個來回。例 “What if the school has no space for extra PE classes?”（Assumption，活動需有場地）
-->

---

<div class="eyebrow">Hidden Assumption Hunt</div>

## What is the argument counting on?

<div class="speech compact-speech">“Schools should replace textbooks with tablets because <strong>tablets are lighter</strong>.”</div>

<div class="assumption-diagram">
  <div class="flow-card"><span>What we heard</span><b>Tablets are lighter</b></div>
  <div class="trapdoor" :class="{ 'is-open': $clicks >= 1 }">
    <span v-if="$clicks === 0">?</span>
    <div v-click="1"><small>Hidden assumption</small><b>Students can get the materials they need on tablets</b></div>
  </div>
  <div class="flow-card"><span>What we want</span><b>Tablets can take the place of books</b></div>
</div>

<div v-click="2" class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Copy this test</div>
  <p>If this were false, would the argument get weaker?</p>
  <p class="small">A hidden assumption is an unstated idea that the argument depends on.</p>
</div>

<!--
第四段 · 10 分鐘，含平板示範、四天上課小組練習和社區服務加碼。說 “A hidden assumption is something the argument needs to be true, but the speaker hasn’t said.” 問學生輕就足夠換掉課本嗎。
[click:1] 揭示「需要的教材能取得」。可再請學生找設備負擔得起、學生會恰當使用、書包變輕有意義等條件。
[click:2] 請學生抄測試句。假設沒有必要教材，輕的確還是輕，但取代課本的理由會變弱。隨機的抱怨（例如不喜歡某種顏色）要先過這個測試。
-->

---

<div class="eyebrow">Hidden Assumption Hunt · Teacher model</div>

## Turn an assumption into a question

<div class="reveal-rows">
  <div><b>Assumption</b><span>Tablets can provide the materials students need.</span></div>
  <div v-click><b>Question</b><span>What if some books or worksheets aren’t available on a tablet?</span></div>
  <div v-click><b>Possible defence</b><span>Use digital copies where we can. Keep paper for materials students still need.</span></div>
</div>

<!--
問 “How could an opponent test this?” 先等學生說問句。
[click] 這個問題測試教材可用性。追問如果電子版缺一兩樣，有沒有辦法維持大部分的好處。
[click] 示範保留部分紙本是如何接住這一點。請學生指出回答對應到哪個風險。也可接受先檢查或補齊電子教材再換成平板；不要假裝電子資源已經齊全。
-->

---

<div class="eyebrow">Hidden Assumption Hunt · Small groups</div>

## A four-day school week?

<div class="speech">“Students should go to school <strong>four days a week</strong> because they would have more free time.”</div>

<div class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Find two hidden assumptions</div>
  <p>For each one, write an <b>assumption</b>, a <b>question</b> and a possible <b>defence</b>.</p>
</div>

<p class="action-line">Choose one to share with the class.</p>

<!--
分小組，給約 4 分鐘。每組針對至少兩個假設各寫三項。先請同學問 “If we’re wrong about this, what happens to the argument?”
參考 1 “Four days still give us enough time to learn.” → “Would we have to miss important lessons?” → “We could test a revised timetable first and check if students still meet the learning goals.”
參考 2 “The extra day can really be free time.” → “What if the school gives us a day of extra work?” → “Keep homework at its usual amount during the trial.”
也可以談需要照顧安排的家庭，或多出的時間是否能讓學生受益。每組分享一個假設及防守，如果時間有限請兩組代表。
-->

---

<div class="eyebrow">Hidden Assumption Hunt · Stretch</div>

## Does helping make us care?

<div class="speech">“Schools should require community service because it teaches students to <strong>care about their communities</strong>.”</div>

<p class="takeaway">What has to be true for this to work?</p>

<!--
較快的組可在四天上課題後做。全班趕進度可以略過此頁。
參考假設 “Students get real chances to help people and see the difference they make.” 追問如果只是簽名或集時數，還能不能培養關心？可能方案：讓學生選一個有實際任務的服務計畫，並用一句話反思幫到了誰。先問具體哪個條件被威脅，再接下一段。
-->

---
layout: statement
class: defence-intro
---

<div class="eyebrow">Targeted Defence</div>

# Defend the<br />exact weak point.

<div class="defence-steps">
  <div v-click class="panel"><b>1</b> Hear the attack</div>
  <div v-click class="panel"><b>2</b> Name the weak point</div>
  <div v-click class="panel"><b>3</b> Answer that point</div>
</div>

<!--
第五段 · 15 分鐘。保留足夠時間給三輪練習，這是本節核心。
[click] “What did they say could go wrong?”
[click] “Which part of our reasoning or plan does that hurt?”
[click] “Give a new detail that deals with that exact problem.” 先請學生說被攻擊的點，再讓他們回答。這堂先不教 Module 2 的正式分類。
-->

---

<div class="eyebrow">Targeted Defence · Teacher model</div>

## Should students get a retake?

<div class="speech compact-speech">“Students should be allowed to retake major tests. One bad day shouldn’t decide their grade.”</div>

<div class="reveal-rows defence-rows">
  <div v-click><b>Attack</b><span>“They might study less for the <strong>first test</strong>.”</span></div>
  <div v-click><b>Weak point</b><span>Will students still prepare for the first test?</span></div>
  <div v-click><b>Defence</b><span>Allow <strong>one retake</strong> and ask students to <strong>correct their mistakes first</strong>.</span></div>
</div>

<!--
先讀主張，確認 retake 是再考一次。
[click] 英文追問 “What exactly is the opponent worried about?” 給時間讓學生說。
[click] 對方質疑的是第一次考試的準備動機。故意說 “Retakes are fair.” 問全班這句有沒有回答準備的問題。
[click] 完整口語示範 “We can allow only one retake and require students to correct their first test before trying again. This keeps the retake from being an easy extra try and gives students a chance to show what they’ve learned.” 問哪一段回到了誘因問題。
-->

---

<div class="eyebrow">Targeted Defence · Round 1</div>

## Later school starts

<div class="defence-round">
  <div>
    <div class="panel round-claim"><div class="eyebrow">Claim</div><p>Schools should start later so students can get more sleep.</p></div>
    <div v-click="1" class="panel round-attack"><div class="eyebrow">Attack</div><p>“Students might just go to bed later.”</p></div>
  </div>
  <PrepTimer v-click="1" :inert="$clicks < 1" :seconds="60" />
</div>

<div v-click="1" class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Write, then say it</div>
  <p>They’re questioning <b>______</b>. We can answer by <b>______</b>.</p>
</div>

<!--
兩人或三人一組。可分答辯者、寫筆記的人、檢查是否切題的聽眾。
[click:1] 揭示攻擊，在投影的簡報視窗按 Start 給約 60 秒，先寫被攻擊的連接，再寫答句。提醒 “Go to bed later” 跟 “sleep more” 有何關係。
參考 “They’re questioning whether a later start will really give us more sleep. We can try a later start for a month, help students keep their usual bedtime, and check how much extra sleep they actually get.”
也可說 “Students who already keep the same bedtime could use the extra morning time to sleep longer.” 接受有條件且合理的回答。分享後問 “Did they answer the actual attack?”
-->

---

<div class="eyebrow">Targeted Defence · Round 2</div>

## Phones in lessons

<div class="defence-round">
  <div>
    <div class="panel round-claim"><div class="eyebrow">Claim</div><p>Schools should limit phones during lessons to cut distractions.</p></div>
    <div v-click="1" class="panel round-attack"><div class="eyebrow">Attack</div><p>“Phones are sometimes useful for learning.”</p></div>
  </div>
  <PrepTimer v-click="1" :inert="$clicks < 1" :seconds="40" />
</div>

<p v-click="1" class="action-line">Name the <strong>weak point</strong>. Give one sentence that answers it.</p>

<!--
[click:1] 在投影的簡報視窗按 Start，給約 40 秒，減少準備時間。請上輪的聽眾現在回答。
參考 “Keep phones away during most of the lesson. Teachers can ask students to take them out for a class activity, then put them away again.” 被攻擊的是限制是否也會擋掉有效的學習用途。問聽眾 “What did the speaker defend?” 若回答只重複手機會讓人分心，請補上對學習用途的處理。
-->

---

<div class="eyebrow">Targeted Defence · Round 3</div>

## Required community service

<div class="defence-round">
  <div>
    <div class="panel round-claim"><div class="eyebrow">Claim</div><p>Schools should require community service to help students care about their community.</p></div>
    <div v-click="1" class="panel round-attack"><div class="eyebrow">Attack</div><p>“If students are forced to do it, they may only do it to finish their hours.”</p></div>
  </div>
  <PrepTimer v-click="1" :inert="$clicks < 1" :seconds="20" />
</div>

<p v-click="1" class="action-line">Listen for the exact attack. <strong>Answer it out loud.</strong></p>

<!--
[click:1] 在投影的簡報視窗按 Start，給約 20 秒，這次直接說。重點是學生會不會投入、服務能不能帶來關心。教案原句 “Forced volunteering is not genuine volunteering.”，頁面改成容易判斷機制的問法。
參考 “Students can choose a cause they care about and do a job with a visible result. Seeing who they helped gives them a reason to care beyond just finishing the hours.” 問哪個條件讓連結更合理。回饋依次問 “What was the exact attack? What did the speaker defend? Did the answer make that link stronger?”
-->

---

<div class="eyebrow">Defence priority</div>

## Which attack would you answer first?

<div class="speech compact-speech">“Schools should give every student a tablet.”</div>

<div class="attack-grid">
  <div class="panel"><b>A</b> Batteries can run out.</div>
  <div class="panel"><b>B</b> Tablets can distract students.</div>
  <div class="panel"><b>C</b> Tablets are expensive to buy and fix.</div>
  <div class="panel"><b>D</b> Some students prefer writing by hand.</div>
</div>

<div class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Rank, then compare</div>
  <p>Write A, B, C and D in order from <b>most</b> to <b>least</b> dangerous.</p>
</div>

<!--
第六段 · 5 分鐘，含 exit ticket。約 45 秒獨自排名，接著和同桌比較。請兩三組說第一名，以及攻擊成立會造成什麼。
參考 C → B → A → D。若學校付不起設備和維修，承諾人人有平板可能無法執行。B 也可排第一，例如核心好處是學習而分心使學習成效變差。A 可藉充電措施降低影響；D 在某些活動仍可保留手寫，也可能挑戰學習需求。允許不同排序，請說受到威脅的是不是整個計畫、主要效果或只有一小部分。這段重點是先答哪個，不用逐個反駁。
-->

---
layout: statement
class: exit-slide
---

<div class="eyebrow">Exit ticket · One sentence</div>

# What would you<br />defend first?

<div class="notebook text-left">
  <div class="eyebrow"><ph-pencil-simple /> Write in your notebook</div>
  <p>The most important attack to answer is <b>______</b> because if we cannot answer it, <b>______</b>.</p>
</div>

<p v-click class="takeaway">Protect the link your argument needs most.</p>

<!--
留約 45–60 秒寫出最後一句。參考 “The most important attack to answer is the cost because if we cannot answer it, the school might not be able to give everyone a tablet.” 問一兩人讀出來，回扣白板大問題。可快速檢查三個目標：是否指出一條弱連接或隱藏假設、是否能切題接住攻擊、是否根據後果決定優先順序。
[click] 口頭回想 “Clarify → Unpack → Locate → Test → Defend → Prioritise.” 預告 “Next time, we’ll decide what to say when an attack is right, or partly right.” 到這裡即可下課。後面兩項各約 5 分鐘，有空再做。
-->

---

<div class="eyebrow">If time allows · Assumption Flip</div>

## Rebuild before the attack

<div class="speech compact-speech">“Schools should use more online textbooks because <strong>every student already has a device</strong>.”</div>

<p class="takeaway">What if some students don’t have one?</p>

<div class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Rewrite the plan</div>
  <p>Schools could use online textbooks and <b>______</b>.</p>
</div>

<p v-click class="action-line">Try again with homework choice. What if students don’t know what they need to practise?</p>

<!--
加碼 A · 5 分鐘。兩人找出原案依賴人人有合適裝置，然後把提案改到比較少依賴這個假設。參考 “Schools could provide digital textbooks and lend devices to students who need them.” 問這樣是主張人人已有裝置，還是改了提案。
[click] 第二題完整論點 “Schools should give students more homework choice because students always know which type of practice they need.” 參考 “Teachers can offer two suitable practice options based on each student’s needs, and students can choose between them.” 請一組分享，看看是否還留著原先立場。
-->

---

<div class="eyebrow">If time allows · Clarify or Clash?</div>

## Sort the questions

<div class="speech compact-speech">“Schools should do more <strong>outdoor learning</strong>.”</div>

<div class="sort-grid">
  <div v-click="1" class="panel">How would being outside help us learn?<span v-click="5">Mechanism</span></div>
  <div v-click="2" class="panel">What if some lessons need to stay indoors?<span v-click="5">Assumption</span></div>
  <div v-click="3" class="panel">What counts as outdoor learning?<span v-click="5">Clarify</span></div>
  <div v-click="4" class="panel">If students enjoy it more, why does that matter?<span v-click="5">Significance</span></div>
</div>

<!--
加碼 B · 5 分鐘，含本頁與下一頁。快速分類，不用回答每一題，可比 1–4 根手指代表階梯。
[click:1] 問效果怎麼發生。
[click:2] 問是不是預設很多課可以搬到戶外。請學生說出假設。
[click:3] 問在講什麼。
[click:4] 先接受更喜歡在戶外，再問喜歡的教育意義。
[click:5] 一次揭示四個分類。可以請學生說哪個詞讓他猜對。
-->

---

<div class="eyebrow">If time allows · Clarify or Clash?</div>

## Write four challenges

<div class="speech">“Students should be allowed to choose <strong>some of their school subjects</strong>.”</div>

<div class="notebook">
  <div class="eyebrow"><ph-pencil-simple /> Write and trade</div>
  <p>Write one question for each level. Trade with another pair and <b>sort their questions</b>.</p>
  <p class="small">Clarify · Mechanism · Assumption · Significance</p>
</div>

<!--
兩人合寫四題，先不要在交換版上標類別；可以在筆記本左欄寫四題、右欄保留自己的標記，交換時只念題目。
參考 1 “Which subjects could students choose?” 2 “How would choosing a subject help students learn?” 3 “What if students choose only classes they think are easy?” 4 “If they enjoy two classes more, why would that matter for their education?”
最後問 “Why should we know what kind of question it is before we answer?” 收在 “It helps us defend the right part of our argument.”
-->
