<template>
	<div>
		<button 
			type="submit" 
			:disabled="disabled" 
			class="group relative overflow-hidden w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md transition duration-200 bg-indigo-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
			:class="buttonClasses"
		>
			<div 
				class="bg-progress bg-indigo-600 absolute top-0 left-0 w-0 h-full transition-all duration-500 ease"
				:style="{'width': formProgress + '%'}"
			></div>
			<span class="absolute left-0 inset-y-0 flex items-center pl-3">
				<LockClosedIcon v-if="disabled" class="h-5 w-5 text-indigo-500 transform group-hover:scale-110 transition duration-100" aria-hidden="true" />
				<CheckIcon v-if="!disabled" class="h-5 w-5 text-indigo-200 transform group-hover:scale-110 transition duration-100" aria-hidden="true" />
			</span>
			<span v-if="formProgress === 0"
				class="text-indigo-600 z-10"
			> Please, fill the form </span>
			<span v-else-if="formProgress === 100"
				class="text-indigo-200 z-10"
			> Register </span> 
			<span v-else
				class="text-indigo-200 z-10"
			> Keep going </span> 
		</button>
	</div>
</template>

<script>
import { LockClosedIcon } from '@heroicons/vue/solid';
import { CheckIcon } from '@heroicons/vue/solid';


export default {
	components: {
		LockClosedIcon,
		CheckIcon
	},
	props: {
		disabled: Boolean,
		formProgress: Number,
	},
	computed: {
		buttonClasses() {
			return {
				'opacity-80 cursor-not-allowed': this.disabled,
				'bg-indigo-700 transform hover:scale-95': !this.disabled
			}
		}
	}
}
</script>