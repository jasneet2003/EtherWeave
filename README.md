# 🎨 EtherWeave

> **Weave a permanent masterpiece, one pixel at a time. On-chain.**

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-purple.svg" alt="License">
  <img src="https://img.shields.io/badge/blockchain-Ethereum-blue.svg" alt="Blockchain">
  <img src="https://img.shields.io/badge/network-Sepolia-orange.svg" alt="Network">
  <img src="https://img.shields.io/badge/tech-Ethers.js-green.svg" alt="Tech">
</p>

<p align="center">
  <a href="https://jasneet2003.github.io/EtherWeave/" target="_blank">
    <img src="https://img.shields.io/badge/Live%20Demo-Launch%20EtherWeave-brightgreen?style=for-the-badge&logo=rocket" alt="Live Demo">
  </a>
</p>

---

## 🧵 What is EtherWeave?

**EtherWeave** is a decentralized, collaborative art experiment built on the **Ethereum blockchain**.  
It's a shared digital canvas where **every user can paint a single pixel**.

Each pixel's color and position are stored **permanently on-chain** via a smart contract — creating a digital tapestry that **can never be altered or deleted**.

---

## 🚀 Getting Started: Your First Pixel

Want to become part of the EtherWeave tapestry?  
It’s simple and takes under 5 minutes. Here’s how:

### 🧩 Step 1: Get a Web3 Wallet

We recommend [MetaMask](https://metamask.io/).

1. **Install MetaMask Extension** in your browser.
2. **Create a Wallet** (Save your 12-word recovery phrase somewhere safe — don't share it!).

### ⛽ Step 2: Get Free Sepolia ETH (Test Network)

EtherWeave runs on **Sepolia**, a free testnet. You’ll need some Sepolia ETH for gas.

1. **Switch to Sepolia** in MetaMask.
2. **Copy your wallet address** (starts with `0x...`).
3. Use a faucet to get test ETH:

> 💧 [Alchemy Sepolia Faucet](https://sepoliafaucet.com) *(requires free Alchemy account)*

Wait 1-2 mins and your test ETH will arrive.

### 🖌️ Step 3: Weave Your Pixel!

1. 🔗 Go to the [Live Demo](https://jasneet2003.github.io/indore-web3-demo/)
2. 🔐 Click **"Connect Wallet"** and approve MetaMask
3. 🎨 Pick a color from the palette
4. 🧱 Click any pixel on the canvas
5. ✅ Approve the transaction in MetaMask

✨ Congrats! You've now contributed to a permanent, on-chain piece of art.

---

## 🛠️ Technical Deep Dive

### 🔧 Architecture Overview

| Component | Description |
|----------|-------------|
| **Frontend** | Static vanilla JS app that interacts with MetaMask and renders the canvas |
| **Smart Contract** | A Solidity contract deployed on Sepolia, stores canvas data |
| **Ethereum Blockchain** | Hosts and secures the smart contract data on-chain |

---

### 📦 Frontend Highlights

- **Vanilla HTML/CSS/JS** with no frontend frameworks
- **Ethers.js** handles wallet connection, contract calls, and event listening
- **Live Updates** using `PixelPainted` event from the contract

```js
window.ethereum.request({ method: 'eth_requestAccounts' });
// Connect to contract, call getCanvas(), listen for PixelPainted events
````

---

### 📜 Smart Contract: `CollaborativeCanvas.sol`

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CollaborativeCanvas {
    uint256 public constant GRID_WIDTH = 50;
    uint256 public constant GRID_HEIGHT = 50;

    string[GRID_WIDTH][GRID_HEIGHT] public canvas;

    event PixelPainted(uint256 x, uint256 y, string color, address painter);

    function paintPixel(uint256 x, uint256 y, string memory color) public {
        require(x < GRID_WIDTH, "X coordinate out of bounds");
        require(y < GRID_HEIGHT, "Y coordinate out of bounds");

        canvas[x][y] = color;
        emit PixelPainted(x, y, color, msg.sender);
    }

    function getCanvas() public view returns (string[GRID_WIDTH][GRID_HEIGHT] memory) {
        return canvas;
    }
}
```

---

## 🧪 Run Locally

```bash
# Clone the repo
git clone https://github.com/your-username/your-repo-name.git

# Navigate into the project
cd your-repo-name

# Start a local server
python -m http.server
# Or (if Python 3)
python3 -m http.server
```

Open [http://localhost:8000](http://localhost:8000) in your browser.

---

## 🔮 Future Roadmap

* 🖼️ **NFT Minting** – Mint the entire canvas as a collectible
* 🗳️ **DAO Governance** – Let pixel holders vote on changes
* 🧩 **Expanded Canvases** – Multiple or larger artboards
* 🧭 **Pixel Ownership History** – See the story of each pixel

---

## ❤️ Contributing

This is an open-source project. Contributions, ideas, and bug reports are welcome!

* Create issues
* Submit PRs
* Share the project!

---

## 📄 License

Licensed under the **MIT License**.

---

> **EtherWeave** – Art that’s permanent, public, and programmable.

```

---

Would you like a hosted version (like GitHub Pages `index.html`) of this README as a styled web landing page too?
```
