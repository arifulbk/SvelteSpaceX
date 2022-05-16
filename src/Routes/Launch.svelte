
<script>
    import { onMount } from "svelte";
    let launches, filtered_launch = []; 
    let filters= {
        s : '',
        sts: '',
        upcoming: false
    }

    const search_by_rocket = s => {
        filters.s = s;
        filter_changed();
    }
    const filter_by_status = sts => {
        filters.sts = sts;
        filter_changed();
    }
    
    const filter_by_date = sts => {
        filters.dt = dt;
        filter_changed();
    }

    const filter_by_arrival = arv => {
        filters.upcoming = arv;
        filter_changed();
    }    
    
    const filter_changed = () => {
        console.log("filter change");
        let new_list = launches; 
        if(filters.s)
        {
            new_list = new_list.filter(l=>l.mission_name.toLowerCase().indexOf(filters.s.toLowerCase()) >=0 );
        }
        if(filters.sts){
            new_list = new_list.filter(st=>st.launch_success ==  (filters.sts == '1' ? true : false) );
        }
        //if(filters.arv){
            new_list = new_list.filter(st=>st.upcoming ==  filters.upcoming);
        //}
        
        filtered_launch = new_list;
    }
    
    onMount(async () => {
        const response = await fetch(`https://api.spacexdata.com/v3/launches`);
        const obj = await response.json();
        launches = obj;
        filtered_launch = obj;
    });
</script>
<main>   

    <div class="bg-[#16171A] grid grid-cols-1 gap-4 md:grid-cols-2 xl:grid-cols-4 p-6">
        <div class="rounded-2xl p-3.5 sm:p-5">
            <input type="search" id="search_rocket" on:keyup={e=>search_by_rocket(e.target.value)} class="form-control relative flex-auto min-w-0 block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" placeholder="Search by rocket name" aria-label="Search" aria-describedby="button-addon2">              
        </div>
        <div class="bg-[#16171A] rounded-2xl p-3.5 sm:p-5">
            <select id="mission_status" on:change={e=>filter_by_date(e.target.value)} class="form-select appearance-none  block w-full  px-3 py-1.5 text-base font-normal text-gray-700
                bg-white bg-clip-padding bg-no-repeat  border border-solid border-gray-300 rounded  transition
                ease-in-out m-0
                focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example">
                    <option selected>Filter by launch date</option>
                    <option value="0">Last week</option>
                    <option value="1">Last month</option>
                    <option value="1">Last year</option>
                </select>
        </div>
        <div class="bg-[#16171A] rounded-2xl p-3.5 sm:p-5">
            <select id="mission_status" on:change={e=>filter_by_status(e.target.value)} class="form-select appearance-none  block w-full  px-3 py-1.5 text-base font-normal text-gray-700
                bg-white bg-clip-padding bg-no-repeat  border border-solid border-gray-300 rounded  transition
                ease-in-out m-0
                focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example">
                    <option selected>Filter by launch status</option>
                    <option value="0">Failure</option>
                    <option value="1">Success</option>
                </select>
        </div>
        <div class="bg-[#16171A] rounded-2xl p-3.5 sm:p-5">
            <div class="form-check">
                <input on:change={e=>filter_by_arrival(e.target.checked)} class="form-check-input appearance-none h-4 w-4 border border-gray-300 rounded-sm bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 mt-1 align-top bg-no-repeat bg-center bg-contain float-left mr-2 cursor-pointer" type="checkbox" value="" id="flexCheckChecked">
                <label class="form-check-label inline-block text-white" for="flexCheckChecked">
                  Upcoming
                </label>
              </div>
        </div>
    </div>

    <div class="grid grid-cols-1 gap-4 md:grid-cols-2 xl:grid-cols-3 p-6">
        {#each filtered_launch as launch}
            <div class="bg-[#16171A] rounded-2xl p-3.5 sm:p-5">
                <div class="text-center rounded-2xl bg-[#212326] p-8 sm:px-20 sm:pb-14 sm:pt-10 flex flex-col items-center">
                    <div class="rounded-full flex justify-center items-center bg-[#16171A] w-28 h-28">
                        <!-- Heroicon name: solid/lightning-bold -->
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 text-yellow-400" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M11.3 1.046A1 1 0 0112 2v5h4a1 1 0 01.82 1.573l-7 10A1 1 0 018 18v-5H4a1 1 0 01-.82-1.573l7-10a1 1 0 011.12-.38z" clip-rule="evenodd"></path>
                        </svg>
                        
                        <img alt={launch.name} class="left-0 top-0 w-full h-full p-2 object-contain object-center transition duration-50" loading="lazy" src={launch.links.mission_patch_small} />
                    </div>
                    <p class="mt-9 text-white font-mulish font-bold text-2xl ">
                        {launch.mission_name}
                    </p>
                    <p class="line-clamp-2 text-1.5xl line-clamp-3 max-h-10 overflow-hidden mt-5 text-white font-mulish leading-[22px] max-w-xs mx-auto">
                        {launch.details == null ? 'Details not available' : launch.details}
                    </p>

                    <p class="pb-6 text-1.5xl line-clamp-3 max-h-10 overflow-hidden mt-5 text-white font-mulish leading-[22px] max-w-xs mx-auto">{launch.launch_date_utc == null ? 'Date not available' : new Date(launch.launch_date_utc).toLocaleDateString('en-us', { weekday:"long", year:"numeric", month:"short", day:"numeric"})}</p>
                
                    {#if launch.launch_success}
                        <span class="text-2xl inline-block py-1 px-2.5 leading-none text-center whitespace-nowrap align-baseline font-bold bg-green-500 text-white rounded">Successful</span>
                    {:else}
                        <span class="text-2xl inline-block py-1 px-2.5 leading-none text-center whitespace-nowrap align-baseline font-bold bg-red-500 text-white rounded">Failed</span>
                    {/if}
                </div>
            </div>
        {/each}
    </div>
</main>
