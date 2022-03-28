<template>
    <div class="flex-item" id="commands">
        <h3>Commands</h3>
        <div class="command">
          Background
          <div class="code">/editprofile background {{backgroundColor.substring(1,7)}}</div>  
          <input type="hidden" id="bg" :value="'/editprofile background '+backgroundColor.substring(1,7)">
          <v-btn @click.stop.prevent="copyColor('bg')">Copy</v-btn>
        </div>
        <div class="command">
          Panels
          <div class="code">/editprofile theme {{panelColor.substring(1,7)}}</div>  
          <input type="hidden" id="panel" :value="'/editprofile theme ' + panelColor.substring(1,7)">
          <v-btn @click.stop.prevent="copyColor('panel')">Copy</v-btn>
        </div>
        <div class="ad-container flex-item" style="">
        <Adsense
          data-ad-client="ca-pub-4611357578399674"
          data-ad-slot="9274429601"
          data-ad-format="auto"
          data-full-width-responsive="true"
        >
        </Adsense>
      </div>
    </div>
</template>

<script>
export default {
    props: ['panelColor', 'backgroundColor'],
    methods: {
        copyColor (qs) {
          let testingCodeToCopy = document.querySelector('#'+qs)
          testingCodeToCopy.setAttribute('type', 'text')
          testingCodeToCopy.select()

          try {
            document.execCommand('copy');
          } catch (err) {
            console.log("Failed to copy!");
          }

          /* unselect the range */
          testingCodeToCopy.setAttribute('type', 'hidden')
          window.getSelection().removeAllRanges()
        },
    },
}
</script>

<style lang="scss" scoped>
    @import '../styles/commands.scss';
</style>