<template>
  <section class="hero">
    <video width="100%" autoplay muted loop>
        <source src="../assets/Bebekhjslamet.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
  </section>
</template>

<style scoped>
.hero {
  text-align: center;
  padding: 0px 0px;
  background-color: #f8f9fa;
  min-height: 50vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.video {
    width: 100%;
  height: 100%;
  object-fit: cover; /* Biar video proporsional memenuhi layar */
  position: absolute; /* Bikin video lepas dari posisi normal */
  top: 0;
  left: 0;
  z-index: -1;
}

h1 {
  font-size: 3rem;
  color: #42b883; /* Warna hijau khas Vue */
}


</style>