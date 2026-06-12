<template>
  <div class="menu-view">
    <!-- Header Banner -->
    <section class="page-banner">
      <div class="container text-center">
        <span class="banner-subtitle">Autentik & Lezat</span>
        <h1 class="banner-title">Daftar Menu Kami</h1>
        <p class="banner-desc">
          Nikmati kelezatan bebek goreng legendaris dengan resep asli tradisional Kartasura dan Sambal Korek ulek dadakan.
        </p>
      </div>
    </section>

    <!-- Menu Catalog Section -->
    <section class="menu-catalog section-padding">
      <div class="container">
        <!-- Category Tabs -->
        <div class="category-tabs-wrapper">
          <div class="category-tabs">
            <button 
              v-for="tab in tabs" 
              :key="tab.value" 
              class="tab-btn" 
              :class="{ 'active': activeTab === tab.value }"
              @click="setActiveTab(tab.value)"
            >
              {{ tab.label }}
            </button>
          </div>
        </div>

        <!-- Catalog Grid -->
        <transition-group name="grid-fade" tag="div" class="menu-grid">
          <div 
            v-for="item in filteredItems" 
            :key="item.id" 
            class="menu-col"
          >
            <MenuCard :menu="item" />
          </div>
        </transition-group>

        <!-- Empty State -->
        <div v-if="filteredItems.length === 0" class="empty-state text-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="empty-icon"><path d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/></svg>
          <h3>Menu Tidak Ditemukan</h3>
          <p>Kategori menu ini sedang kosong atau sedang diperbarui. Silakan pilih kategori lain.</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import MenuCard from '../components/MenuCard.vue'

const activeTab = ref('all')

const tabs = [
  { label: 'Semua Menu', value: 'all' },
  { label: 'Bebek Goreng', value: 'bebek' },
  { label: 'Ayam Goreng', value: 'ayam' },
  { label: 'Lauk Pendamping', value: 'lauk' },
  { label: 'Minuman', value: 'minuman' }
]

const menuItems = ref([
  // Bebek
  {
    id: 1,
    name: 'Bebek Goreng',
    description: 'Potongan Bebek yang dibakar dengan kematangan yang sempurna. Sehingga menghasilkan cita rasa smokey yang lezat ',
    price: 32000,
    image: 'bebekbakar.jpg',
    category: 'Bebek Goreng',
    isFavorite: true,
    spicyLevel: 5
  },
  {
    id: 2,
    name: 'Bebek Goreng Cabe Ijo',
    description: 'Daging bebek bagian dada/paha yang digoreng sangat renyah bersama Sambal Cabe Ijo yang pedas nan gurih.',
    price: 28000,
    image: 'bebekcabeijo.jpg',
    category: 'Bebek Goreng',
    isFavorite: true,
    spicyLevel: 4
  },
  {
    id: 3,
    name: 'Bebek Madura',
    description: 'Daging bebek bagian dada/paha yang dibakar dengan kematangan yang sempurna dan disiram dengan bumbu khas madura yang manis gurih.',
    price: 20000,
    image: 'bebekmadura.jpg',
    category: 'Bebek Goreng',
    isFavorite: false,
    spicyLevel: 5
  },
  {
    id: 4,
    name: 'Bebek Goreng Utuh (Satu Ekor)',
    description: 'Satu ekor bebek utuh goreng garing (terdiri dari 2 dada, 2 paha, kepala, ati ampela). Pilihan pas untuk makan besar bersama keluarga.',
    price: 120000,
    image: 'bebek_goreng_piring.png',
    category: 'Bebek Goreng',
    isFavorite: false,
    spicyLevel: 5
  },
  // Ayam
  {
    id: 5,
    name: 'Ayam Goreng Paha Kremes',
    description: 'Paha ayam kampung empuk dengan bumbu ungkep tradisional gurih meresap, digoreng renyah dengan taburan kremes gurih yang melimpah.',
    price: 24000,
    image: 'ayamkampung.jpg', // use fallback hero.png which will load nicely
    category: 'Ayam Goreng',
    isFavorite: false,
    spicyLevel: 4
  },
  {
    id: 6,
    name: 'Ayam Goreng Cabe Ijo',
    description: 'ayam kampung bagian dada/paha yang digoreng sangat renyah bersama Sambal Cabe Ijo yang pedas nan gurih, pilihan pas untuk kamu yang ingin makan ayam dengan sensasi pedas membara.',
    price: 25000,
    image: 'ayam_cabe.jpg',
    category: 'Ayam Goreng',
    isFavorite: false,
    spicyLevel: 4
  },
  // Lauk
  {
    id: 7,
    name: 'Sambal Korek Cobek Tambahan',
    description: 'Satu porsi tambahan Sambal Korek ulek dadakan yang segar dan pedas membara, disiram minyak panas gurih bekas goreng bebek.',
    price: 6000,
    image: 'sambal_korek_cobek.png',
    category: 'lauk',
    isFavorite: false,
    spicyLevel: 5
  },
  {
    id: 8,
    name: 'Tempe Goreng Rempah',
    description: '2 pcs tempe gurih diungkep rempah kuning kelapa lalu digoreng renyah, pendamping wajib makanan kalian.',
    price: 8000,
    image: 'full_tempe-01.jpg',
    category: 'lauk',
    isFavorite: false,
    spicyLevel: 0
  },
 
])

