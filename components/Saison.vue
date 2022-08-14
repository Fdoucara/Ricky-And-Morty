<template>
  <div>
    <div class="container_saison">
      <img src="../assets/images/leftGun.png" class="slide_photo" @click="saisonLeft">
      <div class="slide">
        <div
          class="slide_body"
          v-for="(saison, index) in allEpTab"
          :key="index"
        >
          <h2 class="slide_body_title">Saison {{ index + 1 }}</h2>
        </div>
      </div>
      <img src="../assets/images/rightGun.png" class="slide_photo" @click="saisonRight">
    </div>

    <div class="container_episode">
      <div class="episode" v-for="(saison, index) in allEpTab" :key="index">
        <Episode :saison="saison" />
      </div>
    </div>
  </div>
</template>

<script>
import Episode from "./Episode.vue";
export default {
  name: "Saison",
  data() {
    return {
      allEpTab: [],
      tabEpisodeS1: [],
      tabEpisodeS2: [],
      tabEpisodeS3: [],
      tabEpisodeS4: [],
      tabEpisodeS5: [],
      tlL: null,
      tlR: null,
      index: 0,
      newIndex: 0,
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
    clickLeft() {
      let allslide = gsap.utils.toArray(".slide_body");
      let allEpisodeGroup = gsap.utils.toArray(".episode");

      this.tlL = gsap.timeline();

      this.tlL.to(allslide[this.index], {
        width: "0%",
        left: "100%",
        autoAlpha: 0,
        duration: 0.7,
        ease: "power2",
      });
      this.tlL.to(allEpisodeGroup[this.newIndex], { x: "0%", duration: 1 }, '-=0.75');
      this.tlL.to(
        allEpisodeGroup[this.index],
        {
          display: "none",
          left: "100%",
          duration: 1,
          ease: "power2",
        },
        "-=0.90"
      );
    },
    clickRight() {
      let allslide = gsap.utils.toArray(".slide_body");
      let allEpisodeGroup = gsap.utils.toArray(".episode");

      this.tlR = gsap.timeline();

      this.tlR
      .to(allslide[this.index], {
        width: "100%",
        left: "0%",
        autoAlpha: 1,
        duration: 0.7,
        ease: "power2",
      });
      this.tlR.to(allEpisodeGroup[this.newIndex], { x: "-100%", duration: 1 }, '-=0.75');
      this.tlR.to(
        allEpisodeGroup[this.index],
        {
          display: "block",
          left: "0%",
          duration: 1,
          ease: "power2",
        },
        "-=0.90"
      );
    },
    saisonLeft() {
      this.handleDirection("prev");
    },
    saisonRight() {
      this.handleDirection("next");
    },
    handleDirection(direction) {
      if (direction === "next") {
        if (this.index === 4 && this.newIndex === 4) {
          let allslide = gsap.utils.toArray(".slide_body");
          let allEpisodeGroup = gsap.utils.toArray(".episode");

          gsap.to(allslide[this.index], {
            keyframes: [
              { duration: 0.1, x: 4 },
              { duration: 0.1, x: -4 },
              { duration: 0.1, x: 4 },
              { duration: 0.1, x: 0 },
            ],
          });

          gsap.to(allEpisodeGroup[this.index], {
            keyframes: [
              { duration: 0.1, x: 4, rotate: 2 },
              { duration: 0.1, x: -4, rotate: -2 },
              { duration: 0.1, x: 4, rotate: 2 },
              { duration: 0.1, x: 0, rotate: 0 },
            ],
          });
          return;
        }
        this.index++;
        this.clickRight();
        this.newIndex++;
      } else if (direction === "prev") {
        if (this.index === 0 && this.newIndex === 0) {
          let allslide = gsap.utils.toArray(".slide_body");
          let allEpisodeGroup = gsap.utils.toArray(".episode");

          gsap.to(allslide[this.index], {
            keyframes: [
              { duration: 0.1, x: -4 },
              { duration: 0.1, x: 4 },
              { duration: 0.1, x: -4 },
              { duration: 0.1, x: 0 },
            ],
          });

          gsap.to(allEpisodeGroup[this.newIndex], {
            keyframes: [
              { duration: 0.1, x: -4, rotate: -2 },
              { duration: 0.1, x: 4, rotate: 2 },
              { duration: 0.1, x: -4, rotate: -2 },
              { duration: 0.1, x: 0, rotate: 0 },
            ],
          });
          return;
        }
        this.newIndex--;
        this.clickLeft();
        this.index--;
      }
    },
  },
  mounted() {
    this.allEpisodes();
  },
  components: { Episode },
};
</script>