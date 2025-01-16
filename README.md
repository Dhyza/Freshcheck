<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FoodCheck: Aman atau Tidak?</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      padding: 20px;
      background-color: #f9f9f9;
      color: #333;
    }
    h1 {
      color: #2a9d8f;
      text-align: center;
    }
    .container {
      max-width: 600px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
    label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      width: 100%;
      padding: 10px;
      background-color: #2a9d8f;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
    }
    button:hover {
      background-color: #21867a;
    }
    .result {
      margin-top: 20px;
      padding: 15px;
      border-radius: 5px;
    }
    .result.safe {
      background-color: #d4edda;
      color: #155724;
    }
    .result.unsafe {
      background-color: #f8d7da;
      color: #721c24;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>FoodCheck</h1>
    <form id="foodCheckForm">
      <label for="foodType">Jenis Makanan</label>
      <select id="foodType">
        <option value="sayuran">Sayuran</option>
        <option value="buah">Buah</option>
        <option value="daging">Daging</option>
      </select>
      
      <label for="expiryDate">Tanggal Kedaluwarsa</label>
      <input type="date" id="expiryDate" required>
      
      <label for="storageCondition">Kondisi Penyimpanan</label>
      <select id="storageCondition">
        <option value="kulkas">Kulkas (0-4°C)</option>
        <option value="ruang">Suhu Ruang</option>
      </select>
      
      <label for="physicalChange">Perubahan Fisik</label>
      <select id="physicalChange">
        <option value="ada">Ada perubahan</option>
        <option value="tidak">Tidak ada perubahan</option>
      </select>
      
      <button type="button" onclick="checkFood()">Cek Kelayakan</button>
    </form>
    <div id="result" class="result" style="display: none;"></div>
  </div>

  <script>
    function checkFood() {
      const expiryDate = new Date(document.getElementById('expiryDate').value);
      const storageCondition = document.getElementById('storageCondition').value;
      const physicalChange = document.getElementById('physicalChange').value;

      const today = new Date();
      const resultDiv = document.getElementById('result');
      resultDiv.style.display = 'block';

      if (expiryDate < today || physicalChange === 'ada') {
        resultDiv.className = 'result unsafe';
        resultDiv.innerText = '❌ Makanan tidak layak dikonsumsi!';
      } else {
        resultDiv.className = 'result safe';
        resultDiv.innerText = '✅ Makanan masih layak dikonsumsi!';
      }
    }

    // Alarm Reminder
    function setExpiryReminder() {
      const expiryDate = new Date(document.getElementById('expiryDate').value);
      const today = new Date();

      const timeDiff = expiryDate - today;
      if (timeDiff > 0) {
        setTimeout(() => {
          alert('⚠️ Pengingat: Makanan Anda mendekati batas kedaluwarsa!');
        }, timeDiff);
      }
    }

    document.getElementById('expiryDate').addEventListener('change', setExpiryReminder);
  </script>
</body>
</html>
# Freshcheck
