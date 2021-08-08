<template>
	<div>
		<strong>Types:</strong> 
		<span v-for="( type, index ) in types" :key="index" class="is-capitalized">
			<span>{{ type.type.name.replace( "-", " " ) }}</span><span v-if="index != Object.keys( types ).length - 1">, </span>
		</span>
	</div>
</template>

<script>
export default {
	props : [ "types" ]
}
</script>