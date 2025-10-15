# Web-Operasional-Surprice
Web App untuk Monitoring Pekerjaan Tim 
[Task10.htm](https://github.com/user-attachments/files/22741692/Task10.htm)
<html lang="id">
<script>
const validUsername = "admin";
const validPassword = "admin1234";

function login() {
  const username = document.getElementById("username").value.trim();
  const password = document.getElementById("password").value.trim();
  const errorMsg = document.getElementById("errorMsg");

  if(username === validUsername && password === validPassword){
    // Login sukses
    document.getElementById("loginPage").style.display = "none";
    document.getElementById("mainApp").style.display = "flex";
    errorMsg.style.display = "none";
  } else {
    // Login gagal
    errorMsg.style.display = "block";
  }
}

// Logout
function logout(){
  document.getElementById("mainApp").style.display = "none";
  document.getElementById("loginPage").style.display = "flex";
}

// Ganti section di sidebar
function showSection(sectionId){
  // Sembunyikan semua section
  document.querySelectorAll(".section-content").forEach(sec => sec.classList.remove("active"));
  
  // Tampilkan section yang dipilih
  if(sectionId === "inventory") document.getElementById("inventorySection").classList.add("active");
  // Tambahkan section lain jika ada
  document.getElementById("pageTitle").textContent = sectionId.charAt(0).toUpperCase() + sectionId.slice(1);
}

// ================= Inventory =====================
// Contoh data array untuk testing
let inventoryData = [];

// Load data dummy / dari Sheets nanti
function loadData() {
  // Hapus pesan loading
  const tbody = document.getElementById("tableBody");
  tbody.innerHTML = "";

  // Contoh data dummy
  inventoryData = [
    {kode:"KFC5003", nama:"Surprice Set Toples Emas 3pcs", stokAwal:3, terjual:2, kembali:0},
    {kode:"PTT5601", nama:"Surprice Set Toples Emas 3pcs", stokAwal:3, terjual:0, kembali:0}
  ];

  inventoryData.forEach((item, index) => {
    const tersisa = item.stokAwal - item.terjual + item.kembali;
    const selisih = tersisa - (item.stokAwal - item.terjual);
    const tr = document.createElement("tr");
    tr.innerHTML = `
      <td>${index+1}</td>
      <td>${item.kode}</td>
      <td>${item.nama}</td>
      <td>${item.stokAwal}</td>
      <td>${item.terjual}</td>
      <td>${item.kembali}</td>
      <td>${tersisa}</td>
      <td>${selisih}</td>
      <td class="badge badge-success">OK</td>
      <td><button onclick="alert('Edit belum tersedia')">✏️</button></td>
    `;
    tbody.appendChild(tr);
  });
}

// Tombol hitung otomatis
function hitungOtomatis(){
  inventoryData.forEach((item, index)=>{
    item.tersisa = item.stokAwal - item.terjual + item.kembali;
    item.selisih = item.tersisa - (item.stokAwal - item.terjual);
  });
  loadData();
}

// Tambah produk (modal dummy)
function openModalTambah(){
  alert("Fungsi tambah produk akan segera dibuat");
}

// Simpan ke Sheets (dummy)
function simpanKeSheets(){
  alert("Fungsi simpan ke Sheets akan segera dibuat");
}

// Export Excel dummy
function exportExcel(){
  alert("Export Excel belum diaktifkan");
}

// Download Excel dummy
function downloadExcel(){
  alert("Download Excel belum diaktifkan");
}

// Delete semua data
function deleteAllData(){
  if(confirm("Apakah yakin ingin menghapus semua data?")){
    inventoryData = [];
    document.getElementById("tableBody").innerHTML = '<tr><td colspan="10" class="loading">📭 Belum ada data. Klik "Muat Data dari Sheets".</td></tr>';
  }
}
</script>

<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Sistem Inventory Booth - Dilwali</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.31/jspdf.plugin.autotable.min.js"></script>
<style>
body{font-family:"Segoe UI",Tahoma,Geneva,Verdana,sans-serif;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);margin:0;padding:0;color:#333;}
.container{max-width:1400px;margin:0 auto;background:#fff;border-radius:0;overflow:hidden;box-shadow:0 0 50px rgba(0,0,0,0.2);display:flex;min-height:100vh;}
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
.sidebar{width:250px;background:linear-gradient(180deg,#667eea 0%,#764ba2 100%);color:#fff;padding:20px 0;position:fixed;height:100vh;overflow-y:auto;box-shadow:2px 0 10px rgba(0,0,0,0.1);z-index:1000;}
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
.config-section{background:#fff3cd;border:2px solid #ffc107;padding:18px;margin:18px 0;border-radius:10px;}
.config-input{display:flex;gap:10px;align-items:center;margin-bottom:10px;}
.config-input label{min-width:160px;font-weight:700;}
input[type="text"]{flex:1;padding:10px;border:1px solid #d0d0d0;border-radius:8px;font-size:14px;}
.toolbar{padding:18px;display:flex;gap:12px;flex-wrap:wrap;border-bottom:1px solid #eee;background:#fff;border-radius:10px;margin-bottom:20px;}
button{padding:10px 16px;border-radius:8px;border:0;font-weight:700;cursor:pointer;transition:background 0.3s;}
.btn-primary{background:#667eea;color:#fff;}.btn-success{background:#10b981;color:#fff;}.btn-warning{background:#f59e0b;color:#fff;}.btn-danger{background:#ef4444;color:#fff;}.btn-info{background:#06b6d4;color:#fff;}
button:hover{opacity:0.9;}
.summary-cards{display:flex;gap:12px;padding:18px;flex-wrap:wrap;background:#fff;border-radius:10px;margin-bottom:20px;}
.card{flex:1;background:linear-gradient(135deg,#667eea,#764ba2);color:#fff;padding:14px;border-radius:10px;text-align:center;min-width:150px;}
table{width:100%;border-collapse:collapse;background:#fff;border-radius:10px;overflow:hidden;box-shadow:0 2px 10px rgba(0,0,0,0.05);}
th{background:#667eea;color:#fff;padding:12px;text-align:left;}
td{padding:10px;border-bottom:1px solid #eee;vertical-align:middle;}
input[type="number"]{width:80px;padding:6px;border-radius:6px;border:1px solid #ddd;text-align:center;}
.badge{display:inline-block;padding:6px 10px;border-radius:12px;font-weight:700;}
.badge-success{background:#d1fae5;color:#065f46;}.badge-warning{background:#fef3c7;color:#92400e;}.badge-danger{background:#fee2e2;color:#991b1b;}
.loading{padding:30px;text-align:center;color:#667eea;}
.modal{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);align-items:center;justify-content:center;z-index:999;}
.modal.active{display:flex;}
.modal-box{background:#fff;padding:20px;border-radius:10px;max-width:420px;width:95%;}
.placeholder{background:#fff;padding:40px;border-radius:10px;text-align:center;box-shadow:0 2px 10px rgba(0,0,0,0.05);margin:20px 0;}
.placeholder h2{color:#667eea;margin-bottom:20px;}
.logout-btn{position:absolute;bottom:20px;left:20px;width:calc(100% - 40px);background:#ef4444;color:#fff;padding:12px;border-radius:8px;border:none;cursor:pointer;font-weight:600;}
.logout-btn:hover{background:#dc2626;}
@media (max-width:768px){.sidebar{width:100%;height:auto;position:relative;margin-bottom:20px;}.main-content{margin-left:0;}.config-input{flex-direction:column;align-items:flex-start;}.input[type="text"]{width:100%;}.summary-cards{flex-direction:column;}}
</style>
</head>
<body>
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

<div id="mainApp" class="container" style="display:none;">
  <nav class="sidebar">
    <h3>🏢 Dashboard Divisi</h3>
    <ul>
      <li><a href="#" onclick="showSection('inventory')" class="active">📦 Divisi Gudang</a>
        <ul style="padding-left:20px;">
          <li><a href="#" onclick="showSection('inventory')"> - Inventory Booth</a></li>
          <style>
  ul {
    list-style-type: none;
    padding-left: 0;
    margin: 0;
  }

  a {
    text-decoration: none;
    color: #333;
    cursor: pointer;
    font-family: Arial, sans-serif;
  }

  a:hover {
    color: #007bff;
  }

  .submenu {
    display: none;
    margin-left: 25px;
    margin-top: 5px;
  }

  .arrow {
    font-size: 14px;
    transition: transform 0.2s ease;
  }

  .open .arrow {
    transform: rotate(90deg);
  }
</style>

<ul>
  <li id="laporan-gudang-menu">
    <a href="#" onclick="toggleSubmenu(event)">
      📦 - Laporan Gudang <span class="arrow">▶</span>
    </a>
    <ul id="submenu-laporan-gudang" class="submenu">
      <li>
        <a href="https://docs.google.com/spreadsheets/d/14phSwmbLXDSVpc1wBo9NZdz9yV1VIOutwBySSQNewJ8/edit" target="_blank">
          🧾 V.2 Log Aktivitas Operasional Surprice 2025
        </a>
       <li>
        <a href="https://docs.google.com/spreadsheets/d/1XET5ZuVH10Yt4dhVxioCe1jww5-cWfjC/edit?gid=2037484461#gid=2037484461" target="_blank">
          📊 Laporan_Operasional_Surprice2025
        </a>
      </ul>
  </ul>

<script>
  function toggleSubmenu(event) {
    event.preventDefault();
    const menuItem = document.getElementById("laporan-gudang-menu");
    const submenu = document.getElementById("submenu-laporan-gudang");

    const isOpen = submenu.style.display === "block";
    submenu.style.display = isOpen ? "none" : "block";
    menuItem.classList.toggle("open", !isOpen);
  }
</script>

      </li>
      <li><a href="#" onclick="showSection('customer-service')">👥 Divisi Customer Service</a>
        <ul style="padding-left:20px;">
          <li><a href="#" onclick="showSection('keluhan')"> - Keluhan Pelanggan</a></li>
          <li><a href="#" onclick="showSection('support')"> - Support Tiket</a></li>
          <li><a href="#" onclick="showSection('feedback')"> - Feedback Survey</a></li>
        </ul>
      </li>
      <li><a href="#" onclick="showSection('marketing')">📈 Divisi Marketing & Sales Digital</a>
        <ul style="padding-left:20px;">
          <li><a href="#" onclick="showSection('kampanye')"> - Kampanye Digital</a></li>
          <li><a href="#" onclick="showSection('sales-report')"> - Laporan Sales</a></li>
          <li><a href="#" onclick="showSection('lead-management')"> - Manajemen Lead</a></li>
        </ul>
      </li>
      <li><a href="#" onclick="showSection('admin')">⚙️ Divisi Admin & Purchasing</a>
        <ul style="padding-left:20px;">
          <li><a href="#" onclick="showSection('pembelian')"> - Pembelian Barang</a></li>
          <li><a href="#" onclick="showSection('admin-report')"> - Laporan Admin</a></li>
          <li><a href="#" onclick="showSection('vendor')"> - Manajemen Vendor</a></li>
        </ul>
      </li>
      <li><a href="#" onclick="showSection('transporter')">🚚 Divisi Transporter</a>
        <ul style="padding-left:20px;">
          <li><a href="#" onclick="showSection('jadwal-pengiriman')"> - Jadwal Pengiriman</a></li>
          <li><a href="#" onclick="showSection('tracking')"> - Tracking Kendaraan</a></li>
          <li><a href="#" onclick="showSection('maintenance')"> - Maintenance</a></li>
        </ul>
      </li>
      <li><a href="#" onclick="showSection('kurir')">📬 Divisi Kurir</a>
        <ul style="padding-left:20px;">
          <li><a href="#" onclick="showSection('pengiriman-paket')"> - Pengiriman Paket</a></li>
          <li><a href="#" onclick="showSection('lacak-paket')"> - Lacak Paket</a></li>
          <li><a href="#" onclick="showSection('laporan-kurir')"> - Laporan Harian</a></li>
        </ul>
      </li>
      <li><a href="#" onclick="showSection('it')">💻 Divisi IT</a>
        <ul style="padding-left:20px;">
          <li><a href="#" onclick="showSection('maintenance-it')"> - Maintenance Sistem</a></li>
          <li><a href="#" onclick="showSection('security')"> - Keamanan Data</a></li>
          <li><a href="#" onclick="showSection('development')"> - Pengembangan Aplikasi</a></li>
          <li><a href="#" onclick="showSection('helpdesk')"> - Helpdesk IT</a></li>
          <li><a href="#" onclick="showSection('backup')"> - Backup & Recovery</a></li>
        </ul>
      </li>
    </ul>
    <button class="logout-btn" onclick="logout()">🚪 Logout</button>
  
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
        <div style="margin-top:8px;font-size:13px;color:#444">Pastikan Apps Script sudah <strong>deploy sebagai Web App</strong> (Execute as: <em>Me</em>, Who has access: <em>Anyone</em>)</div>
      </div>

      <div class="toolbar">
        <div style="flex:1">
          <button class="btn-success" onclick="openModalTambah()">➕ Tambah Produk</button>
          <button class="btn-info" onclick="hitungOtomatis()">🔄 Hitung Otomatis</button>
          <button class="btn-warning" onclick="simpanKeSheets()">💾 Simpan ke Sheets</button>
          <button class="btn-primary" onclick="exportExcel()">📊 Export Excel</button>
          <button class="btn-danger" onclick="downloadExcel()">⬇️ Download Excel</button>
          <button class="btn-danger" onclick="deleteAllData()">🗑️ Delete Semua Data</button>
        </div>
      </div>

      <div class="summary-cards" id="summaryCards">
        <div class="card"><div style="opacity:.9">Total Item</div><div id="totalItem" style="font-size:20px">0</div></div>
        <div class="card"><div style="opacity:.9">Stok Awal</div><div id="stokAwal" style="font-size:20px">0</div></div>
        <div class="card"><div style="opacity:.9">Terjual</div><div id="totalTerjual" style="font-size:20px">0</div></div>
        <div class="card"><div style="opacity:.9">Kembali</div><div id="totalKembali" style="font-size:20px">0</div></div>
        <div class="card"><div style="opacity:.9">Tersedia</div><div id="stokTersedia" style="font-size:20px">0</div></div>
      </div>

      <div style="padding:18px">
        <div style="overflow:auto">
          <table id="inventoryTable">
            <thead>
              <tr>
                <th style="width:50px">No</th><th>Kode Barang</th><th>Nama Barang</th><th style="width:110px">Stok Awal</th>
                <th style="width:110px">Terjual</th><th style="width:110px">Kembali</th><th style="width:110px">Tersedia</th>
                <th style="width:90px">Selisih</th><th style="width:120px">Status</th><th style="width:90px">Aksi</th>
              </tr>
            </thead>
            <tbody id="tableBody">
              <tr><td colspan="10" class="loading">📭 Belum ada data. Klik "Muat Data dari Sheets".</td></tr>
            </tbody>
