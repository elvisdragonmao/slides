---
theme: ../_shared/theme-em
title: 棚拍攝影入門
titleTemplate: "%s — 毛哥EM"
author: 毛哥EM
---

# 棚拍攝影入門

從 Auto 拍爽到 Lightroom 調色輸出

毛哥EM ・ 陽明交大創創工坊

<ph-camera class="absolute right-24 top-1/2 -mt-28 text-[14rem] opacity-80" />

---
layout: statement
class: say
---

<div class="eyebrow">文章教學</div>

這份簡報可以搭配文章一起服用

<div class="qr mt-8">
<img src="./img/course-qr.svg" alt="文章教學 QR Code" />
</div>

<div class="sub mt-4">
<a href="https://emtech.cc/course/ict/photography/">emtech.cc/course/ict/photography</a>
</div>

---
src: ../global/me.md
---

---

<div class="eyebrow">Today</div>

## 今天會做什麼？

<div class="grid grid-cols-4 gap-4 mt-6">
<div class="card">
<ph-device-mobile class="card-icon" />
<h3>破題</h3>
<p class="dim">相機和手機<br />到底差在哪</p>
</div>
<div class="card">
<ph-camera class="card-icon" />
<h3>拍爽</h3>
<p class="dim">認識相機<br />Auto 拍第一張<br />構圖、拍狐狸</p>
</div>
<div class="card">
<ph-sliders class="card-icon" />
<h3>參數</h3>
<p class="dim">光圈、快門、ISO<br />測光、白平衡<br />白黑綠背景</p>
</div>
<div class="card">
<ph-palette class="card-icon" />
<h3>Lightroom</h3>
<p class="dim">挑片、調色<br />遮色片<br />匯出到 IG</p>
</div>
</div>

<p class="lead !mt-10">今天的主角：<strong>Canon EOS 6D Mark II</strong> + <strong>EF 24-105mm</strong>，還有一隻狐狸。</p>

---
layout: section
---

<div class="eyebrow">Chapter 01</div>

# 相機跟手機差在哪？

---
layout: statement
class: say
---

你的手機可能比這台相機還新。

<p v-click>4800 萬畫素 vs 2620 萬畫素，200 克 vs 1.5 公斤。</p>

<p v-click class="muted">那為什麼大家還要扛相機？</p>

---
layout: statement
class: say
---

手機靠「算」，相機靠「物理」。

<p v-click class="sub !mt-6">手機按一次快門會連拍好幾張，對齊、合成、降噪、提亮、加飽和、加銳利，給你一張「已經修好」的照片。</p>

---

<div class="eyebrow">Spec</div>

## 規格放在一起看

<div class="table-clean table-tight mt-4">

|            | Canon 6D Mark II             | iPhone 17 Pro 主鏡頭              |
| ---------- | ---------------------------- | --------------------------------- |
| 感光元件   | 35.9 × 24 mm（全片幅）       | 約 10 × 7.6 mm（1/1.28 吋型）     |
| 面積       | 約 862 mm²                   | 約 76 mm²（大約是相機的 1/11）    |
| 畫素       | 2620 萬                      | 4800 萬（平常合併成 2400 萬輸出） |
| 鏡頭上寫的 | 24–105 mm f/4（實際焦距）    | 「24 mm」f/1.78（等效焦距）       |
| 實際焦距   | 24–105 mm                    | 約 7 mm                           |
| 快門       | 1/4000 秒到 30 秒，還有 B 門 | 系統自己決定                      |
| 棚燈閃燈   | 可以接觸發器同步             | 基本上不行                        |
| 重量       | 機身＋鏡頭約 1.56 kg         | 約 206 g                          |

</div>

---

<div class="eyebrow">Sensor</div>

## 感光元件：面積差 11 倍

<div class="sensors mt-10">
<div>
<div class="sensor is-ff">35.9 × 24 mm</div>
<div class="sensor-label">6D Mark II 全片幅</div>
</div>
<div>
<div class="sensor is-phone">10 × 7.6</div>
<div class="sensor-label">手機主鏡頭</div>
</div>
</div>

<p class="lead text-center !mt-8">面積越大，收到的光越多 → 雜訊越少、亮部暗部細節越多。</p>

<p v-click class="muted text-center">「1 吋」其實對角線只有約 16 mm，是真空管時代留下來的命名。</p>

---

<div class="eyebrow">Aperture</div>

## 光圈數字騙不了物理

<div class="pupils mt-8">
<div class="text-center">
<div class="pupil" style="width: 20px; height: 20px"></div>
<p class="mono !mt-4">手機 7 mm f/1.78</p>
<p class="num">≈ 4 mm</p>
</div>
<div class="text-center">
<div class="pupil" style="width: 130px; height: 130px"></div>
<p class="mono !mt-4">相機 105 mm f/4</p>
<p class="num">≈ 26 mm</p>
</div>
</div>

<p class="lead text-center !mt-6">f 值是比例：<strong>焦距 ÷ 開口直徑</strong>。背景能糊多少，看的是<strong>開口的實際大小</strong>。</p>

<p v-click class="muted text-center">換算成全片幅，手機主鏡頭的景深效果大約等於 f/6。</p>

---

<div class="eyebrow">Bokeh</div>

## 背景模糊：真的和算的

<div class="grid grid-cols-2 gap-8 mt-6">
<div class="card">
<ph-cpu class="card-icon" />
<h3>手機人像模式</h3>
<p class="dim">先猜一張深度圖，再用演算法把背景糊掉</p>
<ul class="dim">
<li>頭髮、<strong>毛</strong>、鬍鬚：剪貼感、光暈</li>
<li>玻璃、眼鏡：透明的猜不準</li>
<li>地板：糊得一層一層的</li>
</ul>
</div>
<div class="card">
<ph-aperture class="card-icon" />
<h3>相機光學模糊</h3>
<p class="dim">光真的沒有對在那裡</p>
<ul class="dim">
<li>毛邊自然</li>
<li>從前景到背景漸進地變糊</li>
<li>不用猜</li>
</ul>
</div>
</div>

<p v-click class="lead text-center !mt-8">今天的主角狐狸，<strong>全身都是毛</strong>。等一下用手機人像模式拍拍看，放大看耳朵和尾巴。</p>

---

<div class="eyebrow">Why Camera</div>

## 差距在這裡被拉開

