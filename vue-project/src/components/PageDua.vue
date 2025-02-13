<script>
export default {
  data() {
    return {
      newImage: "", 
      searchId: "", 
      images: [], 
      searchedImage: null, 
    };
  },
  methods: {
    async fetchImageById() {
      if (!this.searchId) {
        alert("Please enter an ID");
        return;
      }
      try {
        const response = await fetch(`http://localhost:8080/image/${this.searchId}`);
        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }
        const data = await response.json();
        this.searchedImage = data.data; 
        console.log("Fetched image:", data);
      } catch (error) {
        console.error("Error fetching image:", error);
      }
    },

    async addImage() {
      if (!this.newImage) {
        alert("Please enter an image URL");
        return;
      }
      try {
        const response = await fetch(`http://localhost:8080/image?url=${this.newImage}`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ url: this.newImage }),
        });

        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }

        console.log(await response.json())

        this.newImage = ""; 
      } catch (error) {
        console.error("Error inserting image:", error);
      }
    },

    async deleteImages() {
      try {
        const response = await fetch("http://localhost:8080/image", { method: "DELETE" });
        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }
        console.log("All images deleted.");
        alert("All images deleted successfully!");
        this.images = []; 
      } catch (error) {
        console.error("Error deleting images:", error);
      }
    },
  },
};
</script>

<template>
  <div>
    <h2>Page Dua</h2>
  </div>

  <div>
    <h3>Insert New Image</h3>
    <input v-model="newImage" placeholder="Image URL" />
    <button @click="addImage">Insert</button>
  </div>

  <div>
    <h3>Search Image By ID</h3>
    <input v-model="searchId" placeholder="Image ID" />
    <button @click="fetchImageById">Search</button>
  </div>

  <div v-if="searchedImage">
    <img :src="searchedImage.url" alt="Searched Image" width="200" />
  </div>

  <div>
    <h3>Delete All Images</h3>
    <button @click="deleteImages" style="width: 210px;">Delete</button>
  </div>
</template>
