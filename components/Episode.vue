<template>
  <div class="episode_card_container">
    <div class="episode_card" v-for="(episode, index) in saison" :key="index">
        <div class="episode_card_header">
          <p> {{ episode.episode }} </p>
        </div>
        <div class="episode_card_body">
          <p> {{ episode.name }} </p>
        </div>
        <div class="episode_card_footer">
          <p> {{ episode.air_date }} </p>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Episode',
  props: ['saison'],
  data() {
    return {
      
    }
  },
}
</script>