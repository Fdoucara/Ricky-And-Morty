<template>
  <v-container class="mx-0">
    <v-layout row wrap>
      <v-card
        class="mx-auto my-4"
        max-width="450"
        v-for="(episode, index) in saison"
        :key="index"
      >
        <v-img
          class="white--text align-end"
          src="https://tse1.mm.bing.net/th?id=OIP.M9bPDxpA_344QDwcOa-uRgHaEK&pid=Api&P=0"
        >
          <v-card-title> {{ episode.name }} </v-card-title>
        </v-img>

        <v-card-subtitle class="pt-6 pb-4 px-5">
          <v-layout row>
            <div>
              {{ episode.episode }}
            </div>
            <v-spacer></v-spacer>
            <div>
              {{ episode.air_date }}
            </div>
          </v-layout>
        </v-card-subtitle>
      </v-card>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: "Episode",
  props: ["saison"],
  data() {
    return {};
  },
};
</script>