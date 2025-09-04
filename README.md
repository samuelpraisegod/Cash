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

  /* Deposit Section */
        .deposit-methods {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
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

  .payment-details {
            margin-bottom: 1.5rem;
        }

   .confirm-btn {
            background: var(--green);
            color: var(--white);
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
            border: none;
            border-radius: 20px;
            cursor: pointer;
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

  .status-completed { background: var(--green); }
        .status-pending { background: #ffc107; }

   /* Withdrawal Section */
        .withdrawal-methods {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

  .security-field {
            margin-top: 1rem;
        }

  .submit-btn {
            background: var(--primary);
            color: var(--white);
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
            border: none;
            border-radius: 20px;
            cursor: pointer;
        }

  /* Responsive Design */
        @media (max-width: 768px) {
            .deposit-methods, .withdrawal-methods {
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
                        <li><a href="#deposit"><span role="img" aria-label="plus-money">➕💵</span> Deposit</a></li>
                        <li><a href="#withdraw"><span role="img" aria-label="withdraw">💸</span> Withdraw</a></li>
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
<!-- Deposit Section -->
                <section id="deposit">
                    <h2>➕ Deposit Funds</h2>
                    <div class="deposit-methods">
                        <div class="method-card" onclick="selectMethod('bank')">💳 Bank Transfer</div>
                        <div class="method-card" onclick="selectMethod('card')">💵 Card Payment</div>
                        <div class="method-card" onclick="selectMethod('crypto')">🔗 Crypto Deposit</div>
                        <div class="method-card" onclick="selectMethod('mobile')">📲 Mobile Money</div>
                    </div>
       <form id="depositForm" class="hidden">
                        <div class="form-group">
                            <label for="deposit-amount">Amount</label>
                            <input type="number" id="deposit-amount" placeholder="Enter Amount" value="500">
                        </div>
                        <div class="form-group">
                            <label for="deposit-currency">Currency</label>
                            <select id="deposit-currency">
                                <option value="USD">USD</option>
                                <option value="NGN">NGN</option>
                            </select>
                        </div>
                        <div id="payment-details" class="payment-details">
                            <!-- Dynamic content will be inserted here -->
                        </div>
                        <button type="button" class="confirm-btn" onclick="confirmDeposit()">✅ Confirm Deposit</button>
                    </form>
       <h3>Recent Deposits</h3>
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
                                <td>01 Sept, 25</td>
                                <td>Card</td>
                                <td>$200</td>
                                <td><span class="status status-completed">✅ Completed</span></td>
                            </tr>
                            <tr>
                                <td>29 Aug, 25</td>
                                <td>Bank</td>
                                <td>$150</td>
                                <td><span class="status status-pending">⏳ Pending</span></td>
                            </tr>
                        </tbody>
                    </table>
                </section>
 <!-- Withdrawal Section -->
                <section id="withdraw">
                    <h2>💸 Withdraw Funds</h2>
                    <div class="form-group">
                        <label>Available Balance: $2,450.00</label>
                    </div>
                    <form id="withdrawForm">
                        <div class="form-group">
                            <label for="withdraw-amount">Amount</label>
                            <input type="number" id="withdraw-amount" placeholder="Enter Amount" value="200">
                        </div>
                        <div class="withdrawal-methods">
                            <div class="method-card" onclick="selectMethod('bank-withdraw')">🏦 Bank Account</div>
                            <div class="method-card" onclick="selectMethod('crypto-withdraw')">🔗 Crypto Wallet</div>
                            <div class="method-card" onclick="selectMethod('mobile-withdraw')">📲 Mobile Money</div>
                        </div>
                        <div id="destination-details" class="form-group">
                            <label for="destination">Destination</label>
                            <input type="text" id="destination" placeholder="Wallet Address / Bank Account">
                        </div>
                        <div class="security-field form-group">
                            <label for="security-code">Security (Enter OTP / PIN)</label>
                            <input type="text" id="security-code" placeholder="Enter OTP / PIN">
                        </div>
                        <button type="button" class="submit-btn" onclick="confirmWithdrawal()">✅ Submit Withdrawal</button>
                    </form>
       <h3>Recent Withdrawals</h3>
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
                                <td>02 Sept, 25</td>
                                <td>Bank</td>
                                <td>$200</td>
                                <td><span class="status status-pending">⏳ Pending</span></td>
                            </tr>
                            <tr>
                                <td>30 Aug, 25</td>
                                <td>Crypto</td>
                                <td>$100</td>
                                <td><span class="status status-completed">✅ Completed</span></td>
                            </tr>
                        </tbody>
                    </table>
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

        // Deposit Method Selection
        function selectMethod(method) {
            const depositForm = document.getElementById('depositForm');
            const paymentDetails = document.getElementById('payment-details');
            depositForm.classList.remove('hidden');

            // Reset active class
            document.querySelectorAll('.method-card').forEach(card => card.classList.remove('active'));
            document.querySelector(`.method-card[onclick="selectMethod('${method}')"]`).classList.add('active');

            // Dynamic payment details
            paymentDetails.innerHTML = '';
            switch (method) {
                case 'bank':
                    paymentDetails.innerHTML = `
                        <label>Bank Details</label>
                        <p>Account No: 1234567890</p>
                        <p>Bank Name: Example Bank</p>
                        <input type="file" placeholder="Upload Proof">
                    `;
                    break;
                case 'card':
                    paymentDetails.innerHTML = `
                        <label>Card Details</label>
                        <input type="text" placeholder="Card Number">
                        <input type="text" placeholder="Expiry (MM/YY)">
                        <input type="text" placeholder="CVV">
                    `;
                    break;
                case 'crypto':
                    paymentDetails.innerHTML = `
                        <label>Crypto Details</label>
                        <p>Wallet Address: 1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa</p>
                        <img src="https://via.placeholder.com/100" alt="QR Code" style="margin-top: 0.5rem;">
                    `;
                    break;
                case 'mobile':
                    paymentDetails.innerHTML = `
                        <label>Mobile Money Details</label>
                        <input type="text" placeholder="Phone Number">
                    `;
                    break;
            }
        }

        // Withdrawal Method Selection (simplified, can be expanded)
        function selectMethod(method) {
            const destinationDetails = document.getElementById('destination-details');
            document.querySelectorAll('.withdrawal-methods .method-card').forEach(card => card.classList.remove('active'));
            document.querySelector(`.withdrawal-methods .method-card[onclick="selectMethod('${method}')"]`).classList.add('active');
            destinationDetails.querySelector('input').placeholder = method.includes('bank') ? 'Bank Account Number' : 'Wallet Address / Phone Number';
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
        };
    </script>
</body>
</html>
