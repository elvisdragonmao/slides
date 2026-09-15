<script setup lang="ts">
import { computed, ref, watch } from "vue";

// 寄包裹：Working Directory → Staging Area → Local Repository → Remote
const props = withDefaults(defineProps<{ step?: number }>(), { step: 0 });

// 往前翻才播放飛行動畫；往回翻直接回到該狀態
const forward = ref(true);
watch(
	() => props.step,
	(now, before) => {
		forward.value = now > before;
	}
);

const current = computed(() => Math.max(0, Math.min(4, props.step)));

const scenes = [
	{ cmd: "", caption: "你改了一些檔案", focus: [0] },
	{ cmd: "git add hi.txt style.css", caption: "挑出這次要寄的東西，放進箱子", focus: [1] },
	{ cmd: 'git commit -m "feat: say hello"', caption: "封箱、寫上說明，收進自己電腦的倉庫", focus: [2] },
	{ cmd: "git push", caption: "寄到收件地址", focus: [3] },
	{ cmd: "git pull", caption: "把別人寄來的新包裹拿回來整合", focus: [0, 2] }
];
const scene = computed(() => scenes[current.value]);

const stations = [
	{ en: "Working Directory", zh: "工作桌", x: 111 },
	{ en: "Staging Area", zh: "箱子", x: 310 },
	{ en: "Local Repository", zh: "你的倉庫", x: 513 },
	{ en: "Remote", zh: "收件地址", x: 756 }
];

type FileState = "changed" | "staged" | "clean";

interface DeskFile {
	name: string;
	state: FileState;
	fresh?: boolean;
}

const files = computed<DeskFile[]>(() => {
	const s = current.value;
	const picked: FileState = s >= 2 ? "clean" : s === 1 ? "staged" : "changed";
	const list: DeskFile[] = [
		{ name: "hi.txt", state: picked },
		{ name: "style.css", state: picked },
		{ name: "draft.md", state: "changed" }
	];
	if (s >= 4) list.push({ name: "navbar.css", state: "clean", fresh: true });
	return list;
});

interface Row {
	id: string;
	msg: string;
	by?: string;
}

const older: Row[] = [
	{ id: "page", msg: "add page" },
	{ id: "init", msg: "init" }
];
const mine: Row = { id: "mine", msg: "feat: say hello" };
const theirs: Row = { id: "theirs", msg: "fix: navbar", by: "海鷗" };

const localRows = computed(() => [...(current.value >= 4 ? [theirs] : []), ...(current.value >= 2 ? [mine] : []), ...older]);
const remoteRows = computed(() => [...(current.value >= 4 ? [theirs] : []), ...(current.value >= 3 ? [mine] : []), ...older]);

// 讓畫面照「封箱 → 搬運 → 入庫」的順序發生
const delays = computed(() => {
	const f = forward.value;
	const s = current.value;
	return {
		"--desk-delay": `${f && s === 4 ? 1.9 : 0}s`,
		"--local-delay": `${f && s === 2 ? 2.2 : f && s === 4 ? 1.5 : 0}s`,
		"--remote-delay": `${f && s === 3 ? 1.05 : 0}s`
	};
});
</script>

