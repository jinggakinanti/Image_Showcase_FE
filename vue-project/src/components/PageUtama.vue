<script>
export default {
  data(){
    return {
        images: [
            "https://images.unsplash.com/photo-1738444515789-0a1a4c4982dc?q=80&w=2831&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
            "https://images.unsplash.com/photo-1738444515789-0a1a4c4982dc?q=80&w=2831&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
            "https://images.unsplash.com/photo-1738444515789-0a1a4c4982dc?q=80&w=2831&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        ],
    };
  },
  methods: {
    
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
      <div v-for="(image, index) in images" :key="index">
        <img :src="image" alt="Image" width="200" />
      </div>
    </div>
</template>


<style >
</style>
