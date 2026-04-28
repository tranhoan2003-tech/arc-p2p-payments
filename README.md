# ✈️ TravelPay — Global P2P Payments for Travelers

> **"Pay anyone, anywhere, in any currency — instantly, with zero hidden fees."**
> Built natively on Arc Network (Circle's stablecoin L1 blockchain).

[![Arc Testnet](https://img.shields.io/badge/Arc-Testnet%20Live-1D9E75?style=flat-square)](https://testnet.arcscan.app/address/0xb6FF38eceCA9a2D014a82640f788DA580C869A43)
[![Contract](https://img.shields.io/badge/Contract-Verified-blue?style=flat-square)](https://testnet.arcscan.app/address/0xb6FF38eceCA9a2D014a82640f788DA580C869A43)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

---

## 🌍 The Problem

Every traveler faces the same pain points:

| Problem | Traditional Solution | Cost |
|---|---|---|
| Paying a friend in another country | Wire transfer / PayPal | 3–7% fee + 3–5 days |
| Splitting hotel with 6 friends | Venmo / cash / IOU notes | Only works domestically |
| Paying a local tour operator | Cash only / card surcharge | 2–4% card fee |
| "How much is 850,000 VND in USD?" | Google + mental math | Error-prone |

**TravelPay solves all of this with one USDC-native app on Arc Network.**

---

## 💡 The Solution

TravelPay is a peer-to-peer payment platform purpose-built for global travelers:

- **🌐 Send USDC to anyone, anywhere** — instant cross-border payments, no bank needed
- **👥 Travel Groups** — create a trip, add friends, track shared expenses and split automatically
- **💱 Smart FX Reference** — see real-time USD equivalent for VND, EUR, JPY, THB, SGD, and more
- **🏨 Merchant Checkout** — hotels, restaurants, and tour operators accept USDC directly
- **📊 Transparent settlement** — every expense settled on-chain, no disputes

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                 TravelPay Frontend (Next.js)             │
│   Wallet: MetaMask / WalletConnect (Arc Testnet)        │
└──────────────────────────┬──────────────────────────────┘
                           │ ethers.js
           ┌───────────────▼────────────────┐
           │       Arc Network Testnet        │
           │   Chain ID: 5042002              │
           │   Gas token: USDC (not ETH!)     │
           │   Finality: sub-second           │
           └───────────────┬────────────────┘
                           │
           ┌───────────────▼────────────────┐
           │        TravelPay.sol            │
           │                                 │
           │  sendPayment()   ← direct P2P   │
           │  createGroup()   ← trip setup   │
           │  addExpense()    ← log shared   │
           │  settleExpense() ← on-chain pay │
           │  payMerchant()   ← checkout     │
           │  getUSDCAmount() ← FX oracle    │
           └─────────────────────────────────┘
```

---

## 🚀 Why Arc Network?

| Feature | Traditional Finance | Arc Network |
|---|---|---|
| Settlement time | 1–5 business days | **Sub-second** |
| Gas fee currency | ETH (volatile) | **USDC (stable $)** |
| Cross-border fee | 3–7% | **0%** |
| 24/7 availability | ❌ Bank hours | **✅ Always on** |
| Transparency | ❌ Hidden fees | **✅ On-chain** |

Arc's USDC-native gas means travelers can pay in dollars — **no ETH, no crypto complexity**.

---

## 📱 User Journeys

### Journey 1: Backpacker in Vietnam
> Mai is traveling through Vietnam. She owes her friend Linh 850,000 VND for a shared motorbike rental.

1. Opens TravelPay → sees "850,000 VND ≈ $33.15 USDC" (live FX)
2. Sends $33.15 USDC to Linh's wallet
3. Linh receives it **instantly** — no bank, no waiting, no fee

### Journey 2: Group Trip to Bali
> 6 friends from 4 countries are doing a 2-week trip to Bali

1. One friend creates a **TravelGroup** "Bali 2026"
2. As expenses come in (villa, surfing, dinners), anyone logs them
3. Contract auto-splits costs equally or by custom shares
4. At end of trip: one-click settlement → everyone pays their balance on-chain

### Journey 3: Local Merchant in Thailand
> A tour operator in Chiang Mai wants to accept foreign travelers without card fees

1. Registers as **TravelPay Merchant**
2. Displays QR code at desk
3. Travelers scan and pay in USDC — operator receives USDC instantly, no 3% card surcharge

---

## 🔧 Smart Contract Features

```solidity
// Direct cross-border payment
sendPayment(recipient, amount, "Sharing hostel, Bangkok", "THB")

// Create a travel group
createGroup("Europe 2026", "Paris/Amsterdam/Berlin", members, startDate, endDate)

// Log a shared expense
addExpense(groupId, 120_000000, "Dinner at Eiffel", "EUR", 11000, members, [])

// Pay a registered merchant
payMerchant(hotelWallet, 50_000000, "USD", 50_00)

// Get FX conversion
getUSDCAmount("VND", 850_000_00) // returns USDC equivalent
```

---

## 🌐 Supported Currencies (FX Reference)

| Currency | Country |
|---|---|
| VND | 🇻🇳 Vietnam |
| EUR | 🇪🇺 Eurozone |
| JPY | 🇯🇵 Japan |
| GBP | 🇬🇧 United Kingdom |
| THB | 🇹🇭 Thailand |
| SGD | 🇸🇬 Singapore |
| AUD | 🇦🇺 Australia |
| KRW | 🇰🇷 South Korea |

*More currencies added via FX oracle network*

---

## 📋 Contract Deployment

| Network | Contract Address |
|---|---|
| Arc Testnet | [`0xb6FF38eceCA9a2D014a82640f788DA580C869A43`](https://testnet.arcscan.app/address/0xb6FF38eceCA9a2D014a82640f788DA580C869A43) |
| USDC (Arc Testnet) | `0x036CbD53842c5426634e7929541eC2318f3dCF7e` |

---

## 🛠️ Quick Start

```bash
git clone https://github.com/tranhoan2003-tech/arc-p2p-payments
cd arc-p2p-payments/arc-p2p
npm install
cp .env.example .env
# Fill in PRIVATE_KEY in .env
npx hardhat run scripts/deploy.js --network arc-testnet
```

**Arc Network Config:**
- RPC: `https://rpc.testnet.arc.network`
- Chain ID: `5042002`
- Faucet: `https://faucet.circle.com` (select Arc Testnet)
- Explorer: `https://testnet.arcscan.app`

---

## 🗺️ Roadmap

- [x] Core P2P USDC payments
- [x] Deploy on Arc Testnet
- [ ] Travel Groups with on-chain expense tracking
- [ ] FX Oracle integration (Chainlink / Pyth)
- [ ] Merchant registration and QR checkout
- [ ] Mobile-first PWA
- [ ] Multi-language UI (Vietnamese, Thai, Japanese, Korean)
- [ ] Arc Mainnet launch

---

## 🤝 Built for Arc Architects Program

This project was built as a contribution to the **Arc Network Architects** community — demonstrating a real-world use case for USDC-native payments on Arc Network.

**Pain point solved:** $48 billion lost annually to travel FX fees and cross-border payment friction.

**Arc advantage:** Instant settlement + USDC as gas = the perfect stack for borderless travel payments.

---

*Built with ❤️ by a Vietnamese developer on Arc Network*
