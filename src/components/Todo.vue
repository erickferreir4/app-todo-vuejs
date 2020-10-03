<template>

	<div class="todo">
		<form v-on:submit.prevent="addTask">
			<label v-on:click="toggleCompleted" v-bind:class="{ active : completedAll && completedActive }">❯</label>
			<input type="text" v-model="newTask" placeholder="What needs to be done?" />
		</form>

		<ul>
			<li v-for="(todo, index) in listTodos" :key="index" v-bind:id="index" v-bind:class="{ completed : todo.completed }">
				<button  v-on:click="completed(index)">isActive</button>
				{{ todo.todo }}
				<button v-on:click="deleteTodo(index)">+</button>
			</li>
		</ul>


		<div class="footer">
			<span>{{ todosLength }}</span>
			<div class="footer-filter">
				<button v-on:click="filter('all')" v-bind:class="{ active : filterAll }">All</button>
				<button v-on:click="filter('active')" v-bind:class="{ active : filterActive }">Active</button>
				<button v-on:click="filter('completed')" v-bind:class="{ active : filterCompleted }">Completed</button>
			</div>

			<button v-on:click="clearCompleted">Clear completed</button>
		</div>

	</div>

</template>




<script>

const getLS = ( ) => {
	let todos = JSON.parse(localStorage.getItem('todos') || '[]');
	return todos;
}

const updateLS = todos => {
	localStorage.setItem('todos', JSON.stringify(todos));
}


export default {
	name: 'Todo',
	data: function() {
		return {
			newTask: '',
			listTodos: getLS(),
			completedAll: false,
			completedActive: false,
			filterAll: false,
			filterActive: false,
			filterCompleted: false

		}
	},
	methods: {
		addTask: function() {
			let todo = {
				'todo': this.newTask,
				'completed': false
			}

			this.listTodos.push(todo);
			this.newTask = ''
			updateLS(this.listTodos);
		},
		deleteTodo: function(index) {
			this.listTodos.splice(index, 1);
			updateLS(this.listTodos);
		},

		filter: function(type) {
			if ( type === 'all' ) {
				this.listTodos = getLS();
				this.filterAll = true
				this.filterCompleted = false 
				this.filterActive = false 
			}
			else if ( type === 'active' ) {
				this.listTodos = getLS().filter( value => !value.completed );
				this.filterActive = true
				this.filterAll = false 
				this.filterCompleted = false 
			}
			else {
				this.listTodos = getLS().filter( value => value.completed );
				this.filterCompleted = true
				this.filterActive = false 
				this.filterAll = false 
			}
		},

		completed: function(index) {
			this.listTodos[index].completed = !this.listTodos[index].completed
			updateLS(this.listTodos);

			this.completedActive = false
		},
		toggleCompleted: function() {
			if ( !this.completedActive ) {
				this.completedAll = false	
			}
			this.listTodos.map( value => {
				value.completed = !this.completedAll;
			})
			this.completedAll = !this.completedAll;
			this.completedActive = true
			updateLS(this.listTodos);
		},
		clearCompleted: function() {
			this.listTodos = this.listTodos.filter( value => !value.completed )
			updateLS(this.listTodos);
		}
	},
	computed: {
		todosLength: function() {
			return this.listTodos.length + ' items left';		
		}
	},
}

</script>



<style>
.todo {
	min-width: 230px;
	max-width: 550px;
	margin: 0 auto;
	background: #fff;
	box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}

.todo form {
    display: flex;
    align-items: center;
	box-shadow: inset 0 -2px 1px rgba(0,0,0,0.03);
}

.todo form label {
	font-size: 22px;
	color: #e6e6e6;
	padding: 10px 27px 10px 27px;
	transform: rotate(90deg);
	cursor: pointer;
}

.todo form label.active {
	color: #737373;
}

.todo form input {
	width: 100%;
	padding: 16px 0;
	border: none;
	background: rgba(0, 0, 0, 0.003);
	font-size: 24px;
	color: #4d4d4d;
}

.todo form input::placeholder {
	color: #ededed
}

.todo ul li {
	padding: 15px 0;
	display: flex;
    align-items: center;
	position: relative;
	border-bottom: 1px solid #ededed;
	font-size: 24px;
}

.todo ul li.completed {
	color: #d9d9d9;
	text-decoration: line-through;
}
.todo ul li.completed button:first-of-type:before{
	content: '\2713';
    display: inline-block;
    color: #008000cc;
    font-size: 20px;
}

.todo ul li:hover button:last-of-type {
	opacity: 1;
}

.todo ul li button {
	cursor: pointer;
	background: #fff;
}

.todo ul li button:first-of-type {
	margin-right: 30px;
	margin-left: 15px;
	font-size: 0;
	height: 30px;
	width: 30px;
	border-radius: 100%;
	border: 1px solid #ededed;
}

.todo ul li button:last-of-type {
	position: absolute;
	right: 20px;
    border: none;
    transform: rotate(45deg);
    font-size: 30px;
    color: #cc9a9a;
	opacity: 0;
}

.todo .footer {
	display: flex;
 	justify-content: space-between;
	align-items: center;
	color: #777;
	padding: 10px 0;
	height: 30px;
}

.todo .footer span{
    margin-left: 15px;
}

.todo .footer > button{
    margin-right: 15px;
}

.todo .footer > button:hover{
	text-decoration: underline;
}

.todo .footer .footer-filter button, .todo .footer > button {
	color: #777;
	background: none;
    border: none;
	cursor: pointer;
}
.todo .footer .footer-filter button {
    margin: 3px;
    padding: 3px 7px;
}

.todo .footer .footer-filter button:hover {
	border: 1px solid rgba(175, 47, 47, 0.2);
}

.todo .footer .footer-filter button.active {
	border: 1px solid rgba(175, 47, 47, 0.2);
}

</style>



