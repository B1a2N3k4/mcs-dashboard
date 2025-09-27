<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>MCS Task Dashboard</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      background: #f4f7fa;
      margin: 0;
      padding: 20px;
      color: #333;
    }
    h2 {
      text-align: center;
      color: #2c3e50;
      margin-bottom: 20px;
    }
    .card {
      background: #fff;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      padding: 20px;
      max-width: 1400px;
      margin: 0 auto 20px;
    }
    label {
      font-weight: bold;
      margin-right: 10px;
    }
    input {
      padding: 6px 10px;
      margin: 5px;
      border-radius: 6px;
      border: 1px solid #ccc;
    }
    button {
      padding: 8px 15px;
      margin: 10px 5px;
      border: none;
      border-radius: 6px;
      background: #3498db;
      color: #fff;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      background: #2980b9;
    }
    #status {
      margin: 10px 0;
      font-weight: bold;
      color: #16a085;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 15px;
      overflow: hidden;
      border-radius: 10px;
    }
    th {
      background: #3498db;
      color: white;
      padding: 12px;
      text-align: left;
    }
    td {
      padding: 10px;
      border-bottom: 1px solid #ddd;
    }

    /* highlight row colors */
    .row-error     { background-color: #ffb3b3 !important; } /* แดงอ่อน */
    .row-timeout-N { background-color: #c8f7c5 !important; } /* เขียวอ่อน */
    .row-timeout-Y { background-color: #ffe0b3 !important; } /* ส้มอ่อน */
    .row-alarm-Y   { background-color: #fff4b3 !important; } /* เหลืองอ่อน */
    
    pre {
      background: #2c3e50;
      color: #ecf0f1;
      padding: 10px;
      border-radius: 8px;
      max-height: 250px;
      overflow: auto;
    }
  </style>
</head>
<body>
  <h2>📊 MCS Task Dashboard</h2>
  <div class="card">
    <label>User: <input id="user" value="opuser" type="text"></label>
    <label>Pass: <input id="pass" value="123456" type="password"></label>
    <button onclick="login()">Login</button>
    <p id="status"></p>
    
    <table id="taskTable">
      <thead>
        <tr>
          <th>Task ID</th>
          <th>Status</th>
          <th>Start Device</th>
          <th>End Device</th>
          <th>Start Time</th>
          <th>Is Timeout</th>
          <th>Is Alarm</th>
          <th>Carrier Pseudo ID</th>
          <th>Lot No</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </div>

  <div class="card">
    <h3>Debug JSON Response</h3>
    <pre id="debug"></pre>
  </div>

  <script>
    let token = null;
    const BASE_URL = "https://kiersten-unceasing-lahoma.ngrok-free.dev/prod-api"; // ✅ ใช้ ngrok

    async function login() {
      const user = document.getElementById("user").value;
      const pass = document.getElementById("pass").value;

      const res = await fetch(`${BASE_URL}/api/login`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ username: user, password: pass })
      });

      const data = await res.json();
      document.getElementById("debug").textContent = JSON.stringify(data, null, 2);

      if (data.code === 200 && data.token) {
        token = data.token;
        document.getElementById("status").textContent = "✅ Login success (Auto-refresh every 5s)";
        loadAllTasks();
        setInterval(loadAllTasks, 5000); // refresh ทุก 5 วินาที
      } else {
        document.getElementById("status").textContent = "❌ Login failed";
      }
    }

    async function loadAllTasks() {
      if (!token) return;
      let allRows = [];
      let pageNum = 1;
      const pageSize = 100;

      while (true) {
        const res = await fetch(`${BASE_URL}/api/task/task/list?pageNum=${pageNum}&pageSize=${pageSize}`, {
          method: "GET",
          headers: { "Authorization": "Bearer " + token }
        });
        const data = await res.json();

        if (data.rows && data.rows.length > 0) {
          allRows = allRows.concat(data.rows);
          if (data.rows.length < pageSize) break;
          pageNum++;
        } else {
          break;
        }
      }

      document.getElementById("debug").textContent = JSON.stringify(allRows, null, 2);
      renderTable(allRows);
    }

    function renderTable(rows) {
      const tbody = document.querySelector("#taskTable tbody");
      tbody.innerHTML = "";

      if (rows && rows.length > 0) {
        // ✅ เอา Alarm ขึ้นก่อน
        rows.sort((a, b) => {
          if (a.isAlarm === "Y" && b.isAlarm !== "Y") return -1;
          if (a.isAlarm !== "Y" && b.isAlarm === "Y") return 1;
          return 0;
        });

        rows.forEach(task => {
          let rowClass = "";
          if (task.statusId === "TS_ERROR") rowClass = "row-error";
          else if (task.isAlarm === "Y") rowClass = "row-alarm-Y";
          else if (task.isTimeout === "Y") rowClass = "row-timeout-Y";
          else if (task.isTimeout === "N") rowClass = "row-timeout-N";

          const tr = document.createElement("tr");
          tr.className = rowClass;
          tr.innerHTML = `
            <td>${task.taskId || "-"}</td>
            <td>${task.statusId || "-"}</td>
            <td>${task.startDeviceName || "-"}</td>
            <td>${task.endDeviceName || "-"}</td>
            <td>${task.startTime || "-"}</td>
            <td>${task.isTimeout || "-"}</td>
            <td>${task.isAlarm || "-"}</td>
            <td>${task.carrierPseudoId || "-"}</td>
            <td>${task.lotNo || "-"}</td>
          `;
          tbody.appendChild(tr);
        });
      } else {
        tbody.innerHTML = `<tr><td colspan="9">No tasks found</td></tr>`;
      }
    }
  </script>
</body>
</html>
