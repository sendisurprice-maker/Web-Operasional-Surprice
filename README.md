<html lang="id">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Sistem Inventory Booth - Dilwali</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.31/jspdf.plugin.autotable.min.js"></script>

  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    
    body {
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      background: #f5f5f5;
      color: #333;
    }

    /* Login Page */
    .login-page {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 100vh;
      background: linear-gradient(135deg, #FF6B00 0%, #E65100 100%);
    }
    
    .login-box {
      background: #fff;
      padding: 40px;
      border-radius: 12px;
      box-shadow: 0 8px 30px rgba(0,0,0,0.2);
      width: 100%;
      max-width: 420px;
      text-align: center;
    }
    
    .login-box h2 {
      margin: 0 0 10px;
      color: #FF6B00;
      font-size: 28px;
      font-weight: 700;
    }
    
    .login-box p {
      color: #666;
      margin-bottom: 25px;
      font-size: 14px;
    }
    
    .form-group {
      margin-bottom: 20px;
      text-align: left;
    }
    
    .form-group label {
      display: block;
      margin-bottom: 8px;
      font-weight: 600;
      color: #555;
      font-size: 14px;
    }
    
    input[type="text"],
    input[type="password"] {
      width: 100%;
      padding: 12px 15px;
      border: 2px solid #ddd;
      border-radius: 6px;
      font-size: 15px;
      transition: all 0.3s;
    }
    
    input[type="text"]:focus,
    input[type="password"]:focus {
      outline: none;
      border-color: #FF6B00;
      box-shadow: 0 0 0 3px rgba(255, 107, 0, 0.1);
    }
    
    .btn-login {
      width: 100%;
      padding: 13px;
      background: #FF6B00;
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      margin-top: 10px;
    }
    
    .btn-login:hover {
      background: #E65100;
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(255, 107, 0, 0.3);
    }
    
    .error-msg {
      color: #ef4444;
      font-size: 14px;
      margin-top: 15px;
      padding: 10px;
      background: #fee;
      border-radius: 6px;
    }

    /* Main Container */
    .container {
      display: flex;
      min-height: 100vh;
      background: #f5f5f5;
    }

    /* Sidebar */
    .sidebar {
      width: 280px;
      background: linear-gradient(180deg, #FF6B00 0%, #E65100 100%);
      color: #fff;
      position: fixed;
      height: 100vh;
      overflow-y: auto;
      box-shadow: 3px 0 15px rgba(0,0,0,0.1);
      display: flex;
      flex-direction: column;
    }
    
    .sidebar-header {
      padding: 25px 20px;
      background: rgba(0,0,0,0.1);
      border-bottom: 2px solid rgba(255,255,255,0.2);
    }
    
    .sidebar-header h2 {
      font-size: 20px;
      font-weight: 700;
      margin-bottom: 5px;
    }
    
    .sidebar-header p {
      font-size: 13px;
      opacity: 0.9;
    }
    
    .sidebar-content {
      flex: 1;
      padding: 20px 0;
      overflow-y: auto;
    }
    
    .sidebar h3 {
      padding: 15px 20px 10px;
      margin: 0;
      font-size: 15px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      border-bottom: 1px solid rgba(255,255,255,0.2);
      opacity: 0.9;
    }
    
    .sidebar ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }
    
    .sidebar li {
      margin: 0;
    }
    
    .sidebar a {
      display: block;
      padding: 12px 20px;
      color: #fff;
      text-decoration: none;
      transition: all 0.3s;
      border-left: 4px solid transparent;
      font-size: 14px;
    }
    
    .sidebar a:hover {
      background: rgba(255,255,255,0.15);
      border-left-color: #fff;
      padding-left: 25px;
    }
    
    .sidebar a.active {
      background: rgba(255,255,255,0.2);
      border-left-color: #fff;
      font-weight: 600;
    }
    
    .submenu {
      display: none;
      margin-left: 15px;
      margin-top: 5px;
      border-left: 2px solid rgba(255,255,255,0.2);
    }
    
    .submenu a {
      padding: 10px 15px;
      font-size: 13px;
    }
    
    .arrow {
      float: right;
      font-size: 12px;
      transition: transform 0.2s ease;
    }
    
    .open .arrow {
      transform: rotate(90deg);
    }
    
    .sidebar-footer {
      padding: 20px;
      background: rgba(0,0,0,0.1);
      border-top: 2px solid rgba(255,255,255,0.2);
    }
    
    .logout-btn {
      width: 100%;
      background: rgba(255,255,255,0.2);
      color: #fff;
      padding: 12px;
      border-radius: 6px;
      border: 2px solid rgba(255,255,255,0.3);
      cursor: pointer;
      font-weight: 600;
      font-size: 14px;
      transition: all 0.3s;
    }
    
    .logout-btn:hover {
      background: rgba(255,255,255,0.3);
      border-color: #fff;
    }

    /* Main Content */
    .main-content {
      flex: 1;
      margin-left: 280px;
      padding: 0;
      background: #f5f5f5;
    }
    
    /* Top Bar */
    .top-bar {
      background: #fff;
      padding: 20px 30px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.08);
      display: flex;
      justify-content: space-between;
      align-items: center;
      position: sticky;
      top: 0;
      z-index: 100;
    }
    
    .top-bar h1 {
      margin: 0;
      font-size: 24px;
      color: #FF6B00;
      font-weight: 700;
    }
    
    .datetime-display {
      text-align: right;
    }
    
    .datetime-display .date {
      font-size: 15px;
      font-weight: 600;
      color: #333;
    }
    
    .datetime-display .time {
      font-size: 22px;
      font-weight: 700;
      color: #FF6B00;
      margin-top: 2px;
    }

    /* Content Area */
    .content-area {
      padding: 30px;
    }
    
    .section-content {
      display: none;
    }
    
    .section-content.active {
      display: block;
    }

    /* Stats Cards */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      margin-bottom: 30px;
    }
    
    .stat-card {
      background: #fff;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      border-left: 4px solid #FF6B00;
      transition: all 0.3s;
    }
    
    .stat-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 6px 20px rgba(0,0,0,0.12);
    }
    
    .stat-card h3 {
      font-size: 14px;
      color: #666;
      margin-bottom: 10px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    
    .stat-card .value {
      font-size: 32px;
      font-weight: 700;
      color: #FF6B00;
      margin-bottom: 5px;
    }
    
    .stat-card .label {
      font-size: 13px;
      color: #999;
    }

    /* Config Section */
    .config-section {
      background: #fff;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      margin-bottom: 25px;
    }
    
    .config-section h3 {
      margin: 0 0 20px;
      color: #FF6B00;
      font-size: 18px;
      font-weight: 700;
      padding-bottom: 15px;
      border-bottom: 2px solid #f0f0f0;
    }
    
    .config-input {
      margin-bottom: 20px;
    }
    
    .config-input label {
      display: block;
      margin-bottom: 8px;
      font-weight: 600;
      color: #555;
      font-size: 14px;
    }
    
    .config-input input {
      width: 100%;
      padding: 12px 15px;
      border: 2px solid #e0e0e0;
      border-radius: 6px;
      font-size: 14px;
    }

    /* Toolbar */
    .toolbar {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
      margin-bottom: 25px;
    }
    
    .toolbar button {
      padding: 12px 20px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 14px;
      font-weight: 600;
      transition: all 0.3s;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    
    .toolbar button:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    }
    
    .btn-primary { background: #FF6B00; color: #fff; }
    .btn-primary:hover { background: #E65100; }
    
    .btn-success { background: #10b981; color: #fff; }
    .btn-success:hover { background: #059669; }
    
    .btn-warning { background: #f59e0b; color: #fff; }
    .btn-warning:hover { background: #d97706; }
    
    .btn-info { background: #3b82f6; color: #fff; }
    .btn-info:hover { background: #2563eb; }
    
    .btn-danger { background: #ef4444; color: #fff; }
    .btn-danger:hover { background: #dc2626; }

    /* Table */
    table {
      width: 100%;
      background: #fff;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }
    
    thead {
      background: linear-gradient(135deg, #FF6B00 0%, #E65100 100%);
      color: #fff;
    }
    
    th {
      padding: 15px;
      text-align: left;
      font-weight: 600;
      font-size: 13px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    
    td {
      padding: 15px;
      border-bottom: 1px solid #f0f0f0;
      font-size: 14px;
    }
    
    tbody tr:hover {
      background: #fff8f3;
    }
    
    .loading {
      text-align: center;
      color: #999;
      padding: 40px !important;
      font-size: 16px;
    }

    /* Laporan Kebersihan */
    .kebersihan-section {
      background: #fff;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      margin-bottom: 25px;
    }
    
    .kebersihan-section h3 {
      margin: 0 0 20px;
      color: #FF6B00;
      font-size: 18px;
      font-weight: 700;
      padding-bottom: 15px;
      border-bottom: 2px solid #f0f0f0;
    }
    
    .photo-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      margin-top: 20px;
    }
    
    .photo-item {
      background: #f9f9f9;
      padding: 15px;
      border-radius: 8px;
      text-align: center;
      border: 2px solid #e0e0e0;
      transition: all 0.3s;
    }
    
    .photo-item:hover {
      border-color: #FF6B00;
      transform: translateY(-3px);
      box-shadow: 0 4px 12px rgba(255, 107, 0, 0.2);
    }
    
    .photo-item a {
      color: #FF6B00;
      text-decoration: none;
      font-weight: 600;
      font-size: 14px;
    }
    
    .photo-item .icon {
      font-size: 36px;
      margin-bottom: 10px;
    }

    /* Responsive */
    @media (max-width: 768px) {
      .sidebar {
        width: 100%;
        position: relative;
        height: auto;
      }
      
      .main-content {
        margin-left: 0;
      }
      
      .top-bar {
        flex-direction: column;
        align-items: flex-start;
        gap: 15px;
      }
      
      .stats-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>

<body>
  <!-- Login Page -->
  <div id="loginPage" class="login-page">
    <div class="login-box">
      <h2>🔐 Login Sistem Inventory</h2>
      <p>Username: admin | Password: admin1234</p>
      <div class="form-group">
        <label>Username:</label>
        <input id="username" type="text" placeholder="Masukkan username" autocomplete="username">
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input id="password" type="password" placeholder="Masukkan password" autocomplete="current-password">
      </div>
      <button class="btn-login" onclick="login()">Login</button>
      <div id="errorMsg" class="error-msg" style="display:none;">Username atau password salah!</div>
    </div>
  </div>

  <!-- Main App -->
  <div id="mainApp" class="container" style="display:none;">
    <!-- Sidebar -->
    <nav class="sidebar">
      <div class="sidebar-header">
        <h2>📦 DILWALI WMS</h2>
        <p>Warehouse Management System</p>
      </div>
      
      <div class="sidebar-content">
        <h3>🏢 Dashboard Divisi</h3>
        <ul>
          <li>
            <a href="#" onclick="showSection('dashboard')" class="active">🏠 Dashboard Utama</a>
          </li>
          
          <li>
            <a href="#" onclick="showSection('inventory')">📦 Divisi Gudang</a>
            <ul style="padding-left:20px;">
              <li><a href="#" onclick="showSection('inventory')"> • Inventory Booth</a></li>
              <li id="laporan-gudang-menu">
                <a href="#" onclick="toggleSubmenu(event, 'submenu-laporan-gudang')">
                  📊 • Laporan Gudang <span class="arrow">▶</span>
                </a>
                <ul id="submenu-laporan-gudang" class="submenu">
                  <li>
                    <a href="https://docs.google.com/spreadsheets/d/14phSwmbLXDSVpc1wBo9NZdz9yV1VIOutwBySSQNewJ8/edit" target="_blank">
                      📋 V.2 Log Aktivitas Operasional
                    </a>
                  </li>
                  <li>
                    <a href="https://docs.google.com/spreadsheets/d/1XET5ZuVH10Yt4dhVxioCe1jww5-cWfjC/edit?gid=2037484461#gid=2037484461" target="_blank">
                      📊 Laporan Operasional Surprice2025
                    </a>
                  </li>
                </ul>
              </li>
              <li><a href="#" onclick="showSection('kebersihan')">🧹 • Laporan Kebersihan</a></li>
              <li><a href="#" onclick="showSection('defect')">⚠️ • Status Defect Barang</a></li>
            </ul>
          </li>

          <li><a href="#" onclick="showSection('customer-service')">👥 Divisi Customer Service</a></li>
          <li><a href="#">📈 Divisi Marketing & Sales Digital</a></li>
          <li><a href="#">⚙️ Divisi Admin & Purchasing</a></li>
          <li><a href="#">🚚 Divisi Transporter</a></li>
          <li><a href="#">📬 Divisi Kurir</a></li>
          <li><a href="#">💻 Divisi IT</a></li>
        </ul>
      </div>

      <div class="sidebar-footer">
        <button class="logout-btn" onclick="logout()">🚪 Logout</button>
      </div>
    </nav>

    <!-- Main Content -->
    <div class="main-content">
      <!-- Top Bar -->
      <div class="top-bar">
        <h1 id="pageTitle">Dashboard Utama</h1>
        <div class="datetime-display">
          <div class="date" id="currentDate">Senin, 15 Oktober 2025</div>
          <div class="time" id="currentTime">14:30:45</div>
        </div>
      </div>

      <!-- Content Area -->
      <div class="content-area">
        
        <!-- Dashboard Section -->
        <div id="dashboardSection" class="section-content active">
          <div class="stats-grid">
            <div class="stat-card">
              <h3>📦 Total Inventory</h3>
              <div class="value" id="totalInventory">0</div>
              <div class="label">Item dalam sistem</div>
            </div>
            <div class="stat-card">
              <h3>⚠️ Defect Jual Murah</h3>
              <div class="value" id="defectJual">0</div>
              <div class="label">Unit</div>
            </div>
            <div class="stat-card">
              <h3>🔧 Defect Perbaikan</h3>
              <div class="value" id="defectPerbaikan">0</div>
              <div class="label">Unit</div>
            </div>
            <div class="stat-card">
              <h3>🗑️ Defect Hancur</h3>
              <div class="value" id="defectHancur">0</div>
              <div class="label">Unit</div>
            </div>
          </div>
          
          <div class="config-section">
            <h3>🎯 Selamat Datang di Sistem WMS Dilwali</h3>
            <p style="line-height: 1.8; color: #666;">
              Sistem Warehouse Management System (WMS) yang terintegrasi untuk mengelola inventory, 
              laporan operasional, kebersihan gudang, dan status defect barang secara real-time. 
              Pilih menu di sidebar untuk mulai bekerja.
            </p>
          </div>
        </div>

        <!-- Inventory Section -->
        <div id="inventorySection" class="section-content">
          <div class="config-section">
            <h3>⚙️ Konfigurasi Google Sheets</h3>
            <div class="config-input">
              <label>URL Google Apps Script:</label>
              <input id="apiUrl" type="text" placeholder="Masukkan URL Web App (/exec) di sini" value="https://script.google.com/macros/s/AKfycbzkCElaoI9fxJaIptSjgddlbs73dPtq6Mc8TMta86dts0rpf8noAYW1Cy82fn3nklcxag/exec">
            </div>
            <div style="display:flex;gap:10px;flex-wrap:wrap">
              <button class="btn-primary" onclick="saveConfig()">💾 Simpan Konfigurasi</button>
              <button class="btn-success" onclick="loadData()">🔄 Muat Data dari Sheets</button>
            </div>
          </div>

          <div class="toolbar">
            <button class="btn-success" onclick="alert('Fitur Tambah Produk')">➕ Tambah Produk</button>
            <button class="btn-info" onclick="alert('Fitur Hitung Otomatis')">🔄 Hitung Otomatis</button>
            <button class="btn-warning" onclick="alert('Fitur Simpan ke Sheets')">💾 Simpan ke Sheets</button>
            <button class="btn-primary" onclick="alert('Fitur Export Excel')">📊 Export Excel</button>
            <button class="btn-danger" onclick="alert('Fitur Download Excel')">⬇️ Download Excel</button>
            <button class="btn-danger" onclick="if(confirm('Hapus semua data?')) alert('Data dihapus')">🗑️ Delete Semua Data</button>
          </div>

          <table id="inventoryTable">
            <thead>
              <tr>
                <th>No</th><th>Kode Barang</th><th>Nama Barang</th><th>Stok Awal</th>
                <th>Terjual</th><th>Kembali</th><th>Tersedia</th><th>Selisih</th>
                <th>Status</th><th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tableBody">
              <tr><td colspan="10" class="loading">📭 Belum ada data. Klik "Muat Data dari Sheets".</td></tr>
            </tbody>
          </table>
        </div>

        <!-- Laporan Kebersihan Section -->
        <div id="kebersihanSection" class="section-content">
          <div class="kebersihan-section">
            <h3>🧹 Laporan Kebersihan Gudang</h3>
            <p style="color: #666; margin-bottom: 20px;">
              Dokumentasi foto kebersihan seluruh area gudang dan lantai kerja
            </p>
            
            <div class="photo-grid">
              <div class="photo-item">
                <div class="icon">📸</div>
                <a href="https://drive.google.com/drive/folders/area-gudang-utama" target="_blank">
                  Area Gudang Utama
                </a>
              </div>
              <div class="photo-item">
                <div class="icon">📸</div>
                <a href="https://drive.google.com/drive/folders/lantai-1" target="_blank">
                  Lantai 1
                </a>
              </div>
              <div class="photo-item">
                <div class="icon">📸</div>
                <a href="https://drive.google.com/drive/folders/lantai-2" target="_blank">
                  Lantai 2
                </a>
              </div>
              <div class="photo-item">
                <div class="icon">📸</div>
                <a href="https://drive.google.com/drive/folders/area-packing" target="_blank">
                  Area Packing
                </a>
              </div>
              <div class="photo-item">
                <div class="icon">📸</div>
                <a href="https://drive.google.com/drive/folders/area-loading" target="_blank">
                  Area Loading
                </a>
              </div>
              <div class="photo-item">
                <div class="icon">📸</div>
                <a href="https://drive.google.com/drive/folders/toilet-ruang-istirahat" target="_blank">
                  Toilet & Ruang Istirahat
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Status Defect Section -->
        <div id="defectSection" class="section-content">
          <div class="stats-grid">
            <div class="stat-card">
              <h3>⚠️ Defect Jual Murah</h3>
              <div class="value" id="defectJualDetail">0</div>
              <div class="label">Unit tersedia untuk dijual dengan harga diskon</div>
            </div>
            <div class="stat-card">
              <h3>🔧 Defect Perbaikan</h3>
              <div class="value" id="defectPerbaikanDetail">0</div>
              <div class="label">Unit sedang dalam proses perbaikan</div>
            </div>
            <div class="stat-card">
              <h3>🗑️ Defect Hancur</h3>
              <div class="value" id="defectHancurDetail">0</div>
              <div class="label">Unit tidak dapat diperbaiki/dijual</div>
            </div>
          </div>

          <div class="config-section">
            <h3>📋 Detail Status Defect Barang</h3>
            <table>
              <thead>
                <tr>
                  <th>No</th>
                  <th>Kode Barang</th>
                  <th>Nama Barang</th>
                  <th>Kategori Defect</th>
                  <th>Jumlah</th>
                  <th>Keterangan</th>
                  <th>Tanggal Update</th>
                </tr>
              </thead>
              <tbody id="defectTableBody">
                <tr><td colspan="7" class="loading">📭 Belum ada data defect.</td></tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Customer Service Section -->
        <div id="customerServiceSection" class="section-content">
          <div class="config-section">
            <h3>👥 Divisi Customer Service</h3>
            <p style="color: #666;">Fitur Customer Service akan segera tersedia...</p>
          </div>
        </div>

      </div>
    </div>
  </div>

  <script>
    // LOGIN
    const validUsername = "admin";
    const validPassword = "admin1234";

    function login() {
      const username = document.getElementById("username").value.trim();
      const password = document.getElementById("password").value.trim();
      const errorMsg = document.getElementById("errorMsg");

      if (username === validUsername && password === validPassword) {
        document.getElementById("loginPage").style.display = "none";
        document.getElementById("mainApp").style.display = "flex";
        errorMsg.style.display = "none";
        updateDateTime();
        setInterval(updateDateTime, 1000);
      } else {
        errorMsg.style.display = "block";
      }
    }

    function logout() {
      if (confirm("Apakah Anda yakin ingin logout?")) {
        document.getElementById("mainApp").style.display = "none";
        document.getElementById("loginPage").style.display = "flex";
        document.getElementById("username").value = "";
        document.getElementById("password").value = "";
      }
    }

    // DATE TIME UPDATE
    function updateDateTime() {
      const now = new Date();
      const days = ['Minggu', 'Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu'];
      const months = ['Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni', 'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'];
      
      const dayName = days[now.getDay()];
      const date = now.getDate();
      const month = months[now.getMonth()];
      const year = now.getFullYear();
      
      const hours = String(now.getHours()).padStart(2, '0');
      const minutes = String(now.getMinutes()).padStart(2, '0');
      const seconds = String(now.getSeconds()).padStart(2, '0');
      
      document.getElementById('currentDate').textContent = `${dayName}, ${date} ${month} ${year}`;
      document.getElementById('currentTime').textContent = `${hours}:${minutes}:${seconds}`;
    }

    // SUBMENU TOGGLE
    function toggleSubmenu(event, submenuId) {
      event.preventDefault();
      const submenu = document.getElementById(submenuId);
      const menuItem = event.currentTarget.parentElement;
      const isOpen = submenu.style.display === "block";
      
      submenu.style.display = isOpen ? "none" : "block";
      menuItem.classList.toggle("open", !isOpen);
    }

    // SHOW SECTION
    function showSection(sectionName) {
      // Hide all sections
      const sections = document.querySelectorAll('.section-content');
      sections.forEach(section => section.classList.remove('active'));
      
      // Remove active class from all menu items
      const menuItems = document.querySelectorAll('.sidebar a');
      menuItems.forEach(item => item.classList.remove('active'));
      
      // Show selected section
      let sectionId = '';
      let pageTitle = '';
      
      switch(sectionName) {
        case 'dashboard':
          sectionId = 'dashboardSection';
          pageTitle = 'Dashboard Utama';
          updateDashboardStats();
          break;
        case 'inventory':
          sectionId = 'inventorySection';
          pageTitle = 'Inventory Booth - Divisi Gudang';
          break;
        case 'kebersihan':
          sectionId = 'kebersihanSection';
          pageTitle = 'Laporan Kebersihan Gudang';
          break;
        case 'defect':
          sectionId = 'defectSection';
          pageTitle = 'Status Defect Barang';
          updateDefectStats();
          break;
        case 'customer-service':
          sectionId = 'customerServiceSection';
          pageTitle = 'Divisi Customer Service';
          break;
        default:
          sectionId = 'dashboardSection';
          pageTitle = 'Dashboard Utama';
      }
      
      document.getElementById(sectionId).classList.add('active');
      document.getElementById('pageTitle').textContent = pageTitle;
      
      // Set active menu item
      event.target.classList.add('active');
    }

    // UPDATE DASHBOARD STATS
    function updateDashboardStats() {
      // Sample data - replace with actual data from your system
      document.getElementById('totalInventory').textContent = '830';
      document.getElementById('defectJual').textContent = '644';
      document.getElementById('defectPerbaikan').textContent = '186';
      document.getElementById('defectHancur').textContent = '0';
    }

    // UPDATE DEFECT STATS
    function updateDefectStats() {
      document.getElementById('defectJualDetail').textContent = '644';
      document.getElementById('defectPerbaikanDetail').textContent = '186';
      document.getElementById('defectHancurDetail').textContent = '0';
      
      // Sample defect data
      const defectData = [
        { kode: 'BRG001', nama: 'Booth Type A', kategori: 'Jual Murah', jumlah: 644, keterangan: 'Goresan ringan', tanggal: '15 Okt 2025' },
        { kode: 'BRG002', nama: 'Booth Type B', kategori: 'Perbaikan', jumlah: 186, keterangan: 'Engsel rusak', tanggal: '15 Okt 2025' },
        { kode: 'BRG003', nama: 'Booth Type C', kategori: 'Hancur', jumlah: 0, keterangan: 'Tidak dapat diperbaiki', tanggal: '15 Okt 2025' },
        { kode: 'BRG004', nama: 'Booth Type A', kategori: 'Jual Murah', jumlah: 0, keterangan: 'Cat mengelupas', tanggal: '15 Okt 2025' },
        { kode: 'BRG005', nama: 'Booth Type D', kategori: 'Perbaikan', jumlah: 0, keterangan: 'Roda macet', tanggal: '15 Okt 2025' },
      ];
      
      const tbody = document.getElementById('defectTableBody');
      tbody.innerHTML = '';
      
      defectData.forEach((item, index) => {
        const row = tbody.insertRow();
        row.innerHTML = `
          <td>${index + 1}</td>
          <td>${item.kode}</td>
          <td>${item.nama}</td>
          <td><span style="padding: 5px 10px; border-radius: 4px; font-size: 12px; font-weight: 600; 
            background: ${item.kategori === 'Jual Murah' ? '#fef3c7' : item.kategori === 'Perbaikan' ? '#dbeafe' : '#fee2e2'};
            color: ${item.kategori === 'Jual Murah' ? '#d97706' : item.kategori === 'Perbaikan' ? '#2563eb' : '#dc2626'};">
            ${item.kategori}
          </span></td>
          <td><strong>${item.jumlah}</strong></td>
          <td>${item.keterangan}</td>
          <td>${item.tanggal}</td>
        `;
      });
    }

    // CONFIG & DATA FUNCTIONS (Placeholder)
    function saveConfig() {
      const apiUrl = document.getElementById('apiUrl').value;
      if (apiUrl) {
        alert('✅ Konfigurasi berhasil disimpan!');
      } else {
        alert('❌ Harap masukkan URL Google Apps Script!');
      }
    }

    function loadData() {
      const apiUrl = document.getElementById('apiUrl').value;
      if (!apiUrl) {
        alert('❌ Harap konfigurasi URL terlebih dahulu!');
        return;
      }
      
      // Simulate loading
      const tbody = document.getElementById('tableBody');
      tbody.innerHTML = '<tr><td colspan="10" class="loading">⏳ Memuat data dari Google Sheets...</td></tr>';
      
      setTimeout(() => {
        tbody.innerHTML = '<tr><td colspan="10" class="loading">✅ Data berhasil dimuat! (Contoh data akan muncul di sini)</td></tr>';
      }, 1500);
    }

    // Initialize on page load
    document.addEventListener('DOMContentLoaded', function() {
      // Set initial datetime if logged in
      if (document.getElementById('mainApp').style.display !== 'none') {
        updateDateTime();
        setInterval(updateDateTime, 1000);
      }
    });
  </script>
</body>
</html>
        
