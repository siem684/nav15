<button on:click={getLocation}>locatie</button>
<p>{angle}</p>
<div class="center" style="transform: rotate({angle}deg)">
    <img src="./icons8-gps-50.png" alt="">
    <p id="demo">{location}</p>
</div>

<script>
    import helper, { angleFromCoordinate, angleJust, bearing } from "./helper.svelte"
    let a=0;
    let location ="test2";
    let myLat = 0;
    let myLong = 0;
    let angle = angleFromCoordinate(myLat,myLong,51.8439911,25.9257);

    function getLocation() {

        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(showPosition);
        } else {
            location = "Geolocation is not supported by this browser.";
        }
    }
    function showPosition(position) {
        location = "Latitude: " + position.coords.latitude +  "<br>Longitude: " + position.coords.longitude;
        myLat=position.coords.latitude;
        myLong=position.coords.longitude;
        angle = angleJust(myLat,myLong,51.9795,5.9257);
    }
</script>