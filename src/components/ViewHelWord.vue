<template>
  <div id="appConteiner">
    <img class="imagetop" alt="helloworld" src="../assets/Mednikov_team.jpg" v-on:click="select($event)" />
     <p class="wordclass"> {{hey}} </p>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      hey: ''
    }
  },
  methods: {
    select: function(event) {
      this.hey = event.currentTarget.alt;
    }
  }
}
</script>

<style>
.imagetop {
  width: 200px;
  height: 200px;
}
</style>
