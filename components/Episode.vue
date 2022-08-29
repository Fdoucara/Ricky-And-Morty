<template>
  <div class="container_episode_item_container">
    <div
      class="container_episode_item_container_card"
      v-for="episode in saison"
      :key="episode.name"
    >
      <div class="container_episode_item_container_card_image">
        <img
          :src="card_image[index]"
          alt="Rick et Morty"
        />
      </div>

      <div class="container_episode_item_container_card_body">
        <p>{{ episode.episode }}</p>
        <p>{{ episode.air_date }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Episode",
  props: ["saison", "index"],
  data() {
    return {
      card_image: [
        'https://tse2.mm.bing.net/th?id=OIP.AtO8nvarM_zTBDYuUwTWKwHaEK&pid=Api&P=0',
        'https://tse4.mm.bing.net/th?id=OIP.KEwJQvR80SIf-V10nKy9JgHaEK&pid=Api&P=0',
        'https://tse3.mm.bing.net/th?id=OIP.vLy8rK_wxlUYESYUbBpo_wHaEK&pid=Api&P=0',
        'https://tse4.mm.bing.net/th?id=OIP.L32Q3mMbsVu931uN1KmTgAHaEK&pid=Api&P=0',
        'https://tse1.mm.bing.net/th?id=OIP.if2yG2TSxJfI5XlGxUgivQHaEK&pid=Api&P=0'
      ]
    };
  },
  methods: {
    changeImage() {
      console.log('tap')
    }
  },
  mounted() {
    console.log(this.index);
    // this.$watch(
    //   () => this.index,
    //   () => {
    //     // this.changeImage();
    //     console.log('ok ', this.index);
    //   }
    // )
  }
};
</script>