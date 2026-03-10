<script lang="ts">
  import { products, type Category, type Species, type RoastLevel } from '$lib/data/products';

  type PriceRange = 'all' | 'under60' | '60to80' | 'above80';

  let filterSpecies = $state<Species | 'all'>('all');
  let filterCategory = $state<Category | 'all'>('all');
  let filterRoast = $state<RoastLevel | 'all'>('all');
  let filterPrice = $state<PriceRange>('all');
  let filterOrigin = $state<string>('all');

  const speciesOptions: (Species | 'all')[] = ['all', 'Arabica', 'Liberica', 'Excelsa', 'Robusta', 'Blend'];
  const categoryOptions: { value: Category | 'all'; label: string }[] = [
    { value: 'all', label: 'Semua' },
    { value: 'single-origin', label: 'Single Origin' },
    { value: 'blend', label: 'Blend' },
    { value: 'espresso', label: 'Espresso' }
  ];
  const roastOptions: { value: RoastLevel | 'all'; label: string }[] = [
    { value: 'all', label: 'Semua' },
    { value: 'light', label: 'Light' },
    { value: 'medium', label: 'Medium' },
    { value: 'medium-dark', label: 'Medium Dark' },
    { value: 'dark', label: 'Dark' },
    { value: 'omni', label: 'Omni' }
  ];
  const priceOptions: { value: PriceRange; label: string }[] = [
    { value: 'all', label: 'Semua Harga' },
    { value: 'under60', label: '< Rp 60.000' },
    { value: '60to80', label: 'Rp 60.000 – 80.000' },
    { value: 'above80', label: '> Rp 80.000' }
  ];

  const uniqueRegions = ['all', ...new Set(products.map(p => p.region))];

  let filtered = $derived(
    products.filter(p => {
      if (filterSpecies !== 'all' && p.species !== filterSpecies) return false;
      if (filterCategory !== 'all' && p.category !== filterCategory) return false;
      if (filterRoast !== 'all' && p.roastLevel !== filterRoast) return false;
      if (filterOrigin !== 'all' && p.region !== filterOrigin) return false;
      if (filterPrice === 'under60') return p.price !== null && p.price < 60000;
      if (filterPrice === '60to80') return p.price !== null && p.price >= 60000 && p.price <= 80000;
      if (filterPrice === 'above80') return p.price !== null && p.price > 80000;
      return true;
    })
  );

  function formatPrice(price: number | null) {
    if (price === null) return 'Cek Harga';
    return 'Rp ' + price.toLocaleString('id-ID');
  }

  function resetFilters() {
    filterSpecies = 'all';
    filterCategory = 'all';
    filterRoast = 'all';
    filterPrice = 'all';
    filterOrigin = 'all';
  }

  const roastLabels: Record<RoastLevel, string> = {
    light: 'Light',
    medium: 'Medium',
    'medium-dark': 'Medium Dark',
    dark: 'Dark',
    omni: 'Omni'
  };

  let filterOpen = $state(false);

  let activeFilterCount = $derived(
    (filterSpecies !== 'all' ? 1 : 0) +
    (filterCategory !== 'all' ? 1 : 0) +
    (filterRoast !== 'all' ? 1 : 0) +
    (filterPrice !== 'all' ? 1 : 0) +
    (filterOrigin !== 'all' ? 1 : 0)
  );
</script>

<svelte:head>
  <title>Our Products – Wandhe Coffee Estate</title>
  <meta name="description" content="Jelajahi koleksi lengkap kopi Wandhe Coffee Estate – Single Origin, Blend, dan Espresso dari Jawa Timur." />
</svelte:head>

<!-- page header -->
<section class="page-header">
  <div class="container">
    <p class="section-label">Koleksi</p>
    <h1 class="page-title">Koleksi Produk Kami</h1>
    <p class="page-subtitle">Setiap varian memiliki karakteristik unik yang mencerminkan keahlian dan dedikasi kami. Diproduksi dengan standar specialty di Jawa Timur.</p>
  </div>
