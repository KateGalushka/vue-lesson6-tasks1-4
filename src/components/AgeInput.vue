<template>
	<h2>Task1</h2>
	<div class="task__descr">
		Розробити компонент для введення віку користувача (з підтримкою v-model). При заданні модифікатора check не допускати введення некоректного віку (вік не може бути більшим за 150). При заданні модифікатора setColor задавати фон (вік менше 10 – зелений, від 10 до 21 – жовтий, інакше – оранжевий). 
	</div>
	<div>
		<label>
			Введіть вік:
			<input type="number" v-model="ageValue" 
			:class="{
				[ageClass] : isModified
			}">
		</label>
		<div class="warning" v-if="showWarning">Вік не може бути більше 150</div>
	</div>
</template>

<script>
	export default {
		name:'AgeInput',
		props: {
			modelValue: {
				type: Number,
			},
			modelModifiers:{ default: ()=>({})}
		},
		data() {
			return {
				showWarning: false,
			}
		},
		computed: {
			ageValue: {
				get(){
					return this.modelValue; 
				},
				set(val){
					this.checkHighest(val);
					this.$emit('update:modelValue', val)
				}
			},
			isModified(){
				return this.ageValue && this.modelModifiers.setColor;
			},
			ageClass(){
				return (this.ageValue < 10) ? 'low' : (this.ageValue < 21) ? 'medium' : 'high';
			}
		},
		methods: {
			checkHighest(val) {
				if (this.modelModifiers.check && val) {
						(val>150)? this.showWarning = true : this.showWarning = false;
					}
			},
		},
	}
</script>

<style lang="scss" scoped>
.low {
	background-color: green;
}
.medium{
	background-color: yellow;
}
.high{
	background-color: orange;
}

</style>