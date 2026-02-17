# Rune Riches

Rune Riches is a **social sweepstakes casino platform** built for the US market, but can easily be modified to offer **social sweepstakes** to other markets. Players purchase virtual Gold Coin packages and receive free Sweepstakes Coins as a promotional bonus. They use these coins to play a full catalog of casino-style games - slots, table games, and more. Sweepstakes Coins can be redeemed for real cash prizes, operating under the sweepstakes legal model that makes the platform legal in most US states.

---

## How It Works

The platform runs on a **dual-currency model**:

| Currency | Symbol | How Players Get It | What It's For |
|---|---|---|---|
| **Gold Coins** | GC / GLD | Purchased in the Shop | Play-for-fun currency used in all games |
| **Sweepstakes Coins** | SC / SS1 | Received free with every GC purchase, or via mail-in AMOE | Can be redeemed for real cash prizes after wagering requirements are met |

Players never directly buy Sweepstakes Coins - they receive them as a free promotional bonus alongside Gold Coin purchases. This is what makes Rune Riches a legal sweepstakes platform rather than a traditional gambling site. Players can also acquire free Sweepstakes Coins through the **AMOE** (Alternative Method of Entry) program without making any purchase.

---

## Who Uses the Platform

**Players** - members of the public who register, verify their identity, play games, and redeem winnings through the player-facing casino web app.

**Administrators** - the operations, compliance, and support team who manage the platform through a dedicated internal back-office panel. Roles include admins, sub-admins, customer service agents, cashiers, and moderators - each with different levels of access.

---

## Platform Overview

### What Players Can Do

- **Register & Sign In** - email/password, Google, or Facebook social login
- **Browse & Play Games** - full casino game catalog from multiple providers, launched within the platform
- **Buy Gold Coin Packages** - the Shop offers regular packages, first-purchase specials, and promotional deals
- **Track Balances** - real-time Gold Coin and Sweepstakes Coin balances that update instantly
- **Redeem Winnings** - cash out Sweepstakes Coins for real prizes (subject to identity verification)
- **Complete KYC** - identity verification via Veriff to unlock redemptions
- **VIP & Loyalty Program** - tier-based progression with rewards and perks at each level
- **Leaderboards** - compete with other players in timed competitions for prizes
- **Promotions** - access platform promotions, bonuses, and special offers
- **Referral Program** - invite friends and earn rewards when they join and play
- **Live Chat** - real-time chat with other players and customer support
- **Responsible Gaming** - self-exclusion and cooldown tools available directly in the app

### What Administrators Can Do

- **Player Management** - search, view, and manage player accounts, balances, KYC status, and transaction history
- **Game & Provider Management** - enable/disable games and providers, manage the catalog
- **Shop & Packages** - configure purchase packages, pricing, discounts, and special offers, with AI-powered image generation for package artwork
- **Rewards & Bonuses** - create reward definitions with coin amounts, wagering requirements, and restrictions
- **Promotions & Leaderboards** - run marketing campaigns and competitive events, with AI-generated promotional artwork
- **Loyalty Program** - configure VIP tiers, benefits, and progression rules
- **Redemption Approvals** - review and approve/reject player cash-out requests
- **Automation Rules** - build event-driven workflows that trigger on player actions (registration, purchases, game play) and execute sequences of actions automatically
- **Dynamic Report Builder** - build custom reports selecting from player attributes and financial metrics, with scheduled email delivery
- **1099 Tax Reporting** - SSN-based tax compliance reporting for large prize winners
- **Content Management** - edit legal pages, FAQs, support articles, and SEO settings
- **Audit Logs** - full trail of all sensitive admin operations
- **AI Assistant (Chariot Ally)** - an AI-powered assistant built into the admin panel that can look up player data, pull financial metrics, build reports, and create automation rules through natural conversation

---

## Repositories

### Applications

| Repository | Description |
|---|---|
| **frontend-runeriches** | The player-facing casino web app - React, Vite, Tailwind CSS |
| **admin-backoffice** | The internal administration panel - React, Vite, Bootstrap |

### Backend Services

| Repository | Description |
|---|---|
| **user-service** | Player accounts, authentication, profiles, KYC verification, VIP program, real-time chat, and notifications |
| **game-service** | Game catalog, session management, and Hub88 game provider integration (handles all bet/win/rollback transactions) |
| **wallet-service** | Coin balances, reward definitions, balance adjustments, and transaction ledger |
| **payment-service** | Purchase and redemption processing via ApcoPay (cards) and NowPayments (crypto) |
| **admin-service** | Back-office API powering the admin panel - reporting, automation rules, event logs, and the Chariot Ally AI assistant |

