# Santorini Eyewear — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a complete single-page institutional website for Santorini Eyewear — a Brazilian wholesale optical products company — using pure HTML/CSS/JS (no framework).

**Architecture:** Single `index.html` with all CSS in a `<style>` block and minimal vanilla JS for the mobile menu. Assets (logo, midias, depoimentos) are referenced by relative paths. Two auxiliary files: `sitemap.xml` and `robots.txt`.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox), vanilla JS, Google Fonts (Dancing Script + Inter), SVG icons inline.

---

## File map

| File | Role |
|---|---|
| `index.html` | Entire site — markup + CSS + JS |
| `sitemap.xml` | SEO sitemap |
| `robots.txt` | Crawler instructions |

Assets already present (read-only):
- `1778084193288_santorini_logo_site.png` — logo
- `Santorini Eyewear_midias/midia_1.png` … `midia_11.jpg` — product photos
- `Santorini Eyewear_depoimentos/depoimento_1.png` … `depoimento_3.png` — Google review screenshots

---

### Task 1: HTML shell + CSS variables + Google Fonts

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create index.html with correct lang, head, CSS variables**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Santorini</title>
  <meta name="description" content="Santorini Eyewear — atacadista de artigos de ótica com design, qualidade e reposição ágil para óticas e revendedores em todo o Brasil.">
  <meta property="og:title" content="Santorini">
  <meta property="og:description" content="Santorini Eyewear — atacadista de artigos de ótica com design, qualidade e reposição ágil para óticas e revendedores em todo o Brasil.">
  <meta property="og:image" content="1778084193288_santorini_logo_site.png">
  <meta property="og:type" content="website">
  <link rel="icon" type="image/png" href="1778084193288_santorini_logo_site.png">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --blue-deep:  #1A3F7A;
      --blue-mid:   #2E6DB4;
      --blue-light: #4A8FD4;
      --white:      #FFFFFF;
      --off-white:  #F8F9FA;
      --gray-light: #F0F4F8;
      --text:       #1A1A2E;
      --text-muted: #4A5568;
      --header-h:   72px;
    }
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body { font-family: 'Inter', sans-serif; color: var(--text); background: var(--white); }
    img { max-width: 100%; display: block; }
    a { text-decoration: none; color: inherit; }
    .script { font-family: 'Dancing Script', cursive; }
  </style>
</head>
<body>
  <!-- sections inserted in subsequent tasks -->
  <div id="root"></div>
  <!-- Rodapé MonteSite - Atualização Automática -->
  <div id="montesite-footer-badge"></div>
  <script src="https://vaabpicspdbolvutnscp.supabase.co/functions/v1/get-footer-iframe"></script>
</body>
</html>
```

- [ ] **Step 2: Open index.html in browser and confirm blank page loads without errors**

```bash
# Verify file exists and lang attribute is correct
grep 'lang="pt-BR"' index.html && echo "OK"
```

Expected: prints `OK`

---

### Task 2: Fixed header

**Files:**
- Modify: `index.html` — add header markup inside `<body>` before `<div id="root">` and header CSS inside `<style>`

- [ ] **Step 1: Add header markup**

Insert after `<body>` opening tag:

```html
<header id="site-header" role="banner">
  <div class="header-inner">
    <a href="#hero" class="header-logo" aria-label="Santorini — página inicial">
      <img src="1778084193288_santorini_logo_site.png" alt="Santorini Eyewear" height="40">
    </a>
    <nav role="navigation" aria-label="Menu principal">
      <ul class="nav-links">
        <li><a href="#sobre">Sobre</a></li>
        <li><a href="#portfolio">Portfólio</a></li>
        <li><a href="#valores">Valores</a></li>
        <li><a href="#depoimentos">Depoimentos</a></li>
        <li><a href="#contato">Contato</a></li>
      </ul>
    </nav>
    <a href="https://wa.me/5521967434256" class="btn-whatsapp-header" aria-label="Falar no WhatsApp">
      Falar no WhatsApp
    </a>
    <button class="hamburger" aria-label="Abrir menu" aria-expanded="false" aria-controls="mobile-menu">
      <span></span><span></span><span></span>
    </button>
  </div>
  <div id="mobile-menu" class="mobile-menu" hidden>
    <ul>
      <li><a href="#sobre">Sobre</a></li>
      <li><a href="#portfolio">Portfólio</a></li>
      <li><a href="#valores">Valores</a></li>
      <li><a href="#depoimentos">Depoimentos</a></li>
      <li><a href="#contato">Contato</a></li>
      <li><a href="https://wa.me/5521967434256">Falar no WhatsApp</a></li>
    </ul>
  </div>
