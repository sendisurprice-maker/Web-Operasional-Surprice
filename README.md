<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dashboard Operasional Surprice 2025</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: "Segoe UI", Arial, sans-serif;
    }

    body {
      display: flex;
      height: 100vh;
      background-color: #f8fafc;
      color: #1e293b;
    }

    /* ==== SIDEBAR ==== */
    nav {
      width: 270px;
      background: linear-gradient(180deg, #0f172a, #1e293b);
      color: white;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      padding: 20px 0;
      box-shadow: 3px 0 10px rgba(0, 0, 0, 0.2);
    }

    .logo-container {
      text-align: center;
      padding: 10px 0 20px;
      border-bottom: 1px solid #334155;
    }

    .logo-container img {
      width: 100px;
      height: auto;
      border-radius: 50%;
    }

    .logo-container h2 {
      margin-top: 10px;
      font-size: 16px;
      color: #facc15;
    }

    nav ul {
      list-style-type: none;
      padding: 0;
    }

    nav li {
      padding: 5px 20px;
    }

    nav a {
      color: #f1f5f9;
      text-decoration: none;
      display: flex;
      align-items: center;
      padding: 8px 10px;
      border-radius: 8px;
      transition: 0.2s;
    }

    nav a:hover {
      background-color: #334155;
    }

    .submenu {
      display: none;
      margin-left: 20px;
    }

    .arrow {
      margin-left: auto;
      font-size: 13px;
      transition: transform 0.2s ease;
    }

    .open .arrow {
      transform: rotate(90deg);
    }

       /* ==== MAIN AREA ==== */
    .main-content {
      flex: 1;
      display: flex;
      flex-direction: column;
    }

    /* Header */
    header {
      background-color: white;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 15px 25px;
      border-bottom: 1px solid #e2e8f0;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
    }

    header h1 {
      font-size: 18px;
      font-weight: 600;
      color: #0f172a;
    }

    .datetime {
      font-size: 14px;
      color: #64748b;
      font-weight: 500;
    }

    /* Konten Utama */
    .content {
      flex: 1;
      padding: 30px;
      overflow-y: auto;
    }

    .content h2 {
      font-size: 20px;
      color: #0f172a;
      margin-bottom: 10px;
    }

    .content p {
      color: #475569;
      line-height: 1.6;
    }

    /* Footer */
    footer {
      text-align: center;
      padding: 12px;
      background-color: #0f172a;
      color: #f1f5f9;
      font-size: 13px;
      border-top: 1px solid #475569;
    }
  </style>
</head>

<body>
  <!-- ===== SIDEBAR ===== -->
  <nav>
    <div>
      <div class="logo-container">
        <img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/Shopee_logo.svg" alt="Surprice Logo" />
        <h2>Surprice Operasional</h2>
      </div>

      <ul>
        <li><a href="#" onclick="showSection('dashboard')">🏠 Dashboard</a></li>
        <li>
          <a href="#" onclick="showSection('inventory')">📦 Divisi Gudang</a>
          <ul>
            <li><a href="#" onclick="showSection('inventory')">- Inventory Booth</a></li>
            <li id="laporan-gudang-menu">
              <a href="#" onclick="toggleSubmenu(event)">
                - Laporan Gudang <span class="arrow">▶</span>
              </a>
              <ul id="submenu-laporan-gudang" class="submenu">
                <li>
                  <a href="https://docs.google.com/spreadsheets/d/14phSwmbLXDSVpc1wBo9NZdz9yV1VIOutwBySSQNewJ8/edit" target="_blank">
                    🧾 V.2 Log Aktivitas Operasional Surprice 2025
                  </a>
                </li>
                <li>
                  <a href="https://docs.google.com/spreadsheets/d/1XET5ZuVH10Yt4dhVxioCe1jww5-cWfjC/edit?gid=2037484461#gid=2037484461" target="_blank">
                    📊 Laporan_Operasional_Surprice2025
                  </a>
                </li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </div>

   </nav>

  <!-- ===== MAIN CONTENT ===== -->
  <div class="main-content">
    <header>
      <h1>Dashboard Operasional Surprice 2025</h1>
      <div class="datetime" id="datetime"></div>
    </header>

    <section class="content" id="content">
      <h2>Selamat Datang 👋</h2>
      <p>
        Ini adalah pusat kontrol aktivitas operasional Surprice tahun 2025.
        Gunakan menu di sisi kiri untuk membuka laporan, log aktivitas, dan data operasional harian.
      </p>
    </section>

    <footer>
      © 2025 Sendi_Muchdianto. All rights reserved.
    </footer>
  </div>

  <!-- ===== SCRIPT ===== -->
  <script>
    // Tanggal dan Waktu Real-time
    function updateDateTime() {
      const now = new Date();
      const options = {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit',
      };
      document.getElementById('datetime').textContent = now.toLocaleDateString('id-ID', options);
    }
    setInterval(updateDateTime, 1000);
    updateDateTime();

    // Toggle submenu
    function toggleSubmenu(event) {
      event.preventDefault();
      const menuItem = document.getElementById('laporan-gudang-menu');
      const submenu = document.getElementById('submenu-laporan-gudang');
      const isOpen = submenu.style.display === 'block';
      submenu.style.display = isOpen ? 'none' : 'block';
      menuItem.classList.toggle('open', !isOpen);
    }

    // Fungsi contoh
    function showSection(sectionId) {
      document.getElementById('content').innerHTML =
        `<h2>${sectionId.replace('-', ' ').toUpperCase()}</h2>
         <p>Konten untuk bagian <b>${sectionId}</b> akan ditampilkan di sini.</p>`;
    }

      }
  </script>
</body>
</html>
