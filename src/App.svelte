<script>
	import Routers from "svelte-spa-router";
	import Home from "./Routes/Home.svelte";
	import Launch from "./Routes/Launch.svelte";
	import Launchpads from "./Routes/Launchpads.svelte";
	import NotFound from "./Routes/NotFound.svelte";

	
	export let company_name = {};
	async function fetch_company_data() {
		const response = await fetch(`https://api.spacexdata.com/v3/info`);
		const obj = await response.json();
		company_name = obj;
		// return obj.name;
	}
	fetch_company_data();

	let routes = {
		"/": Home,
		"/home": Home,
		"/launch": Launch,
		"/launchpads": Launchpads,
	}
	/*
	function main () {
		window.NotFound = new NotFound({
		  target: document.body
		});
	  }	  
	document.addEventListener('DOMContentLoaded', main);
	*/
</script>

<main>
	<!-- <h1>Hello {name}!</h1> -->
	<!-- <p class="bg-amber-300">Initial SpaceX application!</p> -->
	
	<nav  class="p-5 bg-black shadow md:flex md:items-center md:justify-between">
		<ul class="sm:flex md:flex md:items-center z-[-1] md:z-auto md:static absolute text-white  w-full left-0 md:w-auto md:py-0 py-4 md:pl-0 pl-7 md:opacity-100 opacity-0 top-[-400px] transition-all ease-in duration-500">
			<li class="mx-4 my-6 md:my-0">
			<!-- svelte-ignore a11y-invalid-attribute -->
			<a href="" class="text-xl hover:text-cyan-500 duration-500 text-white">Company Info</a>
			</li>
			<li class="mx-4 my-6 md:my-0">
			<a href="#/launch" class="text-xl hover:text-cyan-500 duration-500 text-white">Launch</a>
			</li>
			<li class="mx-4 my-6 md:my-0">
			<a href="#/launchpads" class="text-xl hover:text-cyan-500 duration-500 text-white">Launchpads</a>
			</li>
		</ul>
	</nav>


	
	<!-- <div class="">
		<h1>{company_name.name}</h1>
		<p>{company_name.summary}</p>
		<p>{company_name.founder}</p>
		<p>{company_name.founded}</p>
	</div> -->
	<Routers {routes} />
</main>

<style>
	/* main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	} */
</style>