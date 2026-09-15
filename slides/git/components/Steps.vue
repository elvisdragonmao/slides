<script setup lang="ts">
import { onSlideEnter, onSlideLeave, useIsSlideActive, useSlideContext } from "@slidev/client";
import { computed, onMounted, ref } from "vue";

type Item = string | { t: string; d?: string };

/**
 * progress：依 step 逐一點亮（完成打勾、目前高亮）
 * reveal：依 step 逐一出現
 * auto：進到這張投影片時自動依序出現
 */
const props = withDefaults(defineProps<{ items: Item[]; step?: number; cols?: number; mode?: "progress" | "reveal" | "auto" }>(), { step: 0, cols: 0, mode: "progress" });

const list = computed(() => props.items.map(item => (typeof item === "string" ? { t: item, d: "" } : { d: "", ...item })));
const columns = computed(() => props.cols || list.value.length);

const { $renderContext } = useSlideContext();
const isActive = useIsSlideActive();
const played = ref(!["slide", "presenter"].includes($renderContext.value));

onMounted(() => {
	if (isActive.value) requestAnimationFrame(() => (played.value = true));
});
onSlideEnter(() => {
	played.value = true;
});
onSlideLeave(() => {
	if (["slide", "presenter"].includes($renderContext.value)) played.value = false;
});

function stateOf(i: number) {
	if (props.mode === "auto") return played.value ? "shown" : "hidden";
	if (props.mode === "reveal") return i <= props.step ? "shown" : "hidden";
	return i < props.step ? "done" : i === props.step ? "current" : "pending";
}

const hasArrow = (i: number) => columns.value > 1 && i < list.value.length - 1 && (i + 1) % columns.value !== 0;
</script>

<template>
	<div class="st" :class="{ 'is-vertical': columns === 1 }" :style="{ gridTemplateColumns: `repeat(${columns}, minmax(0, 1fr))` }">
		<div v-for="(item, i) in list" :key="i" class="st-item" :class="`is-${stateOf(i)}`" :style="{ '--i': i }">
			<div class="st-mark">
				<ph-check-bold v-if="stateOf(i) === 'done'" />
				<span v-else>{{ i + 1 }}</span>
			</div>
			<div class="st-text">
				<div class="st-title">{{ item.t }}</div>
				<div v-if="item.d" class="st-desc">{{ item.d }}</div>
			</div>
			<ph-caret-right-bold v-if="hasArrow(i)" class="st-arrow" />
		</div>
	</div>
</template>

<style scoped>
.st {
	display: grid;
	column-gap: 24px;
	row-gap: 14px;
	width: 100%;
}

.st.is-vertical {
	row-gap: 10px;
}

.st-item {
	position: relative;
	display: flex;
	align-items: center;
	gap: 12px;
	min-width: 0;
	padding: 12px 14px;
	border-radius: 14px;
	background: var(--surface);
	border: 1px solid var(--hairline);
	transition:
		opacity 0.45s var(--ease),
		transform 0.55s var(--ease),
		border-color 0.3s,
		filter 0.45s var(--ease);
}

.st-mark {
	flex: none;
	display: grid;
	place-items: center;
	width: 26px;
	height: 26px;
	border-radius: 50%;
	border: 1px solid var(--hairline-strong);
	font-family: var(--mono);
	font-size: 12px;
	color: var(--comment);
	transition:
		background 0.3s,
		color 0.3s,
		border-color 0.3s;
}

.st-text {
	min-width: 0;
}

.st-title {
	font-size: 15.5px;
	line-height: 1.35;
}

.st-desc {
	margin-top: 2px;
	font-size: 12.5px;
	color: var(--comment);
}

.st-arrow {
	position: absolute;
	right: -19px;
	top: 50%;
	margin-top: -7px;
	font-size: 14px;
	color: var(--comment);
}

/* progress */
.st-item.is-pending {
	opacity: 0.35;
}

.st-item.is-current {
	border-color: var(--purple);
}

.st-item.is-current .st-mark {
	background: var(--purple);
	border-color: var(--purple);
	color: var(--ink);
}

.st-item.is-done .st-mark {
	background: var(--green);
	border-color: var(--green);
	color: var(--ink);
}

/* reveal / auto */
.st-item.is-hidden {
	opacity: 0;
	transform: translateY(10px);
	filter: blur(4px);
}

.st-item.is-shown {
	transition-delay: calc(var(--i) * 70ms);
}

.st-item.is-hidden {
	transition-delay: 0s;
}
</style>
