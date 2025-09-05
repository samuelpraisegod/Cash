import tkinter as tk
from tkinter import messagebox, Toplevel, Listbox, Scrollbar
import json
import os

# Data for Prop Firms (account sizes, prices, and challenge rules)
prop_firms = {
    "FTMO": {
        "accounts": [
            {"size": "$1,000", "price": 13.0},
            {"size": "$2,000", "price": 17.0},
            {"size": "$5,000", "price": 30.0},
            {"size": "$10,000", "price": 155.0},
            {"size": "$100,000", "price": 500.0},  # Example from requirements
            {"size": "$200,000", "price": 1080.0}
        ],
        "challenge_rules": "Must hit 10% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily loss, 10% max drawdown."
    },
    "MyForexFunds": {
        "accounts": [
            {"size": "$10,000", "price": 49.0},
            {"size": "$50,000", "price": 299.0},
            {"size": "$200,000", "price": 999.0}
        ],
        "challenge_rules": "Must hit 8% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily drawdown, 12% max drawdown."
    },
    "E8 Funding": {
        "accounts": [
            {"size": "$25,000", "price": 228.0},
            {"size": "$100,000", "price": 398.0},
            {"size": "$400,000", "price": 998.0}
        ],
        "challenge_rules": "Must hit 8% profit target in 30 days (Step 1), 5% in 60 days (Step 2), max 5% daily drawdown, 8% max loss."
    },
    "The Funded Trader": {
        "accounts": [
            {"size": "$50,000", "price": 299.0},
            {"size": "$100,000", "price": 499.0},
            {"size": "$200,000", "price": 899.0}
        ],
        "challenge_rules": "Must hit 10% profit target in 35 days (Step 1), 5% in 60 days (Step 2), max 6% daily loss, 12% max drawdown."
    },
    "System/Partner Will Choose": {
        "accounts": [{"size": "N/A", "price": 0.0}],
        "challenge_rules": "No specific challenge rules; system or partner will select the Prop Firm and account size."
    }
}

class PropFirmApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Prop Firm Co-Funding Platform")
        self.root.geometry("600x800")

 # Variables
 self.selected_firm = tk.StringVar(value="System/Partner Will Choose")
        self.selected_account = tk.StringVar(value="N/A")
        self.profit_split = tk.StringVar(value="50:50")  # Default to 50:50
        self.requester_share = tk.StringVar(value="N/A")
        self.co_funder_share = tk.StringVar(value="N/A")
        self.account_price = 0.0

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
        tk.Label(root, text="Profit Split Ratio (e.g., 50:50 for requester:co-funder):").pack()
        tk.Entry(root, textvariable=self.profit_split).pack(pady=5)

 # Shares Display
tk.Label(root, text="Your Contribution (Requester's Share):").pack()
        tk.Label(root, textvariable=self.requester_share).pack(pady=5)
        tk.Label(root, text="Co-Funder's Contribution:").pack()
        tk.Label(root, textvariable=self.co_funder_share).pack(pady=5)
  # Trace variables to auto-calculate shares
  self.selected_account.trace("w", self.calculate_shares)
        self.profit_split.trace("w", self.calculate_shares)

 # Buttons
   tk.Button(root, text="Submit Request", command=self.submit_request).pack(pady=10)
        tk.Button(root, text="View Pending Requests", command=self.view_pending_requests).pack(pady=10)

  # Recent Results Placeholder
   tk.Label(root, text="Recent Results", font=("Arial", 12, "bold")).pack(pady=10)
        tk.Label(root, text="Placeholder for recent results (e.g., success rates, payouts).", wraplength=500).pack(pady=5)
  def update_account_sizes(self, firm):
        # Clear previous radio buttons
        for widget in self.account_frame.winfo_children():
            widget.destroy()

   # Populate new radio buttons for account sizes
   for account in prop_firms[firm]["accounts"]:
            tk.Radiobutton(
                self.account_frame,
                text=f"{account['size']} - ${account['price']:.2f}",
                variable=self.selected_account,
                value=account["size"],
                anchor="w"
            ).pack(fill="x", padx=10)

   # Update challenge rules
self.challenge_label.config(text=prop_firms[firm]["challenge_rules"])
        self.calculate_shares()

  def calculate_shares(self, *args):
        firm = self.selected_firm.get()
        account_size = self.selected_account.get()
        profit_split = self.profit_split.get() or "50:50"

 if firm == "System/Partner Will Choose" or account_size == "N/A":
            self.requester_share.set("N/A")
            self.co_funder_share.set("N/A")
            self.account_price = 0.0
            return

   # Find the price for the selected account
   accounts = prop_firms[firm]["accounts"]
        selected_acc = next((acc for acc in accounts if acc["size"] == account_size), None)
        if not selected_acc:
            return

