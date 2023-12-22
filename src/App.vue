<script setup lang="ts">

import { ref } from "vue";
import axios from "axios";

let hrefs = ref(['']);
const request = 'https://api.thecatapi.com/v1/images/search';

const getCats = async (req: string) => {
	console.log(req);
	const { data } = await axios(req);
	if (data.length < 0)
		return;

	hrefs.value = [];

	console.log(data);

	hrefs.value = data.map((el: any) => {
		return el.url
	});

	console.log(hrefs.value);
}

const getSingleCat = async () => {
	getCats(request);
}

const getTenCats = () => {
	getCats(request + `?limit=10`);
}

getSingleCat();

</script>

<template>
	<header>
		<button v-on:click="getSingleCat" class="button-92">Get cat</button>
		<button v-on:click="getTenCats" class="button-92">Get 10 cats</button>
	</header>

	<main>
		<img class="cat-image" v-for="href in hrefs" :src="href" />
	</main>
</template>

<style scoped>

main {
	display: flex;
	flex-direction: column;
}

.button-92 {
  --c: #fff;
  /* text color */
  background: linear-gradient(90deg, #0000 33%, #fff5, #0000 67%) var(--_p,100%)/300% no-repeat,
    #004dff;
  /* background color */
  color: #0000;
  border: none;
  transform: perspective(500px) rotateY(calc(20deg*var(--_i,-1)));
  text-shadow: calc(var(--_i,-1)* 0.08em) -.01em 0   var(--c),
    calc(var(--_i,-1)*-0.08em)  .01em 2px #0004;
  outline-offset: .1em;
  transition: 0.3s;
}

.button-92:hover,
.button-92:focus-visible {
  --_p: 0%;
  --_i: 1;
}

.button-92:active {
  text-shadow: none;
  color: var(--c);
  box-shadow: inset 0 0 9e9q #0005;
  transition: 0s;
}

.button-92 {
  font-weight: bold;
  font-size: 2rem;
  margin: 10px;
  cursor: pointer;
  padding: .1em .3em;
}

.cat-image {
	max-width: 50vw;
	margin: 10px;
	border-radius: 30px;
}

</style>
