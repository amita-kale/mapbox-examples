<template>


    <head>
        <link href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css" rel="stylesheet">
    </head>
    <v-map class="w-full h-full" :options="state.map" @loaded="onMapLoaded"></v-map>

    <div id="map"></div>
</template>

<script setup lang="ts">
import VMap from "v-mapbox";
import mapboxgl from "mapbox-gl";
mapboxgl.accessToken = "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ";
const state: any = reactive({
    map: {
        // accessToken:
        //     "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ",
        // style: "mapbox://styles/mapbox/streets-v11?optimize=true",
        // // style: "https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json",
        // center: [444.04931277036667, 26.266912177018096] as number[], //uses longitude, latitude
        // zoom: 6,
        // maxZoom: 22,
        // projection: 'globe'
        container: 'map',
        style: 'mapbox://styles/mapbox/satellite-streets-v11',
        zoom: 11,
        center: [444.04931277036667, 26.266912177018096] as number[],
        projection: 'globe'
    }
});

async function onMapLoaded(map: mapboxgl.Map) {
    console.log("mathod call");
    map.on('load', () => {
        // Set the default atmosphere style
        map.setFog({});
    });
    // map.addControl(new mapboxgl.NavigationControl(), 'top-left');
}
</script>
<style scoped>
#map {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 100%;
}

/* .w-screen {
    width: 100vw;
}

.h-screen {
    height: 100vh;
} */

.h-full {
    height: 100%;
}

.w-full {
    width: 100%;
}

.mapboxgl-popup {
    max-width: 400px;
    font: 12px/20px 'Helvetica Neue', Arial, Helvetica, sans-serif;
}
</style> 

