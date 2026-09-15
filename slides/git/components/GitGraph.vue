<script setup lang="ts">
import { computed, onBeforeUnmount, reactive, watch } from "vue";

type Tone = "purple" | "green" | "orange" | "pink" | "cyan" | "red" | "muted";

interface Move {
	at: number;
	x?: number;
	y?: number;
	label?: string;
	tone?: Tone;
	note?: string;
}

interface GNode {
	id: string;
	x: number;
	y: number;
	label?: string;
	note?: string;
	tone?: Tone;
	at?: number;
	until?: number;
	ghost?: boolean;
	small?: boolean;
	moves?: Move[];
}

interface GEdge {
	from: string;
	to: string;
	tone?: Tone;
	at?: number;
	until?: number;
	dashed?: boolean;
}

interface GTag {
	text: string;
	node: string;
	tone?: Tone;
	at?: number;
	until?: number;
	head?: boolean;
	side?: "top" | "bottom";
	moves?: { at: number; node?: string; text?: string }[];
}

interface Caption {
	cmd?: string;
	text?: string;
}

interface Preset {
	gx: number;
	gy: number;
	padX?: number;
	padTop?: number;
	padBottom?: number;
	nodes: GNode[];
	edges: GEdge[];
	tags?: GTag[];
	captions?: Caption[];
}

const props = withDefaults(defineProps<{ preset: string; step?: number }>(), { step: 0 });

const COLORS: Record<Tone, string> = {
	purple: "var(--purple)",
	green: "var(--green)",
	orange: "var(--orange)",
	pink: "var(--pink)",
	cyan: "var(--cyan)",
	red: "var(--red)",
	muted: "var(--comment)"
};

const mainLine = (): GNode[] => [
	{ id: "a", x: 0, y: 0, label: "A" },
	{ id: "b", x: 1, y: 0, label: "B" },
	{ id: "c", x: 2, y: 0, label: "C" }
];
const mainEdges = (): GEdge[] => [
	{ from: "a", to: "b" },
	{ from: "b", to: "c" }
];

