<script setup lang="ts">
import { computed, ref, watch } from "vue";

/**
 * HTTP Method 寄包裹：GET 是腳踏車（資料疊在外面、寫在網址），POST 是貨車（資料鎖在貨櫃 Body）
 * bike  step：0 在家裝好 → 1 到伺服器 → 2 載著回應回來
 * truck step：0 箱子在地上 → 1 裝進貨櫃 → 2 到伺服器 → 3 載著回應回來
 */
const props = withDefaults(
	defineProps<{
		vehicle?: "bike" | "truck";
		step?: number;
		method?: string;
		url?: string;
		cargo?: string[];
		response?: string[];
		status?: string;
		from?: string;
		to?: string;
		toIcon?: "server" | "github";
	}>(),
	{ vehicle: "bike", step: 0, method: "", url: "", cargo: () => [], response: () => [], status: "", from: "你的瀏覽器", to: "伺服器", toIcon: "server" }
);

const isBike = computed(() => props.vehicle === "bike");
const phases = computed(() => (isBike.value ? ["loaded", "there", "back"] : ["load", "loaded", "there", "back"]));
const phase = computed(() => phases.value[Math.max(0, Math.min(phases.value.length - 1, props.step))]);

const W = 860;
const vw = computed(() => (isBike.value ? 170 : 230));
const x = computed(() => (phase.value === "there" ? W - 150 - vw.value : 150));

// 腳踏車車頭朝右、貨車車頭朝左：出發時要面向伺服器，回程面向使用者
const flipped = computed(() => (isBike.value ? phase.value === "back" : phase.value === "there"));

const moving = ref(false);
let timer: ReturnType<typeof setTimeout> | undefined;
watch(
	() => x.value,
	() => {
		moving.value = true;
		clearTimeout(timer);
		timer = setTimeout(() => (moving.value = false), 1400);
	}
);

const load = computed(() => (phase.value === "back" ? props.response : props.cargo));
const methodLabel = computed(() => props.method || (isBike.value ? "GET" : "POST"));
const loadedInTruck = computed(() => phase.value !== "load");
</script>

<template>
	<div class="ride" :class="[`is-${vehicle}`, `is-${phase}`]">
		<div class="ride-bar">
			<span class="ride-method" :class="isBike ? 'is-get' : 'is-post'">{{ methodLabel }}</span>
			<span class="ride-url">{{ url }}</span>
		</div>

		<div class="ride-road" />

		<div class="ride-end ride-from" :class="{ 'is-focus': phase !== 'there' }">
			<img src="../img/imac.svg" alt="" />
			<div class="ride-end-label">{{ from }}</div>
			<Transition name="ride-pop">
				<div v-if="phase === 'back' && status" class="ride-status" :class="{ 'is-bad': /^[45]/.test(status) }">{{ status }}</div>
			</Transition>
		</div>

		<div class="ride-end ride-to" :class="{ 'is-focus': phase === 'there' }">
			<div class="ride-pulse" />
			<img v-if="toIcon === 'server'" src="../img/server.svg" alt="" />
			<ph-github-logo v-else class="ride-gh" />
			<div class="ride-end-label">{{ to }}</div>
		</div>

		<div class="ride-veh" :class="{ 'is-moving': moving }" :style="{ width: `${vw}px`, transform: `translateX(${x}px)` }">
			<div class="ride-bob">
				<img v-if="isBike" src="../img/bike.svg" class="ride-art" :class="{ 'is-flipped': flipped }" alt="" />
				<img v-else src="../img/truck.svg" class="ride-art" :class="{ 'is-flipped': flipped }" alt="" />

				<!-- 腳踏車：東西直接疊在後座，大家都看得到 -->
				<TransitionGroup v-if="isBike" tag="div" name="ride-box" class="ride-stack" :class="{ 'is-flipped': flipped, 'is-tall': load.length > 4 }">
					<div v-for="(label, i) in load" :key="`${phase === 'back' ? 'r' : 'c'}-${label}`" class="ride-box" :style="{ '--i': i }">
						<img src="../img/box.svg" alt="" />
						<span>{{ label }}</span>
					</div>
				</TransitionGroup>

				<!-- 貨車：東西鎖在貨櫃裡，外面只看得到一張標籤 -->
				<Transition v-else name="ride-pop">
					<div v-if="loadedInTruck && load.length" :key="phase === 'back' ? 'r' : 'c'" class="ride-body" :class="{ 'is-flipped': flipped }">
						<ph-lock-simple-bold />
						Body
						<span class="ride-body-count">× {{ load.length }}</span>
					</div>
				</Transition>
			</div>
		</div>

		<!-- 貨車裝貨：箱子從地上飛進貨櫃 -->
		<div v-if="!isBike" class="ride-ground" :class="{ 'is-loaded': loadedInTruck }">
			<div v-for="(label, i) in cargo" :key="label" class="ride-box" :style="{ '--i': i }">
				<img src="../img/box.svg" alt="" />
				<span>{{ label }}</span>
			</div>
		</div>
	</div>
