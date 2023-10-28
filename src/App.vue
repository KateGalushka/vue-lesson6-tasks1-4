<template>
	<div>
		<age-input v-model.check.setColor="userAge"/>
		<div class="testing"> Для перевірки userAge: {{ userAge }}</div>
		<hr>

		<url-input v-model.checkPath="urlValue"/>
		<div class="testing"> Для перевірки urlValue: {{ urlValue }}</div>
		<hr>

		<domen-input v-model.addDomenAddress.check="emailValue"/>
		<div class="testing"> Для перевірки emailValue: {{ emailValue }}</div>
		<hr>
		
		<user-name-age-input
			v-model:userName4.checkEmpty="userNameTask4"
			v-model:userAge4.checkAge="userAgeTask4"
		/>
		<div>Для перевірки: userNameTask4- {{ userNameTask4 }} userAgeTask4- {{ userAgeTask4 }}</div>
	</div>
</template>

<script>
import AgeInput from './components/AgeInput.vue';
import DomenInput from './components/DomenInput.vue';
import UrlInput from './components/UrlInput.vue';
import UserNameAgeInput from './components/UserNameAgeInput.vue';

export default {
  name: "App",
  components: {
    AgeInput,
    UrlInput,
    DomenInput,
    UserNameAgeInput
},
  data() {
	return {
		userAge: null,
		urlValue: null,
		emailValue: null,
		userNameTask4: null,
		userAgeTask4: null
	}
  },
};
</script>

<style lang="scss">
.task__descr{
	font-style: italic;
	margin-bottom: 30px;
}
.testing{
	margin-bottom: 30px;
	font-style: italic;
}
.warning{
	color: red;
}
.error{
	background-color: rgb(237, 162, 162);
}


</style>
