<template>
  <div class="about-contact-view">
    <!-- Header Banner -->
    <section class="page-banner">
      <div class="container text-center">
        <span class="banner-subtitle">Mengenal Lebih Dekat</span>
        <h1 class="banner-title">Tentang & Kontak Kami</h1>
        <p class="banner-desc">
          Ketahui sejarah perjalanan bebek goreng legendaris dan sampaikan saran, kritik, atau pertanyaan Anda langsung kepada kami.
        </p>
      </div>
    </section>

    <!-- Main Content Section -->
    <section class="about-contact-content section-padding">
      <div class="container main-grid">
        <!-- Left Side: History & Brand Identity -->
        <div class="history-column">
          <div class="story-card">
            <h2 class="column-title">Sejarah Bebek Haji Slamet</h2>
            <div class="title-underline"></div>
            
            <p class="story-p lead-text">
              Rasa legendaris yang berawal dari kesederhanaan di Kartasura pada tahun 1986.
            </p>
            <p class="story-p">
              Bebek Goreng Haji Slamet pertama kali dirintis oleh Bapak H. Slamet Raharjo bersama sang istri di halaman teras rumah mereka di Kartasura, Sukoharjo, Jawa Tengah. Berbekal komitmen menyajikan hidangan bebek goreng yang empuk dan tidak bau amis, beliau terus menyempurnakan resep ungkepan rempah tradisional yang kini diwariskan secara turun-temurun.
            </p>
            <p class="story-p">
              Kunci utama kelezatan bebek kami terletak pada pemilihan bebek afkir (bebek petelur yang sudah tidak produktif) karena memiliki serat daging padat yang jika diolah dengan benar akan menghasilkan rasa gurih alami yang jauh lebih kaya dibanding bebek muda. Ditambah ulekan dadakan cabai rawit merah segar dalam balutan minyak panas menjadi mahakarya bernama <strong>Sambal Korek</strong>.
            </p>
            <p class="story-p">
              Kini, Bebek Goreng Haji Slamet telah menjadi ikon kuliner bebek goreng Indonesia yang memiliki puluhan cabang resmi dan dicintai oleh jutaan pelanggan setia.
            </p>
          </div>

          <!-- Timeline or Milestones -->
          <div class="timeline-box">
            <h3 class="timeline-title">Pencapaian Kami</h3>
            <div class="timeline">
              <div class="timeline-item">
                <span class="timeline-year">1986</span>
                <h4 class="timeline-event">Kios Pertama di Kartasura</h4>
                <p>Mulai berjualan dengan tenda sederhana berkapasitas hanya beberapa kursi.</p>
              </div>
              <div class="timeline-item">
                <span class="timeline-year">1992</span>
                <h4 class="timeline-event">Paten Sambal Korek Asli</h4>
                <p>Mematenkan resep ulek dadakan Sambal Korek khas H. Slamet Raharjo.</p>
              </div>
              <div class="timeline-item">
                <span class="timeline-year">2005</span>
                <h4 class="timeline-event">Ekspansi Luar Kota</h4>
                <p>Membuka cabang resmi pertama di luar kota (Solo & Yogyakarta) dan mulai dikenal luas.</p>
              </div>
              <div class="timeline-item">
                <span class="timeline-year">2010 - Kini</span>
                <h4 class="timeline-event">Waralaba Nasional</h4>
                <p>Membuka puluhan outlet di Jabodetabek, Jawa Barat, Jawa Timur, dan pulau lainnya.</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Right Side: Contact Form -->
        <div class="contact-column">
          <div class="contact-form-card">
            <h2 class="column-title">Hubungi Kami & Kirim Saran</h2>
            <div class="title-underline"></div>
            
            <p class="form-instruction">
              Punya pertanyaan mengenai franchise, saran menu, atau keluhan layanan? Tulis pesan Anda di bawah ini:
            </p>

            <!-- Success Alert -->
            <transition name="alert-zoom">
              <div v-if="formSubmitted" class="success-alert">
                <div class="success-icon-wrapper">
                  <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" class="success-icon"><polyline points="20 6 9 17 4 12"></polyline></svg>
                </div>
                <h3>Pesan Terkirim!</h3>
                <p>Terima kasih, <strong>{{ formData.name }}</strong>. Pesan Anda telah kami terima dan akan segera diproses oleh tim Humas kami.</p>
                <button class="btn btn-primary btn-sm" @click="resetFormState">Kirim Pesan Baru</button>
              </div>
            </transition>

            <!-- Contact Form -->
            <form v-if="!formSubmitted" @submit.prevent="submitForm" class="contact-form" novalidate>
              <!-- Name Input -->
              <div class="form-group" :class="{ 'has-error': errors.name }">
                <label for="name" class="form-label">Nama Lengkap *</label>
                <input 
                  type="text" 
                  id="name" 
                  v-model="formData.name" 
                  class="form-control" 
                  placeholder="Masukkan nama lengkap Anda"
                  @input="clearError('name')"
                />
                <span v-if="errors.name" class="error-msg">{{ errors.name }}</span>
              </div>

              <!-- Email Input -->
              <div class="form-group" :class="{ 'has-error': errors.email }">
                <label for="email" class="form-label">Alamat Email *</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="formData.email" 
                  class="form-control" 
                  placeholder="contoh@email.com"
                  @input="clearError('email')"
                />
                <span v-if="errors.email" class="error-msg">{{ errors.email }}</span>
              </div>

              <!-- Phone Input -->
              <div class="form-group" :class="{ 'has-error': errors.phone }">
                <label for="phone" class="form-label">Nomor Handphone *</label>
                <input 
                  type="tel" 
                  id="phone" 
                  v-model="formData.phone" 
                  class="form-control" 
                  placeholder="Contoh: 081234567890"
                  @input="clearError('phone')"
                />
                <span v-if="errors.phone" class="error-msg">{{ errors.phone }}</span>
              </div>

              <!-- Subject Select -->
              <div class="form-group">
                <label for="subject" class="form-label">Subjek Pesan</label>
                <select id="subject" v-model="formData.subject" class="form-control form-select">
                  <option value="saran">Kritik & Saran Layanan</option>
                  <option value="kemitraan">Informasi Kemitraan (Franchise)</option>
                  <option value="catering">Pemesanan Katering / Acara</option>
                  <option value="lainnya">Lainnya</option>
                </select>
              </div>

              <!-- Message Textarea -->
              <div class="form-group" :class="{ 'has-error': errors.message }">
                <label for="message" class="form-label">Isi Pesan *</label>
                <textarea 
                  id="message" 
                  v-model="formData.message" 
                  rows="5" 
                  class="form-control" 
                  placeholder="Tuliskan pesan Anda secara mendetail di sini..."
                  @input="clearError('message')"
                ></textarea>
                <span v-if="errors.message" class="error-msg">{{ errors.message }}</span>
              </div>

              <!-- Submit button -->
              <button type="submit" class="btn btn-primary btn-block" :disabled="isSubmitting">
                <span v-if="isSubmitting" class="spinner"></span>
                {{ isSubmitting ? 'Mengirimkan...' : 'Kirim Pesan' }}
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const formData = ref({
  name: '',
  email: '',
  phone: '',
  subject: 'saran',
  message: ''
})

