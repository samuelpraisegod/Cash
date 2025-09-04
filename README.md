<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MarketFlow - Collaborative Trading Platform</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
    <style>
        /* CSS Variables */
        :root {
            --primary: #0a1f44;
            --secondary: #d4af37;
            --light-bg: #f9f9f9;
            --white: #fff;
            --text: #333;
            --shadow: rgba(0,0,0,0.1);
        }

   /* Global Styles */
        body {
            font-family: 'Segoe UI', sans-serif;
            background: var(--light-bg);
            color: var(--text);
            margin: 0;
            padding: 0;
            line-height: 1.6;
            overflow-x: hidden;
        }

  /* Header Styles */
        header {
            background: #4a2626;
            color: var(--white);
            padding: 1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 5px var(--shadow);
            position: sticky;
            top: 0;
            z-index: 100;
        }

  .header-title h1 {
            margin: 0;
            font-size: 1.5rem;
        }

  nav {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

  .hamburger {
            font-size: 1.5rem;
            cursor: pointer;
            position: relative;
        }

 .hamburger-menu {
            display: none;
            position: absolute;
            top: 100%;
            right: 0;
            width: 250px;
            background: var(--white);
            padding: 1rem;
            border-right: 1px solid #eee;
            box-shadow: 2px 2px 5px var(--shadow);
            z-index: 60;
        }

.hamburger.active .hamburger-menu {
            display: block;
        }

  .hamburger .brand {
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 1rem;
            text-align: center;
        }

  .hamburger-menu ul {
            list-style: none;
            padding: 0;
        }

  .hamburger-menu ul li a {
            display: flex;
            align-items: center;
            padding: 0.5rem;
            color: var(--text);
            text-decoration: none;
        }

  .hamburger-menu ul li a:hover {
            background: var(--light-bg);
            border-radius: 5px;
        }

  .btn {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            text-decoration: none;
            background: var(--secondary);
            color: var(--primary);
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

 .btn:hover {
            opacity: 0.9;
        }

 /* Main Content */
        .main-content {
            padding: 2rem;
        }

 /* Balance Section */
        #balance {
            background: var(--white);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 5px var(--shadow);
            margin-bottom: 2rem;
        }

 /* Wallet Overview */
        .wallet-overview {
            text-align: center;
            margin-bottom: 1.5rem;
        }

 .main-balance {
            font-size: 2rem;
            font-weight: bold;
            color: var(--primary);
            margin-bottom: 0.5rem;
        }

.sub-row {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-bottom: 0.5rem;
        }

  .sub-row span {
            display: flex;
            align-items: center;
            gap: 0.3rem;
        }

  /* Quick Action Buttons */
        .quick-actions {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

  /* Fund Allocation */
        .fund-allocation {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

 .allocation-card {
            background: var(--light-bg);
            padding: 1rem;
            border-radius: 10px;
            text-align: center;
        }

  /* Recent Transactions */
        .transactions-table {
            width: 100%;
            border-collapse: collapse;
            background: var(--white);
            box-shadow: 0 2px 5px var(--shadow);
        }

 .transactions-table th, .transactions-table td {
            padding: 0.5rem;
            text-align: left;
            border-bottom: 1px solid #ccc;
        }

 .transactions-table th {
            background: var(--primary);
            color: var(--white);
        }

.status {
            padding: 0.25rem 0.5rem;
            border-radius: 5px;
            color: var(--white);
            font-size: 0.875rem;
        }

  .status-completed { background: #28a745; }
        .status-pending { background: #ffc107; }

 /* Performance Snapshot */
        .performance-snapshot {
            height: 150px;
            background: #eee;
            text-align: center;
            padding: 1rem;
            margin-bottom: 1.5rem;
        }

  /* Notifications */
        .notifications {
            background: var(--light-bg);
            padding: 1rem;
            border-radius: 10px;
            margin-top: 1rem;
        }

 .notification-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 0.5rem;
        }

 /* Footer */
        footer {
            text-align: center;
            padding: 1rem;
            background: var(--primary);
            color: var(--white);
            position: relative;
            bottom: 0;
            width: 100%;
        }

  /* Utility Classes */
        .hidden {
            display: none;
        }

 /* Responsive Design */
        @media (max-width: 768px) {
            .sub-row {
                flex-direction: column;
                gap: 0.5rem;
            }
            .quick-actions {
                flex-direction: column;
                gap: 0.5rem;
            }
            .fund-allocation {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="header-title">
            <h1>MarketFlow</h1>
        </div>
        <nav>
            <div class="hamburger" onclick="toggleMenu()">
                ☰
                <div class="hamburger-menu">
                    <div class="brand">MarketFlow</div>
                    <ul>
                        <li><a href="#balance"><span role="img" aria-label="bank">🏦</span> Balance</a></li>
                        <li><a href="#deposit-withdrawals"><span role="img" aria-label="plus-money">➕💵</span> Deposit & Withdrawals</a></li>
                        <li><a href="#available-funded"><span role="img" aria-label="briefcase">💼</span> Available Funded</a></li>
                        <li><a href="#available-traders"><span role="img" aria-label="people">👥</span> Available Traders</a></li>
                        <li><a href="#co-funding"><span role="img" aria-label="handshake">🤝</span> Co-Funding</a></li>
                        <li><a href="#requests"><span role="img" aria-label="envelope">📩</span> Requests</a></li>
                        <li><a href="#active"><span role="img" aria-label="chart">📊</span> Active</a></li>
                        <li><a href="#orders"><span role="img" aria-label="document">📑</span> Orders</a></li>
                        <li><a href="#completed"><span role="img" aria-label="check">✅</span> Completed</a></li>
                        <li><a href="#profile-verification"><span role="img" aria-label="user-id">👤🔍</span> Profile & Verification</a></li>
                        <li><a href="#performance-chart"><span role="img" aria-label="graph">📈</span> Performance Chart</a></li>
                        <li><a href="#messages"><span role="img" aria-label="speech">💬</span> Messages</a></li>
                    </ul>
                </div>
            </div>
            <a href="#" id="auth-btn" class="btn btn-primary">Login</a>
        </nav>
    </header>

 <div id="home-content">
        <div class="hero">
            <h1>MarketFlow: Collaborative Trading</h1>
            <p>Join a community-driven platform to co-fund trading accounts and maximize profits.</p>
            <a href="#" class="btn btn-primary" onclick="login()">Get Started</a>
        </div>
    </div>

 <div id="dashboard-content" class="hidden">
        <div class="dashboard">
            <main class="main-content">
                <section id="balance">
                    <h2>Balance</h2>
  <!-- 1. Top Section (Wallet Overview) -->
                    <div class="wallet-overview">
                        <div class="main-balance">$2,450.00</div>
                        <div class="sub-row">
                            <span><span role="img" aria-label="money">💵</span> Available Balance: $1,800.00</span>
                            <span><span role="img" aria-label="lock">🔒</span> Locked / Pending Funds: $650.00</span>
                            <span><span role="img" aria-label="clock">🕒</span> Last Transaction: Sept 2, 25</span>
                        </div>
                    </div>
 <!-- 2. Quick Action Buttons -->
                    <div class="quick-actions">
                        <a href="#deposit" class="btn"><span role="img" aria-label="plus">➕</span> Deposit</a>
                        <a href="#withdraw" class="btn"><span role="img" aria-label="withdraw">💸</span> Withdraw</a>
                        <a href="#transfer" class="btn"><span role="img" aria-label="transfer">🔄</span> Transfer</a>
                    </div>
  <!-- 3. Fund Allocation -->
                    <div class="fund-allocation">
                        <div class="allocation-card">
                            <span role="img" aria-label="briefcase">💼</span> Available Funded Accounts: $1,200.00
                        </div>
                        <div class="allocation-card">
                            <span role="img" aria-label="people">👥</span> Available for Trading: $600.00
                        </div>
                        <div class="allocation-card">
                            <span role="img" aria-label="handshake">🤝</span> Reserved for Co-Funding: $650.00
                        </div>
                    </div>
 <!-- 4. Recent Transactions -->
                    <h3>Recent Transactions</h3>
                    <table class="transactions-table">
                        <thead>
                            <tr>
                                <th>Date</th>
                                <th>Type</th>
                                <th>Amount</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Sept 2, 25</td>
                                <td>Deposit</td>
                                <td>$500</td>
                                <td><span class="status status-completed">✅ Completed</span></td>
                            </tr>
                            <tr>
                                <td>Sept 1, 25</td>
                                <td>Withdraw</td>
                                <td>$200</td>
                                <td><span class="status status-pending">⏳ Pending</span></td>
                            </tr>
                            <tr>
                                <td>Aug 30, 25</td>
                                <td>Co-Funding</td>
                                <td>$100</td>
                                <td><span class="status status-completed">✅ Completed</span></td>
                            </tr>
                        </tbody>
                    </table>
  <!-- 5. Performance Snapshot -->
                    <div class="performance-snapshot">
                        <h4>Performance Snapshot</h4>
                        <div>Chart Placeholder (Line/Bar Chart)</div>
                        <div>Toggle: <button>Daily</button> <button>Weekly</button> <button>Monthly</button></div>
                    </div>
   <!-- 6. Notifications -->
                    <div class="notifications">
                        <h4>Notifications</h4>
                        <div class="notification-item">
                            <span role="img" aria-label="check">✅</span> Deposit Successful
                        </div>
                        <div class="notification-item">
                            <span role="img" aria-label="handshake">🤝</span> You have 1 new Co-Funding Request
                        </div>
                    </div>
                </section>
 <!-- Other sections remain unchanged but can be added as needed -->
                <section id="deposit-withdrawals">
                    <h2>Deposit & Withdrawals</h2>
                    <p>Manage your deposits and withdrawals.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Type</th>
                                <th>Amount</th>
                                <th>Date</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Deposit</td>
                                <td>$5,000</td>
                                <td>2025-09-03</td>
                                <td><span class="status status-active">Completed</span></td>
                            </tr>
                            <tr>
                                <td>Withdrawal</td>
                                <td>$2,000</td>
                                <td>2025-09-04</td>
                                <td><span class="status status-pending">Pending</span></td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <!-- Add other sections as needed -->
            </main>
        </div>
    </div>

 <footer>
        <p>&copy; 2025 MarketFlow</p>
    </footer>

 <script>
        let isLoggedIn = false;

        function updateUI() {
            const homeContent = document.getElementById('home-content');
            const dashboardContent = document.getElementById('dashboard-content');
            const authBtn = document.getElementById('auth-btn');

            if (isLoggedIn) {
                homeContent.classList.add('hidden');
                dashboardContent.classList.remove('hidden');
                authBtn.textContent = 'Logout';
                authBtn.onclick = logout;
            } else {
                homeContent.classList.remove('hidden');
                dashboardContent.classList.add('hidden');
                authBtn.textContent = 'Login';
                authBtn.onclick = login;
            }
        }

        function toggleMenu() {
            const hamburger = document.querySelector('.hamburger');
            hamburger.classList.toggle('active');
        }

        function login() {
            isLoggedIn = true;
            updateUI();
        }

        function logout() {
            isLoggedIn = false;
            updateUI();
        }

        // Simulate initial login to show dashboard
        window.onload = () => {
            login();
        };
    </script>
</body>
</html>
