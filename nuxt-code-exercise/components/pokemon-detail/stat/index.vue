<template>
	<div class="stat column is-half-tablet is-one-third-widescreen">
		<div class="box h-100 is-flex is-flex-direction-column is-justify-content-space-between">
			<h1 class="is-size-4 is-capitalized has-text-centered has-text-weight-normal mb-3">
				{{ stat.stat.name.replace( "-", " " ) }}
			</h1>
			<p class="is-size-1 has-text-centered has-text-weight-bold">{{ stat.base_stat }}</p>
		</div>
	</div>
</template>

<script>
import axios from 'axios';

export default {
	props : [ 'stat' ]
}
</script>