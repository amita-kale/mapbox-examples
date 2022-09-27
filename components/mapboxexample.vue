<template>

    <head>
        <link href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css" rel="stylesheet">
        <link rel='stylesheet'
            href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.2.0/mapbox-gl-draw.css'
            type='text/css' />
        <link rel="stylesheet"
            href="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/v5.0.0/mapbox-gl-geocoder.css"
            type="text/css">
    </head>
    <v-map class="w-full h-full" :options="state.map" @loaded="onMapLoaded">

    </v-map>

    <div id="map">
        <select id="droupdownid" class="dropdown">
            <option id="streets-v11" type="radio" name="rtoggle" value="streets-v11" checked="checked">streets</option>
            <option id="light-v10" type="radio" name="rtoggle" value="light-v10">light</option>
            <option id="dark-v10" type="radio" name="rtoggle" value="dark-v10">dark</option>
            <option id="outdoors-v11" type="radio" name="rtoggle" value="outdoors-v11">outdoors</option>
            <option id="satellite-v9" type="radio" name="rtoggle" value="satellite-v9">satellite</option>
        </select>
    </div>
</template>

<script setup lang="ts">
import VMap from "v-mapbox";
import mapboxgl from "mapbox-gl";
import MapboxDraw from "@mapbox/mapbox-gl-draw";
import MapboxGeocoder from "@mapbox/mapbox-gl-geocoder";




const state: any = reactive({
    map: {
        accessToken:
            "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ",
        style: "mapbox://styles/mapbox/streets-v11?optimize=true",
        // style: "https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json",
        center: [444.04931277036667, 26.266912177018096] as number[], //uses longitude, latitude
        zoom: 1,
        maxZoom: 22,
        // projection: 'globe'

    }
});


async function onMapLoaded(map) {

    // Add the control to the map.
    map.addControl(
        new MapboxGeocoder({
            accessToken: "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ",
            mapboxgl: mapboxgl
        })
    );


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
    //     }).setLngLat([e.lngLat.lng, e.lngLat.lat]).addTo(map);
    // })


    map.addSource('maine', {
        type: 'geojson',
        data: {
            "type": "FeatureCollection",
            "features": [
                {
                    "type": "Feature",
                    "properties": {},
                    "geometry": {
                        "type": "Polygon",
                        "coordinates": [
                            [
                                [
                                    -15.468749999999998,
                                    7.710991655433217
                                ],
                                [
                                    -4.5703125,
                                    -21.289374355860424
                                ],
                                [
                                    33.046875,
                                    -11.867350911459294
                                ],
                                [
                                    12.65625,
                                    7.710991655433217
                                ],
                                [
                                    -15.468749999999998,
                                    7.710991655433217
                                ]
                            ]
                        ]
                    }
                },
                {
                    "type": "Feature",
                    "properties": {},
                    "geometry": {
                        "type": "LineString",
                        "coordinates": [
                            [
                                -46.7578125,
                                44.33956524809713
                            ],
                            [
                                -2.109375,
                                51.17934297928927
                            ]
                        ]
                    }
                },
                {
                    "type": "Feature",
                    "properties": {},
                    "geometry": {
                        "type": "Polygon",
                        "coordinates": [
                            [
                                [
                                    27.773437499999996,
                                    34.016241889667015
                                ],
                                [
                                    63.6328125,
                                    34.016241889667015
                                ],
                                [
                                    63.6328125,
                                    49.83798245308484
                                ],
                                [
                                    27.773437499999996,
                                    49.83798245308484
                                ],
                                [
                                    27.773437499999996,
                                    34.016241889667015
                                ]
                            ]
                        ]
                    }
                },
                {
                    "type": "Feature",
                    "properties": {},
                    "geometry": {
                        "type": "Point",
                        "coordinates": [
                            46.7578125,
                            -21.943045533438166
                        ]
                    }
                }
            ]
        }
    });

    // Add a new layer to visualize the polygon.
    map.addLayer({
        'id': 'maine',
        'type': 'fill',
        'source': 'maine', // reference the data source
        'layout': {},
        'paint': {
            'fill-color': '#0080ff', // blue color fill
            'fill-opacity': 0.5
        }
    });
    // Add a black outline around the polygon.
    map.addLayer({
        'id': 'outline',
        'type': 'line',
        'source': 'maine',
        'layout': {},
        'paint': {
            'line-color': '#000',
            'line-width': 3
        }
    });


    map.addControl(new mapboxgl.FullscreenControl());
    map.addControl(new mapboxgl.NavigationControl(), 'top-right');

    var selectId: any = document.getElementById('droupdownid');
    selectId.addEventListener('change', event => {
        console.log(event);
        map.setStyle('mapbox://styles/mapbox/' + event.target.value);
    })
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


.dropdown {
    margin-top: 1%;
    margin-left: 2%;
    width: 10%;
    height: 5%;
    font-size: large;
}
</style> 

