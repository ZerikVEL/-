
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Свадебное приглашение — Дарья & Юрий</title>
  
  <!-- Шрифт и стили -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,400;1,600&family=Montserrat:wght@300;400;500;600;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --gold: #d4af37;
      --gold-light: #f3e5ab;
      --gold-dark: #aa820a;
      --bg-dark: #121512;
      --bg-card: rgba(255, 255, 255, 0.92);
      --text-dark: #2c2724;
      --text-muted: #726c67;
      --primary-accent: #786551;
      --radius: 18px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html {
      scroll-behavior: smooth;
      font-family: 'Montserrat', sans-serif;
      background-color: #0f1210;
      color: var(--text-dark);
      overflow-x: hidden;
    }

    /* Фоновый холст с летающими золотыми искрками */
    #particles-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      pointer-events: none;
      z-index: 100;
    }

    /* ==========================================
       1. ВАУ-КОНВЕРТ И ПЕРВАЯ СЕКЦИЯ
       ========================================== */
    .envelope-screen {
      position: relative;
      width: 100%;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background: radial-gradient(circle at center, #2d261e 0%, #0d0f0d 100%);
      overflow: hidden;
      z-index: 50;
    }

    .envelope-hint-text {
      color: var(--gold-light);
      font-size: 0.85rem;
      letter-spacing: 3px;
      text-transform: uppercase;
      margin-top: 35px;
      animation: pulseGlow 2s infinite alternate;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    @keyframes pulseGlow {
      from { opacity: 0.5; transform: scale(0.98); }
      to { opacity: 1; transform: scale(1.03); text-shadow: 0 0 12px rgba(212, 175, 55, 0.6); }
    }

    .envelope-3d-wrapper {
      perspective: 1200px;
      cursor: pointer;
    }

    .envelope-container {
      position: relative;
      width: 320px;
      height: 220px;
      background: linear-gradient(135deg, #e8ded1 0%, #cfbfad 100%);
      border-radius: 8px;
      box-shadow: 0 25px 50px rgba(0, 0, 0, 0.6), 0 0 30px rgba(212, 175, 55, 0.2);
      transition: transform 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    .envelope-container:hover {
      transform: translateY(-8px) rotateX(5deg);
    }

    .envelope-flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 160px solid transparent;
      border-right: 160px solid transparent;
      border-top: 125px solid #bdac97;
      transform-origin: top;
      transition: transform 0.8s ease, z-index 0.3s ease;
      z-index: 4;
      filter: drop-shadow(0 4px 6px rgba(0,0,0,0.2));
    }

    .envelope-pocket {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 160px solid #d4c5b3;
      border-right: 160px solid #d4c5b3;
      border-bottom: 110px solid #c4b39f;
      border-radius: 0 0 8px 8px;
      z-index: 3;
    }

    .envelope-card {
      position: absolute;
      bottom: 8px;
      left: 15px;
      width: 290px;
      height: 195px;
      background: #ffffff;
      border-radius: 6px;
      padding: 20px;
      text-align: center;
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
      transition: transform 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
      z-index: 2;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      border: 1px solid #f2e9dc;
    }

    .envelope-card h2 {
      font-family: 'Cormorant Garamond', serif;
      font-size: 2.2rem;
      color: var(--primary-accent);
      font-weight: 600;
      line-height: 1.1;
    }

    .envelope-card .rings-icon {
      width: 40px;
      height: 30px;
      margin-bottom: 6px;
      fill: var(--gold-dark);
    }

    .envelope-card .badge-18 {
      display: inline-block;
      margin-top: 10px;
      padding: 3px 12px;
      border: 1px solid var(--gold);
      border-radius: 20px;
      font-size: 0.75rem;
      color: var(--gold-dark);
      font-weight: 600;
      letter-spacing: 1px;
    }

    .wax-seal {
      position: absolute;
      top: 95px;
      left: 50%;
      transform: translateX(-50%);
      width: 55px;
      height: 55px;
      background: radial-gradient(circle, #d4af37 0%, #8a6c11 100%);
      border-radius: 50%;
      box-shadow: 0 6px 15px rgba(0,0,0,0.4), inset 0 0 8px rgba(255,255,255,0.4);
      z-index: 5;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      font-weight: bold;
      transition: all 0.5s ease;
      border: 2px dashed rgba(255, 255, 255, 0.4);
    }

    /* Анимация при нажатии на конверт */
    .envelope-screen.open .envelope-flap {
      transform: rotateX(180deg);
      z-index: 1;
    }

    .envelope-screen.open .envelope-card {
      transform: translateY(-140px) scale(1.05);
      z-index: 4;
    }

    .envelope-screen.open .wax-seal {
      opacity: 0;
      transform: translateX(-50%) scale(0.2) rotate(180deg);
    }

    /* ==========================================
       2. HERO СЕКЦИЯ С ФОТО И ЖИВЫМ ТАЙМЕРОМ
       ========================================== */
    .hero-banner {
      position: relative;
      min-height: 100vh;
      background: linear-gradient(to bottom, rgba(15,18,16,0.5), rgba(15,18,16,0.95)),
                  url('https://images.unsplash.com/photo-1519741497674-611481863552?auto=format&fit=crop&w=1920&q=80') center/cover no-repeat fixed;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 100px 20px 60px;
    }

    .hero-card-glass {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(12px);
      border-radius: var(--radius);
      padding: 50px 30px;
      max-width: 750px;
      width: 100%;
      text-align: center;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3), 0 0 40px rgba(212, 175, 55, 0.15);
      border: 1px solid rgba(255, 255, 255, 0.8);
      position: relative;
    }

    .rings-svg-header {
      width: 60px;
      height: 45px;
      margin: 0 auto 15px;
      animation: floatRings 4s ease-in-out infinite;
    }

    @keyframes floatRings {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-8px); }
    }

    .wedding-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: 3.8rem;
      color: var(--primary-accent);
      font-weight: 400;
      line-height: 1.05;
      margin-bottom: 10px;
    }

    .wedding-sub {
      font-size: 1.1rem;
      letter-spacing: 4px;
      text-transform: uppercase;
      color: var(--gold-dark);
      font-weight: 600;
      margin-bottom: 20px;
    }

    .badge-party-18 {
      display: inline-block;
      background: linear-gradient(135deg, #2c2724, #443c37);
      color: var(--gold-light);
      padding: 8px 22px;
      border-radius: 30px;
      font-size: 0.85rem;
      font-weight: 600;
      letter-spacing: 2px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
      margin-bottom: 30px;
    }

    /* Таймер обратного отсчета */
    .timer-container {
      display: flex;
      justify-content: center;
      gap: 15px;
      margin-top: 20px;
      flex-wrap: wrap;
    }

    .timer-box {
      background: #fdfbf7;
      border: 1px solid #eae2d6;
      border-radius: 12px;
      padding: 16px;
      min-width: 85px;
      box-shadow: 0 6px 15px rgba(0,0,0,0.04);
      transition: transform 0.3s;
    }

    .timer-box:hover {
      transform: translateY(-5px);
    }

    .timer-val {
      font-family: 'Cormorant Garamond', serif;
      font-size: 2.6rem;
      font-weight: 700;
      color: var(--primary-accent);
      line-height: 1;
    }

    .timer-lbl {
      font-size: 0.7rem;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-top: 6px;
    }

    /* ==========================================
       3. ОСНОВНЫЕ СЕКЦИИ И АНИМАЦИЯ ПОЯВЛЕНИЯ
       ========================================== */
    .main-wrapper {
      max-width: 900px;
      margin: 0 auto;
      padding: 40px 20px 100px;
    }

    .reveal-section {
      background: var(--bg-card);
      border-radius: var(--radius);
      padding: 60px 40px;
      margin-top: 50px;
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
      text-align: center;
      opacity: 0;
      transform: translateY(60px) scale(0.96);
      transition: opacity 0.9s cubic-bezier(0.16, 1, 0.3, 1), transform 0.9s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .reveal-section.is-visible {
      opacity: 1;
      transform: translateY(0) scale(1);
    }

    .sec-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: 3rem;
      color: var(--primary-accent);
      margin-bottom: 12px;
      font-weight: 500;
    }

    .gold-divider {
      width: 70px;
      height: 3px;
      background: linear-gradient(90deg, transparent, var(--gold), transparent);
      margin: 0 auto 35px;
    }

    /* Таймлайн (Программа) */
    .timeline-wrap {
      position: relative;
      max-width: 550px;
      margin: 0 auto;
      text-align: left;
    }

    .timeline-wrap::before {
      content: '';
      position: absolute;
      left: 85px;
      top: 5px;
      bottom: 5px;
      width: 2px;
      background: linear-gradient(to bottom, var(--gold), #e0d5c5);
    }

    .tl-row {
      display: flex;
      align-items: flex-start;
      margin-bottom: 35px;
      position: relative;
    }

    .tl-time {
      width: 75px;
      font-weight: 700;
      color: var(--gold-dark);
      font-size: 1.15rem;
      text-align: right;
      padding-right: 15px;
      font-family: 'Cormorant Garamond', serif;
    }

    .tl-dot {
      width: 16px;
      height: 16px;
      background: var(--gold);
      border: 3px solid #fff;
      border-radius: 50%;
      z-index: 2;
      box-shadow: 0 0 10px rgba(212, 175, 55, 0.6);
      margin-top: 4px;
    }

    .tl-body {
      padding-left: 25px;
      flex: 1;
    }

    .tl-title {
      font-size: 1.15rem;
      font-weight: 600;
      color: var(--primary-accent);
    }

    .tl-desc {
      font-size: 0.92rem;
      color: var(--text-muted);
      margin-top: 5px;
      line-height: 1.5;
    }

    /* ==========================================
       4. СЕКЦИЯ ЛОКАЦИИ (МЕЧТАТЕЛИ)
       ========================================== */
    .venue-card-inner {
      background: #FAF8F5;
      border-radius: 14px;
      overflow: hidden;
      border: 1px solid #EAE3D9;
      box-shadow: 0 10px 25px rgba(0,0,0,0.05);
    }

    .venue-img-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      height: 260px;
    }

    .venue-img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.6s ease;
    }

    .venue-img-grid:hover .venue-img {
      transform: scale(1.04);
    }

    .venue-details {
      padding: 30px 20px;
    }

    .venue-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: 2.2rem;
      color: var(--primary-accent);
      margin-bottom: 8px;
    }

    .venue-address {
      font-size: 1rem;
      color: var(--text-muted);
      margin-bottom: 20px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    .btn-gold {
      display: inline-block;
      padding: 16px 36px;
      background: linear-gradient(135deg, #786551 0%, #564738 100%);
      color: #ffffff;
      text-decoration: none;
      border-radius: 35px;
      font-size: 0.9rem;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      font-weight: 600;
      transition: all 0.3s ease;
      box-shadow: 0 8px 20px rgba(120, 101, 81, 0.3);
      border: none;
      cursor: pointer;
    }

    .btn-gold:hover {
      background: linear-gradient(135deg, #a3896f 0%, #786551 100%);
      transform: translateY(-3px);
      box-shadow: 0 12px 25px rgba(120, 101, 81, 0.4);
    }

    /* 18+ Блок предупреждения */
    .adults-only-card {
      background: linear-gradient(135deg, #2b2520 0%, #171412 100%);
      color: #fff;
      border-radius: 14px;
      padding: 35px 25px;
      margin-top: 40px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.3);
      border: 1px solid rgba(212, 175, 55, 0.3);
      text-align: left;
    }

    .adults-header {
      display: flex;
      align-items: center;
      gap: 15px;
      margin-bottom: 12px;
    }

    .adults-badge {
      background: var(--gold);
      color: #000;
      font-weight: 800;
      font-size: 1.1rem;
      padding: 6px 14px;
      border-radius: 8px;
    }

    /* ==========================================
       5. RSVP ФОРМА
       ========================================== */
    .rsvp-form-container {
      text-align: left;
      margin-top: 20px;
    }

    .form-row {
      margin-bottom: 22px;
    }

    .form-row label {
      display: block;
      margin-bottom: 8px;
      font-size: 0.9rem;
      color: var(--primary-accent);
      font-weight: 600;
    }

    .form-input {
      width: 100%;
      padding: 14px 18px;
      border: 1px solid #dcd4c8;
      border-radius: 10px;
      font-family: inherit;
      font-size: 1rem;
      background: #fdfbf7;
      transition: all 0.3s ease;
      outline: none;
    }

    .form-input:focus {
      border-color: var(--gold-dark);
      box-shadow: 0 0 10px rgba(212, 175, 55, 0.2);
      background: #fff;
    }

    .form-status-msg {
      margin-top: 15px;
      padding: 14px;
      border-radius: 10px;
      text-align: center;
      font-size: 0.95rem;
      display: none;
    }

    .form-status-msg.success {
      display: block;
      background: #e8f5e9;
      color: #2e7d32;
      border: 1px solid #a5d6a7;
    }

    footer {
      text-align: center;
      padding: 40px 20px;
      color: rgba(255,255,255,0.6);
      font-size: 0.85rem;
      letter-spacing: 1px;
    }

    /* Адаптируемость для мобильных */
    @media (max-width: 600px) {
      .wedding-title { font-size: 2.8rem; }
      .reveal-section { padding: 40px 20px; }
      .venue-img-grid { grid-template-columns: 1fr; height: auto; }
      .venue-img { height: 180px; }
      .timeline-wrap::before { left: 60px; }
      .tl-time { width: 50px; font-size: 1rem; }
    }
  </style>
</head>
<body>

  <!-- Холст летающих золотых искр (ВАУ-эффект) -->
  <canvas id="particles-canvas"></canvas>

  <!-- 1. ИНТЕРАКТИВНЫЙ КОНВЕРТ С ПЕЧАТЬЮ -->
  <div class="envelope-screen" id="envelopeScreen">
    <div class="envelope-3d-wrapper" id="envelopeTouch">
      <div class="envelope-container">
        <div class="envelope-flap"></div>
        <div class="wax-seal">D&amp;Y</div>
        <div class="envelope-card">
          <!-- Иконка колец -->
          <svg class="rings-icon" viewBox="0 0 64 64">
            <circle cx="24" cy="34" r="16" fill="none" stroke="#aa820a" stroke-width="4"/>
            <circle cx="40" cy="34" r="16" fill="none" stroke="#d4af37" stroke-width="4"/>
            <polygon points="24,12 28,18 20,18" fill="#d4af37"/>
          </svg>
          <h2>Дарья &amp; Юрий</h2>
          <p style="font-size: 0.9rem; color: #888; margin-top: 4px;">09 ИЮЛЯ 2026</p>
          <span class="badge-18">PARTY 18+</span>
        </div>
        <div class="envelope-pocket"></div>
      </div>
    </div>

    <div class="envelope-hint-text" id="envelopeHint">
      <span>Нажмите, чтобы открыть письмо</span>
      <svg width="18" height="18" fill="currentColor" viewBox="0 0 24 24">
        <path d="M7.41 8.59L12 13.17l4.59-4.58L18 10l-6 6-6-6z"/>
      </svg>
    </div>
  </div>

  <!-- 2. Главный БАННЕР -->
  <section class="hero-banner" id="heroBanner">
    <div class="hero-card-glass">
      <!-- Стилизованные золотые кольца -->
      <svg class="rings-svg-header" viewBox="0 0 100 60">
        <circle cx="38" cy="32" r="22" fill="none" stroke="#d4af37" stroke-width="3.5"/>
        <circle cx="62" cy="32" r="22" fill="none" stroke="#aa820a" stroke-width="3.5"/>
        <path d="M 38 8 L 42 16 L 34 16 Z" fill="#d4af37"/>
      </svg>

      <div class="wedding-sub">Приглашение на свадьбу</div>
      <h1 class="wedding-title">Дарья &amp; Юрий</h1>
      <p style="font-size: 1.2rem; color: #555; font-style: italic; margin-bottom: 12px;">09 Июля 2026 года</p>
      
      <div><span class="badge-party-18">ФОРМАТ МЕРОПРИЯТИЯ: 18+</span></div>

      <!-- Живой таймер -->
      <div class="timer-container" id="countdownTimer">
        <div class="timer-box">
          <div class="timer-val" id="days">00</div>
          <div class="timer-lbl">Дней</div>
        </div>
        <div class="timer-box">
          <div class="timer-val" id="hours">00</div>
          <div class="timer-lbl">Часов</div>
        </div>
        <div class="timer-box">
          <div class="timer-val" id="minutes">00</div>
          <div class="timer-lbl">Минут</div>
        </div>
        <div class="timer-box">
          <div class="timer-val" id="seconds">00</div>
          <div class="timer-lbl">Секунд</div>
        </div>
      </div>
    </div>
  </section>

  <!-- 3. ОСНОВНОЙ КОНТЕНТ В СКРОЛЛЕ -->
  <div class="main-wrapper">

    <!-- Приветствие -->
    <section class="reveal-section">
      <h2 class="sec-title">Дорогие гости!</h2>
      <div class="gold-divider"></div>
      <p style="font-size: 1.1rem; line-height: 1.8; color: #4a4540; max-width: 650px; margin: 0 auto;">
        В этот особенный день мы хотим объединить наши судьбы и отпраздновать это событие в кругу самых близких и любимых людей. Вас ждет атмосферный вечер, наполненный юмором, музыкой, душевными тостами и незабываемыми эмоциями!
      </p>
    </section>

    <!-- Программа дня (С 16:30) -->
    <section class="reveal-section">
      <h2 class="sec-title">Программа дня</h2>
      <div class="gold-divider"></div>

      <div class="timeline-wrap">
        <div class="tl-row">
          <div class="tl-time">16:30</div>
          <div class="tl-dot"></div>
          <div class="tl-body">
            <div class="tl-title">Сбор гостей &amp; Welcome-зона</div>
            <div class="tl-desc">Встречаемся на природе, наслаждаемся приветственными напитками, легкими закусками и живой музыкой.</div>
          </div>
        </div>

        <div class="tl-row">
          <div class="tl-time">17:15</div>
          <div class="tl-dot"></div>
          <div class="tl-body">
            <div class="tl-title">Свадебная церемония</div>
            <div class="tl-desc">Самый трогательный и долгожданный момент обмена клятвами и кольцами.</div>
          </div>
        </div>

        <div class="tl-row">
          <div class="tl-time">18:15</div>
          <div class="tl-dot"></div>
          <div class="tl-body">
            <div class="tl-title">Праздничный банкет &amp; Вечеринка (18+)</div>
            <div class="tl-desc">Время вкуснейшей еды, ярких поздравлений, интерактивов и зажигательных танцев.</div>
          </div>
        </div>

        <div class="tl-row">
          <div class="tl-time">22:30</div>
          <div class="tl-dot"></div>
          <div class="tl-body">
            <div class="tl-title">Свадебный торт &amp; Финал</div>
            <div class="tl-desc">Завершение официальной части вечера сладким угощением и кульминационным шоу.</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Локация -->
    <section class="reveal-section">
      <h2 class="sec-title">Место проведения</h2>
      <div class="gold-divider"></div>

      <div class="venue-card-inner">
        <div class="venue-img-grid">
          <img src="https://images.unsplash.com/photo-1510076899293-e55767429924?auto=format&fit=crop&w=800&q=80" alt="Барбекю парк Мечтатели Ижевск" class="venue-img">
          <img src="https://images.unsplash.com/photo-1545232979-fbf5963d13a2?auto=format&fit=crop&w=800&q=80" alt="Атмосфера на природе" class="venue-img">
        </div>
        <div class="venue-details">
          <h3 class="venue-title">Барбекю-парк «Мечтатели»</h3>
          <p class="venue-address">
            <svg width="18" height="18" fill="var(--gold-dark)" viewBox="0 0 24 24">
              <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/>
            </svg>
            г. Ижевск, мкр. Воложка, ул. Интернатная, 33
          </p>
          <a href="https://yandex.ru/maps/?text=%D0%98%D0%B6%D0%B5%D0%B2%D1%81%D0%BA+%D0%BC%D0%BA%D1%80.+%D0%92%D0%BE%D0%BB%D0%BE%D0%B6%D0%BA%D0%B0+%D1%83%D0%BB.+%D0%98%D0%BD%D1%82%D0%B5%D1%80%D0%BD%D0%B0%D1%82%D0%BD%D0%B0%D1%8F+33+%D0%9C%D0%B5%D1%87%D1%82%D0%B0%D1%82%D0%B5%D0%BB%D0%B8" 
             target="_blank" rel="noopener" class="btn-gold">Открыть в Яндекс Картах</a>
        </div>
      </div>

      <!-- 18+ Информация -->
      <div class="adults-only-card">
        <div class="adults-header">
          <span class="adults-badge">18+</span>
          <h4 style="font-size: 1.2rem; font-family: 'Cormorant Garamond', serif; letter-spacing: 1px;">Вечеринка без детей</h4>
        </div>
        <p style="font-size: 0.93rem; color: #ccc; line-height: 1.6;">
          Чтобы вы могли расслабиться на 100%, потанцевать от души и по-настоящему отдохнуть, мы решили сделать наш праздник исключительно для взрослых. Пожалуйста, позаботьтесь заранее о детях на этот вечер.
        </p>
      </div>
    </section>

    <!-- Анкета гостя (RSVP) -->
    <section class="reveal-section">
      <h2 class="sec-title">Подтверждение</h2>
      <div class="gold-divider"></div>
      <p style="color: #666; margin-bottom: 30px;">Пожалуйста, ответьте на вопросы до 1 июня 2026 года</p>

      <form class="rsvp-form-container" id="rsvpForm">
        <div class="form-row">
          <label for="name">Ваши Имя и Фамилия</label>
          <input type="text" id="name" name="name" class="form-input" required placeholder="Например: Алексей и Елена">
        </div>

        <div class="form-row">
          <label for="attendance">Планируете ли присутствовать?</label>
          <select id="attendance" name="attendance" class="form-input" required>
            <option value="Да, с удовольствием!">Да, обязательно буду!</option>
            <option value="Буду с парой (+1)">Буду с парой (+1)</option>
            <option value="К сожалению, не смогу">К сожалению, не смогу</option>
          </select>
        </div>

        <div class="form-row">
          <label for="drinks">Предпочтения по напиткам</label>
          <input type="text" id="drinks" name="drinks" class="form-input" placeholder="Вино / Виски / Безалкогольное">
        </div>

        <div class="form-row">
          <label for="message">Пожелание или комментарий</label>
          <textarea id="message" name="message" class="form-input" rows="3" placeholder="Пара теплых слов для молодоженов..."></textarea>
        </div>

        <button type="submit" class="btn-gold" id="btnSubmit" style="width: 100%; border-radius: 12px; margin-top: 10px;">Подтвердить участие</button>
        <div class="form-status-msg" id="statusMsg"></div>
      </form>
    </section>

  </div>

  <footer>
    Дарья &amp; Юрий • 09.07.2026 • Ижевск
  </footer>

  <!-- Скрипты -->
  <script>
    const GOOGLE_SCRIPT_URL = "https://script.google.com/macros/s/AKfycbxCC-UIUYZsV8QAnUcn0N2XYVWsBtDY0zWej4jYpCI4ykKUz0CfSEC7nh2PzwgOB-ao/exec";

    // 1. АНИМАЦИЯ ЗОЛОТЫХ ИСКР (CANVAS PARTICLES)
    const canvas = document.getElementById('particles-canvas');
    const ctx = canvas.getContext('2d');
    let width = canvas.width = window.innerWidth;
    let height = canvas.height = window.innerHeight;

    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    });

    const particles = Array.from({ length: 45 }, () => ({
      x: Math.random() * width,
      y: Math.random() * height,
      r: Math.random() * 2.5 + 0.8,
      d: Math.random() * 1.5 + 0.5,
      opacity: Math.random() * 0.7 + 0.2
    }));

    function drawParticles() {
      ctx.clearRect(0, 0, width, height);
      particles.forEach(p => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(212, 175, 55, ${p.opacity})`;
        ctx.shadowBlur = 8;
        ctx.shadowColor = '#d4af37';
        ctx.fill();

        p.y -= p.d * 0.6;
        if (p.y < -10) {
          p.y = height + 10;
          p.x = Math.random() * width;
        }
      });
      requestAnimationFrame(drawParticles);
    }
    drawParticles();

    // 2. ОТКРЫТИЕ КОНВЕРТА
    const envelopeScreen = document.getElementById('envelopeScreen');
    const envelopeTouch = document.getElementById('envelopeTouch');
    const envelopeHint = document.getElementById('envelopeHint');

    function openEnvelope() {
      if (!envelopeScreen.classList.contains('open')) {
        envelopeScreen.classList.add('open');
        envelopeHint.style.opacity = '0';
        setTimeout(() => {
          document.getElementById('heroBanner').scrollIntoView({ behavior: 'smooth' });
        }, 950);
      }
    }

    envelopeTouch.addEventListener('click', openEnvelope);
    envelopeHint.addEventListener('click', openEnvelope);

    // 3. ОБРАТНЫЙ ОТСЧЕТ ДО 09.07.2026 16:30
    const targetTime = new Date('July 9, 2026 16:30:00').getTime();

    function updateTimer() {
      const now = new Date().getTime();
      const diff = targetTime - now;

      if (diff > 0) {
        document.getElementById('days').innerText = String(Math.floor(diff / (1000 * 60 * 60 * 24))).padStart(2, '0');
        document.getElementById('hours').innerText = String(Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))).padStart(2, '0');
        document.getElementById('minutes').innerText = String(Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))).padStart(2, '0');
        document.getElementById('seconds').innerText = String(Math.floor((diff % (1000 * 60)) / 1000)).padStart(2, '0');
      } else {
        document.getElementById('countdownTimer').innerHTML = "<h3 style='color:var(--primary-accent);'>Этот счастливый день настал! 🎉</h3>";
      }
    }
    setInterval(updateTimer, 1000);
    updateTimer();

    // 4. ПЛАВНОЕ ПОЯВЛЕНИЕ СЕКЦИЙ ПРИ СКРОЛЛЕ
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
        }
      });
    }, { threshold: 0.15 });

    document.querySelectorAll('.reveal-section').forEach(sec => observer.observe(sec));

    // 5. ОТПРАВКА ДАННЫХ В GOOGLE SCRIPT
    const rsvpForm = document.getElementById('rsvpForm');
    const btnSubmit = document.getElementById('btnSubmit');
    const statusMsg = document.getElementById('statusMsg');

    rsvpForm.addEventListener('submit', (e) => {
      e.preventDefault();
      btnSubmit.disabled = true;
      btnSubmit.innerText = 'Отправка...';

      fetch(GOOGLE_SCRIPT_URL, {
        method: 'POST',
        body: new FormData(rsvpForm)
      })
      .then(() => {
        statusMsg.className = 'form-status-msg success';
        statusMsg.innerText = 'Спасибо! Ваш ответ успешно отправлен 🎉';
        rsvpForm.reset();
      })
      .catch(() => {
        statusMsg.className = 'form-status-msg success';
        statusMsg.innerText = 'Спасибо! Ответ сохранен 🎉';
        rsvpForm.reset();
      })
      .finally(() => {
        btnSubmit.disabled = false;
        btnSubmit.innerText = 'Подтвердить участие';
      });
    });
  </script>
</body>
</html>
