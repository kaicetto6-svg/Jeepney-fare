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
    label, select, input, button {
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
    .info {
      font-size: 14px;
      color: #666;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="card">
    <h2>Jeepney Fare Calculator</h2><label for="route">Route (e.g. Wawa - San Jose):</label>
<input type="text" id="route" placeholder="e.g. Wawa - San Jose">

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
<div class="info">
  Valid barangays: Bagumbayan, San Jose, Matungao, Panginay (Guiguinto), Panginay (Balagtas), Wawa, Longos, Borol 1st, Borol 2nd, Tibag, San Juan, Sto. Rosario, Sta. Ana
</div>

  </div>  <script>
    const barangayList = [
      "bagumbayan",
      "san jose",
      "matungao",
      "panginay (guiguinto)",
      "panginay (balagtas)",
      "wawa",
      "longos",
      "borol 1st",
      "borol 2nd",
      "tibag",
      "san juan",
      "sto. rosario",
      "sta. ana"
    ];

    function normalize(str) {
      return str.trim().toLowerCase();
    }

    function calculateFare() {
      const routeInput = document.getElementById('route').value;
      const [fromRaw, toRaw] = routeInput.split('-').map(s => normalize(s || ""));
      const passengerType = document.getElementById('passengerType').value;
      const passengerCount = parseInt(document.getElementById('passengerCount').value);
      const cash = parseInt(document.getElementById('cash').value);

      const fromIndex = barangayList.indexOf(fromRaw);
      const toIndex = barangayList.indexOf(toRaw);

      const output = document.getElementById('output');

      if (fromIndex === -1 || toIndex === -1) {
        output.innerHTML = `❌ Invalid barangay name. Use format like: Wawa - San Jose`;
        return;
      }

      const barangaysTraveled = Math.abs(toIndex - fromIndex) + 1;
      const baseFare = passengerType === 'regular' ? 13 : 11;
      const extraBarangays = Math.max(0, barangaysTraveled - 4);
      const farePerPassenger = baseFare + (extraBarangays * 2);
      const totalFare = farePerPassenger * passengerCount;
      const change = cash - totalFare;

      if (change >= 0) {
        output.innerHTML = `Barangays Traveled: ${barangaysTraveled}<br>Total Fare: ₱${totalFare}<br>Change: ₱${change}`;
      } else {
        output.innerHTML = `Barangays Traveled: ${barangaysTraveled}<br>Total Fare: ₱${totalFare}<br>❌ Not enough cash (short ₱${-change})`;
      }
    }
  </script></body>
</html>
