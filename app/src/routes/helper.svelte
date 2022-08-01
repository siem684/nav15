<script context="module">
    export function angleFromCoordinate(lat1,lon1,lat2,lon2) {
    var p1 = {
        x: lat1,
        y: lon1
    };

    var p2 = {
        x: lat2,
        y: lon2
    };
    // angle in radians
    var angleRadians = Math.atan2(p2.y - p1.y, p2.x - p1.x);
    // angle in degrees
    var angleDeg = Math.atan2(p2.y - p1.y, p2.x - p1.x) * 180 / Math.PI;
    console.log(angleDeg);
    return angleDeg;
    }
    export function angleJust(lat1,lon1,lat2,lon2) {
        lat1=toRadians(lat1);
        lat2=toRadians(lat2);
        lon1=toRadians(lon1);
        lon2=toRadians(lon2);

        let X = Math.cos(lat2)*Math.sin(lon2-lon1);
        alert("X is "+ X)
        let Y = Math.cos(lat1)*Math.sin(lat2)-Math.sin(lat1)*Math.cos(lat2)*Math.cos(lon2-lon1);
        alert("Y is "+ Y)
        let Beta = Math.atan2(X,Y)
        alert("Beta is " + Beta)
        let BetaDeg = (toDegrees(Beta) + 360) % 360;
        alert("Beta in Deg is " + BetaDeg);
    return BetaDeg;
    }

    // Converts from degrees to radians.
function toRadians(degrees) {
  return degrees * Math.PI / 180;
};
 
// Converts from radians to degrees.
function toDegrees(radians) {
  return radians * 180 / Math.PI;
}


export function bearing(startLat, startLng, destLat, destLng){
  startLat = toRadians(startLat);
  startLng = toRadians(startLng);
  destLat = toRadians(destLat);
  destLng = toRadians(destLng);

  y = Math.sin(destLng - startLng) * Math.cos(destLat);
  x = Math.cos(startLat) * Math.sin(destLat) -
        Math.sin(startLat) * Math.cos(destLat) * Math.cos(destLng - startLng);
  brng = Math.atan2(y, x);
  brng = toDegrees(brng);
  return (brng + 360) % 360;
}
</script>