</header>
```

- [ ] **Step 2: Add header CSS inside `<style>`**

```css
/* ── HEADER ── */
#site-header {
  position: fixed; top: 0; left: 0; width: 100%; z-index: 1000;
  background: var(--blue-deep);
  box-shadow: 0 2px 12px rgba(0,0,0,0.18);
}
.header-inner {
  max-width: 1200px; margin: 0 auto;
  height: var(--header-h);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 24px; gap: 16px;
}
.header-logo img { filter: brightness(0) invert(1); height: 40px; width: auto; }
.nav-links { list-style: none; display: flex; gap: 32px; }
.nav-links a {
  color: rgba(255,255,255,0.85); font-size: 0.9rem; font-weight: 500;
  letter-spacing: 0.02em; transition: color 0.2s;
}
.nav-links a:hover { color: var(--white); }
.btn-whatsapp-header {
  background: var(--white); color: var(--blue-deep);
  padding: 10px 20px; border-radius: 6px;
  font-size: 0.85rem; font-weight: 600; white-space: nowrap;
  transition: background 0.2s, color 0.2s;
}
.btn-whatsapp-header:hover { background: var(--blue-light); color: var(--white); }
.hamburger {
  display: none; flex-direction: column; justify-content: center; gap: 5px;
  background: none; border: none; cursor: pointer; padding: 4px;
}
.hamburger span {
  display: block; width: 24px; height: 2px;
  background: var(--white); border-radius: 2px; transition: 0.3s;
}
.mobile-menu {
  background: var(--blue-deep); border-top: 1px solid rgba(255,255,255,0.1);
}
.mobile-menu ul { list-style: none; padding: 16px 24px; display: flex; flex-direction: column; gap: 12px; }
.mobile-menu a { color: var(--white); font-size: 1rem; font-weight: 500; padding: 8px 0; display: block; }
@media (max-width: 900px) {
  .nav-links, .btn-whatsapp-header { display: none; }
  .hamburger { display: flex; }
}
```

- [ ] **Step 3: Add hamburger JS before closing `</body>`**

```html
<script>
  const hamburger = document.querySelector('.hamburger');
  const mobileMenu = document.getElementById('mobile-menu');
  hamburger.addEventListener('click', () => {
    const open = mobileMenu.hidden;
    mobileMenu.hidden = !open;
    hamburger.setAttribute('aria-expanded', String(open));
  });
  mobileMenu.querySelectorAll('a').forEach(a => {
    a.addEventListener('click', () => { mobileMenu.hidden = true; hamburger.setAttribute('aria-expanded','false'); });
  });
</script>
```

---

### Task 3: Hero section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add hero markup after `<header>`**

```html
<section id="hero" role="main" aria-label="Hero Santorini Eyewear">
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <h1 class="script hero-title">Santorini</h1>
    <h2 class="hero-subtitle">Seu parceiro atacadista em artigos de ótica</h2>
    <p class="hero-slogan">Santorini, perfeito pra você.</p>
    <a href="https://wa.me/5521967434256" class="btn-hero" aria-label="Falar no WhatsApp">
      Falar no WhatsApp
    </a>
  </div>
