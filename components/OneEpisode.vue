<template>
    <div
        class="saison_episode_focus_container_card"
      >
        <img
          class="saison_episode_focus_container_card_image"
          :src="card_image"
          alt="Rick et Morty"
        />

        <div
          class="saison_episode_focus_container_card_contain"
        >
          <!-- <p> {{ this.info.episode }} </p> -->
          <!-- <p> {{ this.info.air_date }} </p> -->
        </div>
      </div>
</template>

<script>
export default {
  props: ['id', 'card_image'],
  data() {
    return {
      // card_image: [
      //   "https://tse2.mm.bing.net/th?id=OIP.AtO8nvarM_zTBDYuUwTWKwHaEK&pid=Api&P=0",
      //   "https://tse4.mm.bing.net/th?id=OIP.KEwJQvR80SIf-V10nKy9JgHaEK&pid=Api&P=0",
      //   "https://tse3.mm.bing.net/th?id=OIP.vLy8rK_wxlUYESYUbBpo_wHaEK&pid=Api&P=0",
      //   "https://tse4.mm.bing.net/th?id=OIP.L32Q3mMbsVu931uN1KmTgAHaEK&pid=Api&P=0",
      //   "https://tse1.mm.bing.net/th?id=OIP.if2yG2TSxJfI5XlGxUgivQHaEK&pid=Api&P=0",
      // ],
      info: null
    }
  },
  methods: {
    getEpInfo() {
      this.$axios.$get("episode/" + this.id)
        .then((reponse) => {
          this.info = reponse;
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