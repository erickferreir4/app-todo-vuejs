<template>
  <div id="app">

	<TodoView>

		<template v-slot:title>
			<TodoTitle title="todos"></TodoTitle>
		</template>

		<template v-slot:todo>
			<Todo></Todo>
		</template>

	</TodoView>
	
  </div>
</template>





<script>
import TodoView from './components/TodoView.vue'
import TodoTitle from './components/TodoTitle.vue'
import Todo from './components/Todo.vue'



export default {
  name: 'App',
  components: {
  	TodoTitle,
	TodoView,
	Todo,
  },
}
</script>





<style>
body {
	background: #f5f5f5;
	background: black;
}

button, input, select, textarea {
	outline: none;
}

ul {
	list-style: none;
	padding: 0;
	margin: 0;
}
#app {
	font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
	line-height: 1.4em;
	color: #4d4d4d;
	font-weight: 300;
}
</style>