<div class="grid grid-cols-4 gap-4 mt-6">
<div class="card">
<ph-person-simple-walk class="card-icon" />
<h3>會動的東西</h3>
<p class="dim">夜景模式要你不能動。相機直接 1/500 秒凝結。<br /><strong>雜訊可以降，糊掉救不回來。</strong></p>
</div>
<div class="card">
<ph-lightning class="card-icon" />
<h3>棚燈</h3>
<p class="dim">閃燈只亮千分之一秒，相機用觸發器在 1/180 秒內同步。手機的閃光燈是手電筒。</p>
</div>
<div class="card">
<ph-file-image class="card-icon" />
<h3>RAW</h3>
<p class="dim">感光元件的原始資料，白平衡、亮部、暗部事後都能大改。直出看起來「灰」是留給你修的。</p>
</div>
<div class="card">
<ph-magnifying-glass-plus class="card-icon" />
<h3>變焦</h3>
<p class="dim">24–105 全是光學變焦，同一塊感光元件。手機的 2×、8× 其實是裁切。</p>
</div>
</div>

---

<div class="eyebrow">Fair</div>

## 公平起見，手機也有贏的地方

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<div>

- **永遠帶在身上**：最好的相機就是你身上那一台
- **逆光、大光比**：自動 HDR，直出就平衡
- **即拍即分享**，自動備份
- **錄影**：4K、防手震超強；6D II 只到 1080p
- **輕**：超廣角到望遠都在口袋裡

</div>
<div class="card">
<h3>縮小看分不出來，放大差很多</h3>
<p class="dim">只在手機上看、只發 IG，很多時候真的看不太出來。放大到 100%、投影到大螢幕或印出來，差距就很明顯。</p>
</div>
</div>

<p v-click class="lead text-center !mt-8">沒有最好的相機，只有最適合情境的相機。</p>

---
layout: section
---

<div class="eyebrow">Chapter 02</div>

# 認識你手上的相機

---

<div class="eyebrow">Canon EOS 6D Mark II</div>

## 2017 年的全片幅單眼

<div class="grid grid-cols-2 gap-10 mt-6">
<div>

- 2620 萬畫素全片幅
- ISO 100–40000
- 快門 1/4000 秒到 30 秒
- 光學觀景窗，視野率約 98%
- 翻轉觸控螢幕
- Wi-Fi、藍牙傳手機

</div>
<div class="card">
<h3>鏡頭：EF 24-105mm</h3>
<p class="dim">看鏡頭前端的紅圈和字：</p>
<ul class="dim">
<li><strong>L 版</strong> f/4L IS II USM：全焦段 f/4</li>
<li><strong>STM 版</strong> f/3.5-5.6 IS STM：24mm f/3.5，105mm f/5.6</li>
</ul>
</div>
</div>

---

<div class="eyebrow">Buttons</div>

## 機身按鈕

<div class="table-clean table-tight mt-2">

| 名稱                  | 位置               | 做什麼                                       |
| --------------------- | ------------------ | -------------------------------------------- |
| 快門按鈕              | 右手食指           | **半按**對焦和測光，**全按**拍照             |
| 主轉盤                | 快門後面，食指轉   | 改快門或光圈（看模式）                       |
| 模式轉盤              | 機頂左邊           | A+、P、Tv、Av、M。**按住中間的鎖鈕才轉得動** |
| AF、DRIVE、ISO、測光  | 機頂液晶面板前面   | 按一下，再轉轉盤就能改                       |
| 觀景窗                | 機背上方           | 旁邊有**屈光度調整鈕**                       |
| 速控轉盤              | 機背大圓盤，拇指轉 | 曝光補償（M 模式下改光圈）                   |
| 多功能控制器          | 速控轉盤內圈       | 8 個方向，移動對焦點、操作選單，中間是 SET   |
| LOCK 開關             | 速控轉盤下方       | **轉盤轉不動，先看這裡**                     |
| Q 按鈕                | 機背               | 速控畫面，直接在螢幕上點選修改               |
| Live View＋START/STOP | 觀景窗右邊         | 改用螢幕拍照                                 |
| 播放、放大、刪除      | 機背右側           | 看照片                                       |

</div>

---

<div class="eyebrow">Lens</div>

## 鏡頭上的開關

<div class="grid grid-cols-2 gap-6 mt-6">
<div class="card">
<h3>AF / MF</h3>
<p class="dim">平常撥在 <strong>AF</strong>。「相機怎麼不對焦了」最常見的原因。</p>
</div>
<div class="card">
<h3>STABILIZER</h3>
<p class="dim">手持開 <strong>ON</strong>。只修正你的手晃，<strong>修正不了狐狸在動</strong>。</p>
</div>
<div class="card">
<h3>變焦環＋變焦鎖</h3>
<p class="dim">24mm（廣）↔ 105mm（近）。<strong>先變焦，再對焦。</strong>轉不動就檢查鎖。</p>
</div>
<div class="card">
<h3>最近對焦距離</h3>
<p class="dim">L 版約 45 cm、STM 版約 40 cm。再近就對不到焦。</p>
</div>
</div>

---

<div class="eyebrow">Hold</div>

## 拿相機的方法

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<ol class="steps lead">
<li><span class="n">1</span>先把背帶掛上脖子</li>
<li><span class="n">2</span>右手握握把，<strong>左手掌心朝上托鏡頭</strong></li>
<li><span class="n">3</span>雙肘夾緊，一腳往前站穩</li>
<li><span class="n">4</span>用觀景窗時，相機貼著臉</li>
<li><span class="n">5</span>移動時永遠托著鏡頭</li>
</ol>
<div class="card">
<h3 class="bad">不要做的事</h3>
<ul class="dim">
<li>指示燈亮著時開卡蓋、拔電池</li>
<li>鏡頭或觀景窗對著太陽、強燈</li>
<li>自己拆鏡頭、清感光元件</li>
</ul>
<p class="muted !mt-3">有問題請舉手。</p>
</div>
</div>

---
layout: section
---

<div class="eyebrow">Chapter 03</div>

# 先用 Auto 拍爽

<p class="muted">不用懂任何參數，先拍出第一張清楚的照片。</p>

---

<div class="eyebrow">Auto</div>

## 九步拍出第一張

<div class="grid grid-cols-2 gap-10 mt-4">
<ol class="steps">
<li><span class="n">1</span>電池、SD 卡裝好，蓋子蓋上</li>
<li><span class="n">2</span>拿下鏡頭蓋，<strong>AF</strong>、防手震 <strong>ON</strong>、變焦鎖解開</li>
<li><span class="n">3</span>電源 <strong>ON</strong></li>
<li><span class="n">4</span>按住鎖鈕，模式轉盤轉到 <strong>A+</strong></li>
<li><span class="n">5</span>看觀景窗，字模糊就轉<strong>屈光度調整鈕</strong></li>
</ol>
<ol class="steps">
<li><span class="n">6</span>轉變焦環決定要拍多大</li>
<li><span class="n">7</span><strong>半按快門</strong>：嗶一聲、綠點亮 = 對到焦</li>
<li><span class="n">8</span><strong>全按快門</strong>拍下去</li>
<li><span class="n">9</span>播放鍵看照片，放大鍵＋主轉盤檢查焦點</li>
</ol>
</div>

