<template>
	<h2>Task3</h2>
		<div class="task__descr">
			 Розробити компонент (з підтримкою v-model), який дозволяє вводити e-mail з домену “edu” (приклад: ivan-hopko@inv.mn.edu). Частинка «@inv.mn.edu» додається автоматично (користувач не вводить її). При заданні модифікатора check відображати червоним фоном input, якщо некоректний.
		</div>
	<div>
		<label>
			Введіть е-мейл:
			<input v-model.lazy="inputValue"	type="e-mail"
				:class="{'error': !isEmailCorrect}" placeholder="ivan-hopko@inv.mn.edu"
				:key="updateKey" ref="emailInput"
			>
		</label>
	</div>
</template>

<script>
	export default {
		name:'DomenInput',
		props: {
			modelValue: {
				type: String,
				default: ''
			},
			modelModifiers: {	default: ()=>({})	}
		},
		data() {
			return {
				updateKey: 0
			}
		},
		
		computed: {
			inputValue: {
				get(){
					return this.modelValue 
				},
				set(val){
					if (val && this.modelModifiers.addDomenAddress) {
						if (this.isDomenAddress(val)) {
							return val
						} else {
							val = val + '@inv.mn.edu';
							this.$nextTick(()=> {
								this.updateKey++;
								this.$nextTick(()=>{
									this.$refs.emailInput.focus()
								})
							})

						}
					
					};
					this.$emit('update:modelValue', val);
				}
			},
			isEmailCorrect(){
				return this.modelModifiers.check && (/[^@]*@inv\.mn\.edu$/.test(this.inputValue))
			},
		},
		methods: {
			isDomenAddress(str) {
				let regExp = /.*@inv\.mn\.edu/;
				return regExp.test(str); 
			},
			
			sanitizeEmail(str){
				return str.replace(/.*@inv\.mn\.edu.*/, '.@inv.mn.edu');
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>