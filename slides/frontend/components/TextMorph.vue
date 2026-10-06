<script setup lang="ts">
import { computed } from "vue";

/**
 * 文字變形：from 一個字一個字散掉，to 一個字一個字長出來
 * 兩段文字疊在同一格，容器寬度跟著比較長的那段
 */
const props = withDefaults(defineProps<{ from: string; to: string; morphed?: boolean }>(), { morphed: false });

const fromChars = computed(() => [...props.from]);
const toChars = computed(() => [...props.to]);
</script>

<template>
	<span class="tm" :class="{ 'is-morphed': morphed }">
		<span class="tm-line tm-from" :aria-hidden="morphed">
			<span v-for="(c, i) in fromChars" :key="`f${i}`" class="tm-char" :style="{ '--i': i, '--n': fromChars.length }">{{ c === " " ? " " : c }}</span>
		</span>
		<span class="tm-line tm-to" :aria-hidden="!morphed">
			<span v-for="(c, i) in toChars" :key="`t${i}`" class="tm-char" :style="{ '--i': i, '--n': toChars.length }">{{ c === " " ? " " : c }}</span>
		</span>
	</span>
</template>

<style scoped>
.tm {
	display: inline-grid;
	justify-items: center;
	vertical-align: bottom;
}

.tm-line {
	grid-area: 1 / 1;
	white-space: nowrap;
}

.tm-char {
	display: inline-block;
	transition:
		opacity 0.35s var(--ease),
		transform 0.5s var(--ease),
		filter 0.35s var(--ease);
}

/* 散掉：從左到右往上飄走 */
.tm-from .tm-char {
	transition-delay: calc(var(--i) * 28ms);
}

.is-morphed .tm-from .tm-char {
	opacity: 0;
	transform: translateY(-0.5em) rotate(-8deg);
	filter: blur(6px);
}

/* 長出來：等舊字走得差不多再從下面浮上來 */
.tm-to .tm-char {
	opacity: 0;
	transform: translateY(0.5em) scale(0.8);
	filter: blur(6px);
	transition-delay: 0s;
}

.is-morphed .tm-to .tm-char {
	opacity: 1;
	transform: none;
	filter: none;
	transition-delay: calc(0.25s + var(--i) * 32ms);
}
</style>
