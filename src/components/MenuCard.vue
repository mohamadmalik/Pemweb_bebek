<template>
  <div class="menu-card" :class="{ 'is-featured': menu.isFavorite }">
    <!-- Card Badge -->
    <div class="card-badges">
      
    </div>

    <!-- Card Image -->
    <div class="card-image-wrapper">
      <img :src="resolveImage(menu.image)" :alt="menu.name" class="card-image" loading="lazy" />
      <div class="image-overlay">
        <router-link to="/about-contact" class="order-btn">Pesan Sekarang</router-link>
      </div>
    </div>

    <!-- Card Body -->
    <div class="card-body">
      <div class="card-header-row">
        <h3 class="menu-title">{{ menu.name }}</h3>
        <span class="menu-price">{{ formatPrice(menu.price) }}</span>
      </div>
      <p class="menu-desc">{{ menu.description }}</p>
      
      <!-- Card Footer info -->
      <div class="card-footer-row">
        <span class="menu-category-tag">{{ formatCategory(menu.category) }}</span>
        
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  menu: {
    type: Object,
    required: true
  }
})

const isLiked = ref(false)

const toggleLike = () => {
  isLiked.value = !isLiked.value
}

const resolveImage = (imageName) => {
  if (imageName.startsWith('http') || imageName.startsWith('data:')) {
    return imageName
  }
  // Vite dynamic asset resolution
  try {
    return new URL(`../assets/${imageName}`, import.meta.url).href
  } catch (error) {
    // fallback if error
    return new URL(`../assets/hero.png`, import.meta.url).href
  }
}

const formatPrice = (val) => {
  return new Intl.NumberFormat('id-ID', {
    style: 'currency',
    currency: 'IDR',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  }).format(val)
}

const formatCategory = (cat) => {
  const categories = {
    bebek: 'Bebek Goreng',
    ayam: 'Ayam Goreng',
    lauk: 'Lauk Pendamping',
    minuman: 'Minuman'
  }
  return categories[cat] || cat
}
</script>

<style scoped>
.menu-card {
  background-color: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  position: relative;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.menu-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-lg);
  border-color: rgba(44, 163, 64, 0.2);
}

.menu-card.is-featured {
  border-left: 3px solid var(--secondary);
}

/* Badges styling */
.card-badges {
  position: absolute;
  top: 16px;
  left: 16px;
  z-index: 10;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.spicy-icon {
  display: inline-block;
  vertical-align: middle;
  margin-right: 2px;
}

/* Image styling */
.card-image-wrapper {
  position: relative;
  width: 100%;
  padding-top: 66.66%; /* 3:2 Aspect Ratio */
  overflow: hidden;
  background-color: #eae5db;
}

.card-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.menu-card:hover .card-image {
  transform: scale(1.08);
}

/* Overlay & Button */
.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(2px);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.menu-card:hover .image-overlay {
  opacity: 1;
}

.order-btn {
  background-color: var(--secondary);
  color: #ffffff;
  font-weight: 700;
  font-size: 0.9rem;
  padding: 8px 18px;
  border-radius: var(--radius-full);
  transform: translateY(15px);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 4px 10px rgba(217, 119, 6, 0.3);
}

.menu-card:hover .order-btn {
  transform: translateY(0);
}

.order-btn:hover {
  background-color: var(--secondary-hover);
  box-shadow: 0 6px 15px rgba(217, 119, 6, 0.4);
}

/* Card Body */
.card-body {
  padding: 20px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  gap: 12px;
}

.card-header-row {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 10px;
}

.menu-title {
  font-family: var(--heading);
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--text-h);
  font-family: Poppins-Bold;
}

.menu-price {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--primary);
  white-space: nowrap;
}

.menu-desc {
  font-size: 0.88rem;
  color: var(--text-light);
  line-height: 1.5;
  flex-grow: 1;
}

.card-footer-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
  padding-top: 12px;
  border-top: 1px dashed var(--border);
}

.menu-category-tag {
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--text-light);
  background-color: var(--border);
  padding: 3px 8px;
  border-radius: var(--radius-sm);
}

.favorite-icon-btn {
  background: none;
  border: none;
  cursor: pointer;
  color: var(--text-light);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  padding: 4px;
}

.favorite-icon-btn:hover {
  color: var(--accent);
  transform: scale(1.15);
}

.favorite-icon-btn.liked {
  transform: scale(1.1) rotate(5deg);
}
</style>
