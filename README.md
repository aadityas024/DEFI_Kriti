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

### **1️⃣ Clone the repository**
```bash
git clone https://github.com/your-repo/p2p-energy-trading.git
cd p2p-energy-trading
```

### **2️⃣ Install dependencies**
```bash
npm install
```

### **3️⃣ Configure Hardhat for zkSync Sepolia Testnet**
Edit `hardhat.config.js`:
```javascript
require("@nomicfoundation/hardhat-toolbox");
require("@matterlabs/hardhat-zksync-deploy");
require("@matterlabs/hardhat-zksync-solc");
require("dotenv").config();

module.exports = {
  solidity: "0.8.19",
  zksolc: {
    version: "latest",
    compilerSource: "binary",
    settings: {},
  },
  networks: {
    hardhat: {
      chainId: 31337,
    },
    zkSyncSepolia: {
      url: "https://sepolia.era.zksync.dev",
      ethNetwork: "sepolia",
      zksync: true,
      accounts: [process.env.PRIVATE_KEY],
    },
  },
};
```
Create a `.env` file and add your **private key**:
```
PRIVATE_KEY=your_wallet_private_key
```

### **4️⃣ Compile Smart Contracts**
```bash
npx hardhat compile
```

### **5️⃣ Deploy Contracts on zkSync Sepolia**
```bash
npx hardhat deploy-zksync --network zkSyncSepolia
```

### **6️⃣ Verify Contract on zkSync Explorer**
```bash
npx hardhat verify --network zkSyncSepolia YOUR_CONTRACT_ADDRESS
```

### **7️⃣ Run Backend Server**
```bash
node server.js
```

---

## **Bridging & Testing**
### **Bridge ETH to zkSync Sepolia**
- 🔗 [zkSync Sepolia Faucet](https://sepolia-faucet.zksync.dev)
- 🔗 [zkSync Bridge](https://portal.zksync.io/bridge)

### **Test Transactions on zkSync**
Open **Hardhat Console**:
```bash
npx hardhat console --network zkSyncSepolia
```
Interact with your contract:
```javascript
const contract = await ethers.getContractAt("EnergyTrade", "YOUR_CONTRACT_ADDRESS");
await contract.sellEnergy(10, ethers.utils.parseEther("0.05"));
```

---

## **Deploy Frontend**
Deploy frontend using **Vercel, Netlify, or IPFS**:
```bash
npm run build
npm run deploy
```

---

## **Monitor & Optimize**
- **Index transactions** with [The Graph](https://thegraph.com/)
- **Track contracts** on [zkSync Explorer](https://explorer.sepolia.zksync.io/)

---

## **🎉 Your dApp is Live on zkSync Sepolia Testnet! 🚀**
Your **P2P Energy Trading Platform & Carbon Credit Marketplace** is now **faster, cheaper, and Ethereum-secured**.

Do you need help with:
✅ **Bridging assets**  
✅ **Testing transactions**  
✅ **Optimizing gas fees**  

Let me know, and I'll assist you! 🚀🔥

