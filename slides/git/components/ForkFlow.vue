<script setup lang="ts">
import { computed, ref, watch } from "vue";

// 原作者 → Fork → Clone → Commit → Push → Pull Request → Merge
const props = withDefaults(defineProps<{ step?: number }>(), { step: 0 });

const forward = ref(true);
watch(
	() => props.step,
	(now, before) => {
		forward.value = now > before;
	}
);

const current = computed(() => Math.max(0, Math.min(6, props.step)));

const scenes = [
	{ title: "someone/cool-project", mono: true, desc: "很酷的專案，但你沒有 Write 權限" },
	{ title: "Fork", desc: "複製一份到你自己的 GitHub 帳號" },
	{ title: "git clone", mono: true, desc: "把「你的 Fork」拿回電腦" },
	{ title: "git commit", mono: true, desc: "開 Branch、修掉 Bug、封箱" },
	{ title: "git push", mono: true, desc: "寄回你自己的 Fork" },
	{ title: "Pull Request", desc: "請原作者把你的包裹簽收進去" },
	{ title: "Merge", desc: "Review 通過，原作者合併。完成！" }
];
const scene = computed(() => scenes[current.value]);
</script>

<template>
	<div class="ff" :class="{ 'is-forward': forward }">
		<svg class="ff-lines" width="860" height="340" viewBox="0 0 860 340">
			<g :class="{ 'is-hidden': current < 1 }">
				<path class="ff-line" d="M334 50H528" pathLength="1" />
				<path class="ff-head" d="M520 42l10 8-10 8" />
			</g>
			<g :class="{ 'is-hidden': current < 2 }">
				<path class="ff-line" d="M760 118V218" pathLength="1" />
				<path class="ff-head" d="M752 210l8 10 8-10" />
			</g>
			<g :class="{ 'is-hidden': current < 4 }">
				<path class="ff-line" d="M636 226V126" pathLength="1" />
				<path class="ff-head" d="M628 134l8-10 8 10" />
			</g>
			<g :class="{ 'is-hidden': current < 5 }">
				<path class="ff-line is-dashed" d="M528 92H334" pathLength="1" />
				<path class="ff-head" d="M342 84l-10 8 10 8" />
			</g>
		</svg>

		<span class="ff-tag" :class="{ 'is-hidden': current < 1 }" style="left: 430px; top: 30px">Fork</span>
		<span class="ff-tag" :class="{ 'is-hidden': current < 2 }" style="left: 806px; top: 170px">Clone</span>
		<span class="ff-tag" :class="{ 'is-hidden': current < 4 }" style="left: 592px; top: 170px">Push</span>
		<span class="ff-tag" :class="{ 'is-hidden': current < 5 }" style="left: 430px; top: 114px">Pull Request</span>

		<div class="ff-card ff-origin" :class="{ 'is-merged': current >= 6 }">
			<ph-github-logo class="ff-icon" />
			<div class="ff-text">
				<div class="ff-title">someone/cool-project</div>
				<div class="ff-sub">原作者的 Repository</div>
			</div>
			<span class="ff-remote" :class="{ 'is-hidden': current < 2 }">upstream</span>
			<span class="ff-status" :class="{ 'is-hidden': current < 5, 'is-done': current >= 6 }">
				<ph-check-bold v-if="current >= 6" />
				{{ current >= 6 ? "已合併" : "等待 Review" }}
			</span>
		</div>

		<div class="ff-card ff-fork" :class="{ 'is-hidden': current < 1 }">
			<ph-git-fork class="ff-icon" />
			<div class="ff-text">
				<div class="ff-title">your-name/cool-project</div>
				<div class="ff-sub">你的 Fork，可以自己 Push</div>
			</div>
			<span class="ff-remote" :class="{ 'is-hidden': current < 2 }">origin</span>
		</div>

		<div class="ff-card ff-pc" :class="{ 'is-hidden': current < 2 }">
			<ph-laptop class="ff-icon" />
			<div class="ff-text">
				<div class="ff-title">你的電腦</div>
				<div class="ff-sub ff-branch">fix/awesome-bug</div>
			</div>
		</div>

		<div class="ff-parcel" :class="{ 'is-hidden': current < 3 }" style="left: 778px; top: 250px">
			<Parcel label="fix" />
		</div>
		<div class="ff-parcel" :class="{ 'is-hidden': current < 4, 'is-late': forward && current === 4 }" style="left: 778px; top: 42px">
			<Parcel label="fix" />
		</div>
		<div class="ff-parcel" :class="{ 'is-hidden': current < 5, 'is-late': forward && current === 5 }" style="left: 258px; top: 42px">
			<Parcel label="fix" />
		</div>

		<div v-if="forward && current === 4" class="ff-flyer" style="--x0: 778px; --y0: 250px; --xm: 700px; --ym: 146px; --x1: 778px; --y1: 42px">
			<Parcel label="fix" />
		</div>
		<div v-if="forward && current === 5" class="ff-flyer" style="--x0: 778px; --y0: 42px; --xm: 518px; --ym: 118px; --x1: 258px; --y1: 42px">
			<Parcel label="fix" />
		</div>

		<div class="ff-caption">
			<Transition name="ff-fade" mode="out-in">
				<div :key="current">
					<div class="ff-no">{{ current === 0 ? "START" : `STEP ${current}` }}</div>
					<div class="ff-cap-title" :class="{ 'is-mono': scene.mono }">{{ scene.title }}</div>
					<div class="ff-cap-desc">{{ scene.desc }}</div>
				</div>
			</Transition>
		</div>
	</div>
