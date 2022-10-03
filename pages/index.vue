<template>
  <div>
    <Loader />
    <Header />
    <Saison />
    <Distribution />
    <Footer />
  </div>
</template>

<script>
import Header from "../components/Header.vue";
import Loader from "../components/Loader.vue";
import Footer from "../components/Footer.vue";
export default {
  name: "IndexPage",
  components: { Header, Loader, Footer },
};
</script>
