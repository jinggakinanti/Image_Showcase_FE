<script>
import PageUtama from './components/PageUtama.vue';
import PageDua from './components/PageDua.vue';

export default {
  components: {
    PageUtama, PageDua
  },
  data(){
    return{
      images: [
        "https://images.unsplash.com/photo-1738444515789-0a1a4c4982dc?q=80&w=2831&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        "https://images.unsplash.com/photo-1738444515789-0a1a4c4982dc?q=80&w=2831&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        "https://images.unsplash.com/photo-1738444515789-0a1a4c4982dc?q=80&w=2831&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      ],
      currentPage: "Utama"
    };
  },
  methods: {
    setPage(newPage) {
      this.currentPage = newPage
    }
  },
};

</script>

<template>

    <section style="display: flex; gap: 16px;">

      <button style="margin-left: auto;" @click="setPage('Utama')">Page Utama</button>
      <button @click="setPage('Dua')" >Page Dua</button>

    </section>

    <div v-if="currentPage === 'Utama'">
      <PageUtama/>
    </div>

    <div v-else-if="currentPage === 'Dua'">
      <PageDua/>
    </div>
</template>


<style >
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
