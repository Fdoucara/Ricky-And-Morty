<template>
  <div class="saison" id="saison">
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
      tabEpisodeS1: [],
      tabEpisodeS2: [],
      tabEpisodeS3: [],
      tabEpisodeS4: [],
      tabEpisodeS5: [],
      id: 0,
      oldId: 0
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
      this.anim();
      this.oldId = this.id;
    },
    anim() {
      this.epInSaison = gsap.utils.toArray(document.querySelectorAll(".saison_episode_container"));
      
      const tl = gsap.timeline();

      if(this.id == this.oldId) {
        tl
        .to(this.epInSaison[this.id], { 
          keyframes: [ 
            { x: "-5", duration: "0.1", rotate: "-2" },
            { x: "5", duration: "0.1", rotate: "2" },
            { x: "-5", duration: "0.1", rotate: "-2" },
            { x: "0", duration: "0.1", rotate: "0" }
         ]
        })
      } else {
        tl
        .to(this.epInSaison[this.oldId], { autoAlpha: 0, scale: '0.6', duration: 0.1 })
        .to(this.epInSaison[this.id], { autoAlpha: 1, scale: '1', duration: 0.7 })
      }
    }
  },
  mounted() {
    this.allEpisodes();
  },
};
</script>