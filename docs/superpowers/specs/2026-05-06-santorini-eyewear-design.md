# Santorini Eyewear — Spec do site institucional

**Data:** 2026-05-06  
**Estilo escolhido:** Opção A · Editorial Fashion  
**Idioma:** pt-BR (obrigatório, `lang="pt-BR"` na tag `<html>`)

---

## 1. Identidade visual

### Paleta de cores
| Papel | Hex | Uso |
|---|---|---|
| Base (60%) | `#FFFFFF` / `#F8F9FA` | Fundo das seções principais |
| Primária (30%) | `#1A3F7A` | Header, seção valores, acentos, botões |
| Destaque (10%) | `#2E6DB4` | Hover, ícones, bordas de ênfase |
| Texto | `#1A1A2E` | Corpo de texto |
| Overlay hero | `rgba(10,25,60,0.70)` | Overlay sobre foto hero |

### Tipografia (Google Fonts)
- **Títulos / logo**: Dancing Script (cursiva, alinhada ao wordmark)
- **Corpo / UI**: Inter (sem-serifa, legível)

---

## 2. Assets disponíveis

| Arquivo | Uso |
|---|---|
| `1778084193288_santorini_logo_site.png` | Logo no header e favicon |
| `Santorini Eyewear_midias/midia_1.png` | Fundo do Hero (mulher de perfil, óculos escuros, céu azul) |
| `Santorini Eyewear_midias/midia_2.jpg` | Seção Sobre (homem, armação preta, foto editorial) |
| `Santorini Eyewear_midias/midia_3.jpg` a `midia_11.jpg` | Grid do Portfólio (9 imagens) |
| `Santorini Eyewear_depoimentos/depoimento_1.png` a `depoimento_3.png` | Cards de depoimentos |

---

## 3. Estrutura HTML (arquivo único `index.html`)

### Ordem das seções
1. `<header>` fixo
2. `#hero`
3. `#sobre`
4. `#valores`
5. `#portfolio`
6. `#mercado`
7. `#depoimentos`
8. `#contato`
9. Rodapé MonteSite
10. Botão flutuante WhatsApp

---

## 4. Especificação por seção

### 4.1 `<header>` — fixo no topo
- Fundo: `#1A3F7A` (azul Santorini), altura ~72px
- Esquerda: logo `santorini_logo_site.png` com `filter: brightness(0) invert(1)` para aparecer branca sobre o fundo azul
- Centro: links de ancoragem — Sobre · Portfólio · Valores · Depoimentos · Contato
- Direita: botão "Falar no WhatsApp" — fundo branco, texto azul, hover fundo azul claro
- Mobile: hamburguer menu, menu drawer azul
- Não sobrepor o Hero: `padding-top` da próxima seção = altura do header

### 4.2 `#hero` — Editorial full-bleed
- Fundo: `midia_1.png` como `background-image`, `background-size: cover`, `background-position: center top`
- Overlay: `rgba(10,25,60,0.70)` sobre a imagem
- Altura mínima: `100vh`
- Conteúdo centralizado verticalmente:
  - `<h1>` Santorini — Dancing Script, ~5rem, branco
  - `<h2>` "Seu parceiro atacadista em artigos de ótica" — Inter 300, ~1.4rem, branco 90%
  - Parágrafo slogan: "Santorini, perfeito pra você."
  - Botão CTA: "Falar no WhatsApp" → `href="https://wa.me/5521967434256"`, outline branco, hover azul Egeu
- Sem seta/ícone de scroll na parte inferior

### 4.3 `#sobre` — A empresa
- Fundo: `#FFFFFF`
- Layout: dois painéis lado a lado (50/50) — texto à esquerda, imagem à direita (`midia_2.jpg`)
- `<h2>` "Sobre nós" — Dancing Script, azul Santorini
- Texto: história (fundada em 2012, CEO com background em moda, migração para setor óptico)
- Mobile: imagem acima, texto abaixo

### 4.4 `#valores` — Missão · Visão · Valores
- Fundo: `#1A3F7A`
- `<h2>` "Missão, visão e valores" — branco, Dancing Script, centralizado
- 3 cards brancos (border-radius 12px, sombra suave), layout 3 colunas
  - **Missão**: "Entregar produtos ópticos com alta qualidade, excelente margem e reposição ágil"
  - **Visão**: "Ser o principal parceiro de óticas e revendedores no Brasil"
  - **Valores**: Lista: Foco em resultado · Qualidade que vende · Agilidade · Parceria de verdade · Preço competitivo · Inovação constante
- Mobile: cards empilhados

