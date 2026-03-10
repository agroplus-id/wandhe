<script lang="ts">
  import type { PageData } from './$types';

  let { data }: { data: PageData } = $props();

  let product = $derived(data.product);
  let images = $derived(product.images?.length ? product.images : [product.image]);
  let activeImg = $state(0);

  function prev() {
    activeImg = (activeImg - 1 + images.length) % images.length;
  }

  function next() {
    activeImg = (activeImg + 1) % images.length;
  }

  function formatPrice(price: number | null) {
    if (price === null) return 'Cek Harga';
    return 'Rp ' + price.toLocaleString('id-ID');
  }

  const roastLabels: Record<string, string> = {
    light: 'Light Roast',
    medium: 'Medium Roast',
    'medium-dark': 'Medium Dark Roast',
    dark: 'Dark Roast',
    omni: 'Omni Roast'
  };

  const categoryLabels: Record<string, string> = {
    'single-origin': 'Single Origin',
    blend: 'Blend',
    espresso: 'Espresso'
  };
</script>

<svelte:head>
  <title>{product.shortName} – Wandhe Coffee Estate</title>
  <meta name="description" content={product.description ?? product.notes.join(', ')} />
</svelte:head>

<!-- breadcrumb -->
<div class="breadcrumb-bar">
  <div class="container">
    <nav class="breadcrumb">
      <a href="/">Home</a>
      <span>›</span>
      <a href="/products">Our Products</a>
      <span>›</span>
      <span class="breadcrumb-current">{product.shortName}</span>
    </nav>
  </div>
</div>

