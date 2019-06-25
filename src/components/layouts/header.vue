<template lang="pug">
  section.hero.bg-blue
    .hero-head
      nav.navbar
        .container
          .navbar-brand
            .navbar-item
              strong.has-text-white VueMusic
            a.navbar-burger.burger.has-text-white(role="button" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample")
              span(aria-hidden="true")
              span(aria-hidden="true")
              span(aria-hidden="true")
          
          .navbar-end.navbar-menu.bg-blue(id="navbarBasicExample")
            .navbar-item
              router-link.has-text-white(to="/") Buscar
            .navbar-item
              router-link.has-text-white(to="/about") Nosotros
    .hero-body
      .container.has-text-centered
        h1.title.has-text-white VueMusic
        h2.subtitle.has-text-light Canciones que estan Vue-nicimas 
        pm-player


</template>

<script>
document.addEventListener('DOMContentLoaded', () => {

  // Get all "navbar-burger" elements
  const $navbarBurgers = Array.prototype.slice.call(document.querySelectorAll('.navbar-burger'), 0);

  // Check if there are any navbar burgers
  if ($navbarBurgers.length > 0) {

    // Add a click event on each of them
    $navbarBurgers.forEach( el => {
      el.addEventListener('click', () => {

        // Get the target from the "data-target" attribute
        const target = el.dataset.target;
        const $target = document.getElementById(target);

        // Toggle the "is-active" class on both the "navbar-burger" and the "navbar-menu"
        el.classList.toggle('is-active');
        $target.classList.toggle('is-active');

      });
    });
  }

});


import PmPlayer from '@/components/Player.vue'

export default {
  components: { PmPlayer }  
}
</script>

<style lang="scss" scoped>

 .bg-blue {
   background-color: #0079ff !important;
 }

  .is-active {
    border: 0 !important;
  }
</style>