</section>
```

- [ ] **Step 2: Add hero CSS**

```css
/* ── HERO ── */
#hero {
  position: relative;
  min-height: 100vh;
  padding-top: var(--header-h);
  background: url('Santorini Eyewear_midias/midia_1.png') center top / cover no-repeat;
  display: flex; align-items: center; justify-content: center;
}
.hero-overlay {
  position: absolute; inset: 0;
  background: linear-gradient(160deg, rgba(10,25,60,0.78) 0%, rgba(26,63,122,0.65) 100%);
}
.hero-content {
  position: relative; z-index: 1;
  text-align: center; color: var(--white);
  padding: 40px 24px; max-width: 700px;
}
.hero-title {
  font-size: clamp(3.5rem, 10vw, 7rem);
  font-weight: 700; line-height: 1.1;
  text-shadow: 0 2px 20px rgba(0,0,0,0.3);
  margin-bottom: 16px;
}
.hero-subtitle {
  font-size: clamp(1.1rem, 3vw, 1.5rem);
  font-weight: 300; opacity: 0.92; margin-bottom: 12px;
}
.hero-slogan {
  font-size: 1rem; font-style: italic; opacity: 0.75; margin-bottom: 36px;
  letter-spacing: 0.04em;
}
.btn-hero {
  display: inline-block;
  border: 2px solid rgba(255,255,255,0.7);
  color: var(--white); background: rgba(255,255,255,0.08);
  padding: 14px 36px; border-radius: 8px;
  font-size: 1rem; font-weight: 600; letter-spacing: 0.03em;
  transition: background 0.25s, border-color 0.25s, color 0.25s;
}
.btn-hero:hover { background: var(--blue-mid); border-color: var(--blue-mid); color: var(--white); }
.btn-hero:focus-visible { outline: 3px solid var(--blue-light); outline-offset: 3px; }
```

---

### Task 4: Sobre seção

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add sobre markup after hero section**

```html
<section id="sobre" aria-label="Sobre a Santorini Eyewear">
  <div class="sobre-inner">
    <div class="sobre-text">
      <h2 class="script section-title blue">Sobre nós</h2>
      <p class="sobre-lead">Fundada em 2012, a Santorini Eyewear nasceu da experiência de seu CEO no mercado de moda, trazendo um olhar estratégico para tendências e estilo.</p>
      <p>Com a migração para o setor óptico, incorporamos esse diferencial ao desenvolvimento do nosso portfólio, oferecendo produtos que unem design, versatilidade e alto potencial de venda.</p>
      <p>Atuamos no mercado atacadista de artigos de ótica, fornecendo soluções completas para óticas, revendedores e distribuidores em todo o Brasil. Nosso foco está em oferecer produtos com alto potencial de venda, acompanhando as principais tendências do setor e garantindo um mix estratégico para diferentes perfis de público.</p>
    </div>
    <div class="sobre-image">
      <img src="Santorini Eyewear_midias/midia_2.jpg" alt="Modelo masculino usando armação preta Santorini Eyewear" loading="lazy">
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add sobre CSS**

```css
/* ── SOBRE ── */
#sobre { background: var(--white); padding: 96px 24px; }
.sobre-inner {
  max-width: 1200px; margin: 0 auto;
  display: grid; grid-template-columns: 1fr 1fr; gap: 64px; align-items: center;
}
.sobre-text { display: flex; flex-direction: column; gap: 20px; }
.section-title { font-size: clamp(2.2rem, 5vw, 3.2rem); line-height: 1.1; }
.section-title.blue { color: var(--blue-deep); }
.section-title.white { color: var(--white); }
.section-title.centered { text-align: center; }
.sobre-lead { font-size: 1.15rem; font-weight: 500; color: var(--blue-deep); line-height: 1.6; }
.sobre-text p { color: var(--text-muted); line-height: 1.8; font-size: 0.97rem; }
.sobre-image img { border-radius: 12px; width: 100%; height: 480px; object-fit: cover; box-shadow: 0 16px 48px rgba(26,63,122,0.15); }
@media (max-width: 768px) {
  .sobre-inner { grid-template-columns: 1fr; gap: 40px; }
  .sobre-image { order: -1; }
  .sobre-image img { height: 320px; }
}
```

---

### Task 5: Missão / Visão / Valores

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add valores markup after sobre section**

