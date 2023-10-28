<template>
	<h2>Task4</h2>
	<div class="task__descr">
		Розробити компонент для вводу віку користувача та імені. Робити форматування при заданні відповідних модифікаторів
		відповідних полів input:
		ім’я користувача - у випадку порожнього поля (червони фон)
		вік (вік менший за 18 – колір фону червоний, інакше – зелений).
	</div>
	<div>
		<label>
			Введіть ім'я:
			<input type="text" v-model="userNameValue" :class="{'error': isInputEmpty}">
		</label>
		<label>
			Введіть вік:
			<input type="text" v-model="userAgeValue" :class="testAgeColor">
		</label>

	</div>
</template>

<script>
export default {
	name: 'UserNameAgeInput',
	props: {
		userName4: {
			type: String,
			default:''
			},
		userAge4: {
			type: String,
			default: null
		},
		userName4Modifiers:{ default: ()=>({}) },
		userAge4Modifiers:{ default: ()=>({}) }
	},
	
	computed: {
		userNameValue:{
			get(){
				return this.userName4 
			},
			set(val){
				this.$emit('update:userName4', val);
			}
		},
		userAgeValue:{
			get(){
				return this.userAge4
			},
			set(val){
				this.$emit('update:userAge4', val)
			}
		},
		isInputEmpty(){
			return (this.userName4Modifiers.checkEmpty && !this.userNameValue)? true: false
		},
		testAgeColor(){
			if (this.userAge4Modifiers.checkAge && this.userAgeValue) {
				 return (this.userAgeValue<18)? 'error' : 'green'
				}
			else return ''
		}
	}

}
</script>

<style lang="scss" scoped>
.green {
	background-color: green;
}
</style>