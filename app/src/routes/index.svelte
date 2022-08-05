
<img width="350px" src="./logo.png" alt="" class="centerhorizontal">

<p class="centerhorizontal red">
    {Math.round(angle)}
    <br/>
    {Math.round(dist)}
    <br/>
    {Math.round(speed)}
</p>


<div class="center" style="transform: rotate({angle}deg)">
    <img src="./icons8-gps-50.png" alt="">
</div>
<div id="biggerblock" class="center">
    <img src="./compass.png" width="150px" alt="">
</div>

<script>
    import helper, { angleJust, getDistanceFromLatLonInKm } from "./helper.svelte"
    let a,times=0;
    let location ="test2";
    let myLat, myLong, angle, dist, speed = 0;
    let destLat = 51.9795;
    let destLong = 5.9257;

    getLocation();
    setInterval(()=>getLocation(),10000);
    function getLocation() {
        times++;
        if (typeof window !== 'undefined') {
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(showPosition);
        } else {
            location = "Geolocation is not supported by this browser.";
        }
    }}
    function showPosition(position) {
        location = "Latitude: " + position.coords.latitude +  "<br>Longitude: " + position.coords.longitude;
        myLat=position.coords.latitude;
        myLong=position.coords.longitude;
        speed=position.coords.speed;
        angle = angleJust(myLat,myLong,destLat,destLong);
        dist = getDistanceFromLatLonInKm(myLat,myLong,destLat,destLong)*2.3

    }
</script>

<style>
.centerhorizontal {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
  @font-face {
    font-family: redFont;
    src: url(bullet-regular.ttf);
}
.red {
    font-family: redFont;
    color: red;
    text-align: center;
    font-size: 30px;
}

#biggerblock {
    top: -20px;
    width: 150px;
    height: 150px;
}
</style>