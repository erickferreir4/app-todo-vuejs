<template>

	<div class="content">
		<slot name="title"></slot>

		<slot name="todo"></slot>
	</div>

</template>



<script>

export default {
	name: 'TodoView',
}

</script>
