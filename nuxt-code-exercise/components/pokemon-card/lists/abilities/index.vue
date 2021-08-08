<template>
	<div>
		<strong>Abilities:</strong> 
		<span v-for="( ability, index ) in abilities" :key="index" class="is-capitalized">
			<span>{{ ability.ability.name.replace( "-", " " ) }}</span><span v-if="index != Object.keys( abilities ).length - 1">, </span>
		</span>
	</div>
</template>

<script>
export default {
	props : [ "abilities" ]
}
</script>