const PRESETS: Record<string, Preset> = {
	branch: {
		gx: 130,
		gy: 100,
		padTop: 70,
		padBottom: 70,
		nodes: [...mainLine(), { id: "d", x: 2, y: 1, label: "D", tone: "green", at: 1 }, { id: "e", x: 3, y: 1, label: "E", tone: "green", at: 2 }, { id: "m", x: 4, y: 0, label: "M", at: 3 }],
		edges: [...mainEdges(), { from: "b", to: "d", tone: "green", at: 1 }, { from: "d", to: "e", tone: "green", at: 2 }, { from: "c", to: "m", at: 3 }, { from: "e", to: "m", tone: "green", at: 3 }],
		tags: [
			{ text: "main", node: "c", moves: [{ at: 3, node: "m" }] },
			{ text: "feat/login", node: "d", tone: "green", at: 1, moves: [{ at: 2, node: "e" }] }
		],
		captions: [
			{ text: "main 保持穩定，是正式版本" },
			{ cmd: "git switch -c feat/login", text: "開一條平行世界" },
			{ text: "在 feat/login 裡慢慢把功能寫完" },
			{ cmd: "git merge feat/login", text: "做完、測完，再合回去" }
		]
	},
	switch: {
		gx: 170,
		gy: 110,
		padTop: 100,
		padBottom: 90,
		nodes: [
			{ id: "a", x: 0, y: 0, label: "A" },
			{ id: "b", x: 1, y: 0, label: "B" },
			{ id: "c", x: 2, y: 1, label: "C", tone: "green", at: 2 }
		],
		edges: [
			{ from: "a", to: "b" },
			{ from: "b", to: "c", tone: "green", at: 2 }
		],
		tags: [
			{ text: "main", node: "b" },
			{ text: "dev", node: "b", tone: "green", at: 1, moves: [{ at: 2, node: "c" }] },
			{
				text: "HEAD → main",
				node: "b",
				tone: "cyan",
				head: true,
				side: "bottom",
				moves: [
					{ at: 1, text: "HEAD → dev" },
					{ at: 2, node: "c" },
					{ at: 3, node: "b", text: "HEAD → main" },
					{ at: 4, node: "c", text: "HEAD → dev" }
				]
			}
		],
		captions: [
			{ text: "現在站在 main" },
			{ cmd: "git switch -c dev", text: "-c 就是 Create：建立並切換過去" },
			{ cmd: 'git commit -m "feat: update greeting"', text: "在 dev 留下新的 Commit" },
			{ cmd: "git switch main", text: "欸？剛剛的修改不見了？" },
			{ cmd: "git switch dev", text: "沒有，它在 dev。平行宇宙的東西又回來了" }
		]
	},
	merge: {
		gx: 120,
		gy: 100,
		padTop: 70,
		padBottom: 70,
		nodes: [...mainLine(), { id: "d", x: 2, y: 1, label: "D", tone: "green" }, { id: "e", x: 3, y: 1, label: "E", tone: "green" }, { id: "m", x: 4, y: 0, label: "M", tone: "orange", at: 1 }],
		edges: [...mainEdges(), { from: "b", to: "d", tone: "green" }, { from: "d", to: "e", tone: "green" }, { from: "c", to: "m", at: 1 }, { from: "e", to: "m", tone: "green", at: 1 }],
		tags: [
			{ text: "main", node: "c", moves: [{ at: 1, node: "m" }] },
			{ text: "feat/login", node: "e", tone: "green" }
		],
		captions: [{ text: "兩條 Branch 各自往前" }, { text: "M 就是 Merge Commit：記錄兩條在這裡合併" }]
	},
	rebase: {
		gx: 120,
		gy: 100,
		padTop: 70,
		padBottom: 70,
		nodes: [
			{ id: "d0", x: 2, y: 1, label: "D", tone: "muted", ghost: true, at: 1 },
			{ id: "e0", x: 3, y: 1, label: "E", tone: "muted", ghost: true, at: 1 },
			...mainLine(),
			{ id: "d", x: 2, y: 1, label: "D", tone: "green", moves: [{ at: 1, x: 3, y: 0, label: "D'", tone: "orange" }] },
			{ id: "e", x: 3, y: 1, label: "E", tone: "green", moves: [{ at: 1, x: 4, y: 0, label: "E'", tone: "orange" }] }
		],
		edges: [
			{ from: "b", to: "d0", tone: "muted", dashed: true, at: 1 },
			{ from: "d0", to: "e0", tone: "muted", dashed: true, at: 1 },
			...mainEdges(),
			{ from: "b", to: "d", tone: "green", until: 1 },
			{ from: "d", to: "e", tone: "green", until: 1 },
			{ from: "c", to: "d", tone: "orange", at: 1 },
			{ from: "d", to: "e", tone: "orange", at: 1 }
		],
		tags: [
			{ text: "main", node: "c" },
			{ text: "feat/login", node: "e", tone: "green" }
		],
		captions: [{ text: "原本從 B 分出去" }, { text: "把 D、E 拿起來，重新接到最新的 C 後面" }]
	},
	squash: {
		gx: 56,
		gy: 100,
		padX: 50,
		padTop: 70,
		padBottom: 70,
		nodes: [
			{ id: "a", x: 0, y: 0, label: "A" },
			{ id: "b", x: 1.4, y: 0, label: "B" },
			...Array.from({ length: 7 }, (_, i): GNode => ({ id: `c${i}`, x: 2.6 + i, y: 1, tone: "green", small: true, until: 2, moves: [{ at: 1, x: 5.6, y: 1 }] })),
			{ id: "s", x: 2.8, y: 0, label: "S", tone: "orange", at: 2 }
		],
		edges: [
			{ from: "a", to: "b" },
			{ from: "b", to: "c0", tone: "green", until: 2 },
			...Array.from({ length: 6 }, (_, i): GEdge => ({ from: `c${i}`, to: `c${i + 1}`, tone: "green", until: 2 })),
			{ from: "b", to: "s", tone: "orange", at: 2 }
		],
		tags: [
			{ text: "main", node: "b", moves: [{ at: 2, node: "s" }] },
			{ text: "feat/login", node: "c6", tone: "green", until: 2 }
		],
		captions: [{ text: "開發時留下的 7 個小 Commit" }, { text: "壓成一個" }, { text: "再放進 main" }]
	},
	conflict: {
		gx: 180,
		gy: 120,
		padTop: 70,
		padBottom: 110,
		nodes: [
			{ id: "a", x: 0, y: 0, label: "A", note: "Hello!" },
			{ id: "d", x: 1, y: 1, label: "D", tone: "green", note: "Hello from dev!", at: 1 },
			{ id: "b", x: 1, y: 0, label: "B", note: "Hello from main!", at: 2 },
			{ id: "x", x: 2, y: 0, label: "!", tone: "red", note: "CONFLICT", at: 3 }
		],
		edges: [
			{ from: "a", to: "d", tone: "green", at: 1 },
			{ from: "a", to: "b", at: 2 },
			{ from: "b", to: "x", tone: "red", dashed: true, at: 3 },
			{ from: "d", to: "x", tone: "red", dashed: true, at: 3 }
		],
		tags: [
			{ text: "main", node: "a", moves: [{ at: 2, node: "b" }] },
			{ text: "dev", node: "d", tone: "green", at: 1 }
		],
		captions: [
			{ text: "hi.txt 原本是 Hello!" },
			{ cmd: "git switch -c dev", text: "改成 Hello from dev!，Commit" },
			{ cmd: "git switch main", text: "同一行改成 Hello from main!，Commit" },
			{ cmd: "git merge dev", text: "同一行有兩個答案" }
		]
	}
};

