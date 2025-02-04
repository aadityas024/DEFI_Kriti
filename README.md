# 🌍 P2P Energy Trading & Carbon Credit Marketplace

## 🔥 Overview  
This project is a **decentralized P2P Energy Trading Platform** and **Carbon Credit Marketplace** powered by **zkSync Sepolia Testnet**. The platform enables direct energy trading between **prosumers** and **consumers**, along with a **trustless carbon credit trading system** using **Solidity smart contracts**.  

Key Features:  
✅ **P2P Energy Trading** with dynamic order-matching and geohash-based pricing.  
✅ **Carbon Credit Marketplace** for buying, selling, and trading carbon credits as ERC-20 tokens (**CCTokens**).  
✅ **IoT-Based Battery Monitoring** to validate storage capacity before approving buy orders.  
✅ **zk-SNARK Validation** ensures privacy and security in transaction verification.  
✅ **Layer 2 Scaling** on **zkSync** for fast, low-cost, and Ethereum-secured transactions.  

---  

## 🚀 Features  

### 🔋 P2P Energy Trading Platform  
1. **User Profile & Authentication**  
   - Unique user profile with username, geolocation (converted to **geohash**), and IoT ID.  
   - **JWT-based authentication** for secure access.  

2. **Sell Order Placement (6-8 AM Window)**  
   - Sellers place orders in multiples of **10 kWh** at a specified **ETH/unit** price.  
   - **Geohash-based transaction fees** ensure fair energy pricing.  
   - No new sell orders allowed after **8 AM**.  

3. **Buy Order Execution (8-10 AM Window)**  
   - Buyers manually pick sell orders based on:  
     - Price per unit  
     - 5% commission  
     - Transfer fee (geohash-based distance cost)  
   - Partial order fulfillment supported.  

4. **Automated Order Matching (Post-10 AM)**  
   - System automatically **matches buy orders** based on:  
     - Quantity requested (**multiples of 10 kWh**)  
     - Maximum ETH/unit the buyer is willing to pay  

5. **Order Management & Cancellation**  
   - **Sell Orders**: Cancelable if unpicked.  
   - **Buy Orders**: Cancelable only if **5 places away** in the queue.  

6. **User Dashboard**  
   - Track active & completed trades, pending buy orders, and trade history.  

---

### 🌱 Carbon Credit Marketplace  
1. **Selling Carbon Credits (ERC-20 CCTokens)**  
   - Sellers list **CCTokens** with a fixed price per token in **ETH**.  
   - Tokens are **escrowed** until the sale is finalized.  

2. **Buying Carbon Credits**  
   - Buyers purchase credits in exchange for ETH.  
   - Smart contract handles **automated settlement**.  

3. **Market Features**  
   - View active listings, retrieve order details, and cancel unfulfilled orders.  

4. **Commissions & Fees**  
   - **1% commission** from the bidder (refundable if the bid is unsuccessful).  
   - **2% commission** from the seller upon finalization.  

---

## 🔗 IoT-Based Battery Capacity Monitoring  
This feature ensures that **buyers have enough battery storage** before placing a buy order.  

### 📡 How It Works  
1. **ESP32 IoT Device Monitors Battery**  
   - Reads battery **voltage** and **remaining capacity** via an analog sensor.  
   - Runs a local **HTTP server** to serve battery status.  

2. **Backend Requests Battery Status**  
   - When a buy order is placed, the backend fetches battery data via:  
     ```
     http://<BUYER_ESP32_IP>/get-battery
     ```

3. **Order Validation**  
   - **ZK-SNARKs** validate whether the buyer has enough storage before confirming the order.  

---

## 🔐 Zero-Knowledge Proofs (zk-SNARKs) for Order Validation  
To prevent over-purchasing, we use **zk-SNARK proofs** to verify:  

- `a` → Buyer’s requested energy (in kWh).  
- `b` → Total pending buy orders in the system.  
- `c` → Remaining battery storage capacity.  

If **`a + b > c`**, the transaction **fails**. Otherwise, it **proceeds**.  

### 🛠 Running zk-SNARK Verification  
```sh
nano input.json  
node circuit_js/generate_witness.js circuit_js/circuit.wasm input.json witness.wtns  
snarkjs wtns export json witness.wtns witness.json  
jq '.[1]' witness.json  
snarkjs groth16 prove circuit_final.zkey witness.wtns proof.json public.json  
snarkjs groth16 verify verification_key.json public.json proof.json  
