<template>
  <div>
    <GmapMap :zoom="12" :center="{ lat: 1.364917, lng: 103.822872 }">
      <DirectionsRenderer travelMode="TRANSIT" 
      :origin="start"
      :destination="end">
        </DirectionsRenderer>
    </GmapMap>
    <br>
  </div>
</template>

<script>
import DirectionsRenderer from "./DirectionsRenderer.js";
import database from '../firebase.js'

export default {
  components: {
    DirectionsRenderer,
  },

  data: function() {
    return {
      start: "",
      end: "",
      uid: ""
    }
  },

  methods: { 
    fetchItems: function() {
      this.user = localStorage.uid;
      database.collection('users').doc(this.user).get().then(doc => {
        this.start = doc.data().start;
        this.end = doc.data().end;
      });
    }
  },

  created() {
    this.fetchItems();
  }
}
</script>


<style>
.vue-map-container {
  height: 600px;
  position:relative
}
</style>