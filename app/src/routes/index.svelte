<script>
	import helper, { angleJust, getDistanceFromLatLonInKm } from './helper.svelte';
	let landscape = false;
	let myLat,
		myLong,
		angle,
		dist,
		speed = 0;
	let destLat = 51.156792571149666;
	let destLong = 5.85393332261703;

	getLocation();
	setInterval(() => getLocation(), 5000);
	if (typeof screen !== 'undefined') {
		screen.orientation.onchange = () => {
			screen.orientation.type.substring(0, 1) == 'l' ? (landscape = true) : (landscape = false);
		};
	}
	function getLocation() {
		let currentDate = new Date();
		let time = currentDate.getHours();
		if (time >= 14) {
			destLat = 50.36086272435071;
			destLong = 5.579208970781638;
		}
		if (typeof window !== 'undefined') {
			if (navigator.geolocation) {
				navigator.geolocation.getCurrentPosition(showPosition),
					(err) => {
						console.log(err);
						alert('fetching the position failed');
					},
					{ enableHighAccuracy: false, timeout: 10000, maximumAge: 0 };
			} else {
				console.log('Geolocation is not supported by this browser.');
			}
		}
	}
	function showPosition(position) {
		location =
			'Latitude: ' + position.coords.latitude + '<br>Longitude: ' + position.coords.longitude;
		myLat = position.coords.latitude;
		myLong = position.coords.longitude;
		speed = position.coords.speed * 10;
		angle = angleJust(myLat, myLong, destLat, destLong);
		dist = getDistanceFromLatLonInKm(myLat, myLong, destLat, destLong) * 6.3;
	}
</script>

{#if !landscape}
	<img width="350px" src="./logo.png" alt="" class="centerhorizontal" />
	<div style="position:relative; top:-50px;">
		<p class="red">
			<br />
			{Math.round(angle)}
			<br />
			{Math.round(dist)}
			<br />
			{Math.round(speed)}
		</p>
	</div>
{:else}
	<p class="red">
		{Math.round(dist)}
	</p>
{/if}

<div class="center" style="transform: rotate({angle}deg)">
	<img src="./icons8-gps-50.png" alt="" />
</div>
<div id="biggerblock" class="center">
	<img src="./compass.png" width="150px" alt="" />
</div>

<style>
	.centerhorizontal {
		display: block;
		margin-left: auto;
		margin-right: auto;
	}
	@font-face {
		font-family: redFont;
		src: url(./bullet-regular.ttf);
	}
	.red {
		margin: 0;
		top: -0px;
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
