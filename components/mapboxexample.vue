<template>

    <head>
        <link href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css" rel="stylesheet">
        <link rel='stylesheet'
            href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.2.0/mapbox-gl-draw.css'
            type='text/css' />
    </head>
    <v-map class="w-full h-full" :options="state.map" @loaded="onMapLoaded"></v-map>

    <div id="map"></div>
</template>

<script setup lang="ts">
import VMap from "v-mapbox";
import mapboxgl from "mapbox-gl";
import MapboxDraw from "@mapbox/mapbox-gl-draw";

const state: any = reactive({
    map: {
        accessToken:
            "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ",
        style: "mapbox://styles/mapbox/streets-v11?optimize=true",
        // style: "https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json",
        center: [444.04931277036667, 26.266912177018096] as number[], //uses longitude, latitude
        zoom: 6,
        maxZoom: 22,
        // projection: 'globe'

    }
});

async function onMapLoaded(map: mapboxgl.Map) {
    console.log("mathod call");
    new mapboxgl.Marker({
        color: "#" + (Math.random().toString(16) + "000000").substring(2, 8),
        draggable: true
    }).setLngLat([30.5, 50.5])
        .addTo(map);

    var Draw = new MapboxDraw();
    map.addControl(Draw, 'top-right');

    // map.on('click', (e) => {
    //     console.log(e);
    //     console.log(e.lngLat)
    //     new mapboxgl.Marker({
    //         draggable: true,
    //         color: "#" + (Math.random().toString(16) + "000000").substring(2, 8),
    //     }).setLngLat([e.lngLat.lng, e.lngLat.lat]).addTo(map)
    //     new mapboxgl.Popup()
    //         .setLngLat([e.lngLat.lng, e.lngLat.lat])
    //         .setHTML("hello world")
    //         .addTo(map);
    // })


    map.addControl(new mapboxgl.FullscreenControl());
    map.addControl(new mapboxgl.NavigationControl(), 'top-right');
}
</script>
<style scoped>
#map {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 100%;
}



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

