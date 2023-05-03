<template>
  <div>
    <input
      ref="file"
      type="file"
      accept="image/*"
      @change="fileChange"
      hidden
    />
    <div
      class="drag-drop-zone"
      @click="upload()"
      @dragover="dragover"
      @dragleave="dragleave"
      @drop="drop"
    >
      <template v-if="isDragging">
        <div class="icon">

          <svg style="color: white" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg"><path fill="white" d="M544 864V672h128L512 480 352 672h128v192H320v-1.6c-5.376.32-10.496 1.6-16 1.6A240 240 0 0 1 64 624c0-123.136 93.12-223.488 212.608-237.248A239.808 239.808 0 0 1 512 192a239.872 239.872 0 0 1 235.456 194.752c119.488 13.76 212.48 114.112 212.48 237.248a240 240 0 0 1-240 240c-5.376 0-10.56-1.28-16-1.6v1.6H544z"></path></svg>

        </div>
        <p>Drop to upload</p>
      </template>
      <img v-else-if="previewImg" class="preview" :src="previewImg" />
      <template v-else>
        <div class="icon">

          <svg style="color: white" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg"><path fill="white" d="M544 864V672h128L512 480 352 672h128v192H320v-1.6c-5.376.32-10.496 1.6-16 1.6A240 240 0 0 1 64 624c0-123.136 93.12-223.488 212.608-237.248A239.808 239.808 0 0 1 512 192a239.872 239.872 0 0 1 235.456 194.752c119.488 13.76 212.48 114.112 212.48 237.248a240 240 0 0 1-240 240c-5.376 0-10.56-1.28-16-1.6v1.6H544z"></path></svg>

        </div>
        <p>Click to upload</p>
        <p class="sub-text">or drag and drop image</p>
      </template>
    </div>
  </div>
</template>



<script>
export default {
  props: {
    value: {
      required: true,
    },
  },
  data() {
    return {
      isDragging: false,
      imageResults: [], // Add this data property to store the received images and strings
    };
  },
  computed: {
    previewImg() {
      if (this.value) {
        return URL.createObjectURL(this.value);
      }
      return null;
    },
  },
  methods: {
    upload() {
      this.$refs.file.click();
    },
    fileChange(e, isDrop = false) {
      const file = isDrop ? e.dataTransfer.files[0] : e.target.files[0];
      this.$emit("input", file);
    },
    dragover(e) {
      e.preventDefault();
      this.isDragging = true;
    },
    dragleave() {
      this.isDragging = false;
    },
    async drop(e) {
      e.preventDefault();
      this.fileChange(e, true);
      this.isDragging = false;
    
      // Sending the image to the Flask server
      const formData = new FormData();
      formData.append("image", this.value);
      
      try {
        // Replace '/predict' with your server URL followed by the API endpoint
        const response = await fetch("https://my-image-server.com/predict", {
          method: "POST",
          body: formData,
        });
        if (response.ok) {
          const data = await response.json();
          // Update the component's data with the received images and strings
          this.imageResults = data;
        } 
        else {
          console.error("Error uploading image:", response.statusText);
        }
      } 
      catch (error) {
        console.error("Error uploading image:", error);
      }
    },
  },
};
</script>



<style scoped>
.drag-drop-zone {
  width: 200px;
  height: 70px;
  border: 1px solid #e5e5e5;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.drag-drop-zone .preview {
  width: 100%;
  height: 100%;
  object-fit: contain;
}
.drag-drop-zone .icon {
  width: 25px;
  height: 20px;
}
.drag-drop-zone .sub-text {
  font-size: 12px;
}
</style>