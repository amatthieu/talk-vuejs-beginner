<template>
	<span>
		<label>
			{{item.instruction}}
			<input type="checkbox" v-model="item.isChecked"/>
			<button @click="remove">Delete</button>
		</label>
	</span>
</template>

<script>
	export default {
		name: "ToDoItem",
		props: {
			item: Object
		},
		methods: {
			remove(event) {
				console.log(event)
				this.$emit("remove")
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>