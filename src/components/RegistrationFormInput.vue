<template>
	<div>
		<label 
			:for="label" 
			class="inline-flex items-center text-sm font-medium text-gray-700"
		>
			{{ label }}
			<CheckCircleIcon 
				v-if="valid" 
				class="w-4 h-4 ml-1 text-green-500" 
			/>
		</label>
		
		<input 
			:id="label" 
			:name="label"
			:value="value" 
			type="text" 
			class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" 
			:class="valid && 'border-green-500'"
			@input="handleInput"
		/>
	</div>
</template>
<script>
import { CheckCircleIcon } from '@heroicons/vue/solid'

export default {
	components: {
		CheckCircleIcon
	},
	props: {
		id: String,
		value: String,
		label: String,
		activated: Boolean,
		valid: Boolean
	},
	methods: {
		handleInput(e) {
			this.$emit('got-input', e.target.value)
		}
	}

}
</script>