</template>

<style scoped>
.ff {
	position: relative;
	width: 860px;
	height: 340px;
	margin: 0 auto;
}

.ff-lines {
	position: absolute;
	left: 0;
	top: 0;
	overflow: visible;
}

.ff-line,
.ff-head {
	fill: none;
	stroke: var(--purple);
	stroke-width: 2.5;
	stroke-linecap: round;
	stroke-linejoin: round;
}

.ff-line {
	stroke-dasharray: 1 1;
	stroke-dashoffset: 0;
	transition:
		stroke-dashoffset 0.7s var(--ease) 0.2s,
		opacity 0s;
}

.ff-line.is-dashed {
	stroke: var(--orange);
	stroke-dasharray: 0.03 0.025;
	transition: opacity 0.4s 0.2s;
}

.ff-head {
	transition: opacity 0.25s 0.7s;
}

/* 收起時透明度歸零，避免圓頭線帽留下小點 */
.is-hidden .ff-line {
	stroke-dashoffset: 1;
	opacity: 0;
	transition:
		stroke-dashoffset 0.4s var(--ease),
		opacity 0s linear 0.4s;
}

.is-hidden .ff-line.is-dashed {
	stroke-dashoffset: 0;
	transition: opacity 0.2s;
}

.is-hidden .ff-head {
	opacity: 0;
	transition-delay: 0s;
}

.ff-tag {
	position: absolute;
	transform: translate(-50%, -50%);
	padding: 2px 10px;
	border-radius: 999px;
	background: var(--background);
	font-family: var(--mono);
	font-size: 13px;
	color: var(--purple);
	white-space: nowrap;
	transition: opacity 0.4s var(--ease) 0.4s;
}

.ff-tag.is-hidden {
	opacity: 0;
	transition-delay: 0s;
}

.ff-card {
	position: absolute;
	box-sizing: border-box;
	display: flex;
	align-items: center;
	gap: 12px;
	width: 300px;
	height: 92px;
	padding: 0 18px;
	background: var(--surface);
	border: 1px solid var(--hairline);
	border-radius: 18px;
	transition:
		opacity 0.5s var(--ease),
		transform 0.8s var(--ease-io),
		border-color 0.4s;
}

.ff-origin {
	left: 20px;
	top: 4px;
}

.ff-fork {
	left: 540px;
	top: 4px;
}

.ff-pc {
	left: 540px;
	top: 226px;
}

