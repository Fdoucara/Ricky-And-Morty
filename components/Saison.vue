<template>
  <div class="saison">
    <div class="saison_btn" >
      <div class="saison_btn_item" v-for="(saison, index) in allEpTab" :key="index">
        <h3 class="saison_btn_item_title" :id="index" @click="showIndex">Saison {{ index + 1 }}</h3>
      </div>
    </div>

    <div class="container_episode">
      <div
        class="container_episode_item"
        v-for="(saison, index) in allEpTab"
        :key="index"
      >
        <Episode :saison="saison" :index="id" />
      </div>
    </div>
  </div>
</template>

<script>
import Episode from "./Episode.vue";
export default {
  name: "Saison",
  components: { Episode },
  data() {
    return {
      allEpTab: [],
      tabEpisodeS1: [],
      tabEpisodeS2: [],
      tabEpisodeS3: [],
      tabEpisodeS4: [],
      tabEpisodeS5: [],
      id: 0,
    };
  },
  methods: {
    allEpisodes() {
      // On récupère tous les épisodes issus des différentes pages de l'API
      for (let i = 1; i <= 3; i++) {
        this.$axios.$get("episode?page=" + i).then((episodes) => {
          // On réalise un tri en regroupant les épisodes par saison.
          for (const episode of episodes.results) {
            if (episode.episode.includes("S01")) {
              this.tabEpisodeS1.push(episode);
            } else if (episode.episode.includes("S02")) {
              this.tabEpisodeS2.push(episode);
            } else if (episode.episode.includes("S03")) {
              this.tabEpisodeS3.push(episode);
            } else if (episode.episode.includes("S04")) {
              this.tabEpisodeS4.push(episode);
            } else if (episode.episode.includes("S05")) {
              this.tabEpisodeS5.push(episode);
            }
          }
        });
      }
      // On insère les différents tableaux obtenus dans un grand tableau.
      this.allEpTab.push(
        this.tabEpisodeS1,
        this.tabEpisodeS2,
        this.tabEpisodeS3,
        this.tabEpisodeS4,
        this.tabEpisodeS5
      );
    },
    showIndex(e) {
      this.id = e.target.id;
      console.log(this.index);
    }
  },
  mounted() {
    this.allEpisodes();
  }
};
</script>