```html
<section id="valores" aria-label="Missão, visão e valores">
  <div class="valores-inner">
    <h2 class="script section-title white centered">Missão, visão e valores</h2>
    <div class="valores-grid">
      <div class="valor-card">
        <div class="valor-icon" aria-hidden="true">
          <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/></svg>
        </div>
        <h3>Missão</h3>
        <p>Entregar aos nossos clientes produtos ópticos com alta qualidade, excelente margem de lucro e reposição ágil, ajudando óticas e revendedores a vender mais todos os dias.</p>
      </div>
      <div class="valor-card">
        <div class="valor-icon" aria-hidden="true">
          <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M12 8v4l3 3"/></svg>
        </div>
        <h3>Visão</h3>
        <p>Ser o principal parceiro de óticas e revendedores no Brasil, reconhecido por oferecer produtos que giram rápido, tendências atualizadas e condições comerciais que impulsionam resultados.</p>
      </div>
      <div class="valor-card">
        <div class="valor-icon" aria-hidden="true">
          <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
        </div>
        <h3>Valores</h3>
        <ul>
          <li>Foco em resultado</li>
          <li>Qualidade que vende</li>
          <li>Agilidade</li>
          <li>Parceria de verdade</li>
          <li>Preço competitivo</li>
          <li>Inovação constante</li>
        </ul>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add valores CSS**

```css
/* ── VALORES ── */
#valores { background: var(--blue-deep); padding: 96px 24px; }
.valores-inner { max-width: 1200px; margin: 0 auto; }
.valores-inner .section-title { margin-bottom: 56px; }
.valores-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 32px; }
.valor-card {
  background: var(--white); border-radius: 16px;
  padding: 40px 32px; box-shadow: 0 8px 32px rgba(0,0,0,0.12);
  display: flex; flex-direction: column; gap: 16px;
}
.valor-icon { color: var(--blue-deep); }
.valor-card h3 { font-size: 1.25rem; font-weight: 700; color: var(--blue-deep); }
.valor-card p { color: var(--text-muted); line-height: 1.7; font-size: 0.95rem; }
.valor-card ul { list-style: none; display: flex; flex-direction: column; gap: 8px; }
.valor-card ul li {
  color: var(--text-muted); font-size: 0.95rem; padding-left: 18px;
  position: relative;
}
.valor-card ul li::before {
  content: ''; position: absolute; left: 0; top: 50%;
  transform: translateY(-50%);
  width: 8px; height: 8px; border-radius: 50%; background: var(--blue-mid);
}
@media (max-width: 900px) { .valores-grid { grid-template-columns: 1fr; } }
```

---

### Task 6: Portfólio (grid editorial)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add portfolio markup after valores section**

```html
<section id="portfolio" aria-label="Portfólio Santorini Eyewear">
  <div class="portfolio-inner">
    <h2 class="script section-title blue centered">Nosso portfólio</h2>
    <p class="portfolio-desc">Design, estilo e versatilidade em cada peça. Conheça alguns dos produtos do nosso catálogo.</p>
    <div class="portfolio-grid">
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_1.png" alt="Mulher usando óculos escuros Santorini" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_2.jpg" alt="Armação preta masculina Santorini" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_3.jpg" alt="Armação cat-eye feminina Santorini" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_4.jpg" alt="Produto óptico Santorini Eyewear" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_5.jpg" alt="Óculos masculino Santorini" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_6.jpg" alt="Produto óptico Santorini Eyewear" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_7.jpg" alt="Produto óptico Santorini Eyewear" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_8.jpg" alt="Produto óptico Santorini Eyewear" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_9.jpg" alt="Produto óptico Santorini Eyewear" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_10.jpg" alt="Produto óptico Santorini Eyewear" loading="lazy"></div>
      <div class="portfolio-item"><img src="Santorini Eyewear_midias/midia_11.jpg" alt="Produto óptico Santorini Eyewear" loading="lazy"></div>
    </div>
    <div class="portfolio-cta">
      <a href="https://wa.me/5521967434256" class="btn-primary">Solicitar catálogo completo</a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add portfolio CSS**

