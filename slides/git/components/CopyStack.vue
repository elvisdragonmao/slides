<script setup lang="ts">
import { computed } from "vue";

// 土法煉鋼版本控制：每一版都整包複製
const props = withDefaults(defineProps<{ step?: number }>(), { step: 0 });

const rows = [
	{ name: "project", note: "今天有一個專案。" },
	{ name: "project-v2", note: "怕改壞？複製一份。" },
	{ name: "project-v3", note: "再改。" },
	{ name: "project-final", note: "做到差不多了。" },
	{ name: "project-final-2", note: "客戶說 Logo 再大一點。" },
	{ name: "project-final-final", note: "晚上十一點半：「不好意思，最後一個小修改。」" },
	{ name: "project-final-final-真的", note: "凌晨兩點。" }
];

const current = computed(() => Math.max(0, Math.min(rows.length - 1, props.step)));
const ratio = computed(() => (current.value + 1) / rows.length);
const level = computed(() => (current.value === rows.length - 1 ? "danger" : current.value >= 4 ? "warn" : "ok"));
</script>

<template>
	<div class="cs">
		<div class="cs-list">
			<div v-for="(row, i) in rows" :key="row.name" class="cs-row" :class="{ 'is-hidden': i > current, 'is-current': i === current }">
				<ph-folder-simple-fill class="cs-folder" />
				<span class="cs-name">{{ row.name }}</span>
			</div>
		</div>
		<div class="cs-side">
			<div class="cs-note-wrap">
				<Transition name="cs-fade" mode="out-in">
					<div :key="current" class="cs-note">{{ rows[current].note }}</div>
				</Transition>
			</div>
			<div class="cs-meter" :class="`is-${level}`">
				<div class="cs-meter-head">
					<span>磁碟空間</span>
					<span class="cs-num">{{ ((current + 1) * 1.8).toFixed(1) }} GB</span>
				</div>
				<div class="cs-track">
					<div class="cs-fill" :style="{ width: `${ratio * 100}%` }" />
				</div>
				<div class="cs-foot">{{ level === "danger" ? "SSD：救命。" : "每一版都整包複製一次" }}</div>
			</div>
		</div>
	</div>
</template>

<style scoped>
.cs {
	display: grid;
	grid-template-columns: 400px 1fr;
	align-items: center;
	gap: 48px;
	width: 860px;
	margin: 0 auto;
}

.cs-list {
	display: flex;
	flex-direction: column;
	gap: 6px;
}

.cs-row {
	display: flex;
	align-items: center;
	gap: 12px;
	height: 38px;
	padding: 0 14px;
	border-radius: 12px;
	font-family: var(--mono);
	font-size: 16px;
	color: hsl(60 30% 96% / 0.45);
	transition:
		opacity 0.45s var(--ease),
		transform 0.55s var(--ease),
		background 0.35s,
		color 0.35s;
}

.cs-row.is-hidden {
	opacity: 0;
	transform: translateY(10px);
}

.cs-row.is-current {
	background: var(--surface);
	color: var(--foreground);
}

.cs-folder {
	flex: none;
	font-size: 20px;
	color: var(--cyan);
	opacity: 0.5;
	transition: opacity 0.35s;
}

.cs-row.is-current .cs-folder {
	opacity: 1;
}

.cs-note-wrap {
	display: flex;
	align-items: flex-end;
	min-height: 130px;
}

.cs-note {
	font-size: 28px;
	font-weight: 600;
	line-height: 1.45;
}

.cs-meter {
	margin-top: 36px;
}

.cs-meter-head {
	display: flex;
	justify-content: space-between;
	margin-bottom: 8px;
	font-size: 13px;
	color: var(--comment);
}

.cs-num {
	font-family: var(--mono);
	color: var(--foreground);
}

.cs-track {
	height: 8px;
	border-radius: 99px;
	background: var(--surface);
	overflow: hidden;
}

.cs-fill {
	height: 100%;
	border-radius: 99px;
	background: var(--green);
	transition:
		width 0.6s var(--ease),
		background 0.4s;
}

.is-warn .cs-fill {
	background: var(--orange);
}

.is-danger .cs-fill {
	background: var(--red);
}

.cs-foot {
	margin-top: 8px;
	font-size: 13px;
	color: var(--comment);
	transition: color 0.3s;
}

.is-danger .cs-foot {
	color: var(--red);
}

.cs-fade-enter-active,
.cs-fade-leave-active {
	transition:
		opacity 0.3s var(--ease),
		transform 0.35s var(--ease),
		filter 0.3s;
}

.cs-fade-enter-from {
	opacity: 0;
	transform: translateY(8px);
	filter: blur(4px);
}

.cs-fade-leave-to {
	opacity: 0;
	transform: translateY(-8px);
	filter: blur(4px);
}
</style>