const graph = computed(() => PRESETS[props.preset] ?? PRESETS.branch);
const padX = computed(() => graph.value.padX ?? 70);
const padTop = computed(() => graph.value.padTop ?? 80);
const padBottom = computed(() => graph.value.padBottom ?? 80);

const visible = (item: { at?: number; until?: number }, step = props.step) => (item.at ?? 0) <= step && (item.until === undefined || step < item.until);

function nodeAt(n: GNode, step: number) {
	let s = { x: n.x, y: n.y, label: n.label ?? "", tone: n.tone ?? ("purple" as Tone), note: n.note ?? "" };
	for (const m of n.moves ?? []) {
		if (m.at <= step) s = { x: m.x ?? s.x, y: m.y ?? s.y, label: m.label ?? s.label, tone: m.tone ?? s.tone, note: m.note ?? s.note };
	}
	return s;
}

function tagAt(t: GTag, step: number) {
	let s = { node: t.node, text: t.text };
	for (const m of t.moves ?? []) {
		if (m.at <= step) s = { node: m.node ?? s.node, text: m.text ?? s.text };
	}
	return s;
}

const px = (x: number) => padX.value + x * graph.value.gx;
const py = (y: number) => padTop.value + y * graph.value.gy;
const sideOf = (t: GTag, y: number) => t.side ?? (y > 0 ? "bottom" : "top");

const size = computed(() => {
	let mx = 0;
	let my = 0;
	for (const n of graph.value.nodes) {
		for (const p of [n, ...(n.moves ?? [])]) {
			mx = Math.max(mx, p.x ?? 0);
			my = Math.max(my, p.y ?? 0);
		}
	}
	return { w: padX.value * 2 + mx * graph.value.gx, h: padTop.value + my * graph.value.gy + padBottom.value };
});

// 節點與標籤的目標座標，一起補間才不會各跑各的
function targets(step: number) {
	const out: Record<string, { x: number; y: number }> = {};
	const states: Record<string, ReturnType<typeof nodeAt>> = {};
	for (const n of graph.value.nodes) {
		states[n.id] = nodeAt(n, step);
		out[n.id] = { x: px(states[n.id].x), y: py(states[n.id].y) };
	}
	const stacks: Record<string, number> = {};
	(graph.value.tags ?? []).forEach((t, i) => {
		const s = tagAt(t, step);
		const node = states[s.node];
		const side = sideOf(t, node.y);
		const key = `${s.node}:${side}`;
		let idx = 0;
		if (visible(t, step)) {
			idx = stacks[key] ?? 0;
			stacks[key] = idx + 1;
		}
		const offset = 38 + idx * 28;
		out[`tag${i}`] = { x: px(node.x), y: py(node.y) + (side === "top" ? -offset : offset) };
	});
	return out;
}

const disp = reactive<Record<string, { x: number; y: number }>>({});
let raf = 0;

