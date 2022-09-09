<template>
  <div>
    <div class="loader">
      <div class="loader_container">
        <div class="loader_container_image">
          <img class="loader_container_image_item" src="../assets/images/rick-and-morty-30967.png">
      </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      element: null
    }
  },
  mounted() {
    this.element = document.querySelector(".loader_container_image_item");
    gsap
      .to(this.element, { rotate: '360px', duration: '2' })
  }
}
</script>