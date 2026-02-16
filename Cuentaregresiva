<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="theme-color" content="#0b1020" />
  <title>Contagem regressiva ❤️</title>

  <!-- Luxon para fuso horário correto (iPhone) -->
  <script src="https://cdn.jsdelivr.net/npm/luxon@3/build/global/luxon.min.js"></script>

  <style>
    :root{
      --bg1:#0b1020;
      --bg2:#121a2f;
      --card: rgba(255,255,255,0.07);
      --stroke: rgba(255,255,255,0.10);
      --text: rgba(255,255,255,0.92);
      --muted: rgba(255,255,255,0.65);
      --accent: rgba(255,170,200,0.75); /* rosa suave */
      --heart: rgba(255,170,200,0.22);  /* corações bem sutis */
      --shadow: 0 18px 60px rgba(0,0,0,0.45);
      --radius: 18px;
    }

    *{ box-sizing:border-box; }
    body{
      margin:0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Inter, Helvetica, Arial, sans-serif;
      color:var(--text);
      min-height:100vh;
      background:
        radial-gradient(1100px 760px at 20% 10%, rgba(160,170,255,0.18), transparent 60%),
        radial-gradient(900px 650px at 85% 30%, rgba(255,170,200,0.14), transparent 60%),
        linear-gradient(160deg, var(--bg1), var(--bg2));
      padding:24px;
      display:flex;
      justify-content:center;
      align-items:flex-start;
      overflow-x:hidden;
    }

    /* Camada dos corações (não interfere no clique) */
    .hearts{
      position:fixed;
      inset:0;
      pointer-events:none;
      z-index:0;
      overflow:hidden;
    }

    .heart{
      position:absolute;
      bottom:-40px;
      left:10%;
      opacity:0;
      transform: translate3d(0,0,0) scale(1);
      will-change: transform, opacity, filter;
      filter: blur(0.2px);
      font-size: 14px;
      color: var(--heart);
      text-shadow: 0 0 14px rgba(255,170,200,0.10);
      animation: floatUp linear infinite;
    }

    /* Movimento: sobe, oscila um pouco, aparece e some */
    @keyframes floatUp{
      0%   { transform: translate3d(0, 0, 0) rotate(-6deg); opacity:0; }
      10%  { opacity:1; }
      50%  { transform: translate3d(var(--drift), -55vh, 0) rotate(6deg); opacity:0.85; }
      90%  { opacity:0.15; }
      100% { transform: translate3d(calc(var(--drift) * 1.2), -110vh, 0) rotate(10deg); opacity:0; }
    }

    /* Conteúdo por cima dos corações */
    .wrap{
      width:min(920px, 100%);
      margin-top:10px;
      position:relative;
      z-index:1;
    }

    .hero{
      border-radius: var(--radius);
      background: linear-gradient(180deg, rgba(255,255,255,0.10), rgba(255,255,255,0.05));
      border:1px solid var(--stroke);
      box-shadow: var(--shadow);
      padding:18px 18px 14px 18px;
      backdrop-filter: blur(10px);
    }

    .headline{
      margin:0;
      font-size:18px;
      letter-spacing:0.2px;
      display:flex;
      align-items:center;
      gap:10px;
    }
    .headline .dot{
      width:10px;height:10px;border-radius:99px;
      background: var(--accent);
      box-shadow: 0 0 18px rgba(255,170,200,0.35);
      display:inline-block;
      flex:0 0 auto;
    }

    .sub{
      margin:8px 0 0 0;
      font-size:13px;
      line-height:1.35;
      color:var(--muted);
    }

    .grid{
      display:grid;
      grid-template-columns: 1fr;
      gap:14px;
      margin-top:14px;
    }
    @media (min-width: 760px){
      .grid{ grid-template-columns: 1fr 1fr; }
      .card.wide{ grid-column: 1 / -1; }
    }

    .card{
      border-radius: var(--radius);
      background: rgba(255,255,255,0.06);
      border:1px solid var(--stroke);
      box-shadow: var(--shadow);
      padding:16px;
      backdrop-filter: blur(10px);
    }

    .kicker{
      font-size:12px;
      color:var(--muted);
      display:flex;
      align-items:center;
      gap:8px;
      margin-bottom:10px;
    }
    .kicker .line{
      height:1px; flex:1;
      background: rgba(255,255,255,0.10);
    }

    .title{
      margin:0;
      font-size:16px;
      letter-spacing:0.2px;
    }

    .date{
      margin-top:6px;
      font-size:12.5px;
      color: rgba(255,255,255,0.70);
      display:flex;
      gap:8px;
      flex-wrap:wrap;
      align-items:center;
    }
    .pill{
      display:inline-flex;
      align-items:center;
      gap:6px;
      padding:6px 10px;
      border-radius:999px;
      border:1px solid rgba(255,255,255,0.12);
      background: rgba(255,255,255,0.05);
    }
    .pill strong{ color: rgba(255,255,255,0.90); font-weight:600; }

    .time{
      margin-top:14px;
      display:grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap:10px;
    }

    .box{
      border-radius: 16px;
      border:1px solid rgba(255,255,255,0.10);
      background: linear-gradient(180deg, rgba(255,255,255,0.10), rgba(255,255,255,0.04));
      padding:12px 8px;
      text-align:center;
    }

    .num{
      margin:0;
      font-size:22px;
      font-weight:750;
      letter-spacing:0.8px;
    }

    .lab{
      margin-top:5px;
      font-size:10.5px;
      letter-spacing:0.6px;
      text-transform: uppercase;
      color: rgba(255,255,255,0.60);
    }

    .footer{
      margin-top:14px;
      text-align:center;
      color: rgba(255,255,255,0.60);
      font-size:12px;
      line-height:1.35;
    }
    .accent{ color: rgba(255,170,200,0.95); }
  </style>