<p v-click class="lead text-center !mt-8">恭喜，你已經會用單眼相機了。</p>

---

<div class="eyebrow">Live View</div>

## 改用螢幕拍

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<ol class="steps lead">
<li><span class="n">1</span>開關撥到相機圖示，按 <kbd>START/STOP</kbd></li>
<li><span class="n">2</span>把螢幕翻出來</li>
<li><span class="n">3</span><strong>點螢幕上想對焦的地方</strong>，例如狐狸的眼睛</li>
<li><span class="n">4</span>按快門</li>
</ol>
<div class="card">
<h3>什麼時候用</h3>
<p class="dim">不想貼著臉、要拍很低或很高的角度。</p>
<p class="muted !mt-3">比較耗電：觀景窗約 1200 張，Live View 約 380 張。</p>
</div>
</div>

---

<div class="eyebrow">Troubleshooting</div>

## 卡關了？

<div class="table-clean table-tight mt-2">

| 狀況                      | 解法                                                   |
| ------------------------- | ------------------------------------------------------ |
| 快門按不下去，綠點一直閃  | 對有明暗交界的地方。**純色背景布對不到焦**，太近就退後 |
| 半按完全不對焦            | 鏡頭撥回 AF                                            |
| 觀景窗模糊                | 轉屈光度調整鈕                                         |
| 觀景窗全黑                | 關掉 Live View；拿下鏡頭蓋                             |
| 模式轉盤轉不動            | 按住中間的鎖鈕再轉                                     |
| 速控轉盤轉不動，出現 LOCK | 把 LOCK 開關撥開                                       |
| 變焦環轉不動              | 在 24mm 把變焦鎖撥開                                   |
| 按快門要等 10 秒          | DRIVE 改回單張                                         |
| 照片變黑白                | 舉手，我們幫你改回來                                   |
| 一直自己關機              | 半按快門就會醒來                                       |

</div>

---
layout: statement
class: say
---

<div class="eyebrow">Practice</div>

先去拍個爽。

<p class="sub !mt-6">相機用 A+，手機也拿出來拍同一隻狐狸，等一下比較。</p>

---
layout: section
---

<div class="eyebrow">Chapter 04</div>

# 構圖

---
layout: statement
class: say
---

構圖只有一個目的：

<p v-click>讓看照片的人知道<strong>該看哪裡</strong>。</p>

<p v-click class="sub !mt-6">就算用 Auto，位置、高度、距離、焦段全部都還在你手上。</p>

---

<div class="eyebrow">Attention</div>

## 人的眼睛先看什麼？

<div class="grid grid-cols-4 gap-4 mt-6">
<div class="card"><p class="num">1</p><h3>最亮的地方</h3></div>
<div class="card"><p class="num">2</p><h3>最鮮豔的顏色</h3></div>
<div class="card"><p class="num">3</p><h3>對比最強的地方</h3></div>
<div class="card"><p class="num">4</p><h3>臉</h3><p class="dim">包括狐狸的臉</p></div>
</div>

<p class="lead !mt-8">橘色、有臉的狐狸放在白、黑、綠背景前，幾乎一定是畫面中最搶眼的東西。</p>

<p v-click class="lead">反過來說，角落一小塊亮亮的燈架、一條白膠帶，就會把視線偷走。</p>

---

<div class="eyebrow">Subtraction</div>

## 先決定主角，再做減法

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<div>
<p class="lead">這張照片的主角是誰？把所有跟主角無關的東西移出畫面。</p>
<p class="lead">無縫背景已經幫你做了大部分的減法。你要做的是別讓<strong>燈架、背景布的邊、膠帶、同學的腳</strong>跑進來。</p>
</div>
<div class="card">
<h3>加道具時</h3>
<p class="dim">一次加一個，每加一個就問：</p>
<p class="big !mt-3">它在幫狐狸，<br />還是在搶戲？</p>
</div>
</div>

---

<div class="eyebrow">Rule of Thirds</div>

## 三分法

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<div class="thirds">
<div class="dot" style="left: 33.33%; top: 33.33%"></div>
</div>
<div>

- 構圖沒想法時最好用的**安全牌**
- 放在線上的是狐狸的**眼睛**，不是整隻狐狸的中心
- 狐狸面向右，就放左邊，讓右邊有「看的空間」

<p v-click class="muted !mt-6">但研究發現它跟好不好看只有很弱的關係。重點是你知道自己為什麼這樣放。</p>

</div>
</div>

---

<div class="eyebrow">Layout</div>

## 其他放法

<div class="grid grid-cols-3 gap-4 mt-6">
<div class="card">
<h3>置中與對稱</h3>
<p class="dim">狐狸正面、正中央、相機對齊眼睛高度，背景純黑或純白，像肖像畫。<strong>差一點點對稱最難看。</strong></p>
</div>
<div class="card">
<h3>留白</h3>
<p class="dim">狐狸只佔一小部分。白背景乾淨、像雪地；黑背景孤單、神祕。<strong>狐狸要看向空的那一邊。</strong></p>
</div>
<div class="card">
<h3>填滿畫面</h3>
<p class="dim">靠近，讓臉塞滿畫面，耳朵切掉一點也沒關係。太近對不到焦就退一步、拉 105mm。</p>
</div>
</div>

<p v-click class="lead text-center !mt-8">「如果你的照片不夠好，那是因為你靠得不夠近。」<span class="muted">—— Robert Capa</span></p>

---

<div class="eyebrow">Cropping</div>

## 頭頂空間與裁切

<div class="grid grid-cols-3 gap-4 mt-6">
<div class="card">
<h3>頭頂空間</h3>
<p class="dim">主角放正中間，頭上空一大塊，看起來像往下沉。眼睛放在上方三分之一的線附近。</p>
</div>
<div class="card">
<h3>不要切在關節</h3>
<p class="dim">腳踝、膝蓋、手肘、手腕會像被截肢。要切就切在關節之間。</p>
</div>
<div class="card">
<h3>不要「差一點點」</h3>
<p class="dim">耳朵尖剛好碰到邊緣最像失誤。要嘛留空間，要嘛果斷多切一點。</p>
</div>
</div>

---

<div class="eyebrow">Height</div>

## 換個高度

<p class="lead">站著往下看，是我們每天看世界的方式，也是<strong>最無聊的角度</strong>。拍動物的共識：<strong>降到牠眼睛的高度</strong>。</p>

