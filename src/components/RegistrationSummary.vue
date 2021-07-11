<template>
	<div class="bg-gray-100 pt-12 w-screen h-screen">
		<div class="bg-white max-w-4xl  mx-auto shadow overflow-hidden sm:rounded-lg">
			<div class="px-4 py-5 sm:px-6">
			<h3 class="text-lg leading-6 font-medium text-gray-900">
				Registration Information
			</h3>
			<p class="mt-1 max-w-2xl text-sm text-gray-500">
				Personal details and application.
			</p>
			</div>
			<div class="border-t border-gray-200">
			<dl>
				<div v-for="field in data" :key="field.label" class="bg-white px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
				<dt class="text-sm font-medium text-gray-500">
					{{ field.label }}
				</dt>
				<dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
					{{ field.value }}
				</dd>
				</div>
			</dl>
			</div>
		</div>
	</div>
</template>

<script>

import { TransitionChild, TransitionRoot } from '@headlessui/vue'


export default {
	props: {
		data: Array
	}

}
</script>