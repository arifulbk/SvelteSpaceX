
<script>	
	export let company_name = {};
	let company_info = {"name":"SpaceX","founder":"Elon Musk","founded":2002,"employees":7000,"vehicles":3,"launch_sites":3,"test_sites":1,"ceo":"Elon Musk","cto":"Elon Musk","coo":"Gwynne Shotwell","cto_propulsion":"Tom Mueller","valuation":27500000000,"headquarters":{"address":"Rocket Road","city":"Hawthorne","state":"California"},"links":{"website":"https://www.spacex.com/","flickr":"https://www.flickr.com/photos/spacex/","twitter":"https://twitter.com/SpaceX","elon_twitter":"https://twitter.com/elonmusk"},"summary":"SpaceX designs, manufactures and launches advanced rockets and spacecraft. The company was founded in 2002 to revolutionize space technology, with the ultimate goal of enabling people to live on other planets."};
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
        <a href="/" id="logo"  class="p-6">
            <svg version="1.1" x="0px" y="0px" viewBox="0 0 400 50">
              <title>SpaceX Logo</title>
              <g class="letter_s">
                <path class="fill-white" d="M37.5,30.5H10.9v-6.6h34.3c-0.9-2.8-3.8-5.4-8.9-5.4H11.4c-5.7,0-9,2.1-9,6.7v4.9c0,4,3.4,6.3,8.4,6.3h26.9v7H1.5
                c0.9,3.8,3.8,5.8,9,5.8h27.1c5.7,0,8.5-2.2,8.5-6.9v-4.9C46.1,33.1,42.8,30.8,37.5,30.5z"></path>
              </g>
              <g class="letter_p">
                <path class="fill-white" d="M91.8,18.6H59v30.7h9.3V37.5h24.2c6.7,0,10.4-2.3,10.4-7.7v-3.4C102.8,21.4,98.6,18.6,91.8,18.6z M94.8,28.4
                c0,2.2-0.4,3.4-4,3.4H68.3l0.1-8h22c4,0,4.5,1.2,4.5,3.3V28.4z"></path>
              </g>
              <g class="letter_a">
                <polygon class="fill-white" points="129.9,17.3 124.3,24.2 133.8,37.3 114,37.3 109.1,42.5 137.7,42.5 142.6,49.3 153.6,49.3 	"></polygon>
              </g>
              <g class="letter_c">
                <path class="fill-white" d="M171.4,23.9h34.8c-0.9-3.6-4.4-5.4-9.4-5.4h-26c-4.5,0-8.8,1.8-8.8,6.7v17.2c0,4.9,4.3,6.7,8.8,6.7h26.3
                c6,0,8.1-1.7,9.1-5.8h-34.8V23.9z"></path>
              </g>
              <g class="letter_e">
                <polygon class="fill-white" points="228.3,43.5 228.3,34.1 247,34.1 247,28.9 218.9,28.9 218.9,49.3 260.4,49.3 260.4,43.5 	"></polygon>
                <rect class="fill-white" x="219.9" y="18.6" width="41.9" height="5.4"></rect>
              </g>
              <g class="letter_x">
                <path class="fill-white" d="M287.6,18.6H273l17.2,12.6c2.5-1.7,5.4-3.5,8-5L287.6,18.6z"></path>
                <path class="fill-white" d="M308.8,34.3c-2.5,1.7-5,3.6-7.4,5.4l13,9.5h14.7L308.8,34.3z"></path>
              </g>
              <g class="letter_swoosh">
                <path class="fill-white" d="M399,0.7c-80,4.6-117,38.8-125.3,46.9l-1.7,1.6h14.8C326.8,9.1,384.3,2,399,0.7L399,0.7z"></path>
              </g>
            </svg>
          </a>

		<!-- <h1 class="transition-colors p-6 font-medium leading-tight text-3xl mt-0 mb-2 ">{company_name.name}</h1> -->
        
        <div class="p-6">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label>Description</label>
            <p class="text-xl font-light leading-relaxed mt-6 mb-4 text-gray-800">{company_name.summary}</p>
           
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label>Founder</label>
            <p class="text-xl font-light leading-relaxed mt-6 mb-4 text-gray-800">{company_name.founder}</p>
    
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label>Year</label>
            <p class="text-xl font-light leading-relaxed mt-6 mb-4 text-gray-800">{company_name.founded}</p>
        </div>       
        
	</div>
</main>
