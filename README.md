<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ootu — Food Delivery App UI</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;0,9..144,700;1,9..144,500&family=Work+Sans:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root{
    --leaf-deep:#233B1E;
    --leaf-mid:#3C5B34;
    --leaf-pale:#DCE7CE;
    --turmeric:#E8A230;
    --turmeric-soft:#F4D9A6;
    --chili:#C1442E;
    --paper:#FBF2DE;
    --paper-warm:#F5E8CB;
    --ink:#241D14;
    --ink-soft:#6E5D45;
    --line:#D8C8A4;
    --display: 'Fraunces', serif;
    --body: 'Work Sans', sans-serif;
    --mono: 'Space Mono', monospace;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    background:#171911;
    font-family:var(--body);
    color:var(--ink);
    padding:48px 24px 80px;
  }
  .intro{
    max-width:900px;
    margin:0 auto 44px;
    color:var(--paper-warm);
  }
  .intro .eyebrow{
    font-family:var(--mono);
    font-size:12px;
    letter-spacing:.14em;
    text-transform:uppercase;
    color:var(--turmeric);
    margin-bottom:10px;
  }
  .intro h1{
    font-family:var(--display);
    font-weight:600;
    font-size:44px;
    margin:0 0 10px;
    color:#FBF2DE;
    letter-spacing:-.01em;
  }
  .intro h1 em{
    font-style:italic;
    color:var(--turmeric);
  }
  .intro p{
    font-size:15px;
    line-height:1.6;
    color:#C9C3B2;
    max-width:560px;
    margin:0;
  }

  .showcase{
    display:flex;
    gap:34px;
    overflow-x:auto;
    padding:12px 4px 40px;
    scroll-snap-type:x proximity;
    max-width:1500px;
    margin:0 auto;
  }
  .screen-label{
    font-family:var(--mono);
    font-size:11px;
    letter-spacing:.1em;
    text-transform:uppercase;
    color:var(--turmeric-soft);
    margin-bottom:14px;
    display:flex;
    align-items:center;
    gap:8px;
  }
  .screen-label .n{
    background:var(--turmeric);
    color:var(--leaf-deep);
    font-weight:700;
    border-radius:50%;
    width:20px;height:20px;
    display:flex;align-items:center;justify-content:center;
    font-size:10px;
  }
  .col{ scroll-snap-align:start; flex:0 0 auto;}

  .phone{
    width:375px;
    height:812px;
    background:var(--paper);
    border-radius:44px;
    border:10px solid #100F0A;
    box-shadow:0 30px 60px -20px rgba(0,0,0,.6);
    overflow:hidden;
    position:relative;
    display:flex;
    flex-direction:column;
  }
  .notch{
    position:absolute;
    top:10px; left:50%; transform:translateX(-50%);
    width:120px; height:22px;
    background:#100F0A;
    border-radius:14px;
    z-index:50;
  }
  .status{
    height:46px;
    flex:0 0 auto;
    display:flex;
    align-items:flex-end;
    justify-content:space-between;
    padding:0 26px 8px;
    font-family:var(--mono);
    font-size:11px;
    font-weight:700;
  }
  .home-indicator{
    position:absolute;
    bottom:8px; left:50%; transform:translateX(-50%);
    width:120px; height:4px;
    background:rgba(0,0,0,.5);
    border-radius:3px;
    z-index:50;
  }
  .scroll{
    flex:1 1 auto;
    overflow-y:auto;
  }
  .scroll::-webkit-scrollbar{display:none;}

  /* ---------- shared bits ---------- */
  .veg-dot{width:10px;height:10px;border:1.5px solid #2E7D32;padding:2px;display:inline-block;}
  .veg-dot i{display:block;width:100%;height:100%;border-radius:50%;background:#2E7D32;}
  .nonveg-dot{width:10px;height:10px;border:1.5px solid var(--chili);padding:2px;display:inline-block;clip-path:polygon(50% 0,100% 100%,0 100%);}
  .nonveg-dot i{display:block;width:100%;height:100%;background:var(--chili);clip-path:polygon(50% 0,100% 100%,0 100%);}

  .chip-scroll{display:flex; gap:10px; overflow-x:auto; padding:2px 20px 4px;}
  .chip{
    flex:0 0 auto;
    font-family:var(--body);
    font-weight:600;
    font-size:12.5px;
    padding:9px 16px;
    border-radius:100px;
    background:var(--paper-warm);
    border:1px solid var(--line);
    display:flex; align-items:center; gap:6px;
    white-space:nowrap;
  }
  .chip.active{ background:var(--leaf-deep); color:var(--paper); border-color:var(--leaf-deep);}

  /* ---------- SCREEN 1: HOME ---------- */
  .home-hero{
    background:var(--leaf-deep);
    color:var(--paper);
    padding:6px 20px 26px;
    border-radius:0 0 28px 28px;
  }
  .loc-row{display:flex; align-items:center; justify-content:space-between; margin-bottom:18px;}
  .loc{font-size:12px; color:var(--turmeric-soft); font-family:var(--mono);}
  .loc b{color:#fff; font-family:var(--body); font-size:14px; display:block; margin-top:2px;}
  .avatar{
    width:34px;height:34px;border-radius:50%;
    background:var(--turmeric);
    display:flex;align-items:center;justify-content:center;
    font-family:var(--display); font-weight:700; color:var(--leaf-deep);
  }
  .greet{font-family:var(--display); font-size:26px; font-weight:600; line-height:1.15; margin:0 0 16px;}
  .greet em{color:var(--turmeric); font-style:italic;}
  .search{
    background:var(--paper);
    border-radius:14px;
    padding:13px 16px;
    display:flex; align-items:center; gap:10px;
    color:var(--ink-soft);
    font-size:13.5px;
  }
  .search svg{flex:0 0 auto;}

  .section-title{
    display:flex; align-items:baseline; justify-content:space-between;
    padding:22px 20px 10px;
  }
  .section-title h3{
    font-family:var(--display); font-size:19px; margin:0; font-weight:600;
  }
  .section-title a{font-size:11.5px; color:var(--chili); font-weight:600; font-family:var(--mono);}

  .leaf-card{
    background:var(--paper-warm);
    margin:0 20px 16px;
    border-radius:20px;
    padding:14px;
    display:flex;
    gap:14px;
    position:relative;
    border:1px solid var(--line);
  }
  .leaf-card::after{
    content:"";
    position:absolute; top:14px; right:14px;
    width:14px;height:14px;
    border-radius:0 12px 0 12px;
    background:var(--leaf-mid);
    opacity:.15;
  }
  .thumb{
    width:66px;height:66px;border-radius:16px;
    background:var(--leaf-pale);
    display:flex;align-items:center;justify-content:center;
    font-size:30px;
    flex:0 0 auto;
  }
  .card-body{flex:1; min-width:0;}
  .card-body h4{margin:0 0 3px; font-family:var(--display); font-size:15.5px; font-weight:600;}
  .card-body .tags{font-size:11.5px; color:var(--ink-soft); margin-bottom:8px;}
  .meta-row{display:flex; align-items:center; gap:10px; font-size:11.5px; color:var(--ink-soft); font-family:var(--mono);}
  .rating{
    background:var(--leaf-deep); color:var(--paper);
    border-radius:6px; padding:2px 7px;
    font-weight:700; display:flex; align-items:center; gap:3px;
  }

  .promo-strip{
    margin:4px 20px 8px;
    background:var(--chili);
    color:var(--paper);
    border-radius:18px;
    padding:16px 18px;
    display:flex;
    align-items:center;
    justify-content:space-between;
    overflow:hidden;
    position:relative;
  }
  .promo-strip .txt b{font-family:var(--display); font-size:16px; display:block;}
  .promo-strip .txt span{font-size:11.5px; opacity:.85;}
  .promo-strip .pct{font-family:var(--mono); font-size:26px; font-weight:700; color:var(--turmeric);}

  /* bottom tab bar */
  .tabbar{
    flex:0 0 auto;
    display:flex;
    justify-content:space-around;
    padding:12px 10px 22px;
    background:var(--paper);
    border-top:1px solid var(--line);
  }
  .tab{display:flex; flex-direction:column; align-items:center; gap:4px; font-size:10px; font-family:var(--mono); color:var(--ink-soft);}
  .tab.active{color:var(--chili); font-weight:700;}
  .tab .dot{width:5px;height:5px;border-radius:50%;background:var(--chili); opacity:0;}
  .tab.active .dot{opacity:1;}

  /* ---------- SCREEN 2: MENU ---------- */
  .menu-hero{
    height:190px;
    background:linear-gradient(160deg, var(--leaf-mid), var(--leaf-deep));
    position:relative;
    color:var(--paper);
    padding:16px 20px;
    flex:0 0 auto;
  }
  .back-btn{
    width:34px;height:34px;border-radius:50%;
    background:rgba(255,255,255,.14);
    display:flex;align-items:center;justify-content:center;
  }
  .menu-hero .name{
    position:absolute; bottom:16px; left:20px; right:20px;
    font-family:var(--display); font-size:24px; font-weight:700;
  }
  .menu-hero .sub{
    position:absolute; bottom:-2px; left:20px;
    font-size:11.5px; font-family:var(--mono); opacity:.85;
  }
  .menu-stats{
    display:flex; gap:0;
    background:var(--paper-warm);
    margin:0 20px; border-radius:14px;
    padding:12px 6px;
    position:relative; top:-16px;
    box-shadow:0 8px 20px -8px rgba(0,0,0,.25);
  }
  .menu-stats .stat{flex:1; text-align:center; border-right:1px solid var(--line);}
  .menu-stats .stat:last-child{border-right:none;}
  .menu-stats .stat b{display:block; font-family:var(--display); font-size:15px;}
  .menu-stats .stat span{font-size:10px; color:var(--ink-soft); font-family:var(--mono);}

  .menu-cat-title{
    padding:18px 20px 4px;
    font-family:var(--mono);
    font-size:11px;
    letter-spacing:.1em;
    text-transform:uppercase;
    color:var(--chili);
    font-weight:700;
  }
  .menu-item{
    display:flex; gap:12px;
    padding:14px 20px;
    border-bottom:1px solid var(--line);
    align-items:center;
  }
  .menu-item .info{flex:1; min-width:0;}
  .menu-item .info .top{display:flex; align-items:center; gap:7px; margin-bottom:4px;}
  .menu-item h5{margin:0; font-family:var(--display); font-size:14.5px; font-weight:600;}
  .menu-item p{margin:0 0 8px; font-size:11.5px; color:var(--ink-soft); line-height:1.4;}
  .price{font-family:var(--mono); font-weight:700; font-size:13px;}
  .add-btn{
    font-family:var(--mono); font-weight:700; font-size:11.5px;
    border:1.5px solid var(--chili); color:var(--chili);
    background:var(--paper);
    border-radius:9px;
    padding:6px 14px;
    flex:0 0 auto;
  }
  .menu-thumb{
    width:58px;height:58px;border-radius:14px;
    background:var(--leaf-pale);
    display:flex;align-items:center;justify-content:center;
    font-size:26px;
    flex:0 0 auto;
  }
  .cart-fab{
    position:absolute; bottom:22px; left:20px; right:20px;
    background:var(--leaf-deep); color:var(--paper);
    border-radius:16px;
    padding:14px 18px;
    display:flex; align-items:center; justify-content:space-between;
    font-family:var(--body); font-weight:600; font-size:13.5px;
    box-shadow:0 10px 24px -8px rgba(0,0,0,.4);
  }
  .cart-fab .badge{
    background:var(--turmeric); color:var(--leaf-deep);
    font-family:var(--mono); font-weight:700; font-size:11px;
    border-radius:50%; width:20px;height:20px;
    display:flex;align-items:center;justify-content:center;
    margin-right:8px;
  }

  /* ---------- SCREEN 3: CART / RECEIPT ---------- */
  .receipt-wrap{padding:20px;}
  .receipt{
    background:var(--paper-warm);
    border-radius:4px;
    padding:22px 18px 0;
    position:relative;
    box-shadow:0 10px 30px -14px rgba(0,0,0,.2);
  }
  .receipt::before, .receipt::after{
    content:"";
    position:absolute; left:0; right:0; height:12px;
    background-image:radial-gradient(circle 6px, var(--paper) 6px, transparent 7px);
    background-size:18px 12px;
    background-repeat:repeat-x;
    background-position:-3px center;
  }
  .receipt::before{ top:-6px; }
  .receipt::after{ bottom:-6px; transform:rotate(180deg); }
  .receipt h4{
    text-align:center; font-family:var(--display); font-size:17px; margin:0 0 2px;
  }
  .receipt .rid{
    text-align:center; font-family:var(--mono); font-size:10.5px; color:var(--ink-soft); margin-bottom:16px;
  }
  .rline{
    display:flex; justify-content:space-between; align-items:flex-start;
    font-size:13px; margin-bottom:12px;
  }
  .rline .qty{font-family:var(--mono); font-weight:700; color:var(--chili); margin-right:8px;}
  .rline .amt{font-family:var(--mono); font-weight:600;}
  .rdash{border-top:1px dashed var(--line); margin:14px 0;}
  .rtotal-row{display:flex; justify-content:space-between; font-size:12.5px; margin-bottom:8px; color:var(--ink-soft);}
  .rtotal-row.grand{
    font-size:16px; font-weight:700; color:var(--ink);
    font-family:var(--display);
    padding-top:8px;
  }
  .rtotal-row.grand .amt{font-family:var(--mono);}
  .coupon{
    margin:16px 0 18px;
    border:1.5px dashed var(--chili);
    border-radius:10px;
    padding:10px 12px;
    display:flex; align-items:center; justify-content:space-between;
    background:#fff;
  }
  .coupon .lbl{font-family:var(--mono); font-size:11.5px; font-weight:700; color:var(--chili);}
  .coupon .apply{font-size:11px; font-weight:700; color:var(--leaf-deep);}
  .addr-box{
    margin:0 20px 18px;
    background:var(--paper-warm);
    border-radius:14px;
    padding:14px 16px;
    border:1px solid var(--line);
    display:flex; gap:12px; align-items:flex-start;
  }
  .addr-box .lab{font-family:var(--mono); font-size:10.5px; color:var(--chili); font-weight:700; margin-bottom:3px;}
  .addr-box p{margin:0; font-size:12.5px; color:var(--ink-soft); line-height:1.4;}
  .pay-btn{
    margin:0 20px;
    background:var(--chili); color:#fff;
    border-radius:16px;
    padding:16px;
    text-align:center;
    font-family:var(--body); font-weight:700; font-size:14.5px;
    display:flex; align-items:center; justify-content:space-between;
    box-shadow:0 10px 24px -10px rgba(193,68,46,.6);
  }
  .pay-btn span.small{font-family:var(--mono); font-weight:400; font-size:11px; opacity:.85; display:block;}

  /* ---------- SCREEN 4: TRACKING ---------- */
  .track-hero{
    background:var(--leaf-deep); color:var(--paper);
    padding:18px 20px 20px;
    flex:0 0 auto;
  }
  .track-hero .eta{font-family:var(--display); font-size:26px; font-weight:700; margin:6px 0 2px;}
  .track-hero .eta span{color:var(--turmeric);}
  .track-hero .status-line{font-family:var(--mono); font-size:11.5px; color:var(--paper-warm); opacity:.8;}
  .map{
    height:150px; margin:16px 20px 0;
    border-radius:16px;
    background:
      repeating-linear-gradient(0deg, transparent, transparent 18px, rgba(60,91,52,.15) 19px),
      repeating-linear-gradient(90deg, transparent, transparent 18px, rgba(60,91,52,.15) 19px),
      var(--leaf-pale);
    position:relative;
    overflow:hidden;
  }
  .map .route{
    position:absolute; top:20%; left:10%;
    width:70%; height:60%;
    border:3px dashed var(--chili);
    border-radius:40% 60% 50% 50%;
    opacity:.6;
  }
  .map .pin{position:absolute; font-size:22px;}
  .map .pin.rider{top:35%; left:20%;}
  .map .pin.home{bottom:18%; right:16%;}

  .rider-card{
    margin:16px 20px;
    background:var(--paper-warm);
    border-radius:16px;
    padding:14px 16px;
    display:flex; align-items:center; gap:12px;
    border:1px solid var(--line);
  }
  .rider-card .pic{
    width:46px;height:46px;border-radius:50%;
    background:var(--turmeric);
    display:flex;align-items:center;justify-content:center;
    font-family:var(--display); font-weight:700; color:var(--leaf-deep); font-size:16px;
  }
  .rider-card .info{flex:1;}
  .rider-card .info b{font-family:var(--display); font-size:14px; display:block;}
  .rider-card .info span{font-size:11px; color:var(--ink-soft); font-family:var(--mono);}
  .icon-btn{
    width:38px;height:38px;border-radius:50%;
    background:var(--leaf-deep); color:var(--paper);
    display:flex;align-items:center;justify-content:center;
  }

  .timeline{margin:6px 20px 0; padding:0;}
  .t-item{
    display:flex; gap:14px; position:relative; padding-bottom:22px;
  }
  .t-item:last-child{padding-bottom:0;}
  .t-item .stem{
    width:2px; background:var(--line);
    position:absolute; left:9px; top:22px; bottom:0;
  }
  .t-item:last-child .stem{display:none;}
  .t-dot{
    width:20px;height:20px;border-radius:50%;
    background:var(--paper-warm); border:2px solid var(--line);
    flex:0 0 auto; display:flex; align-items:center; justify-content:center;
    font-size:10px; z-index:1;
  }
  .t-item.done .t-dot{background:var(--leaf-deep); border-color:var(--leaf-deep); color:var(--paper);}
  .t-item.active .t-dot{background:var(--turmeric); border-color:var(--turmeric);}
  .t-body b{display:block; font-size:13px; font-family:var(--body); font-weight:600;}
  .t-body span{font-size:11px; color:var(--ink-soft); font-family:var(--mono);}

  .ticket-code{
    margin:18px 20px 0;
    text-align:center;
    font-family:var(--mono);
    font-size:11px;
    color:var(--ink-soft);
    letter-spacing:.08em;
  }
  .ticket-code b{display:block; font-size:15px; color:var(--ink); letter-spacing:.15em; margin-top:2px;}
</style>
</head>
<body>

<div class="intro">
  <div class="eyebrow">UI / UX — Mobile app · 4 screens</div>
  <h1>kiramathu — <em>samayal.</h1>
  <p>Tamil Nadu food-delivery app concept. Banana-leaf serving language, chili-red CTAs, turmeric accents, and a ticket-stub feel for tracking — built from the vocabulary of a local kadai, not a generic delivery template.</p>
</div>

<div class="showcase">

  <div class="col">
    <div class="screen-label"><span class="n">1</span>Home — browse</div>
    <div class="phone">
      <div class="notch"></div>
      <div class="status" style="color:#fff; background:var(--leaf-deep);">
        <span>9:41</span><span>●●● ▲ 100%</span>
      </div>
      <div class="scroll">
        <div class="home-hero">
          <div class="loc-row">
            <div class="loc">DELIVERING TO<b>Gandhipuram, Coimbatore</b></div>
            <div class="avatar">R</div>
          </div>
          <h2 class="greet">Vanakkam, Ram 👋<br>What's today's <em>saapadu</em>?</h2>
          <div class="search">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="7"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
            Search kadai, biryani, sweets…
          </div>
        </div>

        <div class="chip-scroll">
          <div class="chip active">🔥 All</div>
          <div class="chip">🍛 Meals</div>
          <div class="chip">🍗 Biryani</div>
          <div class="chip">🥘 Chettinad</div>
          <div class="chip">🍩 Sweets</div>
          <div class="chip">☕ Kadai Tea</div>
        </div>

        <div class="promo-strip">
          <div class="txt"><b>First order free delivery</b><span>on orders above ₹199</span></div>
          <div class="pct">50%</div>
        </div>

        <div class="section-title"><h3>Near you</h3><a>SEE ALL</a></div>

        <div class="leaf-card">
          <div class="thumb">🍛</div>
          <div class="card-body">
            <h4>Amma's Kitchen</h4>
            <div class="tags">Veg meals · Sambar · Rasam</div>
            <div class="meta-row">
              <div class="rating">★ 4.6</div><span>25 min</span><span>·</span><span>₹150 for one</span>
            </div>
          </div>
        </div>

        <div class="leaf-card">
          <div class="thumb">🍗</div>
          <div class="card-body">
            <h4>Anjappar Biryani Kadai</h4>
            <div class="tags">Chettinad · Non-veg · Biryani</div>
            <div class="meta-row">
              <div class="rating">★ 4.8</div><span>32 min</span><span>·</span><span>₹280 for one</span>
            </div>
          </div>
        </div>

        <div class="leaf-card">
          <div class="thumb">🍩</div>
          <div class="card-body">
            <h4>Grand Sweets & Snacks</h4>
            <div class="tags">Mysore pak · Murukku · Adhirasam</div>
            <div class="meta-row">
              <div class="rating">★ 4.7</div><span>20 min</span><span>·</span><span>₹120 for one</span>
            </div>
          </div>
        </div>

        <div class="leaf-card">
          <div class="thumb">☕</div>
          <div class="card-body">
            <h4>Sangeetha Filter Kaapi</h4>
            <div class="tags">Tumbler filter coffee · Bajji</div>
            <div class="meta-row">
              <div class="rating">★ 4.5</div><span>15 min</span><span>·</span><span>₹60 for one</span>
            </div>
          </div>
        </div>
      </div>

      <div class="tabbar">
        <div class="tab active"><span class="dot"></span>🏠<span>Home</span></div>
        <div class="tab">🔎<span>Search</span></div>
        <div class="tab">🧾<span>Orders</span></div>
        <div class="tab">👤<span>Profile</span></div>
      </div>
      <div class="home-indicator"></div>
    </div>
  </div>

  <div class="col">
    <div class="screen-label"><span class="n">2</span>Menu — restaurant</div>
    <div class="phone">
      <div class="notch"></div>
      <div class="status" style="color:#fff;position:absolute;top:0;left:0;right:0;z-index:20; padding:14px 26px 0;">
        <span>9:41</span><span>●●● ▲ 100%</span>
      </div>
      <div class="scroll" style="position:relative;">
        <div class="menu-hero">
          <div class="back-btn">←</div>
          <div class="name">Anjappar Biryani Kadai</div>
          <div class="sub">Chettinad · Non-veg · Open till 11 PM</div>
        </div>
        <div class="menu-stats">
          <div class="stat"><b>★ 4.8</b><span>2.3K RATINGS</span></div>
          <div class="stat"><b>32 min</b><span>DELIVERY</span></div>
          <div class="stat"><b>₹280</b><span>FOR ONE</span></div>
        </div>

        <div class="menu-cat-title">Biryani</div>

        <div class="menu-item">
          <div class="menu-thumb">🍛</div>
          <div class="info">
            <div class="top"><span class="nonveg-dot"><i></i></span><h5>Chicken Chettinad Biryani</h5></div>
            <p>Slow-cooked with 12 spices, served with onion raita</p>
            <span class="price">₹220</span>
          </div>
          <div class="add-btn">ADD +</div>
        </div>

        <div class="menu-item">
          <div class="menu-thumb">🍚</div>
          <div class="info">
            <div class="top"><span class="veg-dot"><i></i></span><h5>Vegetable Dum Biryani</h5></div>
            <p>Basmati, mixed vegetables, fried cashew</p>
            <span class="price">₹170</span>
          </div>
          <div class="add-btn">ADD +</div>
        </div>

        <div class="menu-cat-title">Kadai specials</div>

        <div class="menu-item">
          <div class="menu-thumb">🍗</div>
          <div class="info">
            <div class="top"><span class="nonveg-dot"><i></i></span><h5>Pepper Chicken Fry</h5></div>
            <p>Dry roasted, curry leaves, black pepper</p>
            <span class="price">₹210</span>
          </div>
          <div class="add-btn">ADD +</div>
        </div>

        <div class="menu-item">
          <div class="menu-thumb">🥘</div>
          <div class="info">
            <div class="top"><span class="nonveg-dot"><i></i></span><h5>Mutton Chukka</h5></div>
            <p>Semi-gravy, roasted coconut, small onions</p>
            <span class="price">₹320</span>
          </div>
          <div class="add-btn"><span style="display:flex;align-items:center;gap:8px;">− 2 +</span></div>
        </div>

        <div class="menu-item" style="border-bottom:none;">
          <div class="menu-thumb">🥣</div>
          <div class="info">
            <div class="top"><span class="veg-dot"><i></i></span><h5>Paruppu Rasam</h5></div>
            <p>Toor dal, tamarind, fresh ground pepper</p>
            <span class="price">₹60</span>
          </div>
          <div class="add-btn">ADD +</div>
        </div>

        <div style="height:90px;"></div>
      </div>
      <div class="cart-fab" style="position:absolute; bottom:26px;">
        <div style="display:flex; align-items:center;"><span class="badge">3</span> View cart</div>
        <div>₹540 →</div>
      </div>
      <div class="home-indicator" style="z-index:30;"></div>
    </div>
  </div>

  <div class="col">
    <div class="screen-label"><span class="n">3</span>Cart — checkout</div>
    <div class="phone">
      <div class="notch"></div>
      <div class="status"><span>9:41</span><span>●●● ▲ 100%</span></div>
      <div class="scroll">
        <div class="section-title" style="padding-top:6px;"><h3>Your order</h3><a>EDIT</a></div>

        <div class="receipt-wrap">
          <div class="receipt">
            <h4>Anjappar Biryani Kadai</h4>
            <div class="rid">TOKEN #AK-2286</div>

            <div class="rline"><div><span class="qty">1×</span>Chicken Chettinad Biryani</div><div class="amt">₹220</div></div>
            <div class="rline"><div><span class="qty">2×</span>Mutton Chukka</div><div class="amt">₹640</div></div>
            <div class="rline"><div><span class="qty">1×</span>Paruppu Rasam</div><div class="amt">₹60</div></div>

            <div class="rdash"></div>

            <div class="rtotal-row"><span>Item total</span><span class="amt">₹920</span></div>
            <div class="rtotal-row"><span>Delivery fee</span><span class="amt">₹25</span></div>
            <div class="rtotal-row"><span>GST & charges</span><span class="amt">₹42</span></div>
            <div class="rtotal-row"><span>Coupon FIRST50</span><span class="amt" style="color:var(--chili);">−₹100</span></div>
            <div class="rtotal-row grand"><span>To pay</span><span class="amt">₹887</span></div>

            <div class="coupon">
              <div><div class="lbl">FIRST50 applied</div></div>
              <div class="apply">CHANGE</div>
            </div>
          </div>
        </div>

        <div class="addr-box">
          <div class="icon-btn" style="background:var(--leaf-deep); flex:0 0 auto;">📍</div>
          <div>
            <div class="lab">DELIVER TO — HOME</div>
            <p>14, Kamaraj Nagar 3rd Street, Gandhipuram, Coimbatore – 641012</p>
          </div>
        </div>

        <div style="height:6px;"></div>
      </div>

      <div style="padding:0 0 22px;">
        <div class="pay-btn">
          <span>Pay ₹887<span class="small">UPI · Cash on delivery available</span></span>
          <span>→</span>
        </div>
      </div>
      <div class="home-indicator"></div>
    </div>
  </div>

  <div class="col">
    <div class="screen-label"><span class="n">4</span>Tracking — order live</div>
    <div class="phone">
      <div class="notch"></div>
      <div class="status" style="color:#fff; background:var(--leaf-deep);"><span>9:41</span><span>●●● ▲ 100%</span></div>
      <div class="scroll">
        <div class="track-hero">
          <div style="font-family:var(--mono); font-size:11px; opacity:.8;">TOKEN #AK-2286</div>
          <div class="eta">12 <span>mins away</span></div>
          <div class="status-line">Kumar is bringing your saapadu</div>
        </div>

        <div class="map">
          <div class="route"></div>
          <div class="pin rider">🛵</div>
          <div class="pin home">🏠</div>
        </div>

        <div class="rider-card">
          <div class="pic">K</div>
          <div class="info"><b>Kumar S.</b><span>TVS Jupiter · TN 38 AX 4471</span></div>
          <div class="icon-btn">📞</div>
        </div>

        <div class="timeline">
          <div class="t-item done">
            <div style="position:relative;"><div class="t-dot">✓</div><div class="stem"></div></div>
            <div class="t-body"><b>Order confirmed</b><span>7:42 PM · Anjappar Biryani Kadai</span></div>
          </div>
          <div class="t-item done">
            <div style="position:relative;"><div class="t-dot">✓</div><div class="stem"></div></div>
            <div class="t-body"><b>Kadai is preparing your food</b><span>7:45 PM · 12 min prep</span></div>
          </div>
          <div class="t-item active">
            <div style="position:relative;"><div class="t-dot">●</div><div class="stem"></div></div>
            <div class="t-body"><b>Kumar picked up your order</b><span>8:02 PM · on the way</span></div>
          </div>
          <div class="t-item">
            <div style="position:relative;"><div class="t-dot"></div></div>
            <div class="t-body"><b>Delivered</b><span>Est. 8:14 PM</span></div>
          </div>
        </div>

        <div class="ticket-code">SHOW THIS CODE ON ARRIVAL<b>4 4 1 9</b></div>
        <div style="height:24px;"></div>
      </div>
      <div class="home-indicator"></div>
    </div>
  </div>

</div>

</body>
</html>
