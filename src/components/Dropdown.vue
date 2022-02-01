<template>
		<div>
			<div class="mt-3"><b-button v-on:click="resetView(reset)">Reset view</b-button>Sentiero selezionato: <strong>{{ selected }}</strong></div>
			<b-form-select v-model="selected" v-on:change="getSelectedItem(selected)" :options="options" class="mb-3 mt-3">
				<template #first>
					<b-form-select-option :value="null" disabled>-- Seleziona un sentiero --</b-form-select-option>
				</template>
			</b-form-select>
			<Graph :trek="selected"/>
			<Information :trek="selected"/>
		</div>
		
</template>

<script>
import Graph from './Graph.vue'
import Information from './Information.vue'


export default {
  name: 'Dropdown',
  props: ['trek'],
  components: {
	Graph,
	Information
  },
  data(){
	return{
		selected: null,
		reset: true,
		options: [
			{ value: '560', text: 'cai 560' },
			{ value: '567', text: 'cai 567' },
			{ value: '483', text: 'cai 483' },
			{ value: '762', text: 'cai 762' },
			{ value: '215', text: 'cai 215' },
			{ value: '333', text: 'cai 333' },
			{ value: '334', text: 'cai 334' },
			{ value: '764', text: 'cai 764' }
		]
	}
  },
	methods: {
		getSelectedItem(item) {
			this.$root.$emit('change',item);
        },
		resetView(reset){
			this.$root.$emit('click',reset)
		}

	}
		
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
