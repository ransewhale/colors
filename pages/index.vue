<template>
  <v-row justify="center" align="center">
    <v-col cols="12" md="9">
      <v-card class="top-card">
        <v-card-title class="text-h3">Colors.</v-card-title>
        <v-card-text class="text-h5">We have 16,777,216 colors. Which color do you like?</v-card-text>
        <SelectBars :sliderItems="sliderItems" :ButtonToTop="false" />
      </v-card>
    </v-col>
  </v-row>
</template>

<script>

export default {
  head(){
    return {
      link: [{ rel: 'stylesheet', type: 'text/css', href: '/top.css' }]
    }
  },
  data(){
    const r = Math.floor(Math.random()*255);
    const b = Math.floor(Math.random()*255);
    const g = Math.floor(Math.random()*255);
    const sliderItems = [
        { name: 'Red', value: r, color: 'red' },
        { name: 'Green', value: g, color: 'green' },
        { name: 'Blue', value: b, color: 'blue' }
      ];
    return {sliderItems};
  }
}

</script>
