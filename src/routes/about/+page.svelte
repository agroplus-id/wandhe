<script lang="ts">
  import { image3, image5 } from '$lib/assets/images';
  import reviewVideo from '$lib/assets/video/review E***t.mp4';
</script>

<svelte:head>
  <title>About Us – Wandhe Coffee Estate</title>
  <meta name="description" content="Kenali perjalanan dan filosofi Wandhe Coffee Estate – dari tanah Wonosalam ke cangkir Anda." />
</svelte:head>

<!-- ── page hero ── -->
<section class="page-hero" style="background-image: url({image3})">
  <div class="page-hero-overlay"></div>
  <div class="page-hero-content">
    <p class="page-hero-label">About Us</p>
    <h1 class="page-hero-title">Tentang Wandhe<br />Coffee Estate</h1>
    <p class="page-hero-subtitle">Komitmen kami terhadap kualitas dimulai dari tanah yang subur hingga cangkir terakhir yang Anda nikmati</p>
  </div>
</section>

<!-- ── sejarah── -->
<section class="history-section">
  <div class="container history-inner">
    <div class="history-text">
      <p class="section-label">Sejarah Kami</p>
      <h2 class="history-title">Sumber Wandhe:<br />Dari Kebun ke Cangkirmu</h2>
      <p class="history-body">
        Sumber Wandhe bermula dari keyakinan sederhana: kopi yang luar biasa lahir dari tanah yang dirawat dengan kasih, dipetik dengan kesabaran, dan diproses dengan ilmu. Di lereng Wonosalam, Jawa Timur, kami menemukan tanah yang sempurna untuk memulai perjalanan ini.
      </p>
      <p class="history-body">
        Dengan bangga kami memperkenalkan karakter kopi Jawa Timur kepada dunia — Liberica dengan aroma nangka yang khas, Excelsa dengan keunikan rasa buah yang tak terduga, Arabica dengan keasaman elegan, dan Robusta dengan kekuatan yang tak terbantahkan.
      </p>
      <p class="history-body">
        Setiap lot yang kami rilis menceritakan musim panen, ketinggian, proses, dan tangan yang merawatnya. Wandhe Coffee Estate bukan hanya sebuah brand — ini adalah identitas dari tanah tempat kopi kami tumbuh.
      </p>
    </div>
    <div class="history-image">
      <video src={reviewVideo} autoplay muted loop playsinline class="history-video"></video>
    </div>
  </div>
</section>

<!-- ── filosofi ── -->
<section class="philosophy-section">
  <div class="container">
    <div class="philosophy-header">
      <p class="section-label">Filosofi</p>
      <h2 class="section-title" style="text-align:center;">Filosofi Brand Kami</h2>
      <p class="section-subtitle" style="text-align:center; margin: 0 auto; max-width:560px;">
        Kami percaya bahwa kopi terbaik terlahir dari harmoni antara alam, ilmu pengetahuan, dan dedikasi tanpa batas
      </p>
    </div>

    <div class="philosophy-cards">
      <div class="phil-card">
        <div class="phil-number">01</div>
        <h3 class="phil-title">Kejujuran Origin</h3>
        <p class="phil-body">Setiap produk kami mencantumkan informasi lengkap — species, region, proses, ketinggian, varietas, hingga processor. Transparansi bukan pilihan, itu standar kami.</p>
      </div>
      <div class="phil-card">
        <div class="phil-number">02</div>
        <h3 class="phil-title">Kesederhanaan Elegan</h3>
        <p class="phil-body">Tidak ada yang berlebihan di Wandhe. Setiap keputusan — dari cara memproses cherry hingga desain kemasan — dibuat dengan prinsip: sederhana, bermakna, dan berkelas.</p>
      </div>
      <div class="phil-card">
        <div class="phil-number">03</div>
        <h3 class="phil-title">Eksplorasi Tanpa Henti</h3>
        <p class="phil-body">Dari Natural Klasik hingga Mossto Anaerobic, kami terus bereksperimen dengan proses-proses yang dapat mengekstrak karakter terbaik dari setiap varietas yang kami tanam.</p>
      </div>
    </div>
  </div>
</section>

