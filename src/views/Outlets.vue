<template>
  <div class="outlets-view">
    <!-- Header Banner -->
    <section class="page-banner">
      <div class="container text-center">
        <span class="banner-subtitle">Kunjungi Kami</span>
        <h1 class="banner-title">Lokasi & Cabang</h1>
        <p class="banner-desc">
          Nikmati Bebek Goreng Haji Slamet yang orisinal di berbagai cabang resmi kami yang tersebar di kota-kota besar di Indonesia.
        </p>
      </div>
    </section>

    <!-- Outlets List Section -->
    <section class="outlets-list section-padding">
      <div class="container">
        <!-- Search & Filter Controls -->
        <div class="controls-row">
          <div class="search-box">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="search-icon"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>
            <input 
              type="text" 
              v-model="searchQuery" 
              placeholder="Cari cabang berdasarkan kota atau nama daerah..." 
              class="search-input"
            />
          </div>
          
          <div class="filter-box">
            <select v-model="selectedRegion" class="region-select">
              <option value="all">Semua Wilayah</option>
              <option value="jateng">Jawa Tengah & DIY</option>
              <option value="jakarta">DKI Jakarta</option>
              <option value="jatim">Jawa Timur</option>
            </select>
          </div>
        </div>

        <!-- Outlets Grid -->
        <div v-if="filteredOutlets.length > 0" class="outlets-grid">
          <div 
            v-for="outlet in filteredOutlets" 
            :key="outlet.id" 
            class="outlet-card"
          >
            <!-- Card Top Info -->
            <div class="outlet-card-header">
              <h3 class="outlet-name">{{ outlet.name }}</h3>
              <span 
                class="status-indicator" 
                :class="outlet.isOpenNow ? 'status-open' : 'status-closed'"
              >
                <span class="status-dot"></span>
                {{ outlet.isOpenNow ? 'Buka' : 'Tutup' }}
              </span>
            </div>

            <!-- Card Body Info -->
            <div class="outlet-card-body">
              <p class="info-row">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="info-icon text-primary"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
                <span class="address-text">{{ outlet.address }}</span>
              </p>
              
              <p class="info-row">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="info-icon text-secondary"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
                <span>{{ outlet.hours }}</span>
              </p>

              <p class="info-row">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="info-icon text-accent"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
                <a :href="'tel:' + outlet.phone" class="phone-link">{{ outlet.phone }}</a>
              </p>
            </div>

            <!-- Card Actions -->
            <div class="outlet-card-footer">
              <a 
                :href="outlet.mapLink" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="btn btn-primary btn-sm btn-block"
              >
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="3 6 9 3 15 6 21 3 21 18 15 21 9 18 3 21"></polygon><line x1="9" y1="3" x2="9" y2="18"></line><line x1="15" y1="6" x2="15" y2="21"></line></svg>
                Petunjuk Arah (Maps)
              </a>
            </div>
          </div>
        </div>

        <!-- Empty Results -->
        <div v-else class="empty-state text-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="empty-icon"><circle cx="12" cy="12" r="10"></circle><line x1="15" y1="9" x2="9" y2="15"></line><line x1="9" y1="9" x2="15" y2="15"></line></svg>
          <h3>Cabang Tidak Ditemukan</h3>
          <p>Kami tidak dapat menemukan cabang dengan kriteria pencarian Anda. Coba kata kunci lainnya.</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const searchQuery = ref('')
const selectedRegion = ref('all')

const outlets = ref([
  {
    id: 1,
    name: 'Kartasura (Pusat / Asli)',
    address: 'Jl. Raya Slamet Riyadi No. 222, Kartasura, Sukoharjo, Jawa Tengah 57161',
    hours: '10:00 - 21:00 WIB',
    phone: '+62 271 716860',
    region: 'jateng',
    openHour: 10,
    closeHour: 21,
    mapLink: 'https://maps.google.com/?q=Bebek+Goreng+Haji+Slamet+Kartasura'
  },
  {
    id: 2,
    name: 'Solo - Penumping',
    address: 'Jl. Bhayangkara No. 55, Penumping, Laweyan, Surakarta, Jawa Tengah 57141',
    hours: '10:00 - 21:00 WIB',
    phone: '+62 271 723456',
    region: 'jateng',
    openHour: 10,
    closeHour: 21,
    mapLink: 'https://maps.google.com/?q=Bebek+Goreng+Haji+Slamet+Penumping'
  },
  {
    id: 3,
    name: 'Yogyakarta - Mrican',
    address: 'Jl. Gejayan No. 24, Mrican, Caturtunggal, Depok, Sleman, Yogyakarta 55281',
    hours: '10:00 - 21:00 WIB',
    phone: '+62 274 553311',
    region: 'jateng',
    openHour: 10,
    closeHour: 21,
    mapLink: 'https://maps.google.com/?q=Bebek+Goreng+Haji+Slamet+Gejayan'
  },
  {
    id: 4,
    name: 'Jakarta - Tebet',
    address: 'Jl. KH Abdullah Syafei No. 46, Manggarai Selatan, Tebet, Jakarta Selatan 12860',
    hours: '10:00 - 21:00 WIB',
    phone: '+62 21 8303030',
    region: 'jakarta',
    openHour: 10,
    closeHour: 21,
    mapLink: 'https://maps.google.com/?q=Bebek+Goreng+Haji+Slamet+Tebet'
  },
  {
    id: 5,
    name: 'Jakarta - Kelapa Gading',
    address: 'Jl. Boulevard Raya Blok FW1 No. 19, Kelapa Gading Timur, Jakarta Utara 14240',
    hours: '10:00 - 21:00 WIB',
    phone: '+62 21 45841022',
    region: 'jakarta',
    openHour: 10,
    closeHour: 21,
    mapLink: 'https://maps.google.com/?q=Bebek+Goreng+Haji+Slamet+Kelapa+Gading'
  },
  {
    id: 6,
    name: 'Surabaya - Dharmahusada',
    address: 'Jl. Dharmahusada Indah Barat No. 34, Mojo, Gubeng, Surabaya, Jawa Timur 60115',
    hours: '10:00 - 21:00 WIB',
    phone: '+62 31 5992323',
    region: 'jatim',
    openHour: 10,
    closeHour: 21,
    mapLink: 'https://maps.google.com/?q=Bebek+Goreng+Haji+Slamet+Dharmahusada'
  }
])

