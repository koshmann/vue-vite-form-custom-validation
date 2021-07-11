<template>

    <transition
      enter-active-class="transition-opacity ease duration-500"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition-opacity ease duration-500"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
		<RegistrationForm
			v-if="!formSent"
			:fields="fields" 
			@user-registration="handleRegistration" 
			@field-changed="handleFieldsChanges"
		/>

		<RegistrationSummary
			v-else-if="formSent"
			:data="fields"
		/>

    </transition>


</template>

<script>
import RegistrationForm from './components/RegistrationForm.vue';
import RegistrationSummary from './components/RegistrationSummary.vue';
import { TransitionChild, TransitionRoot } from '@headlessui/vue'

export default {

	components: {
		RegistrationForm,
		RegistrationSummary,
		TransitionChild, 
		TransitionRoot
	},
	data() {
		return {
			formSent: false,
			fields: getFields()
		}
	},
	methods: {
		handleRegistration(){
			this.formSent = true
		},
		handleFieldsChanges(fieldNewData) {
			let changedField = this.fields[fieldNewData.fieldIndex];

			changedField.value = fieldNewData.fieldValue;
			changedField.activated = fieldNewData.fieldActivated;
			changedField.valid = changedField.pattern.test(changedField.value);
		}
	},
	created(){
		this.fields.forEach(field => {
			field.valid = false;
			field.activated = false;
		})
	}
	
}

function getFields(){
	return (
		[
			{
				label: 'Name',
				value: '',
				pattern: /^[a-zA-Z ]{2,30}$/
			},
			{
				label: 'Phone',
				value: '',
				pattern: /^[0-9]{7,14}$/
			},
			{
				label: 'Email',
				value: '',
				pattern: /.+/
			},
			{
				label: 'Some Field 1',
				value: '',
				pattern: /.+/
			},
			{
				label: 'Some Field 2',
				value: '',
				pattern: /.+/
			}
		]
	)
}

</script>
