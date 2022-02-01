<template>
  <div id="app">
	<div class="cell cell-map">
      <Map/>
    </div>
    <div class="cell cell-edit">
		<Menu/>
		<Dropdown/>
    </div>
  </div>
</template>

<script>
import Map from './components/Map.vue'
import Menu from './components/Menu.vue'
import Dropdown from './components/Dropdown.vue'

export default {
  name: 'App',
  components: {
    Map,
	Menu,
	Dropdown,
  },
  methods:{
  }
}
</script>

<style>
	.nav-item.nav-item.nav-item a {
		color: white;
	}
	html, body {
    height: 100%;
    margin: 0;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    height: 100%;
    display: grid;
    grid-template-columns: 100vh;
    grid-auto-rows: 1fr;
    grid-gap: 1rem;
    padding: 1rem;
    box-sizing: border-box;
  }

  .cell {
    border-radius: 4px;
    background-color: lightgrey;
  }

  .cell-map {
    grid-column: 1;
    grid-row-start: 1;
    grid-row-end: 2;
  }

  .cell-edit {
    grid-column: 2;
    grid-row: 1;
  }

  </style>
