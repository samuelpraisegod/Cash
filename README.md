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
            display: grid;
            grid-template-columns: 250px 1fr;
            min-height: calc(100vh - 60px);
        }

  .sidebar {
            background: var(--white);
            padding: 1rem;
            position: sticky;
            top: 60px;
            height: calc(100vh - 60px);
            border-right: 1px solid #eee;
        }

  .sidebar ul {
            list-style: none;
            padding: 0;
        }

  .sidebar ul li a {
            display: block;
            padding: 0.5rem;
            color: var(--text);
            text-decoration: none;
        }

  .sidebar ul li a:hover {
            background: var(--light-bg);
            border-radius: 5px;
        }

  .main-content {
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
            .dashboard {
                grid-template-columns: 1fr;
            }
            .sidebar {
                position: static;
                height: auto;
            }
            .hero h1 {
                font-size: 1.5rem;
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
            <nav class="sidebar">
                <ul>
                    <li><a href="#requests">Requests</a></li>
                    <li><a href="#active-orders">Active Orders</a></li>
                </ul>
            </nav>
            <main class="main-content">
                <section id="requests">
                    <h2>Request System</h2>
                    <div class="tabs">
                        <button class="tab-btn active" onclick="openTab('co-funding')">Co-Funding</button>
                        <button class="tab-btn" onclick="openTab('dashboard')">Dashboard</button>
                    </div>
                    <div id="co-funding" class="tab-content active">
                        <h3>Co-Funding Request</h3>
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
                    </div>
                    <div id="dashboard" class="tab-content">
                        <h3>Dashboard</h3>
                        <p>View and manage all your requests and agreements.</p>
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
                                <tr>
                                    <td>Co-Funding</td>
                                    <td>FTMO, $25k</td>
                                    <td><span class="status status-active">Accepted</span></td>
                                    <td><button class="btn btn-primary">View</button></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </section>
                <section id="active-orders">
                    <h2>Active Orders</h2>
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
                                <td>#ORD001</td>
                                <td>Co-Funding</td>
                                <td><span class="status status-active">Active</span></td>
                            </tr>
                            <tr>
                                <td>#ORD002</td>
                                <td>Co-Funding</td>
                                <td><span class="status status-active">Active</span></td>
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

        function login() {
            isLoggedIn = true;
            updateUI();
        }

        function logout() {
            isLoggedIn = false;
            updateUI();
        }

        function openTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById(tabName).classList.add('active');
            document.querySelector(`button[onclick="openTab('${tabName}')"]`).classList.add('active');
        }
 // Simulate initial login for testing
        window.onload = () => {
            login(); // Automatically log in to show dashboard
        };
    </script>
</body>
</html>
