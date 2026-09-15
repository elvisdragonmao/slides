<script setup lang="ts">
import { computed } from "vue";

// Commit = 一個個封好的包裹；D 壞掉時可以回頭看 C
const props = withDefaults(defineProps<{ step?: number }>(), { step: 0 });

const commits = [
	{ id: "A", msg: "建立網站" },
	{ id: "B", msg: "加入登入頁面" },
	{ id: "C", msg: "修正登入 Bug" },
	{ id: "D", msg: "加入深色模式" }
];

const current = computed(() => Math.max(0, Math.min(5, props.step)));
</script>

<template>
	<div class="hs" :class="{ 'is-broken': current >= 4, 'is-looking': current >= 5 }">
		<div class="hs-track">
			<div class="hs-track-fill" :style="{ width: `${Math.min(3, current) * 200}px` }" />
		</div>

		<svg class="hs-arrow" width="860" height="96" viewBox="0 0 860 96">
			<path class="hs-arrow-line" d="M718 80C700 14 560 14 542 76" pathLength="1" />
			<path class="hs-arrow-head" d="M533 66l9 12 9-12" />
		</svg>
		<div class="hs-arrow-text">回去看看 C</div>

		<div v-for="(c, i) in commits" :key="c.id" class="hs-commit" :class="[`is-${c.id.toLowerCase()}`, { 'is-hidden': i > current }]" :style="{ left: `${130 + i * 200}px` }">
			<div class="hs-parcel">
				<Parcel :label="c.id" />
			</div>
			<div class="hs-dot" />
			<div class="hs-msg">
				<span class="hs-id">{{ c.id }}</span>
				{{ c.msg }}
			</div>
		</div>

		<div class="hs-note hs-note-d">
			<ph-warning-fill />
			D 爆炸了
		</div>
		<div class="hs-note hs-note-c">C 的時候到底長什麼樣子？</div>
	</div>
</template>

<style scoped>
.hs {
	position: relative;
	width: 860px;
	height: 330px;
	margin: 0 auto;
}

.hs-track {
	position: absolute;
	left: 130px;
	top: 222px;
	width: 600px;
	height: 2px;
	background: var(--hairline);
}

.hs-track-fill {
	height: 100%;
	background: var(--purple);
	transition: width 0.7s var(--ease);
}

.hs-commit {
	position: absolute;
	top: 0;
	width: 180px;
	margin-left: -90px;
	transition: opacity 0.4s var(--ease);
}

.hs-parcel {
	width: 112px;
	margin: 96px auto 0;
	transition:
		opacity 0.45s var(--ease),
		transform 0.7s var(--spring);
}

.hs-dot {
	position: absolute;
	left: 50%;
	top: 215px;
	width: 16px;
	height: 16px;
	margin-left: -8px;
	border-radius: 50%;
	box-sizing: border-box;
	background: var(--background);
	border: 2px solid var(--purple);
	transition:
		opacity 0.4s,
		background 0.3s,
		border-color 0.3s,
		transform 0.4s var(--spring);
}

.hs-msg {
	position: absolute;
	left: 0;
	right: 0;
	top: 244px;
	text-align: center;
	font-size: 16px;
	white-space: nowrap;
	transition: opacity 0.4s;
}

.hs-id {
	margin-right: 6px;
	font-family: var(--mono);
	font-weight: 700;
	color: var(--purple);
}

.hs-commit.is-hidden .hs-parcel {
	opacity: 0;
	transform: translateY(-40px);
}

.hs-commit.is-hidden .hs-dot,
.hs-commit.is-hidden .hs-msg {
	opacity: 0;
}

/* D 爆炸 */
.is-broken .is-d .hs-parcel {
	transform: translateY(10px) rotate(9deg);
	animation: hs-shake 0.5s var(--ease);
}

.is-broken .is-d .hs-dot {
	background: var(--red);
	border-color: var(--red);
}

.is-broken .is-d .hs-id {
	color: var(--red);
}

@keyframes hs-shake {
	0%,
	100% {
		rotate: 0deg;
	}
	25% {
		rotate: -7deg;
	}
	50% {
		rotate: 6deg;
	}
	75% {
		rotate: -3deg;
	}
}

/* 回頭看 C */
.is-looking .hs-commit:not(.is-c) {
	opacity: 0.35;
}

.is-looking .is-c .hs-parcel {
	transform: translateY(-10px) scale(1.06);
}

.is-looking .is-c .hs-dot {
	background: var(--purple);
	transform: scale(1.2);
}

.hs-arrow {
	position: absolute;
	left: 0;
	top: 0;
	overflow: visible;
}

.hs-arrow-line,
.hs-arrow-head {
	fill: none;
	stroke: var(--purple);
	stroke-width: 2.5;
	stroke-linecap: round;
	stroke-linejoin: round;
}

/* 收起時透明度歸零，避免圓頭線帽留下小點 */
.hs-arrow-line {
	stroke-dasharray: 1 1;
	stroke-dashoffset: 1;
	opacity: 0;
	transition:
		stroke-dashoffset 0.4s var(--ease),
		opacity 0s linear 0.4s;
}

.is-looking .hs-arrow-line {
	opacity: 1;
	transition:
		stroke-dashoffset 0.8s var(--ease),
		opacity 0s;
}

.hs-arrow-head {
	opacity: 0;
	transition: opacity 0.2s;
}

.is-looking .hs-arrow-line {
	stroke-dashoffset: 0;
}

.is-looking .hs-arrow-head {
	opacity: 1;
	transition-delay: 0.6s;
}

.hs-arrow-text {
	position: absolute;
	left: 630px;
	top: 4px;
	transform: translateX(-50%);
	font-size: 14px;
	color: var(--purple);
	opacity: 0;
	transition: opacity 0.4s 0.3s;
}

.is-looking .hs-arrow-text {
	opacity: 1;
}

.hs-note {
	position: absolute;
	top: 280px;
	display: flex;
	align-items: center;
	gap: 6px;
	transform: translateX(-50%);
	padding: 4px 12px;
	border-radius: 999px;
	font-size: 13px;
	white-space: nowrap;
	opacity: 0;
	transition: opacity 0.4s var(--ease);
}

.hs-note-d {
	left: 730px;
	color: var(--red);
	border: 1px solid color-mix(in srgb, var(--red) 45%, transparent);
}

.hs-note-c {
	left: 530px;
	color: var(--purple);
	border: 1px solid color-mix(in srgb, var(--purple) 45%, transparent);
}

.is-broken .hs-note-d,
.is-looking .hs-note-c {
	opacity: 1;
}
</style>