<!-- ── komitmen ── -->
<section class="commitment-section">
  <div class="commitment-bg" style="background-image: url({image5})">
    <div class="commitment-overlay"></div>
    <div class="container commitment-content">
      <p class="section-label" style="color: var(--brown-200);">Komitmen Kami</p>
      <h2 class="section-title section-title--white" style="max-width:600px;">Kualitas yang Tidak Pernah Berkompromi</h2>
      <div class="commitment-points">
        <div class="point">
          <div class="point-icon">✓</div>
          <div>
            <h4 class="point-title">Seleksi Ketat</h4>
            <p class="point-desc">Hanya cherry matang sempurna yang kami proses, dipilih dengan tangan oleh pemetik berpengalaman.</p>
          </div>
        </div>
        <div class="point">
          <div class="point-icon">✓</div>
          <div>
            <h4 class="point-title">Proses Terkontrol</h4>
            <p class="point-desc">Setiap jam fermentasi, setiap derajat pengeringan dipantau untuk memastikan konsistensi rasa di setiap lot.</p>
          </div>
        </div>
        <div class="point">
          <div class="point-icon">✓</div>
          <div>
            <h4 class="point-title">Roasting Presisi</h4>
            <p class="point-desc">Profil roasting dikembangkan khusus untuk setiap varietas agar karakter asli biji kopi terjaga dengan sempurna.</p>
          </div>
        </div>
        <div class="point">
          <div class="point-icon">✓</div>
          <div>
            <h4 class="point-title">Keberlanjutan Ekosistem</h4>
            <p class="point-desc">Praktik pertanian yang memperhatikan keseimbangan alam, mendukung petani lokal, dan menjaga tanah tetap subur untuk generasi berikutnya.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── nilai dan visi ── -->
