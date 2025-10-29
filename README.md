🗓️ DailyCheckIn – Wallet-Based Attendance DApp

A simple decentralized daily check-in application built with Solidity and deployed on the Ethereum Testnet.  
This project demonstrates how blockchain can securely record user attendance using wallet-based authentication, ensuring transparency, immutability, and decentralization.

<img width="1919" height="1079" alt="Screenshot 2025-10-29 135314" src="https://github.com/user-attachments/assets/d6f5d35d-f429-4af8-8b72-8a5df12d89eb" />

📜 Project Description
DailyCheckIn allows users to mark their daily attendance through their crypto wallet.  
Each wallet address can check in once every 24 hours, and the record is stored permanently on-chain.  

This project is ideal for beginners learning Solidity and exploring wallet authentication, timestamp validation, and on-chain record keeping.  
It can easily be extended to build loyalty systems, streak trackers, or community engagement tools.


⚙️ What It Does
- Users connect their wallet (e.g., MetaMask).  
- Each wallet can check in once per day.  
- The smart contract records the timestamp of each user’s last check-in.  
- Anyone can view their latest check-in time and verify activity on-chain.  
- The contract maintains the total number of check-ins performed by all users.

In simple terms — it’s a Web3 attendance system powered by smart contracts.


🌟 Features
🧠 Beginner-Friendly: Clean, well-commented Solidity code that’s easy to understand.  
🔒 One Check-In Per Day: Prevents multiple submissions within 24 hours.  
⛓️ Fully On-Chain: Every check-in is verifiable through blockchain explorers.  
💼 Wallet-Based Authentication: No sign-up or password needed — your wallet is your identity.  
📊 Global Tracking: Tracks the total number of check-ins recorded.  
⚙️ Upgradeable Design: Perfect base for adding rewards, streaks, or gamification later.


📄 Smart Contract
Language: Solidity ^0.8.20  
Framework: Remix / Hardhat Compatible  
Network: Ethereum Testnet  

Deployed Contract:  
0x55D2e8369Fabd459c93ea267Ba702CcE157B3f55  
View on Etherscan:  
https://etherscan.io/address/0x55D2e8369Fabd459c93ea267Ba702CcE157B3f55


💻 Smart Contract Code
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/*
    Daily Check-In Smart Contract
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


🚀 How to Run Locally

1. Clone the Repository  
   git clone https://github.com/your-username/dailycheckin.git  
   cd dailycheckin  

2. Open Remix IDE  
   Visit https://remix.ethereum.org  
   Create a new file: DailyCheckIn.sol  
   Paste the smart contract code above  

3. Compile & Deploy  
   Select Solidity Compiler version ^0.8.20  
   Choose Injected Web3 (MetaMask) as the environment  
   Click Deploy and confirm the transaction in MetaMask  

4. Interact with the Contract  
   checkIn() – Record your daily attendance  
   hasCheckedInToday(address) – Check if a user has already checked in  
   lastCheckIn(address) – View your most recent check-in timestamp  


🧩 Future Enhancements
- Streak Tracking: Count consecutive check-in days per wallet  
- Reward System: Distribute tokens or NFTs for consistent check-ins  
- Frontend Dashboard: Build a React-based UI to visualize check-in data  
- Calendar Integration: Show check-in history and activity logs  
- Identity Verification: Optional off-chain or DID-based user verification  


🙌 Acknowledgments
Ethereum Testnet for contract deployment  
Remix IDE for smart contract testing and deployment  
Etherscan for blockchain record verification and transparency  


Pro Tip: Start small — deploy locally, test features, then build your frontend. Every transaction is a step toward mastering Web3.


Made with ❤️ by Ashu  
Track your day, the Web3 way.
