<template>
  <v-row justify="center" align="center">
    <v-col cols="9" md="8" lg="6">
      <v-card class="ma-4">
        <v-row>
          <v-col cols="12" md="6">
            <v-card-text class="pt-0 pb-0 text-h4 text-center text-md-left">Color</v-card-text>
          </v-col>
          <v-col cols="12" md="6">
            <v-card-text class="pt-0 pb-0 text-h4 text-center text-md-right"> #{{color}}</v-card-text>
          </v-col>
        </v-row>
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
        <SelectBars :sliderItems="sliderItems" :ButtonToTop="true" />
      </v-card>
    </v-col>
  </v-row>
</template>

<script>

function num(s){
  let ret = 0;
  for(let i=0; i<s.length; ++i){
    ret *= 16;
    switch(s[i]){
      case 'F':
      ret += 1;
      case 'E':
      ret += 1;
      case 'D':
      ret += 1;
      case 'C':
      ret += 1;
      case 'B':
      ret += 1;
      case 'A':
      ret += 1;
      case '9':
      ret += 1;
      case '8':
      ret += 1;
      case '7':
      ret += 1;
      case '6':
      ret += 1;
      case '5':
      ret += 1;
      case '4':
      ret += 1;
      case '3':
      ret += 1;
      case '2':
      ret += 1;
      case '1':
      ret += 1;
      case '0':
      break;
      default:
      return -1;
    }
  }
  return ret;
}

export default {
  async asyncData({error, params }) {
    const color = params.color.toUpperCase();
    let r,g,b;
    if(color.length === 6 ){
      r = num(color.substring(0,2));
      g = num(color.substring(2,4));
      b = num(color.substring(4,6));
    }else if(color.length === 3){
      r = num(color.substring(0,1))*17;
      g = num(color.substring(1,2))*17;
      b = num(color.substring(2,3))*17;
    }else{
      error({ statusCode: 404, message: 'Not Found' });
    }
    try{
      if(r<0 || g<0 || b<0){
        throw new Error("入力が不正です。");
      }
    }catch(e){
      error({ statusCode: 404, message: 'Not Found' });
    }
    const vals = [
      {
        value: r,
        name: 'Red',
        color: 'red'
      },
      {
        value: g,
        name: 'Green',
        color: 'green'
      },
      {
        value: b,
        name: 'Blue',
        color: 'blue'
      }
    ];
    const items = vals.map(x => ({name: x.name, color: x.color, value: x.value, percent: 0}));
    const sliderItems = [
        { label: 'Red', value: r, color: 'red' },
        { label: 'Green', value: g, color: 'green' },
        { label: 'Blue', value: b, color: 'blue' }
      ];
    return {items,color,sliderItems};
  },
  mounted(){
    this.items = this.items.map(x => ({name: x.name, color: x.color, value: x.value, percent: x.value*100/255}));
  },
  head(){
    return {
      title: '#'+this.color,
      link: [{ rel: 'stylesheet', type: 'text/css', href: 'https://api.andirnu.ml/colors/bg.php?id='+this.color}]
    }
  }
}

</script>
