<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Jeepney Fare Calculator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #f2f2f2;
      color: #333;
    }
    .card {
      background: #fff;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      max-width: 400px;
      margin: auto;
    }
    label, select, button {
      display: block;
      width: 100%;
      margin: 10px 0;
      font-size: 16px;
    }
    button {
      padding: 10px;
      background-color: #4CAF50;
      border: none;
      color: white;
      border-radius: 8px;
      cursor: pointer;
    }
    .result {
      margin-top: 15px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="card">
    <h2>Jeepney Fare Calculator</h2><label for="barangays">Barangays Traveled:</label>
<select id="barangays">
  <option value="1">1</option>
  <option value="2">2</option>
  <option value="3">3</option>
  <option value="4" selected>4</option>
  <option value="5">5</option>
  <option value="6">6</option>
  <option value="7">7</option>
  <option value="8">8</option>
  <option value="9">9</option>
  <option value="10">10</option>
  <option value="11">11</option>
  <option value="12">12</option>
</select>

<label for="passengerType">Passenger Type:</label>
<select id="passengerType">
  <option value="regular">Regular</option>
  <option value="student">Senior/Student</option>
</select>

<label for="passengerCount">Number of Passengers:</label>
<select id="passengerCount">
  <option value="1" selected>1</option>
  <option value="2">2</option>
  <option value="3">3</option>
  <option value="4">4</option>
  <option value="5">5</option>
  <option value="6">6</option>
  <option value="7">7</option>
  <option value="8">8</option>
  <option value="9">9</option>
  <option value="10">10</option>
</select>

<label for="cash">Cash Given (₱):</label>
<select id="cash">
  <option value="20">₱20</option>
  <option value="50">₱50</option>
  <option value="100">₱100</option>
</select>

<button onclick="calculateFare()">Calculate</button>

<div class="result" id="output"></div>

  </div>  <script>
    function calculateFare() {
      const barangays = parseInt(document.getElementById('barangays').value);
      const passengerType = document.getElementById('passengerType').value;
      const passengerCount = parseInt(document.getElementById('passengerCount').value);
      const cash = parseInt(document.getElementById('cash').value);

      const baseFare = passengerType === 'regular' ? 13 : 11;
      const extraBarangays = Math.max(0, barangays - 4);
      const farePerPassenger = baseFare + (extraBarangays * 2);
      const totalFare = farePerPassenger * passengerCount;
      const change = cash - totalFare;

      const output = document.getElementById('output');
      if (change >= 0) {
        output.innerHTML = `Total Fare: ₱${totalFare} <br> Change: ₱${change}`;
      } else {
        output.innerHTML = `Total Fare: ₱${totalFare} <br> ❌ Not enough cash (short ₱${-change})`;
      }
    }
  </script></body>
</html