<div class="grid grid-cols-3 gap-4 mt-6">
<div class="card">
<h3>俯拍</h3>
<p class="dim">狐狸看起來渺小、可憐。背景變成地上的布，最乾淨。</p>
</div>
<div class="card">
<h3>平視</h3>
<p class="dim">平等、親近，像在跟牠對話。</p>
</div>
<div class="card">
<h3>仰拍</h3>
<p class="dim">很有氣勢。但很容易拍到背景布上緣或天花板。</p>
</div>
</div>

<p v-click class="muted text-center !mt-6">不想趴？打開 Live View、把螢幕翻上來貼地拍。</p>

---

<div class="eyebrow">Tricks</div>

## 其他好用的技巧

<div class="grid grid-cols-2 gap-x-10 gap-y-2 mt-6 lead">
<p><strong>引導線</strong>：一排積木、一條繩子從角落往狐狸延伸</p>
<p><strong>框架</strong>：手、紙箱開口、空相框放在鏡頭前</p>
<p><strong>對角線</strong>：狐狸斜著擺比正面擺更有動感</p>
<p><strong>前中後景</strong>：鏡頭前放失焦的東西，後面再放一個道具</p>
<p><strong>奇數</strong>：狐狸加兩個道具，通常比兩個、四個有趣</p>
</div>

---

<div class="eyebrow">Shot Size</div>

## 景別：遠一點還是近一點

<div class="table-clean mt-4">

| 景別 | 狐狸怎麼拍                   | 用途             |
| ---- | ---------------------------- | ---------------- |
| 遠景 | 狐狸很小，周圍的空間佔滿畫面 | 交代環境、孤獨感 |
| 全景 | 整隻狐狸，包括尾巴和腳       | 介紹主角         |
| 中景 | 狐狸的上半身                 | 動作             |
| 特寫 | 狐狸的臉塞滿畫面             | 情緒             |
| 細節 | 眼睛、鼻子、毛               | 質感、故事線索   |

</div>

<p v-click class="lead text-center !mt-6">全景、中景、特寫、細節排在一起，就是一個小故事。</p>

---

<div class="eyebrow">Focal Length</div>

## 24mm 和 105mm 差在哪？

<div class="grid grid-cols-2 gap-6 mt-6">
<div class="card">
<h3>24mm：貼得很近</h3>
<p class="dim">背景帶進一大片，布邊、燈架幾乎一定穿幫。鼻子變大、耳朵變小。</p>
</div>
<div class="card">
<h3>105mm：退得很遠</h3>
<p class="dim">背景只剩狐狸後面一小塊乾淨的布，臉的比例也比較自然。</p>
</div>
</div>

<p class="lead text-center !mt-8">真正改變遠近比例的是<strong>拍攝距離</strong>，焦段只是逼你站在不同的地方。</p>

<p v-click class="muted text-center">用腳變焦：先決定焦段，再用腳移動構圖，最後才用變焦環微調。</p>

---

<div class="eyebrow">Edge Patrol</div>

## 按快門前：邊界巡邏

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<div>
<p class="lead">用眼睛沿著畫面四邊繞一圈：</p>
<ul class="lead">
<li>燈架、電線、膠帶？</li>
<li>背景布的邊？</li>
<li>同學的腳？</li>
<li>有沒有東西從狐狸頭上「長出來」？</li>
</ul>
</div>
<div class="card">
<h3>觀景窗只看到 98%</h3>
<p class="dim">照片邊緣會比你看到的多一點。仔細檢查時用 Live View，或拍完放大看四個角。</p>
<p class="muted !mt-3">格線、水平儀已經先打開了，水平儀按 INFO 叫出來。</p>
</div>
</div>

---
layout: section
---

<div class="eyebrow">Chapter 05</div>

# 練習：幫狐狸拍照

<ph-paw-print class="text-6xl mx-auto mt-6" />

---

<div class="eyebrow">Missions</div>

## 任務

<div class="table-clean table-tight mt-2">

| 任務               | 時間    | 內容                                                                         |
| ------------------ | ------- | ---------------------------------------------------------------------------- |
| 一隻狐狸，五種構圖 | 10 分鐘 | **不准動狐狸，只能動你自己**。置中、三分法、留白一半以上、塞滿畫面、自選一種 |
| 三種高度           | 5 分鐘  | 俯拍、平視、仰拍。哪一張最勇敢？哪一張最孤單？                               |
| 只用 105mm         | 5 分鐘  | 變焦環固定 105mm，只能靠走路拍出全景、中景、特寫                             |
| 留白一半           | 5 分鐘  | 狐狸佔四分之一以下，看向空的那邊。白、黑背景各一張                           |
| 四格故事           | 8 分鐘  | 全景、中景、特寫、細節，例如「狐狸發現了一本書」                             |
| 邊界巡邏           | 3 分鐘  | 棚裡藏了幾個「穿幫物」，拍一張四邊完全乾淨的照片                             |

</div>

<p class="muted !mt-4 text-center">輪流用相機，等待時用手機練同一個任務。每個任務結束，<strong>每組選出最好的一張</strong>。</p>

---

<div class="eyebrow">Critique</div>

## 看照片的時候怎麼講

<div class="grid grid-cols-3 gap-4 mt-6">
<div class="card">
<p class="num">1</p>
<h3>「我的眼睛先看到……」</h3>
<p class="dim">先描述，不評價。</p>
</div>
<div class="card">
<p class="num">2</p>
<h3>「我喜歡……，因為……」</h3>
<p class="dim">不要只說「好看」，說出具體做得好的地方。</p>
</div>
<div class="card">
<p class="num">3</p>
<h3>「如果……會怎樣？」</h3>
<p class="dim">提出一個可以試試看的改變，例如「如果蹲低一點呢？」</p>
</div>
</div>

<p v-click class="lead text-center !mt-8">最後請拍照的人說：「我想表達的是……」</p>

---
layout: section
---

<div class="eyebrow">Chapter 06</div>

# 參數：光圈、快門、ISO

<p class="muted">Auto 只想把每張照片拍成「亮度正常」，它不知道你想要什麼。</p>

---

<div class="eyebrow">Exposure</div>

## 曝光：進到相機的光有多少

<div class="trio mt-6">
<div class="card">
<ph-aperture class="card-icon" />
<h3>光圈</h3>
<p class="dim">開口多大<br />決定<strong>流量</strong></p>
</div>
<div class="card">
<ph-timer class="card-icon" />
<h3>快門</h3>
<p class="dim">開口打開多久<br />決定<strong>時間</strong></p>
</div>
<div class="card">
<ph-sliders class="card-icon" />
<h3>ISO</h3>
<p class="dim">訊號<strong>放大</strong>多少倍<br />不會讓更多光進來</p>
</div>
</div>

<p v-click class="lead text-center !mt-8">ISO 像錄音的音量旋鈕：轉大，人聲變大，底噪也變大。真正的解法是靠近麥克風，讓更多光進來。</p>

---

<div class="eyebrow">Stop</div>

