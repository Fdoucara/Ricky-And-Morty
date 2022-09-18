<template>
  <div>
    <div class="saison_episode_focus_container_card">
      <img
        class="saison_episode_focus_container_card_image"
        :src="card_image"
        alt="Rick et Morty"
      />

      <div class="saison_episode_focus_container_card_contain">
        <p>{{ epNum }}</p>
        <p>{{ epDate }}</p>
        <p>{{ epName }}</p>
      </div>
    </div>

    <div class="saison_episode_focus_container_distribution">
      <h2 class="saison_episode_focus_container_title"> Distribution </h2>
    </div>
  </div>
</template>

<script>
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
      this.$axios.$get("episode/" + this.id).then((reponse) => {
        this.info = reponse;
        this.epName = reponse.name;
        this.epNum = reponse.episode;
        this.epDate = reponse.air_date;
        for (let perso of reponse.characters) {
          this.epPerso.push(perso);
        }
        console.log("Perso ", this.epPerso);
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
};
</script>