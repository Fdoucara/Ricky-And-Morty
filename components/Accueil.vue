<template>
  <div class="home">
    <div class="home_img">
      <img src="../assets/images/right.png" />
    </div>
    <div class="home_card">
      <nav class="home_card_body">
        <nuxt-link class="home_card_body_item" to=""> Episodes </nuxt-link>
        <nuxt-link class="home_card_body_item" to=""> Personnages </nuxt-link>
        <nuxt-link class="home_card_body_item" to=""> Lieux </nuxt-link>
      </nav>
      <div class="home_card_logo">
        <img src="../assets/images/rick-and-morty.png">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Accueil",
  data() {
    return {
      img: null,
      sideGroup: null
    };
  },
  methods: {
    imageAnim() {
      this.img = document.querySelector(".home_img img");
      this.sideGroup = document.querySelector('.home_card');

      let TL = gsap.timeline();

      TL
      .to(this.img, {
        width: "35%",
        rotate: "360deg",
        autoAlpha: 1,
        duration: 3,
        ease: "bounce",
      })
      .to(this.sideGroup, {
        left: "50%",
        autoAlpha: 1,
        duration: 2,
        ease: "power4",
      }, 
      '-=0.90'
      );
    },
  },
  mounted() {
    this.imageAnim();
  },
};
</script>
<style lang="">
</style>