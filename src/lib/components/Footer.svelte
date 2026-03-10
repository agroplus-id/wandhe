<footer class="footer">
  <div class="footer-inner container">
    <div class="footer-brand">
      <p class="footer-brand-name">Wandhe Coffee Estate</p>
      <p class="footer-tagline">Menghadirkan pengalaman kopi terbaik dengan komitmen terhadap kualitas dan keberlanjutan.</p>
    </div>

    <div class="footer-nav">
      <p class="footer-heading">Navigasi</p>
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About Us</a></li>
        <li><a href="/products">Products</a></li>
        <li><a href="/auction">Auction</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
    </div>

    <div class="footer-contact">
      <p class="footer-heading">Kontak</p>
      <ul>
        <li>
          <a href="mailto:info@wandhecoffeeestate.com">info@wandhecoffeeestate.com</a>
        </li>
        <li>
          <a href="https://wa.me/6281234567890" target="_blank" rel="noopener noreferrer">+62 812-3456-7890</a>
        </li>
        <li>Wandhe Coffee Estate, Jawa Timur</li>
      </ul>
    </div>
  </div>

  <div class="footer-bottom">
    <p>© {new Date().getFullYear()} Wandhe Coffee Estate. All rights reserved.</p>
  </div>
</footer>

<style>
  .footer {
    background: var(--brown-800);
    color: rgba(255, 255, 255, 0.75);
  }

  .footer-inner {
    display: grid;
    grid-template-columns: 2fr 1fr 1.5fr;
    gap: 60px;
    padding-top: 64px;
    padding-bottom: 48px;
  }

  .footer-brand-name {
    font-family: var(--font-serif);
    font-size: 20px;
    font-weight: 600;
    color: var(--white);
    margin-bottom: 14px;
  }

  .footer-tagline {
    font-size: 14px;
    line-height: 1.7;
    color: rgba(255, 255, 255, 0.55);
    max-width: 260px;
  }

  .footer-heading {
    font-family: var(--font-sans);
    font-size: 11px;
    letter-spacing: 2.5px;
    text-transform: uppercase;
    color: var(--brown-300);
    margin-bottom: 20px;
  }

  .footer-nav ul,
  .footer-contact ul {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .footer-nav a,
  .footer-contact a,
  .footer-contact li {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.6);
    transition: color 0.2s;
  }

  .footer-nav a:hover,
  .footer-contact a:hover {
    color: var(--brown-200);
  }

  .footer-bottom {
    border-top: 1px solid rgba(255, 255, 255, 0.08);
    padding: 20px 40px;
    text-align: center;
    font-size: 13px;
    color: rgba(255, 255, 255, 0.35);
  }

  @media (max-width: 900px) {
    .footer-inner {
      grid-template-columns: 1fr 1fr;
      gap: 40px;
    }

    .footer-brand {
      grid-column: 1 / -1;
    }
  }

  @media (max-width: 600px) {
    .footer-inner {
      grid-template-columns: 1fr;
      gap: 32px;
      padding-bottom: 36px;
    }

    .footer-bottom {
      padding: 20px;
    }
  }
</style>
