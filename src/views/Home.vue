<template>
    <v-container class="ma-0 pa-0 full-height">
        <div
            id="map"
            ref="map"
        />
    </v-container>
</template>

<script>
import 'ol/ol.css';
import Map  from 'ol/Map';
import View from 'ol/View';

import OSMSource     from 'ol/source/OSM';
import GeoTIFFSource from 'ol/source/GeoTIFF';

import TileLayer      from 'ol/layer/Tile';
import WebGLTileLayer from 'ol/layer/WebGLTile';

export default {
    name: 'Home',
    async mounted() {
        const source = new GeoTIFFSource( {
            sources: [
                {
                    url: 'https://sentinel-cogs.s3.us-west-2.amazonaws.com/sentinel-s2-l2a-cogs/2020/S2A_36QWD_20200701_0_L2A/TCI.tif'
                    // min: 0,
                    // max: 1768,
                    // nodata: 0,
                }
            ]
        } );

        console.log( GeoTIFFSource );

        const map = new Map( {
            target: this.$refs.map,
            layers: [
                new TileLayer( {
                    source: new OSMSource()
                } ),
                new WebGLTileLayer( {
                    source: source
                } )
            ],
            view: new View( {
                projection: 'EPSG:4326',
                center: [ 0, 0 ],
                zoom: 0,
                showFullExtent: true
            } )
        } );
    }
};
</script>

<style>
#map {
    position: absolute;

    background-color: orange;

    width: 100%;
    min-width: 100%;
    height: 100%;
    min-height: 100%;
}
</style>
