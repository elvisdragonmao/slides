<script setup lang="ts">
import { computed, onUnmounted, ref } from "vue";
import { onSlideLeave } from "@slidev/client";

const props = defineProps<{ seconds: number }>();
const remaining = ref(props.seconds);
const running = ref(false);
let deadline = 0;
let interval: number | undefined;

const time = computed(() => `${Math.floor(remaining.value / 60)}:${String(remaining.value % 60).padStart(2, "0")}`);

function pause() {
	window.clearInterval(interval);
	interval = undefined;
	running.value = false;
}

function reset() {
	pause();
	remaining.value = props.seconds;
}

function tick() {
	remaining.value = Math.max(0, Math.ceil((deadline - performance.now()) / 1000));
	if (remaining.value === 0) pause();
}

function toggle() {
	if (running.value) {
		pause();
		return;
	}

	if (remaining.value === 0) reset();
	deadline = performance.now() + remaining.value * 1000;
	running.value = true;
	interval = window.setInterval(tick, 100);
}

onSlideLeave(reset);
onUnmounted(pause);
</script>

<template>
	<div class="panel prep-timer">
		<div class="eyebrow">
			<ph-clock />
			Prep time
		</div>
		<div class="prep-time" role="timer" :class="{ 'time-up': remaining === 0 }">{{ time }}</div>
		<div class="timer-actions" @mousedown.prevent>
			<button type="button" @click.stop="toggle" @keydown.space.stop>{{ running ? "Pause" : remaining === 0 ? "Restart" : "Start" }}</button>
			<button type="button" @click.stop="reset" @keydown.space.stop>Reset</button>
		</div>
		<div class="timer-status" role="status">{{ remaining === 0 ? "Time to speak!" : "" }}</div>
	</div>
</template>

<style scoped>
.prep-timer {
	min-height: 100%;
	text-align: center;
}

.prep-timer .eyebrow {
	justify-content: center;
}

.prep-time {
	margin: 2px 0 10px;
	color: var(--cyan);
	font-size: 49px;
	line-height: 1.1;
	font-weight: 760;
	font-variant-numeric: tabular-nums;
}

.prep-time.time-up {
	color: var(--orange);
}

.timer-actions {
	display: flex;
	justify-content: center;
	gap: 6px;
}

button {
	border: 1px solid #666a86;
	padding: 4px 10px;
	border-radius: 7px;
	color: var(--foreground);
	background: #393d55;
	font-size: 15px;
	font-weight: 650;
}

button:hover,
button:focus-visible {
	border-color: var(--cyan);
}

.timer-status {
	min-height: 1.3em;
	margin-top: 6px;
	color: var(--orange);
	font-size: 13px;
}
</style>
