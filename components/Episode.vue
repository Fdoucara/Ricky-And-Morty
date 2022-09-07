<template>
  <div class="saison_episode_container_item">
    <div
      class="saison_episode_container_item_card"
      v-for="(episode, index) in saison"
      :key="index"
    >
      <div class="saison_episode_container_item_card_image">
        <img :src="card_image[2]" alt="Rick et Morty" />
      </div>

      <div class="saison_episode_container_item_card_body">
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
        "https://tse2.mm.bing.net/th?id=OIP.AtO8nvarM_zTBDYuUwTWKwHaEK&pid=Api&P=0",
        "https://tse4.mm.bing.net/th?id=OIP.KEwJQvR80SIf-V10nKy9JgHaEK&pid=Api&P=0",
        "https://tse3.mm.bing.net/th?id=OIP.vLy8rK_wxlUYESYUbBpo_wHaEK&pid=Api&P=0",
        "https://tse4.mm.bing.net/th?id=OIP.L32Q3mMbsVu931uN1KmTgAHaEK&pid=Api&P=0",
        "https://tse1.mm.bing.net/th?id=OIP.if2yG2TSxJfI5XlGxUgivQHaEK&pid=Api&P=0",
      ],
    };
  },
};
</script>