## 1 級 = 光量變 2 倍或一半

<p class="lead">三個參數用同一個單位，可以互相交換。下面三組亮度都一樣：</p>

<div class="grid grid-cols-3 gap-4 mt-6 text-center">
<div class="card"><p class="mono text-lg font-bold whitespace-nowrap">f/4 · 1/125 · ISO 400</p></div>
<div class="card" v-click><p class="mono text-lg font-bold whitespace-nowrap">f/5.6 · 1/60 · ISO 400</p><p class="dim">光圈縮 1 級，快門慢 1 級</p></div>
<div class="card" v-click><p class="mono text-lg font-bold whitespace-nowrap">f/5.6 · 1/125 · ISO 800</p><p class="dim">光圈縮 1 級，ISO 高 1 級</p></div>
</div>

<p class="muted text-center !mt-8">轉盤一格是 1/3 級，轉三格 = 1 級。剪影刻意拍暗、高調刻意拍亮：<strong>沒有唯一正確的曝光</strong>。</p>

---

<div class="eyebrow">Aperture</div>

## 光圈：數字越小，洞越大

<div class="apertures mt-8">
<div><div class="hole" style="width: 120px; height: 120px"></div><p class="mono">f/4</p></div>
<div><div class="hole" style="width: 85px; height: 85px"></div><p class="mono">f/5.6</p></div>
<div><div class="hole" style="width: 60px; height: 60px"></div><p class="mono">f/8</p></div>
<div><div class="hole" style="width: 44px; height: 44px"></div><p class="mono">f/11</p></div>
<div><div class="hole" style="width: 30px; height: 30px"></div><p class="mono">f/16</p></div>
<div><div class="hole" style="width: 22px; height: 22px"></div><p class="mono">f/22</p></div>
</div>

<p class="lead text-center !mt-8">f/4 是焦距的四分之一，f/8 是八分之一。就像 1/4 個披薩比 1/8 個大。</p>

<p v-click class="muted text-center">f/8 附近畫質最好；縮到 f/16、f/22 會因為繞射變軟。</p>

---

<div class="eyebrow">Depth of Field</div>

## 景深：前後清楚的範圍

<div class="grid grid-cols-2 gap-10 mt-6">
<div>
<p class="lead"><strong class="good">大光圈 f/4</strong>：景深淺，背景糊</p>
<p class="lead"><strong>小光圈 f/11</strong>：前後都清楚</p>
<p class="lead !mt-6">影響景深的還有：</p>
<ol class="steps lead">
<li><span class="n">1</span><strong>距離</strong>：越近越淺（最常被忽略）</li>
<li><span class="n">2</span><strong>焦段</strong>：105mm 背景看起來更糊</li>
<li><span class="n">3</span><strong>狐狸離背景多遠</strong></li>
</ol>
</div>
<div class="card">
<h3>105mm、f/4、1 公尺</h3>
<p class="num">≈ 2 cm</p>
<p class="dim">對焦在鼻子，眼睛可能就糊了。<strong>淺景深一定要對焦在眼睛。</strong></p>
</div>
</div>

---

<div class="eyebrow">Bokeh</div>

## 背景怎麼都糊不起來？

<ol class="steps lead mt-6">
<li><span class="n">1</span>光圈開到最大</li>
<li><span class="n">2</span>拉到 105mm</li>
<li><span class="n">3</span>人靠近狐狸</li>
<li><span class="n">4</span><strong>把狐狸移到離背景遠一點</strong></li>
</ol>

<p v-click class="lead !mt-8">純色背景布本來就看不太出糊不糊。在狐狸後面一兩公尺放一串燈或一個道具，效果就很明顯。</p>

---

<div class="eyebrow">Shutter</div>

## 快門：凝結還是拖影

<div class="table-clean mt-6">

| 1/1000           | 1/250        | 1/125                 | 1/60                  | 1/15       | 1 秒以上             |
| ---------------- | ------------ | --------------------- | --------------------- | ---------- | -------------------- |
| 凝結拋起來的狐狸 | 一般走動的人 | 手持 105mm 的安全快門 | 棚內 LED 燈最穩的速度 | 揮動會拖影 | 要上腳架，可以玩光繪 |

</div>

<p class="lead !mt-8"><strong>安全快門</strong>：手持至少「1/焦距」秒。105mm 就至少 1/125 秒。</p>

<p v-click class="muted">防手震可以讓你慢一點，但它只修正你的手晃，修正不了狐狸在動。</p>

---

<div class="eyebrow">ISO</div>

## ISO：能低就低

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<div>

- **ISO 100** 畫質最好
- 3200 以內很乾淨，6400 一般用途沒問題
- 寧可有一點雜訊，也不要照片糊掉

<p class="lead !mt-6">順序：先依畫面決定<strong>快門</strong>和<strong>光圈</strong>，剩下的亮度缺口再用 ISO 補。</p>

</div>
<div class="card">
<h3 class="bad">不要故意拍暗再回家拉亮</h3>
<p class="dim">6D Mark II 在低 ISO 拉亮暗部時雜訊特別明顯。<strong>光線不夠，當場把 ISO 開高比較乾淨。</strong></p>
</div>
</div>

---

<div class="eyebrow">Modes</div>

## 拍攝模式：你決定什麼？

<div class="table-clean table-tight mt-2">

| 模式                | 你決定                       | 相機決定   | 什麼時候用                           |
| ------------------- | ---------------------------- | ---------- | ------------------------------------ |
| **A+** 場景智能自動 | 幾乎不用                     | 全部       | 交給別人隨手拍                       |
| **CA** 創意自動     | 「背景模糊」滑桿（就是光圈） | 其他       | 還沒準備好碰參數                     |
| **P** 程式自動      | ISO、白平衡、對焦            | 光圈＋快門 | 快速抓拍                             |
| **Av** 光圈先決     | 光圈                         | 快門       | 控制背景多糊。**新手最推薦**         |
| **Tv** 快門先決     | 快門                         | 光圈       | 凝結或拖出動態                       |
| **M** 手動          | 光圈＋快門＋ISO              | 只顯示建議 | **棚拍**、閃燈、光繪、每張曝光都一樣 |
| **B** 快門          | 快門開多久                   | —          | 超過 30 秒的長曝光                   |

</div>

---

<div class="eyebrow">Dials</div>

## 轉盤在每個模式管什麼

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<div class="table-clean">

| 模式 | 主轉盤（食指） | 速控轉盤（拇指） |
| ---- | -------------- | ---------------- |
| P    | 換光圈快門組合 | 曝光補償         |
| Tv   | 快門           | 曝光補償         |
| Av   | 光圈           | 曝光補償         |
| M    | 快門           | 光圈             |

