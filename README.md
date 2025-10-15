<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Web Operasional Surprice</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #f8fbff;
    color: #333;
    margin: 0;
  }

  header {
    background-color: #004aad;
    color: white;
    padding: 15px 25px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  header h1 {
    margin: 0;
    font-size: 22px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .datetime {
    font-size: 14px;
    color: #cce0ff;
  }

  nav {
    background-color: #e8f0ff;
    padding: 15px;
  }

  nav a {
    display: block;
    color: #004aad;
    text-decoration: none;
    font-weight: bold;
    margin: 8px 0;
  }

  nav a:hover {
    text-decoration: underline;
  }

  .content {
    padding: 20px;
  }

  .config-input {
    margin-bottom: 10px;
  }

  input {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    margin-bottom: 10px;
    border-radius: 6px;
    border: 1px solid #ccc;
  }

  button {
    padding: 8px 15px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-weight: bold;
  }

  .btn-primary {
    background-color: #004aad;
    color: white;
  }

  .btn-success {
    background-color: #2eb82e;
    color: white;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  ul li {
    margin-bottom: 5px;
  }

  ul li a {
    color: #004aad;
    text-decoration: none;
  }

  footer {
    background-color: #004aad;
    color: white;
    text-align: center;
    padding: 10px;
    margin-top: 40px;
    font-size: 13px;
  }
</style>
</head>

<body>

<header>
  <h1>
    <img src="https://upload.wikimedia.org/wikipedia/en/a/a9/Shopee_logo.svg" alt="Shopee" width="40">
    Web Operasional Surprice
  </h1>
  <div class="datetime" id="datetime"></div>
</header>

<nav>
  <a href="#" onclick="showSection('laporan-gudang')">📦 Laporan Gudang</a>
  <a href="#" onclick="showSection('divisi-admin')">
    <img src="https://cdn-icons-png.flaticon.com/512/3050/3050525.png" alt="Kurir" width="20" style="vertical-align: middle; margin-right: 5px;">
    Divisi Admin & Purchasing
  </a>
</nav>

<div class="content">
  <div id="divisi-admin" style="display:block;">
    <h3>🚚 Divisi Admin & Purchasing</h3>
    <div class="config-input">
      <label>Nama Laporan:</label>
      <input id="sheetName" type="text" placeholder="Masukkan nama laporan">

      <label>URL Google Sheets:</label>
      <input id="apiUrlAdmin" type="text" placeholder="Masukkan URL Google Sheets">
    </div>

    <button class="btn-primary" onclick="saveSheetUrl()">💾 Simpan URL</button>
    <button class="btn-success" onclick="showSavedSheets()">📋 Lihat Daftar</button>

    <ul id="savedSheets"></ul>
  </div>
</div>

<footer>
  Copyright © Sendi_Muchdianto 2025 | All Rights Reserved
</footer>

<script>
function updateDateTime() {
  const now = new Date();
  const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
  const time = now.toLocaleTimeString('id-ID');
  const date = now.toLocaleDateString('id-ID', options);
  document.getElementById('datetime').textContent = `${date} | ${time}`;
}
setInterval(updateDateTime, 1000);
updateDateTime();

function saveSheetUrl() {
  const name = document.getElementById('sheetName').value.trim();
  const url = document.getElementById('apiUrlAdmin').value.trim();
  if (!name || !url) return alert('Isi nama dan URL terlebih dahulu.');

  let sheets = JSON.parse(localStorage.getItem('savedSheets')) || [];
  sheets.push({ name, url });
  localStorage.setItem('savedSheets', JSON.stringify(sheets));

  document.getElementById('sheetName').value = '';
  document.getElementById('apiUrlAdmin').value = '';
  showSavedSheets();
}

function showSavedSheets() {
  const sheets = JSON.parse(localStorage.getItem('savedSheets')) || [];
  const list = document.getElementById('savedSheets');
  list.innerHTML = sheets.map((s, i) =>
    `<li>
      <a href="${s.url}" target="_blank">${s.name}</a>
      <button onclick="deleteSheet(${i})" style="margin-left:10px; background:#ff4d4d; color:white; border:none; border-radius:4px;">❌</button>
    </li>`
  ).join('');
}

function deleteSheet(i) {
  let sheets = JSON.parse(localStorage.getItem('savedSheets')) || [];
  sheets.splice(i, 1);
  localStorage.setItem('savedSheets', JSON.stringify(sheets));
  showSavedSheets();
}

function showSection(sectionId) {
  document.querySelectorAll('.content > div').forEach(div => div.style.display = 'none');
  document.getElementById(sectionId).style.display = 'block';
}

showSavedSheets();
</script>
</body>
</html>
