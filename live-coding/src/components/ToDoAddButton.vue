<template>
	<div>
		<button @click="beginCreation" v-show="!isAdding">Ajouter un ToDo</button>
		<div v-show="isAdding">
			<button @click="cancel">X</button>
			<form @submit.prevent="create">
				<label>
					Instruction :
					<input type="text" v-model="text"/>
				</label>
				<input type="submit" value="Créer"/>
			</form>
		</div>
	</div>
</template>

<script>
	export default {
		name: "ToDoAddButton",
		data() {
			return {
				isAdding: false,
				text: "",
				id: 0
			}
		},
		methods: {
			beginCreation() {
				this.isAdding = true
			},
			cancel() {
				this.isAdding = false
				this.text = ""
			},
			create() {
				this.$emit("add", {
					instruction: this.text,
					id: this.id
				})
				this.text = ""
				this.isAdding = false
				++this.id
				return true
			}
		}
	}
</script>

<style scoped>

</style>