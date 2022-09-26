<template>
  <div class="saison_episode_focus_characters_container">
    <div
      class="saison_episode_focus_characters_container_card"
      v-for="(perso, index) in epPerso"
      :id="perso.id"
      :key="index"
    >
      <img
        class="saison_episode_focus_characters_container_card_image"
        :src="perso.image"
        alt="Photo personnage"
      />

      <div class="saison_episode_focus_characters_container_card_contain" :id="perso.id">
        <p>{{ perso.name }}</p>
        <p>{{ perso.species }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Distribution',
  props: ['epPerso'],
  data() {
    return {};
  },
};
</script>