function go(step: number, instant: boolean) {
	cancelAnimationFrame(raf);
	const to = targets(step);
	if (instant) {
		Object.assign(disp, to);
		return;
	}
	const from: Record<string, { x: number; y: number }> = {};
	for (const k in to) from[k] = disp[k] ? { ...disp[k] } : { ...to[k] };
	const start = performance.now();
	const tick = (now: number) => {
		const p = Math.min(1, (now - start) / 720);
		const e = p < 0.5 ? 4 * p * p * p : 1 - Math.pow(-2 * p + 2, 3) / 2;
		for (const k in to) disp[k] = { x: from[k].x + (to[k].x - from[k].x) * e, y: from[k].y + (to[k].y - from[k].y) * e };
		if (p < 1) raf = requestAnimationFrame(tick);
	};
	raf = requestAnimationFrame(tick);
}

go(props.step, true);
watch(
	() => props.step,
	s => go(s, false)
);
watch(
	() => props.preset,
	() => go(props.step, true)
);
onBeforeUnmount(() => cancelAnimationFrame(raf));

const nodes = computed(() => graph.value.nodes.map(n => ({ n, s: nodeAt(n, props.step), show: visible(n) })));

const tags = computed(() =>
	(graph.value.tags ?? []).map((t, i) => {
		const s = tagAt(t, props.step);
		return { key: `tag${i}`, t, s, show: visible(t), w: s.text.length * 7.4 + 22 };
	})
);

const bottomTags = computed(() => {
	const count: Record<string, number> = {};
	for (const t of graph.value.tags ?? []) {
		if (!visible(t)) continue;
		const s = tagAt(t, props.step);
		const node = graph.value.nodes.find(n => n.id === s.node);
		if (node && sideOf(t, nodeAt(node, props.step).y) === "bottom") count[s.node] = (count[s.node] ?? 0) + 1;
	}
	return count;
});

function edgePath(e: GEdge) {
	const a = disp[e.from];
	const b = disp[e.to];
	if (!a || !b) return "";
	if (Math.abs(a.y - b.y) < 0.5) return `M${a.x} ${a.y}L${b.x} ${b.y}`;
	const mx = (a.x + b.x) / 2;
	return `M${a.x} ${a.y}C${mx} ${a.y} ${mx} ${b.y} ${b.x} ${b.y}`;
}

const caption = computed(() => {
	const list = graph.value.captions;
	if (!list?.length) return null;
	return list[Math.max(0, Math.min(list.length - 1, props.step))];
});
</script>

<template>
	<div class="gg">
		<svg class="gg-svg" :width="size.w" :height="size.h" :viewBox="`0 0 ${size.w} ${size.h}`">
			<path
				v-for="(e, i) in graph.edges"
				:key="`e${i}`"
				class="gg-edge"
				:class="{ 'is-hidden': !visible(e), 'is-dashed': e.dashed }"
				:d="edgePath(e)"
				pathLength="1"
				:style="{ stroke: COLORS[e.tone ?? 'purple'] }"
			/>
			<g v-for="{ n, s, show } in nodes" :key="n.id" :transform="`translate(${disp[n.id]?.x ?? 0} ${disp[n.id]?.y ?? 0})`">
				<g class="gg-node" :class="{ 'is-hidden': !show, 'is-ghost': n.ghost }">
					<circle :r="n.small ? 11 : 17" :style="{ stroke: COLORS[s.tone] }" />
					<text v-if="s.label" class="gg-label" dy="0.36em" :style="{ fill: COLORS[s.tone] }">{{ s.label }}</text>
				</g>
				<text v-if="s.note" class="gg-note" :class="{ 'is-hidden': !show, 'is-alert': s.tone === 'red' }" :y="36 + (bottomTags[n.id] ?? 0) * 28" dy="0.36em">{{ s.note }}</text>
			</g>
			<g v-for="tag in tags" :key="tag.key" :transform="`translate(${disp[tag.key]?.x ?? 0} ${disp[tag.key]?.y ?? 0})`">
				<g class="gg-tag" :class="{ 'is-hidden': !tag.show }">
					<rect :x="-tag.w / 2" y="-11" :width="tag.w" height="22" rx="11" :style="{ stroke: COLORS[tag.t.tone ?? 'purple'], fill: tag.t.head ? COLORS[tag.t.tone ?? 'cyan'] : undefined }" />
					<text dy="0.36em" :style="{ fill: tag.t.head ? 'var(--ink)' : COLORS[tag.t.tone ?? 'purple'] }">{{ tag.s.text }}</text>
				</g>
			</g>
		</svg>
		<div v-if="caption" class="gg-caption">
			<Transition name="gg-fade" mode="out-in">
				<div :key="step" class="gg-caption-inner">
					<span v-if="caption.cmd" class="gg-cmd">{{ caption.cmd }}</span>
					<span v-if="caption.text" class="gg-text">{{ caption.text }}</span>
				</div>
			</Transition>
		</div>
	</div>
