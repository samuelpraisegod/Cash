<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MarketFlow - Wallet Dashboard</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
    <style>
        /* Existing CSS remains unchanged */
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
        /* ... (other styles remain unchanged) */
        .status-pending { background: #ffc107; }
        .status-active { background: #17a2b8; }
        .status-completed { background: var(--green); }
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
                        <li><a href="#balance" onclick="showTab('balance')">🏦 Balance</a></li>
                        <li><a href="#wallet" onclick="showTab('wallet')">💼 Wallet Dashboard</a></li>
                        <li><a href="#available-funded" onclick="showTab('available-funded')">💼 Available Funded</a></li>
                        <li><a href="#available-traders" onclick="showTab('available-traders')">👥 Available Traders</a></li>
                        <li><a href="#co-funding" onclick="showTab('co-fund-request')">🤝 Co-Funding</a></li>
                        <li><a href="#requests" onclick="showTab('requests')">📩 Requests</a></li>
                        <li><a href="#active" onclick="showTab('active')">📊 Active</a></li>
                        <li><a href="#orders" onclick="showTab('orders')">📑 Orders</a></li>
                        <li><a href="#completed" onclick="showTab('completed')">✅ Completed</a></li>
                        <li><a href="#profile-verification" onclick="showTab('profile-verification')">👤🔍 Profile & Verification</a></li>
                        <li><a href="#performance-chart" onclick="showTab('performance-chart')">📈 Performance Chart</a></li>
                        <li><a href="#messages" onclick="showTab('messages')">💬 Messages</a></li>
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
                <!-- Balance Section -->
                <section id="balance-tab" class="tab-content">
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
                        <a href="#deposit" class="btn" onclick="showTab('deposit')">➕ Deposit</a>
                        <a href="#withdraw" class="btn" onclick="showTab('withdraw')">💸 Withdraw</a>
                        <a href="#transfer" class="btn" onclick="showTab('transfer')">🔄 Transfer</a>
                    </div>
                </section>
   <!-- Wallet Dashboard -->
                <section id="wallet-tab" class="tab-content">
                    <h2>Wallet Dashboard</h2>
                    <div class="wallet-tabs">
                        <button class="tab-button" onclick="showTab('deposit')">Deposit (➕)</button>
                        <button class="tab-button" onclick="showTab('withdraw')">Withdraw (💸)</button>
                    </div>
                    <div id="deposit-tab" class="tab-content">
                        <!-- Existing deposit content -->
                    </div>
                    <div id="withdraw-tab" class="tab-content">
                        <!-- Existing withdrawal content -->
                    </div>
                </section>
  <!-- Co-Funding Section -->
                <section id="co-funding-tab" class="tab-content">
                    <h2>🤝 Co-Funding</h2>
                    <div class="wallet-tabs">
                        <button class="tab-button" onclick="showTab('co-fund-request')">Co-Funding Request</button>
                        <button class="tab-button" onclick="showTab('managed-trading')">Managed Trading Account</button>
                        <button class="tab-button" onclick="showTab('managed-account')">Managed Account Request</button>
                        <button class="tab-button" onclick="showTab('requests-dashboard')">Request Dashboard</button>
                    </div>
                    <div id="co-fund-request-tab" class="tab-content">
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
                    <div id="managed-trading-tab" class="tab-content">
                        <!-- Managed Trading content -->
                    </div>
                    <div id="managed-account-tab" class="tab-content">
                        <!-- Managed Account content -->
                    </div>
                    <div id="requests-dashboard-tab" class="tab-content">
                        <!-- Request Dashboard content -->
                    </div>
                </section>
    <!-- Other sections (unchanged structure) -->
                <section id="available-funded-tab" class="tab-content">
                    <h2>Available Funded</h2>
                    <p>View available funded accounts.</p>
                    <table>
                        <thead><tr><th>Firm</th><th>Amount</th><th>Availability</th></tr></thead>
                        <tbody><tr><td>FTMO</td><td>$10,000</td><td>Available</td></tr></tbody>
                    </table>
                </section>
            </main>
        </div>
    </div
        
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
            showTab('balance'); // Default to Balance tab on login
        }

        function logout() {
            isLoggedIn = false;
            updateUI();
        }

        // Enhanced Tab Switching
        function showTab(tab) {
            // Remove active class from all tab buttons and content
            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));

            // Activate the selected tab and its content
            const tabButton = document.querySelector(`.tab-button[onclick="showTab('${tab}')"]`) ||
                             document.querySelector(`a[onclick="showTab('${tab}')"]`);
            if (tabButton) tabButton.classList.add('active');

            const tabContent = document.getElementById(`${tab}-tab`);
            if (tabContent) tabContent.classList.add('active');
        }

        // Form Submission Functions
        function submitCoFundRequest() {
            if (confirm('Submit Co-Funding Request?')) {
                alert('Request submitted successfully! Status: Pending');
                document.querySelector('#co-fund-request-tab .status-tracker .status').textContent = 'Pending';
                document.querySelector('#co-fund-request-tab .status-tracker .status').className = 'status status-pending';
            }
        }

        // Placeholder for other submission functions
        function submitManagedTradingRequest() { alert('Managed Trading Request submitted!'); }
        function submitManagedAccountRequest() { alert('Managed Account Request submitted!'); }
        function acceptRequest(id) { alert(`Accepted request ${id}!`); }
        function declineRequest(id) { alert(`Declined request ${id}!`); }
        function viewNotification() { alert('Viewing notification...'); }
        function downloadHistory() { alert('Downloading agreement history as PDF...'); }

        window.onload = () => {
            login();
        };
    </script>
</body>
</html>
