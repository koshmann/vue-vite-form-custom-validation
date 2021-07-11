<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-50 py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-md w-full space-y-8">
      <div>
        <h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900">Register an account</h2>
        <p class="mt-2 text-center text-sm text-gray-600">just for testing</p>
      </div>
      <form class="mt-8 space-y-4" action="#" method="POST" @submit.prevent="showModal=true">

		<registration-form-input
			v-for="field,i in fields"
			:key="field.label" 
			:label="field.label"
			:value="field.value"
			:valid="field.valid"
			:activated="field.activated"
			@got-input="onInput(i, $event)"
		/>

		<registration-form-progress 
			:disabled="!everyFieldValid"
			:formProgress="formProgress" 
		/>
		
	  </form>
    </div>
	<ConfirmationModal 
		:open="showModal" 
		@registration-cancelled="showModal=false" 
		@registration-confirmed="handleRegistration" 
	/>
  </div>
</template>

<script>
import RegistrationFormInput from './RegistrationFormInput.vue';
import RegistrationFormProgress from './RegistrationFormProgress.vue';
import ConfirmationModal from './ConfirmationModal.vue'

export default {
  components: {
	RegistrationFormInput,
	RegistrationFormProgress,
	ConfirmationModal
  },
  props: {
	  fields: Array
  },
  data() {
		return {
			showModal: false,
		}
	},
	computed: {
		everyFieldValid() {
			return this.fields.every( field => field.valid );
		},
		formProgress() {
			let validFields = 0;
			this.fields.forEach( field => {
				field.valid && validFields++
			});
			let percentProgress = ( validFields / this.fields.length ) * 100;

			return percentProgress
		}
	},
	methods: {
		onInput(i, val){
			let fieldInfo = {
				fieldIndex: i,
				fieldValue: val.trim(),
				fieldActivated: true
			}
			this.$emit('field-changed', fieldInfo)
		},
		handleRegistration() {
			this.$emit('user-registration');
		}
	},
	
}
</script>