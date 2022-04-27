<template>
  <div class="mapa1" ref="mapa1"></div>
  <div class="logo-container">
    <img src="../assets/itecgeo4.png" alt=""/>
  </div>
  
</template>

<script setup>
  import maplibregl from 'maplibre-gl';
  import { ref, onMounted } from 'vue'
  const mapa1 = ref(null)

  onMounted(() => {
    
    const map = new maplibregl.Map({
      container: mapa1._value,
      style: 'https://api.maptiler.com/maps/topo/style.json?key=jrcIzdt1OrHwCiQa3qeS', // stylesheet location
      center: [0,0], // starting position [lng, lat]
      zoom: 1, // starting zoom,
      pitch:0,
      bearing: 0
    });

    map.on("load",function() {
      map.flyTo({
        center: [-99.65631,19.2902],
        zoom: 12, // starting zoom,
        pitch:45,
        bearing: 180,
        speed: 0.2,
        curve: 1,
        easing(t) {
          return t;
        }
      })
    });

    map.on('zoomend', function() {
      rotateCamera(0)
    });

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
  height: 100vh;
}

.logo-container{
  position: fixed;
  display: flex;
  top:0;
  left: 0;
  height: 100vh;
  width: 100%;
  justify-content: center;
  align-items: center;
  background-color: #4141412e;
}

.logo-container img{
  height: 75px;
}
</style>