const filteredItems = computed(() => {
  if (activeTab.value === 'all') {
    return menuItems.value
  }
  return menuItems.value.filter(item => item.category === activeTab.value)
})

const setActiveTab = (tabValue) => {
  activeTab.value = tabValue
}
</script>

<style scoped>
.menu-view {
  padding-top: 70px;
}

/* Banner section */
.page-banner {
  background: linear-gradient(rgba(26, 30, 22, 0.75), rgba(26, 30, 22, 0.85)), url('../assets/hero.png');
  background-size: cover;
  background-position: center;
  color: #ffffff;
  padding: 60px 0;
  border-bottom: 3px solid var(--primary);
}

.banner-subtitle {
  color: var(--secondary);
  font-weight: 700;
  font-size: 0.85rem;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.banner-title {
  font-size: 3rem;
  color: #ffffff;
  margin: 10px 0 15px;
}

.banner-desc {
  max-width: 600px;
  margin: 0 auto;
  color: #e5e7eb;
  font-size: 1rem;
  line-height: 1.6;
}

/* Catalog Filter Tabs */
.category-tabs-wrapper {
  margin-bottom: 40px;
  display: flex;
  justify-content: center;
}

.category-tabs {
  display: flex;
  background-color: var(--bg-card);
  padding: 6px;
  border-radius: var(--radius-full);
  border: 1px solid var(--border);
  box-shadow: var(--shadow-sm);
  overflow-x: auto;
  max-width: 100%;
  scrollbar-width: none; /* Hide scrollbars */
}

.category-tabs::-webkit-scrollbar {
  display: none;
}

.tab-btn {
  background: none;
  border: none;
  padding: 10px 24px;
  font-family: var(--sans);
  font-weight: 600;
  font-size: 0.95rem;
  color: var(--text-light);
  border-radius: var(--radius-full);
  cursor: pointer;
  white-space: nowrap;
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}

.tab-btn:hover {
  color: var(--primary);
}

.tab-btn.active {
  background-color: var(--primary);
  color: #ffffff !important;
  box-shadow: 0 4px 12px rgba(44, 163, 64, 0.2);
}

/* Grid Layout */
.menu-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 30px;
}

@media (max-width: 1200px) {
  .menu-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 992px) {
  .menu-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 576px) {
  .menu-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}

/* Empty State */
.empty-state {
  padding: 60px 0;
  max-width: 400px;
  margin: 0 auto;
}

.empty-icon {
  color: var(--text-light);
  margin-bottom: 20px;
}

.empty-state h3 {
  font-size: 1.35rem;
  margin-bottom: 8px;
}

.empty-state p {
  font-size: 0.9rem;
  color: var(--text-light);
}

/* Animation for transition-group catalog item change */
.grid-fade-enter-active,
.grid-fade-leave-active {
  transition: all 0.4s ease;
}

.grid-fade-enter-from {
  opacity: 0;
  transform: scale(0.9) translateY(15px);
}

.grid-fade-leave-to {
  opacity: 0;
  transform: scale(0.9) translateY(-15px);
  position: absolute; /* needed for smooth sliding effect on leave */
}

/* ensures moving elements animate smoothly */
.grid-fade-move {
  transition: transform 0.4s ease;
}
</style>
