<template>
  <div class="designer">
    <div id="intro">
      <h2>Welcome to Midari Profile Studio</h2>
      <p>
        Customize your profile and run the commands in any channel that has access to the Midari Bot.<br>
        Your settings are not saved locally. Refreshing the page will reset all colors!<br>
        This tool is still work in progress!
      </p>
    </div>
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
      <BadgeSelector />
    </div>
  </div>
</template>

<script>
import Preview from './Preview.vue';
import Commands from './Commands.vue';
import BadgeSelector from './BadgeSelector.vue';

export default {
  name: 'Designer',
  components: { Preview, Commands, BadgeSelector },
  props: {
    msg: String
  },
  data: ()=>({
    panelColor: '3D985D',
    backgroundColor: '303144'
  })
}
</script>

<style scoped lang="scss">
    @import '../styles/specifics.scss';
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>
