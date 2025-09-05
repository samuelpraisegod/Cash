<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prop Firm Co-Funding Platform</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px; }
        h2 { font-size: 18px; margin-top: 20px; }
        label { display: block; margin-bottom: 5px; }
        input, select { width: 100%; padding: 8px; margin-bottom: 10px; box-sizing: border-box; }
        .account-options { margin-bottom: 10px; }
        .share-display { font-weight: bold; }
        button { padding: 10px 20px; margin-right: 10px; cursor: pointer; }
        #pending-modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); justify-content: center; align-items: center; }
        #pending-content { background: white; padding: 20px; max-width: 500px; width: 90%; max-height: 80%; overflow-y: auto; }
        #pending-list { list-style: none; padding: 0; }
        #pending-list li { margin-bottom: 10px; border-bottom: 1px solid #ddd; padding-bottom: 10px; }
    </style>
</head>
<body>
    <h1>Prop Firm Co-Funding Platform</h1>
 <!-- Step 1: Prop Firm Selection -->
    <h2>Step 1: Select Prop Firm</h2>
    <select id="prop-firm">
        <option value="System/Partner Will Choose">System/Partner Will Choose</option>
        <option value="FTMO">FTMO</option>
        <option value="MyForexFunds">MyForexFunds</option>
        <option value="E8 Funding">E8 Funding</option>
        <option value="The Funded Trader">The Funded Trader</option>
    </select>
 <!-- Step 2: Account Sizes -->
    <h2>Step 2: Select Account Size</h2>
    <div id="account-options" class="account-options"></div>
  <!-- Step 3: Challenge Rules -->
    <h2>Step 3: Challenge Rules</h2>
    <p id="challenge-rules">No specific challenge rules; system or partner will select the Prop Firm and account size.</p>
 <!-- Step 4: Co-Funding Details -->
    <h2>Step 4: Co-Funding Details</h2>
    <label for="profit-split">Profit Split Ratio (e.g., 50:50 for requester:co-funder):</label>
    <input type="text" id="profit-split" value="50:50">

 <label>Your Contribution (Requester's Share):</label>
    <span id="requester-share" class="share-display">N/A</span>

  <label>Co-Funder's Contribution:</label>
    <span id="co-funder-share" class="share-display">N/A</span>

<!-- Buttons -->
 <button id="submit-request">Submit Request</button>
    <button id="view-pending">View Pending Requests</button>

  <!-- Recent Results Placeholder -->
 <h2>Recent Results</h2>
    <p>Placeholder for recent results (e.g., success rates, payouts).</p>

    <!-- Pending Requests Modal -->
 <div id="pending-modal">
        <div id="pending-content">
            <h2>Pending Requests</h2>
            <ul id="pending-list"></ul>
            <button id="close-modal">Close</button>
        </div>
    </div>

 <script>
        // Data for Prop Firms
        const propFirms = {
            "FTMO": {
                "accounts": [
                    { "size": "$1,000", "price": 13.0 },
                    { "size": "$2,000", "price": 17.0 },
                    { "size": "$5,000", "price": 30.0 },
                    { "size": "$10,000", "price": 155.0 },
                    { "size": "$100,000", "price": 500.0 },
                    { "size": "$200,000", "price": 1080.0 }
                ],
                "challenge_rules": "Must hit 10% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily loss, 10% max drawdown."
            },
            "MyForexFunds": {
                "accounts": [
                    { "size": "$10,000", "price": 49.0 },
                    { "size": "$50,000", "price": 299.0 },
                    { "size": "$200,000", "price": 999.0 }
                ],
                "challenge_rules": "Must hit 8% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily drawdown, 12% max drawdown."
            },
            "E8 Funding": {
                "accounts": [
                    { "size": "$25,000", "price": 228.0 },
                    { "size": "$100,000", "price": 398.0 },
                    { "size": "$400,000", "price": 998.0 }
                ],
                "challenge_rules": "Must hit 8% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily drawdown, 8% max loss."
            },
            "The Funded Trader": {
                "accounts": [
                    { "size": "$50,000", "price": 299.0 },
                    { "size": "$100,000", "price": 499.0 },
                    { "size": "$200,000", "price": 899.0 }
                ],
                "challenge_rules": "Must hit 10% profit target in 35 days (Step 1), 5% in 60 days (Step 2), max 6% daily loss, 12% max drawdown."
            },
            "System/Partner Will Choose": {
                "accounts": [{ "size": "N/A", "price": 0.0 }],
                "challenge_rules": "No specific challenge rules; system or partner will select the Prop Firm and account size."
            }
        };

        // Elements
        const firmSelect = document.getElementById('prop-firm');
        const accountOptions = document.getElementById('account-options');
        const challengeRules = document.getElementById('challenge-rules');
        const profitSplitInput = document.getElementById('profit-split');
        const requesterShare = document.getElementById('requester-share');
        const coFunderShare = document.getElementById('co-funder-share');
        const submitButton = document.getElementById('submit-request');
        const viewPendingButton = document.getElementById('view-pending');
        const pendingModal = document.getElementById('pending-modal');
        const pendingList = document.getElementById('pending-list');
        const closeModalButton = document.getElementById('close-modal');

        let selectedAccount = 'N/A';
        let accountPrice = 0.0;

        // Load requests from localStorage
        function loadRequests() {
            return JSON.parse(localStorage.getItem('requests')) || [];
        }

        // Save requests to localStorage
        function saveRequests(requests) {
            localStorage.setItem('requests', JSON.stringify(requests));
        }

        // Update account sizes
        function updateAccountSizes() {
            const firm = firmSelect.value;
            accountOptions.innerHTML = '';
            selectedAccount = 'N/A';
            accountPrice = 0.0;

            propFirms[firm].accounts.forEach(acc => {
                const label = document.createElement('label');
                const radio = document.createElement('input');
                radio.type = 'radio';
                radio.name = 'account-size';
                radio.value = acc.size;
                radio.addEventListener('change', () => {
                    selectedAccount = acc.size;
                    accountPrice = acc.price;
                    calculateShares();
                });
                label.appendChild(radio);
                label.appendChild(document.createTextNode(` ${acc.size} - $${acc.price.toFixed(2)}`));
                accountOptions.appendChild(label);
            });

            challengeRules.textContent = propFirms[firm].challenge_rules;
            calculateShares();
        }

        // Calculate shares
        function calculateShares() {
            const profitSplit = profitSplitInput.value || '50:50';
            if (selectedAccount === 'N/A') {
                requesterShare.textContent = 'N/A';
                coFunderShare.textContent = 'N/A';
                return;
            }

            try {
                const [reqPart, coPart] = profitSplit.split(':').map(Number);
                const totalParts = reqPart + coPart;
                if (totalParts === 0) throw new Error();
                const reqShare = (reqPart / totalParts) * accountPrice;
                const coShare = (coPart / totalParts) * accountPrice;
                requesterShare.textContent = `$${reqShare.toFixed(2)} (Locked in Escrow)`;
                coFunderShare.textContent = `$${coShare.toFixed(2)} (Awaiting Co-Funder)`;
            } catch {
                requesterShare.textContent = 'Invalid Ratio';
                coFunderShare.textContent = 'Invalid Ratio';
            }
        }

        // Submit request
        function submitRequest() {
            const firm = firmSelect.value;
            if (firm === 'System/Partner Will Choose' || selectedAccount === 'N/A') {
                alert('Please select a valid Prop Firm and Account Size.');
                return;
            }

            const profitSplit = profitSplitInput.value || '50:50';
            if (!profitSplit.includes(':')) {
                alert('Please enter a valid profit split ratio (e.g., 50:50).');
                return;
            }

            const reqShareText = requesterShare.textContent;
            if (reqShareText.includes('Invalid')) {
                alert('Invalid share calculation.');
                return;
            }

            const reqShareVal = parseFloat(reqShareText.replace('$', '').split(' ')[0]);
            const coShareVal = parseFloat(coFunderShare.textContent.replace('$', '').split(' ')[0]);

            const requests = loadRequests();
            const newRequest = {
                id: requests.length + 1,
                prop_firm: firm,
                account_size: selectedAccount,
                account_price: accountPrice,
                profit_split: profitSplit,
                requester_share: reqShareVal,
                co_funder_share: coShareVal,
                status: 'pending'
            };
            requests.push(newRequest);
            saveRequests(requests);

            alert(`Request submitted! Your contribution: $${reqShareVal.toFixed(2)} (Locked in Escrow). Waiting for a co-funder...`);

            // Reset form
            profitSplitInput.value = '50:50';
            firmSelect.value = 'System/Partner Will Choose';
            updateAccountSizes();
        }

        // View pending requests
        function viewPending() {
            const requests = loadRequests();
            const pending = requests.filter(req => req.status === 'pending');
            pendingList.innerHTML = '';

            if (pending.length === 0) {
                alert('No pending co-funding requests.');
                return;
            }

            pending.forEach(req => {
                const li = document.createElement('li');
                li.textContent = `ID: ${req.id} | Firm: ${req.prop_firm} | Size: ${req.account_size} | Price: $${req.account_price.toFixed(2)} | Profit Split: ${req.profit_split} | Requester Share: $${req.requester_share.toFixed(2)} (Escrow) | Co-Funder Share: $${req.co_funder_share.toFixed(2)} | Status: ${req.status}`;
                
                const acceptButton = document.createElement('button');
                acceptButton.textContent = 'Accept as Co-Funder';
                acceptButton.onclick = () => acceptRequest(req.id);
                li.appendChild(acceptButton);
                
                pendingList.appendChild(li);
            });

            pendingModal.style.display = 'flex';
        }

        // Accept request
        function acceptRequest(id) {
            const requests = loadRequests();
            const req = requests.find(r => r.id === id && r.status === 'pending');
            if (!req) return;

            const total = req.requester_share + req.co_funder_share;
            if (Math.abs(total - req.account_price) > 0.01) {
                alert('Total shares do not match account price.');
                return;
            }

            req.status = 'funded';
            saveRequests(requests);
            alert(`Request ID ${id} accepted! Total funded: $${req.account_price.toFixed(2)}. Account ready for purchase.`);
            pendingModal.style.display = 'none';
            viewPending();
        }

        // Event listeners
        firmSelect.addEventListener('change', updateAccountSizes);
        profitSplitInput.addEventListener('input', calculateShares);
        submitButton.addEventListener('click', submitRequest);
        viewPendingButton.addEventListener('click', viewPending);
        closeModalButton.addEventListener('click', () => pendingModal.style.display = 'none');

        // Initial load
        updateAccountSizes();
    </script>
</body>
</html>
