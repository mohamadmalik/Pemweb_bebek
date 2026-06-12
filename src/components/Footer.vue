<template>
  <footer class="site-footer">
    <div class="footer-top">
      <div class="container footer-grid">
        <!-- Brand Section -->
        <div class="footer-brand">
          <div class="brand-logo">
            <img src="../assets/bebekslametijologo.png" alt="Logo" class="logo-img" />
            <h3 class="brand-title" style="font-family: Poppins-Bold;">Bebek Goreng<br><span class="brand-sub" style="font-family: sans-serif; font-weight: 500;">Haji Slamet</span></h3>
          </div>
          <p class="brand-desc">
            Kuliner bebek goreng legendaris sejak tahun 1986 dari Kartasura. Terkenal akan daging bebeknya yang empuk, bumbu gurih meresap, dan Sambal Korek super pedas yang bikin ketagihan.
          </p>
          <div class="social-links">
            <a href="#" class="social-icon" aria-label="Facebook">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path></svg>
            </a>
            <a href="#" class="social-icon" aria-label="Instagram">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line></svg>
            </a>
            <a href="#" class="social-icon" aria-label="TikTok">
              <!-- custom tiktok svg -->
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 12a4 4 0 1 0 4 4V4a5 5 0 0 0 5 5"></path></svg>
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div class="footer-links">
          <h4 class="footer-heading">Navigasi</h4>
          <ul>
            <li><router-link to="/">Home</router-link></li>
            <li><router-link to="/menu">Daftar Menu</router-link></li>
            <li><router-link to="/outlets">Cabang & Lokasi</router-link></li>
            <li><router-link to="/about-contact">Tentang & Kontak</router-link></li>
          </ul>
        </div>

        <!-- Working Hours -->
        <div class="footer-hours">
          <h4 class="footer-heading">Jam Operasional</h4>
          <p class="hours-text">Setiap Hari:</p>
          <p class="hours-time">10:00 - 21:00 WIB</p>
          <p class="hours-note">*Jam operasional dapat berbeda di setiap cabang selama hari libur nasional.</p>
        </div>

        <!-- Contact Info -->
        <div class="footer-contact">
          <h4 class="footer-heading">Kontak Pusat</h4>
          <p class="contact-item">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="contact-icon"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
            +62 271 716860 (Kartasura)
          </p>
          <p class="contact-item">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="contact-icon"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path><polyline points="22,6 12,13 2,6"></polyline></svg>
            info@bebekhajislamet.com
          </p>
          <p class="contact-item">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="contact-icon"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
            Kartasura, Sukoharjo, Jawa Tengah
          </p>
        </div>
      </div>
    </div>

    <!-- Footer Bottom -->
    <div class="footer-bottom">
      <div class="container footer-bottom-flex">
        <p>&copy; 2026 Bebek Goreng Haji Slamet (Kartasura). All rights reserved.</p>
        <p class="developer-credit">Takeover & Re-engineered by Senior Frontend Team</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.site-footer {
  background-color: #1a1e16;
  color: #d1d5db;
  border-top: 2px solid var(--primary);
  margin-top: auto;
}

.footer-top {
  padding: 60px 0 40px;
}

.footer-grid {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1.25fr;
  gap: 40px;
}

@media (max-width: 992px) {
  .footer-grid {
    grid-template-columns: 1fr 1fr;
    gap: 30px;
  }
}

@media (max-width: 576px) {
  .footer-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }
}

.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.brand-logo {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-img {
  height: 60px;
  width: auto;
}

.brand-title {
  font-family: var(--heading);
  font-size: 1.25rem;
  color: #ffffff;
  line-height: 1.15;
}

.brand-sub {
  color: var(--primary);
  font-weight: 800;
  font-size: 1.1rem;
}

.brand-desc {
  font-size: 0.9rem;
  color: #9ca3af;
  line-height: 1.6;
}

.social-links {
  display: flex;
  gap: 12px;
  margin-top: 5px;
}

.social-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.05);
  color: #d1d5db;
  transition: all 0.25s ease;
}

.social-icon:hover {
  background-color: var(--primary);
  color: #ffffff;
  transform: translateY(-3px);
}

.footer-heading {
  font-family: var(--heading);
  font-size: 1.15rem;
  color: #ffffff;
  margin-bottom: 20px;
  position: relative;
  padding-bottom: 8px;
}

.footer-heading::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 30px;
  height: 2px;
  background-color: var(--primary);
}

.footer-links ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.footer-links a {
  color: #9ca3af;
  font-size: 0.95rem;
  transition: all 0.25s ease;
}

.footer-links a:hover {
  color: var(--primary);
  padding-left: 5px;
}

.hours-text {
  font-weight: 600;
  color: #ffffff;
  font-size: 0.95rem;
  margin-bottom: 4px;
}

.hours-time {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--secondary);
  margin-bottom: 12px;
}

.hours-note {
  font-size: 0.8rem;
  color: #6b7280;
  line-height: 1.4;
}

.footer-contact {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  font-size: 0.9rem;
  color: #9ca3af;
  line-height: 1.4;
}

.contact-icon {
  margin-top: 2px;
  color: var(--primary);
  flex-shrink: 0;
}

/* Footer Bottom */
.footer-bottom {
  background-color: #11140e;
  padding: 20px 0;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  font-size: 0.85rem;
  color: #6b7280;
}

.footer-bottom-flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

@media (max-width: 768px) {
  .footer-bottom-flex {
    flex-direction: column;
    gap: 10px;
    text-align: center;
  }
}

.developer-credit {
  font-style: italic;
}
</style>
