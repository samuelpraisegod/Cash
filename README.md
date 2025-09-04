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
        <p>“Create a co-fund request by selecting an amount. Your deposit will be locked in escrow until matched. The system will match co-funders and auto-purchase the prop firm account upon agreement.”</p>
        <form id="co-fund-form">
            <div class="form-group">
                <label for="co-fund-amount">Co-Fund Amount</label>
                <select id="co-fund-amount" onchange="calculatePercentage()">
                    <option value="500">$500</option>
                    <option value="1000">$1,000</option>
                    <option value="2500">$2,500</option>
                    <option value="5000">$5,000</option>
                </select>
            </div>
            <div class="form-group">
                <label for="profit-ratio">Profit Ratio</label>
                <select id="profit-ratio">
                    <option value="50:50">50:50</option>
                    <option value="60:40">60:40</option>
                    <option value="70:30">70:30</option>
                </select>
            </div>
            <div class="form-group">
                <label for="your-contribution">Your Contribution ($)</label>
                <input type="number" id="your-contribution" placeholder="e.g., $250" min="0" onchange="calculatePercentage()">
            </div>
            <div class="form-group">
                <label for="account-size">Account Size ($)</label>
                <input type="number" id="account-size" placeholder="e.g., $1,000" min="0" onchange="calculatePercentage()">
            </div>
            <div class="form-group">
                <label for="percentage-contribution">Percentage of Contribution (%)</label>
                <input type="text" id="percentage-contribution" readonly>
            </div>
            <div class="form-group">
                <label>Type of Trader</label>
                <div>
                    <input type="radio" id="scalping" name="trader-type" value="Scalping" checked>
                    <label for="scalping">Scalping</label>
                    <input type="radio" id="swing" name="trader-type" value="Swing">
                    <label for="swing">Swing</label>
                    <input type="radio" id="algo" name="trader-type" value="Algo">
                    <label for="algo">Algo</label>
                </div>
            </div>
            <div class="form-group">
                <label for="track-record">Track Record Upload</label>
                <input type="file" id="track-record" accept="image/*,.pdf">
            </div>
            <button type="button" class="confirm-btn" onclick="submitCoFundRequest()">Submit Request</button>
        </form>
        <div class="status-tracker" style="margin-top: 1rem; color: #666;">Status: <span class="status status-pending">Pending</span></div>
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
