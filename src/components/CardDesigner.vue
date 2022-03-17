<template>
  <div>
    <Intro header="Card Designer" body="This Tool is currently being build..." />
    <v-row justify="center" class="pa-10">
      <div class="button-wrapper">
        <v-btn class="button" @click="$refs.file.click()">
          <input v-show="false" type="file" ref="file" @change="loadImage($event)" accept="image/*">
          Load image
        </v-btn>
      </div>
    </v-row>
    <v-row justify="center" class="pa-10">
      <cropper ref="cropper"
        class="cropper"
        @change="onChange"
        :debounce="false"
        :src="image.src"
        :stencil-props="{
        handlers: {},
        movable: false,
        scalable: false,
        aspectRatio: 300/500,
        }"
        :resize-image="{
          adjustStencil: false
        }"
        image-restriction="stencil" 
      />
      <div class="card-container">
        <img id="frame" src="../assets/cards/overlay.png" alt="">
        <Preview id="card"
          :image="result.image" 
          :coordinates="result.coordinates"

        />
        <div id="card" :style="{ backgroundImage : 'url(' + result.image + ')' }"></div>
      </div>
      <v-btn class="button ma-10" @click="crop()">
        Save Image
      </v-btn>

    </v-row>
  </div>
</template>

<script>
import { Cropper, Preview } from 'vue-advanced-cropper';
import 'vue-advanced-cropper/dist/style.css';
import { saveAs } from 'file-saver';
import Intro from './Intro.vue';

// This function is used to detect the actual image type, 
function getMimeType(file, fallback = null) {
  const byteArray = (new Uint8Array(file)).subarray(0, 4);
    let header = '';
    for (let i = 0; i < byteArray.length; i++) {
       header += byteArray[i].toString(16);
    }
  switch (header) {
        case "89504e47":
            return "image/png";
        case "47494638":
            return "image/gif";
        case "ffd8ffe0":
        case "ffd8ffe1":
        case "ffd8ffe2":
        case "ffd8ffe3":
        case "ffd8ffe8":
            return "image/jpeg";
        default:
            return fallback;
    }
}

export default {
  components: {
    Cropper, Preview, Intro
  },
  data: () => ({
    image: {
      src: null,
      type: null
    },
    result: {
      coordinates: null,
      image: null,
      dataUrl: null
    }
  }),
  methods: {
    crop() {
			const { canvas } = this.$refs.cropper.getResult();
			canvas.toBlob((blob) => {
				saveAs(blob);
			}, this.image.type);
		},
    onChange({ coordinates, image }) {
			this.result = {
				coordinates,
				image
			};
		},
    reset() {
      this.image = {
        src: null,
        type: null
      }
    },
    loadImage(event) {
      // Reference to the DOM input element
      const { files } = event.target;
      // Ensure that you have a file before attempting to read it
      if (files && files[0]) {
        // 1. Revoke the object URL, to allow the garbage collector to destroy the uploaded before file
        if (this.image.src) {
          URL.revokeObjectURL(this.image.src)
        }
        // 2. Create the blob link to the file to optimize performance:
        const blob = URL.createObjectURL(files[0]);
        
        // 3. The steps below are designated to determine a file mime type to use it during the 
        // getting of a cropped image from the canvas. You can replace it them by the following string, 
        // but the type will be derived from the extension and it can lead to an incorrect result:
        //
        // this.image = {
        //    src: blob;
        //    type: files[0].type
        // }
        
        // Create a new FileReader to read this image binary data
        const reader = new FileReader();
        // Define a callback function to run, when FileReader finishes its job
        reader.onload = (e) => {
          // Note: arrow function used here, so that "this.image" refers to the image of Vue component
          this.image = {
            // Set the image source (it will look like blob:http://example.com/2c5270a5-18b5-406e-a4fb-07427f5e7b94)
            src: blob,
            // Determine the image type to preserve it during the extracting the image from canvas:
            type: getMimeType(e.target.result, files[0].type),
          };
        };
        // Start the reader job - read file as a data url (base64 format)
        reader.readAsArrayBuffer(files[0]);
      }
    },
  },
  destroyed() {
    // Revoke the object URL, to allow the garbage collector to destroy the uploaded before file
    if (this.image.src) {
      URL.revokeObjectURL(this.image.src)
    }
  }
}
</script>

<style scoped lang="scss">
//FIXME: Outsource styles
.cropper {
  min-height: 500px;
  max-height: 600px;
  max-width: 400px;
  background: transparent;
}

.button-wrapper {
  display: block;
}

.card-container {
  height: 500px;
  width: 300px;
}

#frame {
  position: absolute;
  z-index: 1;
  max-height: 100%;
}
#card {
  height: 100%;
  width: 100%;
  background-size: contain;
}
</style>