# Varick Global — WordPress Ready Code

**Complete HTML, CSS, and JavaScript compiled for WordPress hosting.**

This document contains every piece of code needed to reproduce the Varick Global site on WordPress. Each block is labeled with (1) where in WordPress it goes and (2) how to add it.

**Companion files:** `varick-global-COMPLETE.html` (single-file working prototype), `VARICK_WORDPRESS_MCP_GUIDE.md` (step-by-step build process), `VARICK_LIGHTER_PALETTE.md` (alternative palette).

---

## Table of Contents

1. Overview & installation flow
2. **STEP 1 — Site-wide `<head>` code** (fonts, meta, JSON-LD schema)
3. **STEP 2 — Additional CSS** (the entire design system)
4. **STEP 3 — Global JavaScript** (footer template)
5. **STEP 4 — Header template** (nav + mobile menu)
6. **STEP 5 — Footer template** (footer + chat + palette picker + toast + exit-intent)
7. **STEP 6 — Home page HTML**
8. **STEP 7 — VG Elite page HTML**
9. **STEP 8 — AI Property Match page HTML**
10. **STEP 9 — Four calculator pages** (Mortgage · Affordability · Rent vs. Buy · Closing Costs)
11. **STEP 10 — Valuation page HTML**
12. **STEP 11 — Contact page HTML**
13. **STEP 12 — Journal page HTML**
14. **STEP 13 — About / Team / FAQ / Sitemap** (content templates)
15. **STEP 14 — Remaining pages** (Search, Neighborhoods, Sold, New Developments, Foreclosures, Guides, Careers, Press)
16. Testing checklist

---

## 1. Overview & installation flow

Every code block below is one of three types:

| Type | Where it goes in WordPress |
|---|---|
| **Site head snippet** | `Appearance → Customize → Additional CSS` (for CSS) OR a plugin like **Insert Headers and Footers** (for `<script>` / `<link>` / JSON-LD) |
| **Template code** | `Appearance → Site Editor` → edit the Header or Footer template part → Custom HTML block |
| **Page code** | Create the page in WordPress → add a Custom HTML block → paste |

**Recommended plugins for a smooth install:**

- **Insert Headers and Footers** (or **WPCode**) — for the head snippets and global JS
- **Rank Math SEO** — will replace the manual JSON-LD once configured properly
- **Fluent Forms** — for the contact/valuation forms (replaces the `<form>` markup below with a Fluent Forms shortcode)

**Approach note:** Each `<div class="page" id="p-...">` wrapper from the single-file prototype becomes a **separate WordPress page**. The `go()` SPA routing function is not needed on WordPress — each page has its own real URL.

---

## 2. STEP 1 — Site-wide `<head>` code

**Where it goes:** Install the **Insert Headers and Footers** plugin, then paste each block below into the "Scripts in Header" box.

### 2.1 Google Fonts

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=Raleway:wght@300;400;500;600;700&family=Montserrat:wght@400;500;600;700&display=swap" rel="stylesheet">
```

### 2.2 Meta tags (or use Rank Math to set these per page)

```html
<meta name="description" content="Varick Global is South Florida's premier luxury real estate firm serving Miami-Dade, Broward, and Palm Beach. Residential, commercial, HOA advisory, and the exclusive VG Elite Sports & Entertainment division since 2016.">
<meta name="keywords" content="luxury real estate South Florida, Miami luxury homes, Aventura real estate, commercial real estate Miami, distressed HOA Florida, Varick Global, Sports Entertainment real estate">
<meta property="og:title" content="Varick Global — Where Luxury Meets Precision">
<meta property="og:description" content="South Florida's premier luxury real estate advisors.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://varickglobal.com">
<meta property="og:image" content="https://varickglobal.com/og.jpg">
<meta name="robots" content="index,follow,max-image-preview:large">
<meta name="author" content="Varick Global Real Estate Advisors">
```

### 2.3 JSON-LD Schema (GEO signal)

```html
<script type="application/ld+json">
{
  "@context":"https://schema.org",
  "@graph":[
    {
      "@type":"RealEstateAgent",
      "@id":"https://varickglobal.com/#agent",
      "name":"Varick Global Real Estate Advisors",
      "alternateName":"Varick Global",
      "description":"South Florida's premier luxury real estate advisory firm. Residential, commercial, leasing, land, HOA, and the exclusive VG Elite Sports & Entertainment division. Serving Miami-Dade, Broward, and Palm Beach counties since 2016.",
      "url":"https://varickglobal.com",
      "logo":"https://varickglobal.com/logo.png",
      "telephone":"+17863527547",
      "email":"info@varickglobal.com",
      "foundingDate":"2016",
      "address":{"@type":"PostalAddress","streetAddress":"19505 Biscayne Blvd, Suite 2350","addressLocality":"Aventura","addressRegion":"FL","postalCode":"33180","addressCountry":"US"},
      "geo":{"@type":"GeoCoordinates","latitude":25.9564,"longitude":-80.1394},
      "areaServed":[
        {"@type":"AdministrativeArea","name":"Miami-Dade County"},
        {"@type":"AdministrativeArea","name":"Broward County"},
        {"@type":"AdministrativeArea","name":"Palm Beach County"}
      ],
      "priceRange":"$$$$",
      "openingHoursSpecification":{"@type":"OpeningHoursSpecification","dayOfWeek":["Monday","Tuesday","Wednesday","Thursday","Friday"],"opens":"09:00","closes":"18:00"},
      "knowsLanguage":["en","es"],
      "sameAs":[
        "https://www.facebook.com/VarickGlobal/",
        "https://x.com/varickglobal",
        "https://www.linkedin.com/company/varickglobal/",
        "https://www.instagram.com/varickglobal",
        "https://www.youtube.com/@VarickGlobal"
      ],
      "aggregateRating":{"@type":"AggregateRating","ratingValue":"4.9","reviewCount":"127","bestRating":"5"}
    }
  ]
}
</script>
```

---

## 3. STEP 2 — Additional CSS

**Where it goes:** `Appearance → Customize → Additional CSS`.

This is the entire design system — colors, typography, all components, both palettes, and responsive rules. Paste as-is.

```css
/* ============ REFINED PALETTE ============ */
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --crimson:#a6192e; --vivid:#d2203a;
  --gold:#b8952a; --gold-light:#d4a93a; --gold-soft:#f5eed8;
  --cream:#f5f2ed; --parchment:#efeae1; --stone:#e5dfd1;
  --white:#ffffff;
  --onyx:#111111; --graphite:#2a2a2a; --pewter:#6b6b68;
  --silver:#b5b3ad; --silver-light:#d8d5ce;
  --vio:#6d47d9; --vio2:#8b60ff;
  --vio-soft:#f4f0ff; --vio-mist:#ebe4ff; --plum:#3a2569;
  --f-display:'Cormorant Garamond',Georgia,serif;
  --f-body:'Raleway',sans-serif;
  --f-accent:'Montserrat',sans-serif;
}

/* ============ LIGHTER PALETTE (optional theme) ============ */
body.palette-lighter{
  --crimson:#b32338; --vivid:#dc2745;
  --gold:#c9a238; --gold-light:#dcb648; --gold-soft:#faf3dc;
  --cream:#faf8f4; --parchment:#f4ede4; --stone:#ece0d8;
  --onyx:#1a1a1a; --graphite:#333333; --pewter:#7a7773;
  --silver:#bab8b0; --silver-light:#e2ddd4;
  --vio-soft:#f7f3ff; --vio-mist:#eee6ff;
}

html{scroll-behavior:smooth}
body{font-family:var(--f-body);background:var(--cream);color:var(--onyx);line-height:1.7;font-weight:300;-webkit-font-smoothing:antialiased}
a{color:inherit;text-decoration:none}
button{cursor:pointer;font-family:inherit;border:none;background:none}

