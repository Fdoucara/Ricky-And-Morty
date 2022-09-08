<template>
  <div class="modale" v-if="toggle">
    <div class="overlay"></div>
    <div class="modale_header"></div>
    <div class="modale_body"></div>
    <div class="modale_footer"></div>
  </div>
</template>

<script>
export default {
  props: ["id", "toggle"],
  data() {
    return {};
  },
  methods: {
    recupData() {
      this.$axios.$get("episode/" + this.id).then((reponse) => {
        console.log(reponse);
      });
    },
  }
};
</script>