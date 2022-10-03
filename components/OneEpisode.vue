<template>
  <div>
    <div class="saison_episode_focus_container">
      <div class="saison_episode_focus_container_card">
        <img
          class="saison_episode_focus_container_card_image"
          :src="card_image"
          alt="Rick et Morty"
        />

        <div class="saison_episode_focus_container_card_contain">
          <p>{{ epName }}</p>
          <p>{{ epDate }}</p>
        </div>
      </div>

      <div class="saison_episode_focus_container_button">
        <div class="saison_episode_focus_container_button_item">
          <p>Lecture épisode {{ epNum }}</p>
        </div>
        <div class="saison_episode_focus_container_button_item">
          <p>Liste de favoris</p>
        </div>
        <div class="saison_episode_focus_container_button_item">
          <p>Télécharger l'épisode</p>
        </div>
      </div>
    </div>

    <h2 class="saison_episode_focus_characters_title"> Personnages dans l'episode </h2>
    <Distribution :epPerso="epPerso" />
  </div>
</template>

<script>
import Distribution from "./Distribution.vue";
export default {
  props: ["id", "card_image"],
  data() {
    return {
      info: null,
      epName: "",
      epNum: "",
      epDate: "",
      epPerso: [],
    };
  },
  methods: {
    getEpInfo() {
      (this.epPerso = []),
        this.$axios.$get("episode/" + this.id).then((reponse) => {
          this.info = reponse;
          this.epName = reponse.name;
          this.epNum = reponse.episode;
          this.epDate = reponse.air_date;
          for (let perso of reponse.characters) {
            let idPerso = new URL(perso);
            this.$axios.$get(idPerso).then((reponse) => {
              this.epPerso.push(reponse);
            });
          }
          console.log(this.epPerso);
        });
    },
  },
  mounted() {
    this.getEpInfo();
    this.$watch(
      () => this.id,
      () => {
        this.id = this.id;
        this.getEpInfo();
      }
    );
  },
  components: { Distribution },
};
</script>