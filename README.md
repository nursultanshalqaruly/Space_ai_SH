# Space_ai_SH
Space_ai_SH for "Ғылым әлемін ашамыз"
<!DOCTYPE html>
<html lang="kk">
<head>
  <meta charset="UTF-8" />
  <title>SpaceAI – Ғарыш қоқысын бақылау</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: radial-gradient(circle at top, #0b1220, #020617);
      color: #e5e7eb;
      line-height: 1.6;
    }
    a { color: inherit; text-decoration: none; }
    .container { max-width: 1100px; margin: 0 auto; padding: 0 1.5rem; }

    header {
      position: sticky;
      top: 0;
      z-index: 50;
      backdrop-filter: blur(16px);
      background: rgba(15, 23, 42, 0.85);
      border-bottom: 1px solid rgba(148, 163, 184, 0.3);
    }
    header .inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0.9rem 0;
    }
    .logo {
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      font-size: 0.9rem;
      color: #38bdf8;
    }
    nav a { margin-left: 1.5rem; font-size: 0.9rem; color: #9ca3af; }
    nav a:hover { color: #e5e7eb; }

    .btn-primary {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      padding: 0.7rem 1.4rem;
      border-radius: 999px;
      background: linear-gradient(to right, #38bdf8, #6366f1);
      color: #0b1120;
      font-weight: 600;
      border: none;
      cursor: pointer;
      font-size: 0.95rem;
      margin-top: 1.2rem;
      box-shadow: 0 18px 45px rgba(37, 99, 235, 0.5);
    }
    .btn-primary:hover {
      filter: brightness(1.1);
      transform: translateY(-1px);
    }

    .hero {
      padding: 4.5rem 0 3rem;
      display: grid;
      grid-template-columns: minmax(0, 1.2fr) minmax(0, 1fr);
      gap: 3rem;
      align-items: center;
    }
    .hero-kicker { font-size: 0.85rem; color: #a5b4fc; text-transform: uppercase; letter-spacing: 0.15em; margin-bottom: 0.9rem; }
    .hero-title {
      font-size: clamp(2.2rem, 4vw, 3rem);
      font-weight: 800;
      margin-bottom: 1rem;
    }
    .hero-title span { color: #38bdf8; }
    .hero-sub {
      color: #9ca3af;
      max-width: 34rem;
      font-size: 0.98rem;
    }
    .hero-meta {
      display: flex;
      flex-wrap: wrap;
      gap: 1.5rem;
      margin-top: 2rem;
      font-size: 0.8rem;
      color: #9ca3af;
    }
    .hero-meta div strong { display: block; color: #e5e7eb; font-size: 0.9rem; }

    .hero-visual {
      position: relative;
      min-height: 260px;
      border-radius: 1.5rem;
      border: 1px solid rgba(148, 163, 184, 0.4);
      background: radial-gradient(circle at top, rgba(56,189,248,.16), rgba(15,23,42,1));
      overflow: hidden;
      box-shadow: 0 30px 80px rgba(15,23,42,0.8);
    }
    .orbit {
      position: absolute;
      border-radius: 999px;
      border: 1px dashed rgba(148, 163, 184, 0.4);
      inset: 16% 12%;
    }
    .orbit:nth-child(2) { inset: 27% 20%; opacity: 0.7; }
    .orbit:nth-child(3) { inset: 38% 30%; opacity: 0.5; }
    .planet {
      position: absolute;
      top: 50%; left: 50%;
      width: 70px; height: 70px;
      margin: -35px;
      border-radius: 999px;
      background: radial-gradient(circle at 30% 30%, #f9fafb, #38bdf8 40%, #0f172a);
      box-shadow: 0 0 40px rgba(56,189,248,0.4);
    }
    .sat {
      position: absolute;
      width: 10px; height: 10px;
      border-radius: 999px;
      background: #38bdf8;
      box-shadow: 0 0 12px rgba(56,189,248,0.9);
      animation: orbit 10s linear infinite;
    }
    .sat:nth-child(5) { animation-duration: 14s; background: #22c55e; }
    .sat:nth-child(6) { animation-duration: 18s; background: #f97316; }
    @keyframes orbit {
      from { transform: rotate(0deg) translateX(150px) rotate(0deg); }
      to   { transform: rotate(360deg) translateX(150px) rotate(-360deg); }
    }

    section { padding: 3rem 0; }
    h2 {
      font-size: 1.6rem;
      margin-bottom: 1.5rem;
      font-weight: 700;
    }
    .grid-3 {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 1.5rem;
    }
    .card {
      background: rgba(15, 23, 42, 0.9);
      border-radius: 1rem;
      padding: 1.4rem;
      border: 1px solid rgba(148, 163, 184, 0.35);
    }
    .card h3 { font-size: 1.02rem; margin-bottom: 0.4rem; }
    .card p { font-size: 0.9rem; color: #9ca3af; }

    .problem-list li {
      margin-bottom: 0.4rem;
      font-size: 0.95rem;
      color: #9ca3af;
    }

    .demo-layout {
      display: grid;
      grid-template-columns: minmax(0, 1.4fr) minmax(0, 1fr);
      gap: 2rem;
      align-items: stretch;
    }
    .space-map {
      border-radius: 1.3rem;
      border: 1px solid rgba(148, 163, 184, 0.4);
      background: radial-gradient(circle at center, #020617, #020617);
      position: relative;
      overflow: hidden;
      padding: 1rem;
    }
    .space-map-inner {
      width: 100%;
      height: 260px;
      position: relative;
      background:
        radial-gradient(circle at 10% 20%, rgba(56, 189, 248, 0.16), transparent 55%),
        radial-gradient(circle at 90% 80%, rgba(96, 165, 250, 0.18), transparent 55%),
        #020617;
    }
    .map-object {
      position: absolute;
      border-radius: 999px;
      width: 12px; height: 12px;
      background: #f97316;
      box-shadow: 0 0 14px rgba(249, 115, 22, .9);
      cursor: pointer;
      transition: transform 0.15s ease, box-shadow 0.15s ease;
    }
    .map-object.selected {
      transform: scale(1.2);
      box-shadow: 0 0 24px rgba(56, 189, 248, 1);
      background: #38bdf8;
    }
    .map-caption {
      margin-top: 0.7rem;
      font-size: 0.8rem;
      color: #9ca3af;
    }

    .object-panel {
      background: rgba(15, 23, 42, 0.9);
      border-radius: 1.3rem;
      padding: 1.2rem 1.4rem;
      border: 1px solid rgba(148,163,184,0.4);
      display: flex;
      flex-direction: column;
      gap: 0.7rem;
      font-size: 0.9rem;
    }
    .object-list button {
      width: 100%;
      text-align: left;
      padding: 0.5rem 0.6rem;
      border-radius: 0.7rem;
      border: 1px solid transparent;
      background: transparent;
      color: #e5e7eb;
      cursor: pointer;
      font-size: 0.9rem;
    }
    .object-list button:hover {
      background: rgba(30,64,175,0.5);
      border-color: rgba(129,140,248,0.7);
    }
    .object-list button.active {
      background: rgba(37,99,235,0.6);
      border-color: rgba(191, 219, 254, 0.9);
    }
    .object-detail {
      margin-top: 0.5rem;
      padding-top: 0.7rem;
      border-top: 1px solid rgba(55,65,81,0.8);
      color: #9ca3af;
    }
    .object-detail strong { color: #e5e7eb; }

    .benefits {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 1.3rem;
      font-size: 0.9rem;
    }
    .benefit-tag {
      display: inline-block;
      font-size: 0.75rem;
      padding: 0.2rem 0.5rem;
      border-radius: 999px;
      background: rgba(55, 65, 81, 0.8);
      margin-bottom: 0.4rem;
      color: #e5e7eb;
    }

    .contact {
      background: radial-gradient(circle at top, rgba(56,189,248,0.18), rgba(15,23,42,1));
      border-radius: 1.5rem;
      padding: 1.8rem 1.7rem 1.9rem;
      border: 1px solid rgba(148,163,184,0.5);
      display: grid;
      grid-template-columns: minmax(0, 1.2fr) minmax(0, 1fr);
      gap: 2rem;
      align-items: center;
    }
    .contact p { font-size: 0.9rem; color: #9ca3af; margin-top: 0.3rem; }
    form { display: grid; gap: 0.7rem; }
    label { font-size: 0.8rem; color: #9ca3af; }
    input, textarea {
      width: 100%;
      background: rgba(15, 23, 42, 0.9);
      border-radius: 0.6rem;
      border: 1px solid rgba(55, 65, 81, 0.9);
      padding: 0.5rem 0.6rem;
      color: #e5e7eb;
      font-size: 0.9rem;
    }
    textarea { min-height: 80px; resize: vertical; }

    footer {
      padding: 1.8rem 0 2.2rem;
      font-size: 0.8rem;
      color: #6b7280;
      text-align: center;
    }

    @media (max-width: 900px) {
      .hero, .demo-layout, .contact {
        grid-template-columns: minmax(0, 1fr);
      }
      .hero { padding-top: 3.2rem; }
      .grid-3, .benefits {
        grid-template-columns: minmax(0, 1fr);
      }
      header .inner { flex-direction: column; align-items: flex-start; gap: 0.5rem; }
      nav a { margin-left: 0.8rem; }
    }
  </style>
</head>
<body>
  <header>
    <div class="container inner">
      <div class="logo">SpaceAI Monitor</div>
      <nav>
        <a href="#problem">Мәселе</a>
        <a href="#solution">Шешім</a>
        <a href="#demo">Демо</a>
        <a href="#contact">Байланыс</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="hero container">
      <div>
        <div class="hero-kicker">Ғарыш қоқысын ЖИ арқылы бақылау</div>
        <h1 class="hero-title">
          <span>Жасанды интеллект</span> көмегімен орбитадағы қауіптерді ерте анықтаңыз
        </h1>
        <p class="hero-sub">
          SpaceAI Monitor – жер маңындағы орбитадағы спутниктер мен ғарыш қоқыстарының траекториясын 
          болжайтын және соқтығысу қаупін автоматты түрде есептейтін аналитикалық платформа.
        </p>
        <button class="btn-primary" onclick="document.getElementById('demo').scrollIntoView({behavior:'smooth'})">
          Онлайн демоны көру
        </button>
        <div class="hero-meta">
          <div>
            <strong>100k+</strong>
            бақылауға алынған ғарыш нысандары
          </div>
          <div>
            <strong>Тәулігіне 24/7</strong>
            нақты уақыттағы деректерді өңдеу
          </div>
          <div>
            <strong>ЖИ-предиктивті модельдер</strong>
            уақыттық қатарлар мен anomaly detection
          </div>
        </div>
      </div>
      <div class="hero-visual">
        <div class="orbit"></div>
        <div class="orbit"></div>
        <div class="orbit"></div>
        <div class="planet"></div>
        <div class="sat" style="top:50%;left:50%;"></div>
        <div class="sat" style="top:50%;left:50%;"></div>
        <div class="sat" style="top:50%;left:50%;"></div>
      </div>
    </section>

    <section id="problem">
      <div class="container">
        <h2>Ғарыш қоқысы неге өзекті мәселе?</h2>
        <p style="color:#9ca3af; max-width:40rem; font-size:0.95rem; margin-bottom:1rem;">
          Жер маңындағы орбитада ондаған мың спутник, пайдаланылмаған ракеталық сатылар және фрагменттер 
          айналып жүр. Әрбір жаңа соқтығысу жүздеген жаңа қоқыс бөлігін тудырып, Kessler синдромына 
          әкелуі мүмкін.
        </p>
        <ul class="problem-list">
          <li>• Орбитадағы объектілер саны қарқынды өсуде, қолмен мониторинг жүргізу мүмкін емес.</li>
          <li>• Шағын фрагменттердің өзі жұмыс істеп тұрған спутникке айтарлықтай зақым келтіреді.</li>
          <li>• Ғылыми миссиялар мен байланыс спутниктерінің жұмысы тоқтауы мүмкін.</li>
          <li>• Жаңа миссиялар үшін қауіпсіз орбиталарды жоспарлау қиындай түсуде.</li>
        </ul>
      </div>
    </section>

    <section id="solution">
      <div class="container">
        <h2>ЖИ негізіндегі шешіміміз</h2>
        <p style="color:#9ca3af; max-width:40rem; font-size:0.95rem; margin-bottom:1.2rem;">
          SpaceAI Monitor классикалық орбиталық механиканы деректерге негізделген ЖИ-модельдерімен 
          біріктіріп, қауіпті траекторияларды ерте анықтайды.
        </p>
        <div class="grid-3">
          <div class="card">
            <h3>Орбита болжамы</h3>
            <p>LSTM/Transformer-type уақыттық қатарлар модельдері орбиталардың эволюциясын болжайды, 
               атмосфералық кедергілер мен гравитациялық әсерлерді ескере отырып.</p>
          </div>
          <div class="card">
            <h3>Қауіпті жұптарды табу</h3>
            <p>Anomaly detection және risk scoring алгоритмдері ықтимал соқтығысуы бар нысандарды автоматты түрде
               бөліп көрсетеді.</p>
          </div>
          <div class="card">
            <h3>Ескерту және визуализация</h3>
            <p>Интерактивті карта мен ескерту жүйесі операторларға тәуекелі жоғары аймақтарды жылдам бағалауға көмектеседі.</p>
          </div>
        </div>
      </div>
    </section>

    <section id="demo">
      <div class="container">
        <h2>Интерактивті демо: ғарыш нысандарын шолу</h2>
        <p style="color:#9ca3af; max-width:40rem; font-size:0.95rem; margin-bottom:1.2rem;">
          Төмендегі қарапайым демо арқылы бірнеше жасанды спутник пен ғарыш қоқысы объектілерін таңдап, 
          олардың сипаттамасын көре аласыз.
        </p>
        <div class="demo-layout">
          <div class="space-map">
            <div class="space-map-inner" id="spaceMap">
              <!-- Объекттер JS арқылы қосылады -->
            </div>
            <div class="map-caption">
              Объектіні картадан немесе тізімнен таңдаңыз. ЖИ жүйесінде осындай мыңдаған нысандар нақты уақыт режимінде бақыланады.
            </div>
          </div>
          <div class="object-panel">
            <div style="font-weight:600;">Нысандар тізімі</div>
            <div class="object-list" id="objectList"></div>
            <div class="object-detail" id="objectDetail">
              Нысанды таңдап, оның түрін, орбитасын және қауіптілік деңгейін көріңіз.
            </div>
          </div>
        </div>
      </div>
    </section>

    <section>
      <div class="container">
        <h2>Кімдер үшін пайдалы?</h2>
        <div class="benefits">
          <div class="card">
            <div class="benefit-tag">Спутник операторлары</div>
            <p>Жұмыс істеп тұрған спутниктерді соқтығысу қаупінен қорғап, қызмет мерзімін ұзартады.</p>
          </div>
          <div class="card">
            <div class="benefit-tag">Ғылыми ұйымдар</div>
            <p>Зерттеу аппараттары мен телескоптардың орбитадағы қауіпсіздігін арттырады, деректер жоғалту 
               тәуекелін азайтады.</p>
          </div>
          <div class="card">
            <div class="benefit-tag">Мемлекеттік агенттіктер</div>
            <p>Space sustainability саясатын қолдап, ғарыш қоқысын басқару бойынша ұлттық стратегияларды
               негіздеуге көмектеседі.</p>
          </div>
        </div>
      </div>
    </section>

    <section id="contact">
      <div class="container">
        <div class="contact">
          <div>
            <h2>Жобаны дамытуға атсалысқыңыз келе ме?</h2>
            <p>
              SpaceAI Monitor – ғылыми-зерттеу және оқу мақсаттарына арналған концептуалды платформа. 
              Егер бірлесіп жұмыс істеуге немесе осындай жүйені оқу/жобалық жұмыс ретінде дамытуға қызықсаңыз,
              байланыс формасын толтырыңыз.
            </p>
          </div>
          <form onsubmit="event.preventDefault(); alert('Хабарыңызға рахмет! (демо)');">
            <div>
              <label for="name">Аты-жөніңіз</label>
              <input id="name" type="text" placeholder="Аты-жөніңіз" required />
            </div>
            <div>
              <label for="email">E-mail</label>
              <input id="email" type="email" placeholder="you@example.com" required />
            </div>
            <div>
              <label for="msg">Хабарлама</label>
              <textarea id="msg" placeholder="Қысқаша жазыңыз..."></textarea>
            </div>
            <button class="btn-primary" type="submit">Хабар жіберу</button>
          </form>
        </div>
      </div>
    </section>
  </main>

  <footer>
    © 2026 SpaceAI Monitor. Оқу және демонстрациялық мақсаттарға арналған концепт.
  </footer>

  <script>
    const objects = [
      {
        id: 'sat1',
        name: 'KazSat-AI',
        type: 'Байланыс спутнигі',
        orbit: 'GEO-like (қысқартылған мысал)',
        risk: 'Төмен',
        desc: 'Ұлттық байланыс қызметтерін қамтамасыз ететін геостационарлық орбитадағы демонстрациялық спутник.'
      },
      {
        id: 'sat2',
        name: 'ResearchCube-1',
        type: 'CubeSat (ғылыми)',
        orbit: 'LEO, 500 км, 97°',
        risk: 'Орташа',
        desc: 'Атмосфераның жоғарғы қабаттарын зерттейтін шағын ғылыми аппарат.'
      },
      {
        id: 'debris1',
        name: 'Debris-Fragment-2026-01',
        type: 'Ғарыш қоқысы (фрагмент)',
        orbit: 'LEO, 780 км, 98°',
        risk: 'Жоғары',
        desc: 'Бұрынғы соқтығысу нәтижесінде пайда болған фрагмент; жақын маңдағы CubeSat-тар үшін қауіпті.'
      },
      {
        id: 'rocket1',
        name: 'UpperStage-Old',
        type: 'Ракетаның соңғы сатысы',
        orbit: 'MEO, эллипстік',
        risk: 'Орташа',
        desc: 'Отынсыз қалған соңғы саты, реттелмеген орбитада баяу ыдырауда.'
      }
    ];

    const positions = {
      sat1: { top: '32%', left: '60%' },
      sat2: { top: '65%', left: '40%' },
      debris1: { top: '45%', left: '25%' },
      rocket1: { top: '20%', left: '30%' }
    };

    const mapEl = document.getElementById('spaceMap');
    const listEl = document.getElementById('objectList');
    const detailEl = document.getElementById('objectDetail');
    let selectedId = null;

    function renderObjects() {
      objects.forEach(obj => {
        const dot = document.createElement('div');
        dot.className = 'map-object';
        dot.style.top = positions[obj.id].top;
        dot.style.left = positions[obj.id].left;
        dot.dataset.id = obj.id;
        dot.title = obj.name;
        dot.addEventListener('click', () => selectObject(obj.id));
        mapEl.appendChild(dot);

        const btn = document.createElement('button');
        btn.textContent = obj.name + ' – ' + obj.type;
        btn.dataset.id = obj.id;
        btn.addEventListener('click', () => selectObject(obj.id));
        listEl.appendChild(btn);
      });
    }

    function selectObject(id) {
      selectedId = id;
      const obj = objects.find(o => o.id === id);
      if (!obj) return;
      document.querySelectorAll('.map-object').forEach(el => {
        el.classList.toggle('selected', el.dataset.id === id);
      });
      document.querySelectorAll('.object-list button').forEach(el => {
        el.classList.toggle('active', el.dataset.id === id);
      });
      detailEl.innerHTML = `
        <strong>${obj.name}</strong><br/>
        Түрі: ${obj.type}<br/>
        Орбитасы: ${obj.orbit}<br/>
        Қауіптілік деңгейі: ${obj.risk}<br/><br/>
        ${obj.desc}
      `;
    }

    renderObjects();
    selectObject('debris1');
  </script>
</body>
</html>
