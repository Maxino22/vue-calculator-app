<template>
	<div
		class="p-3"
		style="max-width: 400px; margin: 50px auto; background: #234"
	>
		<!-- calculator results -->
		<div
			class="w-full rounded m-1 p-3 text-sm-right lead font-weight-bold text-white bg-vue-dark"
		>
			{{ calculatorValue || 0 }}
		</div>
		<!-- calculator buttons -->
		<div class="row gx-0">
			<div class="col-3" v-for="i in calculatorElements" :key="i">
				<div
					class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
					:class="{
						'bg-vue-green': ['C', '*', '%', '/', '-', '+', '='].includes(i),
					}"
					@click="action(i)"
				>
					{{ i }}
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue'

const calculatorValue = ref('')
const previousCalculatorValue = ref('')

const operator = ref(null)
const calculatorElements = ref([
	'C',
	'*',
	'/',
	'-',
	7,
	8,
	9,
	'+',
	4,
	5,
	6,
	'%',
	1,
	2,
	3,
	'=',
	'0',
	'.',
])
function action(n) {
	// apppend value
	if (!isNaN(n) || n === '.') {
		calculatorValue.value += n + ''
	}
	// clear value
	if (n === 'C') {
		calculatorValue.value = ''
	}
	// percentage
	if (n === '%') {
		calculatorValue.value = calculatorValue.value / 100
	}

	if (['/', '*', '-', '+'].includes(n)) {
		operator.value = n
		previousCalculatorValue.value = calculatorValue.value
		calculatorValue.value = ''
	}
	if (n === '=') {
		calculatorValue.value = eval(
			previousCalculatorValue.value + operator.value + calculatorValue.value
		)
		previousCalculatorValue.value = ''
		operator.value = null
	}
}
</script>

<style>
.bg-vue-dark {
	background-color: #31475e;
}
.bg-vue-green {
	background-color: #3fb984;
	text-decoration: dashed;
}
.hover-class:hover {
	cursor: pointer;
	background-color: #3d5875;
}
</style>