</div>
<div>
<p class="lead">M 模式看觀景窗底部的<strong>曝光指示標尺</strong>：中間是相機覺得剛好，往右偏亮、往左偏暗。</p>
<p class="lead !mt-6">不想記轉盤？按 <kbd>Q</kbd>，直接在螢幕上點。</p>
</div>
</div>

---
layout: statement
class: say
---

<div class="eyebrow">Metering</div>

為什麼白背景會變灰？

<p v-click class="sub !mt-6">測光表不知道東西本來是白還是黑，它只會把看到的東西都拍成<strong>中間灰</strong>。</p>

---

<div class="eyebrow">Metering</div>

## 白加黑減

<div class="grid grid-cols-2 gap-6 mt-6">
<div class="card">
<div class="swatch is-white"></div>
<h3>白背景佔滿畫面</h3>
<p class="dim">相機以為太亮 → 壓暗 → 白變灰、狐狸變暗</p>
<p class="num !mt-3">+1 ~ +2</p>
</div>
<div class="card">
<div class="swatch is-black"></div>
<h3>黑背景佔滿畫面</h3>
<p class="dim">相機以為太暗 → 拉亮 → 黑變灰、狐狸過曝</p>
<p class="num !mt-3">−1 ~ −2</p>
</div>
</div>

<p v-click class="lead text-center !mt-8">更好的做法：<strong>M 模式</strong>。照在狐狸身上的光沒變，曝光就不該變。</p>

---

<div class="eyebrow">Histogram</div>

## 直方圖：不要相信螢幕

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
<div>
<p class="lead">暗暗的攝影棚裡，螢幕看起來特別亮。播放時按 <kbd>INFO</kbd> 看直方圖：</p>
<ul class="lead">
<li>撞到最右邊：亮部過曝，救不回來</li>
<li>撞到最左邊：暗部全黑</li>
</ul>
<p class="muted !mt-4">沒有標準的直方圖。白背景本來就該靠右，黑背景本來就該靠左。</p>
</div>
<div class="card">
<h3>高光警告</h3>
<p class="dim">過曝的地方會黑白閃爍。</p>
<p class="lead !mt-3"><span class="good">背景閃：沒關係</span><br /><span class="bad">狐狸閃：不行</span></p>
</div>
</div>

---

<div class="eyebrow">White Balance</div>

## 白平衡：白色要是白色

<div class="kelvin mt-10"></div>
<div class="kelvin-scale">
<span>燭光 1500K</span>
<span>燈泡 3000K</span>
<span>螢光燈 4500K</span>
<span>閃燈、LED 5500K</span>
<span>陰天 7000K</span>
</div>

<div class="grid grid-cols-3 gap-4 mt-8">
<div class="card"><h3>AWB</h3><p class="dim">大部分時候夠用</p></div>
<div class="card"><h3>K 值</h3><p class="dim">燈上標幾 K 就設幾 K，最準</p></div>
<div class="card"><h3>自訂</h3><p class="dim">對白紙或灰卡拍一張當基準</p></div>
</div>

<p v-click class="muted text-center !mt-6">設 7000K 是告訴相機「現場偏藍」，相機加黃抵消，所以照片反而變暖。</p>

---

<div class="eyebrow">Focus</div>

## 對焦

<div class="grid grid-cols-2 gap-10 mt-6">
<div>
<h3>對焦模式（機頂 AF 按鈕）</h3>

- **ONE SHOT**：對到就鎖住、嗶一聲。擺好不動的狐狸
- **AI SERVO**：半按期間一直追焦。拋起來的狐狸
- **AI FOCUS**：相機自己判斷

</div>
<div>
<h3>對焦點</h3>
<p class="dim">Auto 很喜歡對最近的東西（鼻子、前景道具）。</p>
<p class="dim">按機背右上的<strong>對焦點選擇按鈕</strong>改成<strong>單點</strong>，用多功能控制器移到狐狸的眼睛。</p>
<p class="muted !mt-3">45 點都集中在中間。主體在邊緣就先對焦再移動構圖，或用 Live View 點螢幕。</p>
</div>
</div>

---

<div class="eyebrow">File</div>

## RAW 還是 JPEG？

<div class="table-clean mt-6">

|          | RAW（.CR2）              | JPEG                     |
| -------- | ------------------------ | ------------------------ |
| 白平衡   | 事後隨便改，不會損失畫質 | 已經套用了，改了會掉品質 |
| 亮部暗部 | 救回來的空間大           | 小很多                   |
| 檔案     | 大                       | 小，可以直接分享         |
| 傳到手機 | 會被轉成 JPEG            | 直接傳                   |

</div>

<p class="lead text-center !mt-8">今天設定成 <strong>RAW + JPEG</strong>：JPEG 馬上分享，RAW 留給 Lightroom。</p>

---

<div class="eyebrow">Lighting</div>

## 攝影棚的燈

<div class="grid grid-cols-2 gap-6 mt-6">
<div class="card">
<h3>LED 持續燈</h3>
<p class="dim">所見即所得，最好學。但台灣的燈每秒閃 120 次，快門太快會出現橫紋、連拍亮度不一。</p>
<p class="num !mt-3">1/60 秒</p>
<p class="muted">最穩。防閃爍拍攝只在用觀景窗時有效。</p>
</div>
<div class="card">
<h3>閃燈（棚燈）</h3>
<ul class="dim">
<li><strong>M 模式</strong>，例如 1/125、f/8、ISO 100</li>
<li>快門<strong>不能快過 1/180</strong>，否則出現黑帶</li>
<li>快門管環境光，光圈管閃燈</li>
<li>測光表量不到閃燈，靠試拍＋直方圖</li>
</ul>
</div>
</div>

---

<div class="eyebrow">Play</div>

## 玩法（一）

<div class="table-clean table-tight mt-2">

| 玩法               | 模式與設定                           | 怎麼拍                                                 |
| ------------------ | ------------------------------------ | ------------------------------------------------------ |
| **淺景深**         | Av、f/4（STM f/5.6）、105mm          | 狐狸離背景 2 公尺以上，單點對焦眼睛。換 f/8、f/16 比較 |
| **深景深**         | Av、f/11、24–35mm                    | 兩三個道具前後拉開，全部清楚                           |
| **凝結拋起的狐狸** | Tv、1/1000、ISO 自動、AI SERVO、連拍 | 先對焦在狐狸會飛到的高度。LED 有橫紋就要靠閃燈         |
| **拖影**           | Tv、1/15–1/4、上腳架                 | 狐狸一邊移動一邊拍                                     |
| **縮放爆炸**       | M 或 Tv、1/4–1/2、f/11、上腳架       | 按下快門後，平順地把變焦環從 105 轉到 24               |
| **晃動相機**       | Tv、1/4–1 秒                         | 按快門的同時平順地移動相機                             |