### Infrastructure & Tooling

| Repository | Description |
|---|---|
| **brand-deployment** | AWS infrastructure as code (Terraform) - EKS Kubernetes cluster, networking, and CI/CD pipelines |
| **status-service** | Internal health monitoring dashboard - polls all services and displays a unified status page |
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
1. Player clicks a game - game-service generates an encrypted launch token
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
| **Hub88** | Game aggregation - provides the full catalog of casino games and processes all game transactions |
| **Veriff** | Identity verification (KYC) - players upload ID documents for automated verification |
| **ApcoPay** | Card payment processing for coin package purchases |
| **NowPayments** | Cryptocurrency payment processing |
| **SendGrid** | Transactional emails - registration, password reset, reports, notifications |
| **Twilio** | SMS and WhatsApp messaging |
| **Dilisense** | AML (anti-money laundering) screening |
| **Zendesk** | Customer support chat widget embedded in the player app |
| **Google / Facebook** | Social login for player registration |
| **Anthropic (Claude)** | Powers the Chariot Ally AI assistant in the admin back-office |
| **Ideogram** | AI image generation for shop package artwork and promotional banner art |
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

## Security Testing (OWASP Top 10)

**125 penetration tests** across all 5 microservices, covering the full OWASP Top 10 (2021) categories. Testing was performed over 5 iterative test-fix-retest cycles.

### Vulnerability Trend

| Cycle | Critical | High | Medium | Low | Total |
|---|---|---|---|---|---|
| Test 1 (Baseline) | 1 | 7 | 5 | 2 | 15 |
| Test 2 (Post-Fix) | 0 | 2 | 6 | 2 | 10 |
| Test 3 (Post-Fix) | 0 | 0 | 5 | 1 | 6 |
| Test 4 (Internal Services) | 0 | 0 | 5 | 1 | 6 |
| **Test 5 (Final)** | **0** | **0** | **8** | **1** | **9** |

### Final OWASP Category Status

| Category | Status |
|---|---|
| A01 - Broken Access Control | Mitigated |
| A02 - Cryptographic Failures | Mitigated |
| A03 - Injection | Mitigated |
| A04 - Insecure Design | Mitigated |
| A05 - Security Misconfiguration | Partially Mitigated |
| A06 - Vulnerable Components | Mitigated |
| A07 - Authentication Failures | Mitigated |
| A08 - Integrity Failures | Mitigated |
| A09 - Logging & Monitoring | Partially Mitigated |
| A10 - SSRF | Mitigated |

**Overall risk level: LOW** - 0 critical, 0 high. Remaining medium findings are infrastructure-level items (security headers, WAF configuration).

---

## Performance & Load Testing

Load tested with k6 against all 5 services running on a single AWS EC2 t3.medium instance (2 vCPU, 3.7 GB RAM).

### Normal Load - 150 Concurrent Users, 10 Minutes

| Metric | Result |
|---|---|
| Total Requests | 24,923 |
| Throughput | 39.6 req/s |
| Error Rate | 0% |
| P95 Latency | 440ms |
| Login Success | 100% |
| Game Launch Success | 100% |
| Check Success Rate | 100% |

### Stress Test - 750 Concurrent Users, 12 Minutes

| Metric | Result |
|---|---|
| Total Requests | 99,446 |
| Throughput | 130.7 req/s |
| Error Rate | 4.56% |
| P95 Latency | 3,740ms |
| Login Success | 100% |
| Wallet Update Success | 100% |
| Check Success Rate | 99.32% |

### Data Integrity Under Load

| Test | Concurrent Operations | Result |
|---|---|---|
| Wallet balance atomicity | 2,500 concurrent increments | Zero lost updates |
| Payment idempotency | 500 submissions (10 unique) | 490 duplicates correctly rejected |
| Optimistic locking | 250 concurrent updates | 1 winner, 249 correctly rejected |
| Cross-service data sync | 150 status toggles | 100% consistency |
| Coin log multi-write | 1,000 operations (x4 writes each) | Zero partial writes |

### Infrastructure Scaling Estimates

