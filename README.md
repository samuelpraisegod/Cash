<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Prop Firm Test</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    .box { background: #f9f9f9; padding: 20px; border-radius: 8px; max-width: 500px; }
    label { font-weight: bold; margin-top: 10px; display: block; }
    select, .accounts, .challenge { margin-top: 10px; }
    .accounts div { margin: 5px 0; }
    .hidden { display: none; }
  </style>
</head>
<body>

  <div class="box">
    <h2>🤝 Co-Funding – Prop Firm Selection (Test)</h2>
 <!-- Step 1: Select Prop Firm -->
    <label for="propFirm">Select Prop Firm:</label>
    <select id="propFirm">
      <option value="">-- Choose Prop Firm --</option>
      <option value="ftmo">FTMO</option>
      <option value="mff">MyForexFunds</option>
      <option value="e8">E8 Funding</option>
    </select>
 <!-- Step 2: Account Sizes -->
    <div id="accountOptions" class="accounts hidden"></div>
 <!-- Step 3: Challenge Phrase -->
    <div id="challengePhrase" class="challenge hidden"></div>
  </div>

  <script>
    // Dummy data for testing
    const propFirms = {
      ftmo: {
        accounts: [
          { size: "$1,000", price: "$13" },
          { size: "$2,000", price: "$17" },
          { size: "$5,000", price: "$30" }
        ],
        challenge: "FTMO Challenge: 10% profit target, 5% daily loss, 30-day phase."
      },
      mff: {
        accounts: [
          { size: "$1,000", price: "$10" },
          { size: "$2,000", price: "$15" },
          { size: "$5,000", price: "$25" }
        ],
        challenge: "MFF Challenge: 8% profit target, 5% daily loss, 60-day phase."
      },
      e8: {
        accounts: [
          { size: "$2,500", price: "$20" },
          { size: "$5,000", price: "$35" }
        ],
        challenge: "E8 Funding Challenge: 8% profit target, 5% drawdown, 30-day phase."
      }
    };

    const propFirmSelect = document.getElementById("propFirm");
    const accountOptions = document.getElementById("accountOptions");
    const challengePhrase = document.getElementById("challengePhrase");

    propFirmSelect.addEventListener("change", function() {
      const selected = this.value;

      if (!selected) {
        accountOptions.classList.add("hidden");
        challengePhrase.classList.add("hidden");
        return;
      }

      const firm = propFirms[selected];

      // Show account sizes
      accountOptions.innerHTML = "<label>Available Accounts:</label>";
      firm.accounts.forEach(acc => {
        accountOptions.innerHTML += `<div>📊 ${acc.size} → ${acc.price}</div>`;
      });
      accountOptions.classList.remove("hidden");

      // Show challenge phrase
      challengePhrase.innerHTML = `<label>Challenge:</label><p>${firm.challenge}</p>`;
      challengePhrase.classList.remove("hidden");
    });
  </script>

</body>
</html>
