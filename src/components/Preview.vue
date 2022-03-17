<template>
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
</template>

<script>
export default {
    props: ['panelColor', 'backgroundColor']
}
</script>

<style scoped lang="scss">
    @import '../styles/preview.scss';
</style> 
