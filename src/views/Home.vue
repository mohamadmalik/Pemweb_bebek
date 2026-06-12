<template>
  <div class="home-view">
    <!-- Hero Section -->
    <section class="hero-section">
      <div class="video-container">
        <video autoplay muted loop playsinline class="hero-video">
          <source src="../assets/Bebekhjslamet.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video>
        <!-- fallback backdrop image in case video fails to load -->
        <div class="video-fallback"></div>
      </div>
      
      
    </section>

    <!-- Keunggulan Section (Value Proposition) -->
    <section class="value-proposition section-padding">
      <div class="container">
        <div class="section-header text-center">
          <span class="section-subtitle" style=" font-size: 50px;">Mengapa Memilih Kami?</span>
          <h2 class="section-title"></h2>
          <div class="divider"></div>
        </div>

        <div class="values-grid">
          <!-- Card 1 -->
          <div class="value-card animate-fade-in delay-1">
            <div class="value-icon-box">
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="value-icon"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
            </div>
            <h3 style="font-family: Poppins-Bold;" >Sejak Tahun 1986</h3>
            <p>Dirintis pertama kali oleh Bpk H. Slamet Raharjo di Kartasura. Resep rahasia tradisional kami tetap terjaga orisinalitasnya demi cita rasa legendaris.</p>
          </div>

          <!-- Card 2 -->
          <div class="value-card animate-fade-in delay-2">
            <div class="value-icon-box">
              <!-- Duck symbol or custom plate symbol -->
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="value-icon"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
            </div>
            <h3 style="font-family: Poppins-Bold;">Bebek Empuk & Gurih</h3>
            <p>Daging bebek pilihan diungkep berjam-jam menggunakan rempah alami nusantara. Menjadikan seratnya empuk hingga ke tulang dan gurih meresap.</p>
          </div>

          <!-- Card 3 -->
          <div class="value-card animate-fade-in delay-2">
            <div class="value-icon-box">
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="value-icon"><path d="M12 2C11.5 2 10 5 10 9C10 14.5 5 13.5 5 18C5 21 7.5 23.5 10.5 23.5C14.5 23.5 19 20 19 14.5C19 9 12.5 2 12 2Z"/></svg>
            </div>
            <h3 style="font-family: Poppins-Bold;">Sambal Korek Asli</h3>
            <p>Dibuat dadakan secara higienis menggunakan cabai pilihan terbaik, garam, bawang putih, lalu disiram minyak goreng bebek panas yang super gurih.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Featured Menus Section -->
    <section class="featured-menus section-padding">
      <div class="container">
        <div class="section-header text-center">
          <span class="section-subtitle" style=" font-size: 50px;">Menu Favorit</span>
          <h2 class="section-title" style="font-family: PoppinsRegular; letter-spacing: 2px; font-size: 24px; ">Pilihan Terpopuler Pelanggan</h2>
          <div class="divider"></div>
        </div>

        <div class="menu-grid">
          <div v-for="item in featuredItems" :key="item.id" class="menu-col">
            <MenuCard :menu="item" />
          </div>
        </div>

        <div class="view-all-wrapper text-center">
          <router-link to="/menu" class="btn btn-secondary">
            Lihat Semua Menu
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="5" y1="12" x2="19" y2="12"></line><polyline points="12 5 19 12 12 19"></polyline></svg>
          </router-link>
        </div>
      </div>
    </section>

    <!-- Banner Promo Section -->
    <section class="cta-banner section-padding">
      <div class="container cta-container">
        <div class="cta-content">
          <h2>Makan Lezat Bersama Keluarga</h2>
          <p>Kunjungi salah satu cabang Bebek Goreng Haji Slamet terdekat di kota Anda. Kami melayani makan di tempat (dine-in), bawa pulang (takeaway), maupun pemesanan partai besar.</p>
          <div class="cta-btn-group">
            <router-link to="/outlets" class="btn btn-primary">Cari Outlet Terdekat</router-link>
            <router-link to="/about-contact" class="btn btn-outline">Hubungi Kami</router-link>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import MenuCard from '../components/MenuCard.vue'

const featuredItems = ref([
  {
    id: 1,
    name: 'Bebek Bakar',
    description: 'Potongan Bebek yang dibakar dengan kematangan yang sempurna. Sehingga menghasilkan cita rasa smokey yang lezat ',
    price: 32000,
    image: 'bebekbakar.jpg',
    category: 'Bebek',
    isFavorite: true,
    spicyLevel: 5
  },
  {
    id: 2,
    name: 'Bebek Goreng Cabe Ijo',
    description: 'Daging bebek bagian dada/paha yang digoreng sangat renyah bersama Sambal Cabe Ijo yang pedas nan gurih.',
    price: 28000,
    image: 'bebekcabeijo.jpg',
    category: 'Bebek',
    isFavorite: true,
    spicyLevel: 4
  },
  {
    id: 3,
    name: 'Bebek Madura',
    description: 'Daging bebek bagian dada/paha yang dibakar dengan kematangan yang sempurna dan disiram dengan bumbu khas madura yang manis gurih.',
    price: 6000,
    image: 'bebekmadura.jpg',
    category: 'Bebek',
    isFavorite: false,
    spicyLevel: 5
  }
])
</script>

