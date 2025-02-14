<script>
export default {
  data(){
    return {
        deleteImage:"",
        hoveredImage:"",
        images: [],
        currPage:1,
        itemPerPage:3,
    };
  },
  computed: {
    paginatedImages() {
      const start = (this.currPage - 1) * this.itemPerPage;
      const end = start + this.itemPerPage;
      return this.images.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.images.length / this.itemPerPage);
    },
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
    },
    async deleteById(imageId){
        try{
            const response = await fetch(`http://localhost:8080/image/${imageId}`,{ method : "DELETE"});
            if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }
        this.fetchImages();
        this.deleteImage="";
        }catch (error){
            console.error("Error fetching images:", error);
        }
    },
    nextPage(){
        if (this.currPage < this.totalPages) {
        this.currPage++;
      }
    },
    prevPage(){
        if (this.currPage > 1){
            this.currPage--;
        }
    }
  },
  mounted() {
    this.fetchImages(); 
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
      <div v-for="image in paginatedImages" :key="image.id">
        <div class="image-container" @mouseover="hoveredImage = image.id" @mouseleave="hoveredImage = null" style="margin-bottom: 10px;">
            <img :src="image.url" alt="Image" width="200" />
            <button @click="deleteById(image.id)" v-show="hoveredImage === image.id" class="delete-button">Delete</button>
        </div>
      </div>
    </div>
    <div class="pagination">
      <button @click="prevPage" :disabled="currPage === 1" style="margin-right: 5px;">Prev</button>
      <span> Page {{ currPage }} of {{ totalPages }} </span>
      <button @click="nextPage" :disabled="currPage === totalPages" style="margin-left: 5px;">Next</button>
    </div>
</template>


<style >
.image-container{
    display: inline-block;
    position: relative;

}
img {
    transition: transform 0.3s ease-in-out;
}

img:hover {
    transform: scale(1.1);
}

.delete-button {
    position: absolute;
    bottom: 10px;
    left: 70px;
    background-color: black;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
    display: block;
}
</style>
