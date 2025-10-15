<html lang="id">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Sistem Inventory Surprice</title>
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
    
    .submenu.show {
      display: block;
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

    /* Saved Sheets List */
    #savedSheets, #savedSheetsTransporter, #savedSheetsKurir, #savedSheetsFinance {
      list-style: none;
      padding: 0;
      margin-top: 20px;
    }
    
    #savedSheets li, #savedSheetsTransporter li, #savedSheetsKurir li, #savedSheetsFinance li {
      background: #f9f9f9;
      padding: 12px 15px;
      border-radius: 6px;
      margin-bottom: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border: 2px solid #e0e0e0;
    }
    
    #savedSheets li:hover, #savedSheetsTransporter li:hover, #savedSheetsKurir li:hover, #savedSheetsFinance li:hover {
      border-color: #FF6B00;
    }
    
    #savedSheets a, #savedSheetsTransporter a, #savedSheetsKurir a, #savedSheetsFinance a {
      color: #FF6B00;
      text-decoration: none;
      font-weight: 600;
    }
    
    #savedSheets button, #savedSheetsTransporter button, #savedSheetsKurir button, #savedSheetsFinance button {
      background: #ef4444;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 12px;
    }

    /* Footer Styles */
    .main-footer {
      background: #fff;
      padding: 40px 30px 20px;
      margin-top: 50px;
      border-top: 3px solid #FF6B00;
      box-shadow: 0 -2px 10px rgba(0,0,0,0.05);
    }
    
    .footer-content {
      max-width: 1200px;
      margin: 0 auto;
    }
    
    .partner-section {
      margin-bottom: 35px;
    }
    
    .partner-section h3 {
      color: #FF6B00;
      font-size: 18px;
      font-weight: 700;
      margin-bottom: 20px;
      text-align: center;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    
    .partner-logos {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 25px;
      flex-wrap: wrap;
    }
    
    .partner-logo {
      background: #f9f9f9;
      padding: 15px 20px;
      border-radius: 8px;
      transition: all 0.3s;
      border: 2px solid #e0e0e0;
      display: flex;
      align-items: center;
      justify-content: center;
      min-width: 120px;
      height: 60px;
    }
    
    .partner-logo:hover {
      transform: translateY(-5px);
      box-shadow: 0 6px 20px rgba(255, 107, 0, 0.15);
      border-color: #FF6B00;
    }
    
    .partner-logo img {
      max-width: 100%;
      max-height: 40px;
      object-fit: contain;
    }
    
    .divider {
      height: 2px;
      background: linear-gradient(to right, transparent, #FF6B00, transparent);
      margin: 30px 0;
    }
    
    .copyright {
      text-align: center;
      color: #666;
      font-size: 14px;
      padding-top: 20px;
      border-top: 1px solid #e0e0e0;
    }
    
    .copyright strong {
      color: #FF6B00;
      font-weight: 600;
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
      
      .footer-content {
        flex-direction: column;
        text-align: center;
      }
      
      .partner-logos {
        justify-content: center;
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
        <h2>📦 SURPRICE WMS</h2>
        <p>Warehouse Management System</p>
      </div>
      
      <div class="sidebar-content">
        <h3>🏢 Dashboard Divisi</h3>
        <ul>
          <li>
            <a href="#" onclick="showSection(event, 'dashboard')" class="active">🏠 Dashboard Utama</a>
          </li>
          
          <li>
            <a href="#" onclick="showSection(event, 'inventory')">📦 Divisi Gudang</a>
            <ul style="padding-left:20px;">
              <li><a href="#" onclick="showSection(event, 'inventory')"> • Inventory Booth</a></li>
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
                  <li>
                    <a href="https://docs.google.com/spreadsheets/d/1rRnAGQWbnhlYo3OFHZwch6zWZx74oeDrhWyMg_os_18/edit?gid=1158692194#gid=1158692194" target="_blank">
                      📊 Laporan Barang Defect 2025
                    </a>
                  </li>
                </ul>
              </li>
              <li><a href="#" onclick="showSection(event, 'kebersihan')">🧹 • Laporan Kebersihan</a></li>
              <li><a href="#" onclick="showSection(event, 'defect')">⚠️ • Status Defect Barang</a></li>
            </ul>
          </li>

          <li>
            <a href="#" onclick="showSection(event, 'customer-service')">👥 Divisi Customer Service</a>
            <ul style="padding-left:20px;">
              <li>
                <a href="https://docs.google.com/spreadsheets/d/1T8coKtJPfxeLhOgo-CHHqJd5MOCs3xmCFIYkXB1ETi0/edit?gid=1946424206#gid=1946424206" target="_blank">
                  📊 Komplain Chat2025
                </a>
              </li>
            </ul>
          </li>

          <li>
            <a href="#" onclick="showSection(event, 'divisi-marketing')">📈 Divisi Marketing & Sales Digital</a>
          </li>

          <li>
            <a href="#" onclick="showSection(event, 'divisi-admin')">⚙️ Divisi Admin & Purchasing</a>
            <ul style="padding-left:20px;">
              <li>
                <a href="https://docs.google.com/spreadsheets/d/1ykt2z6HEhI3XAAezp3PYgMp9nHr4AxSfsOB5il_I8nU/edit?gid=0#gid=0" target="_blank">
                  📊 Laporan Tiktok dan Selisih Ongkir 2025
                </a>
              </li>
            </ul>
          </li>

          <li><a href="#" onclick="showSection(event, 'divisi-transporter')">🚚 Divisi Transporter</a></li>
          <li><a href="#" onclick="showSection(event, 'divisi-kurir')">📬 Divisi Kurir</a></li>
          <li><a href="#" onclick="showSection(event, 'divisi-finance')">💰 Divisi Finance</a></li>
          <li><a href="#" onclick="showSection(event, 'divisi-hrd')">👔 Divisi HRD</a></li>
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
          <div class="date" id="tanggal"></div>
          <div class="time" id="waktu"></div>
        </div>
      </div>

      <!-- Content Area -->
      <div class="content-area">
        
        <!-- Dashboard Section -->
        <div id="dashboardSection" class="section-content active">
          <div class="stats-grid">
            <div class="stat-card">
              <h3>📦 Total Inventory</h3>
              <div class="value" id="totalInventory">830</div>
              <div class="label">Item dalam sistem</div>
            </div>
            <div class="stat-card">
              <h3>⚠️ Defect Jual Murah</h3>
              <div class="value" id="defectJual">644</div>
              <div class="label">Unit</div>
            </div>
            <div class="stat-card">
              <h3>🔧 Defect Perbaikan</h3>
              <div class="value" id="defectPerbaikan">186</div>
              <div class="label">Unit</div>
            </div>
            <div class="stat-card">
              <h3>🗑️ Defect Hancur</h3>
              <div class="value" id="defectHancur">0</div>
              <div class="label">Unit</div>
            </div>
          </div>
          
          <div class="config-section">
            <h3>🎯 Selamat Datang di Sistem WMS Surprice</h3>
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
              <input id="apiUrl" type="text" placeholder="Masukkan URL Web App (/exec) di sini" value="">
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
            <button class="btn-danger" onclick="if(confirm('Hapus semua data?'))