const errors = ref({
  name: '',
  email: '',
  phone: '',
  message: ''
})

const isSubmitting = ref(false)
const formSubmitted = ref(false)

const clearError = (field) => {
  errors.value[field] = ''
}

const validateEmail = (email) => {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return re.test(email)
}

const validatePhone = (phone) => {
  const re = /^[0-9+ ]{9,15}$/
  return re.test(phone)
}

const validateForm = () => {
  let isValid = true
  
  if (!formData.value.name.trim()) {
    errors.value.name = 'Nama lengkap wajib diisi.'
    isValid = false
  }

  if (!formData.value.email.trim()) {
    errors.value.email = 'Alamat email wajib diisi.'
    isValid = false
  } else if (!validateEmail(formData.value.email)) {
    errors.value.email = 'Format alamat email tidak valid.'
    isValid = false
  }

  if (!formData.value.phone.trim()) {
    errors.value.phone = 'Nomor handphone wajib diisi.'
    isValid = false
  } else if (!validatePhone(formData.value.phone)) {
    errors.value.phone = 'Format nomor handphone tidak valid (minimal 9-15 digit angka).'
    isValid = false
  }

  if (!formData.value.message.trim()) {
    errors.value.message = 'Isi pesan tidak boleh kosong.'
    isValid = false
  } else if (formData.value.message.trim().length < 10) {
    errors.value.message = 'Isi pesan terlalu pendek (minimal 10 karakter).'
    isValid = false
  }

  return isValid
}