</head>

<body>
  <!-- corações flutuando -->
  <div class="hearts" id="hearts"></div>

  <div class="wrap">
    <div class="hero">
      <p class="headline"><span class="dot"></span> Falta pouco para começar esta vida ao teu lado ❤️</p>
      <p class="sub">
        Contagens regressivas com horário de <strong>Primavera do Leste</strong>
        (<span class="accent">America/Cuiaba</span>).
      </p>
    </div>

    <div class="grid">
      <!-- Principal -->
      <div class="card wide" id="card-main">
        <div class="kicker">⏳ Contagem principal <span class="line"></span></div>
        <h2 class="title">Data limite</h2>
        <div class="date">
          <span class="pill">📍 Fuso: <strong>Primavera do Leste</strong></span>
          <span class="pill">🗓️ <strong>25/02/2026</strong> às <strong>15:00</strong></span>
        </div>

        <div class="time">
          <div class="box"><p class="num" id="main-d">--</p><div class="lab">Dias</div></div>
          <div class="box"><p class="num" id="main-h">--</p><div class="lab">Horas</div></div>
          <div class="box"><p class="num" id="main-m">--</p><div class="lab">Minutos</div></div>
          <div class="box"><p class="num" id="main-s">--</p><div class="lab">Segundos</div></div>
        </div>
      </div>

      <!-- Voo 1 -->
      <div class="card" id="card-f1">
        <div class="kicker">🛫 Voo <span class="line"></span></div>
        <h2 class="title">Primeiro voo Montevidéu - São Paulo</h2>
        <div class="date">
          <span class="pill">🗓️ <strong>25/02/2026</strong> às <strong>01:25</strong></span>
        </div>

        <div class="time">
          <div class="box"><p class="num" id="f1-d">--</p><div class="lab">Dias</div></div>
          <div class="box"><p class="num" id="f1-h">--</p><div class="lab">Horas</div></div>
          <div class="box"><p class="num" id="f1-m">--</p><div class="lab">Minutos</div></div>
          <div class="box"><p class="num" id="f1-s">--</p><div class="lab">Segundos</div></div>
        </div>
      </div>

      <!-- Voo 2 -->
      <div class="card" id="card-f2">
        <div class="kicker">🛬 Voo <span class="line"></span></div>
        <h2 class="title">Voo São Paulo - Cuiabá</h2>
        <div class="date">
          <span class="pill">🗓️ <strong>25/02/2026</strong> às <strong>03:50</strong></span>
        </div>

        <div class="time">
          <div class="box"><p class="num" id="f2-d">--</p><div class="lab">Dias</div></div>
          <div class="box"><p class="num" id="f2-h">--</p><div class="lab">Horas</div></div>
          <div class="box"><p class="num" id="f2-m">--</p><div class="lab">Minutos</div></div>
          <div class="box"><p class="num" id="f2-s">--</p><div class="lab">Segundos</div></div>
        </div>
      </div>
    </div>

    <div class="footer">
      Feito com carinho — Te amo, não importa quando você leia isso
    </div>
  </div>