### 4.5 `#portfolio` — Portfólio
- Fundo: `#F8F9FA`
- `<h2>` "Nosso portfólio" — Dancing Script, azul Santorini, centralizado
- Grid 3 colunas, `gap: 16px`, usando todas as 11 mídias (`midia_1.png` a `midia_11.jpg`) — as mesmas imagens do hero e do Sobre podem ser reutilizadas aqui para um portfólio completo
- Cada card: imagem com `object-fit: cover`, hover com overlay azul semitransparente
- Mobile: 1 coluna; tablet: 2 colunas

### 4.6 `#mercado` — Mercado de atuação
- Fundo: `#FFFFFF`
- `<h2>` "Mercado de atuação" — Dancing Script, azul Santorini, centralizado
- Parágrafo descritivo (mercado atacadista, óticas e revendedores em todo o Brasil)
- 3 ícones de destaque em linha:
  - "Desde 2012" · "Todo o Brasil" · "Reposição ágil"
- Fundo dos ícones: círculo azul

### 4.7 `#depoimentos` — O que dizem sobre nós
- Fundo: `#F0F4F8`
- `<h2>` "O que dizem sobre nós" — Dancing Script, azul Santorini, centralizado
- 3 cards lado a lado com `depoimento_1.png`, `depoimento_2.png`, `depoimento_3.png`
- Cards: fundo branco, border-radius 12px, sombra, imagem com `width: 100%`
- Mobile: swipe horizontal (overflow-x: auto) ou empilhado

### 4.8 `#contato` — Localização e contato
- Fundo: `#FFFFFF`
- `<h2>` "Contato" — Dancing Script, azul Santorini, centralizado
- Layout dois painéis:
  - **Esquerda**: mapa Google embed via `<iframe>` — URL: `https://maps.google.com/maps?q=Rua+das+Rosas,+95,+Vila+Valqueire,+Rio+de+Janeiro,+RJ&output=embed`, `width="100%"`, `height="400"`, `frameborder="0"`, `allowfullscreen`
  - **Direita**: 
    - Endereço: Rua das Rosas, 95 – Vila Valqueire, Rio de Janeiro – RJ
    - Telefone: (21) 96743-4256
    - E-mail: santorinioculos@hotmail.com
    - Horário: Segunda a sexta, 9h às 17h
    - Instagram: @santorinioculos → link `https://www.instagram.com/santorinioculos/`
    - Botão WhatsApp: "Chamar no WhatsApp" → `href="https://wa.me/5521967434256"`
- Mobile: mapa acima, informações abaixo

### 4.9 Rodapé MonteSite
```html
<!-- Rodapé MonteSite - Atualização Automática -->
<div id="montesite-footer-badge"></div>
<script src="https://vaabpicspdbolvutnscp.supabase.co/functions/v1/get-footer-iframe"></script>
```
Inserido logo após `<div id="root"></div>` no `<body>`.

### 4.10 Botão flutuante WhatsApp
- Posição: `fixed`, `bottom: 24px`, `right: 24px`, `z-index: 9999`
- Link: `href="https://wa.me/5521967434256"` — URL completa, sem JS redirect
- Ícone SVG do WhatsApp + cor `#25D366`
- Sem animação de pulo ou piscar
- `aria-label="Falar pelo WhatsApp"`

---

## 5. SEO e metadados

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
</head>
```

---

## 6. Acessibilidade

- Contraste mínimo 4.5:1 em todos os estados de botão
- `alt` descritivo em todas as imagens
- Navegação por teclado: `focus-visible` em todos os elementos interativos
- Header com `role="banner"`, main com `role="main"`, nav com `role="navigation"`

---

## 7. Responsividade

- **Mobile** (<768px): menu hamburguer, colunas empilhadas, grid 1 coluna
- **Tablet** (768px–1024px): grid 2 colunas nos produtos
- **Desktop** (>1024px): layout completo conforme descrito

---

## 8. Arquivos a gerar

| Arquivo | Conteúdo |
|---|---|
| `index.html` | Site completo (HTML + CSS + JS inline) |
| `sitemap.xml` | Sitemap com URL da página principal |
| `robots.txt` | `User-agent: * / Allow: /` |

---

## 9. Informações de contato (referência)

- **WhatsApp**: +55 21 96743-4256 → `https://wa.me/5521967434256`
- **E-mail**: santorinioculos@hotmail.com
- **Endereço**: Rua das Rosas, 95 – Vila Valqueire, Rio de Janeiro – RJ, 21330-680
- **Horário**: Segunda a sexta, 9h às 17h
- **Instagram**: https://www.instagram.com/santorinioculos/
- **CNPJ**: 57.503.557/0001-62
- **Mapa embed**: https://www.google.com/maps/place/R.+das+Rosas,+95+-+Vila+Valqueire,+Rio+de+Janeiro+-+RJ,+21330-680/
