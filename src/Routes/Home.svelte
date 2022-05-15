
<script>	
	export let company_name = {};
	let company_info = {}; //{"name":"SpaceX","founder":"Elon Musk","founded":2002,"employees":7000,"vehicles":3,"launch_sites":3,"test_sites":1,"ceo":"Elon Musk","cto":"Elon Musk","coo":"Gwynne Shotwell","cto_propulsion":"Tom Mueller","valuation":27500000000,"headquarters":{"address":"Rocket Road","city":"Hawthorne","state":"California"},"links":{"website":"https://www.spacex.com/","flickr":"https://www.flickr.com/photos/spacex/","twitter":"https://twitter.com/SpaceX","elon_twitter":"https://twitter.com/elonmusk"},"summary":"SpaceX designs, manufactures and launches advanced rockets and spacecraft. The company was founded in 2002 to revolutionize space technology, with the ultimate goal of enabling people to live on other planets."};
	fetch("https://api.spacexdata.com/v3/launches").then(function(response){
        console.log(response);
		company_info = response;
    });

	async function fetch_company_data() {
		const response = await fetch(`https://api.spacexdata.com/v3/info`);
		const obj = await response.json();
		company_name = obj;
		// return obj.name;
	}

	fetch_company_data();
</script>
<main>
	<div class="">
		<h1 class="transition-colors p-6 leading-tight text-6xl mt-0 mb-2">{company_name.name}</h1>
        <hr>
        <div class="p-6">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label class="underline">Description</label>
            <p class="text-xl font-light leading-relaxed mt-6 mb-4 text-gray-800">{company_name.summary}</p>
           
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label class="underline">Founder</label>
            <p class="text-xl font-light leading-relaxed mt-6 mb-4 text-gray-800">{company_name.founder}</p>
    
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label class="underline">Year founded</label>
            <p class="text-xl font-light leading-relaxed mt-6 mb-4 text-gray-800">{company_name.founded}</p>
        </div>       
        
	</div>
</main>
