<template>
  <v-wrapper>
    <v-row
      v-for="(item, index) in sliderItems"
      :key="index" class="mb-0 mt-0">
      <v-col cols="2" md="1" class="mb-0 mt-0 mr-0 pr-0 pb-0 pt-0">
        <v-card-text :style="'color: '+item.color+';'" class="text-center text-h6 ma-0 pl-0 pr-0 pt-2 pb-0">{{item.label.substring(0,1)}}</v-card-text>
      </v-col>
      <v-col cols="10" md="11" class="mb-0 mt-0 ml-0 pl-0 pb-0 pt-0">
        <v-slider
          v-model="item.value"
          :color="item.color"
          :track-color="item.color"
          :thumb-color="item.color"
          :thumb-label="true"
          min="0" max="255"
          :hide-details="true" :dense="true"
          class="mt-2 mb-2 ml-0 mr-2">
        </v-slider>
      </v-col>
    </v-row>
    <v-wrapper class="d-flex justify-center pt-0 pb-4">
      <v-btn v-bind:color="'rgb('+sliderItems[0].value+','+sliderItems[1].value+','+sliderItems[2].value+')'" v-bind:to="'/'+sliderItems[0].value.toString(16).padStart(2,'0')+sliderItems[1].value.toString(16).padStart(2,'0')+sliderItems[2].value.toString(16).padStart(2,'0')">
        <span v-bind:style="'color: rgb('+((sliderItems[0].value+128)%256)+','+((sliderItems[1].value+128)%256)+','+((sliderItems[2].value+128)%256)+');'" class="mr-2">
          Go to #{{sliderItems[0].value.toString(16).padStart(2,'0')}}{{sliderItems[1].value.toString(16).padStart(2,'0')}}{{sliderItems[2].value.toString(16).padStart(2,'0')}}
        </span>
      </v-btn>
      <v-btn v-if="ButtonToTop" to="/" class="ml-2">
        Go to Top
      </v-btn>
    </v-wrapper>
  </v-wrapper>
</template>

<script>
export default {
  props: ['sliderItems','ButtonToTop']
}
</script>