</div>

---

<div class="eyebrow">Play</div>

## 玩法（二）

<div class="table-clean table-tight mt-2">

| 玩法         | 模式與設定                               | 怎麼拍                                                        |
| ------------ | ---------------------------------------- | ------------------------------------------------------------- |
| **光繪**     | M 10–30 秒、f/8、ISO 100、腳架、2 秒自拍 | 先開燈對焦再切 MF。關燈後用手機手電筒畫圖，最後刷過狐狸照亮牠 |
| **剪影**     | M、讓白背景剛好變白                      | 只打亮白背景，狐狸前面完全不打光                              |
| **多重曝光** | 拍攝選單 → 多重曝光 → 平均、2–3 張       | 用 Live View 拍，黑背景上做出分身狐狸                         |
| **高調**     | M（或 Av +1.7）、白背景                  | 背景比狐狸亮一點。背景閃可以，狐狸不行                        |
| **低調**     | M、黑背景、側後方一盞輪廓光              | 狐狸離黑背景 2–3 公尺，光只照到狐狸                           |

</div>

<p class="muted !mt-4 text-center">光繪關燈後走路小心燈架和電線，不要拿手電筒照別人眼睛。</p>

---
layout: section
---

<div class="eyebrow">Chapter 07</div>

# 白、黑、綠背景怎麼拍

---

<div class="eyebrow">Backdrops</div>

## 三種背景，三種拍法

<div class="grid grid-cols-3 gap-4 mt-4">
<div class="card">
<div class="swatch is-white"></div>
<h3>白：背景另外打燈</h3>
<ul class="dim">
<li>狐狸離背景 1.5 公尺以上</li>
<li>背景比狐狸亮約 1 級</li>
<li>高光警告<strong>剛好</strong>開始閃就好，太亮會反光、吃掉毛邊</li>
</ul>
</div>
<div class="card">
<div class="swatch is-black"></div>
<h3>黑：別讓光碰到背景</h3>
<ul class="dim">
<li>狐狸離背景 2–3 公尺</li>
<li>燈靠近狐狸</li>
<li>側後方加<strong>輪廓光</strong>勾出毛邊</li>
<li>關燈試拍應該全黑</li>
</ul>
</div>
<div class="card">
<div class="swatch is-green"></div>
<h3>綠：為了後製去背</h3>
<ul class="dim">
<li>綠幕打得<strong>均勻</strong></li>
<li>狐狸離綠幕 2–3 公尺</li>
<li>白平衡固定，不要 AWB</li>
<li>白毛、塑膠眼珠最容易泛綠</li>
</ul>
</div>
</div>

<p v-click class="muted text-center !mt-4">Lightroom 不能去背，要換背景得用 Photoshop。</p>

---
layout: section
---

<div class="eyebrow">Chapter 08</div>

# Lightroom 調色與輸出

---

<div class="eyebrow">Lightroom</div>

## 非破壞性編輯

<p class="lead">每一個滑桿都只是一筆紀錄，原始檔案永遠不會被改動。</p>

<div class="table-clean mt-4">

|          | Lightroom Classic    | Lightroom（雲端版）      |
| -------- | -------------------- | ------------------------ |
| 平台     | 只有電腦             | 電腦、手機、網頁         |
| 照片放哪 | 自己的硬碟           | Adobe 雲端               |
| 適合     | 大量照片、功能最完整 | 多裝置同步、介面比較簡單 |

</div>

<p class="muted !mt-4">手機版免費，遮色片、RAW 編輯要 Premium。電腦版每月 NT$420，7 天免費試用（2026 年 10 月價格）。</p>

---

<div class="eyebrow">Import</div>

## 拿到照片、挑片

<div class="grid grid-cols-2 gap-10 mt-6">
<div>
<h3>拿到照片</h3>
<p class="dim"><strong>SD 卡 → 讀卡機</strong>：RAW＋JPEG 原檔</p>
<p class="dim"><strong>Wi-Fi → Camera Connect</strong>：只有 JPEG，一台相機一次連一支手機</p>
<h3 class="!mt-6">讀入</h3>
<p class="dim">圖庫 → 讀入 → 選記憶卡 → <strong>拷貝</strong> → 選資料夾</p>
</div>
<div>
<h3>先挑再修</h3>
<p class="lead"><kbd>G</kbd> 格線　<kbd>P</kbd> 喜歡　<kbd>X</kbd> 不要</p>
<p class="lead"><kbd>1</kbd>–<kbd>5</kbd> 星等　<kbd>D</kbd> 編輯相片</p>
<div class="card !mt-6">
<h3 class="bad">沒有「儲存」，只有「匯出」</h3>
<p class="dim">學校電腦可能被還原，下課前一定要匯出。</p>
</div>
</div>
</div>

---

<div class="eyebrow">Workflow</div>

## 修圖順序

<div class="grid grid-cols-2 gap-x-10 mt-6">
<ol class="steps lead">
<li><span class="n">1</span>描述檔、鏡頭校正</li>
<li><span class="n">2</span>裁切、拉直</li>
<li><span class="n">3</span>白平衡</li>
<li><span class="n">4</span>曝光、對比、亮部、陰影、白黑</li>
<li><span class="n">5</span>紋理、清晰度、飽和度</li>
</ol>
<ol class="steps lead">
<li><span class="n">6</span>顏色混合器（特定顏色）</li>
<li><span class="n">7</span>顏色分級（氣氛）</li>
<li><span class="n">8</span>遮色片（局部）</li>
<li><span class="n">9</span>去除灰塵</li>
<li><span class="n">10</span>匯出</li>
</ol>
</div>

<p class="muted text-center !mt-6">不是硬性規定，只是為了少繞路。</p>

---

<div class="eyebrow">Profile & White Balance</div>

## 描述檔、白平衡

<div class="grid grid-cols-2 gap-6 mt-6">
<div class="card">
<h3>描述檔</h3>
<p class="dim">RAW 讀進來顏色「跳一下」是因為預設 Adobe Color。想跟相機螢幕一樣：<strong>相機比對 → 相機標準</strong>。</p>
<p class="dim !mt-3">鏡頭校正勾<strong>移除色差</strong>、<strong>啟用鏡頭校正</strong>。</p>
</div>
<div class="card">
<h3>白平衡：按 <kbd>W</kbd> 點灰色的地方</h3>
<ul class="dim">
<li>有灰卡就點灰卡</li>
<li>白背景：點<strong>沒過曝</strong>的淺灰角落</li>
<li>黑背景：改點狐狸白色的毛</li>
<li>綠背景：<strong>不要點綠色</strong>，會變紫</li>
</ul>
</div>
</div>

---

<div class="eyebrow">Light</div>

## 亮度

