<template>
  <div class="designer">
    <Intro header="Welcome to Midari Profile Studio" :body="introBody" />
    <div class="flex-container"> <!-- ToDo: fix container -->
      <Preview :panelColor="panelColor" :backgroundColor="backgroundColor" />
      <div class="flex-item">
        <h3>Background</h3>
        <v-color-picker style="margin: 0 auto;"  
          v-model="backgroundColor"
          hide-inputs
          canvas-height="200"
          dot-size="25"
          swatches-max-height="100"
          elevation="5"
          mode="hexa"
        ></v-color-picker>
      
        <h3>Panels</h3>
        <v-color-picker style="margin: 0 auto;" 
          v-model="panelColor"
          hide-inputs
          canvas-height="200"
          dot-size="25"
          swatches-max-height="100"
          elevation="5"
          mode="hexa"
        ></v-color-picker>
      </div>
      <Commands :panelColor="panelColor" :backgroundColor="backgroundColor" />
    </div>
  </div>
</template>

<script>
import Preview from './Preview.vue';
import Commands from './Commands.vue';
import Intro from './Intro.vue';

export default {
  name: 'Designer',
  components: { Preview, Commands, Intro },
  props: {
    msg: String
  },
  data: ()=>({
    panelColor: '3D985D',
    backgroundColor: '303144',
    introBody: `Customize your profile and run the commands in any channel that has access to the Midari Bot.<br>
                Your settings are not saved locally. Refreshing the page will reset all colors!<br>
                This tool is still work in progress!`
  })
}
</script>

<style scoped lang="scss">
    @import '../styles/specifics.scss';
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>
