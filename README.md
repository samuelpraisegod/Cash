<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MarketFlow - Wallet Dashboard</title>
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
            --green: #28a745;
            --red: #dc3545;
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

        .status-completed { background: var(--green); }
        .status-pending { background: #ffc107; }

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
                <!-- Balance Section (unchanged for now) -->
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
 <!-- Wallet Dashboard -->
                <section id="wallet">
                    <h2>Wallet Dashboard</h2>
                    <div class="wallet-tabs">
                        <button class="tab-button active" onclick="showTab('deposit')">Deposit (➕)</button>
                        <button class="tab-button" onclick="showTab('withdraw')">Withdraw (💸)</button>
                    </div>
 <!-- Deposit Tab -->
                    <div id="deposit-tab" class="tab-content active">
                        <h2>➕ Deposit Funds</h2>
                        <div class="balance-overview">
                            <div>Available Balance: $2,450.00</div>
                            <div>Pending Deposits: $100.00</div>
                            <div>Minimum Deposit Limit: $10.00</div>
                        </div>

  <div class="deposit-methods">
                            <div class="method-card" onclick="selectMethod('bank')">💳 Bank Transfer</div>
                            <div class="method-card" onclick="selectMethod('card')">💵 Card Payment</div>
                            <div class="method-card" onclick="selectMethod('crypto')">🔗 Crypto Wallet</div>
                        </div>

  <form id="depositForm" class="hidden">
                            <div class="form-group">
                                <label for="deposit-amount">Enter Amount</label>
                                <input type="number" id="deposit-amount" placeholder="Enter Amount" value="500" oninput="calculateNetDeposit()">
                            </div>
                            <div class="form-group">
                                <label for="deposit-currency">Currency</label>
                                <select id="deposit-currency" onchange="calculateNetDeposit()">
                                    <option value="USD">USD</option>
                                    <option value="NGN">NGN</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>You will receive: <span id="net-deposit">$487.50 (after 2.5% fee)</span></label>
                            </div>
                            <div id="payment-details" class="payment-details">
                                <!-- Dynamic content will be inserted here -->
                            </div>
                            <button type="button" class="confirm-btn" onclick="confirmDeposit()">✅ Confirm Deposit</button>
                            <div class="instructions" style="margin-top: 1rem; color: #666;">
                                ⚠️ Please make payment to the account/wallet shown above. Your deposit will be confirmed once payment is received.
                            </div>
                        </form>

  <h3>Recent Transactions (Deposits)</h3>
                        <table class="transactions-table">
                            <thead>
                                <tr>
                                    <th>Date</th>
                                    <th>Method</th>
                                    <th>Amount</th>
                                    <th>Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Sept 4, 25</td>
                                    <td>Bank Transfer</td>
                                    <td>$300</td>
                                    <td><span class="status status-completed">✅ Completed</span></td>
                                </tr>
                                <tr>
                                    <td>Sept 3, 25</td>
                                    <td>Crypto (USDT)</td>
                                    <td>$100</td>
                                    <td><span class="status status-pending">⏳ Pending</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
  <!-- Withdrawal Tab -->
                    <div id="withdraw-tab" class="tab-content">
                        <h2>💸 Withdraw Funds</h2>
                        <div class="balance-overview">
                            <div>Available Balance: $2,450.00</div>
                            <div>Pending Withdrawals: $200.00</div>
                            <div>Minimum Withdrawal Limit: $10.00</div>
                        </div>

  <form id="withdrawForm">
                            <div class="form-group">
                                <label for="withdraw-amount">Enter Withdrawal Amount</label>
                                <input type="number" id="withdraw-amount" placeholder="Enter Amount" value="200" oninput="calculateNetAmount()">
                            </div>
                            <div class="form-group">
                                <label for="withdraw-currency">Currency</label>
                                <select id="withdraw-currency" onchange="calculateNetAmount()">
                                    <option value="USD">USD</option>
                                    <option value="NGN">NGN</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>You will receive: <span id="net-amount">$195.00 (after 2.5% fee)</span></label>
                            </div>
                            <div class="withdrawal-methods">
                                <div class="method-card" onclick="selectMethod('bank-withdraw')">🏦 Bank Transfer</div>
                                <div class="method-card" onclick="selectMethod('crypto-withdraw')">🔗 Crypto Wallet</div>
                                <div class="method-card" onclick="selectMethod('mobile-withdraw')">📲 Mobile Money</div>
                            </div>
                            <div id="destination-details" class="payment-details">
                                <!-- Dynamic content will be inserted here -->
                            </div>
                            <div class="form-group security-field">
                                <label for="security-code">Security (Enter OTP / 2FA Code)</label>
                                <input type="text" id="security-code" placeholder="Enter OTP / 2FA Code">
                            </div>
                            <div class="form-group security-field">
                                <label for="withdrawal-pin">Withdrawal PIN (Optional 🔒)</label>
                                <input type="password" id="withdrawal-pin" placeholder="Enter PIN">
                            </div>
                            <button type="button" class="submit-btn" onclick="confirmWithdrawal()">✅ Submit Withdrawal</button>
                        </form>

  <div class="status-section" style="margin-top: 1rem; color: #666;">
                            <p>Processing Time: Bank transfers take 1–2 business days.</p>
                        </div>

  <h3>Recent Transactions (Withdrawals)</h3>
                        <table class="transactions-table">
                            <thead>
                                <tr>
                                    <th>Date</th>
                                    <th>Method</th>
                                    <th>Amount</th>
                                    <th>Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Sept 4, 25</td>
                                    <td>Bank Transfer</td>
                                    <td>$200</td>
                                    <td><span class="status status-pending">⏳ Pending</span></td>
                                </tr>
                                <tr>
                                    <td>Sept 2, 25</td>
                                    <td>Crypto (USDT)</td>
                                    <td>$100</td>
                                    <td><span class="status status-completed">✅ Completed</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </section>
 <!-- Other sections remain unchanged but can be added as needed -->
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
            document.querySelector(`.tab-button[onclick="showTab('${tab}')"]`).classList.add('active');

            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            document.getElementById(`${tab}-tab`).classList.add('active');

            if (tab === 'deposit') {
                calculateNetDeposit();
            } else if (tab === 'withdraw') {
                calculateNetAmount();
            }
        }

        // Method Selection
        function selectMethod(method) {
            const depositForm = document.getElementById('depositForm');
            const paymentDetails = document.getElementById('payment-details');
            const withdrawForm = document.getElementById('withdrawForm');
            const destinationDetails = document.getElementById('destination-details');

            if (method.includes('bank') || method.includes('crypto') || method.includes('mobile')) {
                withdrawForm.classList.remove('hidden');
                depositForm.classList.add('hidden');
                document.querySelectorAll('.withdrawal-methods .method-card').forEach(card => card.classList.remove('active'));
                document.querySelector(`.withdrawal-methods .method-card[onclick="selectMethod('${method}')"]`).classList.add('active');
                destinationDetails.innerHTML = '';
                switch (method) {
                    case 'bank-withdraw':
                        destinationDetails.innerHTML = `
                            <div class="form-group">
                                <label for="bank-name">Bank Name</label>
                                <select id="bank-name">
                                    <option value="GTBank">GTBank</option>
                                    <option value="Zenith">Zenith</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="account-number">Account Number</label>
                                <input type="text" id="account-number" placeholder="Enter Account Number" value="0123456789">
                            </div>
                            <div class="form-group">
                                <label for="account-holder">Account Holder Name</label>
                                <input type="text" id="account-holder" placeholder="Enter Account Holder Name" value="MarketFlowFX Ltd">
                            </div>
                            <div class="form-group">
                                <label for="branch">Branch (Optional)</label>
                                <input type="text" id="branch" placeholder="Enter Branch">
                            </div>
                            <div class="form-group save-default">
                                <input type="checkbox" id="save-default"> <label for="save-default">✔ Save as Default</label>
                            </div>
                        `;
                        break;
                    case 'crypto-withdraw':
                        destinationDetails.innerHTML = `
                            <div class="form-group">
                                <label for="crypto-coin">Select Coin</label>
                                <select id="crypto-coin">
                                    <option value="USDT">USDT</option>
                                    <option value="BTC">BTC</option>
                                    <option value="ETH">ETH</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="network-type">Network Type</label>
                                <select id="network-type">
                                    <option value="TRC20">TRC20</option>
                                    <option value="ERC20">ERC20</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="wallet-address">Wallet Address</label>
                                <input type="text" id="wallet-address" placeholder="Enter Wallet Address" value="0xAB123456789CDEFFED1234...">
                                <button class="copy-btn" onclick="copyToClipboard(document.getElementById('wallet-address').value)">📋 Copy</button>
                            </div>
                        `;
                        break;
                    case 'mobile-withdraw':
                        destinationDetails.innerHTML = `
                            <div class="form-group">
                                <label for="provider">Mobile Money Provider</label>
                                <select id="provider">
                                    <option value="MTN">MTN</option>
                                    <option value="Airtel">Airtel</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="phone-number">Phone Number</label>
                                <input type="text" id="phone-number" placeholder="Enter Phone Number" value="+2348012345678">
                            </div>
                            <div class="form-group">
                                <label for="account-name">Account Name</label>
                                <input type="text" id="account-name" placeholder="Enter Account Name" value="John Doe">
                            </div>
                        `;
                        break;
                }
            } else {
                depositForm.classList.remove('hidden');
                withdrawForm.classList.add('hidden');
                document.querySelectorAll('.deposit-methods .method-card').forEach(card => card.classList.remove('active'));
                document.querySelector(`.deposit-methods .method-card[onclick="selectMethod('${method}')"]`).classList.add('active');
                paymentDetails.innerHTML = '';
                const referenceCode = `DEP${Math.floor(Math.random() * 100000)}`;
                switch (method) {
                    case 'bank':
                        paymentDetails.innerHTML = `
                            <div class="form-group">
                                <label>Bank Name: GTBank</label>
                            </div>
                            <div class="form-group">
                                <label>Account Name: MarketFlowFX Ltd</label>
                            </div>
                            <div class="form-group">
                                <label>Account Number: 0123456789</label>
                            </div>
                            <div class="form-group">
                                <label>Reference Code: ${referenceCode}</label>
                            </div>
                            <div class="form-group">
                                <label>📎 Upload Proof of Payment</label>
                                <input type="file">
                            </div>
                        `;
                        break;
                    case 'card':
                        paymentDetails.innerHTML = `
                            <div class="form-group">
                                <label>Card Details</label>
                                <input type="text" placeholder="Card Number">
                                <input type="text" placeholder="Expiry (MM/YY)">
                                <input type="text" placeholder="CVV">
                            </div>
                            <p>Auto processed - Redirects to payment gateway.</p>
                        `;
                        break;
                    case 'crypto':
                        paymentDetails.innerHTML = `
                            <div class="form-group">
                                <label for="crypto-coin">Select Coin</label>
                                <select id="crypto-coin">
                                    <option value="BTC">BTC</option>
                                    <option value="USDT">USDT</option>
                                    <option value="ETH">ETH</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Wallet Address: 0xAB123456789CDEFFED1234...</label>
                                <button class="copy-btn" onclick="copyToClipboard('0xAB123456789CDEFFED1234...')">📋 Copy</button>
                            </div>
                            <div class="form-group">
                                <img src="https://via.placeholder.com/100" alt="QR Code" style="margin-top: 0.5rem;">
                            </div>
                        `;
                        break;
                }
            }
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => alert('Copied to clipboard!'));
        }

        function calculateNetDeposit() {
            const amount = parseFloat(document.getElementById('deposit-amount').value) || 0;
            const currency = document.getElementById('deposit-currency').value;
            const feeRate = 0.025; // 2.5% fee
            const fee = amount * feeRate;
            const netDeposit = amount - fee;
            document.getElementById('net-deposit').textContent = `${currency} ${netDeposit.toFixed(2)} (after ${feeRate * 100}% fee)`;
        }

        function calculateNetAmount() {
            const amount = parseFloat(document.getElementById('withdraw-amount').value) || 0;
            const currency = document.getElementById('withdraw-currency').value;
            const feeRate = 0.025; // 2.5% fee
            const fee = amount * feeRate;
            const netAmount = amount - fee;
            document.getElementById('net-amount').textContent = `${currency} ${netAmount.toFixed(2)} (after ${feeRate * 100}% fee)`;
        }

        function confirmDeposit() {
            if (confirm('Are you sure you want to confirm this deposit?')) {
                alert('Deposit submitted successfully! ✅');
            }
        }

        function confirmWithdrawal() {
            if (confirm('Are you sure you want to submit this withdrawal?')) {
                alert('Withdrawal submitted successfully! ✅');
            }
        }

        window.onload = () => {
            login();
            calculateNetDeposit(); // Initialize net deposit display
            calculateNetAmount(); // Initialize net withdrawal display
        };
    </script>
</body>
</html>
