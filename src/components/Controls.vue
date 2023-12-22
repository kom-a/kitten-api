<script setup lang="ts">

import { ref } from "vue";
import axios from "axios";

let href = ref("");

const getImage = async () => {
	const { data } = await axios('https://api.thecatapi.com/v1/images/search');
	if (data.length < 0)
		return;

	href.value = data[0].url;

	console.log(href);
}

</script>

<template>
	<button v-on:click="getImage">Get image</button>
	<input type="number" id="limit" name="limit" min="1" max="25" />
</template>

<style scoped>
h1 {
	font-weight: 500;
	font-size: 2.6rem;
	position: relative;
	top: -10px;
}

h3 {
	font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
	text-align: center;
}

@media (min-width: 1024px) {

	.greetings h1,
	.greetings h3 {
		text-align: left;
	}
}
</style>
