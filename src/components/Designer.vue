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
      <div id="preview" class="flex-item">
        <h3>Preview</h3>
        <div class="profile-container">
          <div class="profile" :style="{backgroundColor: backgroundColor}">
            <svg class="overlay-panels" width="100%" height="100%" viewBox="0 0 800 500" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:2;">
                  <g>
                      <g id="TopBar" transform="matrix(7.20721,0,0,1.325,-79.2793,-24.85)" :style="{fill:panelColor}">
                          <rect x="11" y="58" width="111" height="40" style="fill-opacity:0.75;"/>
                      </g>
                      <g id="MainCard" transform="matrix(2.3908,0,0,3.80899,-63.8046,-414.112)" :style="{fill:panelColor}">
                          <path d="M130,148.662C130,147.193 128.1,146 125.759,146L47.241,146C44.9,146 43,147.193 43,148.662L43,232.338C43,233.807 44.9,235 47.241,235L125.759,235C128.1,235 130,233.807 130,232.338L130,148.662Z" style="fill-opacity:0.75;"/>
                      </g>
                      <g id="Description" transform="matrix(5.86207,0,0,1.07865,-0.0689655,-15.4831)" :style="{fill:panelColor}">
                          <path d="M130,155.792C130,150.388 129.193,146 128.198,146L44.802,146C43.807,146 43,150.388 43,155.792L43,225.208C43,230.612 43.807,235 44.802,235L128.198,235C129.193,235 130,230.612 130,225.208L130,155.792Z" style="fill-opacity:0.75;"/>
                      </g>
                      <g id="Badges" transform="matrix(5.86207,0,0,1.07865,-0.0689655,83.5169)" :style="{fill:panelColor}">
                          <path d="M130,156.173C130,150.558 129.161,146 128.128,146L44.872,146C43.839,146 43,150.558 43,156.173L43,224.827C43,230.442 43.839,235 44.872,235L128.128,235C129.161,235 130,230.442 130,224.827L130,156.173Z" style="fill-opacity:0.75;"/>
                      </g>
                      <g id="Showcase" transform="matrix(5.86207,0,0,1.58427,-0.0689655,108.697)" :style="{fill:panelColor}">
                          <path d="M130,152.767C130,149.032 129.181,146 128.171,146L44.829,146C43.819,146 43,149.032 43,152.767L43,228.233C43,231.968 43.819,235 44.829,235L128.171,235C129.181,235 130,231.968 130,228.233L130,152.767Z" style="fill-opacity:0.75;"/>
                      </g>
                  </g>
            </svg>
            <div class="overlay-icons"></div>
            <img class="user-image" src="../assets/user.webp" alt="">
          </div>
        </div>
      </div>
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
      <div class="flex-item" id="commands">
        <h3>Commands</h3>
        <div class="command">
          Background
          <div class="code">mep b {{backgroundColor.substring(1,7)}}</div>  
          <input type="hidden" id="bg" :value="'mep b '+backgroundColor.substring(1,7)">
          <v-btn @click.stop.prevent="copyColor('bg')">Copy</v-btn>
        </div>
        <div class="command">
          Panels
          <div class="code">mep t {{panelColor.substring(1,7)}}</div>  
          <input type="hidden" id="panel" :value="'mep t ' + panelColor.substring(1,7)">
          <v-btn @click.stop.prevent="copyColor('panel')">Copy</v-btn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Designer',
  props: {
    msg: String
  },
  data: ()=>({
    panelColor: '3D985D',
    backgroundColor: '303144'
  }),
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

#intro {
  h2 {
    text-align: center;
  }

  p {
    margin-bottom: 0;
  }

  width: 50%;
  margin: 0 auto;
  padding: 25px;
}

.profile-container {
  width: 900px;
  max-width: 100%;
  margin: 0 auto;
  resize: horizontal;
  align-content: center;
  justify-content: center;
  //height: calc(45vh - 16px);
  box-sizing: border-box;
  display: inline-block;

  .profile {
    position: relative;
    width: 100%;
    padding-bottom: 62.5%;
    background-color: red;
  }
  .overlay-panels {
    position:absolute;
    width:  100%;
    height: 100%;
    left: 0;
  }

  .overlay-icons {
    position: absolute;
    width:  100%;
    height: 100%;
    left: 0;
    background-size:cover;
    background-image: url('../assets/midari_overlay.png');
  }

  .user-image {
    position: absolute;
    left: 1.6%;
    top:  2.3%;
    width: 14.5%;
    border-radius: 100%;
  }
}

.flex-container {
  max-width: 100%;
  width: 100%;
  display: inline-flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-evenly;
  margin-bottom: 25px;
}

.flex-item {
  max-width: 100%;
}

#preview {
  order: -1;
  //flex-basis: 50%;
}
#commands {
  min-width: 300px;
  align-self: flex-start;

  .command {
    position: relative;
    margin: 20px;
  }

  button {
    position: absolute;
    right: 0px;
    bottom: 6px;
    height: 45px;
  }
}

.code {
  background-color: #0a0a0a;
  border-radius: 5px;
  padding: 11px;
  width: 100%;
  display: inline-block;
  margin: 5px 0;
  font-family: monospace;
}



h3 {
  margin: 25px 0 0;
  text-align: center;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

p {
  padding: 25px;
}
</style>