self.account_price = see ected_acc["price"]

  # Parse profit split ratio
  try:
            req_part, co_part = map(float, profit_split.split(":"))
            total_parts = req_part + co_part
            if total_parts == 0:
                raise ValueError
            req_share = (req_part / total_parts) * self.account_price
            co_share = (co_part / total_parts) * self.account_price
            self.requester_share.set(f"${req_share:.2f} (Locked in Escrow)")
            self.co_funder_share.set(f"${co_share:.2f} (Awaiting Co-Funder)")
        except ValueError:
            self.requester_share.set("Invalid Ratio")
            self.co_funder_share.set("Invalid Ratio")
 def submit_request(self):
        firm = self.selected_firm.get()
        account_size = self.selected_account.get()
        profit_split = self.profit_split.get() or "50:50"
        req_share = self.requester_share.get()
        co_share = self.co_funder_share.get()

   if firm == "System/Partner Will Choose" or account_size == "N/A":
            messagebox.showerror("Error", "Please select a valid Prop Firm and Account Size.")
            return

  if "Invalid" in req_share or not profit_split or ":" not in profit_split:
            messagebox.showerror("Error", "Please enter a valid profit split ratio (e.g., 50:50).")
            return

   try:
            req_share_val = float(req_share.replace("$", "").split(" ")[0])
            co_share_val = float(co_share.replace("$", "").split(" ")[0])
        except ValueError:
            messagebox.showerror("Error", "Invalid share calculation.")
            return

  # Save request
   request = {
            "id": len(self.load_requests()) + 1,
            "prop_firm": firm,
            "account_size": account_size,
            "account_price": self.account_price,
            "profit_split": profit_split,
            "requester_share": req_share_val,
            "co_funder_share": co_share_val,
            "status": "pending"
        }

 requests = self.load_requests()
        requests.append(request)
        self.save_requests(requests)

  messagebox.showinfo("Success", f"Request submitted! Your contribution: ${req_share_val:.2f} (Locked in Escrow). Waiting for a co-funder...")
        self.profit_split.set("50:50")
        self.selected_firm.set("System/Partner Will Choose")
        self.selected_account.set("N/A")
        self.update_account_sizes("System/Partner Will Choose")
        self.calculate_shares()
 def view_pending_requests(self):
        requests = self.load_requests()
        pending = [req for req in requests if req["status"] == "pending"]

  if not pending:
            messagebox.showinfo("No Requests", "No pending co-funding requests.")
            return

  pending_window = Toplevel(self.root)
        pending_window.title("Pending Co-Funding Requests")
        pending_window.geometry("600x400")

  tk.Label(pending_window, text="Pending Requests", font=("Arial", 12, "bold")).pack(pady=10)

  list_frame = tk.Frame(pending_window)
        list_frame.pack(fill="both", expand=True, pady=5)

   scrollbar = Scrollbar(list_frame)
        scrollbar.pack(side="right", fill="y")

   listbox = Listbox(list_frame, yscrollcommand=scrollbar.set, font=("Arial", 10))
        listbox.pack(side="left", fill="both", expand=True)

scrollbar.config(command=listbox.yview)

  for req in pending:
            display_text = (
                f"ID: {req['id']} | Firm: {req['prop_firm']} | Size: {req['account_size']} | "
                f"Price: ${req['account_price']:.2f} | Profit Split: {req['profit_split']} | "
                f"Requester Share: ${req['requester_share']:.2f} (Escrow) | "
                f"Co-Funder Share: ${req['co_funder_share']:.2f} | Status: {req['status']}"
            )
            listbox.insert("end", display_text)

   def accept_selected():
            selection = listbox.curselection()
            if not selection:
                messagebox.showerror("Error", "Please select a request to accept.")
                return
    index = selection[0]
            req = pending[index]
            req_id = req["id"]

   # Verify total matches account price    all_requests = self.load_requests()
 for r in all_requests:
                if r["id"] == req_id:
                    total = r["requester_share"] + r["co_funder_share"]
                    if abs(total - r["account_price"]) > 0.01:  # Allow small float errors
                        messagebox.showerror("Error", "Total shares do not match account price.")
                        return
                    r["status"] = "funded"
                    break

self.save_requests(all_requests)
            messagebox.showinfo("Success", f"Request ID {req_id} accepted! Total funded: ${req['account_price']:.2f}. Account ready for purchase.")
            pending_window.destroy()
            self.view_pending_requests()

   tk.Button(pending_window, text="Accept as Co-Funder", command=accept_selected).pack(pady=10)
  def load_requests(self):
        if os.path.exists("requests.json"):
            with open("requests.json", "r") as f:
                return json.load(f)
        return []

 def save_requests(self, requests):
        with open("requests.json", "w") as f:
            json.dump(requests, f, indent=4)

def main():
    root = tk.Tk()
    app = PropFirmApp(root)
    root.mainloop()

if __name__ == "__main__":
    main()
