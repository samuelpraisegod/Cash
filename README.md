<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      display: flex;
    }
    /* Sidebar */
    .sidebar {
      width: 220px;
      background: #222;
      color: white;
      height: 100vh;
      padding-top: 20px;
      position: fixed;
    }
    .sidebar button {
      width: 100%;
      padding: 12px;
      border: none;
      background: none;
      color: white;
      text-align: left;
      cursor: pointer;
    }
    .sidebar button:hover {
      background: #444;
    }
    /* Content */
    .content {
      margin-left: 220px;
      padding: 20px;
      flex-grow: 1;
    }
    .section { display: none; }
    .active { display: block; }
  </style>
</head>
<body>

  <!-- Sidebar Menu -->
  <div class="sidebar">
    <button onclick="showSection('balance')">🏦 Balance</button>
    <button onclick="showSection('deposit')">➕ Deposit</button>
    <button onclick="showSection('withdraw')">💸 Withdraw</button>
    <button onclick="showSection('funded')">💼 Available Funded</button>
    <button onclick="showSection('traders')">👥 Available Traders</button>
    <button onclick="showSection('cofunding')">🤝 Co-Funding</button>
    <button onclick="showSection('requests')">📩 Requests</button>
    <button onclick="showSection('active')">📊 Active</button>
    <button onclick="showSection('orders')">📑 Orders</button>
    <button onclick="showSection('completed')">✅ Completed</button>
    <button onclick="showSection('profits')">💵 Profits & Withdrawals</button>
    <button onclick="showSection('performance')">📈 Performance Chart</button>
    <button onclick="showSection('messages')">💬 Messages</button>
  </div>

  <!-- Main Content -->
  <div class="content">
    <div id="balance" class="section active">
      <h2>🏦 Balance</h2>
      <p>Show wallet balance, available funds, and history.</p>
    </div>

 <div id="deposit" class="section">
      <h2>➕ Deposit</h2>
      <p>Deposit form goes here (bank account, crypto wallet, etc.).</p>
    </div>

  <div id="withdraw" class="section">
      <h2>💸 Withdraw</h2>
      <p>Withdrawal form goes here (bank transfer, crypto, mobile money).</p>
    </div>

 <div id="funded" class="section">
      <h2>💼 Available Funded</h2>
      <p>Show funded accounts and available allocation.</p>
    </div>

  <div id="traders" class="section">
      <h2>👥 Available Traders</h2>
      <p>List of traders available for managed trading or co-funding.</p>
    </div>

   <div id="cofunding" class="section">
      <h2>🤝 Co-Funding</h2>
      <p>Co-funding request form and agreements appear here.</p>
    </div>

  <div id="requests" class="section">
      <h2>📩 Requests</h2>
      <p>List of all co-funding and managed trading requests.</p>
    </div>

  <div id="active" class="section">
      <h2>📊 Active</h2>
      <p>Show active requests, trades, or accounts.</p>
    </div>

  <div id="orders" class="section">
      <h2>📑 Orders</h2>
      <p>Orders and transactions history goes here.</p>
    </div>

  <div id="completed" class="section">
      <h2>✅ Completed</h2>
      <p>Show completed requests, trades, or agreements.</p>
    </div>

 <div id="profits" class="section">
      <h2>💵 Profits & Withdrawals</h2>
      <p>Profits, earnings, and withdrawal records.</p>
    </div>

  <div id="performance" class="section">
      <h2>📈 Performance Chart</h2>
      <p>Analytics, performance metrics, and charts.</p>
    </div>

 <div id="messages" class="section">
      <h2>💬 Messages</h2>
      <p>Chat and notifications system goes here.</p>
    </div>
  </div>

  <script>
    function showSection(id) {
      // Hide all sections
      let sections = document.querySelectorAll('.section');
      sections.forEach(sec => sec.style.display = 'none');

      // Show the clicked section
      document.getElementById(id).style.display = 'block';
    }
  </script>

</body>
</html>
