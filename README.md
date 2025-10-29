# 🌐 XYZ – Daily Check-In Smart Contract

### 🚀 Project Description
**XYZ** is a blockchain-based project that records **daily user check-ins using wallet authentication**.  
Instead of traditional logins, this contract verifies users through their **wallet address**, allowing them to check in securely and immutably on the blockchain.

This project serves as a perfect starting point for beginners who want to understand:
- How to interact with **wallet-based authentication**
- How to record user actions on-chain
- How to use **timestamps, mappings, and events** in Solidity

---

### 💡 What It Does
- Allows each wallet address to **check in once every 24 hours**.  
- Stores the **timestamp** of each user’s last check-in permanently on the blockchain.  
- Keeps a count of the **total check-ins** across all users.  
- Emits an event every time a check-in happens for easy frontend tracking.  
- Provides public functions to verify if a user has checked in today.

In simple terms, it’s a **Web3 attendance tracker** — decentralized, transparent, and simple to use!

---

### ✨ Features
✅ **Wallet-based Authentication** – No need for usernames or passwords.  
✅ **One Check-in Per Day** – Prevents multiple entries within 24 hours.  
✅ **Fully On-Chain Record** – Every check-in is verifiable on the blockchain.  
✅ **Event Logging** – Each check-in emits an event that frontends can track easily.  
✅ **Beginner-Friendly Solidity Code** – Ideal for learning smart contract basics.  
✅ **Extensible Design** – Add streaks, rewards, or NFT badges later.

---

### 🧱 Smart Contract Code
```solidity
//paste your code
