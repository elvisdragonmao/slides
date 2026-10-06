<script setup lang="ts">
import { ref } from "vue";

// 專案成品示範：跟投影片上的程式碼做一樣的事
const API = "https://open.er-api.com/v6/latest/TWD";

const amount = ref(1000);
const currency = ref("USD");
const result = ref("—");
const loading = ref(false);

async function convert() {
	loading.value = true;
	try {
		const response = await fetch(API);
		const data = await response.json();
		const rate = data.rates[currency.value];
		const money = amount.value * rate;
		result.value = `${money.toFixed(2)} ${currency.value}`;
	} catch {
		result.value = "匯率抓不到，等一下再試";
	}
	loading.value = false;
}
</script>

<template>
	<div class="cd">
		<main class="cd-card">
			<h1>💱 匯率計算機</h1>
			<input v-model.number="amount" type="number" />
			<span>新台幣 TWD 換成</span>
			<select v-model="currency">
				<option value="USD">美金 USD</option>
				<option value="JPY">日圓 JPY</option>
				<option value="KRW">韓元 KRW</option>
				<option value="EUR">歐元 EUR</option>
			</select>
			<button :disabled="loading" @click="convert">{{ loading ? "換算中…" : "換算" }}</button>
			<p class="cd-result">{{ result }}</p>
		</main>
	</div>
</template>

<style scoped>
.cd {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 360px;
	border-radius: 16px;
	background: linear-gradient(135deg, #d9f99d, #bae6fd);
	font-family: system-ui, sans-serif;
}

.cd-card {
	width: 280px;
	padding: 20px;
	border-radius: 20px;
	background: #fff;
	box-shadow: 0 12px 30px -12px rgb(0 0 0 / 0.3);
	display: flex;
	flex-direction: column;
	gap: 8px;
	text-align: center;
	color: #222;
}

/* 主題會把 h1 放大成封面標題，這裡要壓回來 */
.cd-card h1 {
	margin: 0 0 4px !important;
	font-size: 22px !important;
	line-height: 1.3 !important;
	color: #222 !important;
}

.cd-card span {
	font-size: 14px;
	color: #666;
}

.cd-card input,
.cd-card select,
.cd-card button {
	font-size: 15px;
	padding: 7px 10px;
	border-radius: 10px;
	border: 1px solid #ccc;
	background: #fff;
	color: #222;
}

.cd-card button {
	border: none;
	background: #0ea5e9;
	color: #fff;
	font-weight: 700;
	cursor: pointer;
	transition: transform 0.2s;
}

.cd-card button:hover {
	transform: scale(1.05);
}

.cd-result {
	margin: 0;
	font-size: 24px;
	font-weight: 800;
	color: #0f172a;
}
</style>
