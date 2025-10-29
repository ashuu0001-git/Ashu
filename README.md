 Daily Check-In Smart Contract

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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/*
   XYZ Daily Check-In Smart Contract
   ---------------------------------
   - Users can check in once per day (based on block timestamp)
   - The contract stores when each wallet last checked in
   - Anyone can view their last check-in time
   - Owner can view total check-ins
*/

contract DailyCheckIn {
    address public owner;

    // Mapping to store each user's last check-in timestamp
    mapping(address => uint256) public lastCheckIn;

    // Count total number of check-ins
    uint256 public totalCheckIns;

    // Event that logs every successful check-in
    event CheckedIn(address indexed user, uint256 time);

    constructor() {
        owner = msg.sender; // deployer is the owner
    }

    // Function for users to check in
    function checkIn() public {
        // Get the last check-in time
        uint256 lastTime = lastCheckIn[msg.sender];

        // Ensure the user can only check in once per day (86400 seconds)
        require(
            block.timestamp - lastTime >= 1 days,
            "You can only check in once per day"
        );

        // Update their last check-in time
        lastCheckIn[msg.sender] = block.timestamp;

        // Increase total check-in counter
        totalCheckIns++;

        // Emit event
        emit CheckedIn(msg.sender, block.timestamp);
    }

    // View function: check if user already checked in today
    function hasCheckedInToday(address _user) public view returns (bool) {
        if (block.timestamp - lastCheckIn[_user] < 1 days) {
            return true;
        }
        return false;
    }

    // View function: get time since last check-in
    function timeSinceLastCheckIn(address _user) public view returns (uint256) {
        if (lastCheckIn[_user] == 0) return 0;
        return block.timestamp - lastCheckIn[_user];
    }
}

