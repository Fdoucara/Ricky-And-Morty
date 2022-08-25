<template>
  <nav>
    <v-app-bar app dark height="80" color="#45B649">
      <v-app-bar-nav-icon app @click.prevent="toggleAnim"></v-app-bar-nav-icon>

      <v-toolbar-title class="text-uppercase"> </v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer app v-model="drawer" dark>
      <v-layout column align-center>
        <v-flex class="mt-5">
          <v-avatar size="130" class="my-3">
            <img src="../assets/images/right.png" />
          </v-avatar>
        </v-flex>
      </v-layout>
      <v-list>
        <v-list-item
          v-for="(link, index) in links"
          :key="index"
          router
          :to="link.route"
        >
          <v-list-item-icon>
            <v-icon class="white--text"> {{ link.icon }} </v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title class="white--text">
              {{ link.name }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  name: "Accueil",
  data() {
    return {
      img: null,
      sideGroup: null,
      drawer: false,
      links: [
        { name: "Episodes", route: "/episodes", icon: "mdi-filter" },
        { name: "Personnages", route: "/personnages", icon: "mdi-filter" },
      ],
    };
  },
  methods: {
    imageAnim() {
      this.img = document.querySelector(".v-avatar img");

      let TL = gsap.timeline();

      TL.to(this.img, {
        width: "100%",
        height: "auto",
        autoAlpha: 1,
        duration: 3,
        ease: "bounce",
      });
    },
    toggleAnim() {
      this.drawer = !this.drawer;
      this.imageAnim();
    },
  },
};
</script>