<!-- main detail -->
<section class="detail-section">
  <div class="container detail-grid">

    <!-- galery-->
    <div class="gallery">
      <div class="gallery-main">
        <img
          src={images[activeImg]}
          alt="{product.name} – foto {activeImg + 1}"
          class="gallery-img"
        />
        {#if images.length > 1}
          <button class="gallery-nav gallery-nav--prev" onclick={prev} aria-label="Foto sebelumnya">‹</button>
          <button class="gallery-nav gallery-nav--next" onclick={next} aria-label="Foto berikutnya">›</button>
          <div class="gallery-dots">
            {#each images as _, i}
              <button
                class="dot"
                class:active={i === activeImg}
                onclick={() => (activeImg = i)}
                aria-label="Foto {i + 1}"
              ></button>
            {/each}
          </div>
        {/if}
      </div>

      {#if images.length > 1}
        <div class="gallery-thumbs">
          {#each images as img, i}
            <button
              class="thumb"
              class:active={i === activeImg}
              onclick={() => (activeImg = i)}
              aria-label="Pilih foto {i + 1}"
            >
              <img src={img} alt="{product.shortName} thumbnail {i + 1}" />
            </button>
          {/each}
        </div>
      {/if}
    </div>

    <!-- info panel -->
    <div class="info">
      <p class="info-label">Roasted in East Java · Sumber Wandhe Coffee Lab</p>

      <div class="info-badges">
        <span class="badge badge--species">{product.species}</span>
        <span class="badge badge--roast">{roastLabels[product.roastLevel]}</span>
        <span class="badge badge--cat">{categoryLabels[product.category] ?? product.category}</span>
      </div>

      <h1 class="info-name">{product.name}</h1>

      <div class="info-price">{formatPrice(product.price)}</div>

      {#if product.notes.length > 0}
        <div class="notes-row">
          <p class="notes-label">Tasting Notes</p>
          <div class="notes-tags">
            {#each product.notes as note}
              <span class="note-tag">{note}</span>
            {/each}
          </div>
        </div>
      {/if}

      <table class="specs-table">
        <tbody>
          <tr><th>Species</th><td>{product.species}</td></tr>
          <tr><th>Region</th><td>{product.region}</td></tr>
          <tr><th>Process</th><td>{product.process}</td></tr>
          <tr><th>Varietas</th><td>{product.variety}</td></tr>
          <tr><th>Altitude</th><td>{product.altitude}</td></tr>
          <tr><th>Berat</th><td>{product.weight}</td></tr>
          <tr><th>Processor</th><td>{product.processor}</td></tr>
        </tbody>
      </table>

      {#if product.description}
        <div class="info-description">
          <p>{product.description}</p>
        </div>
      {/if}

      <div class="cta-row">
        <a
          href={product.tokopediaLink}
          target="_blank"
          rel="noopener noreferrer"
          class="btn-tokped"
        >
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
            <path d="M5 4h14l-1.5 9H6.5L5 4zm0 0L4 2H2M9 20a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm8 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2z"/>
          </svg>
          Beli di Tokopedia
        </a>
        <a href="/contact" class="btn-ask">Tanya Produk</a>
      </div>
    </div>

  </div>
</section>

<!-- ripiu -->
{#if product.reviews.length > 0}
  <section class="reviews-section">
    <div class="container">
      <h2 class="reviews-title">Ulasan Pelanggan</h2>
      <div class="reviews-grid">
        {#each product.reviews as review}
          <div class="review-card" class:has-image={!!review.image}>
            <div class="review-body">
              <div class="review-star">★★★★★</div>
              <p class="review-text">"{review.text}"</p>
              <p class="review-author">— {review.author}</p>
            </div>
            {#if review.image}
              <img src={review.image} alt="Foto ulasan {review.author}" class="review-img" />
            {/if}
          </div>
        {/each}
      </div>
    </div>
  </section>
{/if}

<div class="back-bar">
  <div class="container">
    <a href="/products" class="back-link">← Kembali ke Semua Produk</a>
  </div>
</div>

<style>
  .breadcrumb-bar {
    background: var(--cream);
    border-bottom: 1px solid var(--cream-dark);
    padding: 14px 0;
  }
  .breadcrumb {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 13px;
    color: var(--text-muted);
  }
  .breadcrumb a { color: var(--text-muted); transition: color 0.2s; }
  .breadcrumb a:hover { color: var(--brown-600); }
  .breadcrumb-current { color: var(--text-secondary); }

  /* ──detail layout── */
  .detail-section {
    padding: 60px 0 100px;
    background: var(--white);
  }
  .detail-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 64px;
    align-items: start;
  }

  /* ──galery── */
  .gallery-main {
    position: relative;
    aspect-ratio: 1;
    overflow: hidden;
    background: var(--cream);
    border: 1px solid var(--cream-dark);
  }
  .gallery-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: opacity 0.25s ease;
  }
  .gallery-nav {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(30, 18, 8, 0.58);
    color: var(--white);
    border: none;
    width: 42px;
    height: 42px;
    font-size: 22px;
    line-height: 1;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background 0.2s;
    z-index: 2;
  }
  .gallery-nav:hover { background: rgba(30, 18, 8, 0.88); }
  .gallery-nav--prev { left: 12px; }
  .gallery-nav--next { right: 12px; }

  .gallery-dots {
    position: absolute;
    bottom: 12px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 6px;
    z-index: 2;
  }
  .dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.45);
    border: none;
    cursor: pointer;
    transition: background 0.2s;
    padding: 0;
  }
  .dot.active { background: var(--white); }

  .gallery-thumbs {
    display: flex;
    gap: 8px;
    margin-top: 10px;
    flex-wrap: wrap;
  }
  .thumb {
    width: 70px;
    height: 70px;
    border: 2px solid transparent;
    overflow: hidden;
    cursor: pointer;
    padding: 0;
    background: var(--cream);
    transition: border-color 0.2s;
    flex-shrink: 0;
  }
  .thumb.active { border-color: var(--brown-600); }
  .thumb img { width: 100%; height: 100%; object-fit: cover; }

  /* ── Info panel ── */
  .info {
    display: flex;
    flex-direction: column;
    gap: 0;
  }
  .info-label {
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 14px;
  }
  .info-badges {
    display: flex;
    gap: 6px;
    margin-bottom: 16px;
    flex-wrap: wrap;
  }
  .badge {
    font-size: 10px;
    letter-spacing: 1px;
    text-transform: uppercase;
    padding: 3px 10px;
    font-family: var(--font-sans);
  }
  .badge--species { background: var(--brown-700); color: var(--white); }
  .badge--roast   { background: var(--brown-500); color: var(--white); }
  .badge--cat     { background: var(--cream-dark); color: var(--text-secondary); }

  .info-name {
    font-family: var(--font-serif);
    font-size: clamp(1.4rem, 2.5vw, 1.9rem);
    color: var(--text-primary);
    line-height: 1.2;
    margin-bottom: 14px;
  }
  .info-price {
    font-size: 28px;
    font-weight: 700;
    color: var(--brown-600);
    margin-bottom: 24px;
  }

  .notes-row { margin-bottom: 24px; }
  .notes-label {
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 8px;
  }
  .notes-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .note-tag {
    font-size: 12px;
    background: var(--cream);
    color: var(--brown-600);
    padding: 4px 12px;
    border-radius: 14px;
    border: 1px solid var(--cream-dark);
  }

  .specs-table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 24px;
    border-top: 1px solid var(--cream-dark);
  }
  .specs-table tr {
    border-bottom: 1px solid var(--cream-dark);
  }
  .specs-table th {
    font-size: 10px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--text-muted);
    font-weight: 400;
    text-align: left;
    padding: 10px 0;
    width: 40%;
    vertical-align: top;
  }
  .specs-table td {
    font-size: 13px;
    color: var(--text-primary);
    padding: 10px 0;
    text-align: right;
  }

  .info-description {
    background: var(--cream);
    border-left: 3px solid var(--brown-400);
    padding: 16px 20px;
    margin-bottom: 28px;
  }
  .info-description p {
    font-size: 14px;
    line-height: 1.85;
    color: var(--text-secondary);
  }

  .cta-row {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    padding-top: 4px;
  }
  .btn-tokped {
    display: flex;
    align-items: center;
    gap: 8px;
    background: var(--brown-700);
    color: var(--white);
    padding: 14px 28px;
    font-size: 14px;
    font-weight: 500;
    transition: background 0.2s;
    text-decoration: none;
    letter-spacing: 0.5px;
  }
  .btn-tokped:hover { background: #2d1a0a; }
  .btn-ask {
    padding: 14px 24px;
    border: 1.5px solid var(--brown-400);
    color: var(--brown-600);
    font-size: 14px;
    transition: all 0.2s;
    text-decoration: none;
  }
  .btn-ask:hover { background: var(--brown-600); color: var(--white); border-color: var(--brown-600); }

  .reviews-section {
    background: var(--cream);
    padding: 60px 0;
    border-top: 1px solid var(--cream-dark);
  }
  .reviews-title {
    font-family: var(--font-serif);
    font-size: clamp(1.4rem, 2.5vw, 1.8rem);
    color: var(--text-primary);
    margin-bottom: 36px;
  }
  .reviews-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 20px;
  }
  .review-card {
    background: var(--white);
    border: 1px solid var(--cream-dark);
    padding: 24px;
    display: flex;
    flex-direction: column;
    gap: 0;
  }
  .review-card.has-image {
    flex-direction: row;
    align-items: flex-start;
    gap: 16px;
  }
  .review-body {
    flex: 1;
    min-width: 0;
  }
  .review-img {
    width: 120px;
    height: 120px;
    object-fit: cover;
    border: 1px solid var(--cream-dark);
    flex-shrink: 0;
    border-radius: 2px;
  }
  .review-star {
    color: var(--brown-400);
    font-size: 13px;
    letter-spacing: 2px;
    margin-bottom: 12px;
  }
  .review-text {
    font-size: 14px;
    line-height: 1.75;
    color: var(--text-secondary);
    margin-bottom: 12px;
    font-style: italic;
  }
  .review-author {
    font-size: 12px;
    color: var(--text-muted);
    font-weight: 500;
  }

  .back-bar {
    padding: 28px 0;
    border-top: 1px solid var(--cream-dark);
    background: var(--white);
  }
  .back-link {
    font-size: 13px;
    color: var(--brown-500);
    transition: color 0.2s;
  }
  .back-link:hover { color: var(--brown-700); }

  /* anjay responsive ??? */
  @media (max-width: 860px) {
    .detail-grid {
      grid-template-columns: 1fr;
      gap: 36px;
    }
  }
  @media (max-width: 560px) {
    .thumb { width: 56px; height: 56px; }
    .info-price { font-size: 22px; }
  }
</style>
