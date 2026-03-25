<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>경도를 기다리며 — 행사 기획 발표</title>
<link href="https://fonts.googleapis.com/css2?family=Gowun+Dodum&family=Black+Han+Sans&family=Noto+Sans+KR:wght@400;700;900&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;
    --card: #161b22;
    --accent1: #f7c948;
    --accent2: #ff6b6b;
    --accent3: #4ecdc4;
    --accent4: #a29bfe;
    --text: #e6edf3;
    --muted: #8b949e;
    --border: #30363d;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Noto Sans KR', sans-serif;
    background: var(--bg);
    color: var(--text);
    overflow: hidden;
    height: 100vh;
    width: 100vw;
  }

  .slide {
    display: none;
    position: absolute;
    inset: 0;
    padding: 48px 64px;
    flex-direction: column;
    justify-content: center;
    animation: fadeIn 0.45s ease;
    overflow: hidden;
  }
  .slide.active { display: flex; }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(18px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .slide-0 { background: radial-gradient(ellipse at 30% 50%, #1a2744 0%, #0d1117 70%); }
  .slide-1 { background: radial-gradient(ellipse at 70% 30%, #1f1b2e 0%, #0d1117 70%); }
  .slide-2 { background: radial-gradient(ellipse at 20% 70%, #0e2018 0%, #0d1117 70%); }
  .slide-3 { background: radial-gradient(ellipse at 80% 60%, #1f1209 0%, #0d1117 70%); }
  .slide-4 { background: radial-gradient(ellipse at 50% 20%, #0c1a2a 0%, #0d1117 70%); }
  .slide-5 { background: radial-gradient(ellipse at 40% 70%, #1a0f2e 0%, #0d1117 70%); }

  .dot-grid {
    position: absolute; inset: 0;
    background-image: radial-gradient(circle, rgba(255,255,255,0.04) 1px, transparent 1px);
    background-size: 32px 32px;
    pointer-events: none;
  }
  .glow {
    position: absolute; border-radius: 50%;
    pointer-events: none; opacity: 0.11; filter: blur(80px);
  }
  .g1 { width:400px;height:400px;background:var(--accent1);top:-100px;right:-100px; }
  .g2 { width:300px;height:300px;background:var(--accent2);bottom:-80px;left:-80px; }
  .g3 { width:350px;height:350px;background:var(--accent3);top:50%;right:20%; }
  .g4 { width:350px;height:350px;background:var(--accent4);bottom:10%;left:30%; }
  .g5 { width:400px;height:400px;background:#a29bfe;top:0;right:10%; }

  .nav {
    position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%);
    display: flex; gap: 10px; z-index: 100;
  }
  .nav button {
    background: var(--card); border: 1px solid var(--border); color: var(--text);
    padding: 9px 26px; border-radius: 999px;
    font-family: 'Noto Sans KR', sans-serif; font-size: 13px;
    cursor: pointer; transition: all 0.2s;
  }
  .nav button:hover { background: var(--accent1); color: #000; border-color: var(--accent1); }

  .dot-nav {
    position: fixed; bottom: 68px; left: 50%; transform: translateX(-50%);
    display: flex; gap: 8px; z-index: 99;
  }
  .dot-nav span {
    width: 7px; height: 7px; border-radius: 50%;
    background: var(--border); cursor: pointer; transition: all 0.3s;
  }
  .dot-nav span.on { background: var(--accent1); transform: scale(1.4); }

  .slide-num {
    position: fixed; bottom: 28px; right: 40px;
    font-size: 12px; color: var(--muted); letter-spacing: 2px; z-index: 100;
  }
  .keyboard-hint {
    position: fixed; top: 20px; right: 24px;
    font-size: 11px; color: var(--muted); z-index: 100;
  }

  .section-tag {
    font-size: 11px; letter-spacing: 3px; color: var(--accent3);
    text-transform: uppercase; margin-bottom: 6px; font-weight: 700;
  }
  .section-title {
    font-family: 'Black Han Sans', sans-serif;
    font-size: clamp(32px, 4.5vw, 52px); margin-bottom: 28px; color: var(--text);
  }

  /* SLIDE 0 */
  .title-badge {
    display: inline-block; background: var(--accent1); color: #000;
    font-size: 12px; font-weight: 700; padding: 4px 14px; border-radius: 999px;
    letter-spacing: 2px; margin-bottom: 18px; width: fit-content;
  }
  .title-main {
    font-family: 'Black Han Sans', sans-serif;
    font-size: clamp(52px, 8vw, 96px); line-height: 1.05; letter-spacing: -2px;
    background: linear-gradient(135deg, #f7c948, #ff6b6b, #4ecdc4);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .title-sub { font-size: 17px; color: var(--muted); margin-top: 14px; }
  .title-meta { display: flex; gap: 32px; margin-top: 44px; }
  .meta-item  { display: flex; flex-direction: column; gap: 4px; }
  .meta-label { font-size: 10px; color: var(--muted); letter-spacing: 2px; text-transform: uppercase; }
  .meta-value { font-size: 16px; font-weight: 700; }
  .title-emoji {
    position: absolute; right: 80px; top: 50%; transform: translateY(-50%);
    font-size: 96px; line-height: 1.3; text-align: center;
    animation: float 4s ease-in-out infinite;
    filter: drop-shadow(0 0 40px rgba(247,201,72,0.3));
  }
  @keyframes float {
    0%,100% { transform: translateY(-50%) rotate(-3deg); }
    50%      { transform: translateY(-56%) rotate(3deg); }
  }

  /* SLIDE 1 개요 */
  .overview-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; }
  .ov-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 14px; padding: 22px; position: relative; overflow: hidden;
    transition: transform 0.25s;
  }
  .ov-card:hover { transform: translateY(-4px); }
  .ov-card::before { content:''; position:absolute; top:0;left:0;right:0; height:3px; }
  .ov-card:nth-child(1)::before{background:var(--accent1);}
  .ov-card:nth-child(2)::before{background:var(--accent2);}
  .ov-card:nth-child(3)::before{background:var(--accent3);}
  .ov-card:nth-child(4)::before{background:var(--accent4);}
  .ov-card:nth-child(5)::before{background:var(--accent1);}
  .ov-card:nth-child(6)::before{background:var(--accent2);}
  .ov-icon  { font-size: 28px; margin-bottom: 8px; }
  .ov-label { font-size: 10px; color: var(--muted); letter-spacing: 2px; text-transform: uppercase; margin-bottom: 4px; }
  .ov-val   { font-size: 15px; font-weight: 700; line-height: 1.45; }
  .ov-val em { color: var(--accent1); font-style: normal; }

  /* SLIDE 2 규칙 */
  .config-row { display: flex; gap: 10px; margin-bottom: 14px; }
  .config-chip {
    background: rgba(255,255,255,0.04); border: 1px solid var(--border);
    border-radius: 10px; padding: 10px 14px; flex: 1; text-align: center;
  }
  .chip-label { font-size: 9px; color: var(--muted); letter-spacing: 1px; text-transform: uppercase; }
  .chip-val   { font-size: 20px; font-weight: 900; margin-top: 2px; }
  .chip-val.police { color: #4fc3f7; }
  .chip-val.thief  { color: #ff6b6b; }
  .chip-val.time   { color: var(--accent1); }
  .chip-val.round  { color: var(--accent3); }

  .rules-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  .rule-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 13px; padding: 18px 22px;
  }
  .rule-title { font-size: 13px; font-weight: 700; margin-bottom: 10px; display: flex; align-items: center; gap: 6px; }
  .rbadge { padding: 2px 10px; border-radius: 999px; font-size: 11px; font-weight: 700; }
  .bp { background:#1a3a5c; color:#4fc3f7; }
  .bt { background:#3a1a1a; color:#ff6b6b; }
  .be { background:#1a3a1a; color:#4ecdc4; }
  .bw { background:#2a2a1a; color:var(--accent1); }
  .rule-list { list-style: none; }
  .rule-list li {
    font-size: 13px; color: #cdd9e5;
    padding: 3px 0 3px 14px; position: relative; line-height: 1.6;
  }
  .rule-list li::before { content:'▸'; position:absolute; left:0; color:var(--accent3); }

  /* SLIDE 3 장소 */
  .places-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  .place-card {
    background: var(--card); border: 1px solid var(--border); border-radius: 14px;
    padding: 22px 24px; display: flex; gap: 16px; align-items: flex-start;
    transition: all 0.25s; position: relative; overflow: hidden;
  }
  .place-card:hover { border-color:var(--accent1); transform:translateY(-3px); box-shadow:0 8px 28px rgba(247,201,72,0.1); }
  .place-num { font-family:'Black Han Sans',sans-serif; font-size:42px; color:var(--border); line-height:1; flex-shrink:0; width:44px; }
  .place-info h3 { font-size: 16px; font-weight: 700; margin-bottom: 4px; }
  .place-info p  { font-size: 12px; color: var(--muted); line-height: 1.6; }
  .place-icon { position:absolute; right:18px; bottom:14px; font-size:30px; opacity:0.25; }
  .criteria-box { margin-top:16px; background:var(--card); border:1px solid var(--border); border-radius:12px; padding:16px 20px; }
  .criteria-label { font-size:10px; color:var(--muted); letter-spacing:2px; text-transform:uppercase; margin-bottom:10px; }
  .criteria-tags  { display:flex; flex-wrap:wrap; gap:7px; }
  .ctag { background:rgba(78,205,196,0.1); border:1px solid rgba(78,205,196,0.3); color:var(--accent3); padding:3px 12px; border-radius:999px; font-size:12px; }

  /* SLIDE 4 타임라인 */
  .tl-wrap { display:flex; flex-direction:column; gap:0; margin-top:4px; }
  .tl-item { display:flex; gap:20px; align-items:stretch; }
  .tl-left { width:150px; flex-shrink:0; display:flex; flex-direction:column; align-items:flex-end; padding:14px 0; }
  .tl-time   { font-family:'Black Han Sans',sans-serif; font-size:20px; color:var(--accent1); }
  .tl-person { font-size:11px; color:var(--muted); margin-top:2px; }
  .tl-conn   { display:flex; flex-direction:column; align-items:center; width:28px; flex-shrink:0; }
  .tl-dot    { width:13px; height:13px; border-radius:50%; background:var(--accent1); margin-top:20px; flex-shrink:0; box-shadow:0 0 10px rgba(247,201,72,0.5); }
  .tl-line   { width:2px; flex:1; background:var(--border); margin:0 auto; }
  .tl-item:last-child .tl-line { display:none; }
  .tl-right  { flex:1; padding:10px 0; }
  .tl-card   { background:var(--card); border:1px solid var(--border); border-radius:11px; padding:12px 18px; }
  .tl-ttl    { font-size:15px; font-weight:700; margin-bottom:3px; }
  .tl-note   { font-size:12px; color:var(--muted); }

  /* SLIDE 5 예산 */
  .budget-top {
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; margin-bottom: 16px;
  }
  .btop-card {
    background: var(--card); border: 1px solid var(--border); border-radius: 14px;
    padding: 20px 22px; text-align: center; position: relative; overflow: hidden;
  }
  .btop-card::before { content:''; position:absolute; top:0;left:0;right:0; height:3px; }
  .btop-card:nth-child(1)::before { background: var(--accent1); }
  .btop-card:nth-child(2)::before { background: var(--accent3); }
  .btop-card:nth-child(3)::before { background: var(--accent4); }
  .btop-icon  { font-size: 26px; margin-bottom: 8px; }
  .btop-label { font-size: 10px; color: var(--muted); letter-spacing: 2px; text-transform: uppercase; margin-bottom: 6px; }
  .btop-val   { font-size: 22px; font-weight: 900; }
  .btop-val.y  { color: var(--accent1); }
  .btop-val.tl { color: var(--accent3); }
  .btop-val.p  { color: var(--accent4); }
  .btop-sub  { font-size: 11px; color: var(--muted); margin-top: 4px; }

  /* 예산 테이블 */
  .budget-table-wrap {
    background: var(--card); border: 1px solid var(--border); border-radius: 14px;
    overflow: hidden; margin-bottom: 14px;
  }
  .budget-table { width: 100%; border-collapse: collapse; }
  .budget-table thead tr { background: rgba(255,255,255,0.04); }
  .budget-table th {
    padding: 12px 18px; font-size: 11px; letter-spacing: 2px; text-transform: uppercase;
    color: var(--muted); font-weight: 700; text-align: left; border-bottom: 1px solid var(--border);
  }
  .budget-table td {
    padding: 13px 18px; font-size: 14px; border-bottom: 1px solid rgba(48,54,61,0.5);
    vertical-align: middle;
  }
  .budget-table tr:last-child td { border-bottom: none; }
  .budget-table tr:hover td { background: rgba(255,255,255,0.02); }
  .cat-badge {
    display: inline-block; padding: 2px 10px; border-radius: 999px;
    font-size: 11px; font-weight: 700; white-space: nowrap;
  }
  .cat-lunch { background: rgba(247,201,72,0.15); color: var(--accent1); }
  .cat-item  { background: rgba(78,205,196,0.15); color: var(--accent3); }
  .amount { font-weight: 700; font-size: 15px; text-align: right; }
  .note-text { font-size: 12px; color: var(--muted); }

  .budget-total {
    background: rgba(247,201,72,0.07); border: 1px solid rgba(247,201,72,0.3);
    border-radius: 12px; padding: 16px 24px;
    display: flex; align-items: center; justify-content: space-between;
  }
  .total-label { font-size: 13px; color: var(--muted); letter-spacing: 1px; }
  .total-amount { font-family: 'Black Han Sans', sans-serif; font-size: 28px; color: var(--accent1); }
  .total-note { font-size: 12px; color: var(--muted); }
</style>
</head>
<body>

<div class="keyboard-hint">← → 키 또는 버튼으로 이동</div>

<!-- SLIDE 0: TITLE -->
<div class="slide slide-0 active">
  <div class="dot-grid"></div>
  <div class="glow g1"></div>
  <div class="glow g2"></div>
  <div class="title-badge">2026 행사 기획 발표</div>
  <div class="title-main">경도를<br>기다리며</div>
  <div class="title-sub">경찰과 도둑 야외 활동 기획안</div>
  <div class="title-meta">
    <div class="meta-item"><span class="meta-label">📅 일시</span><span class="meta-value">2026. 5. 2 (토)</span></div>
    <div class="meta-item"><span class="meta-label">📍 장소</span><span class="meta-value">중랑캠핑숲 근처 (미정)</span></div>
    <div class="meta-item"><span class="meta-label">👥 인원</span><span class="meta-value">총 30명</span></div>
  </div>
  <div class="title-emoji">🏃‍♂️<br>🚨<br>🌳</div>
</div>

<!-- SLIDE 1: 행사 개요 -->
<div class="slide slide-1">
  <div class="dot-grid"></div>
  <div class="glow g3"></div>
  <div class="section-tag">01 — OVERVIEW</div>
  <div class="section-title">행사 개요</div>
  <div class="overview-grid">
    <div class="ov-card">
      <div class="ov-icon">📅</div>
      <div class="ov-label">일시</div>
      <div class="ov-val">2026년 5월 2일 (토)<br><em>오전 10시 ~ 오후 2시</em></div>
    </div>
    <div class="ov-card">
      <div class="ov-icon">📍</div>
      <div class="ov-label">장소</div>
      <div class="ov-val">중랑캠핑숲 근처 공원<br><span style="font-size:12px;color:var(--muted)">(답사 후 최종 확정)</span></div>
    </div>
    <div class="ov-card">
      <div class="ov-icon">👥</div>
      <div class="ov-label">참가 인원</div>
      <div class="ov-val">총 <em>30명</em><br><span style="font-size:12px;color:var(--muted)">고등학생 20명 · 선생님 10명</span></div>
    </div>
    <div class="ov-card">
      <div class="ov-icon">💰</div>
      <div class="ov-label">총 예산</div>
      <div class="ov-val"><em>124,940원</em><br><span style="font-size:12px;color:var(--muted)">경도 물품 + 점심식사</span></div>
    </div>
    <div class="ov-card">
      <div class="ov-icon">🎫</div>
      <div class="ov-label">참가비</div>
      <div class="ov-val">1인당 <em>3,000~5,000원</em><br><span style="font-size:12px;color:var(--muted)">지원 예산에 따라 변동</span></div>
    </div>
    <div class="ov-card">
      <div class="ov-icon">🎯</div>
      <div class="ov-label">주요 활동</div>
      <div class="ov-val" style="font-size:13px"><em>경찰과 도둑 게임</em><br><span style="font-size:12px;color:var(--muted)">2~3라운드 야외 진행</span></div>
    </div>
  </div>
</div>

<!-- SLIDE 2: 게임 규칙 -->
<div class="slide slide-2">
  <div class="dot-grid"></div>
  <div class="glow g4"></div>
  <div class="section-tag">02 — GAME RULES</div>
  <div class="section-title">🚨 경찰과 도둑 게임</div>
  <div class="config-row">
    <div class="config-chip"><div class="chip-label">👮 경찰</div><div class="chip-val police">10명</div></div>
    <div class="config-chip"><div class="chip-label">🦹 도둑</div><div class="chip-val thief">20명</div></div>
    <div class="config-chip"><div class="chip-label">⏱ 게임 시간</div><div class="chip-val time">1시간</div></div>
    <div class="config-chip"><div class="chip-label">🔄 라운드</div><div class="chip-val round">2~3라운드</div></div>
    <div class="config-chip"><div class="chip-label">📸 종군기자</div><div class="chip-val" style="color:var(--accent4)">2명</div></div>
  </div>
  <div class="rules-layout">
    <div style="display:flex;flex-direction:column;gap:12px;">
      <div class="rule-card">
        <div class="rule-title"><span class="rbadge bp">👮 경찰</span></div>
        <ul class="rule-list">
          <li>도둑을 손으로 터치하면 체포</li>
          <li>감옥 주변 1~2명 배치 가능 (탈옥 방지)</li>
        </ul>
      </div>
      <div class="rule-card">
        <div class="rule-title"><span class="rbadge bt">🦹 도둑</span></div>
        <ul class="rule-list">
          <li>제한 시간 동안 최대한 오래 살아남기</li>
          <li>잡히면 감옥으로 이동 후 대기</li>
        </ul>
      </div>
    </div>
    <div style="display:flex;flex-direction:column;gap:12px;">
      <div class="rule-card">
        <div class="rule-title"><span class="rbadge be">🔓 탈옥 규칙</span></div>
        <ul class="rule-list">
          <li>자유 도둑이 감옥 내 도둑의 손을 터치 → 탈옥 성공</li>
          <li>탈옥 후 <strong style="color:var(--accent3)">10초 무적</strong></li>
          <li>한 번에 한 명씩만 탈옥 가능</li>
        </ul>
      </div>
      <div class="rule-card">
        <div class="rule-title"><span class="rbadge bw">🏆 승리 조건</span></div>
        <ul class="rule-list">
          <li><strong style="color:#4fc3f7">경찰 승리</strong> — 제한 시간 내 도둑 전원 체포</li>
          <li><strong style="color:#ff6b6b">도둑 승리</strong> — 시간 종료까지 한 명이라도 자유 유지</li>
        </ul>
      </div>
    </div>
  </div>
</div>

<!-- SLIDE 3: 장소 -->
<div class="slide slide-3">
  <div class="dot-grid"></div>
  <div class="glow g1" style="opacity:0.08;"></div>
  <div class="section-tag">03 — LOCATIONS</div>
  <div class="section-title">📍 장소 후보지</div>
  <div class="places-grid">
    <div class="place-card">
      <div class="place-num">01</div>
      <div class="place-info"><h3>우디안</h3><p>공간 구조 및 숨을 공간 확인 예정</p></div>
      <div class="place-icon">🌲</div>
    </div>
    <div class="place-card">
      <div class="place-num">02</div>
      <div class="place-info"><h3>근린공원</h3><p>교회에서의 동선 유리</p></div>
      <div class="place-icon">🏞️</div>
    </div>
    <div class="place-card">
      <div class="place-num">03</div>
      <div class="place-info"><h3>중랑캠핑숲 근처 공원</h3><p>현재 1순위 후보 — 공간 규모 적합</p></div>
      <div class="place-icon">⛺</div>
    </div>
    <div class="place-card">
      <div class="place-num">04</div>
      <div class="place-info"><h3>중랑구청사거리 공원</h3><p>접근성 좋음 — 토요일 분위기 확인 필요</p></div>
      <div class="place-icon">🏙️</div>
    </div>
  </div>
  <div class="criteria-box">
    <div class="criteria-label">📋 답사 체크리스트</div>
    <div class="criteria-tags">
      <span class="ctag">단체 모일 수 있는 스팟</span>
      <span class="ctag">주차장 유무</span>
      <span class="ctag">토요일 오전 분위기</span>
      <span class="ctag">감옥 구역 활용 공간</span>
      <span class="ctag">숨을 공간 충분한지</span>
      <span class="ctag">안전성</span>
      <span class="ctag">교회 동선 연결</span>
    </div>
  </div>
</div>

<!-- SLIDE 4: 타임라인 -->
<div class="slide slide-4">
  <div class="dot-grid"></div>
  <div class="glow g2" style="opacity:0.08;"></div>
  <div class="section-tag">04 — TIMELINE</div>
  <div class="section-title">🕙 당일 타임라인</div>
  <div class="tl-wrap">
    <div class="tl-item">
      <div class="tl-left"><div class="tl-time">10:00</div><div class="tl-person">👤 김환희</div></div>
      <div class="tl-conn"><div class="tl-dot"></div><div class="tl-line"></div></div>
      <div class="tl-right"><div class="tl-card"><div class="tl-ttl">집합 및 오리엔테이션</div><div class="tl-note">역할 설정 및 룰 설명</div></div></div>
    </div>
    <div class="tl-item">
      <div class="tl-left"><div class="tl-time">11:00</div><div class="tl-person">👤 김환희</div></div>
      <div class="tl-conn"><div class="tl-dot"></div><div class="tl-line"></div></div>
      <div class="tl-right"><div class="tl-card"><div class="tl-ttl">경찰과 도둑 장소 도착</div><div class="tl-note">2차 룰 설명</div></div></div>
    </div>
    <div class="tl-item">
      <div class="tl-left"><div class="tl-time">11:15</div><div class="tl-person">👤 이성호</div></div>
      <div class="tl-conn"><div class="tl-dot" style="background:var(--accent3);box-shadow:0 0 10px rgba(78,205,196,0.5)"></div><div class="tl-line"></div></div>
      <div class="tl-right"><div class="tl-card"><div class="tl-ttl">🤸 준비 운동</div><div class="tl-note">부상 방지 스트레칭</div></div></div>
    </div>
    <div class="tl-item">
      <div class="tl-left"><div class="tl-time">11:30</div><div class="tl-person">👥 전체</div></div>
      <div class="tl-conn"><div class="tl-dot" style="background:var(--accent2);box-shadow:0 0 10px rgba(255,107,107,0.5)"></div><div class="tl-line"></div></div>
      <div class="tl-right"><div class="tl-card" style="border-color:rgba(255,107,107,0.4);background:rgba(255,107,107,0.07)"><div class="tl-ttl" style="color:var(--accent2)">🚨 경찰과 도둑 진행</div><div class="tl-note">2~3라운드 / 약 1시간</div></div></div>
    </div>
    <div class="tl-item">
      <div class="tl-left"><div class="tl-time">12:30</div><div class="tl-person">👤 김환희</div></div>
      <div class="tl-conn"><div class="tl-dot" style="background:var(--accent4);box-shadow:0 0 10px rgba(162,155,254,0.5)"></div><div class="tl-line"></div></div>
      <div class="tl-right"><div class="tl-card"><div class="tl-ttl">🏆 종료 및 교회 복귀</div><div class="tl-note">시상식 및 점심식사</div></div></div>
    </div>
  </div>
</div>

<!-- SLIDE 5: 예산 -->
<div class="slide slide-5">
  <div class="dot-grid"></div>
  <div class="glow g5" style="opacity:0.09;"></div>
  <div class="section-tag">05 — BUDGET</div>
  <div class="section-title">💰 예산 계획</div>

  <div class="budget-top">
    <div class="btop-card">
      <div class="btop-icon">💵</div>
      <div class="btop-label">총 예산</div>
      <div class="btop-val y">124,940원</div>
      <div class="btop-sub">경도 물품 + 점심식사</div>
    </div>
    <div class="btop-card">
      <div class="btop-icon">🎒</div>
      <div class="btop-label">경도 물품</div>
      <div class="btop-val tl">34,300원</div>
      <div class="btop-sub">경찰 방울 + 도둑 표시 장치</div>
    </div>
    <div class="btop-card">
      <div class="btop-icon">🍱</div>
      <div class="btop-label">점심식사</div>
      <div class="btop-val p">90,640원</div>
      <div class="btop-sub">소소김밥 + 물</div>
    </div>
  </div>

  <div class="budget-table-wrap">
    <table class="budget-table">
      <thead>
        <tr>
          <th>구분</th>
          <th>항목</th>
          <th style="text-align:right">금액</th>
          <th>비고</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><span class="cat-badge cat-lunch">🍱 점심식사</span></td>
          <td>소소김밥</td>
          <td class="amount">80,000원</td>
          <td class="note-text">기본 김밥 4,000원 · 인원 20명 기준</td>
        </tr>
        <tr>
          <td><span class="cat-badge cat-item">🎒 경도 물품</span></td>
          <td>경찰 방울</td>
          <td class="amount">4,600원</td>
          <td class="note-text">10개 4,600원</td>
        </tr>
        <tr>
          <td><span class="cat-badge cat-item">🎒 경도 물품</span></td>
          <td>도둑 표시 장치</td>
          <td class="amount">29,700원</td>
          <td class="note-text">1개 990원</td>
        </tr>
        <tr>
          <td><span class="cat-badge cat-lunch">🍱 점심식사</span></td>
          <td>물</td>
          <td class="amount">10,640원</td>
          <td class="note-text">40개 500ml</td>
        </tr>
      </tbody>
    </table>
  </div>

  <div class="budget-total">
    <div>
      <div class="total-label">합계</div>
      <div class="total-note">참가비 별도 (1인 3,000~5,000원, 지원 예산에 따라 변동)</div>
    </div>
    <div class="total-amount">₩124,940</div>
  </div>
</div>

<!-- NAVIGATION -->
<div class="dot-nav" id="dotNav"></div>
<div class="nav">
  <button onclick="changeSlide(-1)">← 이전</button>
  <button onclick="changeSlide(1)">다음 →</button>
</div>
<div class="slide-num" id="slideNum"></div>

<script>
  const slides = document.querySelectorAll('.slide');
  const dotNav = document.getElementById('dotNav');
  const slideNum = document.getElementById('slideNum');
  let current = 0;

  slides.forEach((_, i) => {
    const d = document.createElement('span');
    d.onclick = () => goTo(i);
    dotNav.appendChild(d);
  });

  function updateUI() {
    slides.forEach((s, i) => s.classList.toggle('active', i === current));
    dotNav.querySelectorAll('span').forEach((d, i) => d.classList.toggle('on', i === current));
    slideNum.textContent = `${current + 1} / ${slides.length}`;
  }
  function changeSlide(dir) {
    current = Math.max(0, Math.min(slides.length - 1, current + dir));
    updateUI();
  }
  function goTo(i) { current = i; updateUI(); }

  document.addEventListener('keydown', e => {
    if (e.key === 'ArrowRight' || e.key === 'ArrowDown') changeSlide(1);
    if (e.key === 'ArrowLeft'  || e.key === 'ArrowUp')   changeSlide(-1);
  });

  updateUI();
</script>
</body>
</html>
