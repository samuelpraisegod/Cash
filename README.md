<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DivoraSplit - Wallet Dashboard</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
    <style>
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

        body {
            font-family: 'Segoe UI', sans-serif;
            background: var(--light-bg);
            color: var(--text);
            margin: 0;
            padding: 0;
            line-height: 1.6;
            overflow-x: hidden;
        }

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

        .btn-primary { background: var(--secondary); color: var(--primary); }
        .btn-success { background: var(--green); color: var(--white); }
        .btn-danger { background: var(--red); color: var(--white); }
        .btn:hover { opacity: 0.9; }

        .dashboard {
            display: flex;
            min-height: calc(100vh - 60px);
        }

        .main-content {
            padding: 2rem;
            width: 100%;
        }

        section {
            background: var(--white);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 5px var(--shadow);
            margin-bottom: 2rem;
            display: none;
        }

        section.active {
            display: block;
        }

        .wallet-tabs {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
            overflow-x: auto;
        }

        .tab-button {
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background: var(--light-bg);
            font-weight: bold;
            white-space: nowrap;
        }

        .tab-button.active {
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

        .confirm-btn {
            background: var(--green);
            color: var(--white);
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            width: 100%;
        }

        .confirm-btn:hover {
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
        .status-completed { background: var(--green); }

        .placeholder {
            text-align: center;
            color: #666;
            font-style: italic;
        }

        .hidden {
            display: none;
        }

        .deposit-method-tabs, .withdrawal-method-tabs {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
        }

        .deposit-method-tab, .withdrawal-method-tab {
            padding: 0.5rem 1rem;
            border: 1px solid #ccc;
            border-radius: 5px;
            cursor: pointer;
            background: var(--light-bg);
        }

        .deposit-method-tab.active, .withdrawal-method-tab.active {
            background: var(--secondary);
            color: var(--white);
            border-color: var(--secondary);
        }

        .qr-code {
            width: 100px;
            height: 100px;
            background: #f0f0f0;
            margin: 1rem 0;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .copy-btn {
            padding: 0.25rem 0.5rem;
            background: var(--primary);
            color: var(--white);
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .copy-btn:hover {
            opacity: 0.9;
        }

        .save-default {
            margin-top: 0.5rem;
        }
    </style>
</head>
<body>
    <header>
        <div class="header-title">
            <h1>DivoraSplit</h1>
        </div>
        <nav>
            <div class="hamburger" onclick="toggleMenu()">
                ☰
                <div class="hamburger-menu">
                    <div class="brand">DivoraSplit</div>
                    <ul>
                        <li><a href="#" onclick="showTab('balance')">🏦 Balance</a></li>
                        <li><a href="#" onclick="showTab('wallet')">💼 Wallet Dashboard</a></li>
                        <li><a href="#" onclick="showTab('available-funded')">💼 Available Funded</a></li>
                        <li><a href="#" onclick="showTab('available-traders')">👥 Available Traders</a></li>
                        <li><a href="#" onclick="showTab('co-funding')">🤝 Co-Funding</a></li>
                        <li><a href="#" onclick="showTab('requests')">📩 Requests</a></li>
                        <li><a href="#" onclick="showTab('active')">📊 Active</a></li>
                        <li><a href="#" onclick="showTab('orders')">📑 Orders</a></li>
                        <li><a href="#" onclick="showTab('completed')">✅ Completed</a></li>
                        <li><a href="#" onclick="showTab('profile-verification')">👤🔍 Profile & Verification</a></li>
                        <li><a href="#" onclick="showTab('performance-chart')">📈 Performance Chart</a></li>
                        <li><a href="#" onclick="showTab('messages')">💬 Messages</a></li>
                    </ul>
                </div>
            </div>
            <a href="#" id="auth-btn" class="btn btn-primary">Login</a>
        </nav>
    </header>

 <div id="home-content">
        <div class="hero">
            <h1>DivoraSplit: Collaborative Trading</h1>
            <p>Join a community-driven platform to co-fund trading accounts and maximize profits.</p>
            <a href="#" class="btn btn-primary" onclick="login()">Get Started</a>
        </div>
    </div>

 <div id="dashboard-content" class="hidden">
        <div class="dashboard">
            <main class="main-content">
                <!-- Balance Section -->
                <section id="balance" class="active">
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
                        <a href="#" class="btn" onclick="showTab('deposit')">➕ Deposit</a>
                        <a href="#" class="btn" onclick="showTab('withdraw')">💸 Withdraw</a>
                        <a href="#" class="btn" onclick="showTab('transfer')">🔄 Transfer</a>
                    </div>
                </section>
 <!-- Wallet Dashboard -->
                <section id="wallet">
                    <h2>Wallet Dashboard</h2>
                    <div class="wallet-tabs">
                        <button class="tab-button" onclick="showTab('deposit')">Deposit (➕)</button>
                        <button class="tab-button" onclick="showTab('withdraw')">Withdraw (💸)</button>
                    </div>
                    <div id="deposit" class="tab-content">
                        <h3>➕ Deposit Funds</h3>
                        <div class="deposit-method-tabs">
                            <div class="deposit-method-tab active" id="bank-tab" onclick="showDepositMethod('bank')">💳 Bank Transfer</div>
                            <div class="deposit-method-tab" id="card-tab" onclick="showDepositMethod('card')">💵 Card Payment</div>
                            <div class="deposit-method-tab" id="crypto-tab" onclick="showDepositMethod('crypto')">🔗 Crypto Wallet</div>
                        </div>
                        <div id="deposit-details" class="form-group">
                            <div id="bank-details" class="deposit-method-content active">
                                <label>Enter Amount</label>
                                <input type="number" placeholder="e.g., $500" min="0">
                                <label>Bank Name</label>
                                <input type="text" value="GTBank" readonly>
                                <label>Account Name</label>
                                <input type="text" value="MarketFlowFX Ltd" readonly>
                                <label>Account Number</label>
                                <input type="text" value="0123456789" readonly>
                                <label>Reference Code</label>
                                <input type="text" value="DEP49382" readonly>
                                <label>Upload Proof of Payment</label>
                                <input type="file" accept="image/*">
                            </div>
                            <div id="card-details" class="deposit-method-content hidden">
                                <label>Enter Amount</label>
                                <input type="number" placeholder="e.g., $500" min="0">
                                <label>Card Number</label>
                                <input type="text" placeholder="1234 5678 9012 3456">
                                <label>Expiry</label>
                                <input type="text" placeholder="MM/YY">
                                <label>CVV</label>
                                <input type="text" placeholder="123">
                            </div>
                            <div id="crypto-details" class="deposit-method-content hidden">
                                <label>Enter Amount</label>
                                <input type="number" placeholder="e.g., $500" min="0">
                                <label>Select Coin</label>
                                <select>
                                    <option value="BTC">BTC</option>
                                    <option value="USDT">USDT</option>
                                    <option value="ETH">ETH</option>
                                </select>
                                <label>Wallet Address</label>
                                <div style="display: flex; gap: 0.5rem;">
                                    <input type="text" value="0xAB123456789CDEFFED1234..." readonly>
                                    <button class="copy-btn" onclick="copyToClipboard('0xAB123456789CDEFFED1234...')">📋 Copy</button>
                                </div>
                                <div class="qr-code">QR Code Here</div>
                            </div>
                        </div>
                        <button class="confirm-btn" onclick="confirmDeposit()">✅ Confirm Deposit</button>
                        <p class="placeholder" style="margin-top: 1rem;">⚠️ Please make payment to the account/wallet shown above. Your deposit will be confirmed once payment is received.</p>
                        <table class="transactions-table" style="margin-top: 1rem; width: 100%;">
                            <thead><tr><th>Date</th><th>Method</th><th>Amount</th><th>Status</th></tr></thead>
                            <tbody>
                                <tr><td>Sept 4, 25</td><td>Bank Transfer</td><td>$300</td><td><span class="status status-completed">✅ Completed</span></td></tr>
                                <tr><td>Sept 3, 25</td><td>Crypto (USDT)</td><td>$100</td><td><span class="status status-pending">⏳ Pending</span></td></tr>
                            </tbody>
                        </table>
                    </div>
                    <div id="withdraw" class="tab-content hidden">
                        <h3>💸 Withdraw Funds</h3>
                        <div class="wallet-overview">
                            <p>Available Balance: $2,450.00</p>
                            <p>Pending Withdrawals: $200.00</p>
                            <p>Minimum Withdrawal Limit: $10.00</p>
                        </div>
                        <div class="form-group">
                            <label>Enter Withdrawal Amount</label>
                            <input type="number" id="withdrawal-amount" placeholder="e.g., $200" min="10" oninput="updateNetAmount()">
                            <label>Currency</label>
                            <select id="withdrawal-currency" onchange="updateNetAmount()">
                                <option value="USD">USD</option>
                                <option value="NGN">NGN</option>
                            </select>
                            <p>You will receive: <span id="net-amount">$195.00</span> (after 2.5% fee)</p>
                        </div>
                        <div class="withdrawal-method-tabs">
                            <div class="withdrawal-method-tab active" id="bank-withdrawal-tab" onclick="showWithdrawalMethod('bank')">🏦 Bank Transfer</div>
                            <div class="withdrawal-method-tab" id="crypto-withdrawal-tab" onclick="showWithdrawalMethod('crypto')">🔗 Crypto Wallet</div>
                            <div class="withdrawal-method-tab" id="mobile-withdrawal-tab" onclick="showWithdrawalMethod('mobile')">📲 Mobile Money</div>
                        </div>
                        <div id="withdrawal-details" class="form-group">
                            <div id="bank-withdrawal-details" class="withdrawal-method-content active">
                                <label>Bank Name</label>
                                <select>
                                    <option value="GTBank">GTBank</option>
                                    <option value="Zenith">Zenith</option>
                                </select>
                                <label>Account Number</label>
                                <input type="text" placeholder="e.g., 0123456789">
                                <label>Account Holder Name</label>
                                <input type="text" placeholder="e.g., John Doe">
                                <label>Branch (Optional)</label>
                                <input type="text" placeholder="e.g., Lagos">
                                <div class="save-default">
                                    <input type="checkbox" id="save-default-bank">
                                    <label for="save-default-bank">✔ Save as default payout account</label>
                                </div>
                            </div>
                            <div id="crypto-withdrawal-details" class="withdrawal-method-content hidden">
                                <label>Select Coin</label>
                                <select>
                                    <option value="BTC">BTC</option>
                                    <option value="USDT">USDT</option>
                                    <option value="ETH">ETH</option>
                                </select>
                                <label>Network Type</label>
                                <select>
                                    <option value="ERC20">ERC20</option>
                                    <option value="TRC20">TRC20</option>
                                </select>
                                <label>Wallet Address</label>
                                <input type="text" placeholder="e.g., 0xAB123456789CDEFFED1234...">
                            </div>
                            <div id="mobile-withdrawal-details" class="withdrawal-method-content hidden">
                                <label>Mobile Money Provider</label>
                                <select>
                                    <option value="MTN">MTN</option>
                                    <option value="Airtel">Airtel</option>
                                </select>
                                <label>Phone Number</label>
                                <input type="tel" placeholder="e.g., +2348012345678">
                                <label>Account Name</label>
                                <input type="text" placeholder="e.g., John Doe">
                            </div>
                        </div>
                        <div class="form-group">
                            <label>Security Verification</label>
                            <input type="text" placeholder="Enter OTP / 2FA Code">
                            <input type="password" placeholder="Withdrawal PIN (Optional)" style="margin-top: 0.5rem;">
                        </div>
                        <button class="confirm-btn" onclick="submitWithdrawal()">✅ Submit Withdrawal</button>
                        <p class="placeholder" style="margin-top: 1rem;">Bank transfers take 1–2 business days. Crypto withdrawals are processed within 24 hours.</p>
                        <table class="transactions-table" style="margin-top: 1rem; width: 100%;">
                            <thead><tr><th>Date</th><th>Method</th><th>Amount</th><th>Status</th></tr></thead>
                            <tbody>
                                <tr><td>Sept 4, 25</td><td>Bank Transfer</td><td>$200</td><td><span class="status status-pending">⏳ Pending</span></td></tr>
                                <tr><td>Sept 2, 25</td><td>Crypto (USDT)</td><td>$100</td><td><span class="status status-completed">✅ Completed</span></td></tr>
                            </tbody>
                        </table>
                    </div>
                </section>
 <!-- Co-Funding Section -->
                <section id="co-funding">
                    <h2>🤝 Co-Funding</h2>
                    <div class="wallet-tabs">
                        <button class="tab-button" onclick="showTab('co-fund-request')">Co-Funding Request</button>
                        <button class="tab-button" onclick="showTab('managed-trading')">Managed Trading Account</button>
                        <button class="tab-button" onclick="showTab('managed-account')">Managed Account Request</button>
                        <button class="tab-button" onclick="showTab('requests-dashboard')">Request Dashboard</button>
                    </div>
                    <div id="co-fund-request" class="tab-content">
                        <p>Create a co-fund request by selecting an amount. Your deposit will be locked in escrow until matched.</p>
                        <form>
                            <div class="form-group">
                                <label for="co-fund-amount">Co-Fund Amount</label>
                                <input type="number" id="co-fund-amount" placeholder="e.g., $5k" value="5000">
                            </div>
                            <button type="button" class="confirm-btn" onclick="submitCoFundRequest()">Submit Request</button>
                            <div class="status-tracker" style="margin-top: 1rem; color: #666;">Status: <span class="status status-pending">Pending</span></div>
                        </form>
                    </div>
                    <div id="managed-trading" class="tab-content">
                        <div class="placeholder">Coming Soon</div>
                    </div>
                    <div id="managed-account" class="tab-content">
                        <div class="placeholder">Coming Soon</div>
                    </div>
                    <div id="requests-dashboard" class="tab-content">
                        <div class="placeholder">Coming Soon</div>
                    </div>
                </section>
 <!-- Other Sections -->
                <section id="available-funded">
                    <h2>Available Funded</h2>
                    <p>View available funded accounts.</p>
                    <table class="transactions-table">
                        <thead><tr><th>Firm</th><th>Amount</th><th>Availability</th></tr></thead>
                        <tbody><tr><td>FTMO</td><td>$10,000</td><td>Available</td></tr></tbody>
                    </table>
                </section>
                <section id="available-traders">
                    <h2>Available Traders</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
                <section id="requests">
                    <h2>Requests</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
                <section id="active">
                    <h2>Active</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
                <section id="orders">
                    <h2>Orders</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
                <section id="completed">
                    <h2>Completed</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
                <section id="profile-verification">
                    <h2>Profile & Verification</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
                <section id="performance-chart">
                    <h2>Performance Chart</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
                <section id="messages">
                    <h2>Messages</h2>
                    <div class="placeholder">Coming Soon</div>
                </section>
            </main>
        </div>
    </div>

  <footer>
        <p>&copy; 2025 DivoraSplit</p>
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
                showTab('balance'); // Default to Balance on login
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
            document.querySelectorAll('section').forEach(section => section.classList.remove('active'));
            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            document.querySelectorAll('.deposit-method-tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.deposit-method-content').forEach(content => content.classList.add('hidden'));
            document.querySelectorAll('.withdrawal-method-tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.withdrawal-method-content').forEach(content => content.classList.add('hidden'));
        }

        function showTab(tab) {
            const dashboardContent = document.getElementById('dashboard-content');
            if (dashboardContent) dashboardContent.classList.remove('hidden');

            document.querySelectorAll('section').forEach(section => {
                section.classList.remove('active');
                const subTabs = section.querySelectorAll('.tab-content');
                subTabs.forEach(subTab => subTab.classList.remove('active'));
            });
            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));

            const activeElement = document.getElementById(tab);
            if (activeElement) {
                if (activeElement.classList.contains('tab-content')) {
                    const parentSection = activeElement.closest('section');
                    if (parentSection) {
                        parentSection.classList.add('active');
                        // Handle exclusive visibility for deposit and withdraw
                        if (tab === 'deposit') {
                            document.getElementById('deposit').classList.add('active');
                            document.getElementById('withdraw').classList.remove('active');
                        } else if (tab === 'withdraw') {
                            document.getElementById('withdraw').classList.add('active');
                            document.getElementById('deposit').classList.remove('active');
                        }
                        // Activate corresponding tab buttons
                        const tabButtons = parentSection.querySelectorAll('.tab-button');
                        tabButtons.forEach(btn => {
                            const btnTab = btn.getAttribute('onclick').match(/showTab\('(\w+)'\)/)[1];
                            if (btnTab === tab) btn.classList.add('active');
                        });
                    }
                } else {
                    activeElement.classList.add('active');
                    const tabButtons = activeElement.querySelectorAll('.wallet-tabs .tab-button');
                    if (tabButtons.length > 0) {
                        const defaultSubTab = tabButtons[0].getAttribute('onclick').match(/showTab\('(\w+)'\)/)[1];
                        showTab(defaultSubTab);
                        return;
                    }
                }
            } else {
                showTab('balance');
            }
        }

        function showDepositMethod(method) {
            document.querySelectorAll('.deposit-method-tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.deposit-method-content').forEach(content => content.classList.add('hidden'));

            document.querySelector(`#${method}-details`).classList.remove('hidden');
            document.querySelector(`#${method}-tab`).classList.add('active');
        }

        function showWithdrawalMethod(method) {
            document.querySelectorAll('.withdrawal-method-tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.withdrawal-method-content').forEach(content => content.classList.add('hidden'));

            document.querySelector(`#${method}-withdrawal-details`).classList.remove('hidden');
            document.querySelector(`#${method}-withdrawal-tab`).classList.add('active');
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => alert('Copied to clipboard!'));
        }

        function updateNetAmount() {
            const amount = parseFloat(document.getElementById('withdrawal-amount').value) || 0;
            const feeRate = 0.025; // 2.5% fee
            const fee = amount * feeRate;
            const netAmount = amount - fee;
            document.getElementById('net-amount').textContent = `${netAmount.toFixed(2)}`;
        }

        function confirmDeposit() {
            alert('Deposit confirmed! Processing will begin once payment is verified.');
        }

        function submitWithdrawal() {
            const otp = document.querySelector('input[placeholder="Enter OTP / 2FA Code"]').value;
            const pin = document.querySelector('input[placeholder="Withdrawal PIN (Optional)"]').value;
            if (otp && (pin || true)) {
                alert('Withdrawal submitted! Processing will begin shortly.');
            } else {
                alert('Please enter OTP and optionally a PIN for security.');
            }
        }

        function submitCoFundRequest() {
            if (confirm('Submit Co-Funding Request?')) {
                alert('Request submitted successfully! Status: Pending');
            }
        }

        window.onload = () => {
            updateUI();
        };
    </script>
</body>
</html>