```css
/* ── PORTFÓLIO ── */
#portfolio { background: var(--off-white); padding: 96px 24px; }
.portfolio-inner { max-width: 1200px; margin: 0 auto; }
.portfolio-desc { text-align: center; color: var(--text-muted); margin: -24px auto 48px; max-width: 520px; line-height: 1.7; }
.portfolio-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
.portfolio-item {
  position: relative; overflow: hidden; border-radius: 10px;
  aspect-ratio: 4/3;
}
.portfolio-item img {
  width: 100%; height: 100%; object-fit: cover;
  transition: transform 0.4s ease;
}
.portfolio-item:hover img { transform: scale(1.05); }
.portfolio-item::after {
  content: ''; position: absolute; inset: 0;
  background: rgba(26,63,122,0); transition: background 0.35s;
}
.portfolio-item:hover::after { background: rgba(26,63,122,0.22); }
.portfolio-cta { text-align: center; margin-top: 48px; }
.btn-primary {
  display: inline-block;
  background: var(--blue-deep); color: var(--white);
  padding: 14px 36px; border-radius: 8px;
  font-size: 1rem; font-weight: 600;
  transition: background 0.25s;
}
.btn-primary:hover { background: var(--blue-mid); }
.btn-primary:focus-visible { outline: 3px solid var(--blue-light); outline-offset: 3px; }
@media (max-width: 900px) { .portfolio-grid { grid-template-columns: repeat(2,1fr); } }
@media (max-width: 600px) { .portfolio-grid { grid-template-columns: 1fr; } }
```

---

### Task 7: Mercado de atuação

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add mercado markup after portfolio section**

```html
<section id="mercado" aria-label="Mercado de atuação">
  <div class="mercado-inner">
    <h2 class="script section-title blue centered">Mercado de atuação</h2>
    <p class="mercado-desc">Atuamos no mercado atacadista de artigos de ótica, fornecendo soluções completas para óticas, revendedores e distribuidores em todo o Brasil.</p>
    <div class="mercado-stats">
      <div class="stat-item">
        <div class="stat-icon" aria-hidden="true">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>
        </div>
        <span class="stat-value">Desde 2012</span>
        <span class="stat-label">Experiência no mercado</span>
      </div>
      <div class="stat-item">
        <div class="stat-icon" aria-hidden="true">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></svg>
        </div>
        <span class="stat-value">Todo o Brasil</span>
        <span class="stat-label">Abrangência nacional</span>
      </div>
      <div class="stat-item">
        <div class="stat-icon" aria-hidden="true">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="23 6 13.5 15.5 8.5 10.5 1 18"/><polyline points="17 6 23 6 23 12"/></svg>
        </div>
        <span class="stat-value">Reposição ágil</span>
        <span class="stat-label">Estoque pronto para entrega</span>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add mercado CSS**

```css
/* ── MERCADO ── */
#mercado { background: var(--white); padding: 96px 24px; }
.mercado-inner { max-width: 1200px; margin: 0 auto; }
.mercado-desc {
  text-align: center; color: var(--text-muted);
  max-width: 600px; margin: -16px auto 56px;
  line-height: 1.8; font-size: 1rem;
}
.mercado-stats { display: grid; grid-template-columns: repeat(3,1fr); gap: 32px; }
.stat-item {
  display: flex; flex-direction: column; align-items: center; gap: 12px;
  padding: 40px 24px; border-radius: 16px;
  background: var(--gray-light);
  text-align: center; transition: box-shadow 0.25s;
}
.stat-item:hover { box-shadow: 0 8px 32px rgba(26,63,122,0.1); }
.stat-icon {
  width: 60px; height: 60px; border-radius: 50%;
  background: var(--blue-deep); color: var(--white);
  display: flex; align-items: center; justify-content: center;
}
.stat-value { font-size: 1.3rem; font-weight: 700; color: var(--blue-deep); }
.stat-label { font-size: 0.85rem; color: var(--text-muted); }
@media (max-width: 768px) { .mercado-stats { grid-template-columns: 1fr; max-width: 360px; margin: 0 auto; } }
```

---

### Task 8: Depoimentos

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add depoimentos markup after mercado section**

```html
<section id="depoimentos" aria-label="Depoimentos de clientes">
  <div class="depoimentos-inner">
    <h2 class="script section-title blue centered">O que dizem sobre nós</h2>
    <p class="depoimentos-desc">Avaliações reais de clientes no Google.</p>
    <div class="depoimentos-grid">
      <div class="depoimento-card">
        <img src="Santorini Eyewear_depoimentos/depoimento_1.png" alt="Avaliações de clientes Santorini Eyewear no Google — captura 1" loading="lazy">
      </div>
      <div class="depoimento-card">
        <img src="Santorini Eyewear_depoimentos/depoimento_2.png" alt="Avaliações de clientes Santorini Eyewear no Google — captura 2" loading="lazy">
      </div>
      <div class="depoimento-card">
        <img src="Santorini Eyewear_depoimentos/depoimento_3.png" alt="Avaliações de clientes Santorini Eyewear no Google — captura 3" loading="lazy">
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add depoimentos CSS**