// Calculate open/close status dynamically
const calculateOpenStatus = () => {
  const currentHour = new Date().getHours()
  outlets.value = outlets.value.map(outlet => {
    return {
      ...outlet,
      isOpenNow: currentHour >= outlet.openHour && currentHour < outlet.closeHour
    }
  })
}

onMounted(() => {
  calculateOpenStatus()
  // Recalculate status every minute
  setInterval(calculateOpenStatus, 60000)
})

const filteredOutlets = computed(() => {
  return outlets.value.filter(outlet => {
    const matchesSearch = outlet.name.toLowerCase().includes(searchQuery.value.toLowerCase()) || 
                          outlet.address.toLowerCase().includes(searchQuery.value.toLowerCase())
    
    const matchesRegion = selectedRegion.value === 'all' || outlet.region === selectedRegion.value
    
    return matchesSearch && matchesRegion
  })
})
</script>

<style scoped>
.outlets-view {
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

/* Search and Filter Controls */
.controls-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  margin-bottom: 40px;
}

@media (max-width: 768px) {
  .controls-row {
    flex-direction: column;
    align-items: stretch;
  }
}

.search-box {
  flex-grow: 1;
  position: relative;
  display: flex;
  align-items: center;
}

.search-icon {
  position: absolute;
  left: 16px;
  color: var(--text-light);
}

.search-input {
  width: 100%;
  padding: 14px 16px 14px 50px;
  border: 1px solid var(--border);
  background-color: var(--bg-card);
  color: var(--text);
  border-radius: var(--radius-full);
  font-family: var(--sans);
  font-size: 0.95rem;
  box-shadow: var(--shadow-sm);
  transition: all 0.3s ease;
}

.search-input:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: var(--shadow-glow);
}

.filter-box {
  min-width: 220px;
}

.region-select {
  width: 100%;
  padding: 14px 20px;
  border: 1px solid var(--border);
  background-color: var(--bg-card);
  color: var(--text);
  border-radius: var(--radius-full);
  font-family: var(--sans);
  font-size: 0.95rem;
  box-shadow: var(--shadow-sm);
  outline: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

.region-select:focus {
  border-color: var(--primary);
  box-shadow: var(--shadow-glow);
}

/* Outlets Grid */
.outlets-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

@media (max-width: 992px) {
  .outlets-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .outlets-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}

.outlet-card {
  background-color: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 24px;
  display: flex;
  flex-direction: column;
  box-shadow: var(--shadow-sm);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.outlet-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-md);
  border-color: rgba(44, 163, 64, 0.2);
}

.outlet-card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 12px;
  margin-bottom: 20px;
  border-bottom: 1px dashed var(--border);
  padding-bottom: 14px;
}

.outlet-name {
  font-family: var(--heading);
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--text-h);
}

.status-indicator {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 4px 10px;
  font-size: 0.75rem;
  font-weight: 700;
  border-radius: var(--radius-full);
  text-transform: uppercase;
}

.status-open {
  background-color: rgba(44, 163, 64, 0.1);
  color: var(--primary);
  border: 1px solid rgba(44, 163, 64, 0.2);
}

.status-closed {
  background-color: rgba(239, 68, 68, 0.1);
  color: var(--accent);
  border: 1px solid rgba(239, 68, 68, 0.2);
}

.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background-color: currentColor;
  display: inline-block;
}

.status-open .status-dot {
  box-shadow: 0 0 8px var(--primary);
  animation: pulse 1.5s infinite alternate;
}

@keyframes pulse {
  from { opacity: 0.5; }
  to { opacity: 1; }
}

.outlet-card-body {
  display: flex;
  flex-direction: column;
  gap: 16px;
  flex-grow: 1;
  margin-bottom: 24px;
}

.info-row {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  font-size: 0.92rem;
  color: var(--text-light);
  line-height: 1.5;
}

.info-icon {
  margin-top: 2px;
  flex-shrink: 0;
}

.address-text {
  color: var(--text);
}

.phone-link {
  color: var(--text);
  font-weight: 600;
  transition: color 0.2s;
}

.phone-link:hover {
  color: var(--primary);
}

.outlet-card-footer {
  margin-top: auto;
}

.btn-sm {
  padding: 10px 16px;
  font-size: 0.88rem;
}

.btn-block {
  width: 100%;
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
</style>
