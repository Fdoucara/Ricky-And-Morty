<template>
  <div class="saison">
    <div class="saison_btn">
      <div
        class="saison_btn_item"
        v-for="(saison, index) in allEpTab"
        :key="index"
      >
        <h3 class="saison_btn_item_title" :id="index" @click="showIndex">
          Saison {{ index + 1 }}
        </h3>
      </div>
    </div>

      <div class="saison_episode">
        <div
          class="saison_episode_container"
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
      epInSaison: null,
      theSaison: null,
      tabEpisodeS1: [],
      tabEpisodeS2: [],
      tabEpisodeS3: [],
      tabEpisodeS4: [],
      tabEpisodeS5: [],
      element: null,
      bcgColor: [
        "linear-gradient(to right, #061700, #52c234)",
        "linear-gradient(to right, #F37335, #FDC830)",
        "linear-gradient(to right, #93291E, #ED213A)",
        "linear-gradient(to right, #ad5389, #3c1053)",
        "linear-gradient(to right, #0f0c29, #302b63, #24243e)",
      ],
      id: 0,
      display: false
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
      this.display = !this.display;
      // this.anim();
    },
    anim() {
      this.theSaison = gsap.utils.toArray(document.querySelectorAll(".container_episode"));
      this.epInSaison = gsap.utils.toArray(document.querySelectorAll(".container_episode_item"));
      
      const tl = gsap.timeline();

      tl
        .to(this.theSaison, { x: 0, width: '100%', duration: 1})
 0
    }
  },
  mounted() {
    this.$watch(
      () => this.id,
      () => {
        this.element = document.querySelector("html");
        this.element.style.background = this.bcgColor[this.id];
      }
    ),
      this.allEpisodes();
  },
};
</script>