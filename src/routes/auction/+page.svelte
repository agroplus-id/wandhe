<script lang="ts">
  import { auctionProducts } from '$lib/data/auction';
  import { image6 } from '$lib/assets/images';

  function formatPrice(price: number) {
    return 'Rp ' + price.toLocaleString('id-ID');
  }

  let selectedProduct = $state<(typeof auctionProducts)[0] | null>(null);

  function openDetail(product: (typeof auctionProducts)[0]) {
    selectedProduct = product;
  }

  function closeDetail() {
    selectedProduct = null;
  }
</script>

<svelte:head>
  <title>Auction – Wandhe Coffee Estate</title>
  <meta name="description" content="Koleksi eksklusif kopi langka Wandhe Coffee Estate – produk premium dengan lot terbatas dan storytelling mendalam." />
</svelte:head>

<!-- ── hero page── -->
<section class="auction-hero" style="background-image: url({image6})">
  <div class="auction-hero-overlay"></div>
  <div class="auction-hero-content">
    <p class="page-hero-label">Eksklusif · Langka · Premium</p>
    <h1 class="auction-hero-title">Koleksi Eksklusif<br />Wandhe Estate</h1>
    <p class="auction-hero-subtitle">Produk-produk istimewa yang lahir dari lot terpilih, proses eksperimental, dan dedikasi yang luar biasa. Diproduksi dalam jumlah sangat terbatas.</p>
  </div>
</section>

<!-- ── auction konsep ── -->
<section class="concept-section">
  <div class="container concept-inner">
    <div class="concept-text">
      <p class="section-label">Mengapa Auction?</p>
      <h2 class="concept-title">Lebih dari Sekadar Kopi</h2>
      <p class="concept-body">
        Koleksi Auction Wandhe hadir untuk mereka yang mencari pengalaman kopi yang melampaui batas biasa. Setiap lot dipilih karena karakternya yang luar biasa — profil rasa yang kompleks, proses yang tidak konvensional, atau origin yang sangat terbatas.
      </p>
      <p class="concept-body">
        Dengan sistem auction, kami memastikan bahwa kopi-kopi terbaik kami sampai ke tangan orang yang benar-benar menghargainya. Ini bukan tentang siapa yang paling berani menawar — ini tentang menemukan kecocokan antara karakter kopi dan palate Anda.
      </p>
    </div>
    <div class="concept-stats">
      <div class="stat"><span class="stat-number">3</span><span class="stat-label">Lot Aktif</span></div>
      <div class="stat"><span class="stat-number">75</span><span class="stat-label">Total Bags</span></div>
      <div class="stat"><span class="stat-number">100%</span><span class="stat-label">Specialty Grade</span></div>
    </div>
  </div>
</section>

