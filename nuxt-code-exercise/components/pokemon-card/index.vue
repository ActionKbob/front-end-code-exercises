
<template>
	<div class="column is-one-third-widescreen">
		<div v-if="error">
			I'm sorry, there was a error returning your request.
		</div>
		<div v-else-if="pokedex" class="pokemon-card card">
			<div class="card-image">
				<figure class="image is-4by3" :style="{'background-image':`url( ${pokedex.sprites.other['official-artwork'].front_default}`}"></figure>
			</div>
			<div class="card-content">
				<h3 class="is-capitalized has-text-weight-bolder is-size-4 pb-3">{{ pokedex.name }}</h3>

				<div class="stats mb-5">

					<AbilityList :abilities="pokedex.abilities"/>

					<TypesList :types="pokedex.types"/>

					<div v-for="( stat, index ) in pokedex.stats.slice(0, 3)" :key="index" class="">
						<strong :class="[stat.stat.name.length === 2 ? 'is-uppercase' : 'is-capitalized']">{{ stat.stat.name }}:</strong>
						<span>{{ stat.base_stat }}</span>
					</div>
				</div>

				<nuxt-link :to="`/pokemon/${ pokedex.name }`">
					<b-button type="is-primary" outlined rounded>Learn more</b-button>
				</nuxt-link>
			</div>
		</div>
	</div>
</template>


<script>
import AbilityList from './lists/abilities';
import TypesList from './lists/types';
import axios from 'axios';

const apiURI = 'https://pokeapi.co/api/v2';

export default {
	props : [ 'name' ],

	components : {
		AbilityList,
		TypesList
	},

	data(){
		return {
			error : false,
			pokedex : undefined
		};
	},

	async created(){
		const requestConfig = {
			headers : {
				'Accept' : 'application/json'
			}
		}

		try
		{
			const response = await axios.get( `${ apiURI }/pokemon/${ this.name }`, requestConfig );
			this.pokedex = response.data;
		}
		catch( error )
		{
			this.error = true;
		}
	}
}
</script>