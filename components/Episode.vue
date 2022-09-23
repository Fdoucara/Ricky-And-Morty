<template>
  <div>
    <div class="saison_episode_container_item">
      <div
        class="saison_episode_container_item_card"
        v-for="(episode, index) in saison"
        :id="episode.id"
        :key="index"
        @click="showIndex"
      >
        <img
          class="saison_episode_container_item_card_image"
          :src="card_image[id]"
          alt="Rick et Morty"
          @click="showIndex"
        />
        
        <div
          class="saison_episode_container_item_card_contain"
          :id="episode.id"
          @click="showIndex"
        >
          <p @click="showIndex">{{ episode.episode }}</p>
          <p @click="showIndex">{{ episode.air_date }}</p>
        </div>
      </div>
    </div>
    <div class="saison_episode_focus">
      <h2 class="saison_episode_focus_title"> Episode Actuel </h2>
      <OneEpisode v-if="epId && card_image[id]" :id="epId" :card_image="card_image[id]"/>
    </div>
  </div>
</template>

<script>
import OneEpisode from "./OneEpisode.vue";
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
      id: this.index,
      epId: 1,
      activeItem: null,
      allItems: null
    };
  },
  methods: {
    showIndex(e) {
      this.epId = e.target.parentNode.id;
      this.activeItem = this.epId - 1;
      this.allItems = Array.from($('.saison_episode_container_item_card'));

      // Utilisation du jquery pour scale l'element sur lequel on est focus     
      $(this.allItems[this.activeItem]).on('click', () => {
        $(this.allItems[this.activeItem]).addClass('scale').siblings().removeClass('scale');
      })
    },
  },
  mounted() {
    this.$watch(
      () => this.index,
      () => {
        this.id = this.index;
      }
    );
  },
  components: { OneEpisode },
};
</script>