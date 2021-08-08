<template>
	<div>
		<h1 class="block is-capitalized has-text-weight-bolder is-size-4 is-flex is-justify-content-space-between">{{ pokedex.name }} <span>#{{ ('00' + pokedex.id).slice(-3) }}</span></h1>
		<img class="block" :src="pokedex.sprites.other['official-artwork'].front_default" :alt="pokedex.name">
		<hr>
		<div class="block">
			<h3 class="has-text-centered has-text-weight-bold mb-2">Types</h3>
			<div class="is-flex is-justify-content-center">
			<span v-for="( type, index ) in pokedex.types" :key="index" class="is-capitalized">
				<span :class='[ "type", type.type.name.replace( "-", " " )]'>{{ type.type.name.replace( "-", " " ) }}</span>
			</span>
			</div>
		</div>
		<hr>
		<div class="columns">
			<div class="column is-flex is-flex-direction-column is-align-items-center">
				<h3 class="has-text-centered has-text-weight-bold mb-2">Height</h3>
				<span>{{ pokedex.height / 10 }}m</span>
			</div>
			<div class="column is-flex is-flex-direction-column is-align-items-center">
				<h3 class="has-text-centered has-text-weight-bold mb-2">Weight</h3>
				<span>{{ pokedex.weight / 10 }}kg</span>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props : [ 'pokedex' ]
}
</script>