</template>

<style scoped>
.gg {
	display: flex;
	flex-direction: column;
	align-items: center;
	gap: 4px;
}

.gg-svg {
	max-width: 100%;
	height: auto;
	overflow: visible;
}

.gg-edge {
	fill: none;
	stroke-width: 3;
	stroke-linecap: round;
	stroke-dasharray: 1 1;
	stroke-dashoffset: 0;
	transition:
		stroke-dashoffset 0.6s var(--ease) 0.12s,
		opacity 0s;
}

/* 收起後也把透明度歸零，避免圓頭線帽在端點留下小點 */
.gg-edge.is-hidden {
	stroke-dashoffset: 1;
	opacity: 0;
	transition:
		stroke-dashoffset 0.4s var(--ease),
		opacity 0s linear 0.4s;
}

.gg-edge.is-dashed {
	stroke-width: 2.5;
	stroke-dasharray: 0.018 0.022;
}

.gg-edge.is-dashed.is-hidden {
	stroke-dashoffset: 0;
	opacity: 0;
}

.gg-node {
	transform-box: fill-box;
	transform-origin: center;
	transition:
		opacity 0.4s var(--ease),
		transform 0.55s var(--spring);
}

.gg-node.is-hidden {
	opacity: 0;
	transform: scale(0.3);
}

.gg-node circle {
	fill: var(--background);
	stroke-width: 3;
	transition: stroke 0.4s;
}

.gg-node.is-ghost {
	opacity: 0.45;
}

.gg-node.is-ghost.is-hidden {
	opacity: 0;
}

.gg-node.is-ghost circle {
	stroke-dasharray: 4 4;
}

.gg-label {
	font-family: var(--mono);
	font-size: 13px;
	font-weight: 700;
	text-anchor: middle;
	transition: fill 0.4s;
}

.gg-note {
	font-family: var(--mono);
	font-size: 12.5px;
	text-anchor: middle;
	fill: var(--dim);
	transition: opacity 0.4s;
}

.gg-note.is-alert {
	fill: var(--red);
	font-weight: 700;
}

.gg-note.is-hidden {
	opacity: 0;
}

.gg-tag {
	transform-box: fill-box;
	transform-origin: center;
	transition:
		opacity 0.4s var(--ease),
		transform 0.5s var(--spring);
}

.gg-tag.is-hidden {
	opacity: 0;
	transform: scale(0.6);
}

.gg-tag rect {
	fill: var(--background);
	stroke-width: 1.5;
}

.gg-tag text {
	font-family: var(--mono);
	font-size: 12px;
	font-weight: 600;
	text-anchor: middle;
}

.gg-caption {
	display: flex;
	justify-content: center;
	min-height: 38px;
}

.gg-caption-inner {
	display: flex;
	flex-wrap: wrap;
	align-items: center;
	justify-content: center;
	gap: 12px;
}

.gg-cmd {
	padding: 6px 12px;
	border-radius: 10px;
	background: var(--ink);
	border: 1px solid var(--hairline);
	font-family: var(--mono);
	font-size: 14px;
}

.gg-text {
	font-size: 16px;
	color: var(--dim);
}

.gg-fade-enter-active,
.gg-fade-leave-active {
	transition:
		opacity 0.3s var(--ease),
		transform 0.3s var(--ease),
		filter 0.3s;
}

.gg-fade-enter-from {
	opacity: 0;
	transform: translateY(6px);
	filter: blur(3px);
}

.gg-fade-leave-to {
	opacity: 0;
	transform: translateY(-6px);
	filter: blur(3px);
}
</style>