.ff-fork.is-hidden {
	opacity: 0;
	transform: translateX(-520px);
}

.ff-pc.is-hidden {
	opacity: 0;
	transform: translateY(-222px);
}

.ff-origin.is-merged {
	border-color: color-mix(in srgb, var(--green) 60%, transparent);
}

.ff-icon {
	flex: none;
	font-size: 24px;
	color: var(--purple);
}

.ff-text {
	min-width: 0;
}

.ff-title {
	font-family: var(--mono);
	font-size: 13px;
	white-space: nowrap;
}

.ff-sub {
	margin-top: 2px;
	font-size: 12.5px;
	color: var(--comment);
}

.ff-branch {
	font-family: var(--mono);
	color: var(--green);
}

.ff-remote {
	position: absolute;
	top: -11px;
	right: 16px;
	padding: 1px 9px;
	border-radius: 999px;
	background: var(--background);
	border: 1px solid color-mix(in srgb, var(--cyan) 50%, transparent);
	font-family: var(--mono);
	font-size: 12px;
	color: var(--cyan);
	transition: opacity 0.4s var(--ease) 0.6s;
}

.ff-remote.is-hidden {
	opacity: 0;
	transition-delay: 0s;
}

.ff-status {
	position: absolute;
	left: 18px;
	bottom: -13px;
	display: flex;
	align-items: center;
	gap: 5px;
	padding: 2px 10px;
	border-radius: 999px;
	background: var(--background);
	border: 1px solid color-mix(in srgb, var(--orange) 50%, transparent);
	font-size: 12px;
	color: var(--orange);
	transition:
		opacity 0.4s var(--ease) 1s,
		color 0.3s,
		border-color 0.3s;
}

.ff-status.is-done {
	border-color: color-mix(in srgb, var(--green) 50%, transparent);
	color: var(--green);
	transition-delay: 0s;
}

.ff-status.is-hidden {
	opacity: 0;
	transition-delay: 0s;
}

.ff-parcel {
	position: absolute;
	width: 44px;
	transition:
		opacity 0.4s var(--ease),
		transform 0.55s var(--spring);
}

.ff-parcel.is-hidden {
	opacity: 0;
	transform: scale(0.5);
}

.ff-parcel.is-late {
	transition-delay: 0.9s;
}

.ff-flyer {
	position: absolute;
	left: 0;
	top: 0;
	z-index: 5;
	width: 44px;
	pointer-events: none;
	animation: ff-fly 1s var(--ease-io) both;
}

@keyframes ff-fly {
	0% {
		transform: translate(var(--x0), var(--y0));
		opacity: 0;
	}
	12% {
		opacity: 1;
	}
	50% {
		transform: translate(var(--xm), var(--ym)) scale(1.3);
		opacity: 1;
	}
	88% {
		opacity: 1;
	}
	100% {
		transform: translate(var(--x1), var(--y1));
		opacity: 0;
	}
}

.ff-caption {
	position: absolute;
	left: 24px;
	top: 176px;
	width: 470px;
}

.ff-no {
	font-family: var(--mono);
	font-size: 12px;
	letter-spacing: 0.16em;
	color: var(--comment);
}

.ff-cap-title {
	margin-top: 6px;
	font-size: 30px;
	font-weight: 700;
	color: var(--foreground);
}

.ff-cap-title.is-mono {
	font-family: var(--mono);
	font-size: 26px;
	color: var(--green);
}

.ff-cap-desc {
	margin-top: 6px;
	font-size: 17px;
	color: var(--dim);
}

.ff-fade-enter-active,
.ff-fade-leave-active {
	transition:
		opacity 0.3s var(--ease),
		transform 0.3s var(--ease),
		filter 0.3s;
}

.ff-fade-enter-from {
	opacity: 0;
	transform: translateY(8px);
	filter: blur(3px);
}

.ff-fade-leave-to {
	opacity: 0;
	transform: translateY(-8px);
	filter: blur(3px);
}
</style>
