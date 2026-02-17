# Rune Riches

Rune Riches is a **social sweepstakes casino platform** built for the US market. Players purchase virtual Gold Coin packages and receive free Sweepstakes Coins as a promotional bonus. They use these coins to play a full catalog of casino-style games — slots, table games, and more. Sweepstakes Coins can be redeemed for real cash prizes, operating under the sweepstakes legal model that makes the platform legal in most US states.

---

## How It Works

The platform runs on a **dual-currency model**:

| Currency | Symbol | How Players Get It | What It's For |
|---|---|---|---|
| **Gold Coins** | GC / GLD | Purchased in the Shop | Play-for-fun currency used in all games |
| **Sweepstakes Coins** | SC / SS1 | Received free with every GC purchase, or via mail-in AMOE | Can be redeemed for real cash prizes after wagering requirements are met |

Players never directly buy Sweepstakes Coins — they receive them as a free promotional bonus alongside Gold Coin purchases. This is what makes Rune Riches a legal sweepstakes platform rather than a traditional gambling site. Players can also acquire free Sweepstakes Coins through the **AMOE** (Alternative Method of Entry) program without making any purchase.

---

## Who Uses the Platform

**Players** — members of the public who register, verify their identity, play games, and redeem winnings through the player-facing casino web app.

**Administrators** — the operations, compliance, and support team who manage the platform through a dedicated internal back-office panel. Roles include admins, sub-admins, customer service agents, cashiers, and moderators — each with different levels of access.

---

## Platform Overview

### What Players Can Do

- **Register & Sign In** — email/password, Google, or Facebook social login
- **Browse & Play Games** — full casino game catalog from multiple providers, launched within the platform
- **Buy Gold Coin Packages** — the Shop offers regular packages, first-purchase specials, and promotional deals
- **Track Balances** — real-time Gold Coin and Sweepstakes Coin balances that update instantly
- **Redeem Winnings** — cash out Sweepstakes Coins for real prizes (subject to identity verification)
- **Complete KYC** — identity verification via Veriff to unlock redemptions
- **VIP & Loyalty Program** — tier-based progression with rewards and perks at each level
- **Leaderboards** — compete with other players in timed competitions for prizes
- **Promotions** — access platform promotions, bonuses, and special offers
- **Referral Program** — invite friends and earn rewards when they join and play
- **Live Chat** — real-time chat with other players and customer support
- **Responsible Gaming** — self-exclusion and cooldown tools available directly in the app

### What Administrators Can Do

- **Player Management** — search, view, and manage player accounts, balances, KYC status, and transaction history
- **Game & Provider Management** — enable/disable games and providers, manage the catalog
- **Shop & Packages** — configure purchase packages, pricing, discounts, and special offers
- **Rewards & Bonuses** — create reward definitions with coin amounts, wagering requirements, and restrictions
- **Promotions & Leaderboards** — run marketing campaigns and competitive events
- **Loyalty Program** — configure VIP tiers, benefits, and progression rules
- **Redemption Approvals** — review and approve/reject player cash-out requests
- **Automation Rules** — build event-driven workflows that trigger on player actions (registration, purchases, game play) and execute sequences of actions automatically
- **Dynamic Report Builder** — build custom reports selecting from player attributes and financial metrics, with scheduled email delivery
- **1099 Tax Reporting** — SSN-based tax compliance reporting for large prize winners
- **Content Management** — edit legal pages, FAQs, support articles, and SEO settings
- **Audit Logs** — full trail of all sensitive admin operations
- **AI Assistant (Chariot Ally)** — an AI-powered assistant built into the admin panel that can look up player data, pull financial metrics, build reports, and create automation rules through natural conversation

---

## Repositories

### Applications

| Repository | Description |
|---|---|
| **frontend-runeriches** | The player-facing casino web app — React, Vite, Tailwind CSS |
| **admin-backoffice** | The internal administration panel — React, Vite, Bootstrap |

### Backend Services

| Repository | Description |
|---|---|
| **user-service** | Player accounts, authentication, profiles, KYC verification, VIP program, real-time chat, and notifications |
| **game-service** | Game catalog, session management, and Hub88 game provider integration (handles all bet/win/rollback transactions) |
| **wallet-service** | Coin balances, reward definitions, balance adjustments, and transaction ledger |
| **payment-service** | Purchase and redemption processing via ApcoPay (cards) and NowPayments (crypto) |
| **admin-service** | Back-office API powering the admin panel — reporting, automation rules, event logs, and the Chariot Ally AI assistant |

### Infrastructure & Tooling

| Repository | Description |
|---|---|
| **brand-deployment** | AWS infrastructure as code (Terraform) — EKS Kubernetes cluster, networking, and CI/CD pipelines |
| **status-service** | Internal health monitoring dashboard — polls all services and displays a unified status page |
| **api-doc-service** | API documentation service |
| **load-testing** | Performance testing scripts for API endpoints |
| **security-testing** | Security audit tooling and vulnerability testing |

---

## How Everything Connects

