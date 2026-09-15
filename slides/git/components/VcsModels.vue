<script setup lang="ts">
import { computed } from "vue";

// 本地端 → 集中式 → 分散式
const props = withDefaults(defineProps<{ step?: number }>(), { step: 0 });
const current = computed(() => Math.max(0, Math.min(2, props.step)));

const models = [
	{ no: "01", name: "本地端", desc: "歷史都放在你自己的電腦。簡單，但電腦死掉，它可能就一起走了。" },
	{ no: "02", name: "集中式", desc: "所有歷史都放在一台中央 Server，大家都得跟它溝通。例如 SVN。" },
	{ no: "03", name: "分散式", desc: "每個人都有完整歷史。沒網路也能 Commit，有網路再交換。Git 就是這種。" }
];
const model = computed(() => models[current.value]);

const people = [
	{ name: "海鷗", x: 170 },
	{ name: "你", x: 430 },
	{ name: "Ben", x: 690 }
];
</script>

<template>
	<div class="vm">
		<svg class="vm-lines" width="860" height="250" viewBox="0 0 860 250">
			<path v-for="p in people" :key="p.name" class="vm-line" :class="{ 'is-hidden': current === 0, 'is-dashed': current === 2 }" :d="`M430 82C430 116 ${p.x} 108 ${p.x} 144`" pathLength="1" />
			<path class="vm-line is-dashed" :class="{ 'is-hidden': current < 2 }" d="M254 194H346" pathLength="1" />
			<path class="vm-line is-dashed" :class="{ 'is-hidden': current < 2 }" d="M514 194H606" pathLength="1" />
		</svg>

		<div class="vm-node vm-server" :class="{ 'is-hidden': current === 0 }">
			<ph-hard-drives class="vm-icon" />
			<div class="vm-name">{{ current === 2 ? "GitHub" : "中央 Server" }}</div>
			<div class="vm-stack">
				<Parcel v-for="i in 3" :key="i" class="vm-parcel" />
			</div>
		</div>

		<div v-for="p in people" :key="p.name" class="vm-node vm-pc" :class="{ 'is-hidden': current === 0 && p.name !== '你' }" :style="{ left: `${(current === 0 ? 430 : p.x) - 82}px` }">
			<ph-laptop class="vm-icon" />
			<div class="vm-name">{{ p.name }}</div>
			<div class="vm-slot">
				<div class="vm-stack" :class="{ 'is-hidden': current === 1 }">
					<Parcel v-for="i in 3" :key="i" class="vm-parcel" />
				</div>
				<div class="vm-file" :class="{ 'is-hidden': current !== 1 }">
					<ph-file-text />
					只有最新檔案
				</div>
			</div>
		</div>

		<div class="vm-caption">
			<Transition name="vm-fade" mode="out-in">
				<div :key="current">
					<div class="vm-title">
						<span class="vm-no">{{ model.no }}</span>
						{{ model.name }}版本控制
					</div>
					<div class="vm-desc">{{ model.desc }}</div>
				</div>
			</Transition>
		</div>
	</div>
</template>

<style scoped>
.vm {
	position: relative;
	width: 860px;
	height: 340px;
	margin: 0 auto;
}

.vm-lines {
	position: absolute;
	left: 0;
	top: 0;
	overflow: visible;
}

.vm-line {
	fill: none;
	stroke: var(--hairline-strong);
	stroke-width: 2;
	stroke-dasharray: 1 1;
	stroke-dashoffset: 0;
	transition:
		stroke-dashoffset 0.7s var(--ease) 0.35s,
		opacity 0.4s;
}

.vm-line.is-dashed {
	stroke: var(--cyan);
	stroke-dasharray: 0.03 0.025;
	opacity: 0.7;
}

.vm-line.is-hidden {
	stroke-dashoffset: 1;
	transition-delay: 0s;
}

.vm-line.is-dashed.is-hidden {
	stroke-dashoffset: 0;
	opacity: 0;
}

.vm-node {
	position: absolute;
	box-sizing: border-box;
	background: var(--surface);
	border: 1px solid var(--hairline);
	border-radius: 16px;
	transition:
		opacity 0.5s var(--ease),
		left 0.8s var(--ease-io),
		transform 0.5s var(--ease);
}

.vm-node.is-hidden {
	opacity: 0;
	transform: scale(0.94);
}

.vm-server {
	left: 300px;
	top: 14px;
	width: 260px;
	height: 68px;
	display: flex;
	align-items: center;
	gap: 10px;
	padding: 0 16px;
}

.vm-server .vm-name {
	flex: 1;
}

.vm-pc {
	top: 144px;
	width: 164px;
	height: 100px;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	gap: 4px;
}

.vm-icon {
	flex: none;
	font-size: 22px;
	color: var(--purple);
}

.vm-name {
	font-size: 15px;
}

.vm-slot {
	position: relative;
	width: 100%;
	height: 24px;
}

.vm-slot > * {
	position: absolute;
	inset: 0;
	display: flex;
	align-items: center;
	justify-content: center;
}

.vm-stack {
	display: flex;
	gap: 4px;
	transition: opacity 0.4s var(--ease);
}

.vm-parcel {
	flex: none;
	width: 22px !important;
}

.vm-file {
	gap: 6px;
	font-size: 12px;
	color: var(--comment);
	transition: opacity 0.4s var(--ease);
}

.vm-stack.is-hidden,
.vm-file.is-hidden {
	opacity: 0;
}

.vm-caption {
	position: absolute;
	left: 0;
	right: 0;
	top: 266px;
	text-align: center;
}

.vm-title {
	font-size: 22px;
	font-weight: 700;
}

.vm-no {
	margin-right: 10px;
	font-family: var(--mono);
	font-size: 13px;
	color: var(--comment);
	vertical-align: 3px;
}

.vm-desc {
	margin-top: 6px;
	font-size: 15px;
	color: var(--dim);
}

.vm-fade-enter-active,
.vm-fade-leave-active {
	transition:
		opacity 0.3s var(--ease),
		transform 0.3s var(--ease),
		filter 0.3s;
}

.vm-fade-enter-from {
	opacity: 0;
	transform: translateY(6px);
	filter: blur(3px);
}

.vm-fade-leave-to {
	opacity: 0;
	transform: translateY(-6px);
	filter: blur(3px);
}
</style>