</template>

<style scoped>
.ride {
	position: relative;
	width: 860px;
	height: 340px;
	margin: 0 auto;
}

.ride-bar {
	position: absolute;
	left: 50%;
	top: 0;
	transform: translateX(-50%);
	display: flex;
	align-items: center;
	gap: 10px;
	min-width: 420px;
	padding: 7px 14px;
	border-radius: 999px;
	background: var(--ink);
	border: 1px solid var(--hairline-strong);
	font-family: var(--mono);
	font-size: 15px;
	white-space: nowrap;
}

.ride-method {
	padding: 1px 8px;
	border-radius: 6px;
	font-size: 12px;
	font-weight: 700;
	color: var(--ink);
}

.ride-method.is-get {
	background: var(--cyan);
}

.ride-method.is-post {
	background: var(--orange);
}

.ride-url {
	color: var(--foreground);
}

.ride-road {
	position: absolute;
	left: 0;
	right: 0;
	top: 282px;
	height: 2px;
	background: repeating-linear-gradient(90deg, var(--hairline-strong) 0 18px, transparent 18px 32px);
}

.ride-end {
	position: absolute;
	top: 176px;
	width: 120px;
	text-align: center;
	opacity: 0.55;
	transition: opacity 0.4s;
}

.ride-end.is-focus {
	opacity: 1;
}

.ride-end img,
.ride-gh {
	display: block;
	height: 100px;
	width: auto;
	margin: 0 auto;
}

.ride-gh {
	width: 100px;
	color: var(--foreground);
}

.ride-end-label {
	margin-top: 14px;
	font-size: 15px;
	color: var(--dim);
}

.ride-from {
	left: 0;
}

.ride-to {
	right: 0;
}

.ride-pulse {
	position: absolute;
	left: 50%;
	top: 50px;
	width: 120px;
	height: 120px;
	margin: -60px 0 0 -60px;
	border-radius: 50%;
	border: 2px solid var(--green);
	opacity: 0;
}

.ride-to.is-focus .ride-pulse {
	animation: ride-pulse 1.4s ease-out 1.3s 2;
}

@keyframes ride-pulse {
	from {
		transform: scale(0.6);
		opacity: 0.9;
	}
	to {
		transform: scale(1.4);
		opacity: 0;
	}
}

.ride-status {
	position: absolute;
	left: 50%;
	top: -46px;
	transform: translateX(-50%);
	padding: 4px 12px;
	border-radius: 999px;
	background: var(--green);
	color: var(--ink);
	font-family: var(--mono);
	font-size: 14px;
	font-weight: 700;
	white-space: nowrap;
	transition-delay: 1.3s;
}

.ride-status.is-bad {
	background: var(--red);
}

/* 交通工具 */
.ride-veh {
	position: absolute;
	left: 0;
	bottom: 56px;
	z-index: 2;
	transition: transform 1.3s var(--ease-io);
}

.ride-veh.is-moving .ride-bob {
	animation: ride-bob 0.32s ease-in-out infinite alternate;
}

