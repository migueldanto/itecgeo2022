<template>
  <img src="../assets/itecgeo4.png" alt=""/>

  <div class="mapa1" ref="mapa1"></div>
</template>

<script setup>
  import maplibregl from 'maplibre-gl';
  import { ref, onMounted } from 'vue'
  const mapa1 = ref(null)

  onMounted(() => {
    console.log(mapa1)
    const map = new maplibregl.Map({
      container: mapa1._value,
      style: 'https://api.maptiler.com/maps/toner/style.json?key=jrcIzdt1OrHwCiQa3qeS', // stylesheet location
      center: [-99.65631,19.2902], // starting position [lng, lat]
      zoom: 12, // starting zoom,
      pitch:50
    });

    map.on("load",function() {
      rotateCamera(0)
    })

    function rotateCamera(timestamp) {
      // clamp the rotation between 0 -360 degrees
      // Divide timestamp by 100 to slow rotation to ~10 degrees / sec
      map.rotateTo((timestamp / 100) % 360, { duration: 0 });
      // Request the next frame of the animation.
      requestAnimationFrame(rotateCamera);
    }
  })
</script>

<style>
.mapa1{
  height: 400px;
}
</style>