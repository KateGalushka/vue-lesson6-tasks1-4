<template>
	<h2>Task2</h2>
		<div class="task__descr">
			 Розробити компонент (з підтримкою v-model), який дозволяє вводити шлях до файлу js (URL, що закінчується розширенням js). При заданні модифікатора checkPath відображати червоним фоном input, якщо шлях некоректний.
		</div>
	<div>
		<label>
			Введіть шлях (URL) до файлу .js (типу http://****.js):
			<input
			v-model="urlInputValue"
			type="string" 
			:class="{'error': !isSucces }">
		</label>
	</div>
</template>

<script>
	export default {
		name: 'UrlInput',
		props: {
			modelValue: {
				type: String,
				default: ''
			},
			modelModifiers: { default: ()=>({})}
		},
		
		computed: {
			urlInputValue: {
				get(){
					return this.modelValue;
				},
				set(val){
					if (this.modelModifiers.checkPath && val) {
						this.getUrlTested(val)
					};
					this.$emit('update:modelValue', val);
				}
			},
			isSucces(){
				return this.getUrlTested(this.urlInputValue)
			},
		},
		methods: {
			getUrlTested(val) {
				const regExp = /https?:\/\/[^\s/$.?#].[^\s]*\.js\b/i;
				return regExp.test(val);
			}
		}
		
	}
</script>

<style lang="scss" scoped>

</style>