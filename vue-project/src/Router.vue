<script>
import PageUtama from './components/PageUtama.vue';
import PageDua from './components/PageDua.vue';

export default {
  components: {
    PageUtama, PageDua
  },
  data(){
    return{
      currentPage: "Utama",
      
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
