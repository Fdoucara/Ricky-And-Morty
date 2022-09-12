<template>
  <div>
    <div class="saison_episode_container_item">
      <div
        class="saison_episode_container_item_card"
        v-for="(episode, index) in saison"
        :key="index"
        @click="toggleModale"
      >
        <div class="saison_episode_container_item_card_body" :id="episode.id">
          <div class="saison_episode_container_item_card_body_image" :id="episode.id">
            <img :src="card_image[id]" alt="Rick et Morty" @click="showIndex"/>
          </div>

          <div class="saison_episode_container_item_card_body_contain" :id="episode.id" @click="showIndex">
            <p @click="showIndex">{{ episode.episode }}</p>
            <p @click="showIndex">{{ episode.air_date }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="saison_episode_container_focus">
      <OneEpisode :id="epId"/>
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
            toggle: false,
        };
    },
    methods: {
        toggleModale() {
            this.toggle = !this.toggle;
        },
        showIndex(e) {
          this.epId = e.target.parentNode.id;
        }
    },
    mounted() {
        this.$watch(() => this.index, () => {
            this.id = this.index;
        });
    },
    components: { OneEpisode }
};
</script>