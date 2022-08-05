
<img width="350px" src="./logo.png" alt="" class="centerhorizontal">

<p class="centerhorizontal red">{Math.round(angle)}</p>
<p>{times}</p>
<div class="center" style="transform: rotate({angle}deg)">
    <img src="./icons8-gps-50.png" alt="">
</div>

<script>
    import helper, { angleJust } from "./helper.svelte"
    let a,times=0;
    let location ="test2";
    let myLat = 0;
    let myLong = 0;
    let angle = 0;

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
        angle = angleJust(myLat,myLong,51.9795,5.9257);
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
</style>