<script>
  const { DateTime } = luxon;

  // Fuso Primavera do Leste / Cuiabá
  const ZONE = "America/Cuiaba";

  // Datas-alvo (25/02/2026)
  const targets = {
    main: DateTime.fromObject({ year: 2026, month: 2, day: 25, hour: 15, minute: 0, second: 0 }, { zone: ZONE }),
    f1:   DateTime.fromObject({ year: 2026, month: 2, day: 25, hour: 1,  minute: 25, second: 0 }, { zone: ZONE }),
    f2:   DateTime.fromObject({ year: 2026, month: 2, day: 25, hour: 3,  minute: 50, second: 0 }, { zone: ZONE }),
  };

  function pad2(n){ return String(n).padStart(2, "0"); }

  function render(prefix, totalSeconds){
    // Quando chegar a 0: fica em 0 (sem efeitos)
    const t = Math.max(0, Math.floor(totalSeconds));

    const days = Math.floor(t / (24*3600));
    const rem1 = t % (24*3600);
    const hours = Math.floor(rem1 / 3600);
    const rem2 = rem1 % 3600;
    const minutes = Math.floor(rem2 / 60);
    const seconds = rem2 % 60;

    document.getElementById(prefix + "-d").textContent = pad2(days);
    document.getElementById(prefix + "-h").textContent = pad2(hours);
    document.getElementById(prefix + "-m").textContent = pad2(minutes);
    document.getElementById(prefix + "-s").textContent = pad2(seconds);
  }

  function tick(){
    const now = DateTime.now().setZone(ZONE);
    const nowS = now.toSeconds();

    render("main", targets.main.toSeconds() - nowS);
    render("f1",   targets.f1.toSeconds()   - nowS);
    render("f2",   targets.f2.toSeconds()   - nowS);
  }

  // ---- Corações flutuando (minimalista) ----
  function makeHearts(){
    const root = document.getElementById("hearts");
    const heartsCount = 18; // quantidade sutil

    for(let i=0; i<heartsCount; i++){
      const h = document.createElement("div");
      h.className = "heart";
      h.textContent = "❤";

      // posição e estilo aleatórios (bem suaves)
      const left = Math.random() * 100;               // %
      const size = 10 + Math.random() * 16;           // px
      const duration = 10 + Math.random() * 12;       // s
      const delay = Math.random() * 10;               // s
      const drift = (-18 + Math.random() * 36).toFixed(2) + "px"; // oscilação lateral

      h.style.left = left.toFixed(2) + "%";
      h.style.fontSize = size.toFixed(0) + "px";
      h.style.animationDuration = duration.toFixed(2) + "s";
      h.style.animationDelay = (-delay).toFixed(2) + "s"; // já começa “rodando”
      h.style.setProperty("--drift", drift);

      // opacidade levemente variada
      h.style.opacity = "0";

      root.appendChild(h);
    }
  }

  makeHearts();
  tick();
  setInterval(tick, 1000);
</script>

</body>
</html>
