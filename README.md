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
            overflow-x: hidden; /* Prevent horizontal scroll */
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

   .header-title h1 {
            margin: 0;
            font-size: 1.5rem;
        }

  nav ul {
            list-style: none;
            margin: 0;
            padding: 0;
            display: flex;
            gap: 1rem;
        }

   nav ul li a {
            color: var(--white);
            text-decoration: none;
        }

   /* Home Content */
        #home-content {
            text-align: center;
            padding: 2rem;
        }

  .hero {
            max-width: 600px;
            margin: 0 auto;
        }

  .hero h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

  /* Dashboard Layout */
        .dashboard {
            display: flex;
            min-height: calc(100vh - 60px);
        }

   .main-content {
            flex: 1;
            padding: 2rem;
        }

   /* Tabs and Forms */
        .tabs {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

  .tab-btn {
            padding: 0.5rem 1rem;
            border: none;
            background: none;
            cursor: pointer;
            border-bottom: 2px solid transparent;
        }

  .tab-btn.active {
            border-bottom-color: var(--secondary);
            font-weight: bold;
        }

  .tab-content {
            display: none;
        }

   .tab-content.active {
            display: block;
        }

   .form-group {
            margin-bottom: 1rem;
        }

  .form-group label {
            display: block;
            margin-bottom: 0.25rem;
        }

  .form-group select {
            width: 100%;
            padding: 0.5rem;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

  /* Tables */
        table {
            width: 100%;
            border-collapse: collapse;
            background: var(--white);
            box-shadow: 0 2px 5px var(--shadow);
        }

  th, td {
            padding: 0.5rem;
            text-align: left;
            border-bottom: 1px solid #ccc;
        }

   th {
            background: var(--primary);
            color: var(--white);
        }

  /* Status Indicators */
        .status {
            padding: 0.25rem 0.5rem;
            border-radius: 5px;
            color: var(--white);
            font-size: 0.875rem;
        }

   .status-pending { background: #ffc107; }
        .status-active { background: #28a745; }
    /* Buttons */
        .btn {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            text-decoration: none;
        }

  .btn-primary {
            background: var(--secondary);
            color: var(--primary);
        }

  .btn-success {
            background: #28a745;
            color: var(--white);
        }

   .btn:hover {
            opacity: 0.9;
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
            .hero h1 {
                font-size: 1.5rem;
            }
            .hamburger-menu {
                right: -10px; /* Adjust for mobile alignment */
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="header-title">
            <h1>MarketFlow</h1>
        </div>
        <div class="hamburger" onclick="toggleMenu()">
            ☰
            <div class="hamburger-menu">
                <div class="brand">MarketFlow</div>
                <ul>
                    <li><a href="#balance"><span role="img" aria-label="bank">🏦</span> Balance</a></li>
                    <li><a href="#deposit"><span role="img" aria-label="plus">➕</span> Deposit</a></li>
                    <li><a href="#available-funded"><span role="img" aria-label="briefcase">💼</span> Available Funded</a></li>
                    <li><a href="#available-traders"><span role="img" aria-label="people">👥</span> Available Traders</a></li>
                    <li><a href="#co-funding"><span role="img" aria-label="handshake">🤝</span> Co-Funding</a></li>
                    <li><a href="#requests"><span role="img" aria-label="envelope">📩</span> Requests</a></li>
                    <li><a href="#active"><span role="img" aria-label="chart">📊</span> Active</a></li>
                    <li><a href="#orders"><span role="img" aria-label="document">📑</span> Orders</a></li>
                    <li><a href="#completed"><span role="img" aria-label="check">✅</span> Completed</a></li>
                    <li><a href="#profits-withdrawals"><span role="img" aria-label="money">💵</span> Profits & Withdrawals</a></li>
                    <li><a href="#performance-chart"><span role="img" aria-label="graph">📈</span> Performance Chart</a></li>
                    <li><a href="#messages"><span role="img" aria-label="speech">💬</span> Messages</a></li>
                </ul>
            </div>
        </div>
        <nav>
            <ul>
                <li><a href="#" id="auth-btn" class="btn btn-primary">Login</a></li>
            </ul>
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
                    <p>View your current and projected balance.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Account</th>
                                <th>Balance</th>
                                <th>Projected</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Trading Account 1</td>
                                <td>$10,000</td>
                                <td>$12,500</td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <section id="deposit">
                    <h2>Deposit</h2>
                    <p>Manage your deposits.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Date</th>
                                <th>Amount</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>2025-09-03</td>
                                <td>$5,000</td>
                                <td><span class="status status-active">Completed</span></td>
                            </tr>
                        </tbody>
                    </table>
                </section>
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
                <section id="available-traders">
                    <h2>Available Traders</h2>
                    <p>Find traders to collaborate with.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>Experience</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>John Doe</td>
                                <td>2 Years</td>
                                <td><span class="status status-active">Online</span></td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <section id="co-funding">
                    <h2>Co-Funding</h2>
                    <p>Create a co-fund request by selecting an account. Your deposit will be locked in Escrow until matched. The system will match co-funders and auto-purchase the prop firm account upon agreement.</p>
                    <form id="coFundingForm">
                        <div class="form-group">
                            <label for="prop-firm">Prop Firm Name</label>
                            <select id="prop-firm">
                                <option value="ftmo">FTMO</option>
                                <option value="myforexfunds">MyForexFunds</option>
                                <option value="fundednext">FundedNext</option>
                            </select>
                        </div>
                        <button type="submit" class="btn btn-primary">Submit</button>
                    </form>
                </section>
                <section id="requests">
                    <h2>Requests</h2>
                    <p>View and manage your requests.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Type</th>
                                <th>Details</th>
                                <th>Status</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Co-Funding</td>
                                <td>FTMO, $10k</td>
                                <td><span class="status status-pending">Pending</span></td>
                                <td><button class="btn btn-success">Accept</button></td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <section id="active">
                    <h2>Active</h2>
                    <p>View active collaborations.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Order ID</th>
                                <th>Type</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>#ACT001</td>
                                <td>Co-Funding</td>
                                <td><span class="status status-active">Active</span></td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <section id="orders">
                    <h2>Orders</h2>
                    <p>Manage your orders.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Order ID</th>
                                <th>Amount</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>#ORD001</td>
                                <td>$5,000</td>
                                <td><span class="status status-pending">Pending</span></td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <section id="completed">
                    <h2>Completed</h2>
                    <p>View completed transactions.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Order ID</th>
                                <th>Amount</th>
                                <th>Date</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>#COMP001</td>
                                <td>$10,000</td>
                                <td>2025-09-03</td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <section id="profits-withdrawals">
                    <h2>Profits & Withdrawals</h2>
                    <p>Track your profits and withdrawals.</p>
                    <table>
                        <thead>
                            <tr>
                                <th>Type</th>
                                <th>Amount</th>
                                <th>Date</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Profit</td>
                                <td>$2,000</td>
                                <td>2025-09-03</td>
                            </tr>
                        </tbody>
                    </table>
                </section>
                <section id="performance-chart">
                    <h2>Performance Chart</h2>
                    <p>View your trading performance.</p>
                    <div style="height: 300px; background: #eee; text-align: center; padding: 1rem;">Chart Placeholder</div>
                </section>
                <section id="messages">
                    <h2>Messages</h2>
                    <p>Send or view messages.</p>
                    <textarea rows="5" placeholder="Type your message..." style="width: 100%; padding: 0.5rem; border: 1px solid #ccc; border-radius: 5px;"></textarea>
                    <button class="btn btn-primary" style="margin-top: 0.5rem;">Send</button>
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

        // Simulate initial login for testing
        window.onload = () => {
            login(); // Automatically log in to show dashboard
        };
    </script>
</body>
</html>