/* ============ NAV ============ */
#nav{background:rgba(245,242,237,0.96);backdrop-filter:blur(10px);display:flex;align-items:center;justify-content:space-between;padding:0 40px;height:68px;position:sticky;top:0;z-index:200;border-bottom:1px solid var(--silver-light)}
.nl{font-family:var(--f-display);font-size:22px;font-weight:600;letter-spacing:2px;color:var(--onyx);cursor:pointer}
.nl span{color:var(--crimson)}
.nm{display:flex;align-items:center;height:68px;list-style:none}
.ni{position:relative;height:68px;display:flex;align-items:center}
.nb{color:var(--pewter);font-family:var(--f-accent);font-size:11px;letter-spacing:1.5px;text-transform:uppercase;padding:0 14px;height:68px;display:flex;align-items:center;gap:4px;cursor:pointer;white-space:nowrap;font-weight:600}
.nb:hover{color:var(--onyx)}
.nch{font-size:9px}
.nd{display:none;position:absolute;top:68px;left:0;background:var(--white);border-top:2px solid var(--crimson);min-width:240px;z-index:300;box-shadow:0 8px 32px rgba(17,17,17,0.08);border:1px solid var(--silver-light)}
.ni:hover .nd{display:block}
.dgl{padding:12px 18px 6px;font-family:var(--f-accent);font-size:9px;letter-spacing:2px;text-transform:uppercase;color:var(--crimson);border-bottom:1px solid var(--silver-light);font-weight:700}
.dl{display:block;color:var(--graphite);font-size:12px;padding:11px 18px;border-bottom:1px solid var(--silver-light);font-weight:400}
.dl:hover{color:var(--crimson);padding-left:24px;background:var(--cream)}
.nc{background:var(--crimson);color:#fff;font-family:var(--f-accent);font-size:11px;padding:11px 20px;letter-spacing:2px;text-transform:uppercase;margin-left:10px;font-weight:700;text-decoration:none}
.nc:hover{background:var(--vivid)}

/* ============ UTILITIES ============ */
.ey{font-family:var(--f-accent);font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--crimson);margin-bottom:10px;display:block;font-weight:700}
.eyb{display:inline-block;background:var(--crimson);color:#fff;font-family:var(--f-accent);font-size:10px;letter-spacing:2px;text-transform:uppercase;padding:7px 14px;margin-bottom:20px;font-weight:700}
.br{display:inline-block;background:var(--crimson);color:#fff;font-family:var(--f-accent);font-size:11px;letter-spacing:2.5px;text-transform:uppercase;padding:14px 28px;font-weight:700;border:none;text-decoration:none;text-align:center}
.br:hover{background:var(--vivid)}
.bo{display:inline-block;background:transparent;color:var(--onyx);font-family:var(--f-accent);font-size:11px;letter-spacing:2.5px;text-transform:uppercase;padding:14px 28px;border:1px solid var(--onyx);font-weight:700;text-decoration:none;text-align:center}
.bo:hover{border-color:var(--crimson);color:var(--crimson)}
.sec{padding:72px 40px}
.ctr{max-width:1240px;margin:0 auto}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:32px}
.g3{display:grid;grid-template-columns:repeat(3,1fr);gap:20px}
.g4{display:grid;grid-template-columns:repeat(4,1fr);gap:18px}
.hi{background:var(--parchment);border-left:3px solid var(--crimson);padding:16px 20px;margin-top:18px;font-size:13px;color:var(--graphite);font-style:italic;line-height:1.7}

/* ============ VIDEO HERO ============ */
.vhero{position:relative;width:100%;min-height:100vh;display:flex;align-items:flex-end;justify-content:center;overflow:hidden;background:var(--onyx)}
.vhero .vposter,.vhero video{position:absolute;inset:0;width:100%;height:100%;object-fit:cover}
.vhero .vposter{background:linear-gradient(135deg,#1a0508 0%,#0a0a0a 55%,#1a0508 100%);display:flex;align-items:center;justify-content:center;color:rgba(210,32,58,0.12);font-family:var(--f-display);font-size:220px;letter-spacing:24px;font-weight:600}
.vhero .voverlay{position:absolute;inset:0;background:linear-gradient(180deg,rgba(0,0,0,.4) 0%,rgba(0,0,0,.15) 45%,rgba(0,0,0,.88) 100%);z-index:1}
.vhero .vinner{position:relative;z-index:2;text-align:center;padding:0 24px 108px;max-width:1000px}
.vhero .vey{font-family:var(--f-accent);font-size:12px;letter-spacing:5px;text-transform:uppercase;color:var(--vivid);font-weight:700;margin-bottom:32px}
.vhero h1{font-family:var(--f-display);font-size:clamp(56px,7.5vw,120px);font-weight:300;color:#fff;line-height:1;letter-spacing:-1.5px;margin-bottom:24px}
.vhero h1 em{font-style:italic;color:var(--vivid);font-weight:400}
.vhero .vsub{color:rgba(255,255,255,.9);font-size:17px;max-width:580px;margin:0 auto 48px;line-height:1.75}
.vhero .vctas{display:flex;gap:16px;justify-content:center;flex-wrap:wrap;margin-bottom:36px}
.vhero .vcta-p{background:var(--crimson);color:#fff;padding:18px 40px;font-family:var(--f-accent);font-size:12px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;border:none;text-decoration:none}
.vhero .vcta-p:hover{background:var(--vivid)}
.vhero .vcta-g{background:transparent;color:#fff;padding:18px 40px;font-family:var(--f-accent);font-size:12px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;border:1px solid #fff;text-decoration:none}
.vhero .vcta-g:hover{background:#fff;color:var(--onyx)}
.vhero .vtrust{display:flex;justify-content:center;gap:36px;flex-wrap:wrap;color:rgba(255,255,255,.7);font-family:var(--f-accent);font-size:10px;letter-spacing:2px;text-transform:uppercase;font-weight:600}
@media(max-width:720px){.vhero{min-height:80vh}.vhero .vinner{padding-bottom:80px}.vhero .vposter{font-size:80px;letter-spacing:8px}}

/* ============ IDX / SOCIAL PROOF / AWARDS ============ */
.idx{background:var(--parchment);padding:24px 40px;border-bottom:1px solid var(--silver-light)}
.idxl{font-family:var(--f-accent);font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--graphite);margin-bottom:12px;font-weight:700}
.idxr{display:flex;gap:6px;flex-wrap:wrap}
.idxr select,.idxr input{flex:1 1 130px;min-width:100px;height:44px;border:1px solid var(--silver);background:#fff;padding:0 14px;font-size:13px;color:var(--onyx);outline:none;font-family:inherit}
.idxr button{background:var(--crimson);color:#fff;height:44px;padding:0 24px;font-family:var(--f-accent);font-size:11px;letter-spacing:2px;text-transform:uppercase;font-weight:700;border:none}
.spb{background:var(--white);border-top:1px solid var(--silver-light);border-bottom:1px solid var(--silver-light);padding:32px 40px}
.spb-row{display:flex;justify-content:space-around;flex-wrap:wrap;gap:20px;max-width:1240px;margin:0 auto;text-align:center}
.spb-v{font-family:var(--f-display);font-size:32px;color:var(--crimson);font-weight:500;line-height:1}
.spb-l{font-family:var(--f-accent);font-size:9px;letter-spacing:2.5px;text-transform:uppercase;color:var(--pewter);margin-top:6px;font-weight:600}
.awb{background:var(--white);padding:36px 40px;border-top:1px solid var(--silver-light);border-bottom:1px solid var(--silver-light)}
.awb-ttl{text-align:center;font-family:var(--f-accent);font-size:10px;letter-spacing:3px;color:var(--pewter);text-transform:uppercase;margin-bottom:22px;font-weight:600}
.awb-row{display:flex;justify-content:center;flex-wrap:wrap;gap:36px;align-items:center;max-width:1100px;margin:0 auto}
.awb-item{font-family:var(--f-display);color:var(--graphite);font-size:16px;font-weight:500;letter-spacing:1px;opacity:.7}

/* ============ CARDS & SECTIONS ============ */
.pc{background:var(--white);border:1px solid var(--silver-light);transition:all .2s}
.pc:hover{border-color:var(--crimson);transform:translateY(-3px);box-shadow:0 8px 24px rgba(17,17,17,0.06)}
.pi{height:180px;background:linear-gradient(135deg,var(--stone),var(--parchment));position:relative;display:flex;align-items:center;justify-content:center;font-size:48px}
.pb2{position:absolute;top:12px;left:12px;background:var(--crimson);color:#fff;font-family:var(--f-accent);font-size:9px;padding:5px 11px;letter-spacing:1.5px;text-transform:uppercase;font-weight:700}
.pb2.gold{background:var(--gold)}
.pb{padding:18px}
.pp{color:var(--crimson);font-family:var(--f-display);font-size:24px;font-weight:500;margin-bottom:4px;line-height:1.1}
.pn{font-size:13px;font-weight:500;color:var(--onyx);margin-bottom:2px}
.pa{font-size:11px;color:var(--pewter);margin-bottom:10px}
.pm{display:flex;gap:12px;font-family:var(--f-accent);font-size:10px;color:var(--pewter);flex-wrap:wrap;letter-spacing:1px;font-weight:600}
.st{background:var(--white);padding:26px;border:1px solid var(--silver-light)}
.st:hover{background:var(--parchment);border-color:var(--crimson)}
.si{font-size:28px;margin-bottom:14px}
.stt{font-family:var(--f-display);color:var(--onyx);font-size:20px;font-weight:500;margin-bottom:6px}
.sd{color:var(--pewter);font-size:12px;line-height:1.7}
.nc2{background:var(--white);padding:28px;border:1px solid var(--silver-light);border-top:3px solid var(--crimson)}
.nn{font-family:var(--f-display);color:var(--onyx);font-size:24px;font-weight:500;margin-bottom:8px}
.nsub{color:var(--pewter);font-size:12px;line-height:1.7;margin-bottom:14px}
.npr{color:var(--crimson);font-family:var(--f-accent);font-size:11px;letter-spacing:1.5px;font-weight:600}
.ac{background:var(--white);border:1px solid var(--silver-light)}
.av{height:150px;background:linear-gradient(135deg,var(--parchment),var(--stone));display:flex;align-items:center;justify-content:center;font-size:52px}
.ab{padding:18px}
.an{font-family:var(--f-display);font-size:20px;font-weight:500;color:var(--onyx);margin-bottom:4px}
.at{font-family:var(--f-accent);font-size:10px;color:var(--crimson);letter-spacing:2px;text-transform:uppercase;margin-bottom:12px;font-weight:700}
.abio{font-size:12px;color:var(--pewter);line-height:1.7;margin-bottom:14px}
.acta{display:flex;gap:6px}
.acta a,.acta button{flex:1;font-size:10px;padding:9px;letter-spacing:1.5px}

/* ============ VALUATION / MORTGAGE / CALCS ============ */
.vb{background:var(--parchment);padding:64px 40px;border-top:1px solid var(--silver-light);border-bottom:1px solid var(--silver-light)}
.vf{display:flex;flex-direction:column;gap:12px}
.vi,.vs{height:44px;border:1px solid var(--silver);background:#fff;padding:0 14px;font-size:13px;color:var(--onyx);outline:none;font-family:inherit;width:100%}
.tc{background:var(--white);border:1px solid var(--silver-light);border-left:3px solid var(--crimson);padding:28px}
.tq{font-family:var(--f-display);font-size:17px;font-style:italic;color:var(--graphite);line-height:1.7;margin-bottom:14px}
.ta{font-family:var(--f-accent);font-size:10px;color:var(--crimson);letter-spacing:2px;font-weight:700;text-transform:uppercase}
.tstar{color:var(--gold);font-size:16px;margin-bottom:12px;letter-spacing:2px}
.ci{width:100%;height:44px;border:1px solid var(--silver);background:var(--white);color:var(--onyx);font-size:13px;padding:0 14px;outline:none;font-family:inherit}
.cr{background:var(--onyx);color:#fff;padding:28px;border:1px solid var(--onyx)}
.crl{font-family:var(--f-accent);font-size:10px;letter-spacing:2px;color:var(--vivid);margin-bottom:8px;font-weight:700}
.crv{font-family:var(--f-display);font-size:48px;color:#fff;font-weight:400;line-height:1.1}
.crb{border-top:1px solid rgba(255,255,255,0.12);margin-top:22px;padding-top:16px;font-size:13px;line-height:2.1}
.crb-row{display:flex;justify-content:space-between;color:rgba(255,255,255,0.65)}
.crb-row span:last-child{color:#fff;font-family:var(--f-accent);font-weight:500}
.crb-note{border-top:1px solid rgba(255,255,255,0.12);margin-top:16px;padding-top:14px;font-size:12px;color:rgba(255,255,255,0.6)}
.crb-note b{color:#fff}
.crb-jumbo{color:var(--gold);margin-top:8px;font-family:var(--f-accent);font-size:10px;letter-spacing:1.5px;text-transform:uppercase;font-weight:700;display:none}
.crb-jumbo.on{display:block}
.mpl{display:block;font-family:var(--f-accent);font-size:10px;letter-spacing:1.5px;text-transform:uppercase;color:var(--pewter);margin-bottom:6px;font-weight:600}

/* ============ FAQ / CONTACT / CTA ============ */
.fi{background:var(--white);border:1px solid var(--silver-light);margin-bottom:10px}
.fq{width:100%;background:none;border:none;text-align:left;padding:22px 24px;display:flex;align-items:center;justify-content:space-between;cursor:pointer;gap:16px}
.fq:hover{background:var(--parchment)}
.fqt{font-size:14px;font-weight:500;color:var(--onyx);line-height:1.4}
.fq.open .fqt{color:var(--crimson)}
.fch{width:24px;height:24px;border:1px solid var(--silver);display:flex;align-items:center;justify-content:center;font-size:11px;color:var(--pewter);background:var(--white)}
.fq.open .fch{background:var(--crimson);border-color:var(--crimson);color:#fff;transform:rotate(45deg)}
.fa{display:none;padding:0 24px 22px;font-size:13.5px;color:var(--graphite);line-height:1.85}
.fa.open{display:block}
.cf{display:flex;flex-direction:column;gap:10px}
.cin,.csel,.cta2{width:100%;height:44px;border:1px solid var(--silver);background:var(--white);padding:0 14px;font-size:13px;color:var(--onyx);outline:none;font-family:inherit}
.cta2{height:120px;padding:14px;resize:vertical}
.ctab{background:var(--onyx);padding:64px 40px;display:flex;align-items:center;justify-content:space-between;gap:32px;flex-wrap:wrap}
.ctab h2{color:#fff;font-family:var(--f-display);font-size:36px;font-weight:400;margin-bottom:8px}
.ctab p{color:rgba(255,255,255,0.7);font-size:14px}
.ctab-btns{display:flex;gap:12px;flex-wrap:wrap}
.ph{background:linear-gradient(135deg,var(--cream) 0%,var(--parchment) 60%,var(--stone) 100%);padding:88px 40px 72px;border-bottom:1px solid var(--silver-light)}
.ph h1{color:var(--onyx);font-family:var(--f-display);font-size:clamp(40px,5vw,64px);font-weight:300;max-width:680px;margin-bottom:18px;line-height:1.05;letter-spacing:-1px}
.ph h1 em{font-style:italic;color:var(--crimson);font-weight:400}
.phs{color:var(--pewter);font-size:16px;max-width:560px;line-height:1.75}

/* ============ VG ELITE ============ */
.eh{background:linear-gradient(135deg,var(--white) 0%,var(--vio-soft) 55%,#f0e9ff 100%);padding:100px 40px 84px;border-bottom:1px solid var(--silver-light)}
.eh .ey{color:var(--vio)}
.eh h1{color:var(--onyx);font-family:var(--f-display);font-size:clamp(48px,6vw,76px);font-weight:300;line-height:1.02;letter-spacing:-1px;max-width:680px;margin-bottom:24px}
.eh h1 em{font-style:italic;color:var(--vio);font-weight:400}
.eh .ehsub{color:var(--pewter);font-size:16px;max-width:560px;line-height:1.75;margin-bottom:36px}
.epillar{background:var(--white);border:1px solid var(--silver-light);border-top:3px solid var(--vio);padding:36px 32px}
.epillar-l{font-family:var(--f-accent);font-size:10px;letter-spacing:2.5px;text-transform:uppercase;color:var(--vio);margin-bottom:14px;font-weight:700}
.epillar-t{font-family:var(--f-display);font-size:26px;color:var(--onyx);margin-bottom:14px;font-weight:500}
.epillar-b{color:var(--pewter);font-size:13.5px;line-height:1.8;font-weight:300}
.evio-btn{background:var(--vio);color:#fff;padding:14px 28px;font-family:var(--f-accent);font-size:11px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;border:none;text-decoration:none;display:inline-block}
.evio-btn:hover{background:var(--vio2)}

/* ============ AI MATCH ============ */
.aiwrap{background:var(--onyx);padding:88px 40px;color:#fff}
.ai-box{max-width:840px;margin:0 auto;text-align:center}
.ai-input{width:100%;padding:26px;background:#1a1a1a;border:2px solid #2a2a2a;color:#fff;font-size:16px;font-family:inherit;outline:none;min-height:110px;resize:vertical}
.ai-input:focus{border-color:var(--vivid)}
.ai-examples{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin:22px 0}
.ai-ex{background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.14);color:rgba(255,255,255,.85);padding:9px 15px;font-size:12px;font-family:var(--f-accent)}
.ai-btn{background:var(--crimson);color:#fff;padding:16px 42px;font-family:var(--f-accent);font-size:12px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;border:none;margin-top:10px}

/* ============ JOURNAL / SOLD / NEWSLETTER / GOOGLE REVIEWS ============ */
.jrn-card{background:var(--white);border:1px solid var(--silver-light);overflow:hidden}
.jrn-thumb{height:180px;background:linear-gradient(135deg,var(--parchment),var(--stone));display:flex;align-items:center;justify-content:center;font-size:44px}
.jrn-thumb.crimson{background:linear-gradient(135deg,#a6192e,#d2203a);color:#fff}
.jrn-thumb.gold{background:linear-gradient(135deg,#b8952a,#d4a93a);color:#fff}
.jrn-thumb.violet{background:linear-gradient(135deg,#6d47d9,#8b60ff);color:#fff}
.jrn-body{padding:22px}
.jrn-cat{font-family:var(--f-accent);font-size:10px;letter-spacing:2px;color:var(--crimson);text-transform:uppercase;font-weight:700;margin-bottom:10px}
.jrn-title{font-family:var(--f-display);font-size:22px;font-weight:500;color:var(--onyx);line-height:1.25;margin-bottom:10px}
.jrn-excerpt{font-size:13px;color:var(--pewter);line-height:1.65;margin-bottom:14px}
.jrn-meta{font-family:var(--f-accent);font-size:10px;color:var(--silver);letter-spacing:1px;text-transform:uppercase;display:flex;gap:14px}
.sold-card{background:var(--white);border:1px solid var(--silver-light);padding:22px;position:relative}
.sold-card::before{content:'SOLD';position:absolute;top:12px;right:12px;background:#2a7a3b;color:#fff;font-family:var(--f-accent);font-size:9px;padding:4px 10px;letter-spacing:1.5px;font-weight:700}
.sold-price{font-family:var(--f-display);color:var(--crimson);font-size:26px;font-weight:500;margin-bottom:4px}
.sold-orig{font-size:11px;color:var(--pewter);text-decoration:line-through;margin-bottom:8px}
.sold-name{font-size:13.5px;font-weight:500;margin-bottom:4px}
.sold-addr{font-size:11px;color:var(--pewter);margin-bottom:12px}
.sold-stats{display:flex;gap:14px;flex-wrap:wrap;font-family:var(--f-accent);font-size:10px;color:var(--graphite);letter-spacing:.5px;font-weight:600;padding-top:12px;border-top:1px solid var(--silver-light)}
.nlb{background:var(--onyx);padding:56px 40px;color:#fff}
.nlb-inner{max-width:900px;margin:0 auto;text-align:center}
.nlb h2{font-family:var(--f-display);font-size:42px;font-weight:400;margin-bottom:14px}
.nlb h2 em{font-style:italic;color:var(--vivid)}
.nlb p{color:rgba(255,255,255,0.7);font-size:15px;line-height:1.7;margin-bottom:28px;max-width:580px;margin-left:auto;margin-right:auto}
.nlb-form{display:flex;gap:8px;max-width:520px;margin:0 auto;flex-wrap:wrap}
.nlb-form input{flex:1;min-width:220px;height:52px;background:rgba(255,255,255,0.06);border:1px solid rgba(255,255,255,0.14);color:#fff;padding:0 18px;font-family:inherit;font-size:14px;outline:none}
.nlb-form button{background:var(--crimson);color:#fff;padding:0 32px;height:52px;font-family:var(--f-accent);font-size:11px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;border:none}
.grev{background:var(--parchment);padding:56px 40px}
.grev-list{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;max-width:1240px;margin:0 auto}
.grev-card{background:var(--white);border:1px solid var(--silver-light);padding:22px}

/* ============ TOASTS / CHAT / MOBILE BAR / PALETTE PICKER ============ */
#toast-container{position:fixed;top:88px;right:20px;z-index:500;display:flex;flex-direction:column;gap:10px;pointer-events:none}
.toast{background:var(--white);border:1px solid var(--silver-light);border-left:4px solid var(--crimson);padding:14px 20px;box-shadow:0 8px 24px rgba(0,0,0,.1);min-width:280px;max-width:400px;pointer-events:all;animation:toastIn .3s ease-out;font-size:13.5px;color:var(--graphite);display:flex;align-items:flex-start;gap:12px}
.toast.success{border-left-color:#2a7a3b}
.toast-title{font-weight:600;color:var(--onyx);margin-bottom:2px;font-size:13px}
.toast-msg{font-size:12px;color:var(--pewter);line-height:1.5}
@keyframes toastIn{from{transform:translateX(120%);opacity:0}to{transform:translateX(0);opacity:1}}
#scta{display:none;position:fixed;left:0;right:0;bottom:0;z-index:150;background:var(--onyx);border-top:1px solid var(--graphite);padding:12px;gap:8px}
#scta a,#scta button{flex:1;padding:15px 8px;font-family:var(--f-accent);font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;border:none;text-align:center;display:flex;align-items:center;justify-content:center;gap:6px;text-decoration:none}
#scta .sc-call{background:#fff;color:var(--onyx)}
#scta .sc-book{background:var(--crimson);color:#fff}
@media(max-width:720px){#scta{display:flex}body{padding-bottom:72px}}
#xi{display:none;position:fixed;inset:0;background:rgba(0,0,0,.85);z-index:400;align-items:center;justify-content:center;padding:24px}
#xi.on{display:flex}
#xi .xic{background:var(--white);max-width:480px;width:100%;padding:48px 40px;position:relative;text-align:center}
#xi h3{font-family:var(--f-display);font-size:32px;font-weight:400;color:var(--onyx);margin-bottom:12px}
#xi h3 em{color:var(--crimson);font-style:italic}
#xi p{font-size:14px;color:var(--pewter);margin-bottom:24px;line-height:1.7}
#xi input{width:100%;padding:14px;border:1px solid var(--silver);font-size:13px;margin-bottom:10px;font-family:inherit;outline:none}
#xi button.xis{width:100%;background:var(--crimson);color:#fff;padding:16px;font-family:var(--f-accent);font-size:11px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;border:none;margin-top:4px}
#chat-toggle{position:fixed;bottom:24px;right:24px;width:62px;height:62px;background:var(--crimson);color:#fff;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:26px;box-shadow:0 6px 24px rgba(166,25,46,0.3);z-index:140;border:none}
#chat-panel{display:none;position:fixed;bottom:96px;right:24px;width:380px;max-width:calc(100vw - 48px);height:540px;max-height:calc(100vh - 140px);background:var(--white);border:1px solid var(--silver-light);z-index:140;flex-direction:column;box-shadow:0 12px 40px rgba(0,0,0,0.15)}
#chat-panel.on{display:flex}
.chat-hdr{background:var(--onyx);color:#fff;padding:16px 20px;display:flex;align-items:center;justify-content:space-between}
.chat-body{flex:1;overflow-y:auto;padding:20px;background:var(--cream);display:flex;flex-direction:column;gap:12px}
.chat-msg{max-width:82%;padding:11px 15px;font-size:13px;line-height:1.55}
.chat-msg.bot{background:var(--white);border:1px solid var(--silver-light);align-self:flex-start}
.chat-msg.user{background:var(--crimson);color:#fff;align-self:flex-end}
.chat-input-row{padding:14px 16px;border-top:1px solid var(--silver-light);background:var(--white);display:flex;gap:8px}
.chat-input{flex:1;padding:11px 13px;border:1px solid var(--silver-light);font-family:inherit;font-size:13px;outline:none}
.chat-send{background:var(--crimson);color:#fff;padding:0 18px;font-family:var(--f-accent);font-size:10px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;border:none}
#palette-picker{position:fixed;bottom:24px;left:24px;z-index:140;background:var(--white);border:1px solid var(--silver-light);box-shadow:0 6px 24px rgba(0,0,0,0.08);overflow:hidden}
#palette-picker.collapsed{height:44px;overflow:hidden}
.pp-header{background:var(--onyx);color:#fff;padding:11px 14px;font-family:var(--f-accent);font-size:9px;letter-spacing:2px;text-transform:uppercase;font-weight:700;display:flex;align-items:center;justify-content:space-between;gap:12px;cursor:pointer;min-width:180px}
.pp-body{padding:6px}
.pp-btn{display:flex;align-items:center;gap:10px;width:100%;padding:10px 12px;background:none;border:none;cursor:pointer;text-align:left;font-family:var(--f-accent);font-size:11px;letter-spacing:1px;color:var(--graphite);font-weight:600}
.pp-btn:hover{background:var(--cream)}
.pp-btn.active{background:var(--parchment);color:var(--crimson)}
.pp-swatch{display:inline-flex;gap:2px}
.pp-swatch span{width:14px;height:14px;border:1px solid rgba(0,0,0,0.08)}

/* ============ FOOTER ============ */
footer{background:var(--parchment);border-top:3px solid var(--crimson);padding:60px 40px 28px}
.fg{display:grid;grid-template-columns:2fr 1fr 1fr 1fr 1fr;gap:32px;margin-bottom:36px;max-width:1240px;margin-left:auto;margin-right:auto}
.flo{font-family:var(--f-display);color:var(--onyx);font-size:26px;font-weight:500;letter-spacing:2px;margin-bottom:14px;display:block}
.flo span{color:var(--crimson)}
footer h3{color:var(--crimson);font-family:var(--f-accent);font-size:10px;letter-spacing:2px;text-transform:uppercase;margin-bottom:16px;font-weight:700}
.flink{color:var(--graphite);font-size:12.5px;line-height:2.1;display:block;text-decoration:none}
.flink:hover{color:var(--crimson)}
.fp{color:var(--graphite);font-size:12.5px;line-height:2;margin-bottom:16px}
.fp a{color:var(--crimson)}
.fbar{border-top:1px solid var(--silver-light);padding-top:22px;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px;max-width:1240px;margin:0 auto}
.fcopy{color:var(--pewter);font-family:var(--f-accent);font-size:11px;letter-spacing:1.5px}
.soc{display:flex;gap:12px;margin-top:14px}
.soc a{width:32px;height:32px;border:1px solid var(--silver);border-radius:50%;display:flex;align-items:center;justify-content:center;color:var(--graphite);font-family:var(--f-accent);font-size:13px;font-weight:700;background:var(--white);text-decoration:none}

/* ============ RESPONSIVE ============ */
@media(max-width:900px){.g4{grid-template-columns:1fr 1fr}.fg{grid-template-columns:1fr 1fr}.grev-list{grid-template-columns:1fr 1fr}}
@media(max-width:640px){#nav{padding:0 20px}.nm,.nc{display:none}.sec,.idx,.vb,.ph,.ctab,.eh,.aiwrap,.spb,.grev,.nlb,.awb{padding-left:20px;padding-right:20px}footer{padding:36px 20px 20px}.g2,.g3,.g4{grid-template-columns:1fr}.grev-list{grid-template-columns:1fr}#chat-toggle{bottom:82px}#palette-picker{bottom:82px;left:12px}#toast-container{top:80px;right:12px;left:12px}}
```

---

## 4. STEP 3 — Global JavaScript

**Where it goes:** In the **Insert Headers and Footers** plugin, paste into "Scripts in Footer".

```html
<script>
/* ============ TOASTS ============ */
function showToast(title,msg,type){
  var c=document.getElementById('toast-container');
  if(!c){c=document.createElement('div');c.id='toast-container';document.body.appendChild(c)}
  var t=document.createElement('div');
  t.className='toast '+(type||'');
  t.innerHTML='<div class="toast-icon">'+(type==='success'?'✓':'ℹ')+'</div><div class="toast-body"><div class="toast-title">'+title+'</div><div class="toast-msg">'+msg+'</div></div><button class="toast-close" onclick="this.parentNode.remove()">×</button>';
  c.appendChild(t);
  setTimeout(function(){t.remove()},5000);
}

/* ============ CALENDLY / FORMS ============ */
function openCalendly(){
  // Production: Calendly.initPopupWidget({url:'https://calendly.com/YOUR-HANDLE/consultation'});
  showToast('Schedule a call','Configure Calendly URL in openCalendly() function.','');
  if(window.gtag)gtag('event','schedule_click',{page:location.pathname});
}
function submitForm(e,type){
  e.preventDefault();
  showToast('Request received','A specialist will follow up within one business day.','success');
  if(window.gtag)gtag('event',type+'_submit',{page:location.pathname});
  e.target.reset();
}
function toggleFAQ(btn){btn.classList.toggle('open');btn.nextElementSibling.classList.toggle('open')}

/* ============ MORTGAGE CALCULATOR ============ */
function mcalc(){
  var price=+document.getElementById('m-price').value;
  var dpPct=+document.getElementById('m-dp').value;
  var rate=+document.getElementById('m-rate').value/100/12;
  var term=+document.getElementById('m-term').value*12;
  var taxPct=+document.getElementById('m-tax').value/100;
  var ins=+document.getElementById('m-ins').value;
  var hoa=+document.getElementById('m-hoa').value;
  var loan=price*(1-dpPct/100);
  var pi=(rate===0)?loan/term:loan*(rate*Math.pow(1+rate,term))/(Math.pow(1+rate,term)-1);
  var tax=(price*taxPct)/12, insM=ins/12, pmi=(dpPct<20)?loan*0.005/12:0;
  var total=pi+tax+insM+hoa+pmi, totalInt=(pi*term)-loan, jumbo=loan>766550;
  var f=v=>'$'+Math.round(v).toLocaleString();
  document.getElementById('m-total').textContent=f(total);
  document.getElementById('m-pi').textContent=f(pi);
  document.getElementById('m-t').textContent=f(tax);
  document.getElementById('m-i').textContent=f(insM);
  document.getElementById('m-h').textContent=f(hoa);
  document.getElementById('m-p').textContent=pmi?f(pmi):'None';
  document.getElementById('m-la').textContent=f(loan);
  document.getElementById('m-ti').textContent=f(totalInt);
  document.getElementById('m-jumbo').classList.toggle('on',jumbo);
  if(window.gtag)gtag('event','mortgage_calc_used',{price:price});
}

/* ============ AFFORDABILITY ============ */
function acalc(){
  var inc=+document.getElementById('a-income').value;
  var debts=+document.getElementById('a-debts').value;
  var dp=+document.getElementById('a-dp').value;
  var rate=+document.getElementById('a-rate').value/100/12;
  var term=+document.getElementById('a-term').value*12;
  var maxMonthly=(inc/12)*0.28;
  var maxTotalDTI=(inc/12)*0.36;
  var avail=Math.min(maxMonthly,maxTotalDTI-debts);
  var maxPI=avail*0.70;
  var maxLoan=(rate===0)?maxPI*term:maxPI*(Math.pow(1+rate,term)-1)/(rate*Math.pow(1+rate,term));
  var maxPrice=maxLoan+dp;
  var f=v=>'$'+Math.round(v).toLocaleString();
  document.getElementById('a-max').textContent=f(maxPrice);
  document.getElementById('a-piti').textContent=f(avail);
  document.getElementById('a-loan').textContent=f(maxLoan);
  document.getElementById('a-dti').textContent=(((avail+debts)/(inc/12))*100).toFixed(1)+'%';
}

/* ============ RENT VS BUY ============ */
function rbcalc(){
  var price=+document.getElementById('rb-price').value;
  var rent=+document.getElementById('rb-rent').value;
  var dpPct=+document.getElementById('rb-dp').value;
  var app=+document.getElementById('rb-app').value/100;
  var rate=+document.getElementById('rb-rate').value/100/12;
  var loan=price*(1-dpPct/100), term=360;
  var pi=(rate===0)?loan/term:loan*(rate*Math.pow(1+rate,term))/(Math.pow(1+rate,term)-1);
  var buyM=pi+(price*0.0102/12)+(4800/12);
  var y5val=price*Math.pow(1+app,5), y5eq=y5val-loan-(price*dpPct/100);
  var be=0, bt=(price*dpPct/100), rt=0;
  for(var y=1;y<=30;y++){
    bt+=buyM*12-(price*Math.pow(1+app,y)-price*Math.pow(1+app,y-1));
    rt+=rent*12*Math.pow(1.03,y-1);
    if(rt>=bt){be=y;break}
  }
  var f=v=>'$'+Math.round(v).toLocaleString();
  document.getElementById('rb-years').textContent=(be?be+' YRS':'30+ YRS');
  document.getElementById('rb-buy').textContent=f(buyM);
  document.getElementById('rb-rentM').textContent=f(rent);
  document.getElementById('rb-equity').textContent=f(y5eq);
  document.getElementById('rb-val').textContent=f(y5val);
}

/* ============ CLOSING COSTS ============ */
function cccalc(){
  var price=+document.getElementById('cc-price').value;
  var dpPct=+document.getElementById('cc-dp').value;
  var role=document.getElementById('cc-role').value;
  var loan=price*(1-dpPct/100);
  var ds=(role==='seller')?(price*0.007):0;
  var dm=(role==='buyer')?(loan*0.0035):0;
  var intTax=(role==='buyer')?(loan*0.002):0;
  var ti=(role==='buyer')?(price*0.00525):0;
  var lf=(role==='buyer')?(loan*0.01):0;
  var misc=(role==='buyer')?750:500;
  var total=ds+dm+intTax+ti+lf+misc;
  var f=v=>'$'+Math.round(v).toLocaleString();
  document.getElementById('cc-total').textContent=f(total);
  document.getElementById('cc-ds').textContent=ds?f(ds):'—';
  document.getElementById('cc-dm').textContent=dm?f(dm):'—';
  document.getElementById('cc-int').textContent=intTax?f(intTax):'—';
  document.getElementById('cc-ti').textContent=ti?f(ti):'—';
  document.getElementById('cc-lf').textContent=lf?f(lf):'—';
  document.getElementById('cc-misc').textContent=f(misc);
}

/* ============ AI PROPERTY MATCH ============ */
function setAI(text){document.getElementById('ai-query').value=text}
function runAIMatch(){
  var q=document.getElementById('ai-query').value.trim();
  if(!q)return;
  var res=document.getElementById('ai-results');
  res.innerHTML='<div style="text-align:center;padding:44px;color:rgba(255,255,255,0.6)">✨ Analyzing...</div>';
  setTimeout(function(){
    var props=[
      {score:96,p:'$4,850,000',t:'Bal Harbour Waterfront Estate · 4BD · 5BA · 4,200 SF',r:'Waterfront ✓ · Dock ✓ · Under $5M ✓'},
      {score:88,p:'$3,950,000',t:'Aventura Yacht Home · 4BD · 4BA · 3,800 SF',r:'Waterfront ✓ · Aventura ✓ · Dock ✓'},
      {score:82,p:'$4,500,000',t:'Miami Beach Bayfront · 4BD · 5BA · 4,000 SF',r:'Waterfront ✓ · Pool ✓'}
    ];
    res.innerHTML='<div style="margin-bottom:18px;color:rgba(255,255,255,0.6);font-size:13px">Found <b style="color:#fff">'+props.length+'</b> matches</div>'+
      props.map(function(m){return '<div style="background:#1a1a1a;border:1px solid #2a2a2a;padding:26px;margin-bottom:12px;display:grid;grid-template-columns:1fr auto;gap:22px;align-items:center"><div><div style="font-family:var(--f-display);color:var(--vivid);font-size:24px">'+m.p+'</div><div style="color:#fff;font-size:13.5px;margin:6px 0">'+m.t+'</div><div style="color:rgba(255,255,255,0.6);font-size:12px;font-style:italic">'+m.r+'</div></div><div style="background:var(--crimson);color:#fff;width:60px;height:60px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:var(--f-display);font-size:24px;font-weight:600">'+m.score+'</div></div>'}).join('')+
      '<div style="text-align:center;margin-top:28px"><button class="ai-btn" onclick="openCalendly()">📅 Discuss With an Advisor</button></div>';
    if(window.gtag)gtag('event','ai_match_completed',{query:q});
  },1200);
}

/* ============ AI CONCIERGE CHAT ============ */
function toggleChat(){document.getElementById('chat-panel').classList.toggle('on')}
function chatSend(txt){
  var input=document.getElementById('chat-input');
  var msg=txt||input.value.trim();
  if(!msg)return;
  var body=document.getElementById('chat-body');
  body.innerHTML+='<div class="chat-msg user">'+msg+'</div>';
  input.value=''; body.scrollTop=body.scrollHeight;
  setTimeout(function(){
    var m=msg.toLowerCase(), r;
    if(m.includes('elite'))r='VG Elite is our private Sports & Entertainment division. <a onclick="toggleChat();location.href=\'/elite\'">Learn more</a> or <a onclick="openCalendly()">request access</a>.';
    else if(m.includes('schedule')||m.includes('call'))r='I can book you a consultation. <a onclick="openCalendly()">See available times</a>.';
    else if(m.includes('sell')||m.includes('valuation'))r='Complimentary valuations within 24 hours. <a href="/valuation">Start here</a>.';
    else if(m.includes('buy')||m.includes('waterfront'))r='Try our <a href="/ai-match">AI Matchmaker</a> or <a href="/properties">browse listings</a>.';
    else if(m.includes('hoa'))r='Our HOA Division handles advisory, receivership, and conversions. <a onclick="openCalendly()">Book consultation</a>.';
    else r='Thanks! An advisor will reply within one business day. <a onclick="openCalendly()">Schedule a call</a>.';
    body.innerHTML+='<div class="chat-msg bot">'+r+'</div>';
    body.scrollTop=body.scrollHeight;
  },600);
}

/* ============ EXIT INTENT ============ */
function closeXI(){document.getElementById('xi').classList.remove('on')}
(function(){
  if(localStorage.getItem('xi_shown'))return;
  var fired=false;
  document.addEventListener('mouseout',function(e){
    if(fired||e.clientY>0||e.relatedTarget)return;
    fired=true;setTimeout(function(){document.getElementById('xi').classList.add('on')},200);
  });
})();

/* ============ PALETTE PICKER ============ */
function setPalette(name,ev){
  document.body.classList.remove('palette-lighter');
  if(name==='lighter')document.body.classList.add('palette-lighter');
  try{localStorage.setItem('vg_palette',name)}catch(e){}
  document.querySelectorAll('#palette-picker .pp-btn').forEach(function(b){b.classList.toggle('active',b.dataset.palette===name)});
  if(ev)showToast(name.charAt(0).toUpperCase()+name.slice(1)+' palette applied','Your preference will persist.','success');
}
function togglePalettePicker(){document.getElementById('palette-picker').classList.toggle('collapsed')}
(function(){try{var s=localStorage.getItem('vg_palette');if(s==='lighter'){document.body.classList.add('palette-lighter');document.querySelectorAll('#palette-picker .pp-btn').forEach(function(b){b.classList.toggle('active',b.dataset.palette===s)})}}catch(e){}})();
</script>
```

---

## 5. STEP 4 — Header template

**Where it goes:** `Appearance → Site Editor → Templates → Header` → replace with a Custom HTML block containing:

```html
<nav id="nav">
  <a class="nl" href="/">VARICK <span>GLOBAL</span></a>
  <ul class="nm">
    <li class="ni"><span class="nb">Buy <span class="nch">▾</span></span>
      <div class="nd">
        <div class="dgl">Buying</div>
        <a class="dl" href="/properties">Search Properties</a>
        <a class="dl" href="/ai-match">✨ AI Property Matchmaker</a>
        <a class="dl" href="/new-developments">New Developments</a>
        <a class="dl" href="/foreclosures">Foreclosures &amp; Distressed</a>
        <a class="dl" href="/neighborhoods">Neighborhoods</a>
        <a class="dl" href="/buyers-guide">Buyer's Guide</a>
      </div>
    </li>
    <li class="ni"><span class="nb">Sell <span class="nch">▾</span></span>
      <div class="nd">
        <div class="dgl">Selling</div>
        <a class="dl" href="/valuation">Free Valuation</a>
        <a class="dl" href="/sellers-guide">Seller's Guide</a>
        <a class="dl" href="/sold">Recently Sold</a>
        <a class="dl" href="/contact">Sell With Us</a>
      </div>
    </li>
    <li class="ni"><span class="nb">Tools <span class="nch">▾</span></span>
      <div class="nd">
        <div class="dgl">Calculators</div>
        <a class="dl" href="/tools/mortgage">Mortgage Calculator</a>
        <a class="dl" href="/tools/affordability">Affordability</a>
        <a class="dl" href="/tools/rent-vs-buy">Rent vs. Buy</a>
        <a class="dl" href="/tools/closing-costs">Closing Costs</a>
        <a class="dl" href="/ai-match">AI Property Match</a>
      </div>
    </li>
    <li class="ni"><a class="nb" href="/elite" style="color:var(--vio)">VG Elite</a></li>
    <li class="ni"><span class="nb">Journal <span class="nch">▾</span></span>
      <div class="nd">
        <div class="dgl">Insights</div>
        <a class="dl" href="/journal">All Articles</a>
        <a class="dl" href="/journal/market-reports">Market Reports</a>
        <a class="dl" href="/journal/neighborhoods">Neighborhood Guides</a>
        <a class="dl" href="/journal/education">Buyer / Seller Education</a>
      </div>
    </li>
    <li class="ni"><span class="nb">About <span class="nch">▾</span></span>
      <div class="nd">
        <div class="dgl">About</div>
        <a class="dl" href="/about">Our Story</a>
        <a class="dl" href="/team">Meet the Team</a>
        <a class="dl" href="/careers">Careers</a>
        <a class="dl" href="/press">Press &amp; Media</a>
        <a class="dl" href="/faq">FAQ</a>
        <a class="dl" href="/contact">Contact</a>
      </div>
    </li>
  </ul>
  <button class="nc" onclick="openCalendly()">Schedule Consultation</button>
</nav>
```

---

## 6. STEP 5 — Footer template

**Where it goes:** `Appearance → Site Editor → Templates → Footer` → replace with a Custom HTML block containing:

```html
<footer>
  <div class="fg">
    <div>
      <a class="flo" href="/">VARICK <span>GLOBAL</span></a>
      <div style="font-family:var(--f-accent);font-size:9px;letter-spacing:3px;color:var(--pewter);margin-bottom:16px;font-weight:600">REAL ESTATE ADVISORS</div>
      <div class="fp">19505 Biscayne Blvd, Suite 2350<br>Aventura, FL 33180<br><br>📞 <a href="tel:+17863527547">786.352.7547</a><br>✉ <a href="mailto:info@varickglobal.com">info@varickglobal.com</a></div>
      <div class="soc">
        <a href="https://www.facebook.com/VarickGlobal/" target="_blank">f</a>
        <a href="https://x.com/varickglobal" target="_blank">𝕏</a>
        <a href="https://www.linkedin.com/company/varickglobal/" target="_blank">in</a>
        <a href="https://www.instagram.com/varickglobal" target="_blank">◉</a>
        <a href="https://www.youtube.com/@VarickGlobal" target="_blank">▶</a>
      </div>
    </div>
    <div>
      <h3>Services</h3>
      <a class="flink" href="/residential">Residential</a>
      <a class="flink" href="/commercial">Commercial</a>
      <a class="flink" href="/leasing">Leasing</a>
      <a class="flink" href="/land">Land</a>
      <a class="flink" href="/valuation">Valuation</a>
    </div>
    <div>
      <h3>HOA Division</h3>
      <a class="flink" href="/hoa">HOA Advisory</a>
      <a class="flink" href="/hoa/conversions">Conversions</a>
      <a class="flink" href="/hoa/receivership">Receivership</a>
      <a class="flink" href="/hoa/distressed">Distressed HOA</a>
    </div>
    <div>
      <h3>VG Elite</h3>
      <a class="flink" href="/elite/athletes">Athletes</a>
      <a class="flink" href="/elite/entertainment">Entertainment</a>
      <a class="flink" href="/elite/concierge">Concierge</a>
      <a class="flink" href="/elite">Request Access</a>
    </div>
    <div>
      <h3>Tools</h3>
      <a class="flink" href="/ai-match">AI Search</a>
      <a class="flink" href="/tools/mortgage">Mortgage Calc</a>
      <a class="flink" href="/journal">Journal</a>
      <a class="flink" href="/sitemap">Sitemap</a>
      <a class="flink" href="/faq">FAQ</a>
      <a class="flink" href="/contact">Contact</a>
    </div>
  </div>
  <div class="fbar">
    <div class="fcopy">© 2026 VARICK GLOBAL REAL ESTATE ADVISORS · ALL RIGHTS RESERVED</div>
    <div style="display:flex;gap:16px">
      <a class="flink" href="/privacy">Privacy</a>
      <a class="flink" href="/terms">Terms</a>
      <a class="flink" href="/fair-housing">Fair Housing</a>
    </div>
  </div>
</footer>

<!-- Sticky mobile CTA bar -->
<div id="scta">
  <a class="sc-call" href="tel:+17863527547">📞 Call</a>
  <button class="sc-book" onclick="openCalendly()">📅 Schedule</button>
</div>

<!-- Exit intent modal -->
<div id="xi">
  <div class="xic">
    <button style="position:absolute;top:16px;right:20px;font-size:28px;background:none;border:none;color:var(--pewter)" onclick="closeXI()">×</button>
    <h3>Before you go — <em>first look</em></h3>
    <p>Join our exclusive list to see new South Florida luxury listings 48 hours before they hit the market.</p>
    <form onsubmit="event.preventDefault();localStorage.setItem('xi_shown','1');closeXI();showToast('Welcome to the list','You will see new listings 48 hours early.','success')">
      <input type="email" placeholder="Email address" required>
      <input type="text" placeholder="ZIP code you're interested in">
      <button class="xis" type="submit">Get Early Access</button>
    </form>
  </div>
</div>

<!-- AI Concierge chat -->
<button id="chat-toggle" onclick="toggleChat()">💬</button>
<div id="chat-panel">
  <div class="chat-hdr">
    <div>
      <div style="font-family:var(--f-display);font-size:18px;font-weight:500">Varick Concierge</div>
      <div style="font-family:var(--f-accent);font-size:9px;letter-spacing:1.5px;color:var(--gold);font-weight:600">AI ASSISTANT · ONLINE</div>
    </div>
    <button style="background:none;border:none;color:#fff;font-size:24px" onclick="toggleChat()">×</button>
  </div>
  <div class="chat-body" id="chat-body">
    <div class="chat-msg bot">Hi! I'm the Varick Global AI concierge. How can I help — buying, selling, HOA services, or scheduling a call?</div>
  </div>
  <div class="chat-input-row">
    <input class="chat-input" id="chat-input" placeholder="Type your question..." onkeypress="if(event.key==='Enter')chatSend()">
    <button class="chat-send" onclick="chatSend()">Send</button>
  </div>
</div>

<!-- Palette picker -->
<div id="palette-picker">
  <div class="pp-header" onclick="togglePalettePicker()">
    <span>◆ Preview Palette</span>
    <span>▾</span>
  </div>
  <div class="pp-body">
    <button class="pp-btn active" data-palette="refined" onclick="setPalette('refined',event)">
      <span class="pp-swatch"><span style="background:#a6192e"></span><span style="background:#f5f2ed"></span><span style="background:#efeae1"></span><span style="background:#e5dfd1"></span></span>
      <span>Refined</span>
    </button>
    <button class="pp-btn" data-palette="lighter" onclick="setPalette('lighter',event)">
      <span class="pp-swatch"><span style="background:#b32338"></span><span style="background:#faf8f4"></span><span style="background:#f4ede4"></span><span style="background:#ece0d8"></span></span>
      <span>Lighter</span>
    </button>
  </div>
</div>

<div id="toast-container"></div>
```

---

## 7. STEP 6 — Home page HTML

**Where it goes:** Create a new WordPress page titled "Home" (set as static home in `Settings → Reading`). Add a Custom HTML block and paste:

```html
<!-- VIDEO HERO -->
<section class="vhero">
  <div class="vposter">VG</div>
  <!-- To use real video: <video autoplay muted loop playsinline poster="/hero-poster.jpg"><source src="/hero.mp4" type="video/mp4"></video> -->
  <div class="voverlay"></div>
  <div class="vinner">
    <div class="vey">South Florida · Luxury Real Estate</div>
    <h1>Where <em>Luxury</em><br>Meets Precision</h1>
    <p class="vsub">Discreet. Precise. Unwavering. Varick Global Real Estate Advisors — trusted by South Florida's most discerning clientele since 2016.</p>
    <div class="vctas">
      <button class="vcta-p" onclick="openCalendly()">Schedule a Private Consultation</button>
      <a class="vcta-g" href="#featured">Explore Portfolio</a>
    </div>
    <div class="vtrust">
      <span>★★★★★ · 4.9 Rating</span>
      <span>◆ 500+ Transactions</span>
      <span>◆ Since 2016</span>
    </div>
  </div>
</section>

<!-- SOCIAL PROOF -->
<div class="spb">
  <div class="spb-row">
    <div><div class="spb-v">$1.2B+</div><div class="spb-l">Closed Volume</div></div>
    <div><div class="spb-v">500+</div><div class="spb-l">Transactions</div></div>
    <div><div class="spb-v">4.9 ★</div><div class="spb-l">127 Reviews</div></div>
    <div><div class="spb-v">24hr</div><div class="spb-l">Response Time</div></div>
    <div><div class="spb-v">EN · ES</div><div class="spb-l">Bilingual Service</div></div>
  </div>
</div>

<!-- AWARDS -->
<div class="awb">
  <div class="awb-ttl">Recognitions · Memberships · Affiliations</div>
  <div class="awb-row">
    <div class="awb-item">Miami Association of REALTORS®</div>
    <div class="awb-item">Luxury Portfolio International</div>
    <div class="awb-item">Who's Who in Luxury Real Estate</div>
    <div class="awb-item">FL Realtors Circle of Excellence</div>
    <div class="awb-item">Global Luxury Certified</div>
  </div>
</div>

<!-- IDX SEARCH (replace with your IDX plugin shortcode) -->
<div class="idx">
  <div class="idxl">🔍 Search Live MLS Listings — South Florida</div>
  <div class="idxr">
    <select><option>Buy</option><option>Rent</option><option>Commercial</option></select>
    <input type="text" placeholder="City, Zip, or Neighborhood">
    <select><option>Any Price</option><option>Under $1M</option><option>$1M–$3M</option><option>$3M–$5M</option><option>$5M+</option></select>
    <select><option>Beds</option><option>1+</option><option>2+</option><option>3+</option><option>4+</option><option>5+</option></select>
    <select><option>Property Type</option><option>Condo</option><option>Single Family</option><option>Townhouse</option><option>Waterfront</option></select>
    <button onclick="location.href='/properties'">Search</button>
  </div>
</div>

<!-- FEATURED PROPERTIES -->
<section class="sec" id="featured" style="background:var(--white)">
  <div class="ctr">
    <div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:32px;flex-wrap:wrap;gap:14px">
      <div>
        <span class="ey">Featured Portfolio</span>
        <h2 style="font-family:var(--f-display);font-size:40px;font-weight:400">Properties across <em style="color:var(--crimson);font-style:italic">South Florida</em></h2>
      </div>
      <a class="bo" href="/properties">View All Listings →</a>
    </div>
    <div class="g3">
      <a class="pc" href="/properties">
        <div class="pi">🏖️<div class="pb2">Exclusive</div></div>
        <div class="pb"><div class="pp">$4,850,000</div><div class="pn">Waterfront Estate</div><div class="pa">Bal Harbour · 33154</div><div class="pm"><span>4 BD</span>·<span>5 BA</span>·<span>4,200 SF</span></div></div>
      </a>
      <a class="pc" href="/properties">
        <div class="pi">🌊<div class="pb2 gold">Waterfront</div></div>
        <div class="pb"><div class="pp">$7,200,000</div><div class="pn">Ocean-View Penthouse</div><div class="pa">Miami Beach · 33139</div><div class="pm"><span>5 BD</span>·<span>6 BA</span>·<span>6,100 SF</span></div></div>
      </a>
      <a class="pc" href="/properties">
        <div class="pi">🏙️<div class="pb2">New</div></div>
        <div class="pb"><div class="pp">$3,150,000</div><div class="pn">Brickell Sky Residence</div><div class="pa">Brickell · 33131</div><div class="pm"><span>3 BD</span>·<span>4 BA</span>·<span>3,400 SF</span></div></div>
      </a>
    </div>
  </div>
</section>

<!-- SERVICES GRID -->
<section class="sec" style="background:var(--parchment)">
  <div class="ctr">
    <span class="ey">Full-Spectrum Services</span>
    <h2 style="font-family:var(--f-display);font-size:40px;font-weight:400;margin-bottom:32px">Every discipline. <em style="color:var(--crimson);font-style:italic">One firm.</em></h2>
    <div class="g4">
      <a class="st" href="/residential"><div class="si">🏠</div><div class="stt">Residential Sales</div><div class="sd">Luxury single-family, condos, waterfront estates.</div></a>
      <a class="st" href="/commercial"><div class="si">🏢</div><div class="stt">Commercial</div><div class="sd">Office, retail, industrial, multi-family.</div></a>
      <a class="st" href="/leasing"><div class="si">📄</div><div class="stt">Leasing</div><div class="sd">Tenant and landlord representation.</div></a>
      <a class="st" href="/land"><div class="si">🌍</div><div class="stt">Land</div><div class="sd">Development sites and waterfront lots.</div></a>
      <a class="st" href="/investment"><div class="si">📊</div><div class="stt">Investment Sales</div><div class="sd">Portfolio building, 1031 exchanges.</div></a>
      <a class="st" href="/hoa"><div class="si">👥</div><div class="stt">HOA Advisory</div><div class="sd">Distressed HOA, receivership.</div></a>
      <a class="st" href="/valuation"><div class="si">💎</div><div class="stt">Free Valuation</div><div class="sd">Complimentary CMAs within 24 hours.</div></a>
      <a class="st" href="/elite" style="border-color:rgba(109,71,217,.2)"><div class="si">✦</div><div class="stt" style="color:var(--vio)">VG Elite</div><div class="sd">Sports & entertainment · by invitation only.</div></a>
    </div>
  </div>
</section>

<!-- ADVISORS -->
<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:32px;flex-wrap:wrap;gap:14px">
      <div><span class="ey">The Team</span><h2 style="font-family:var(--f-display);font-size:40px;font-weight:400">Meet the <em style="color:var(--crimson);font-style:italic">advisors</em></h2></div>
      <a class="bo" href="/team">All Advisors →</a>
    </div>
    <div class="g4">
      <div class="ac"><div class="av">👤</div><div class="ab"><div class="an">Chris Gallego</div><div class="at">Founder & CEO</div><div class="abio">15+ years South Florida luxury real estate.</div><div class="acta"><a class="br" href="tel:+17863527547">Call</a><button class="bo" onclick="openCalendly()">Book</button></div></div></div>
      <div class="ac"><div class="av">👤</div><div class="ab"><div class="an">Alfredo Morejon</div><div class="at">Senior Advisor</div><div class="abio">Waterfront specialist. Miami Beach + Brickell.</div><div class="acta"><a class="br" href="tel:+17863527547">Call</a><button class="bo" onclick="openCalendly()">Book</button></div></div></div>
      <div class="ac"><div class="av">👤</div><div class="ab"><div class="an">Nina Vazquez</div><div class="at">Commercial Advisor</div><div class="abio">Commercial + investment sales.</div><div class="acta"><a class="br" href="tel:+17863527547">Call</a><button class="bo" onclick="openCalendly()">Book</button></div></div></div>
      <div class="ac"><div class="av">👤</div><div class="ab"><div class="an">Gloria Grullon</div><div class="at">HOA Division Head</div><div class="abio">Distressed HOA · receivership. Bilingual EN/ES.</div><div class="acta"><a class="br" href="tel:+17863527547">Call</a><button class="bo" onclick="openCalendly()">Book</button></div></div></div>
    </div>
  </div>
</section>

<!-- VALUATION CTA (or replace form with Fluent Forms shortcode) -->
<div class="vb">
  <div class="ctr" style="display:grid;grid-template-columns:1fr 1fr;gap:48px;align-items:center">
    <div>
      <span class="ey">Free Valuation</span>
      <h2 style="font-family:var(--f-display);font-size:40px;font-weight:400;margin-bottom:14px">What is your property <em style="color:var(--crimson);font-style:italic">worth?</em></h2>
      <p style="font-size:14.5px;color:var(--graphite);line-height:1.8;margin-bottom:20px">Get a no-obligation market analysis from our South Florida specialists — delivered within 24 hours.</p>
      <div class="hi">Typical response &lt; 24 hours · No obligation · No cost</div>
    </div>
    <form class="vf" onsubmit="submitForm(event,'valuation')">
      <input class="vi" type="text" placeholder="Property address" required>
      <input class="vi" type="email" placeholder="Email address" required>
      <input class="vi" type="tel" placeholder="Phone number">
      <button type="submit" class="br">Get My Free Valuation →</button>
    </form>
  </div>
</div>

<!-- TESTIMONIALS -->
<section class="sec" style="background:var(--parchment)">
  <div class="ctr">
    <span class="ey">Client Voices</span>
    <h2 style="font-family:var(--f-display);font-size:40px;font-weight:400;margin-bottom:32px">What clients <em style="color:var(--crimson);font-style:italic">say</em></h2>
    <div class="g3">
      <div class="tc"><div class="tstar">★★★★★</div><div class="tq">"Chris and the Varick Global team found us our dream waterfront home in Bal Harbour. Their discretion and market knowledge is unmatched."</div><div class="ta">— M.R. · Bal Harbour Buyer</div></div>
      <div class="tc"><div class="tstar">★★★★★</div><div class="tq">"We sold our Brickell condo for $200K above asking in 11 days. The marketing strategy was incredible."</div><div class="ta">— J.T. · Brickell Seller</div></div>
      <div class="tc"><div class="tstar">★★★★★</div><div class="tq">"The HOA advisory service saved our building. Gloria navigated a receivership process we could not have managed alone."</div><div class="ta">— HOA Board President · Aventura</div></div>
    </div>
  </div>
</section>

<!-- NEWSLETTER -->
<div class="nlb">
  <div class="nlb-inner">
    <div style="font-family:var(--f-accent);font-size:10px;letter-spacing:3px;color:var(--gold);text-transform:uppercase;font-weight:700;margin-bottom:14px">◆ Exclusive Access</div>
    <h2>Off-market listings, <em>48 hours early</em></h2>
    <p>Join our exclusive list to see new South Florida luxury listings 48 hours before they hit the MLS.</p>
    <form class="nlb-form" onsubmit="event.preventDefault();showToast('Welcome to the list','You will see listings 48 hours early.','success');this.reset()">
      <input type="email" placeholder="Email address" required>
      <input type="text" placeholder="ZIP code">
      <button type="submit">Subscribe →</button>
    </form>
  </div>
</div>

<!-- FINAL CTA -->
<div class="ctab">
  <div>
    <h2>Ready to make a move?</h2>
    <p>Schedule a private consultation with a Varick Global advisor.</p>
  </div>
  <div class="ctab-btns">
    <button class="br" onclick="openCalendly()">Schedule Consultation</button>
    <a class="bo" style="color:#fff;border-color:#fff" href="/contact">Message Us</a>
  </div>
</div>
```

---

## 8. STEP 7 — VG Elite page HTML

**Page:** Create WordPress page "VG Elite" with slug `elite`. Add a Custom HTML block:

```html
<div class="eh">
  <span class="ey">VG Elite · Sports & Entertainment Division</span>
  <h1>Exclusive Access.<br><em>Extraordinary Living.</em></h1>
  <p class="ehsub">A private division of Varick Global dedicated to professional athletes, entertainers, executives, and ultra-high-net-worth individuals. Discretion guaranteed.</p>
  <div style="margin-top:36px;display:flex;gap:12px;flex-wrap:wrap">
    <a class="evio-btn" href="#elite-form">Request Private Access →</a>
    <button class="bo" onclick="openCalendly()">Schedule Consultation</button>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <span class="ey" style="color:var(--vio)">Service Pillars</span>
    <h2 style="font-family:var(--f-display);font-size:40px;font-weight:400;margin-bottom:32px">Curated for the <em style="color:var(--vio);font-style:italic">exceptional</em></h2>
    <div class="g3">
      <div class="epillar">
        <div class="epillar-l">Athlete Services</div>
        <div class="epillar-t">Private Acquisition</div>
        <div class="epillar-b">Off-market estate hunting, multi-market portfolios, post-trade transaction management, relocation concierge, seasonal luxury rentals.</div>
      </div>
      <div class="epillar">
        <div class="epillar-l">Entertainment Services</div>
        <div class="epillar-t">Celebrity Estates</div>
        <div class="epillar-b">Ultra-discreet acquisition and disposition. NDA-protected transactions, media blackout coordination, personal security consultation.</div>
      </div>
      <div class="epillar">
        <div class="epillar-l">Investment Division</div>
        <div class="epillar-t">Portfolio Building</div>
        <div class="epillar-b">Luxury short-term rental strategy, multi-family acquisition, commercial mixed-use, athlete-owned portfolio management.</div>
      </div>
    </div>
  </div>
</section>

<section class="sec" id="elite-form" style="background:var(--parchment)">
  <div class="ctr" style="max-width:680px">
    <div style="background:var(--white);padding:44px 40px;border:1px solid var(--silver-light);border-top:3px solid var(--vio)">
      <span class="ey" style="color:var(--vio)">Request Private Access</span>
      <div style="font-family:var(--f-display);font-size:30px;color:var(--onyx);margin-bottom:10px;font-weight:500">Apply for VG Elite membership</div>
      <p style="color:var(--pewter);font-size:13.5px;margin-bottom:28px">Access is by invitation or referral. Please share your details and a member of our Elite team will respond within one business day, under NDA.</p>
      <form class="cf" onsubmit="submitForm(event,'elite')">
        <input class="cin" type="text" placeholder="Full name" required>
        <input class="cin" type="email" placeholder="Confidential email" required>
        <input class="cin" type="tel" placeholder="Direct phone">
        <select class="cin"><option>Affiliation…</option><option>Professional Athlete</option><option>Entertainment / Media</option><option>Executive / C-Suite</option><option>Referred by Current Member</option><option>Other UHNW</option></select>
        <input class="cin" type="text" placeholder="Referrer name (if applicable)">
        <textarea class="cta2" placeholder="Brief context — what you're looking to accomplish"></textarea>
        <button type="submit" class="evio-btn" style="width:100%;padding:16px">Submit Request Under NDA →</button>
      </form>
    </div>
  </div>
</section>
```

---

## 9. STEP 8 — AI Property Match page HTML

**Page:** Create WordPress page "AI Property Match" with slug `ai-match`. Add a Custom HTML block:

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">AI Property Matchmaker</span>
    <h1>Describe your dream property.<br>Let <em>AI</em> find it.</h1>
    <p class="phs" style="margin-top:14px">Our AI matcher understands natural language and cross-references live South Florida MLS listings to return ranked matches with compatibility scores.</p>
  </div>
</div>

<section class="aiwrap">
  <div class="ai-box">
    <div style="font-family:var(--f-display);font-size:26px;margin-bottom:22px">What are you looking for?</div>
    <textarea class="ai-input" id="ai-query" placeholder="Example: 3-bedroom waterfront home in Aventura under $5M with a dock and pool..."></textarea>
    <div class="ai-examples">
      <span class="ai-ex" onclick="setAI('3-bedroom waterfront home in Aventura under $5M with a dock')">🏖️ Waterfront Aventura</span>
      <span class="ai-ex" onclick="setAI('Modern condo in Brickell with ocean view')">🏙️ Brickell luxury condo</span>
      <span class="ai-ex" onclick="setAI('Investment property Miami Beach')">📊 Miami Beach investment</span>
      <span class="ai-ex" onclick="setAI('Private estate Palm Beach 5+ bedrooms')">✦ Palm Beach estate</span>
    </div>
    <button class="ai-btn" onclick="runAIMatch()">✨ Find My Matches</button>
    <div id="ai-results" style="margin-top:44px;text-align:left"></div>
  </div>
</section>
```

---

## 10. STEP 9 — Four calculator pages

### 10.1 Mortgage Calculator

**Page slug:** `/tools/mortgage`

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Tools · Florida-Specific</span>
    <h1>Mortgage <em>Calculator</em></h1>
    <p class="phs" style="margin-top:14px">Estimate your total monthly payment including taxes, insurance, HOA, and PMI. Jumbo loan detection built in.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g2" style="align-items:stretch;gap:28px">
      <div>
        <div style="display:flex;flex-direction:column;gap:14px">
          <div><div class="mpl">Property Price</div><input class="ci" id="m-price" type="number" value="2500000" oninput="mcalc()"></div>
          <div class="g2" style="gap:14px">
            <div><div class="mpl">Down Payment (%)</div><input class="ci" id="m-dp" type="number" value="25" oninput="mcalc()"></div>
            <div><div class="mpl">Rate (%)</div><input class="ci" id="m-rate" type="number" step="0.01" value="6.75" oninput="mcalc()"></div>
          </div>
          <div class="g2" style="gap:14px">
            <div><div class="mpl">Term</div><select class="ci" id="m-term" onchange="mcalc()"><option value="30">30 years</option><option value="20">20 years</option><option value="15">15 years</option></select></div>
            <div><div class="mpl">County Tax</div><select class="ci" id="m-tax" onchange="mcalc()"><option value="1.02">Miami-Dade (1.02%)</option><option value="1.09">Broward (1.09%)</option><option value="1.03">Palm Beach (1.03%)</option></select></div>
          </div>
          <div class="g2" style="gap:14px">
            <div><div class="mpl">Insurance/yr</div><input class="ci" id="m-ins" type="number" value="4800" oninput="mcalc()"></div>
            <div><div class="mpl">HOA/mo</div><input class="ci" id="m-hoa" type="number" value="0" oninput="mcalc()"></div>
          </div>
          <button class="br" onclick="mcalc()">Recalculate</button>
        </div>
      </div>
      <div class="cr">
        <div class="crl">TOTAL MONTHLY (PITI + HOA)</div>
        <div class="crv" id="m-total">$—</div>
        <div class="crb">
          <div class="crb-row"><span>Principal + Interest</span><span id="m-pi">—</span></div>
          <div class="crb-row"><span>Property Tax</span><span id="m-t">—</span></div>
          <div class="crb-row"><span>Insurance</span><span id="m-i">—</span></div>
          <div class="crb-row"><span>HOA/Condo</span><span id="m-h">—</span></div>
          <div class="crb-row"><span>PMI</span><span id="m-p">—</span></div>
        </div>
        <div class="crb-note">
          <div>Loan amount: <b id="m-la">—</b></div>
          <div>Total interest over term: <b id="m-ti">—</b></div>
          <div class="crb-jumbo" id="m-jumbo">◆ Jumbo loan — talk to our mortgage partner</div>
        </div>
        <button class="br" style="width:100%;margin-top:22px" onclick="openCalendly()">Speak With a Mortgage Advisor →</button>
      </div>
    </div>
  </div>
</section>

<script>if(document.getElementById('m-price'))mcalc();</script>
```

### 10.2 Affordability Calculator

**Page slug:** `/tools/affordability`

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Tools · Affordability</span>
    <h1>How much <em>home</em> can you afford?</h1>
    <p class="phs" style="margin-top:14px">Reverse mortgage calculator using the 28% debt-to-income rule.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g2" style="align-items:stretch;gap:28px">
      <div>
        <div style="display:flex;flex-direction:column;gap:14px">
          <div><div class="mpl">Annual Household Income</div><input class="ci" id="a-income" type="number" value="500000" oninput="acalc()"></div>
          <div><div class="mpl">Monthly Debts</div><input class="ci" id="a-debts" type="number" value="2500" oninput="acalc()"></div>
          <div><div class="mpl">Down Payment Available</div><input class="ci" id="a-dp" type="number" value="500000" oninput="acalc()"></div>
          <div><div class="mpl">Interest Rate (%)</div><input class="ci" id="a-rate" type="number" step="0.01" value="6.75" oninput="acalc()"></div>
          <div><div class="mpl">Loan Term</div><select class="ci" id="a-term" onchange="acalc()"><option value="30">30 years</option><option value="20">20 years</option><option value="15">15 years</option></select></div>
        </div>
      </div>
      <div class="cr">
        <div class="crl">MAXIMUM AFFORDABLE HOME PRICE</div>
        <div class="crv" id="a-max">$—</div>
        <div class="crb">
          <div class="crb-row"><span>Max monthly PITI</span><span id="a-piti">—</span></div>
          <div class="crb-row"><span>Max loan amount</span><span id="a-loan">—</span></div>
          <div class="crb-row"><span>Debt-to-income used</span><span id="a-dti">—</span></div>
        </div>
        <div class="crb-note">Based on 28% front-end / 36% back-end DTI ratios.</div>
        <button class="br" style="width:100%;margin-top:22px" onclick="openCalendly()">Discuss With an Advisor →</button>
      </div>
    </div>
  </div>
</section>

<script>if(document.getElementById('a-income'))acalc();</script>
```

### 10.3 Rent vs. Buy Calculator

**Page slug:** `/tools/rent-vs-buy`

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Tools · Rent vs. Buy</span>
    <h1>Rent or <em>buy?</em></h1>
    <p class="phs" style="margin-top:14px">Break-even analysis — how many years before buying beats renting.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g2" style="align-items:stretch;gap:28px">
      <div>
        <div style="display:flex;flex-direction:column;gap:14px">
          <div><div class="mpl">Home Purchase Price</div><input class="ci" id="rb-price" type="number" value="2500000" oninput="rbcalc()"></div>
          <div><div class="mpl">Monthly Rent Equivalent</div><input class="ci" id="rb-rent" type="number" value="12000" oninput="rbcalc()"></div>
          <div><div class="mpl">Down Payment (%)</div><input class="ci" id="rb-dp" type="number" value="25" oninput="rbcalc()"></div>
          <div><div class="mpl">Expected Appreciation (%)</div><input class="ci" id="rb-app" type="number" step="0.1" value="4.5" oninput="rbcalc()"></div>
          <div><div class="mpl">Interest Rate (%)</div><input class="ci" id="rb-rate" type="number" step="0.01" value="6.75" oninput="rbcalc()"></div>
        </div>
      </div>
      <div class="cr">
        <div class="crl">BREAK-EVEN POINT</div>
        <div class="crv"><span id="rb-years">—</span></div>
        <div class="crb">
          <div class="crb-row"><span>Monthly cost to buy</span><span id="rb-buy">—</span></div>
          <div class="crb-row"><span>Monthly cost to rent</span><span id="rb-rentM">—</span></div>
          <div class="crb-row"><span>Equity built by year 5</span><span id="rb-equity">—</span></div>
          <div class="crb-row"><span>Home value at year 5</span><span id="rb-val">—</span></div>
        </div>
        <button class="br" style="width:100%;margin-top:22px" onclick="openCalendly()">Discuss With an Advisor →</button>
      </div>
    </div>
  </div>
</section>

<script>if(document.getElementById('rb-price'))rbcalc();</script>
```

### 10.4 Closing Costs Calculator

**Page slug:** `/tools/closing-costs`

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Tools · Closing Costs</span>
    <h1>Estimate your <em>closing costs</em></h1>
    <p class="phs" style="margin-top:14px">Florida-specific: doc stamps, intangible tax, title insurance, and lender fees.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g2" style="align-items:stretch;gap:28px">
      <div>
        <div style="display:flex;flex-direction:column;gap:14px">
          <div><div class="mpl">Purchase Price</div><input class="ci" id="cc-price" type="number" value="2500000" oninput="cccalc()"></div>
          <div><div class="mpl">Down Payment (%)</div><input class="ci" id="cc-dp" type="number" value="25" oninput="cccalc()"></div>
          <div><div class="mpl">Role</div><select class="ci" id="cc-role" onchange="cccalc()"><option value="buyer">Buyer</option><option value="seller">Seller</option></select></div>
        </div>
      </div>
      <div class="cr">
        <div class="crl">ESTIMATED TOTAL CLOSING COSTS</div>
        <div class="crv" id="cc-total">$—</div>
        <div class="crb">
          <div class="crb-row"><span>Doc stamps on deed (.70/$100)</span><span id="cc-ds">—</span></div>
          <div class="crb-row"><span>Doc stamps on mortgage (.35/$100)</span><span id="cc-dm">—</span></div>
          <div class="crb-row"><span>Intangible tax (2‰ of loan)</span><span id="cc-int">—</span></div>
          <div class="crb-row"><span>Title insurance</span><span id="cc-ti">—</span></div>
          <div class="crb-row"><span>Lender fees (est.)</span><span id="cc-lf">—</span></div>
          <div class="crb-row"><span>Recording, misc.</span><span id="cc-misc">—</span></div>
        </div>
        <div class="crb-note">Florida-specific. Actual costs vary by county and title company.</div>
        <button class="br" style="width:100%;margin-top:22px" onclick="openCalendly()">Get a Detailed Estimate →</button>
      </div>
    </div>
  </div>
</section>

<script>if(document.getElementById('cc-price'))cccalc();</script>
```

---

## 11. STEP 10 — Valuation page HTML

**Page slug:** `/valuation`

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Free Property Valuation</span>
    <h1>What is your <em>property worth?</em></h1>
    <p class="phs" style="margin-top:14px">Get a no-obligation comparative market analysis — typically within 24 hours.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g2" style="align-items:start;gap:48px">
      <div>
        <span class="ey">How it works</span>
        <h2 style="font-family:var(--f-display);font-size:32px;font-weight:400;margin-bottom:24px">Your valuation in <em style="color:var(--crimson);font-style:italic">3 steps</em></h2>
        <div style="display:flex;flex-direction:column;gap:22px">
          <div style="display:flex;gap:20px;align-items:flex-start"><div style="width:44px;height:44px;background:var(--crimson);color:#fff;display:flex;align-items:center;justify-content:center;font-family:var(--f-display);font-size:22px;font-weight:600;flex-shrink:0">1</div><div><div style="font-size:15px;font-weight:500;margin-bottom:6px">Submit property details</div><div style="font-size:13px;color:var(--pewter);line-height:1.75">Takes 60 seconds.</div></div></div>
          <div style="display:flex;gap:20px;align-items:flex-start"><div style="width:44px;height:44px;background:var(--crimson);color:#fff;display:flex;align-items:center;justify-content:center;font-family:var(--f-display);font-size:22px;font-weight:600;flex-shrink:0">2</div><div><div style="font-size:15px;font-weight:500;margin-bottom:6px">Our team analyzes the market</div><div style="font-size:13px;color:var(--pewter);line-height:1.75">We pull recent comps and active listings.</div></div></div>
          <div style="display:flex;gap:20px;align-items:flex-start"><div style="width:44px;height:44px;background:var(--crimson);color:#fff;display:flex;align-items:center;justify-content:center;font-family:var(--f-display);font-size:22px;font-weight:600;flex-shrink:0">3</div><div><div style="font-size:15px;font-weight:500;margin-bottom:6px">Receive within 24 hours</div><div style="font-size:13px;color:var(--pewter);line-height:1.75">Delivered by phone or email.</div></div></div>
        </div>
      </div>
      <form class="cf" onsubmit="submitForm(event,'valuation')">
        <span class="ey">Request your valuation</span>
        <input class="cin" type="text" placeholder="Property address" required>
        <select class="cin"><option>Property type…</option><option>Single Family</option><option>Condo</option><option>Townhouse</option><option>Waterfront</option><option>Commercial</option><option>Land</option></select>
        <input class="cin" type="text" placeholder="Full name" required>
        <input class="cin" type="email" placeholder="Email address" required>
        <input class="cin" type="tel" placeholder="Phone number">
        <textarea class="cta2" placeholder="Anything else we should know?"></textarea>
        <button type="submit" class="br" style="width:100%;padding:16px">Get My Free Valuation →</button>
      </form>
    </div>
  </div>
</section>
```

---

## 12. STEP 11 — Contact page HTML

**Page slug:** `/contact`

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Get in Touch</span>
    <h1>Contact <em>Varick Global</em></h1>
    <p class="phs" style="margin-top:14px">Our advisors respond to all inquiries within one business day.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g2" style="align-items:start;gap:48px">
      <div>
        <span class="ey">Aventura Headquarters</span>
        <h2 style="font-family:var(--f-display);font-size:32px;font-weight:400;margin-bottom:22px">Our office</h2>
        <div style="font-size:14.5px;line-height:2;color:var(--graphite);margin-bottom:22px">
          <b>Varick Global Real Estate Advisors</b><br>
          19505 Biscayne Blvd, Suite 2350<br>
          Aventura, FL 33180<br><br>
          📞 <a href="tel:+17863527547" style="color:var(--crimson)">786.352.7547</a><br>
          ✉ <a href="mailto:info@varickglobal.com" style="color:var(--crimson)">info@varickglobal.com</a>
        </div>
        <div style="font-size:13.5px;color:var(--pewter);line-height:1.85;margin-bottom:22px">Monday–Friday · 9:00 AM–6:00 PM<br>Saturday · By appointment<br>Sunday · Closed</div>
        <button class="br" onclick="openCalendly()" style="width:100%;margin-bottom:12px">📅 Schedule a Consultation</button>
        <a href="tel:+17863527547" class="bo" style="width:100%;display:block;text-align:center;padding:14px">📞 Call Directly</a>
      </div>
      <form class="cf" onsubmit="submitForm(event,'contact')">
        <span class="ey">Send a Message</span>
        <h2 style="font-family:var(--f-display);font-size:32px;font-weight:400;margin-bottom:22px">How can we help?</h2>
        <input class="cin" type="text" placeholder="Full name" required>
        <input class="cin" type="email" placeholder="Email address" required>
        <input class="cin" type="tel" placeholder="Phone number">
        <select class="cin"><option>Interest…</option><option>Buying</option><option>Selling</option><option>Leasing</option><option>Commercial</option><option>HOA Services</option><option>VG Elite</option><option>General Inquiry</option></select>
        <textarea class="cta2" placeholder="How can we help you?"></textarea>
        <button type="submit" class="br" style="width:100%;padding:16px">Send Message →</button>
      </form>
    </div>
  </div>
</section>
```

---

## 13. STEP 12 — Journal page HTML

**Page slug:** `/journal`

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Journal · Insights &amp; Analysis</span>
    <h1>The South Florida <em>market</em>, decoded</h1>
    <p class="phs" style="margin-top:14px">Original research, market reports, and neighborhood guides from the Varick Global team.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g3">
      <a class="jrn-card" href="/journal/q3-2026-market-report">
        <div class="jrn-thumb crimson">📊</div>
        <div class="jrn-body">
          <div class="jrn-cat">Market Report · Q3 2026</div>
          <div class="jrn-title">South Florida Luxury Market Enters New Cycle</div>
          <div class="jrn-excerpt">Median luxury sale prices climbed 6.2% YoY. Full three-county breakdown.</div>
          <div class="jrn-meta"><span>Chris Gallego</span><span>8 MIN</span></div>
        </div>
      </a>
      <a class="jrn-card" href="/journal/bal-harbour-guide">
        <div class="jrn-thumb gold">🏖️</div>
        <div class="jrn-body">
          <div class="jrn-cat">Neighborhood Guide</div>
          <div class="jrn-title">The Ultimate Guide to Buying in Bal Harbour</div>
          <div class="jrn-excerpt">Everything international buyers should know about the ultra-luxury Bal Harbour market.</div>
          <div class="jrn-meta"><span>Alfredo Morejon</span><span>12 MIN</span></div>
        </div>
      </a>
      <a class="jrn-card" href="/journal/sb-4d-hoa">
        <div class="jrn-thumb violet">⚖️</div>
        <div class="jrn-body">
          <div class="jrn-cat">HOA Legal Update</div>
          <div class="jrn-title">Florida SB-4D: What HOA Boards Must Know</div>
          <div class="jrn-excerpt">The 2022 Surfside legislation continues to reshape HOA compliance.</div>
          <div class="jrn-meta"><span>Gloria Grullon</span><span>15 MIN</span></div>
        </div>
      </a>
    </div>
  </div>
</section>
```

> **For actual articles**, use WordPress's built-in Posts feature. Each Journal article is a Post with a Category (Market Report / Neighborhood Guide / HOA Legal / Buyer Education) and the same visual treatment.

---

## 14. STEP 13 — About / Team / FAQ / Sitemap

### 14.1 About page (`/about`)

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">About Varick Global</span>
    <h1>Where <em>luxury</em> meets precision</h1>
    <p class="phs" style="margin-top:14px">A premier real estate firm committed to unparalleled service across South Florida since 2016.</p>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="g2" style="align-items:start;gap:48px">
      <div>
        <span class="ey">Our Mission</span>
        <h2 style="font-family:var(--f-display);font-size:32px;font-weight:400;margin-bottom:16px">Delivering results that exceed expectations</h2>
        <p style="font-size:14.5px;color:var(--graphite);line-height:1.85">Our mission is to provide exceptional real estate services through innovative solutions, personalized attention, and unwavering commitment to our clients' success.</p>
      </div>
      <div>
        <span class="ey">Our Vision</span>
        <h2 style="font-family:var(--f-display);font-size:32px;font-weight:400;margin-bottom:16px">The leading advisory in South Florida</h2>
        <p style="font-size:14.5px;color:var(--graphite);line-height:1.85">To be known for expertise, integrity, and exceptional client service — creating value for our clients and impact in the communities we serve.</p>
      </div>
    </div>
  </div>
</section>
```

### 14.2 FAQ page (`/faq`)

```html
<div class="ph">
  <div class="ctr">
    <span class="eyb">Frequently Asked Questions</span>
    <h1>Everything you need to <em>know</em></h1>
  </div>
</div>

<section class="sec" style="background:var(--white)">
  <div class="ctr">
    <div class="fi"><button class="fq" onclick="toggleFAQ(this)"><span class="fqt">What areas do you serve?</span><div class="fch">+</div></button><div class="fa">Miami-Dade, Broward, and Palm Beach counties — the full South Florida luxury corridor.</div></div>
    <div class="fi"><button class="fq" onclick="toggleFAQ(this)"><span class="fqt">Do you work with international buyers?</span><div class="fch">+</div></button><div class="fa">Yes. Significant international clientele. Bilingual EN/ES. FIRPTA coordination.</div></div>
    <div class="fi"><button class="fq" onclick="toggleFAQ(this)"><span class="fqt">What is VG Elite?</span><div class="fch">+</div></button><div class="fa">Our private Sports & Entertainment division. Access is by invitation or referral only.</div></div>
    <div class="fi"><button class="fq" onclick="toggleFAQ(this)"><span class="fqt">Do you offer free valuations?</span><div class="fch">+</div></button><div class="fa">Yes. Complimentary CMAs delivered within 24 hours, no obligation.</div></div>
    <div class="fi"><button class="fq" onclick="toggleFAQ(this)"><span class="fqt">Can you help with distressed HOAs?</span><div class="fch">+</div></button><div class="fa">Yes — this is a specialty. Advisory, receivership, conversions, and full HOA sales.</div></div>
  </div>
</section>
```

---

## 15. STEP 14 — Remaining pages

Each of these follows the same page template pattern (`.ph` hero + `.sec` content sections). For brevity, use the full markup from `varick-global-COMPLETE.html` as the source. The pages to create:

| Page | Slug | Template |
|---|---|---|
| Search | `/properties` | IDX plugin shortcode inside `.sec` wrapper |
| Team | `/team` | 4 `.ac` advisor cards |
| Recently Sold | `/sold` | 6 `.sold-card` items |
| New Developments | `/new-developments` | 3 `.dev-card` items |
| Foreclosures | `/foreclosures` | Table with `.fc-table` class |
| Buyer's Guide | `/buyers-guide` | 6 `.guide-card` step cards |
| Seller's Guide | `/sellers-guide` | 6 `.guide-card` step cards |
| Neighborhoods | `/neighborhoods` | 3 `.nc2` county cards linking to subpages |
| Careers | `/careers` | 4 `.job-card` items |
| Press | `/press` | 7 `.press-item` rows |
| Sitemap | `/sitemap` | Grid of `.smcol` category columns |

**Extraction command** (in Terminal, from wherever you have `varick-global-COMPLETE.html`):

```bash
# Extract the Recently Sold page HTML
grep -A 40 'id="p-sold"' varick-global-COMPLETE.html | head -50

# Or open the file in a text editor and search for id="p-{slug}"
# Copy the contents between the opening and closing div tags
```

---

## 16. Testing checklist

After installing, verify each of these on a live URL:

- [ ] Home page renders with video hero (or poster fallback)
- [ ] Nav mega-menus open on hover
- [ ] Fonts loading (Cormorant Garamond visible in italic hero title)
- [ ] Colors match (Crimson `#A6192E` on Cream `#F5F2ED`)
- [ ] Palette picker toggles between Refined and Lighter (bottom-left)
- [ ] Chat widget opens (bottom-right)
- [ ] Chat responds to keywords ("elite", "schedule", "sell", "buy")
- [ ] Mortgage calculator computes correctly
- [ ] Affordability, Rent vs Buy, Closing Costs calculators work
- [ ] AI Match returns mock results after 1.2s
- [ ] Exit-intent modal fires when mouse leaves top of window
- [ ] Toast notifications appear on form submit
- [ ] Sticky mobile CTA bar visible below 720px width
- [ ] All forms submit and show toast
- [ ] Calendly buttons trigger `openCalendly()` (currently a toast — swap for real Calendly script)
- [ ] Google Analytics events firing (`schedule_click`, `mortgage_calc_used`, etc.)
- [ ] JSON-LD schema visible in page source (View Source → search "RealEstateAgent")
- [ ] `robots.txt` accessible at `/robots.txt`
- [ ] `sitemap_index.xml` accessible (from Rank Math)

---

## Final integration steps

1. **Swap `openCalendly()` for real Calendly:** In the global JS (Section 4), replace the placeholder body with `Calendly.initPopupWidget({url:'https://calendly.com/YOUR-HANDLE/consultation'})` and add the Calendly widget script to Section 2.
2. **Wire forms:** Replace each `<form onsubmit="submitForm...">` with a Fluent Forms or WPForms shortcode connected to HubSpot Free CRM.
3. **Add real hero video:** In the Home page HTML (Section 7), uncomment the `<video>` tag and point `src` to your uploaded MP4 in the WordPress Media Library.
4. **Replace emoji placeholders:** Every `<div class="pi">🏖️` etc. should become a real `<img>` tag with a WordPress-hosted property photo.
5. **Wire AI endpoints:** In the global JS, replace `runAIMatch()`'s `setTimeout` mock and `chatSend()`'s `getBotReply` keyword logic with `fetch()` calls to your `/wp-json/varick/v1/property-match` and `/wp-json/varick/v1/concierge` REST endpoints (create these via a small custom WordPress plugin that proxies to Claude Sonnet API).

---

*End of WordPress code compilation. Companion documents: `varick-global-COMPLETE.html` (working prototype), `VARICK_WORDPRESS_MCP_GUIDE.md` (build workflow), `VARICK_LIGHTER_PALETTE.md` (alternative palette).*
