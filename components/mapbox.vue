<script setup lang="ts">
import "mapbox-gl/dist/mapbox-gl.css";
import mapboxgl from "mapbox-gl";

onMounted(() => {
  var geojson = {
    type: "FeatureCollection",
    features: [
      {
        type: "Feature",
        geometry: {
          type: "Point",
          coordinates: [-77.032, 38.913],
        },
        properties: {
          title: "Mapbox",
          description: "Washington, D.C.",
        },
      },
      {
        type: "Feature",
        geometry: {
          type: "Point",
          coordinates: [-122.414, 37.776],
        },
        properties: {
          title: "Mapbox",
          description: "San Francisco, California",
        },
      },
    ],
  };

  mapboxgl.accessToken =
    "pk.eyJ1IjoibWFyazQ0bW9sZXMiLCJhIjoiY2x0OHFzNjk0MHg5eDJrbzFtb3d3Z3htdCJ9.M2uv_CFtmoeqSSMKQMcY2Q";
  const map = new mapboxgl.Map({
    container: "map",
    projection: "mercator",
    style: "mapbox://styles/mark44moles/cltgz3ens018h01pjcyn14wnx",
    center: [-74.0060152, 40.7127281],
    zoom: 2.5,
    maxZoom: 8,
  });

  // add markers to map
  geojson.features.forEach(function (marker, i) {
    // create a HTML element for each feature

    // make a marker for each feature and add it to the map
    new mapboxgl.Marker({
      element: createRoundedMarker(),
    })
      .setLngLat(marker.geometry.coordinates)
      .setPopup(
        new mapboxgl.Popup({
          offsetY: 10,
        }).setHTML(`
        <div class="h-full flex">
          <button tabindex="-1" class='w-full rounded-[4rem] mt-auto bg-red-500 hover:bg-opacity-50 duration-500 text-xs py-[0.62rem]'>Learn more</button>
        </div>`)
      )
      .addTo(map);
  });
});

const createRoundedMarker = () => {
  var marker = document.createElement("div");
  marker.className = "rounded-marker";
  marker.innerHTML = "<span></span>";
  return marker;
};
</script>

<template>
  <div class="relative container m-auto">
    <div id="map" style="width: 100%; height: 100vh"></div>
  </div>
</template>
