# Freelancer Business OS — Rate Simulator

> A premium hourly rate calculator widget for freelancers.  
> Built to be embedded in Notion templates via GitHub Pages.

## ✨ Features

- **Hourly Rate Calculation** — Revenue-based formula considering taxes, expenses, and billable hours
- **Tax Vault** — Shows monthly/annual tax reserves to set aside
- **Multi-Currency** — USD, GBP, EUR, CAD, AUD, JPY
- **Multi-Language** — English, 日本語, Español, Français, Deutsch
- **Premium Dark UI** — Glassmorphism, animations, mobile-responsive
- **Single File** — No build tools, no dependencies, just one HTML file

## 🧮 Calculation Logic

```
Gross Revenue = (Desired Net Income / (1 - Tax Rate)) + Business Expenses
Total Billable Hours = (52 - Weeks Off) × Billable Hours per Week
Minimum Hourly Rate = Gross Revenue / Total Billable Hours
Recommended Rate = Minimum Rate × 1.20
Tax Vault (Annual) = Gross Revenue × Tax Rate
Tax Vault (Monthly) = Tax Vault Annual / 12
```

**Default assumptions (hardcoded in MVP):**
- Tax Rate: 25%
- Weeks Off: 4 per year
- Working Weeks: 48 per year

## 🚀 Usage

### Local Preview
Open `index.html` directly in your browser.

### Deploy to GitHub Pages
1. Create a GitHub repository
2. Push `index.html` to the `main` branch
3. Enable GitHub Pages in Settings → Pages → Deploy from branch
4. Use the published URL to embed in Notion via `/embed`

### Embed in Notion
1. In your Notion page, type `/embed`
2. Paste your GitHub Pages URL
3. Resize the embed block as needed

## 📁 Project Structure

```
freelancer-rate-simulator/
├── index.html              # Rate Simulator widget (HTML + CSS + JS)
├── notion-db-design.md     # Notion database schema documentation
└── README.md               # This file
```

## 🗺 Roadmap

- [x] MVP — Core rate calculation
- [x] Tax Vault — Monthly/annual tax reserve display
- [x] Multi-currency support (6 currencies)
- [x] Multi-language support (5 languages)
- [ ] Custom tax rate & weeks off inputs
- [ ] Deploy to GitHub Pages
- [ ] Notion template with 7 linked databases
- [ ] Dashboard page with embedded widgets
- [ ] Pomodoro timer widget
- [ ] Revenue progress ring widget
- [ ] List on Gumroad / Etsy

## 📄 License

MIT
