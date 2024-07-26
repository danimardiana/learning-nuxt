<script setup lang="ts">
	const id = ref(null)

	const { data, status } = useLazyFetch(() => `https://reqres.in/api/users/${id.value}`,{
		immediate: false
	})

	const pending = computed(() => status.value === 'pending')
</script>

<template>
	<div>
		<input type="number" v-model="id" :disabled="pending" min="1">

		<div v-if="status === 'idle'">
			Type an User ID
		</div>

		<div v-else-if="status === 'pending'">
			Loading ...
		</div>
		
		<div v-else-if="status === 'error'">
			Error data
		</div>

		<div v-else>
			<pre>
				{{ data }}
			</pre>
		</div>
	</div>
</template>