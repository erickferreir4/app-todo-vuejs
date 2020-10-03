<template>
	<h1>{{ title }}</h1>
</template>

<script>
export default {
  name: 'TodoTitle',
  props: {
  	title: {
		type: String,
		required: true
	}
  },
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1 {
	font-size: 100px;
    color: rgba(175, 47, 47, 0.15);
    font-weight: 100;
    text-align: center;
}


</style>
