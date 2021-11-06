<template>
  <v-row justify="center" align="center">
    <v-col cols="9" md="8" lg="6">
      <v-card class="ma-4">
        <v-row>
          <v-col v-if="$vuetify.breakpoint.name!=='xs'" cols="12" sm="6">
            <v-card-text class="pt-0 pb-0 text-h4 text-center text-sm-left">Color</v-card-text>
          </v-col>
          <v-col cols="12" sm="6">
            <v-card-text class="pt-0 pb-0 text-h4 text-center text-sm-right"> #{{color}}</v-card-text>
          </v-col>
        </v-row>
        <ColorCharts :items="items" />
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
    const sliderItems = [
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
    const items = sliderItems.map(x => ({name: x.name, color: x.color, value: x.value, percent: 0}));
    return {items,sliderItems,color};
  },
  head(){
    return {
      title: '#'+this.color,
      link: [{ rel: 'stylesheet', type: 'text/css', href: 'https://api.andirnu.ml/colors/bg.php?id='+this.color}]
    }
  },
  mounted(){
    this.items = this.items.map(x => ({name: x.name, color: x.color, value: x.value, percent: x.value*100/255}));
  }
}

</script>