@keyframes ride-bob {
	to {
		transform: translateY(-3px) rotate(-0.6deg);
	}
}

.ride-bob {
	position: relative;
}

.ride-art {
	display: block;
	width: 100%;
	height: auto;
	transition: transform 0.35s var(--ease);
}

.ride-art.is-flipped {
	transform: scaleX(-1);
}

/* 箱子 */
.ride-box {
	position: relative;
	width: 78px;
	height: 45px;
	flex: none;
}

.ride-box img {
	width: 100%;
	height: 100%;
	display: block;
}

.ride-box span {
	position: absolute;
	left: 6px;
	right: 6px;
	top: 52%;
	transform: translateY(-50%);
	padding: 1px 3px;
	border-radius: 4px;
	background: #fff7e8;
	color: #7a4a12;
	font-family: var(--mono);
	font-size: 10px;
	font-weight: 700;
	text-align: center;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}

.ride-stack {
	position: absolute;
	left: 18%;
	bottom: 66%;
	display: flex;
	flex-direction: column-reverse;
	align-items: center;
	transition: left 0.35s var(--ease);
}

.ride-stack.is-flipped {
	left: calc(82% - 78px);
}

.ride-stack.is-tall .ride-box span {
	font-size: 8.5px;
	padding: 0 2px;
}

.ride-stack .ride-box {
	margin-top: -4px;
}

/* 疊太高開始搖搖晃晃，箱子也縮小一點才塞得進畫面 */
.ride-stack.is-tall .ride-box {
	width: 56px;
	height: 28px;
	margin-top: -6px;

	animation: ride-wobble 1.6s ease-in-out infinite alternate;
	animation-delay: calc(var(--i) * -0.2s);
}

@keyframes ride-wobble {
	from {
		transform: translateX(calc(var(--i) * -1.2px)) rotate(calc(var(--i) * -0.5deg));
	}
	to {
		transform: translateX(calc(var(--i) * 1.2px)) rotate(calc(var(--i) * 0.5deg));
	}
}

.ride-box-enter-active {
	transition:
		opacity 0.4s var(--ease) calc(var(--i) * 90ms),
		transform 0.5s var(--spring) calc(var(--i) * 90ms);
}

.ride-box-leave-active {
	position: absolute;
	transition: opacity 0.25s;
}

.ride-box-enter-from {
	opacity: 0;
	transform: translateY(-40px);
}

.ride-box-leave-to {
	opacity: 0;
}

/* 貨車貨櫃上的標籤 */
.ride-body {
	position: absolute;
	right: 9%;
	top: 26%;
	width: 54%;
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 6px;
	padding: 6px 0;
	border-radius: 8px;
	background: var(--ink);
	color: var(--orange);
	font-family: var(--mono);
	font-size: 14px;
	font-weight: 700;
	transition: right 0.35s var(--ease);
}

.ride-body.is-flipped {
	right: 37%;
}

.ride-body-count {
	color: var(--dim);
	font-weight: 400;
}

.ride-ground {
	position: absolute;
	left: 400px;
	bottom: 58px;
	display: flex;
	gap: 8px;
	z-index: 3;
}

.ride-ground .ride-box {
	transition:
		transform 0.7s var(--ease-io) calc(var(--i) * 120ms),
		opacity 0.3s linear calc(0.45s + var(--i) * 120ms);
}

.ride-ground.is-loaded .ride-box {
	transform: translate(calc(-80px - var(--i) * 86px), -60px) scale(0.6);
	opacity: 0;
}

.ride-pop-enter-active,
.ride-pop-leave-active {
	transition:
		opacity 0.35s var(--ease),
		transform 0.45s var(--spring);
}

.ride-pop-enter-active {
	transition-delay: 0.9s;
}

.ride-pop-enter-from,
.ride-pop-leave-to {
	opacity: 0;
	transform: translateY(8px) scale(0.9);
}

.ride-status.ride-pop-enter-from,
.ride-status.ride-pop-leave-to {
	transform: translate(-50%, 8px) scale(0.9);
}
</style>
