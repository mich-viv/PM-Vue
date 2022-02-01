<template>
		<div class="mb-3">
			<b-button v-b-toggle.sidebar-no-header>Menù</b-button>
			<p class="my-4">Project mountain V1.0, upgraded with Vue.js (WIP ATM)</p>
			<b-sidebar id="sidebar-no-header" bg-variant="secondary" aria-labelledby="sidebar-no-header-title" text-variant="light" no-header shadow>
			<template #default="{ hide }">
				<div class="p-3 text-center" align-v="center">
				<h4 id="sidebar-no-header-title">Menu</h4>
				<img src="../assets/logo_2.png" fluid thumbnail>
				<br>
				<br>
				<nav class="mb-3">
					<b-nav vertical>
						<!--<div>
							<b-form-group label="Seleziona il tema: " v-slot="{ ariaDescribedby }">
							<b-form-radio v-model="selected" :aria-describedby="ariaDescribedby" name="some-radios" id="dark" value="Dark">Tema chiaro</b-form-radio>
							<b-form-radio v-model="selected" :aria-describedby="ariaDescribedby" name="some-radios" id="light" value="Light">Tema scuro</b-form-radio>
							</b-form-group>
							</div>

							<input type="radio" id="dark" value="Dark" v-model="picked">
							<label for="one">dark</label>
							<br>
							<input type="radio" id="light" value="Light" v-model="picked">
							<label for="two">light</label>
							<br>
							<div class="mt-3">Selected: <strong>{{ picked }}</strong></div>
						-->
						<a class="mt-3" href="https://github.com/mich-viv">Other personal project</a>
						
						<a class="mt-3" href="https://www.linkedin.com/in/michele-vivianipd/">Contacts</a>
					</b-nav>
				</nav>
				<b-button variant="danger" block @click="hide">Chiudi menù</b-button>
				</div>
			</template>
			</b-sidebar>			
		</div>
</template>

<script>
export default {
  name: 'Menu',
  props: {
    msg: String
  },
  
  watch:{
		
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

a{
	color:white;
}
a:hover{
	color:white;
}
</style>
