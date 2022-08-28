<template>
  <div class="container_episode_item_container">
    <div
      class="container_episode_item_container_card"
      v-for="episode in saison"
      :key="episode.name"
    >
      <div class="container_episode_item_container_card_image">
        <img
          src="https://tse1.mm.bing.net/th?id=OIP.M9bPDxpA_344QDwcOa-uRgHaEK&pid=Api&P=0"
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
  props: ["saison"],
  data() {
    return {};
  },
};
</script>