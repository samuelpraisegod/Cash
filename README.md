<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MarketFlow - Wallet Dashboard</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
    <style>
        /* CSS Variables (unchanged) */
        :root {
            --primary: #0a1f44;
            --secondary: #d4af37;
            --light-bg: #f9f9f9;
            --white: #fff;
            --text: #333;
            --shadow: rgba(0,0,0,0.1);
            --green: #28a745;
            --red: #dc3545;
        }

 /* Global Styles (unchanged) */
        body {
            font-family: 'Segoe UI', sans-serif;
            background: var(--light-bg);
            color: var(--text);
            margin: 0;
            padding: 0;
            line-height: 1.6;
            overflow-x: hidden;
        }

 /* Header Styles (unchanged) */
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
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

 .btn-primary {
            background: var(--secondary);
            color: var(--primary);
        }

  .btn-success {
            background: var(--green);
            color: var(--white);
        }

 .btn-danger {
            background: var(--red);
            color: var(--white);
        }

  .btn:hover {
            opacity: 0.9;
        }

   /* Main Content */
        .main-content {
            padding: 2rem;
        }

  section {
            background: var(--white);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 5px var(--shadow);
            margin-bottom: 2rem;
        }

  /* Wallet Dashboard */
        .wallet-tabs {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

  .tab-button {
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background: var(--light-bg);
            font-weight: bold;
        }

 .tab-button.active {
            background: var(--secondary);
            color: var(--white);
        }

 .tab-content {
            display: none;
        }

  .tab-content.active {
            display: block;
        }

  .balance-overview {
            margin-bottom: 1.5rem;
        }

  .balance-overview div {
            margin-bottom: 0.5rem;
        }

 .method-card {
            background: var(--light-bg);
            padding: 1rem;
            border-radius: 10px;
            cursor: pointer;
            text-align: center;
            flex: 1;
        }

 .method-card.active {
            background: var(--secondary);
            color: var(--white);
        }

  .form-group {
            margin-bottom: 1rem;
        }

 .form-group label {
            display: block;
            margin-bottom: 0.25rem;
        }

 .form-group input, .form-group select {
            width: 100%;
            padding: 0.5rem;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

   .copy-btn {
            background: var(--primary);
            color: var(--white);
            padding: 0.25rem 0.5rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-left: 0.5rem;
        }

  .copy-btn:hover {
            opacity: 0.9;
        }

 .confirm-btn, .submit-btn {
            background: var(--green);
            color: var(--white);
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            width: 100%;
        }

  .confirm-btn:hover, .submit-btn:hover {
            opacity: 0.9;
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

 .status-pending { background: #ffc107; }
        .status-active { background: #17a2b8; }
        .status-completed { background: var(--green); }

   /* Responsive Design */
        @media (max-width: 768px) {
            .wallet-tabs, .deposit-methods, .withdrawal-methods {
                flex-direction: column;
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
                        <li><a href="#wallet"><span role="img" aria-label="wallet">💼</span> Wallet Dashboard</a></li>
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
                <!-- Balance Section (unchanged) -->
                <section id="balance">
                    <h2>Balance</h2>
                    <div class="wallet-overview">
                        <div class="main-balance">$2,450.00</div>
                        <div class="sub-row">
                            <span><span role="img" aria-label="money">💵</span> Available Balance: $1,800.00</span>
                            <span><span role="img" aria-label="lock">🔒</span> Locked / Pending Funds: $650.00</span>
                            <span><span role="img" aria-label="clock">🕒</span> Last Transaction: Sept 2, 25</span>
                        </div>
                    </div>
                    <div class="quick-actions">
                        <a href="#deposit" class="btn"><span role="img" aria-label="plus">➕</span> Deposit</a>
                        <a href="#withdraw" class="btn"><span role="img" aria-label="withdraw">💸</span> Withdraw</a>
                        <a href="#transfer" class="btn"><span role="img" aria-label="transfer">🔄</span> Transfer</a>
                    </div>
                </section>
 <!-- Wallet Dashboard (unchanged) -->
                <section id="wallet">
                    <!-- Existing Deposit and Withdrawal tabs remain unchanged -->
                    <div id="deposit-tab" class="tab-content active">
                        <!-- Existing deposit content -->
                    </div>
                    <div id="withdraw-tab" class="tab-content">
                        <!-- Existing withdrawal content -->
                    </div>
                </section>
 <!-- Co-Funding Section -->
                <section id="co-funding" class="tab-content">
                    <h2>🤝 Co-Funding</h2>
                    <div class="wallet-tabs">
                        <button class="tab-button active" onclick="showTab('co-fund-request')">Co-Funding Request</button>
                        <button class="tab-button" onclick="showTab('managed-trading')">Managed Trading Account</button>
                        <button class="tab-button" onclick="showTab('managed-account')">Managed Account Request</button>
                        <button class="tab-button" onclick="showTab('requests-dashboard')">Request Dashboard</button>
                    </div>
 <!-- Co-Funding Request Tab -->
                    <div id="co-fund-request-tab" class="tab-content active">
                        <p>Create a co-fund request by selecting an amount. Your deposit will be locked in escrow until matched. The system will match co-funders and auto-purchase the prop firm account upon agreement.</p>
                        <form id="coFundForm">
                            <div class="form-group">
                                <label for="co-fund-amount">Co-Fund Amount</label>
                                <input type="number" id="co-fund-amount" placeholder="e.g., $5k" value="5000">
                            </div>
                            <div class="form-group">
                                <label for="profit-ratio">Profit Ratio</label>
                                <select id="profit-ratio">
                                    <option value="50/50">50/50</option>
                                    <option value="60/40">60/40</option>
                                    <option value="70/30">70/30</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="your-contribution">Your Contribution ($)</label>
                                <input type="number" id="your-contribution" placeholder="e.g., $2500" value="2500">
                            </div>
                            <div class="form-group">
                                <label for="account-size">Account Size</label>
                                <input type="number" id="account-size" placeholder="e.g., $10k" value="10000">
                            </div>
                            <div class="form-group">
                                <label for="percentage-contribution">Percentage of Contribution (%)</label>
                                <input type="number" id="percentage-contribution" placeholder="e.g., 50" value="50">
                            </div>
                            <div class="form-group">
                                <label for="trader-type">Type of Trader</label>
                                <select id="trader-type">
                                    <option value="scalping">Scalping</option>
                                    <option value="swing">Swing</option>
                                    <option value="algo">Algo</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="track-record">Track Record (Upload Link/Screenshot)</label>
                                <input type="file" id="track-record">
                            </div>
                            <button type="button" class="confirm-btn" onclick="submitCoFundRequest()">Submit Request</button>
                            <div class="status-tracker" style="margin-top: 1rem; color: #666;">Status: <span class="status status-pending">Pending</span></div>
                        </form>
                    </div>
  <!-- Managed Trading Account Tab (Placeholder) -->
                    <div id="managed-trading-tab" class="tab-content">
                        <p>This form is for traders who want to manage an investor's capital. Agree on the investment size, type of account, profit targets, and return cycle. Investors control withdrawals, and profits are shared based on the agreed terms.</p>
                        <form id="managedTradingForm">
                            <div class="form-group">
                                <label for="investment-plan">Investment Plan (Capital Size)</label>
                                <input type="number" id="investment-plan" placeholder="e.g., $5k" value="5000">
                            </div>
                            <div class="form-group">
                                <label for="trader-type-managed">Type of Trader</label>
                                <select id="trader-type-managed">
                                    <option value="forex">Forex</option>
                                    <option value="stocks">Stocks</option>
                                    <option value="crypto">Crypto</option>
                                    <option value="commodities">Commodities</option>
                                    <option value="all">All</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="return-cycle">Return Cycle</label>
                                <select id="return-cycle">
                                    <option value="daily">Daily</option>
                                    <option value="weekly">Weekly</option>
                                    <option value="monthly">Monthly</option>
                                    <option value="long-term">Long-term</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="profit-target">Profit Target (%)</label>
                                <input type="number" id="profit-target" placeholder="e.g., 10" value="10">
                            </div>
                            <div class="form-group">
                                <label for="withdrawal-terms">Withdrawal Terms</label>
                                <input type="text" id="withdrawal-terms" placeholder="e.g., Monthly">
                            </div>
                            <div class="form-group">
                                <label for="lot-size">Lot Size</label>
                                <input type="number" id="lot-size" placeholder="e.g., 0.1" value="0.1">
                            </div>
                            <div class="form-group">
                                <label for="experience-level">Experience Level</label>
                                <input type="text" id="experience-level" placeholder="e.g., 2 years">
                            </div>
                            <div class="form-group">
                                <label for="proof-experience">Proof of Experience (Upload)</label>
                                <input type="file" id="proof-experience">
                            </div>
                            <div class="form-group">
                                <label for="proof-trades">Proof of Trades (Screenshot Upload)</label>
                                <input type="file" id="proof-trades">
                            </div>
                            <button type="button" class="confirm-btn" onclick="submitManagedTradingRequest()">Submit Request</button>
                            <div class="status-tracker" style="margin-top: 1rem; color: #666;">Status: <span class="status status-pending">Pending</span></div>
                        </form>
                    </div>
  <!-- Managed Account Request Tab (Placeholder) -->
                    <div id="managed-account-tab" class="tab-content">
                        <p>For investors: Create a managed account request to link with a trader without revealing sensitive broker details. Input your broker name, account ID, and the trader's platform ID. The system will securely connect you.</p>
                        <form id="managedAccountForm">
                            <div class="form-group">
                                <label for="broker-name">Broker Name</label>
                                <input type="text" id="broker-name" placeholder="e.g., XM" value="XM">
                            </div>
                            <div class="form-group">
                                <label for="account-id">Account ID</label>
                                <input type="text" id="account-id" placeholder="e.g., 123456" value="123456">
                            </div>
                            <div class="form-group">
                                <label for="investment-plan-managed">Investment Plan (Capital Size)</label>
                                <input type="number" id="investment-plan-managed" placeholder="e.g., $5k" value="5000">
                            </div>
                            <div class="form-group">
                                <label for="profit-split">Profit Split (%)</label>
                                <select id="profit-split">
                                    <option value="50/50">50/50</option>
                                    <option value="60/40">60/40</option>
                                    <option value="70/30">70/30</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="target-cycle">Target Amount / Return Cycle</label>
                                <select id="target-cycle">
                                    <option value="daily">Daily</option>
                                    <option value="weekly">Weekly</option>
                                    <option value="monthly">Monthly</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="profit-target-managed">Profit Target (%)</label>
                                <input type="number" id="profit-target-managed" placeholder="e.g., 10" value="10">
                            </div>
                            <button type="button" class="confirm-btn" onclick="submitManagedAccountRequest()">Submit Request</button>
                            <div class="status-tracker" style="margin-top: 1rem; color: #666;">Status: <span class="status status-pending">Pending</span></div>
                        </form>
                    </div>
 <!-- Request Dashboard Tab (Placeholder) -->
                    <div id="requests-dashboard-tab" class="tab-content">
                        <p>View and manage all your requests and agreements here. Accept or decline pending requests, track active agreements, and monitor profit-sharing status.</p>
                        <div class="dashboard-features">
                            <h3>Pending Requests</h3>
                            <table class="transactions-table">
                                <thead>
                                    <tr>
                                        <th>Request ID</th>
                                        <th>Type</th>
                                        <th>Amount</th>
                                        <th>Actions</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>REQ001</td>
                                        <td>Co-Funding</td>
                                        <td>$5,000</td>
                                        <td>
                                            <button class="btn btn-success" onclick="acceptRequest('REQ001')">Accept</button>
                                            <button class="btn btn-danger" onclick="declineRequest('REQ001')">Decline</button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>

  <h3>Active Agreements</h3>
                            <table class="transactions-table">
                                <thead>
                                    <tr>
                                        <th>Agreement ID</th>
                                        <th>Partner</th>
                                        <th>Amount</th>
                                        <th>Status</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>AGR001</td>
                                        <td>TraderX</td>
                                        <td>$10,000</td>
                                        <td><span class="status status-active">Active</span></td>
                                    </tr>
                                </tbody>
                            </table>

 <h3>Completed Agreements</h3>
                            <table class="transactions-table">
                                <thead>
                                    <tr>
                                        <th>Agreement ID</th>
                                        <th>Profit</th>
                                        <th>Status</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>AGR002</td>
                                        <td>$500</td>
                                        <td><span class="status status-completed">Completed</span></td>
                                    </tr>
                                </tbody>
                            </table>

<h3>Notifications</h3>
                            <p>New request from TraderY - <button class="btn btn-primary" onclick="viewNotification()">View</button></p>

   <h3>Agreement History</h3>
                            <button class="btn btn-primary" onclick="downloadHistory()">Download PDF</button>
                        </div>
                    </div>
                </section>
 <!-- Other sections (unchanged) -->
                <section id="available-funded">
                    <h2>Available Funded</h2>
                    <p>View available funded accounts.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Firm</th>
                                <th>Amount</th>
                                <th>Availability</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>FTMO</td>
                                <td>$10,000</td>
                                <td>Available</td>
                            </tr>
                        </tbody>
                    </table>
                </section>
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

        // Tab Switching
        function showTab(tab) {
            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll(`.wallet-tabs .tab-button[onclick="showTab('${tab}')"]`).forEach(btn => btn.classList.add('active'));

            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            document.getElementById(`${tab}-tab`).classList.add('active');
        }

        // Placeholder functions for form submissions
        function submitCoFundRequest() {
            if (confirm('Submit Co-Funding Request?')) {
                alert('Request submitted successfully! Status: Pending');
            }
        }

        function submitManagedTradingRequest() {
            if (confirm('Submit Managed Trading Request?')) {
                alert('Request submitted successfully! Status: Pending');
            }
        }

        function submitManagedAccountRequest() {
            if (confirm('Submit Managed Account Request?')) {
                alert('Request submitted successfully! Status: Pending');
            }
        }

        function acceptRequest(id) {
            alert(`Accepted request ${id}!`);
        }

        function declineRequest(id) {
            alert(`Declined request ${id}!`);
        }

        function viewNotification() {
            alert('Viewing notification...');
        }

        function downloadHistory() {
            alert('Downloading agreement history as PDF...');
        }

        window.onload = () => {
            login();
        };
    </script>
</body>
</html>
