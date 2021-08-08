<template>
	<div class="box">
		<h1 class="is-size-4 is-capitalized has-text-weight-bold mb-3">
			{{ ability.name.replace( "-", " " ) }}
		</h1>
		<p v-if="flavor_text">{{ flavor_text }}</p>
	</div>
</template>

<script>
import axios from 'axios';

export default {
	props : [ 'ability' ],

	data(){
		return {
			error : false,
			flavor_text : undefined
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
			const response = await axios.get( `${ this.ability.url }`, requestConfig );
			this.flavor_text = response.data.flavor_text_entries.filter( obj => {
				return obj.language.name === "en";
			} )[0].flavor_text;
			console.log(this.flavor_text)
		}
		catch( error )
		{
			this.error = true;
		}
	}
}
</script>