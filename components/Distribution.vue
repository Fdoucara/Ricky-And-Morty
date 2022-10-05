<template>
  <div class="saison_episode_focus_characters">
    <div
      class="saison_episode_focus_characters_card"
      v-for="(perso, index) in epPerso"
      :id="perso.id"
      :key="index"
    >
      <img
        class="saison_episode_focus_characters_card_image"
        :src="perso.image"
        alt="Photo personnage"
      />

      <div class="saison_episode_focus_characters_card_contain" :id="perso.id">
        <p>{{ perso.name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Distribution",
  props: ["epPerso"],
  data() {
    return {};
  },
};
</script>