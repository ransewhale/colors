<template>
  <v-wrapper>
    <v-row class="ml-2 mr-2 mt-0">
      <v-col
        v-for="(item, index) in items"
        :key="index" 
        cols="12" md="4" class="ma-0">
        <v-card-text :class="item.color+'--text pb-0 pt-0 text-center text-h6'">{{item.name}}</v-card-text>
        <v-card flat class="d-flex justify-center">
          <v-progress-circular
            :rotate="-90"
            :value="item.percent"
            :size="150"
            :width="25"
            :color="item.color">
            <v-card-text  class="ma-0 pa-0 text-h4"> {{item.value}} </v-card-text>
          </v-progress-circular>
        </v-card>
      </v-col>
    </v-row>
  </v-wrapper>
</template>

<script>
export default {
  props: ['items']
}
</script>