const submitForm = () => {
  if (!validateForm()) return
  
  isSubmitting.value = true
  
  // Simulate API post
  setTimeout(() => {
    isSubmitting.value = false
    formSubmitted.value = true
  }, 1200)
}

const resetFormState = () => {
  formData.value = {
    name: '',
    email: '',
    phone: '',
    subject: 'saran',
    message: ''
  }
  formSubmitted.value = false
}
</script>

<style scoped>
.about-contact-view {
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

/* Main Grid Layout */
.main-grid {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 50px;
  align-items: start;
}

@media (max-width: 992px) {
  .main-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}

.column-title {
  font-size: 1.85rem;
  color: var(--text-h);
  margin-bottom: 8px;
}

.title-underline {
  width: 50px;
  height: 3px;
  background-color: var(--primary);
  border-radius: var(--radius-full);
  margin-bottom: 24px;
}

/* History styling */
.story-card {
  margin-bottom: 40px;
}

.story-p {
  font-size: 0.98rem;
  line-height: 1.7;
  color: var(--text-light);
  margin-bottom: 16px;
}

.lead-text {
  font-size: 1.15rem;
  font-weight: 600;
  color: var(--primary);
}

/* Timeline milestones styling */
.timeline-box {
  background-color: var(--bg-card);
  border: 1px solid var(--border);
  padding: 30px;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-sm);
}

.timeline-title {
  font-size: 1.35rem;
  margin-bottom: 24px;
}

.timeline {
  position: relative;
  padding-left: 24px;
  border-left: 2px solid var(--border);
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.timeline-item {
  position: relative;
}

.timeline-item::before {
  content: '';
  position: absolute;
  left: -33px;
  top: 4px;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background-color: var(--bg-card);
  border: 3px solid var(--primary);
  z-index: 2;
  transition: all 0.3s ease;
}

.timeline-item:hover::before {
  background-color: var(--primary);
  transform: scale(1.2);
}

.timeline-year {
  font-weight: 800;
  color: var(--secondary);
  font-size: 0.9rem;
  display: block;
  margin-bottom: 4px;
}

.timeline-event {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--text-h);
  margin-bottom: 6px;
}

.timeline-item p {
  font-size: 0.88rem;
  line-height: 1.5;
}

/* Contact Form styling */
.contact-form-card {
  background-color: var(--bg-card);
  border: 1px solid var(--border);
  padding: 40px;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-md);
}

@media (max-width: 576px) {
  .contact-form-card {
    padding: 24px;
  }
}

.form-instruction {
  font-size: 0.92rem;
  color: var(--text-light);
  margin-bottom: 24px;
}

.form-group {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.form-label {
  font-size: 0.88rem;
  font-weight: 600;
  color: var(--text);
}

.form-control {
  padding: 12px 16px;
  border: 1px solid var(--border);
  background-color: var(--bg);
  color: var(--text);
  border-radius: var(--radius-sm);
  font-family: var(--sans);
  font-size: 0.95rem;
  transition: all 0.3s ease;
  width: 100%;
}

.form-control:focus {
  outline: none;
  border-color: var(--primary);
  background-color: var(--bg-card);
  box-shadow: var(--shadow-glow);
}

.form-select {
  cursor: pointer;
}

.has-error .form-control {
  border-color: var(--accent);
  background-color: rgba(239, 68, 68, 0.02);
}

.error-msg {
  color: var(--accent);
  font-size: 0.8rem;
  font-weight: 500;
}

.btn-block {
  width: 100%;
}

/* Spinner for loading state */
.spinner {
  display: inline-block;
  width: 16px;
  height: 16px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: #ffffff;
  animation: spin 0.8s linear infinite;
  margin-right: 8px;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Success Alert Styling */
.success-alert {
  text-align: center;
  padding: 40px 10px;
}

.success-icon-wrapper {
  width: 64px;
  height: 64px;
  background-color: rgba(44, 163, 64, 0.1);
  color: var(--primary);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px;
  border: 2px solid rgba(44, 163, 64, 0.2);
}

.success-alert h3 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.success-alert p {
  font-size: 0.95rem;
  color: var(--text-light);
  margin-bottom: 30px;
  line-height: 1.6;
}

/* Alert zoom animation */
.alert-zoom-enter-active {
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.alert-zoom-enter-from {
  opacity: 0;
  transform: scale(0.8);
}
</style>
