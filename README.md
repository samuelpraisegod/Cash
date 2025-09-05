import tkinter as tk
from tkinter import messagebox
import json
import os

# Data for Prop Firms (account sizes, prices, and challenge rules)
prop_firms = {
    "FTMO": {
        "accounts": [
            {"size": "$1,000", "price": "$13"},
            {"size": "$2,000", "price": "$17"},
            {"size": "$5,000", "price": "$30"},
            {"size": "$10,000", "price": "$155"},
            {"size": "$200,000", "price": "$1,080"}
        ],
        "challenge_rules": "Must hit 10% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily loss, 10% max drawdown."
    },
    "MyForexFunds": {
        "accounts": [
            {"size": "$10,000", "price": "$49"},
            {"size": "$50,000", "price": "$299"},
            {"size": "$200,000", "price": "$999"}
        ],
        "challenge_rules": "Must hit 8% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily drawdown, 12% max drawdown."
    },
    "E8 Funding": {
        "accounts": [
            {"size": "$25,000", "price": "$228"},
            {"size": "$100,000", "price": "$398"},
            {"size": "$400,000", "price": "$998"}
        ],
        "challenge_rules": "Must hit 8% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily drawdown, 8% max loss."
    },
    "The Funded Trader": {
        "accounts": [
            {"size": "$50,000", "price": "$299"},
            {"size": "$100,000", "price": "$499"},
            {"size": "$200,000", "price": "$899"}
        ],
        "challenge_rules": "Must hit 10% profit target in 35 days (Step 1), 5% in 60 days (Step 2), max 6% daily loss, 12% max drawdown."
    },
    "System/Partner Will Choose": {
        "accounts": [{"size": "N/A", "price": "N/A"}],
        "challenge_rules": "No specific challenge rules; system or partner will select the Prop Firm and account size."
    }
}

class PropFirmApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Prop Firm Co-Funding Request")
        self.root.geometry("600x700")

   # Variables
  self.selected_firm = tk.StringVar(value="System/Partner Will Choose")
        self.selected_account = tk.StringVar(value="N/A")
        self.funding_amount = tk.StringVar()
        self.ratio = tk.StringVar()

   # Step 1: Prop Firm Selection
   tk.Label(root, text="Step 1: Select Prop Firm", font=("Arial", 12, "bold")).pack(pady=10)
        firm_dropdown = tk.OptionMenu(root, self.selected_firm, *prop_firms.keys(), command=self.update_account_sizes)
        firm_dropdown.pack(pady=5)

   # Step 2: Account Sizes
   tk.Label(root, text="Step 2: Select Account Size", font=("Arial", 12, "bold")).pack(pady=10)
        self.account_frame = tk.Frame(root)
        self.account_frame.pack(pady=5)
        self.update_account_sizes(self.selected_firm.get())

  # Step 3: Challenge Rules
  tk.Label(root, text="Step 3: Challenge Rules", font=("Arial", 12, "bold")).pack(pady=10)
        self.challenge_label = tk.Label(root, text=prop_firms[self.selected_firm.get()]["challenge_rules"], wraplength=500, justify="left")
        self.challenge_label.pack(pady=5)

  # Step 4: Co-Funding Details
  tk.Label(root, text="Step 4: Co-Funding Details", font=("Arial", 12, "bold")).pack(pady=10)
        tk.Label(root, text="Funding Amount ($):").pack()
        tk.Entry(root, textvariable=self.funding_amount).pack(pady=5)
        tk.Label(root, text="Co-Funding Ratio (e.g., 50:50):").pack()
        tk.Entry(root, textvariable=self.ratio).pack(pady=5)

  # Recent Results Placeholder
   tk.Label(root, text="Recent Results", font=("Arial", 12, "bold")).pack(pady=10)
        tk.Label(root, text="Placeholder for recent results (e.g., success rates, payouts).", wraplength=500).pack(pady=5)

  # Submit Button
  tk.Button(root, text="Submit Request", command=self.submit_request).pack(pady=20)

 def update_account_sizes(self, firm):
        # Clear previous radio buttons
        for widget in self.account_frame.winfo_children():
            widget.destroy()

  # Populate new radio buttons for account sizes
  for account in prop_firms[firm]["accounts"]:
            tk.Radiobutton(
                self.account_frame,
                text=f"{account['size']} - {account['price']}",
                variable=self.selected_account,
                value=account["size"],
                anchor="w"
            ).pack(fill="x", padx=10)

  # Update challenge rules
  self.challenge_label.config(text=prop_firms[firm]["challenge_rules"])

   def submit_request(self):
        # Validate inputs
        firm = self.selected_firm.get()
        account_size = self.selected_account.get()
        funding_amount = self.funding_amount.get()
        ratio = self.ratio.get()

  if not funding_amount or not ratio:
            messagebox.showerror("Error", "Please fill in all co-funding details.")
            return

  try:
            float(funding_amount)
            if not (":" in ratio and all(part.isdigit() for part in ratio.split(":"))):
                raise ValueError
        except ValueError:
            messagebox.showerror("Error", "Funding amount must be a number, and ratio must be in format 'X:Y' (e.g., 50:50).")
            return

  # Save request to JSON
   request = {
            "prop_firm": firm,
            "account_size": account_size,
            "funding_amount": funding_amount,
            "ratio": ratio
        }

   # Load existing requests or create new list
  requests = []
        if os.path.exists("requests.json"):
            with open("requests.json", "r") as f:
                requests = json.load(f)

   requests.append(request)
        with open("requests.json", "w") as f:
            json.dump(requests, f, indent=4)

   messagebox.showinfo("Success", "Co-funding request submitted successfully!")
        # Clear inputs
        self.funding_amount.set("")
        self.ratio.set("")
        self.selected_firm.set("System/Partner Will Choose")
        self.selected_account.set("N/A")
        self.update_account_sizes("System/Partner Will Choose")

def main():
    root = tk.Tk()
    app = PropFirmApp(root)
    root.mainloop()

if __name__ == "__main__":
    main()
