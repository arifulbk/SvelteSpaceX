<script>
	export let name;

	fetch("https://api.spacexdata.com/v3/launches").then(function(response){
        console.log(response)
    })
</script>

<main>
	<h1>Hello {name}!</h1>
	<p class="bg-amber-300">Initial SpaceX application!</p>
</main>

<style>
	main {
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
	}
</style>