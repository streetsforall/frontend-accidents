<script lang='ts'>
import mapboxgl, { type MapboxGeoJSONFeature } from 'mapbox-gl';
	import { onMount } from 'svelte';

    onMount(() => {
        const map = new mapboxgl.Map({
    container: 'map',
    crossSourceCollisions: true,
    hash: true,
    antialias: true,
    style:
    'mapbox://styles/kylerschin/clm2i6cmg00fw01of2vp5h9p5', // stylesheet location
    accessToken: "pk.eyJ1Ijoia3lsZXJzY2hpbiIsImEiOiJjajFsajI0ZHMwMDIzMnFwaXNhbDlrNDhkIn0.VdZpwJyJ8gWA--JNzkU5_Q",
    center: [-118.2171,33.9711], // starting position [lng, lat]
    //keep the centre at Los Angeles, since that is our primary user base currently
    //switch to IP geolocation and on the fly rendering for this soon
    zoom: 9.9, // starting zoom (must be greater than 8.1)
    fadeDuration: 0
});



map.on('load', () => {

    map.addSource("visionzerosource", {
    type: "vector",
    url: "https://s4a-martin.catenarymaps.org/visionzeromap"
})

map.addLayer(
{
'id': 'visionzero',
'type': 'circle',
'source': 'visionzerosource',
'source-layer': 'visionzeromap',
'paint': {
'circle-radius': 1,
'circle-color': '#ff0000',
}
} // Add layer below labels
)
})
    })
</script>

<div id='wrapgang'>
    <div id="map" style="width: 100%; height: 100%;" />

</div>
<svelte:head>
    <link href="https://api.mapbox.com/mapbox-gl-js/v2.14.1/mapbox-gl.css" rel="stylesheet">
    </svelte:head>
<style>
	:root {
		--background: #0a233f;
		--primary: #79bd43;
		--radius: 8px;
		--glow: 0;
	}

	* {
		cursor: default;
	}

	#map {
		width: 100%;
		height: 100%;
	}

    #wrapgang {
        width: 100vw;
        height: 100vh;
    }

    .mapboxgl-canvas-container {
        height: 100% !important;
    }
    
    :global(body) {
        overflow: none;
    }
   
    </style>