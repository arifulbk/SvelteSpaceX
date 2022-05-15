
<script>
    // import { onMount } from "svelte";
    export let launchpads = [];
    launchpads = []; 
    async function get_launchpads() {
		const response = await fetch(`https://api.spacexdata.com/v3/launchpads`);
        const obj = await response.json();
		launchpads = obj;
        let google = window.google;
        let map = document.getElementById("map-canvas");
        
        let lat = launchpads[0].location.latitude;
        let lng = launchpads[0].location.longitude;
        const myLatlng = new google.maps.LatLng(lat, lng);
        const mapOptions = {
            zoom: 2,
            scrollwheel: false,
            center: myLatlng,
            mapTypeId: google.maps.MapTypeId.ROADMAP
        };

        map = new google.maps.Map(map, mapOptions);
        var marker = null;
        
        for(var i = 0 ; i < launchpads.length; i++)
        {
            marker = new google.maps.Marker({
                position:  new google.maps.LatLng(launchpads[i].location.latitude, launchpads[i].location.longitude),
                map: map,
                animation: google.maps.Animation.DROP,
                title: "Launchpad location",
            });
        }        
        
        const contentString =
            '<div class="info-window-content"><h2>Notus Svelte</h2>' +
            "<p>A beautiful Dashboard for Bootstrap 4. It is Free and Open Source.</p></div>";

        const infowindow = new google.maps.InfoWindow({
            content: contentString,
        });

        google.maps.event.addListener(marker, "click", function () {
            infowindow.open(map, marker);
        });
	}

    get_launchpads();   
    // onMount(async () => {
    // });
</script>
<main>
    <div style="height:500px;" id="map-canvas" class="relative w-full rounded h-600-px container mx-auto p-6">
    </div>
</main>