Based on load test data where a single t3.medium (2 vCPU, 4 GB) handled 750 concurrent users at 130.7 req/s. All estimates assume sub-500ms P95 latency and less than 1% error rate as the target.

**EKS (Backend Services)**

| Component | 3,000 Concurrent | 7,500 Concurrent | 15,000 Concurrent |
|---|---|---|---|
| EKS Worker Nodes | 4-5x t3.xlarge | 8-10x m5.xlarge | 15-20x m5.xlarge |
| Pods per Service | 2-3 | 4-6 | 8-12 |
| Total Pods (5 services) | 10-15 | 20-30 | 40-60 |
| MongoDB Atlas | M40 (4 vCPU, 16 GB) | M50 (8 vCPU, 32 GB) | M60 (16 vCPU, 64 GB) |
| MSK (Kafka) Brokers | 2x kafka.m5.large | 3x kafka.m5.large | 3-5x kafka.m5.xlarge |
| ElastiCache (Redis) | 1x cache.r6g.large | 2x cache.r6g.large (replica) | cache.r6g.xlarge (cluster) |
| ALB | 1 (auto-scales) | 1 (auto-scales) | 1-2 (auto-scales) |
| NAT Gateways | 2 (multi-AZ) | 2 (multi-AZ) | 3 (multi-AZ) |

**CloudFront (Static Assets - Player App & Admin Panel)**

| Component | 3,000 Concurrent | 7,500 Concurrent | 15,000 Concurrent |
|---|---|---|---|
| Distribution | 1 per app (2 total) | 1 per app (2 total) | 1 per app (2 total) |
| Price Class | 100 (US & Europe) | 200 (US, Europe, Asia) | All Edge Locations |
| Origin | S3 bucket | S3 bucket | S3 bucket |
| Cache Policy | 24h TTL, gzip/brotli | 24h TTL, gzip/brotli | 24h TTL, gzip/brotli |
| WAF | AWS WAF Basic | AWS WAF with rate rules | AWS WAF with bot control |
| Estimated Transfer | ~50 GB/day | ~125 GB/day | ~250 GB/day |

**Estimated Monthly Cost (us-east-1, On-Demand)**

| Component | 3,000 Concurrent | 7,500 Concurrent | 15,000 Concurrent |
|---|---|---|---|
| EKS Control Plane | $73 | $73 | $73 |
| EC2 Worker Nodes | $605 (5x t3.xlarge) | $1,260 (9x m5.xlarge) | $2,520 (18x m5.xlarge) |
| MongoDB Atlas | $540 (M40) | $1,050 (M50) | $2,100 (M60) |
| MSK (Kafka) | $326 (2 brokers) | $499 (3 brokers) | $1,308 (4 brokers) |
| ElastiCache (Redis) | $121 (1 node) | $242 (2 nodes) | $726 (3-node cluster) |
| ALB | $40 | $75 | $120 |
| NAT Gateways | $116 (2 AZs) | $186 (2 AZs) | $339 (3 AZs) |
| CloudFront | $128 (~1.5 TB/mo) | $319 (~3.75 TB/mo) | $638 (~7.5 TB/mo) |
| WAF | $10 | $20 | $60 |
| S3 + ECR + Route 53 | $15 | $15 | $15 |
| CloudWatch / Logging | $50 | $100 | $200 |
| **Total** | **~$2,024/mo** | **~$3,839/mo** | **~$8,099/mo** |

All prices are on-demand list pricing for us-east-1 (N. Virginia) with no reserved instance or savings plan discounts applied.

**Notes:**
- CloudFront handles all static asset delivery (JS bundles, CSS, images) - cost scales linearly with traffic
- Redis is required at 3,000+ for Socket.IO adapter (sticky sessions across pods) and rate limiter state
- The primary bottleneck at scale is the external Hub88 game provider API, not internal services
- MongoDB connection pooling should be tuned to ~10 connections per pod at higher tiers
- All estimates assume a single AWS region (us-east-1) deployment
- Reserved instances or savings plans typically reduce EC2 and ElastiCache costs by 30-40%

---

## Platform Operations

### Player Behaviour Tracking - PostHog

PostHog is an open-source product analytics platform used to understand how players interact with the casino. It captures every click, page view, and action players take - giving the team a clear picture of what's working and what isn't.