<template>
	<div class="pf" :class="{ 'is-forward': forward }" :style="delays">
		<div class="pf-zone pf-zone-local" :class="{ 'is-focus': current < 3 }">
			<span class="pf-zone-label">
				<ph-laptop />
				你的電腦
			</span>
		</div>
		<div class="pf-zone pf-zone-remote" :class="{ 'is-focus': current >= 3 }">
			<span class="pf-zone-label">
				<ph-github-logo />
				GitHub
			</span>
		</div>

		<div v-for="st in stations" :key="`floor-${st.en}`" class="pf-floor" :style="{ left: `${st.x - 92}px` }" />

		<TransitionGroup tag="div" name="pf-row" class="pf-list pf-desk">
			<div v-for="f in files" :key="f.name" class="pf-chip" :class="[`is-${f.state}`, { 'is-fresh': f.fresh }]">
				<ph-file-text class="pf-chip-icon" />
				<span class="pf-chip-text">{{ f.name }}</span>
				<ph-check-bold v-if="f.state === 'staged'" class="pf-staged" />
				<span v-else-if="f.state === 'changed'" class="pf-dot" />
			</div>
		</TransitionGroup>

		<template v-if="current === 1 && forward">
			<div v-for="(name, i) in ['hi.txt', 'style.css']" :key="`drop-${name}`" class="pf-chip pf-drop" :style="{ '--y0': `${56 + i * 38}px`, animationDelay: `${i * 0.14}s` }">
				<ph-file-text class="pf-chip-icon" />
				<span class="pf-chip-text">{{ name }}</span>
			</div>
		</template>

		<div class="pf-parcel" :class="{ 'is-stored': current >= 2 }">
			<Parcel :open="current <= 1" label="feat: say hello" />
		</div>

		<TransitionGroup tag="div" name="pf-row" class="pf-list pf-local">
			<div v-for="r in localRows" :key="r.id" class="pf-chip">
				<Parcel class="pf-mini" />
				<span class="pf-chip-text">{{ r.msg }}</span>
				<span v-if="r.by" class="pf-by">{{ r.by }}</span>
			</div>
		</TransitionGroup>

		<TransitionGroup tag="div" name="pf-row" class="pf-list pf-remote">
			<div v-for="r in remoteRows" :key="r.id" class="pf-chip">
				<Parcel class="pf-mini" />
				<span class="pf-chip-text">{{ r.msg }}</span>
				<span v-if="r.by" class="pf-by">{{ r.by }}</span>
			</div>
		</TransitionGroup>

		<div v-if="current === 3 && forward" class="pf-flyer" style="--x0: 431px; --y0: 60px; --x1: 681px; --y1: 60px">
			<Parcel label="feat: say hello" />
		</div>
		<div v-if="current === 4 && forward" class="pf-flyer is-late" style="--x0: 681px; --y0: 60px; --x1: 431px; --y1: 60px">
			<Parcel label="fix: navbar" />
		</div>

		<div v-for="(st, i) in stations" :key="st.en" class="pf-station" :class="{ 'is-focus': scene.focus.includes(i) }" :style="{ left: `${st.x}px` }">
			<div class="pf-station-en">{{ st.en }}</div>
			<div class="pf-station-zh">{{ st.zh }}</div>
		</div>

		<div class="pf-command">
			<Transition name="pf-fade" mode="out-in">
				<div :key="current" class="pf-command-inner">
					<span v-if="scene.cmd" class="pf-cmd">
						<span class="pf-prompt">$</span>
						{{ scene.cmd }}
					</span>
					<span class="pf-caption">{{ scene.caption }}</span>
				</div>
			</Transition>
		</div>
	</div>
</template>

<style scoped>
.pf {
	position: relative;
	width: 860px;
	height: 340px;
	margin: 0 auto;
	font-size: 14px;
}

.pf-zone {
	position: absolute;
	top: 0;
	height: 282px;
	border: 1px solid var(--hairline);
	border-radius: 20px;
	transition: border-color 0.4s;
}

.pf-zone.is-focus {
	border-color: var(--hairline-strong);
}

.pf-zone-local {
	left: 0;
	width: 626px;
}

.pf-zone-remote {
	left: 650px;
	width: 210px;
}

.pf-zone-label {
	position: absolute;
	left: 16px;
	top: 14px;
	display: flex;
	align-items: center;
	gap: 6px;
	font-size: 12px;
	letter-spacing: 0.04em;
	color: var(--comment);
}

.pf-floor {
	position: absolute;
	top: 226px;
	width: 184px;
	height: 1px;
	background: var(--hairline-strong);
}

/* 檔案與歷史列表 */
.pf-list {
	position: absolute;
	top: 56px;
	display: flex;
	flex-direction: column;
	gap: 8px;
}

.pf-desk {
	left: 24px;
	width: 174px;
	--delay: var(--desk-delay);
}

.pf-local {
	left: 420px;
	width: 186px;
	--delay: var(--local-delay);
}

.pf-remote {
	left: 670px;
	width: 172px;
	--delay: var(--remote-delay);
}

.pf-chip {
	box-sizing: border-box;
	display: flex;
	align-items: center;
	gap: 8px;
	width: 100%;
	height: 30px;
	padding: 0 10px;
	border-radius: 9px;
	background: var(--surface);
	border: 1px solid var(--hairline);
	font-family: var(--mono);
	font-size: 12px;
	color: var(--foreground);
	white-space: nowrap;
}

.pf-chip-icon {
	flex: none;
	font-size: 14px;
	color: var(--comment);
}

.pf-chip-text {
	flex: 1;
	overflow: hidden;
	text-overflow: ellipsis;
}

.pf-dot {
	flex: none;
	width: 7px;
	height: 7px;
	border-radius: 50%;
	background: var(--orange);
}