```
                          ┌─────────────────────────────────────────┐
                          │              PLAYER BROWSER              │
                          │         frontend-runeriches app          │
                          └──────────────────┬──────────────────────┘
                                             │
                                             ▼
                          ┌─────────────────────────────────────────┐
                          │            USER SERVICE                  │
                          │  Auth, Profiles, KYC, VIP, Chat, Notif  │
                          └───┬──────────┬──────────┬───────────────┘
                              │          │          │
                    ┌─────────▼──┐  ┌────▼─────┐  ┌▼──────────────┐
                    │   WALLET   │  │   GAME   │  │   PAYMENT     │
                    │  SERVICE   │  │  SERVICE  │  │   SERVICE     │
                    │            │  │           │  │               │
                    │ Balances,  │  │ Catalog,  │  │ Purchases,    │
                    │ Rewards,   │◄─┤ Sessions, │  │ Redemptions,  │
                    │ Ledger     │  │ Hub88     │  │ ApcoPay/Crypto│
                    └────────────┘  └─────┬─────┘  └───────────────┘
                                          │
                                          │ Webhooks
                                          ▼
                                   ┌──────────────┐
                                   │    Hub88      │
                                   │ Game Provider │
                                   │ (100+ games)  │
                                   └──────────────┘

                          ┌─────────────────────────────────────────┐
                          │              ADMIN BROWSER               │
                          │         admin-backoffice app             │
                          └──────────────────┬──────────────────────┘
                                             │
                                             ▼
                          ┌─────────────────────────────────────────┐
                          │            ADMIN SERVICE                 │
                          │  Back-office API, Reports, Automation,   │
                          │  AI Assistant, Event Logs                │
                          └───┬──────────┬──────────┬───────────────┘
                              │          │          │
                              ▼          ▼          ▼
                         user-service  wallet    payment
                                      service    service
```

### Key Flows

**When a player buys a Gold Coin package:**
1. Player selects a package in the Shop
2. The request flows through user-service to payment-service
3. Payment-service creates the transaction and redirects to the payment provider (ApcoPay or NowPayments)
4. The payment provider processes the card/crypto payment and sends a confirmation webhook
5. Payment-service confirms success and tells wallet-service to credit the coins
6. The player's Gold Coin and Sweepstakes Coin balances update in real time via WebSocket

**When a player plays a game:**
1. Player clicks a game — game-service generates an encrypted launch token
2. Hub88 opens the game in the player's browser
3. For every bet and win, Hub88 sends webhook calls to game-service
4. Game-service deducts or credits coins via wallet-service
5. All transactions are recorded in the ledger and streamed as events

**When a player redeems Sweepstakes Coins:**
1. Player requests a cash-out through the app
2. The request is created in payment-service and enters a pending state
3. An administrator reviews the request in the Redemption Approvals section of the back-office
4. Once approved, the payout is processed and the coins are deducted from the player's wallet

---

## External Integrations

| Provider | What It Does |
|---|---|
| **Hub88** | Game aggregation — provides the full catalog of casino games and processes all game transactions |
| **Veriff** | Identity verification (KYC) — players upload ID documents for automated verification |
| **ApcoPay** | Card payment processing for coin package purchases |
| **NowPayments** | Cryptocurrency payment processing |
| **SendGrid** | Transactional emails — registration, password reset, reports, notifications |
| **Twilio** | SMS and WhatsApp messaging |
| **Dilisense** | AML (anti-money laundering) screening |
| **Zendesk** | Customer support chat widget embedded in the player app |
| **Google / Facebook** | Social login for player registration |
| **Anthropic (Claude)** | Powers the Chariot Ally AI assistant in the admin back-office |
| **AWS S3** | Image and asset storage (game thumbnails, avatars, provider logos) |
| **AWS MSK (Kafka)** | Event streaming across services for real-time data flow |

---

## Deployment & Environments

The platform runs on **AWS** using **Amazon EKS (Kubernetes)**. All backend services are containerised and deployed with horizontal auto-scaling. Infrastructure is managed with **Terraform** and deployed through CI/CD pipelines.

| Environment | Player App | Admin Panel | Purpose |
|---|---|---|---|
| **Development** | dev.runeriches.com | dev-admin.runeriches.com | Active development and testing |
| **Staging** | staging.runeriches.com | staging-admin.runeriches.com | Pre-production validation |
| **Production** | TBD | admin.runeriches.com | Live platform |

---

## Tech Stack

| Layer | Technologies |
|---|---|
| **Player App** | React 19, Vite, Tailwind CSS, Socket.IO |
| **Admin Panel** | React 18, Vite, Bootstrap 5, ReactFlow (visual automation builder) |
| **Backend Services** | Node.js 18+, Express 5, MongoDB (Mongoose), Passport JWT |
| **Real-time** | Socket.IO (balance updates, chat, notifications), Kafka (event streaming) |
| **Infrastructure** | AWS EKS, ECR, S3, MSK, ALB, Terraform |
| **AI** | Anthropic Claude API (admin assistant) |
