<script>
   export let launches = []; // {"name":"SpaceX","founder":"Elon Musk","founded":2002,"employees":7000,"vehicles":3,"launch_sites":3,"test_sites":1,"ceo":"Elon Musk","cto":"Elon Musk","coo":"Gwynne Shotwell","cto_propulsion":"Tom Mueller","valuation":27500000000,"headquarters":{"address":"Rocket Road","city":"Hawthorne","state":"California"},"links":{"website":"https://www.spacex.com/","flickr":"https://www.flickr.com/photos/spacex/","twitter":"https://twitter.com/SpaceX","elon_twitter":"https://twitter.com/elonmusk"},"summary":"SpaceX designs, manufactures and launches advanced rockets and spacecraft. The company was founded in 2002 to revolutionize space technology, with the ultimate goal of enabling people to live on other planets."};
    // fetch("https://api.spacexdata.com/v3/launches").then(function(response){
    //     console.log(response);
    //     launches = response;
    // });

	async function fetch_launch_data() {
		const response = await fetch(`https://api.spacexdata.com/v3/launches`);
        
		const obj = await response.json();
		launches = obj;
		// return obj.name;
	}
    fetch_launch_data();
</script>
<main>

    

    <div class="grid grid-cols-4 gap-4 p-6">
        <div class="flex justify-center">
            <div class="mb-3 xl:w-96">
            <label for="search_rocket" class="text-left">Rocket name</label>
              <div class="input-group relative flex items-stretch w-full mb-4">
                <input type="search" id="search_rocket" class="form-control relative flex-auto min-w-0 block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" placeholder="Search by rocket name" aria-label="Search" aria-describedby="button-addon2">
                <button class="btn inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700  focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out flex items-center" type="button" id="button-addon2">
                  <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="search" class="w-4" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
                    <path fill="currentColor" d="M505 442.7L405.3 343c-4.5-4.5-10.6-7-17-7H372c27.6-35.3 44-79.7 44-128C416 93.1 322.9 0 208 0S0 93.1 0 208s93.1 208 208 208c48.3 0 92.7-16.4 128-44v16.3c0 6.4 2.5 12.5 7 17l99.7 99.7c9.4 9.4 24.6 9.4 33.9 0l28.3-28.3c9.4-9.4 9.4-24.6.1-34zM208 336c-70.7 0-128-57.2-128-128 0-70.7 57.2-128 128-128 70.7 0 128 57.2 128 128 0 70.7-57.2 128-128 128z"></path>
                  </svg>
                </button>
              </div>
            </div>
        </div>   

        <div class="flex justify-center">
        <div class="mb-3 xl:w-96">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label for="mission_launch" class="text-left">Launch Date</label>
            <input  class="form-control relative flex-auto min-w-0 block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" type="date" id="mission_launch" name="mission_launch">
        </div>
        </div>

        <div class="flex justify-center">
        <div class="mb-3 xl:w-96">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label for="mission_status" class="text-left">Launch Status</label>
            <select id="mission_status" class="form-select appearance-none  block w-full  px-3 py-1.5 text-base font-normal text-gray-700
            bg-white bg-clip-padding bg-no-repeat  border border-solid border-gray-300 rounded  transition
            ease-in-out m-0
            focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example">
                <option selected>Mission status</option>
                <option value="1">Failure</option>
                <option value="0">Success</option>
            </select>
        </div>
        </div>

        <div class="flex justify-center">
        <div class="mb-3 xl:w-96">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label for="mission_arrival" class="text-left">Mission arrival</label>
            <select id="mission_arrival" class="form-select appearance-none  block w-full  px-3 py-1.5 text-base font-normal text-gray-700
            bg-white bg-clip-padding bg-no-repeat  border border-solid border-gray-300 rounded  transition
            ease-in-out m-0
            focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example">
                <option selected>Mission arrival</option>
                <option value="1">Recent</option>
                <option value="0">Upcoming</option>
            </select>
        </div>
        </div>
    </div>
    

    <div class="grid grid-cols-4 gap-4 p-6">
        {#each launches as launch}
            <!-- <div class="p-6 max-w-sm bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700"> -->
            <div class="bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700">
                <h5 class="p-6 mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{launch.mission_name}</h5>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400 px-px">{launch.details == null ? 'Details not available' : launch.details}</p>
                
            </div>
        {/each}
    </div>
    
</main>
