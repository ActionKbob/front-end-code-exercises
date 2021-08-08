<template>
	<div class="container">
		<div class="section">
			<div v-if="error">
				I'm sorry, there was a error returning your request.
			</div>
			<div v-else-if="pokedex" class="columns is-flex is-flex-column-mobile is-justify-content-space-between">
				<div class="column is-two-thirds-widescreen mb-5">
					<div class="mb-6">
						<h1 class="is-size-3 has-text-weight-bolder mb-5">Abilities</h1>
						<Ability v-for="ability in pokedex.abilities" :ability="ability.ability" :key="ability.ability.name" />
					</div>
					<div>
						<h1 class="is-size-3 has-text-weight-bolder mb-5">Stats</h1>
						<div class="columns is-flex-wrap-wrap">
							<Stat v-for="(stat, index) in pokedex.stats" :stat="stat" :key="index" />
						</div>
					</div>
				</div>
				<div class="column box is-one-quarter-widescreen order-negative-one-mobile mb-5">
					<Sidebar :pokedex="pokedex"/>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios';

import Sidebar from '../../../components/pokemon-detail/sidebar';
import Ability from '../../../components/pokemon-detail/ability';
import Stat from '../../../components/pokemon-detail/stat';

const apiURI = 'https://pokeapi.co/api/v2';

export default {
	data(){
		return {
			error : false,
			pokedex : undefined
		};
	},

	components : {
		Sidebar,
		Ability,
		Stat
	},

	async created(){
		const requestConfig = {
			headers : {
				'Accept' : 'application/json'
			}
		}

		try
		{
			const response = await axios.get( `${ apiURI }/pokemon/${ this.$route.params.id }`, requestConfig );
			this.pokedex = response.data;
			console.log(this.pokedex)
		}
		catch( error )
		{
			this.error = true;
		}
	}
}
</script>