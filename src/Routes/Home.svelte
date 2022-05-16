
<script>	
	export let company_name = {};
    let address = "";
	// let company_info = {}; 
	// fetch("https://api.spacexdata.com/v3/launches").then(function(response){
    //     console.log(response);
	// 	company_info = response;
    // });

	async function fetch_company_data() {
		const response = await fetch(`https://api.spacexdata.com/v3/info`);
		const obj = await response.json();
		company_name = obj;
        address = company_name.headquarters.address + ', '+ company_name.headquarters.city + ', ' +company_name.headquarters.state;
		// return obj.name;
	}
	fetch_company_data();
</script>
<main>
      <div class="relative overflow-x-auto shadow-md sm:rounded-lg p-6 rounded-md rounded-md">
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <tbody>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                    <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                        Name
                    </th>
                    <td class="px-6 py-4">
                        {company_name.name}
                    </td>
                </tr>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                    <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                        Description
                    </th>
                    <td class="px-6 py-4">
                        {company_name.summary}
                    </td>
                </tr>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                    <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                        Founder
                    </th>
                    <td class="px-6 py-4">
                        {company_name.founder}
                    </td>
                </tr>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                    <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                        Year Founded
                    </th>
                    <td class="px-6 py-4">
                        {company_name.founded}
                    </td>
                </tr>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                    <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                        No. of employee
                    </th>
                    <td class="px-6 py-4">
                        {company_name.employees}
                    </td>
                </tr>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                    <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                        Address 
                    </th>
                    <td class="px-6 py-4">
                        {address}
                    </td>
                </tr>
            </tbody>
        </table>
    </div>


    
</main>
