# Web-Operasional-Surprice 2025
<html lang="id">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Sistem Inventory Booth - Dilwali</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.31/jspdf.plugin.autotable.min.js"></script>

  <style>
    body{font-family:"Segoe UI",Tahoma,Geneva,Verdana,sans-serif;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);margin:0;padding:0;color:#333;}
    .container{max-width:1400px;margin:0 auto;background:#fff;overflow:hidden;box-shadow:0 0 50px rgba(0,0,0,0.2);display:flex;min-height:100vh;}
    .login-page{display:flex;align-items:center;justify-content:center;width:100%;height:100vh;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);}
    .login-box{background:#fff;padding:40px;border-radius:14px;box-shadow:0 12px 40px rgba(0,0,0,0.18);width:100%;max-width:400px;text-align:center;}
    .login-box h2{margin:0 0 20px;color:#667eea;font-size:28px;}
    .form-group{margin-bottom:20px;text-align:left;}
    .form-group label{display:block;margin-bottom:5px;font-weight:600;color:#555;}
    input[type="text"],input[type="password"]{width:100%;padding:12px;border:2px solid #ddd;border-radius:8px;font-size:16px;transition:border-color 0.3s;}
    input[type="text"]:focus,input[type="password"]:focus{outline:none;border-color:#667eea;}
    .btn-login{width:100%;padding:12px;background:#667eea;color:#fff;border:none;border-radius:8px;font-size:16px;font-weight:600;cursor:pointer;transition:background 0.3s;}
    .btn-login:hover{background:#5a67d8;}
    .error-msg{color:#ef4444;font-size:14px;margin-top:10px;}
    .sidebar{width:250px;background:linear-gradient(180deg,#667eea 0%,#764ba2 100%);color:#fff;padding:20px 0;position:fixed;height:100vh;overflow-y:auto;box-shadow:2px 0 10px rgba(0,0,0,0.1);}
    .sidebar h3{padding:0 20px;margin:20px 0 10px;font-size:18px;border-bottom:1px solid rgba(255,255,255,0.2);}
    .sidebar ul{list-style:none;padding:0;margin:0;}
    .sidebar li{margin:0;}
    .sidebar a{display:block;padding:12px 20px;color:#fff;text-decoration:none;transition:background 0.3s;border-left:3px solid transparent;}
    .sidebar a:hover,.sidebar a.active{background:rgba(255,255,255,0.1);border-left-color:#fff;}
    .main-content{flex:1;margin-left:250px;padding:20px;background:#f8f9fa;}
    .header{background:#fff;padding:20px;text-align:center;border-bottom:1px solid #eee;margin-bottom:20px;border-radius:10px;box-shadow:0 2px 10px rgba(0,0,0,0.05);}
    .header h1{margin:0;font-size:28px;color:#667eea;}
    .section-content{display:none;}
    .section-content.active{display:block;}
    .submenu{display:none;margin-left:25px;margin-top:5px;}
    .arrow{font-size:14px;transition:transform 0.2s ease;}
    .open .arrow{transform:rotate(90deg);}
    .logout-btn{position:absolute;bottom:20px;left:20px;width:calc(100% - 40px);background:#ef4444;color:#fff;padding:12px;border-radius:8px;border:none;cursor:pointer;font-weight:600;}
    .logout-btn:hover{background:#dc2626;}
  </style>
</head>

<body>
  <!-- Login Page -->
  <div id="loginPage" class="login-page">
    <div class="login-box">
      <h2>🔐 Login Sistem Inventory</h2>
      <p style="color:#666;margin-bottom:20px;">Username: admin | Password: admin1234</p>
      <div class="form-group">
        <label>Username:</label>
        <input id="username" type="text" placeholder="Masukkan username">
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input id="password" type="password" placeholder="Masukkan password">
      </div>
      <button class="btn-login" onclick="login()">Login</button>
      <div id="errorMsg" class="error-msg" style="display:none;">Username atau password salah!</div>
    </div>
  </div>

  <!-- Main App -->
  <div id="mainApp" class="container" style="display:none;">
    <nav class="sidebar">
      <h3>🏢 Dashboard Divisi</h3>
      <ul>
        <li>
          <a href="#" onclick="showSection('inventory')" class="active">📦 Divisi Gudang</a>
          <ul style="padding-left:20px;">
            <li><a href="#" onclick="showSection('inventory')"> - Inventory Booth</a></li>
            <li id="laporan-gudang-menu">
              <a href="#" onclick="toggleSubmenu(event)">
                🧾 - Laporan Gudang <span class="arrow">▶</span>
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

        <li><a href="#" onclick="showSection('customer-service')">👥 Divisi Customer Service</a>
          <ul style="padding-left:20px;">
            <li><a href="#"> - Keluhan Pelanggan</a></li>
            <li><a href="#"> - Support Tiket</a></li>
            <li><a href="#"> - Feedback Survey</a></li>
          </ul>
        </li>

        <li><a href="#">📈 Divisi Marketing & Sales Digital</a></li>
        <li><a href="#">⚙️ Divisi Admin & Purchasing</a></li>
        <li><a href="#">🚚 Divisi Transporter</a></li>
        <li><a href="#">📬 Divisi Kurir</a></li>
        <li><a href="#">💻 Divisi IT</a></li>
      </ul>

      <button class="logout-btn" onclick="logout()">🚪 Logout</button>
    </nav>

    <div class="main-content">
      <div class="header">
        <h1 id="pageTitle">Selamat Datang di Sistem Inventory</h1>
      </div>

      <div id="inventorySection" class="section-content active">
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
          <button class="btn-success" onclick="openModalTambah()">➕ Tambah Produk</button>
          <button class="btn-info" onclick="hitungOtomatis()">🔄 Hitung Otomatis</button>
          <button class="btn-warning" onclick="simpanKeSheets()">💾 Simpan ke Sheets</button>
          <button class="btn-primary" onclick="exportExcel()">📊 Export Excel</button>
          <button class="btn-danger" onclick="downloadExcel()">⬇️ Download Excel</button>
          <button class="btn-danger" onclick="deleteAllData()">🗑️ Delete Semua Data</button>
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
      } else {
        errorMsg.style.display = "block";
      }
    }

    function logout() {
      document.getElementById("mainApp").style.display = "none";
      document.getElementById("loginPage").style.display = "flex";
    }

    // SUBMENU LAPORAN GUDANG
    function toggleSubmenu(event) {
      event.preventDefault();
      const menuItem = document.getElementById("laporan-gudang-menu");
      const submenu = document.getElementById("submenu-laporan-gudang");
      const isOpen = submenu.style.display === "block";
      submenu.style.display = isOpen ? "none" : "block";
      menuItem.classList.toggle("open", !isOpen);
    }
  </script>
  <footer style="
  text-align: center;
  padding: 15px;
  background-color: #f4f4f4;
  color: #555;
  font-size: 14px;
  border-top: 1px solid #ddd;
  margin-top: 30px;
">
  © 2025 Sendi_Muchdianto. All rights reserved.
</footer>

</body>
</html>
