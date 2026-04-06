# 📊 Personal Finance Tracker — Power BI Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)

A personal finance dashboard built in **Power BI** to track daily expenses, savings, SIP investments, FD & RD, EMI loans, and payment notifications — all in one place.

---
<!--
## 📸 Screenshots

| Overview | Daily Expenses |
|----------|---------------|
| ![Overview](screenshots/01_overview.png) | ![Expenses](screenshots/02_expenses.png) |

| SIP Portfolio | FD & RD |
|---------------|---------|
| ![SIP](screenshots/03_sip.png) | ![FD RD](screenshots/04_fd_rd.png) |

| EMI / Loans | Notifications |
|-------------|--------------|
| ![EMI](screenshots/05_emi.png) | ![Alerts](screenshots/06_notifications.png) |
---
-->
## 🗂 Project Structure

```
personal-finance-powerbi/
├── database/
│   ├── schema.sql          # Full PostgreSQL schema + views
│   └── seed_data.sql       # Category & payment method seed data
├── excel_templates/
│   └── PersonalFinance.xlsx  # Template with dummy data (safe to share)
├── powerbi/
│   └── PersonalFinance.pbix  # Main Power BI report
├── screenshots/              # Dashboard page exports
├── docs/
│   └── ProjectGuide.docx    # Full setup guide
└── README.md
```

---

## 🧩 Features

- **Overview Page** — Total income, expenses, net savings, savings rate KPI
- **Daily Expenses** — Category-wise breakdown, daily trend, top spenders
- **SIP Portfolio** — Invested vs current value, fund-wise returns, XIRR
- **FD & RD Tracker** — Maturity timeline, interest accrued, status badges
- **EMI / Loans** — Outstanding balance, principal vs interest split, payoff date
- **Notifications** — Colour-coded due payment alerts (Overdue / Due Soon / Upcoming)

---

## ⚙️ Setup — Phase 1 (Excel)

1. Download `excel_templates/PersonalFinance.xlsx`
2. Fill in your data across the 11 sheets (Expenses, Income, SIP_Plans, etc.)
3. Open `powerbi/PersonalFinance.pbix` in Power BI Desktop
4. Update the data source path to your Excel file
5. Refresh — all visuals will populate

---

## 🐘 Setup — Phase 2 (PostgreSQL)

```bash
# 1. Create database
createdb personal_finance

# 2. Run schema
psql -d personal_finance -f database/schema.sql

# 3. Connect Power BI
# Get Data → PostgreSQL → host: localhost, port: 5432, db: personal_finance
```

---

## 📐 Key DAX Measures

```dax
Net Savings     = [Total Income] - [Total Expense]
Savings %       = DIVIDE([Net Savings], [Total Income], 0) * 100
SIP Gain/Loss   = [SIP Current Value] - SUM(sip_transactions[amount_invested])
Overdue Count   = COUNTROWS(FILTER(due_payments,
                    due_payments[due_date] < TODAY() && !due_payments[is_paid]))
```

---

## 🔮 Future Improvements

- [ ] Live bank data via account aggregator API
- [ ] WhatsApp/email alerts for due payments (Python + cron)
- [ ] Annual tax summary (80C, FD TDS)
- [ ] Budget vs Actual with variance alerts
- [ ] Mobile-optimised report layout

---

## 🔒 Privacy Note

The Excel template in this repo contains **dummy data only**. Never commit files with real financial information. Add your personal `.xlsx` files to `.gitignore`.

---

## 👤 Author

**Sahil Bhaidkar** — [LinkedIn](https://linkedin.com/in/sahil-bhaidkar) | [Portfolio](https://sahil-bhaidkar.github.io/)
