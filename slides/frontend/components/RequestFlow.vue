<script setup lang="ts">
import { computed } from "vue";

/**
 * Request & Response
 * step：0 準備 → 1 送出請求 → 2 伺服器回傳檔案 → 3 附上狀態碼
 */
const props = withDefaults(defineProps<{ step?: number; ask?: string; status?: string }>(), { step: 0, ask: "請給我 google.com", status: "200 OK" });

const s = computed(() => Math.max(0, Math.min(3, props.step)));

const files = [
	{ src: "html", label: "index.html" },
	{ src: "css", label: "style.css" },
	{ src: "js", label: "script.js" }
];

const icon = (name: string) => (name === "js" ? new URL("../img/javascript.png", import.meta.url).href : new URL(`../img/${name}.svg`, import.meta.url).href);
</script>

<template>
	<div class="rf" :class="`is-step-${s}`">
		<div class="rf-end rf-client" :class="{ 'is-focus': s !== 1 && s !== 2 }">
			<img src="../img/imac.svg" alt="" />
			<div class="rf-label">使用者（瀏覽器）</div>
		</div>
		<div class="rf-end rf-server" :class="{ 'is-focus': s === 1 || s === 2 }">
			<img src="../img/server.svg" alt="" />
			<div class="rf-label">伺服器</div>
		</div>

		<div class="rf-lane rf-lane-req" :class="{ 'is-on': s >= 1 }">
			<span class="rf-lane-name">Request</span>
			<ph-arrow-right-bold class="rf-lane-arrow" />
		</div>
		<div class="rf-lane rf-lane-res" :class="{ 'is-on': s >= 2 }">
			<ph-arrow-left-bold class="rf-lane-arrow" />
			<span class="rf-lane-name">Response</span>
		</div>

		<div class="rf-ask" :class="{ 'is-sent': s >= 1, 'is-gone': s >= 2 }">{{ ask }}</div>

		<div v-for="(f, i) in files" :key="f.src" class="rf-file" :class="{ 'is-sent': s >= 2 }" :style="{ '--i': i }">
			<img :src="icon(f.src)" alt="" />
			<span>{{ f.label }}</span>
		</div>

		<Transition name="rf-pop">
			<div v-if="s >= 3" class="rf-status" :class="{ 'is-bad': /^[45]/.test(status) }">{{ status }}</div>
		</Transition>
	</div>
</template>

<style scoped>
.rf {
	position: relative;
	width: 860px;
	height: 320px;
	margin: 0 auto;
}

.rf-end {
	position: absolute;
	top: 70px;
	width: 160px;
	text-align: center;
	opacity: 0.55;
	transition: opacity 0.4s;
}

.rf-end.is-focus {
	opacity: 1;
}

.rf-end img {
	height: 130px;
	width: auto;
	display: block;
	margin: 0 auto;
}

.rf-label {
	margin-top: 12px;
	font-size: 16px;
	color: var(--dim);
}

.rf-client {
	left: 0;
}

.rf-server {
	right: 0;
}

.rf-lane {
	position: absolute;
	left: 190px;
	right: 190px;
	display: flex;
	align-items: center;
	gap: 8px;
	height: 2px;
	background: var(--hairline-strong);
	transition: background 0.4s;
}

.rf-lane.is-on {
	background: var(--purple);
}

.rf-lane-req {
	top: 112px;
	justify-content: flex-end;
}

.rf-lane-res {
	top: 196px;
}

.rf-lane-name {
	position: absolute;
	left: 50%;
	top: 8px;
	transform: translateX(-50%);
	font-family: var(--mono);
	font-size: 12px;
	letter-spacing: 0.1em;
	color: var(--comment);
}

.rf-lane-arrow {
	color: var(--hairline-strong);
	font-size: 18px;
	margin: 0 -6px;
	transition: color 0.4s;
}

.rf-lane.is-on .rf-lane-arrow {
	color: var(--purple);
}

.rf-ask {
	position: absolute;
	top: 66px;
	left: 190px;
	padding: 6px 14px;
	border-radius: 14px 14px 14px 4px;
	background: var(--surface-strong);
	border: 1px solid var(--hairline-strong);
	white-space: nowrap;
	font-size: 15px;
	transition:
		transform 1.1s var(--ease-io),
		opacity 0.4s;
}

.rf-ask.is-sent {
	transform: translateX(270px);
}

.rf-ask.is-gone {
	opacity: 0;
}

.rf-file {
	position: absolute;
	top: 214px;
	left: 600px;
	width: 64px;
	text-align: center;
	opacity: 0;
	transition:
		transform 1.1s var(--ease-io) calc(var(--i) * 0.18s),
		opacity 0.3s linear calc(var(--i) * 0.18s);
}

.rf-file img {
	height: 48px;
	width: 48px;
	object-fit: contain;
	display: block;
	margin: 0 auto;
	border-radius: 6px;
}

.rf-file span {
	display: block;
	margin-top: 4px;
	font-family: var(--mono);
	font-size: 10.5px;
	color: var(--dim);
}

.rf-file.is-sent {
	opacity: 1;
	transform: translateX(calc(-380px + var(--i) * 74px));
}

.rf-status {
	position: absolute;
	left: 80px;
	top: 26px;
	transform: translateX(-50%);
	padding: 4px 14px;
	border-radius: 999px;
	background: var(--green);
	color: var(--ink);
	font-family: var(--mono);
	font-weight: 700;
	white-space: nowrap;
}

.rf-status.is-bad {
	background: var(--red);
}

.rf-pop-enter-active,
.rf-pop-leave-active {
	transition:
		opacity 0.35s var(--ease),
		transform 0.45s var(--spring);
}

.rf-pop-enter-from,
.rf-pop-leave-to {
	opacity: 0;
	transform: translate(-50%, 8px) scale(0.9);
}
</style>
