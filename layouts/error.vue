<template>
  <v-row justify="center" align="center">
    <v-col cols="9" md="8" lg="6">
      <v-card class="top-card">
        <v-card-title class="text-h4" v-if="error.statusCode === 404">
          {{ pageNotFound }}
        </v-card-title>
        <v-card-title class="text-h4" v-else>
          {{ otherError }}
        </v-card-title>
        <v-card-text class="text-h5">We randomly picked a color from 16,777,216 colors. Do you like it?</v-card-text>
        <ColorCharts :items="items" />
        <SelectBars :sliderItems="sliderItems" :ButtonToTop="true" />
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  layout: 'empty',
  props: {
    error: {
      type: Object,
      default: null
    }
  },
  data () {
    const r = Math.floor(Math.random()*255);
    const b = Math.floor(Math.random()*255);
    const g = Math.floor(Math.random()*255);
    const sliderItems = [
        { name: 'Red', value: r, color: 'red' },
        { name: 'Green', value: g, color: 'green' },
        { name: 'Blue', value: b, color: 'blue' }
      ];
    const items = sliderItems.map(x => ({name: x.name, color: x.color, value: x.value, percent: 0}));
    const color = r.toString(16).padStart(2,'0')+g.toString(16).padStart(2,'0')+b.toString(16).padStart(2,'0')
    return {
      pageNotFound: '404 Not Found',
      otherError: 'An error occurred',
      sliderItems: sliderItems,
      items: items,
      color: color
    }
  },
  head () {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : this.otherError;
    const link = [{ rel: 'stylesheet', type: 'text/css', href: 'https://api.andirnu.ml/colors/bg.php?id='+this.color}];
    return {
      title, link
    }
  },
  mounted(){
    this.items = this.items.map(x => ({name: x.name, color: x.color, value: x.value, percent: x.value*100/255}));
  }
}
</script>

<style scoped>
h1 {
  font-size: 20px;
}
</style>