</section>

<!-- filters -->
<section class="filters-section">
  <div class="container">
    <div class="filter-toggle-bar">
      <button class="filter-toggle-btn" onclick={() => filterOpen = !filterOpen}>
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="4" y1="6" x2="20" y2="6"/>
          <line x1="8" y1="12" x2="20" y2="12"/>
          <line x1="12" y1="18" x2="20" y2="18"/>
        </svg>
        {filterOpen ? 'Sembunyikan Filter' : 'Tampilkan Filter'}
        {#if activeFilterCount > 0}
          <span class="filter-badge">{activeFilterCount}</span>
        {/if}
        <svg class="toggle-chevron" class:open={filterOpen} width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="6 9 12 15 18 9"/>
        </svg>
      </button>
      <p class="filter-count-inline">{filtered.length} produk</p>
    </div>

    {#if filterOpen}
    <div class="filters-row">
      <!-- Species -->
      <div class="filter-group">
        <p class="filter-label">Species</p>
        <div class="filter-pills">
          {#each speciesOptions as s}
            <button
              class="filter-pill"
              class:active={filterSpecies === s}
              onclick={() => filterSpecies = s}
            >{s === 'all' ? 'Semua' : s}</button>
          {/each}
        </div>
      </div>

      <div class="filter-selects">
        <!--category -->
        <div class="filter-select-group">
          <label for="category-filter" class="filter-label">Kategori</label>
          <select id="category-filter" bind:value={filterCategory} class="filter-select">
            {#each categoryOptions as opt}
              <option value={opt.value}>{opt.label}</option>
            {/each}
          </select>
        </div>

        <!-- roast -->
        <div class="filter-select-group">
          <label for="roast-filter" class="filter-label">Roast Level</label>
          <select id="roast-filter" bind:value={filterRoast} class="filter-select">
            {#each roastOptions as opt}
              <option value={opt.value}>{opt.label}</option>
            {/each}
          </select>
        </div>

        <!-- price -->
        <div class="filter-select-group">
          <label for="price-filter" class="filter-label">Harga</label>
          <select id="price-filter" bind:value={filterPrice} class="filter-select">
            {#each priceOptions as opt}
              <option value={opt.value}>{opt.label}</option>
            {/each}
          </select>
        </div>

        <!-- region -->
        <div class="filter-select-group">
          <label for="origin-filter" class="filter-label">Origin</label>
          <select id="origin-filter" bind:value={filterOrigin} class="filter-select">
            {#each uniqueRegions as r}
              <option value={r}>{r === 'all' ? 'Semua Origin' : r}</option>
            {/each}
          </select>
        </div>
      </div>
    </div>

    <div class="filter-meta">
      <p class="filter-count">{filtered.length} produk ditemukan</p>
      {#if activeFilterCount > 0}
        <button class="reset-btn" onclick={resetFilters}>Reset Filter</button>
      {/if}
    </div>
    {/if}
  </div>
</section>

<!-- ── produk grid ── -->
<section class="products-section">
  <div class="container">
    {#if filtered.length === 0}
      <div class="empty-state">
        <p class="empty-title">Tidak ada produk yang sesuai filter</p>
        <button class="btn-outline-dark" onclick={resetFilters}>Lihat Semua Produk</button>
      </div>
    {:else}
      <div class="products-grid">
        {#each filtered as product}
          <div class="product-card">
            <div class="product-img-wrap">
              <img src={product.image} alt={product.name} class="product-img" loading="lazy" />
              <div class="product-badges">
                <span class="badge badge--species">{product.species}</span>
                <span class="badge badge--roast">{roastLabels[product.roastLevel]}</span>
              </div>
            </div>

            <div class="product-body">
              <p class="product-region">{product.region} · {product.weight}</p>
              <h3 class="product-name">{product.shortName}</h3>

              <div class="product-spec-row">
                <div class="spec-item">
                  <span class="spec-label">Proses</span>
                  <span class="spec-value">{product.process}</span>
                </div>
                <div class="spec-item">
                  <span class="spec-label">Altitude</span>
                  <span class="spec-value">{product.altitude}</span>
                </div>
              </div>

              {#if product.notes.length > 0}
                <div class="product-notes">
                  {#each product.notes.slice(0, 4) as note}
                    <span class="note-tag">{note}</span>
                  {/each}
                </div>
              {/if}

              <div class="product-footer">
                <span class="product-price">{formatPrice(product.price)}</span>
                <a
                  href={`/products/${product.id}`}
                  class="tokped-btn"
                >
                  Lihat Detail →
                </a>
              </div>
            </div>
          </div>
        {/each}
      </div>
    {/if}
  </div>
</section>

<!-- ── cta ── -->
<section class="products-cta">
  <div class="container cta-inner-row">
    <div>
      <h2 class="cta-title">Tidak yakin memilih yang mana?</h2>
      <p class="cta-sub">Hubungi kami dan kami akan membantu menemukan kopi yang tepat untuk selera Anda.</p>
    </div>
    <a href="/contact" class="btn-primary">Hubungi Kami</a>
  </div>
</section>

<style>
  .page-header {
    padding: 80px 0 56px;
    background: var(--white);
    border-bottom: 1px solid var(--cream-dark);
  }

  .page-title {
    font-family: var(--font-serif);
    font-size: clamp(2rem, 4vw, 3rem);
    color: var(--text-primary);
    margin-bottom: 16px;
  }

  .page-subtitle {
    font-size: 15px;
    color: var(--text-muted);
    max-width: 560px;
    line-height: 1.75;
  }

  /* filters */
  .filters-section {
    padding: 16px 0;
    background: var(--cream);
    border-bottom: 1px solid var(--cream-dark);
    position: sticky;
    top: var(--nav-height);
    z-index: 50;
  }

  .filter-toggle-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 4px 0;
  }

  .filter-toggle-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    background: none;
    border: 1px solid var(--brown-200);
    color: var(--text-secondary);
    font-family: var(--font-sans);
    font-size: 13px;
    padding: 7px 14px;
    cursor: pointer;
    border-radius: 4px;
    transition: border-color 0.2s, color 0.2s;
  }

  .filter-toggle-btn:hover {
    border-color: var(--brown-400);
    color: var(--brown-700);
  }

  .filter-badge {
    background: var(--brown-600);
    color: var(--white);
    font-size: 11px;
    font-weight: 600;
    line-height: 1;
    padding: 2px 6px;
    border-radius: 10px;
  }

  .toggle-chevron {
    transition: transform 0.25s ease;
  }

  .toggle-chevron.open {
    transform: rotate(180deg);
  }

  .filter-count-inline {
    font-size: 13px;
    color: var(--text-muted);
  }

  .filters-row {
    margin-top: 20px;
  }

  .filters-row {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .filter-label {
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 10px;
    display: block;
    font-family: var(--font-sans);
  }

  .filter-pills {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .filter-pill {
    padding: 6px 16px;
    border: 1px solid var(--brown-200);
    background: var(--white);
    color: var(--text-secondary);
    font-size: 13px;
    border-radius: 20px;
    cursor: pointer;
    transition: all 0.2s;
  }

  .filter-pill:hover {
    border-color: var(--brown-400);
    color: var(--brown-600);
  }

  .filter-pill.active {
    background: var(--brown-600);
    border-color: var(--brown-600);
    color: var(--white);
  }

  .filter-selects {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
  }

  .filter-select-group {
    display: flex;
    flex-direction: column;
    min-width: 160px;
    flex: 1;
  }

  .filter-select {
    padding: 8px 12px;
    border: 1px solid var(--brown-200);
    background: var(--white);
    color: var(--text-primary);
    font-family: var(--font-sans);
    font-size: 13px;
    cursor: pointer;
    appearance: none;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%239B8B7A' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");
    background-repeat: no-repeat;
    background-position: right 10px center;
    padding-right: 28px;
  }

  .filter-meta {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 14px;
  }

  .filter-count {
    font-size: 13px;
    color: var(--text-muted);
  }

  .reset-btn {
    font-size: 12px;
    color: var(--brown-500);
    text-decoration: underline;
    cursor: pointer;
    background: none;
    border: none;
  }

  .reset-btn:hover {
    color: var(--brown-700);
  }

  .products-section {
    padding: 60px 0 100px;
    background: var(--white);
  }

  .products-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 28px;
  }

  .product-card {
    border: 1px solid var(--cream-dark);
    overflow: hidden;
    transition: box-shadow 0.3s ease;
    display: flex;
    flex-direction: column;
  }

  .product-card:hover {
    box-shadow: 0 8px 32px rgba(92, 51, 23, 0.1);
  }

  .product-img-wrap {
    position: relative;
    aspect-ratio: 4/3;
    overflow: hidden;
  }

  .product-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.4s ease;
  }

  .product-card:hover .product-img {
    transform: scale(1.04);
  }

  .product-badges {
    position: absolute;
    top: 12px;
    left: 12px;
    display: flex;
    gap: 6px;
  }

  .badge {
    font-size: 10px;
    letter-spacing: 1px;
    text-transform: uppercase;
    padding: 3px 9px;
    font-family: var(--font-sans);
  }

  .badge--species {
    background: rgba(30, 18, 8, 0.75);
    color: var(--white);
  }

  .badge--roast {
    background: rgba(92, 51, 23, 0.85);
    color: var(--white);
  }

  .product-body {
    padding: 20px 22px 22px;
    display: flex;
    flex-direction: column;
    flex: 1;
  }

  .product-region {
    font-size: 11px;
    letter-spacing: 0.5px;
    color: var(--text-muted);
    margin-bottom: 6px;
    text-transform: uppercase;
  }

  .product-name {
    font-family: var(--font-serif);
    font-size: 18px;
    color: var(--text-primary);
    margin-bottom: 16px;
    line-height: 1.25;
  }

  .product-spec-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-bottom: 16px;
    padding-bottom: 16px;
    border-bottom: 1px solid var(--cream-dark);
  }

  .spec-item {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .spec-label {
    font-size: 10px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .spec-value {
    font-size: 13px;
    color: var(--text-secondary);
  }

  .product-notes {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-bottom: 18px;
  }

  .note-tag {
    font-size: 11px;
    background: var(--cream);
    color: var(--brown-500);
    padding: 3px 10px;
    border-radius: 12px;
    border: 1px solid var(--cream-dark);
  }

  .product-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
  }

  .product-price {
    font-size: 16px;
    font-weight: 600;
    color: var(--brown-600);
  }

  .tokped-btn {
    font-size: 13px;
    background: var(--brown-600);
    color: var(--white);
    padding: 8px 16px;
    transition: background 0.2s;
    border-radius: 2px;
  }

  .tokped-btn:hover {
    background: var(--brown-700);
  }

  .empty-state {
    text-align: center;
    padding: 80px 24px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 24px;
  }

  .empty-title {
    font-family: var(--font-serif);
    font-size: 22px;
    color: var(--text-muted);
  }

  .products-cta {
    background: var(--cream);
    padding: 56px 0;
    border-top: 1px solid var(--cream-dark);
  }

  .cta-inner-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 32px;
  }

  .cta-title {
    font-family: var(--font-serif);
    font-size: clamp(1.4rem, 2.5vw, 1.8rem);
    color: var(--text-primary);
    margin-bottom: 8px;
  }

  .cta-sub {
    font-size: 14px;
    color: var(--text-muted);
  }

  @media (max-width: 900px) {
    .products-grid {
      grid-template-columns: 1fr 1fr;
    }

    .filters-section {
      position: static;
    }
  }

  @media (max-width: 640px) {
    .products-grid {
      grid-template-columns: 1fr;
    }

    .cta-inner-row {
      flex-direction: column;
      text-align: center;
    }
  }

  @media (max-width: 500px) {
    .filter-selects {
      flex-direction: column;
    }
  }
</style>