<!-- ── auctions lot ── -->
<section class="lots-section">
  <div class="container">
    <div class="lots-header">
      <p class="section-label">Lot Tersedia</p>
      <h2 class="section-title">Pilih Lot Anda</h2>
    </div>

    <div class="lots-list">
      {#each auctionProducts as product, i}
        <article class="lot-card" class:reverse={i % 2 !== 0}>
          <div class="lot-image-wrap">
            <img src={product.image} alt={product.name} class="lot-image" loading="lazy" />
            <div class="lot-availability">
              <span class="avail-dot" class:active={product.available}></span>
              {product.available ? 'Tersedia' : 'Habis'}
            </div>
          </div>

          <div class="lot-content">
            <div class="lot-meta">
              <span class="lot-number">{product.lot}</span>
              <span class="lot-crop">Crop {product.crop}</span>
            </div>

            <p class="lot-subtitle">{product.subtitle}</p>
            <h2 class="lot-name">{product.name}</h2>

            <div class="lot-specs">
              <div class="lot-spec">
                <span class="spec-k">Species</span>
                <span class="spec-v">{product.species}</span>
              </div>
              <div class="lot-spec">
                <span class="spec-k">Region</span>
                <span class="spec-v">{product.region}</span>
              </div>
              <div class="lot-spec">
                <span class="spec-k">Process</span>
                <span class="spec-v">{product.process}</span>
              </div>
              <div class="lot-spec">
                <span class="spec-k">Altitude</span>
                <span class="spec-v">{product.altitude}</span>
              </div>
            </div>

            <div class="lot-notes">
              {#each product.notes as note}
                <span class="lot-note-tag">{note}</span>
              {/each}
            </div>

            <blockquote class="lot-story">
              {product.story}
            </blockquote>

            <div class="lot-cta">
              <div class="lot-price-block">
                <span class="lot-price-label">Mulai dari</span>
                <span class="lot-price">{formatPrice(product.startingPrice)}<span class="per-100">/100g</span></span>
              </div>
              <div class="lot-actions">
                <a
                  href={product.tokopediaLink}
                  target="_blank"
                  rel="noopener noreferrer"
                  class="btn-primary"
                >
                  Lihat di Tokopedia
                </a>
                <a
                  href="https://wa.me/6281234567890?text=Halo%20Wandhe%2C%20saya%20tertarik%20dengan%20{encodeURIComponent(product.name)}"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="btn-outline-dark"
                >
                  Tanya via WhatsApp
                </a>
              </div>
            </div>
          </div>
        </article>
      {/each}
    </div>
  </div>
</section>

<!-- ── faq auction── -->
<section class="faq-section">
  <div class="container faq-inner">
    <div class="faq-header">
      <p class="section-label">FAQ</p>
      <h2 class="section-title">Pertanyaan Umum</h2>
    </div>

    <div class="faq-list">
      <details class="faq-item">
        <summary class="faq-q">Berapa minimum pembelian untuk produk auction?</summary>
        <p class="faq-a">Minimum pembelian adalah 1 bag (100g) per lot. Beberapa lot memungkinkan pembelian lebih dari satu bag selama stok tersedia.</p>
      </details>
      <details class="faq-item">
        <summary class="faq-q">Apakah produk auction bisa dipesan sebelum rilis?</summary>
        <p class="faq-a">Ya! Hubungi kami via WhatsApp untuk informasi pre-order dan notifikasi lot baru sebelum dipublikasikan secara resmi.</p>
      </details>
      <details class="faq-item">
        <summary class="faq-q">Apa yang membedakan produk auction dengan produk regular?</summary>
        <p class="faq-a">Produk auction adalah lot-lot eksklusif dengan jumlah sangat terbatas, menggunakan proses eksperimental atau bahan baku dari pohon-pohon tua pilihan yang tidak diproduksi secara massal.</p>
      </details>
      <details class="faq-item">
        <summary class="faq-q">Bagaimana cara mengetahui lot baru yang tersedia?</summary>
        <p class="faq-a">Ikuti akun media sosial kami atau daftarkan email Anda melalui halaman Contact untuk mendapatkan notifikasi pertama setiap kali lot baru tersedia.</p>
      </details>
    </div>
  </div>
</section>

<!-- ── cta ── -->
<section class="auction-bottom-cta">
  <div class="container">
    <h2 class="cta-title">Tertarik dengan lot khusus?</h2>
    <p class="cta-sub">Hubungi kami langsung untuk diskusi lebih lanjut tentang ketersediaan dan character profil setiap lot.</p>
    <div class="cta-actions">
      <a href="https://wa.me/6281234567890" target="_blank" rel="noopener noreferrer" class="btn-primary">
        Chat WhatsApp
      </a>
      <a href="/contact" class="btn-outline">Form Kontak</a>
    </div>
  </div>
</section>

<style>
  .auction-hero {
    position: relative;
    height: 60vh;
    min-height: 440px;
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .auction-hero-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(to bottom, rgba(30, 18, 8, 0.7), rgba(30, 18, 8, 0.55));
  }

  .auction-hero-content {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 0 24px;
    max-width: 680px;
  }

  .page-hero-label {
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--brown-200);
    margin-bottom: 16px;
    font-family: var(--font-sans);
  }

  .auction-hero-title {
    font-family: var(--font-serif);
    font-size: clamp(2.2rem, 5vw, 3.8rem);
    color: var(--white);
    margin-bottom: 18px;
    line-height: 1.1;
  }

  .auction-hero-subtitle {
    font-size: 15px;
    color: rgba(255, 255, 255, 0.72);
    line-height: 1.7;
  }

  .concept-section {
    padding: 80px 0;
    background: var(--cream);
  }

  .concept-inner {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 80px;
    align-items: center;
  }

  .concept-title {
    font-family: var(--font-serif);
    font-size: clamp(1.7rem, 3vw, 2.4rem);
    color: var(--brown-700);
    margin-bottom: 20px;
  }

  .concept-body {
    font-size: 15px;
    color: var(--text-secondary);
    line-height: 1.8;
    margin-bottom: 14px;
  }

  .concept-stats {
    display: flex;
    flex-direction: column;
    gap: 32px;
    border-left: 1px solid var(--brown-200);
    padding-left: 60px;
  }

  .stat {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .stat-number {
    font-family: var(--font-serif);
    font-size: 40px;
    font-weight: 600;
    color: var(--brown-600);
    line-height: 1;
  }

  .stat-label {
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .lots-section {
    padding: 80px 0 100px;
    background: var(--white);
  }

  .lots-header {
    margin-bottom: 64px;
  }

  .lots-list {
    display: flex;
    flex-direction: column;
    gap: 80px;
  }

  .lot-card {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: start;
  }

  .lot-card.reverse {
    direction: rtl;
  }

  .lot-card.reverse > * {
    direction: ltr;
  }

  .lot-image-wrap {
    position: relative;
    aspect-ratio: 4/3;
    overflow: hidden;
  }

  .lot-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .lot-availability {
    position: absolute;
    top: 16px;
    right: 16px;
    background: rgba(30, 18, 8, 0.85);
    color: var(--white);
    font-size: 12px;
    padding: 6px 14px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .avail-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #888;
  }

  .avail-dot.active {
    background: #6abf69;
  }

  .lot-content {
    padding: 8px 0;
  }

  .lot-meta {
    display: flex;
    gap: 16px;
    margin-bottom: 12px;
    align-items: center;
  }

  .lot-number {
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--brown-400);
    font-family: var(--font-sans);
  }

  .lot-crop {
    font-size: 11px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--text-muted);
    font-family: var(--font-sans);
  }

  .lot-subtitle {
    font-size: 13px;
    color: var(--brown-400);
    letter-spacing: 0.5px;
    margin-bottom: 10px;
  }

  .lot-name {
    font-family: var(--font-serif);
    font-size: clamp(1.8rem, 3vw, 2.6rem);
    color: var(--text-primary);
    margin-bottom: 28px;
    line-height: 1.15;
  }

  .lot-specs {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin-bottom: 24px;
    padding-bottom: 24px;
    border-bottom: 1px solid var(--cream-dark);
  }

  .lot-spec {
    display: flex;
    flex-direction: column;
    gap: 3px;
  }

  .spec-k {
    font-size: 10px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .spec-v {
    font-size: 13px;
    color: var(--text-secondary);
  }

  .lot-notes {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 28px;
  }

  .lot-note-tag {
    font-size: 12px;
    background: var(--cream);
    color: var(--brown-500);
    padding: 4px 12px;
    border-radius: 14px;
    border: 1px solid var(--cream-dark);
  }

  .lot-story {
    font-size: 14px;
    font-style: italic;
    color: var(--text-secondary);
    line-height: 1.8;
    border-left: 2px solid var(--brown-300);
    padding-left: 20px;
    margin-bottom: 32px;
  }

  .lot-cta {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    gap: 24px;
    flex-wrap: wrap;
  }

  .lot-price-block {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .lot-price-label {
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    color: var(--text-muted);
  }

  .lot-price {
    font-family: var(--font-serif);
    font-size: 28px;
    color: var(--brown-600);
    font-weight: 600;
  }

  .per-100 {
    font-size: 14px;
    color: var(--text-muted);
    font-family: var(--font-sans);
    font-weight: 400;
  }

  .lot-actions {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
  }

  .faq-section {
    padding: 80px 0;
    background: var(--cream);
  }

  .faq-inner {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 80px;
    align-items: start;
  }

  .faq-header {
    position: sticky;
    top: 100px;
  }

  .faq-list {
    display: flex;
    flex-direction: column;
  }

  .faq-item {
    border-bottom: 1px solid var(--brown-100);
    padding: 24px 0;
  }

  .faq-q {
    font-family: var(--font-serif);
    font-size: 17px;
    color: var(--text-primary);
    cursor: pointer;
    list-style: none;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 16px;
  }

  .faq-q::-webkit-details-marker {
    display: none;
  }

  details[open] .faq-q {
    color: var(--brown-600);
  }

  .faq-a {
    font-size: 14px;
    color: var(--text-secondary);
    line-height: 1.75;
    margin-top: 14px;
    padding-right: 24px;
  }

  .auction-bottom-cta {
    background: var(--brown-800);
    padding: 80px 0;
    text-align: center;
  }

  .auction-bottom-cta .cta-title {
    font-family: var(--font-serif);
    font-size: clamp(1.8rem, 3.5vw, 2.6rem);
    color: var(--white);
    margin-bottom: 12px;
  }

  .auction-bottom-cta .cta-sub {
    font-size: 15px;
    color: rgba(255, 255, 255, 0.65);
    max-width: 500px;
    margin: 0 auto 36px;
    line-height: 1.7;
  }

  .cta-actions {
    display: flex;
    gap: 16px;
    justify-content: center;
    flex-wrap: wrap;
  }

  .cta-actions .btn-primary {
    background: var(--white);
    color: var(--brown-700);
  }

  .cta-actions .btn-primary:hover {
    background: var(--cream);
  }

  /* Responsive */
  @media (max-width: 900px) {
    .concept-inner {
      grid-template-columns: 1fr;
    }

    .concept-stats {
      flex-direction: row;
      border-left: none;
      border-top: 1px solid var(--brown-200);
      padding-left: 0;
      padding-top: 32px;
    }

    .lot-card,
    .lot-card.reverse {
      grid-template-columns: 1fr;
      direction: ltr;
      gap: 36px;
    }

    .faq-inner {
      grid-template-columns: 1fr;
    }

    .faq-header {
      position: static;
    }
  }

  @media (max-width: 600px) {
    .lots-section {
      padding: 56px 0 64px;
    }

    .lots-list {
      gap: 56px;
    }

    .lot-specs {
      grid-template-columns: 1fr;
    }

    .lot-cta {
      flex-direction: column;
      align-items: flex-start;
    }
  }
</style>