<div class="table-clean table-tight mt-2">

| 滑桿   | 做什麼                 | 棚拍提示                 |
| ------ | ---------------------- | ------------------------ |
| 曝光度 | 整體亮度，+1 約多 1 級 | 先讓狐狸的亮度對         |
| 對比   | 亮的更亮、暗的更暗     | 白背景加太多容易斷層     |
| 亮部   | 往左拉回過亮的細節     | 狐狸白色的毛             |
| 陰影   | 往右提亮暗部           | 黑背景不要拉太多，會變灰 |
| 白色   | 畫面最亮的點           | 白背景往右拉到剛好純白   |
| 黑色   | 畫面最暗的點           | 黑背景往左拉更黑         |

</div>

<p class="lead text-center !mt-6"><kbd>J</kbd> 剪裁警示：紅色過曝、藍色全黑。拖白色、黑色時按住 <kbd>Alt</kbd>。</p>

---

<div class="eyebrow">Presence & Color</div>

## 外觀與顏色

<div class="grid grid-cols-3 gap-4 mt-6">
<div class="card">
<h3>外觀</h3>
<ul class="dim">
<li><strong>紋理 +10~+30</strong>：毛絨玩具的好朋友</li>
<li>清晰度：少量，太多有光暈</li>
<li>去朦朧：黑背景可加一點</li>
<li>先動<strong>鮮豔度</strong>，再動飽和度</li>
</ul>
</div>
<div class="card">
<h3>顏色混合器</h3>
<p class="dim">用<strong>目標調整工具</strong>在狐狸毛上往上拖。例如橘色飽和度 +12、明度 +8。</p>
<p class="muted !mt-3">有人入鏡時膚色也是橘的，改用「點顏色」或遮色片。</p>
</div>
<div class="card">
<h3>顏色分級</h3>
<p class="dim"><strong>暖亮冷暗</strong>：亮部加橘黃、暗部加藍。</p>
<p class="mono dim !mt-3">亮部 45° / 12<br />陰影 210° / 8</p>
<p class="muted !mt-3">按 <kbd>\</kbd> 比較前後。</p>
</div>
</div>

---

<div class="eyebrow">Masking</div>

## 遮色片：只調某個地方

<p class="lead"><kbd>Shift</kbd>+<kbd>W</kbd>，讓 AI 選出主體或背景。</p>

<div class="grid grid-cols-3 gap-4 mt-4">
<div class="card">
<div class="swatch is-white"></div>
<h3>白背景變純白</h3>
<p class="dim">選取背景 → 曝光 +0.8、<strong>飽和度 −60</strong>、亮部 +40、白色 +30。按 J 確認毛邊沒被吃掉。</p>
</div>
<div class="card">
<div class="swatch is-black"></div>
<h3>黑背景更黑</h3>
<p class="dim">選取背景 → 曝光 −1.0、黑色 −30。</p>
</div>
<div class="card">
<ph-paw-print class="card-icon" />
<h3>狐狸提亮</h3>
<p class="dim">選取主體 → 曝光 +0.2、紋理 +10。</p>
</div>
</div>

---

<div class="eyebrow">Finish</div>

## 去灰塵、裁切、套一整組

<div class="grid grid-cols-3 gap-4 mt-6">
<div class="card">
<h3>去灰塵 <kbd>Q</kbd></h3>
<p class="dim">勾<strong>顯現污點</strong>，背景布上的髒點會很明顯，點一下去掉。</p>
</div>
<div class="card">
<h3>裁切 <kbd>R</kbd></h3>
<p class="dim">IG 直式用 4:5 或 3:4，拖曳旋轉可以拉直。隨時可以改。</p>
</div>
<div class="card">
<h3>同步化</h3>
<p class="dim">選修好的那張，Shift 選其他張 → <strong>同步化</strong>，取消勾裁切和污點移除。AI 遮色片會每張重新偵測。</p>
</div>
</div>

<p v-click class="muted text-center !mt-6">常用的存成預設集，例如「白背景狐狸」。不要勾白平衡和曝光。</p>

---

<div class="eyebrow">Export</div>

## 匯出 <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>E</kbd>

<div class="table-clean table-tight mt-2">

| 用途         | 格式         | 色域     | 尺寸                        | 品質   |
| ------------ | ------------ | -------- | --------------------------- | ------ |
| **IG 貼文**  | JPEG         | **sRGB** | 寬 1080（4:5 是 1080×1350） | 80–100 |
| 網站、作品集 | JPEG         | sRGB     | 長邊 2048                   | 80     |
| 列印         | JPEG 或 TIFF | 先問店家 | 不縮放                      | 100    |

</div>

<div class="card !mt-6">
<h3>顏色跟 Lightroom 裡不一樣？</h3>
<ul class="dim">
<li>色域一定選 <strong>sRGB</strong>，AdobeRGB 在手機上會灰灰的</li>
<li>不要用 Messenger、LINE 傳，會被壓縮</li>
<li>IG 打開「以最高品質上傳」</li>
</ul>
</div>

---

<div class="eyebrow">Mobile</div>

## 只有手機也可以

<div class="grid grid-cols-2 gap-x-10 mt-6">
<ol class="steps lead">
<li><span class="n">1</span>Camera Connect 存到手機</li>
<li><span class="n">2</span>Lightroom App 按「+」匯入</li>
<li><span class="n">3</span><strong>光線</strong>：兩指拖滑桿看過曝</li>
<li><span class="n">4</span><strong>顏色</strong>：滴管點白色，橘色加一點</li>
</ol>
<ol class="steps lead">
<li><span class="n">5</span><strong>效果</strong>：紋理 +20</li>
<li><span class="n">6</span><strong>裁切</strong>：4:5</li>
<li><span class="n">7</span><strong>長按</strong>看修改前</li>
<li><span class="n">8</span>匯出：JPG、長邊 1440、品質 90</li>
</ol>
</div>

<p class="muted text-center !mt-6">免費版就夠修 JPEG。</p>

---
layout: statement
class: say
---

<div class="eyebrow">Recap</div>

如果只記得三件事

<p v-click><strong>主角是誰？</strong> <span class="muted">減法、檢查四個邊</span></p>

<p v-click><strong>光從哪裡來？</strong> <span class="muted">白加黑減、M 模式、看直方圖</span></p>

<p v-click><strong>換個位置。</strong> <span class="muted">構圖靠的是你的腳</span></p>

---
layout: statement
class: say
---

相機只是工具，

<p v-click>真正決定照片好不好看的，是你看世界的方式。</p>

<p v-click class="sub !mt-8">完整教材：<a href="https://emtech.cc/course/ict/photography/">emtech.cc/course/ict/photography</a></p>

---
layout: statement
class: say
---

# Q & A

---
src: ../global/cc.md
---
