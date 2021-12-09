<template>
	<div class="main">
		<img class="logo" src="./assets/pokemon-logo.jpg" alt="Pokemon">
		<h1>PokeGuía</h1>
		<Search @search-pkmn="handleSearch"></Search>

		<div v-if="show" class="datos">
			<img :src="sprite">

			<Moves :data="moves"></Moves>
			<Abilities :data="abilities"></Abilities>	
		</div>
		<p v-else class="error">Pokémon no encontrado</p>
	</div>
</template>

<script>
import axios from 'axios'
import { ref, computed, reactive, onMounted } from "vue"
import Search from './components/Search.vue'
import Moves from './components/Moves.vue'
import Abilities from './components/Abilities.vue'
export default {
	components: { Search, Moves, Abilities },
	setup() {
		// Variables
		const show = ref(true)
		const name = ref("pikachu")
		const pkmn = reactive({
			sprite: '',
			moves: [],
			abilities: []
		})

		// Computed
		const sprite = computed(()=> {
			return pkmn.sprite
		})

		const moves = computed(()=> {
			return pkmn.moves
		})

		const abilities = computed(()=> {
			return pkmn.abilities
		})

		// Watch
		// watch(show, (curr, prev)=> {
		// 	//...
		// })


		// Methods
		const handleSearch = (e)=> {
			name.value = e
			getData()
		}

		const getData = ()=> {
			if(!name.value) return

			axios
				.get(`https://pokeapi.co/api/v2/pokemon/${name.value}`)
				.then( response => {
					show.value = true

					pkmn.sprite = response.data.sprites.front_shiny
					pkmn.moves = response.data.moves
					pkmn.abilities = response.data.abilities
				})
				.catch(error => {
					console.log("ERROR", error)
					show.value = false
				})
		}

		// Hooks
		onMounted(()=> getData())


		return {
			show,
			name,
			pkmn,
			sprite,
			moves,
			abilities,
			handleSearch
		}
	}
}
</script>

<style>
.main {
	font-family: Arial, Helvetica, sans-serif;
	text-align: center;
	color: #2c3e50;
	margin-top: 3rem;
}

.logo {
	width: 300px;
}

input {
	margin: 0 0.5rem;
	padding: 0.25rem 0.5rem;
}

button {
	padding: 0.25rem 1rem;
	cursor: pointer;
}

.datos {
	margin-top: 3rem;
}

img {
	width: 150px;
}

ul {
  list-style: none;
  padding: 0;
  margin-bottom: 3rem;
}

li {
	margin-bottom: 0.25rem;
}

.error {
  margin-top: 4rem;
  font-weight: bold;
}
</style>