<style>
@font-face {
            font-family: 'PoppinsRegular';
            src: url('../font/Poppins-Regular.ttf') format('truetype');
        }

        @font-face {
            font-family: 'Poppins-Bold';
            src: url('../font/Poppins-Bold.ttf') format('truetype');
        }

        @font-face {
            font-family: 'Horizon-Bold';
            src: url('../font/Horizon.otf') format('Opentype');
        }
</style>
<style scoped>

.home-view {
  padding-top: 70px; /* offset navbar sticky */
}



/* Hero section */
.hero-section {
  position: relative;
  height: calc(100vh - 70px);
  min-height: 550px;
  overflow: hidden;
  display: flex;
  align-items: center;
}

.video-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.hero-video {
  
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.video-fallback {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(26, 30, 22, 0); /* dark brand background overlay */
}

.hero-overlay {
  position: relative;
  z-index: 2;
  width: 100%;
  height: 100%;
  background: linear-gradient(to right, rgba(18, 20, 15, 0.85) 40%, rgba(18, 20, 15, 0.4) 100%);
  display: flex;
  align-items: center;
}

.hero-content-wrapper {
  display: flex;
  justify-content: flex-start;
}

.hero-card {
  max-width: 600px;
  padding: 40px;
  border-radius: var(--radius-lg);
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

@media (max-width: 768px) {
  .hero-card {
    padding: 24px;
    margin: 0 10px;
    background: rgba(18, 20, 15, 0.8);
    border-color: rgba(255, 255, 255, 0.08);
  }
  .hero-section {
    height: 550px;
  }
}

.hero-tagline-small {
  display: inline-block;
  color: var(--secondary);
  font-weight: 700;
  font-size: 0.9rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 15px;
}

.hero-title {
  font-size: 3.5rem;
  color: #ffffff;
  margin-bottom: 20px;
  line-height: 1.1;
}

@media (max-width: 576px) {
  .hero-title {
    font-size: 2.5rem;
  }
}

.highlight-text {
  color: var(--primary);
  text-shadow: 0 0 15px rgba(44, 163, 64, 0.3);
}

.hero-description {
  color: #e5e7eb;
  font-size: 1.1rem;
  margin-bottom: 30px;
  line-height: 1.6;
}

.hero-actions {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.btn-outline-white {
  background-color: transparent;
  border: 2px solid rgba(255, 255, 255, 0.6);
  color: #ffffff !important;
}

.btn-outline-white:hover {
  background-color: #ffffff;
  color: var(--text-h) !important;
  border-color: #ffffff;
  transform: translateY(-2px);
}

/* Section headers styling */
.section-header {
  margin-bottom: 50px;
}

.section-subtitle {
  color: var(--primary);
  font-weight: 700;
  font-size: 2.4rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-family: Poppins-Bold;
}

.section-title {
  margin-top: 8px;
  position: relative;
  font-size: 2.25rem;
}

.divider {
  width: 60px;
  height: 3px;
  background-color: var(--secondary);
  margin: 15px auto 0;
  border-radius: var(--radius-full);
}

/* Value Proposition */
.values-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

@media (max-width: 992px) {
  .values-grid {
    grid-template-columns: 1fr;
  }
}

.value-card {
  background-color: var(--bg-card);
  border: 1px solid var(--border);
  padding: 40px 30px;
  border-radius: var(--radius-md);
  text-align: center;
  box-shadow: var(--shadow-sm);
  transition: all 0.3s ease;
}

.value-card:hover {
  transform: translateY(-6px);
  box-shadow: var(--shadow-md);
  border-color: rgba(44, 163, 64, 0.2);
}

.value-icon-box {
  width: 64px;
  height: 64px;
  background-color: rgba(44, 163, 64, 0.1);
  color: var(--primary);
  border-radius: var(--radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 24px;
  transition: all 0.3s ease;
}

.value-card:hover .value-icon-box {
  background-color: var(--primary);
  color: #ffffff;
  transform: rotate(5deg);
}

.value-card h3 {
  font-size: 1.35rem;
  margin-bottom: 12px;
}

.value-card p {
  font-size: 0.95rem;
  line-height: 1.6;
}

/* Featured Menus styling */
.bg-warm {
  background-color: rgba(244, 240, 230, 0.3);
}

.menu-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  margin-bottom: 45px;
}

@media (max-width: 992px) {
  .menu-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 576px) {
  .menu-grid {
    grid-template-columns: 1fr;
  }
}

.view-all-wrapper {
  margin-top: 30px;
}

/* CTA Banner Section */
.cta-banner {
  background: linear-gradient(135deg, rgba(44, 163, 64, 0.05) 0%, rgba(217, 119, 6, 0.03) 100%);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
}

.cta-container {
  max-width: 800px;
  text-align: center;
}

.cta-content h2 {
  font-size: 2.25rem;
  margin-bottom: 16px;
}

.cta-content p {
  font-size: 1.05rem;
  color: var(--text-light);
  margin-bottom: 30px;
}

.cta-btn-group {
  display: flex;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
}
</style>