<section class="values-section">
  <div class="container">
    <div class="values-header">
      <p class="section-label">Nilai & Visi</p>
      <h2 class="section-title">Yang Menggerakkan Kami</h2>
    </div>

    <div class="values-layout">
      <div class="values-list">
        <div class="value-item">
          <h4 class="value-item-title">Humble</h4>
          <p class="value-item-desc">Tidak berlebihan, membumi, jujur. Kami berbicara melalui kualitas produk, bukan klaim yang kosong.</p>
        </div>
        <div class="value-item">
          <h4 class="value-item-title">Friendly</h4>
          <p class="value-item-desc">Hangat dan mudah dipahami. Kami ingin setiap orang — dari barista profesional hingga pecinta kopi pemula — merasakan sambutan yang tulus.</p>
        </div>
        <div class="value-item">
          <h4 class="value-item-title">Elegant</h4>
          <p class="value-item-desc">Pemilihan kata rapi dan berkelas. Dalam setiap komunikasi, kami menjaga estetika yang mencerminkan kualitas produk kami.</p>
        </div>
        <div class="value-item">
          <h4 class="value-item-title">Sophisticated</h4>
          <p class="value-item-desc">Berwawasan, berkarakter, tidak norak. Kami memahami kopi secara mendalam dan menyampaikannya dengan cara yang bermartabat.</p>
        </div>
      </div>

      <div class="vision-box">
        <p class="vision-label">Visi Kami</p>
        <blockquote class="vision-quote">
          "Menjadi coffee estate Jawa Timur yang dikenal dunia — bukan hanya karena rasa kopinya, tetapi karena identitas, nilai, dan cerita di balik setiap cangkir yang kami hadirkan."
        </blockquote>
        <div class="vision-cta">
          <a href="/products" class="btn-primary" style="margin-top: 12px;">Lihat Koleksi Kami</a>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .page-hero {
    position: relative;
    height: 56vh;
    min-height: 400px;
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .page-hero-overlay {
    position: absolute;
    inset: 0;
    background: rgba(30, 18, 8, 0.62);
  }

  .page-hero-content {
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

  .page-hero-title {
    font-family: var(--font-serif);
    font-size: clamp(2.2rem, 5vw, 3.6rem);
    color: var(--white);
    margin-bottom: 18px;
    line-height: 1.1;
  }

  .page-hero-subtitle {
    font-size: 16px;
    color: rgba(255, 255, 255, 0.72);
    line-height: 1.65;
  }

  .history-section {
    padding: 100px 0;
    background: var(--white);
  }

  .history-inner {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
  }

  .history-title {
    font-family: var(--font-serif);
    font-size: clamp(1.7rem, 3vw, 2.4rem);
    color: var(--brown-700);
    margin-bottom: 24px;
    line-height: 1.2;
  }

  .history-body {
    font-size: 15px;
    color: var(--text-secondary);
    line-height: 1.85;
    margin-bottom: 18px;
  }

  .history-video {
    width: 100%;
    aspect-ratio: 9/16;
    object-fit: cover;
    display: block;
  }

  .philosophy-section {
    padding: 100px 0;
    background: var(--cream);
  }

  .philosophy-header {
    text-align: center;
    margin-bottom: 64px;
  }

  .philosophy-cards {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 28px;
  }

  .phil-card {
    background: var(--white);
    padding: 36px 28px;
  }

  .phil-number {
    font-family: var(--font-serif);
    font-size: 48px;
    font-weight: 600;
    color: var(--brown-100);
    line-height: 1;
    margin-bottom: 20px;
  }

  .phil-title {
    font-family: var(--font-serif);
    font-size: 20px;
    color: var(--brown-700);
    margin-bottom: 14px;
  }

  .phil-body {
    font-size: 14px;
    color: var(--text-secondary);
    line-height: 1.8;
  }

  /* Commitment */
  .commitment-section {
    position: relative;
  }

  .commitment-bg {
    background-size: cover;
    background-position: center;
    position: relative;
    padding: 100px 0;
  }

  .commitment-overlay {
    position: absolute;
    inset: 0;
    background: rgba(30, 18, 8, 0.78);
  }

  .commitment-content {
    position: relative;
    z-index: 1;
  }

  .commitment-points {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 32px;
    margin-top: 48px;
  }

  .point {
    display: flex;
    gap: 16px;
  }

  .point-icon {
    flex-shrink: 0;
    width: 28px;
    height: 28px;
    border: 1px solid var(--brown-300);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--brown-200);
    font-size: 13px;
    margin-top: 2px;
  }

  .point-title {
    font-family: var(--font-serif);
    font-size: 17px;
    color: var(--white);
    margin-bottom: 8px;
  }

  .point-desc {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.65);
    line-height: 1.7;
  }

  .values-section {
    padding: 100px 0;
    background: var(--white);
  }

  .values-header {
    margin-bottom: 64px;
  }

  .values-layout {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: start;
  }

  .values-list {
    display: flex;
    flex-direction: column;
    gap: 32px;
  }

  .value-item {
    border-left: 2px solid var(--brown-200);
    padding-left: 24px;
  }

  .value-item-title {
    font-family: var(--font-serif);
    font-size: 19px;
    color: var(--brown-700);
    margin-bottom: 8px;
  }

  .value-item-desc {
    font-size: 14px;
    color: var(--text-secondary);
    line-height: 1.75;
  }

  .vision-box {
    background: var(--cream);
    padding: 48px 44px;
    border-top: 3px solid var(--brown-600);
  }

  .vision-label {
    font-size: 11px;
    letter-spacing: 2.5px;
    text-transform: uppercase;
    color: var(--brown-400);
    margin-bottom: 20px;
    font-family: var(--font-sans);
  }

  .vision-quote {
    font-family: var(--font-serif);
    font-size: 18px;
    font-style: italic;
    color: var(--text-primary);
    line-height: 1.7;
    margin-bottom: 28px;
  }

  @media (max-width: 900px) {
    .history-inner,
    .values-layout {
      grid-template-columns: 1fr;
      gap: 48px;
    }

    .philosophy-cards {
      grid-template-columns: 1fr 1fr;
    }

    .commitment-points {
      grid-template-columns: 1fr;
    }
  }

  @media (max-width: 600px) {
    .history-section,
    .philosophy-section,
    .values-section {
      padding: 64px 0;
    }

    .commitment-bg {
      padding: 64px 0;
    }

    .philosophy-cards {
      grid-template-columns: 1fr;
    }

    .vision-box {
      padding: 32px 24px;
    }
  }
</style>
