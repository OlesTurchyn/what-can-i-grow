<template>
  <div class="map-container" ref="mapContainer"></div>
</template>

<script setup>
import { onMounted, ref, defineEmits } from "vue";
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import MapboxGeocoder from "@mapbox/mapbox-gl-geocoder";
import "@mapbox/mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";

// GeoJSON data
const geoJsonData = {
  type: "FeatureCollection",
  features: [
    {
      type: "Feature",
      properties: {
        name: "Zone 1",
        temperatureRange: "-30°C to -20°C",
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [-80.09574293481757, 42.76159766876401],
            [-80.3175840113152, 43.11589280079406],
            [-80.36043820610416, 43.29070565474515],
            [-80.40519141920524, 43.42828001068116],
            [-80.49617555024057, 43.678488601546036],
            [-80.55967837632056, 43.79157612860362],
            [-80.6042185168029, 43.94131280289909],
            [-80.64947025568898, 44.07865682258358],
            [-80.77572380846487, 44.341707213144986],
            [-80.99235448455647, 44.55686340451874],
            [-81.04080322221233, 44.6445888737218],
            [-81.08714322446268, 44.78190974226749],
            [-81.09851916172644, 44.918674738333294],
            [-81.23574345378526, 44.99554844609503],
            [-81.28053011140162, 45.182712412048375],
            [-81.63020265168322, 45.26240693676334],
            [-81.28173663567452, 44.73566673452487],
            [-81.50785316018425, 44.281019269792864],
            [-81.70439470174094, 44.086088341791225],
            [-81.73784790011288, 43.530444867799446],
            [-81.84950635843147, 43.17370858591599],
            [-82.36225452050896, 42.9451954926362],
            [-82.45215535250071, 42.57502100187793],
            [-82.45546808784263, 42.33971738863207],
            [-82.99102945460533, 42.293978792197606],
            [-83.07532072556137, 42.14553320692926],
            [-83.00977883862322, 41.94663070194946],
            [-82.64331228151264, 41.99399681158718],
            [-82.4774277653625, 41.94278571880628],
            [-82.40861937539975, 42.1035613192341],
            [-82.19042198083223, 42.17550978843991],
            [-81.97238802297053, 42.20975154870871],
            [-81.78431278788159, 42.38050649509648],
            [-81.30605383926618, 42.63200550461033],
            [-80.730895466203, 42.630972177648715],
            [-80.42636462970236, 42.61014741602315],
            [-80.09574293481757, 42.76159766876401],
          ],
        ],
      },
    },
  ],
};

const mapContainer = ref(null);
const emits = defineEmits(["updateCard"]);

onMounted(() => {
  if (mapContainer.value) {
    // Set your Mapbox access token
    mapboxgl.accessToken =
      "pk.eyJ1Ijoib2xlc3R1cmNoeW4iLCJhIjoiY2x6OWJkcWdrMDF5dTJycTJoNGhhZjAzeCJ9.G7kYp-RVYSXaO5CRpNuMNA";

    // Initialize the map
    const map = new mapboxgl.Map({
      container: mapContainer.value,
      style: "mapbox://styles/mapbox/standard", // You can change the style
      center: [0, 0], // Longitude, Latitude
      zoom: 1.5,
      projection: "globe", // Display the map as a 3D globe
    });

    // Add the Geocoder (Search) control to the map
    const geocoder = new MapboxGeocoder({
      accessToken: mapboxgl.accessToken,
      mapboxgl: mapboxgl,
      marker: false, // Optional: Disable default marker
      placeholder: "Search for locations", // Optional: Custom placeholder text for the search input
    });

    map.addControl(geocoder);

    // Add controls to the map
    map.addControl(new mapboxgl.NavigationControl());

    // Add the GeoJSON data to the map
    map.on("load", () => {
      map.addSource("zones", {
        type: "geojson",
        data: geoJsonData,
      });

      map.addLayer({
        id: "zones-layer",
        type: "fill",
        source: "zones",
        layout: {},
        paint: {
          "fill-color": "#D32C08",
          "fill-opacity": 0.4,
        },
      });

      // Change the cursor to a pointer when over the zones
      map.on("mouseenter", "zones-layer", () => {
        map.getCanvas().style.cursor = "pointer";
      });

      map.on("mouseleave", "zones-layer", () => {
        map.getCanvas().style.cursor = "";
      });
    });
  }
});
</script>

<style scoped>
.map-container {
  height: 94vh;
  width: 100%;
}
</style>
