<template>
  <div class="saison_episode_focus_container">
    
  </div>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      
    }
  },
  methods: {
    getEpInfo() {
      this.$axios.$get("episode/" + this.id)
        .then((reponse) => {
          // console.log(reponse);
        })
    }
  },
  mounted() {    
    this.getEpInfo();
    this.$watch(() => this.id, () => {
      this.id = this.id;
      this.getEpInfo();
    });
  },
}
</script>