```css
/* ── DEPOIMENTOS ── */
#depoimentos { background: var(--gray-light); padding: 96px 24px; }
.depoimentos-inner { max-width: 1100px; margin: 0 auto; }
.depoimentos-desc {
  text-align: center; color: var(--text-muted); margin: -16px auto 48px; font-size: 0.95rem;
}
.depoimentos-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 24px; }
.depoimento-card {
  background: var(--white); border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.07);
  overflow: hidden; transition: box-shadow 0.25s;
}
.depoimento-card:hover { box-shadow: 0 8px 32px rgba(26,63,122,0.12); }
.depoimento-card img { width: 100%; height: auto; display: block; }
@media (max-width: 768px) { .depoimentos-grid { grid-template-columns: 1fr; max-width: 420px; margin: 0 auto; } }
```

---

### Task 9: Contato + Mapa

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add contato markup after depoimentos section**

```html
<section id="contato" aria-label="Localização e contato">
  <div class="contato-inner">
    <h2 class="script section-title blue centered">Contato</h2>
    <div class="contato-grid">
      <div class="contato-map">
        <iframe
          src="https://maps.google.com/maps?q=Rua+das+Rosas,+95,+Vila+Valqueire,+Rio+de+Janeiro,+RJ&output=embed"
          width="100%" height="400" frameborder="0"
          allowfullscreen loading="lazy"
          title="Localização Santorini Eyewear — Rua das Rosas 95, Rio de Janeiro"
          aria-label="Mapa mostrando a localização da Santorini Eyewear"></iframe>
      </div>
      <div class="contato-info">
        <div class="info-item">
          <div class="info-icon" aria-hidden="true">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/><circle cx="12" cy="10" r="3"/></svg>
          </div>
          <div>
            <strong>Endereço</strong>
            <p>Rua das Rosas, 95 — Vila Valqueire<br>Rio de Janeiro – RJ, 21330-680</p>
          </div>
        </div>
        <div class="info-item">
          <div class="info-icon" aria-hidden="true">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 13a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.6 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L7.91 9.91a16 16 0 0 0 6.06 6.06l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
          </div>
          <div>
            <strong>Telefone</strong>
            <p>(21) 96743-4256</p>
          </div>
        </div>
        <div class="info-item">
          <div class="info-icon" aria-hidden="true">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
          </div>
          <div>
            <strong>E-mail</strong>
            <p><a href="mailto:santorinioculos@hotmail.com">santorinioculos@hotmail.com</a></p>
          </div>
        </div>
        <div class="info-item">
          <div class="info-icon" aria-hidden="true">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
          </div>
          <div>
            <strong>Horário de funcionamento</strong>
            <p>Segunda a sexta: 9h às 17h</p>
          </div>
        </div>
        <div class="info-item">
          <div class="info-icon" aria-hidden="true">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="2" width="20" height="20" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"/></svg>
          </div>
          <div>
            <strong>Instagram</strong>
            <p><a href="https://www.instagram.com/santorinioculos/" target="_blank" rel="noopener noreferrer">@santorinioculos</a></p>
          </div>
        </div>
        <a href="https://wa.me/5521967434256" class="btn-whatsapp-contato" aria-label="Falar com a Santorini pelo WhatsApp">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/></svg>
          Chamar no WhatsApp
        </a>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add contato CSS**

```css
/* ── CONTATO ── */
#contato { background: var(--white); padding: 96px 24px; }
.contato-inner { max-width: 1200px; margin: 0 auto; }
.contato-inner .section-title { margin-bottom: 56px; }
.contato-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 48px; align-items: start; }
.contato-map { border-radius: 16px; overflow: hidden; box-shadow: 0 8px 32px rgba(26,63,122,0.1); }
.contato-map iframe { display: block; }
.contato-info { display: flex; flex-direction: column; gap: 28px; }
.info-item { display: flex; gap: 16px; align-items: flex-start; }
.info-icon {
  flex-shrink: 0; width: 40px; height: 40px; border-radius: 8px;
  background: var(--gray-light); color: var(--blue-deep);
  display: flex; align-items: center; justify-content: center;
}
.info-item strong { display: block; font-weight: 600; color: var(--blue-deep); margin-bottom: 4px; font-size: 0.9rem; }
.info-item p, .info-item a { color: var(--text-muted); font-size: 0.95rem; line-height: 1.5; }
.info-item a:hover { color: var(--blue-mid); }
.btn-whatsapp-contato {
  display: flex; align-items: center; justify-content: center; gap: 10px;
  background: #25D366; color: var(--white);
  padding: 14px 24px; border-radius: 10px;
  font-size: 1rem; font-weight: 600;
  transition: background 0.25s; margin-top: 8px;
}
.btn-whatsapp-contato:hover { background: #1EB858; }
.btn-whatsapp-contato:focus-visible { outline: 3px solid #25D366; outline-offset: 3px; }
@media (max-width: 768px) { .contato-grid { grid-template-columns: 1fr; } }
```

---

### Task 10: Botão flutuante WhatsApp

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add floating WhatsApp button markup before `<div id="root">`**

```html
<a href="https://wa.me/5521967434256"
   class="whatsapp-float"
   aria-label="Falar pelo WhatsApp"
   target="_blank" rel="noopener noreferrer">
  <svg width="28" height="28" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
    <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/>
  </svg>
</a>
```

- [ ] **Step 2: Add floating button CSS**

```css
/* ── WHATSAPP FLUTUANTE ── */
.whatsapp-float {
  position: fixed; bottom: 24px; right: 24px; z-index: 9999;
  width: 56px; height: 56px; border-radius: 50%;
  background: #25D366; color: var(--white);
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 4px 16px rgba(37,211,102,0.35);
  transition: background 0.25s, box-shadow 0.25s;
}
.whatsapp-float:hover { background: #1EB858; box-shadow: 0 6px 24px rgba(37,211,102,0.45); }
.whatsapp-float:focus-visible { outline: 3px solid #25D366; outline-offset: 3px; }
```

---

### Task 11: sitemap.xml e robots.txt

**Files:**
- Create: `sitemap.xml`
- Create: `robots.txt`

- [ ] **Step 1: Create sitemap.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://santorinieyewear.com.br/</loc>
    <lastmod>2026-05-06</lastmod>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

- [ ] **Step 2: Create robots.txt**

```
User-agent: *
Allow: /
Sitemap: https://santorinieyewear.com.br/sitemap.xml
```

---

### Task 12: Verificação final

**Files:**
- Read: `index.html`

- [ ] **Step 1: Verify lang attribute**
```bash
grep 'lang="pt-BR"' index.html && echo "PASS: lang pt-BR OK"
```
Expected: `PASS: lang pt-BR OK`

- [ ] **Step 2: Verify all WhatsApp links use full wa.me URL**
```bash
grep -c 'wa.me/5521967434256' index.html
```
Expected: `4` (header btn, hero CTA, contato btn, floating btn)

- [ ] **Step 3: Verify all sections present**
```bash
for id in hero sobre valores portfolio mercado depoimentos contato; do
  grep -q "id=\"$id\"" index.html && echo "OK: #$id" || echo "MISSING: #$id"
done
```
Expected: all 7 lines print `OK`

- [ ] **Step 4: Verify MonteSite footer elements**
```bash
grep -c 'montesite-footer-badge' index.html && grep -c 'get-footer-iframe' index.html
```
Expected: `1` and `1`

- [ ] **Step 5: Open in browser and do visual check**
```bash
xdg-open index.html 2>/dev/null || open index.html 2>/dev/null || echo "Open index.html manually in your browser"
```
Checklist visual:
- [ ] Header fixo azul com logo branca
- [ ] Hero full-bleed com overlay e texto centralizado
- [ ] Botão flutuante WhatsApp aparece fixo canto inferior direito, sem animação
- [ ] Grid de portfólio com 11 imagens
- [ ] Mapa embutido visível na seção de contato
- [ ] Site responsivo em mobile (menu hamburguer)
