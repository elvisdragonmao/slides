<script setup lang="ts">
// 包裹美術取自 ../img/box.svg，拆成箱體、蓋子、膠帶與標籤，才能分開做動畫
withDefaults(
	defineProps<{
		open?: boolean;
		label?: string;
		muted?: boolean;
	}>(),
	{ open: false, label: "", muted: false }
);
</script>

<template>
	<div class="parcel" :class="{ 'is-open': open, 'is-labeled': label && !open, 'is-muted': muted }">
		<svg class="parcel-art" viewBox="0 0 512 512" aria-hidden="true">
			<path class="parcel-inside" d="M.005 124.412 58.874.001h394.263l58.867 124.411z" />
			<path d="M.005 124.416h511.999V512.01H.005z" fill="#ca936c" />
			<path d="M215.703 404.406h80.593v107.593h-80.593z" fill="#764f43" />
			<path
				d="m46.265 386.756 12.988-12.988v62.022c0 4.328 3.508 7.837 7.837 7.837s7.837-3.509 7.837-7.837v-62.022l12.987 12.987a7.8 7.8 0 0 0 5.542 2.296 7.81 7.81 0 0 0 5.542-2.296 7.835 7.835 0 0 0 0-11.082l-26.365-26.366a7.837 7.837 0 0 0-11.084 0l-26.366 26.366a7.835 7.835 0 0 0 0 11.082 7.835 7.835 0 0 0 11.082.001M124.629 386.756l12.987-12.987v62.022a7.837 7.837 0 0 0 7.837 7.837 7.837 7.837 0 0 0 7.837-7.837v-62.022l12.987 12.987a7.8 7.8 0 0 0 5.542 2.296 7.81 7.81 0 0 0 5.542-2.296 7.835 7.835 0 0 0 0-11.082l-26.365-26.366a7.837 7.837 0 0 0-11.084 0l-26.365 26.366a7.837 7.837 0 0 0 11.082 11.082M171.312 455.12H41.229a7.837 7.837 0 0 0-7.837 7.837 7.837 7.837 0 0 0 7.837 7.837h130.082a7.837 7.837 0 0 0 7.837-7.837 7.836 7.836 0 0 0-7.836-7.837"
				fill="#764f43"
			/>
			<g class="parcel-stamp">
				<path d="M333.39 177.695h139.483v108.147H333.39z" fill="#f5ffff" />
				<path
					d="M443.624 220.83h-79.93c-4.329 0-7.837-3.509-7.837-7.837s3.508-7.837 7.837-7.837h79.93c4.329 0 7.837 3.509 7.837 7.837s-3.508 7.837-7.837 7.837M443.624 258.383h-79.93c-4.329 0-7.837-3.509-7.837-7.837s3.508-7.837 7.837-7.837h79.93c4.329 0 7.837 3.509 7.837 7.837s-3.508 7.837-7.837 7.837"
					fill="#764f43"
				/>
			</g>
			<path class="parcel-tape-body" d="M215.707 124.416h80.593v107.593h-80.593z" fill="#764f43" />
			<g class="parcel-lid">
				<path d="M.005 124.412 58.874.001h394.263l58.867 124.411z" fill="#e9bb91" />
				<path class="parcel-tape-lid" d="M215.708 124.412 224.975.001h62.06l9.267 124.411z" fill="#8e6459" />
			</g>
		</svg>
		<div class="parcel-label">{{ label }}</div>
	</div>
</template>

<style scoped>
.parcel {
	position: relative;
	width: 100%;
	aspect-ratio: 1;
	container-type: inline-size;
}

.parcel-art {
	position: absolute;
	inset: 0;
	width: 100%;
	height: 100%;
	overflow: visible;
	transition: filter 0.4s;
}

.parcel-inside {
	fill: #7d5139;
}

.parcel-lid,
.parcel-tape-lid,
.parcel-tape-body {
	transform-box: fill-box;
}

.parcel-lid {
	transform-origin: 50% 100%;
	transition: transform 0.55s var(--ease-io, ease);
}

.parcel-tape-lid,
.parcel-tape-body {
	transform-origin: 50% 0;
	transition: transform 0.3s var(--ease, ease) 0.4s;
}

.parcel-tape-body {
	transition-delay: 0.58s;
}

.parcel-stamp {
	transition: opacity 0.3s;
}

.parcel-label {
	position: absolute;
	left: 7%;
	right: 7%;
	top: 49%;
	padding: 0.35em 0.4em;
	border-radius: 0.25em;
	background: #f5ffff;
	color: #764f43;
	font-family: var(--mono, ui-monospace, monospace);
	font-size: 8.4cqw;
	font-weight: 700;
	line-height: 1.2;
	text-align: center;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	box-shadow: 0 0.12em 0 rgb(0 0 0 / 0.18);
	opacity: 0;
	transform: translateY(12%) rotate(-6deg) scale(0.8);
	transition:
		opacity 0.3s var(--ease, ease) 0.72s,
		transform 0.5s var(--spring, ease) 0.72s;
}

/* 打開：蓋子掀起、膠帶割開 */
.is-open .parcel-lid {
	transform: translate(-18px, -138px) rotate(-8deg);
}

.is-open .parcel-tape-lid,
.is-open .parcel-tape-body {
	transform: scaleY(0);
	transition-duration: 0.15s;
	transition-delay: 0s;
}

.is-open .parcel-label {
	transition-delay: 0s;
}

/* 封箱後貼上 Commit Message */
.is-labeled .parcel-stamp {
	opacity: 0;
}

.is-labeled .parcel-label {
	opacity: 1;
	transform: rotate(-3deg);
}

.is-muted .parcel-art {
	filter: saturate(0.5) brightness(0.78);
}
</style>
