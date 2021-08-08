<template>
	<div class="columns">
		<PokemonCard v-for="pokemon in pokemonList" :key="pokemon" :name="pokemon"/>
	</div>
</template>

<script>
import PokemonCard from '../pokemon-card';

export default {
	data(){
		return {
			pokemonList : [ 'charmander', 'bulbasaur', 'squirtle' ]
		}
	}
}
</script>