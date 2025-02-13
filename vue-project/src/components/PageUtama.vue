<script>
export default {
  data(){
    return {
        images: [],
    };
  },
  methods: {
    async fetchImages() {
      try {
        const response = await fetch("http://localhost:8080/image"); 
        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }
        const responseBody = await response.json(); 
        this.images = responseBody.data;
      } catch (error) {
        console.error("Error fetching images:", error);
      }
    }
  },
  mounted() {
    this.fetchImages(); // Fetch images when the component is mounted
  }
};

</script>

<template>
    <div>
        <h2>Page Utama</h2>
    </div>
    <div v-if="images.length === 0">No images found.
    </div>
    <div v-else>
      <div v-for="image in images" :key="image.id">
        <img :src="image.url" alt="Image" width="200" />
      </div>
    </div>
</template>


<style >
</style>
