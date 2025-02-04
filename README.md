# P2P Energy Trading Platform & Carbon Credit Marketplace on zkSync Sepolia Testnet

## Overview
The **P2P Energy Trading Platform** is a decentralized marketplace that enables direct energy trading between prosumers and consumers using **blockchain technology**. The platform leverages **Solidity smart contracts** and a **Node.js backend** to facilitate **secure, transparent, and automated energy transactions**. It utilizes **geohash-based pricing** and a **dynamic order-matching mechanism** to optimize energy distribution and pricing.

Additionally, the **Carbon Credit Marketplace** is a decentralized platform for **buying, selling, and trading carbon credits** as ERC-20 tokens (**CCTokens**). This ensures secure, transparent, and trustless transactions through smart contract automation.

This application is developed as part of the **EnergyChain Challenge** to address key issues such as **energy equity, sustainability, and transparent carbon credit trading**.

## Features

### P2P Energy Trading Platform
1. **User Profile & Authentication**
   - Unique user profile with:
     - Username
     - User ID
     - Geolocation (lat, long) → converted to geohash
     - Unique IoT ID
   - **JWT-based authentication** for secure access.

2. **Sell Order Placement (6-8 AM Window)**
   - Sellers place sell orders with:
     - Amount (multiples of **10 kWh**)
     - Price per unit (**ETH/unit**)
     - Geohash-based transaction fees
   - No new sell orders after **8 AM**.

3. **Buy Order Execution (8-10 AM Window)**
   - Buyers select sell orders manually based on:
     - Seller’s price
     - 5% commission
     - Transfer fee (geohash distance-based)
   - Partial order fulfillment allowed.

4. **Automated Buy Order Matching (Post-10 AM)**
   - Buy orders are **queued & processed automatically**.
   - Order matching criteria:
     - Quantity (multiples of **10 kWh**)
     - Maximum ETH/unit willing to pay

5. **Order Management & Cancellation**
   - **Sell Orders**: Cancelable if not picked for trade.
   - **Buy Orders**: Cancelable if **at least 5 places away** from queue front.

6. **User Dashboard & Trade History**
   - Users can view:
     1. Active Sell Orders
     2. Completed Sell Transactions
     3. Completed Buy Transactions
     4. Canceled Sell Orders
     5. Pending Buy Orders

---

### Carbon Credit Marketplace (Solidity Smart Contract)

1. **Selling Carbon Credits**
   - Sellers list **CCTokens** for sale with:
     - Quantity (number of tokens)
     - Price per token (**ETH**)
   - Tokens **escrowed** until sold or canceled.

2. **Buying Carbon Credits**
   - Buyers purchase tokens by sending ETH.
   - Upon purchase:
     - Tokens transferred to buyer.
     - Seller receives ETH.

3. **Market Functions**
   - View active sell orders.
   - Retrieve specific order details.
   - Cancel unfulfilled orders.

4. **Order Matching Mechanism**
   - Orders matched at **fixed seller-set prices**.
   - Buyers choose purchase amount.

5. **Security & Transparency**
   - **Escrow mechanism** prevents fraud.
   - **On-chain transaction history** ensures auditability.
   - Sellers can cancel orders before fulfillment.

6. **Commissions**
   - **1% commission** taken from the bidder (refunded if bid not finalized).
   - **2% commission** taken from seller upon auction finalization.

---

## Installation & Setup

