<template>
  <div>
    <Intro header="Card Designer" body="This Tool is currently being built...<br/>Mobile cropper might behave weird. <br/>Known Issues: <br/>- (mobile) Moving cropper to the right changes tabs <br/>- (mobile) Pinch to zoom affects page instead of crop area <br>- Initial crop area doesn't cover the maximum size possible" />
    <v-row justify="center" class="pa-10">
      <div class="button-wrapper">
        <input
          ref="input"
          type="file"
          name="image"
          accept="image/*"
          @change="setImage"
        />
        <v-btn x-large class="button ma-10" @click="showFileChooser()">
          Open Image
          <v-icon right dark>
            mdi-cloud-upload
          </v-icon>
        </v-btn>
      </div>
    </v-row>
    <v-row justify="center">
      <section class="cropper-area">
        <div class="img-cropper">
          <vue-cropper
            ref="cropper"
            :src="imgSrc"
            preview=".custom-preview"
            :viewMode="2"
            :zoomable="true"
            :aspectRatio="3/5"
          />
        </div>
      </section>

      <section class="preview-area">
        <div class="card-container">
          <img id="frame" src="../assets/cards/overlay.png" alt="">
          <div class="custom-preview" />
        </div>
      </section>
    </v-row>
    <v-row justify="center" class="pa-10">
      <v-btn x-large class="button ma-10" @click="cropImage()">
        Save Image
        <v-icon right dark>
          mdi-cloud-download
        </v-icon>
      </v-btn>
    </v-row>
  </div>
</template>

<script>

import { saveAs } from 'file-saver';
import Intro from './Intro.vue';
import VueCropper from 'vue-cropperjs';
import 'cropperjs/dist/cropper.css';

// This function is used to detect the actual image type, 

export default {
  components: {
    VueCropper, Intro
  },
  data: () => ({
    imgSrc: require("../assets/cards/akashi_placeholder.jpg"),
    cropImg: '',
    data: null
  }),
  methods: {
    cropImage() {
      // get image data for post processing, e.g. upload or setting image src
      this.cropImg = this.$refs.cropper.getCroppedCanvas().toDataURL();
      this.$refs.cropper.getCroppedCanvas().toBlob(blob => {
        let i = new FormData()
        i.append('picture', blob)    
        console.log(i)
        saveAs(blob, "custom-card");
      })

    },
    crop() {
			const { canvas } = this.$refs.cropper.getResult();
			canvas.toBlob((blob) => {
				saveAs(blob);
			}, this.image.type);
		},

    reset() {
      this.image = {
        src: null,
        type: null
      }
    },
    setImage(e) {
      const file = e.target.files[0];

      if (file.type.indexOf('image/') === -1) {
        alert('Please select an image file');
        return;
      }

      if (typeof FileReader === 'function') {
        const reader = new FileReader();

        reader.onload = (event) => {
          this.imgSrc = event.target.result;
          // rebuild cropperjs with the updated source
          this.$refs.cropper.replace(event.target.result);
        };

        reader.readAsDataURL(file);
      } else {
        alert('Sorry, FileReader API not supported');
      }
    },
    showFileChooser() {
      this.$refs.input.click();
    }
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

.cropper-area {
  padding-right: 25px;
}

.img-cropper {
  max-width: 50%;
}

input[type="file"] {
  display: none;
}

.custom-preview {
  width: 100%;
  height: 100%;
  overflow: hidden;
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