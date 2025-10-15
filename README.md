<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Dashboard Operasional Surprice 2025</title>
  <style>
    /* Reset & base */
    * { box-sizing: border-box; margin: 0; padding: 0; }
    html,body { height: 100%; }
    body {
      font-family: "Segoe UI", Roboto, Arial, sans-serif;
      background: #f3f7fb;
      color: #063259; /* teks gelap biru */
      display: flex;
      min-height: 100vh;
    }

    /* ---------- SIDEBAR ---------- */
    nav.sidebar {
      width: 280px;
      background: linear-gradient(180deg,#053a78 0%, #0a4b9b 100%); /* kantor pos style */
      color: #ffffff;
      padding: 22px;
      display: flex;
      flex-direction: column;
      gap: 18px;
      box-shadow: 4px 0 18px rgba(3,37,76,0.12);
    }

    .brand {
      display:flex;
      gap:12px;
      align-items:center;
    }
    .brand img {
      width:56px;
      height:56px;
      border-radius:8px;
      background:#fff;
      padding:6px;
      object-fit:contain;
    }
    .brand .title {
      font-weight:700;
      font-size:16px;
      color:#fff;
      line-height:1;
    }
    .brand .subtitle {
      font-size:12px;
      color:rgba(255,255,255,0.85);
    }

    .nav-section { flex:1; overflow:auto; padding-right:6px; }
    .menu { list-style:none; margin-top:8px; }
    .menu > li { margin-bottom:6px; }
    .menu a {
      display:flex;
      align-items:center;
      gap:10px;
      text-decoration:none;
      color:rgba(255,255,255,0.95);
      padding:10px 12px;
      border-radius:8px;
      transition: background .16s, transform .12s;
      font-weight:600;
    }
    .menu a:hover { background: rgba(255,255,255,0.06); transform:translateX(2px); }
    .menu .sub {
      margin-top:6px;
      margin-left:12px;
      list-style:none;
      display:none;
    }
    .menu .sub li a {
      padding:8px 12px; font-weight:500; font-size:13px;
    }
    .menu .open > a { background: rgba(255,255,255,0.08); }
    .menu .open .sub { display:block; }

    /* small helper */
    .muted { color: rgba(255,255,255,0.8); font-weight:500; font-size:13px; }

    /* ---------- MAIN ---------- */
    .main {
      flex:1;
      display:flex;
      flex-direction:column;
      min-height:100vh;
    }

    header.topbar {
      background: #ffffff;
      border-bottom: 1px solid #e6eef8;
      padding: 14px 22px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:12px;
    }
    .page-title {
      display:flex; flex-direction:column;
    }
    .page-title h1 { font-size:18px; color:#052a4a; margin-bottom:4px; }
    .page-title p { color:#375b7a; font-size:13px; margin:0; }

    .datetime-box {
      display:flex;
      flex-direction:column;
      align-items:flex-end;
      gap:4px;
      font-weight:700;
      color:#052a4a;
    }
    .datetime-box .day { font-size:14px; color:#0b3a67; }
    .datetime-box .date { font-size:13px; color:#1f5a86; font-weight:600; }
    .datetime-box .time { font-size:20px; color:#052a4a; font-weight:800; }

    /* ---------- CONTENT ---------- */
    .content {
      padding: 24px;
      background: linear-gradient(180deg,#f7fbff 0%, #f3f7fb 100%);
      flex:1;
      overflow:auto;
    }

    .card-row {
      display:grid;
      grid-template-columns: repeat(4, 1fr);
      gap:16px;
      margin-bottom:18px;
    }
    .card {
      background:#fff;
      border-radius:10px;
      padding:16px;
      box-shadow: 0 6px 16px rgba(7,28,56,0.06);
      border-left: 4px solid #0b63b6;
    }
    .card h3 { font-size:13px; color:#16384f; margin-bottom:8px; font-weight:800; }
    .card .value { font-size:20px; color:#052a4a; font-weight:900; }

    .panel {
      background:#fff;
      border-radius:10px;
      padding:16px;
      box-shadow: 0 6px 16px rgba(7,28,56,0.06);
    }

    table {
      width:100%;
      border-collapse:collapse;
      margin-top:10px;
    }
    th, td {
      padding:10px 12px;
      text-align:left;
      border-bottom:1px solid #eef6ff;
      color:#08304f;
      font-size:13px;
    }
    th { background:#f4fbff; font-weight:800; color:#0c3a5a; }

    /* responsive */
    @media (max-width:1000px) {
      .card-row { grid-template-columns: repeat(2, 1fr); }
      nav.sidebar { width: 230px; }
      .datetime-box { align-items:flex-start; }
    }
    @media (max-width:600px) {
      body { flex-direction:column; }
      nav.sidebar { width:100%; flex-direction:row; gap:12px; padding:12px; }
      nav.sidebar .nav-section { display:none; }
      .main { margin-top:12px; }
      .card-row { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <!-- SIDEBAR -->
  <nav class="sidebar" aria-label="Sidebar">
    <div>
      <div class="brand">
        <!-- ganti src dengan logo Surprice kamu -->
        <img src="https://via.placeholder.com/120x120.png?text=Surprice" alt="Logo Surprice">
        <div>
          <div class="title">Surprice Operasional</div>
          <div class="subtitle">Dashboard & Laporan 2025</div>
        </div>
      </div>

      <div style="height:12px;"></div>

      <div class="nav-section">
        <div style="padding:8px 0 8px 6px;">
          <div class="muted" style="font-size:12px">Menu Utama</div>
        </div>

        <ul class="menu" id="mainMenu">
          <li>
            <a href="#" onclick="showSection('dashboard')">🏠 Dashboard</a>
          </li>

          <li id="menu-gudang">
            <a href="#" onclick="showSection('inventory')">📦 Divisi Gudang</a>
            <ul class="sub" id="sub-gudang">
              <li><a href="#" onclick="showSection('inventory')">- Inventory Booth</a></li>
              <li>
                <a href="#" class="toggle-sub" onclick="toggleSub(event)">
                  - Laporan Gudang <span style="margin-left:auto" class="arrow">▶</span>
                </a>
                <ul class="sub" id="laporanGudangList" style="display:none;">
                  <li><a href="https://docs.google.com/spreadsheets/d/14phSwmbLXDSVpc1wBo9NZdz9yV1VIOutwBySSQNewJ8/edit" target="_blank">🧾 V.2 Log Aktivitas Operasional Surprice 2025</a></li>
                  <li><a href="https://docs.google.com/spreadsheets/d/1XET5ZuVH10Yt4dhVxioCe1jww5-cWfjC/edit?gid=2037484461#gid=2037484461" target="_blank">📊 Laporan_Operasional_Surprice2025</a></li>
                </ul>
              </li>
            </ul>
          </li>

          <li>
            <a href="#" onclick="showSection('cs')">👥 Divisi Customer Service</a>
          </li>

          <li>
            <a href="#" onclick="showSection('marketing')">📈 Marketing & Sales</a>
          </li>

          <li>
            <a href="#" onclick="showSection('it')">💻 IT & Development</a>
          </li>
        </ul>
      </div>
    </div>

    <!-- footer kecil di sidebar (informasi singkat) -->
    <div style="font-size:12px;color:rgba(255,255,255,0.85);padding:6px 4px;">
      <div style="margin-bottom:6px">User: <strong style="color:#fff">admin</strong></div>
      <div style="font-size:11px;color:rgba(255,255,255,0.75)">Versi 1.0 • Surprice</div>
    </div>
  </nav>

  <!-- MAIN -->
  <div class="main">
    <header class="topbar">
      <div class="page-title">
        <h1>Dashboard Operasional Surprice</h1>
        <p>Ringkasan aktivitas & laporan harian tim</p>
      </div>

      <div class="datetime-box" aria-live="polite">
        <div class="day" id="dayName">-</div>
        <div class="date" id="dateFull">-</div>
        <div class="time" id="timeNow">-</div>
      </div>
    </header>

    <main class="content" id="contentArea">
      <!-- cards -->
      <div class="card-row">
        <div class="card">
          <h3>Total Item</h3>
          <div class="value" id="cardTotalItem">0</div>
        </div>
        <div class="card">
          <h3>Stok Awal</h3>
          <div class="value" id="cardStokAwal">0</div>
        </div>
        <div class="card">
          <h3>Terjual</h3>
          <div class="value" id="cardTerjual">0</div>
        </div>
        <div class="card">
          <h3>Tersisa</h3>
          <div class="value" id="cardTersisa">0</div>
        </div>
      </div>

      <!-- inventory table -->
      <div class="panel">
        <h3 style="margin-bottom:8px">Tabel Inventory</h3>
        <div style="overflow:auto">
          <table>
            <thead>
              <tr>
                <th>No</th><th>Kode</th><th>Nama Barang</th><th>Stok Awal</th><th>Terjual</th><th>Kembali</th><th>Tersisa</th><th>Selisih</th>
              </tr>
            </thead>
            <tbody id="tableBody">
              <tr><td colspan="8" style="text-align:center;padding:18px;color:#0b3a67">📭 Belum ada data. Klik "Muat Data dari Sheets".</td></tr>
            </tbody>
          </table>
        </div>
      </div>
    </main>

    <footer style="background:#0a4b9b;color:#fff;padding:12px;text-align:center;font-size:13px;">
      © 2025 Sendi_Muchdianto • Surprice Operasional
    </footer>
  </div>

  <!-- SCRIPTS: tanggal/waktu + menu + contoh data -->
  <script>
    // ---------- Date & Time (Asia/Jakarta) ----------
    function pad(n){ return n.toString().padStart(2,'0'); }

    function updateDateTime() {
      // Use Intl to format in id-ID timezone Asia/Jakarta
      const now = new Date();
      // Convert to Jakarta time by using locale with timeZone
      const optionsDate = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric', timeZone: 'Asia/Jakarta' };
      const optionsTime = { hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: false, timeZone: 'Asia/Jakarta' };

      const dayName = new Intl.DateTimeFormat('id-ID', { weekday: 'long', timeZone: 'Asia/Jakarta' }).format(now);
      const dateFull = new Intl.DateTimeFormat('id-ID', optionsDate).format(now);
      const timeNow = new Intl.DateTimeFormat('id-ID', optionsTime).format(now);

      document.getElementById('dayName').textContent = dayName.charAt(0).toUpperCase() + dayName.slice(1);
      document.getElementById('dateFull').textContent = dateFull;
      document.getElementById('timeNow').textContent = timeNow;
    }
    setInterval(updateDateTime, 1000);
    updateDateTime();

    // ---------- Toggle laporan gudang submenu ----------
    function toggleSub(e){
      e.preventDefault();
      const list = document.getElementById('laporanGudangList');
      const visible = list.style.display === 'block';
      list.style.display = visible ? 'none' : 'block';

      // rotate arrow
      const arrow = e.currentTarget.querySelector('.arrow');
      if(arrow) arrow.style.transform = visible ? 'none' : 'rotate(90deg)';
    }

    // ---------- Simple showSection (replace content) ----------
    function showSection(key){
      const content = document.getElementById('contentArea');
      // keep same layout but update header + sample content
      let html = '';
      if(key === 'dashboard'){
        html = `
          <div class="card-row">
            <div class="card"><h3>Total Item</h3><div class="value" id="cardTotalItem">128</div></div>
            <div class="card"><h3>Stok Awal</h3><div class="value" id="cardStokAwal">320</div></div>
            <div class="card"><h3>Terjual</h3><div class="value" id="cardTerjual">192</div></div>
            <div class="card"><h3>Tersisa</h3><div class="value" id="cardTersisa">128</div></div>
          </div>
          <div class="panel"><h3>Ringkasan Hari Ini</h3><p>Gunakan menu di kiri untuk membuka laporan atau log aktivitas. Klik "Laporan Gudang" untuk buka Google Sheets terkait.</p></div>
        `;
      } else if(key === 'inventory'){
        html = `
          <div class="panel"><h3>Inventory Booth</h3><p>Data inventory ditampilkan di bawah.</p>
            <table style="margin-top:12px">
              <thead><tr><th>No</th><th>Kode</th><th>Nama Barang</th><th>Stok Awal</th><th>Terjual</th><th>Kembali</th><th>Tersisa</th><th>Selisih</th></tr></thead>
              <tbody>
                <tr><td>1</td><td>KFC5003</td><td>Surprice Set Toples Emas 3pcs</td><td>10</td><td>4</td><td>0</td><td>6</td><td>0</td></tr>
                <tr><td>2</td><td>PTT5601</td><td>Surprice Set Toples Emas 3pcs</td><td>8</td><td>2</td><td>0</td><td>6</td><td>0</td></tr>
              </tbody>
            </table>
          </div>
        `;
      } else {
        html = `<div class="panel"><h3>${key.toUpperCase()}</h3><p>Konten ${key} belum diisi. Fitur bisa dikembangkan lebih lanjut.</p></div>`;
      }
      content.innerHTML = html;
    }

    // inisialisasi tampilan default
    showSection('dashboard');

    // ---------- (optional) prevent accidental selection when clicking sidebar on mobile ----------
    document.querySelectorAll('nav.sidebar a').forEach(a => a.addEventListener('click', (e) => {
      // keep default behavior for links with target _blank
      if(a.target === '_blank') return;
      e.preventDefault();
    }));
  </script>
</body>
</html>
