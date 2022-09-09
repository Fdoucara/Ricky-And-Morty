<template>
  <div>
    <Loader />
    <Header />
    <Saison />
  </div>
</template>

<script>
import Header from "../components/Header.vue";
import Loader from "../components/Loader.vue";
export default {
  name: "IndexPage",
  components: { Header, Loader },
};
</script>