- **Session Replays** - watch real player sessions to see exactly how they navigate the site, where they get stuck, and what makes them leave
- **Funnels** - track conversion at every step (registration to first purchase, game browse to game play, etc.) and identify where players drop off
- **Feature Flags** - roll out new features to a small percentage of players first, measure the impact, then expand or roll back without deploying new code
- **Retention Analysis** - understand which players come back, how often, and what keeps them engaged
- **Cohort Segmentation** - group players by behaviour (e.g. "players who purchased in their first week" vs "players who only use free coins") and compare outcomes
- **Self-Hosted Option** - PostHog can be self-hosted, meaning player data stays within our own infrastructure rather than being sent to a third party - important for a platform handling financial transactions

### Error Tracking - Sentry

Sentry monitors both the player casino app and the admin panel in real time, catching errors the moment they happen - before players report them.

- **Automatic Error Capture** - every JavaScript error, failed API call, or unhandled exception is captured with full context (browser, device, user actions leading up to the error)
- **Release Tracking** - errors are tied to specific code releases, making it easy to see if a new deployment introduced problems and which commit caused it
- **Performance Monitoring** - tracks page load times, slow API calls, and rendering bottlenecks across all user devices
- **Alerting** - the team gets notified immediately when error rates spike, allowing issues to be fixed before they affect a large number of players
- **Breadcrumbs** - every error comes with a trail of user actions (clicked button, navigated to page, submitted form) that led to the failure, making debugging faster

### Website Delivery - CloudFront

CloudFront is Amazon's content delivery network (CDN) that serves the player casino app and admin panel to users worldwide. Instead of every request going back to a single server, CloudFront caches the website at edge locations close to where players are.

- **Fast Load Times** - static assets (JavaScript, CSS, images, fonts) are served from the nearest AWS edge location rather than crossing the internet to a central server. A player in New York gets the site from a New York edge, not from a data centre in Virginia
- **Automatic Scaling** - CloudFront handles traffic spikes without any manual intervention. Whether 100 or 100,000 players load the site simultaneously, the CDN absorbs the load
- **DDoS Protection** - built-in protection against distributed denial-of-service attacks via AWS Shield, keeping the platform online even under malicious traffic
- **HTTPS Everywhere** - all traffic is encrypted with TLS certificates managed automatically by AWS
- **Cost Efficiency** - because cached content is served from the edge, the backend servers handle far fewer requests, reducing compute costs significantly
- **Compression** - assets are automatically compressed (gzip/brotli) before delivery, reducing bandwidth usage and speeding up page loads

### Backend Services - Amazon EKS

Amazon EKS (Elastic Kubernetes Service) runs all five backend microservices as containerised applications. Think of it as the engine room - it keeps every service running, scales them up when demand increases, and restarts them if anything goes wrong.

- **Automatic Scaling** - when more players come online (e.g. during a promotion), EKS automatically spins up additional copies of each service to handle the load, and scales back down when traffic drops to save costs
- **Self-Healing** - if a service crashes or becomes unresponsive, EKS automatically restarts it within seconds. Players may never notice the interruption
- **Zero-Downtime Deployments** - new code is rolled out gradually (rolling updates), so the platform stays fully operational during deployments. If a bad release is detected, it rolls back automatically
- **Service Isolation** - each microservice (user, game, wallet, payment, admin) runs independently. A problem in one service doesn't bring down the others
- **Resource Efficiency** - EKS packs services efficiently across worker nodes, making the most of available compute. Services that need more CPU or memory can be allocated more without affecting others
- **Infrastructure as Code** - the entire EKS cluster, networking, and scaling rules are defined in Terraform, meaning the infrastructure is version-controlled, repeatable, and auditable

---

## Tech Stack

| Layer | Technologies |
|---|---|
| **Player App** | React 19, Vite, Tailwind CSS, Socket.IO |
| **Admin Panel** | React 19, Vite, Bootstrap 5, ReactFlow (visual automation builder) |
| **Backend Services** | Node.js 18+, Express 5, MongoDB (Mongoose), Passport JWT |
| **Real-time** | Socket.IO (balance updates, chat, notifications), Kafka (event streaming) |
| **Analytics** | PostHog (product analytics, session replays, feature flags) |
| **Monitoring** | Sentry (error tracking, performance monitoring, release health) |
| **Infrastructure** | AWS EKS, CloudFront, ECR, S3, MSK, ALB, Terraform |
| **AI** | Anthropic Claude API (admin assistant), Ideogram API (image generation) |
