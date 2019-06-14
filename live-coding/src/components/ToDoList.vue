<template>
	<div>
		<to-do-add-button @add="add"></to-do-add-button>
		<transition-group name="list" tag="p">
			<to-do-item :item="item" v-for="item in list" @remove="remove(item)" :key="item.id" class="item"></to-do-item>
		</transition-group>
		{{toDoCount}}/{{totalCount}}
	</div>
</template>

<script>
	import ToDoItem from './ToDoItem'
	import ToDoAddButton from './ToDoAddButton'

	export default {
		name: "ToDoList",
		components: {ToDoAddButton, ToDoItem},
		data() {
			return {
				list: []
			}
		},
		computed: {
			toDoCount() {
				return this.list.filter(item => !item.isChecked).length
			},
			totalCount() {
				return this.list.length
			}
		},
		methods: {
			add({instruction, id}) {
				this.list.push({
					instruction,
					isChecked: false,
					id
				})
			},
			remove(item) {
				this.list.splice(this.list.indexOf(item), 1)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.item {
		transition: all 1s;
		display: inline-block;
		margin-right: 10px;
	}
	.list-leave-active {
		position: absolute;
	}
	.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
		opacity: 0;
		transform: translateY(30px);
	}
</style>