.pf-staged {
	flex: none;
	font-size: 13px;
	color: var(--green);
}

.pf-chip.is-fresh .pf-chip-text {
	color: var(--cyan);
}

.pf-by {
	flex: none;
	font-size: 11px;
	color: var(--pink);
}

.pf-mini {
	flex: none;
	width: 22px !important;
}

.pf-row-enter-active {
	transition:
		opacity 0.45s var(--ease) var(--delay),
		transform 0.55s var(--ease) var(--delay);
}

.pf-row-leave-active {
	position: absolute;
	transition:
		opacity 0.2s,
		transform 0.2s;
}

.pf-row-enter-from {
	opacity: 0;
	transform: translateY(-10px) scale(0.96);
}

.pf-row-leave-to {
	opacity: 0;
	transform: translateY(-6px);
}

.pf-row-move {
	transition: transform 0.5s var(--ease) var(--delay);
}

/* 主角包裹：箱子 → 倉庫 */
.pf-parcel {
	position: absolute;
	left: 0;
	top: 0;
	z-index: 3;
	width: 120px;
	transform-origin: 0 0;
	transform: translate(250px, 104px);
	transition:
		transform 0.6s var(--ease-io),
		opacity 0.2s linear;
}

.pf-parcel.is-stored {
	transform: translate(431px, 60px) scale(0.1833);
	opacity: 0;
}

.is-forward .pf-parcel.is-stored {
	transition:
		transform 0.75s var(--ease-io) 1.45s,
		opacity 0.2s linear 2.1s;
}

/* 檔案副本掉進箱子 */
.pf-drop {
	position: absolute;
	left: 0;
	top: 0;
	z-index: 4;
	width: 174px;
	transform-origin: 0 0;
	animation: pf-drop 0.9s var(--ease-io) both;
}

@keyframes pf-drop {
	0% {
		transform: translate(24px, var(--y0));
		opacity: 1;
	}
	60% {
		transform: translate(240px, 26px) scale(0.7);
		opacity: 1;
	}
	100% {
		transform: translate(275px, 112px) scale(0.4);
		opacity: 0;
	}
}

/* Push / Pull 的包裹飛行 */
.pf-flyer {
	position: absolute;
	left: 0;
	top: 0;
	z-index: 6;
	width: 120px;
	transform-origin: 0 0;
	pointer-events: none;
	animation: pf-fly 1.05s var(--ease-io) both;
}

.pf-flyer.is-late {
	animation-delay: 0.45s;
}

@keyframes pf-fly {
	0% {
		transform: translate(var(--x0), var(--y0)) scale(0.1833);
		opacity: 0;
	}
	15% {
		opacity: 1;
	}
	50% {
		transform: translate(522px, -14px) scale(0.55);
		opacity: 1;
	}
	85% {
		opacity: 1;
	}
	100% {
		transform: translate(var(--x1), var(--y1)) scale(0.1833);
		opacity: 0;
	}
}

.pf-station {
	position: absolute;
	top: 236px;
	transform: translateX(-50%);
	text-align: center;
	white-space: nowrap;
	opacity: 0.45;
	transition: opacity 0.4s;
}

.pf-station.is-focus {
	opacity: 1;
}

.pf-station-en {
	font-family: var(--mono);
	font-size: 12px;
	color: var(--comment);
	transition: color 0.4s;
}

.pf-station.is-focus .pf-station-en {
	color: var(--purple);
}

.pf-station-zh {
	margin-top: 2px;
	font-size: 15px;
}

.pf-command {
	position: absolute;
	left: 0;
	right: 0;
	top: 298px;
	display: flex;
	justify-content: center;
}

.pf-command-inner {
	display: flex;
	align-items: center;
	gap: 14px;
}

.pf-cmd {
	padding: 7px 14px;
	border-radius: 10px;
	background: var(--ink);
	border: 1px solid var(--hairline);
	font-family: var(--mono);
	font-size: 15px;
	color: var(--foreground);
}

.pf-prompt {
	margin-right: 4px;
	color: var(--green);
}

.pf-caption {
	font-size: 16px;
	color: var(--dim);
}

.pf-fade-enter-active,
.pf-fade-leave-active {
	transition:
		opacity 0.3s var(--ease),
		transform 0.3s var(--ease),
		filter 0.3s;
}

.pf-fade-enter-from {
	opacity: 0;
	transform: translateY(6px);
	filter: blur(3px);
}

.pf-fade-leave-to {
	opacity: 0;
	transform: translateY(-6px);
	filter: blur(3px);
}
</style>
