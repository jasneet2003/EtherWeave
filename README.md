EtherWeave 🎨
Weave a permanent masterpiece, one pixel at a time. On-chain.
<p align="center">
<img src="https://img.shields.io/badge/license-MIT-purple.svg" alt="License">
<img src="https://img.shields.io/badge/blockchain-Ethereum-blue.svg" alt="Blockchain">
<img src="https://img.shields.io/badge/network-Sepolia-orange.svg" alt="Network">
<img src="https://img.shields.io/badge/tech-Ethers.js-green.svg" alt="Tech">
</p>

EtherWeave is a decentralized, collaborative art experiment built on the Ethereum blockchain. It's a shared digital canvas where every user can paint a single pixel. Each pixel's color and position are stored permanently on-chain in a smart contract, creating a digital tapestry that can never be modified or taken down.

<p align="center">
<a href="https://jasneet2003.github.io/indore-web3-demo/" target="_blank">
<img src="https://img.shields.io/badge/Live%20Demo-Launch%20EtherWeave-brightgreen?style=for-the-badge&logo=rocket" alt="Live Demo">
</a>
</p>

🚀 Getting Started: Your First Pixel
To become part of the EtherWeave tapestry, you'll need a Web3 wallet and some free "play" money called Sepolia ETH. It's easy and takes less than 5 minutes!

Step 1: Get a Digital Wallet
A Web3 wallet is your passport to the decentralized web. We recommend MetaMask.

Install MetaMask: Add the official MetaMask extension to your browser.

➡️ Install MetaMask

Create a Wallet: Follow the on-screen instructions to create your new wallet. Crucially, write down your 12-word Secret Recovery Phrase on paper and store it somewhere safe.

Step 2: Get Free Test Money (Sepolia ETH)
EtherWeave runs on Sepolia, a free "test network" for Ethereum. This lets you use the app without spending real money. To paint a pixel, you need to pay a tiny transaction fee (called "gas") with Sepolia ETH.

Switch to Sepolia: In your MetaMask wallet, click the network dropdown at the top-left and select "Sepolia".

Copy Your Address: Click on your account name to copy your wallet address (it starts with 0x...).

Use a Faucet: A "faucet" is a website that gives out free test currency. Go to a reliable faucet, paste your address, and request funds.

➡️ Alchemy Sepolia Faucet (Recommended: requires a free Alchemy account)

Wait a minute or two, and you'll see the Sepolia ETH appear in your wallet!

Step 3: Weave Your Pixel!
You're all set!

Go to the EtherWeave Live Demo.

Click "Connect Wallet" and approve the connection in MetaMask.

Pick a color from the palette.

Click any pixel on the canvas.

Approve the transaction in MetaMask.

Congratulations! You've just woven your color into a permanent, on-chain piece of art.

🛠️ The Technical Deep Dive
For those who want to look under the hood, here's how EtherWeave works.

Architecture Overview
EtherWeave consists of three core components:

Frontend (The dApp): A vanilla HTML/CSS/JavaScript application that users interact with. It's responsible for rendering the canvas and communicating with the user's wallet.

Smart Contract (The Brain): A Solidity contract deployed on the Sepolia testnet. This is the "backend" and single source of truth for the entire application.

Ethereum Blockchain (The Ledger): The decentralized network that hosts and executes our smart contract, ensuring data permanence and security.

Frontend Breakdown
The entire user interface is a static site built with modern, dependency-free code.

Ethers.js: We use this essential library to communicate with the blockchain. It handles wallet connections, contract interactions, and event listening.

Wallet Connection: The app uses window.ethereum to detect a browser-injected wallet like MetaMask. It requests account access and ensures the user is on the correct network (Sepolia) using wallet_switchEthereumChain.

State Rendering: On connection, the dApp calls the getCanvas() view function on the smart contract to fetch the entire 2D array of pixels and renders them.

Real-Time Updates: The app subscribes to the PixelPainted event from the smart contract. When anyone in the world paints a pixel, the contract emits this event, and our frontend instantly updates the specific pixel without needing to refresh the entire canvas.

Smart Contract: CollaborativeCanvas.sol
The heart of EtherWeave is a simple but powerful smart contract.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CollaborativeCanvas {
    // The dimensions of our canvas.
    uint256 public constant GRID_WIDTH = 50;
    uint256 public constant GRID_HEIGHT = 50;

    // The core state variable: a 2D array storing the hex color of each pixel.
    string[GRID_WIDTH][GRID_HEIGHT] public canvas;

    // An event broadcasted to the world whenever a pixel is updated.
    // The frontend listens for this to enable real-time updates.
    event PixelPainted(uint256 x, uint256 y, string color, address painter);

    /**
     * @dev The main function that allows a user to paint a single pixel.
     * It requires coordinates to be within bounds, then updates the state.
     */
    function paintPixel(uint256 x, uint256 y, string memory color) public {
        require(x < GRID_WIDTH, "X coordinate out of bounds");
        require(y < GRID_HEIGHT, "Y coordinate out of bounds");

        // Update the state of the canvas.
        canvas[x][y] = color;

        // Broadcast the change to the world.
        emit PixelPainted(x, y, color, msg.sender);
    }

    /**
     * @dev A view function to get the entire canvas state at once.
     * Used for initial page load.
     */
    function getCanvas() public view returns (string[GRID_WIDTH][GRID_HEIGHT] memory) {
        return canvas;
    }
}

⚙️ How to Run Locally
Want to experiment or contribute?

Clone the repository:

git clone https://github.com/your-username/your-repo-name.git

Navigate to the directory:

cd your-repo-name

Start a local server:
This is the easiest way to run the index.html file.

python -m http.server

(If that fails, try python3 -m http.server)

Open in browser:
Go to http://localhost:8000 in your browser.

🔮 Future Roadmap
EtherWeave is just the beginning. Here are some ideas for the future:

NFT Minting: Allow users to mint the final state of the canvas as a commemorative NFT.

DAO Governance: Create a DAO where pixel owners can vote on future canvas parameters (size, color palette, etc.).

Expanded Canvases: Introduce larger or multiple themed canvases.

Pixel Ownership History: A UI to view the history of a single pixel.

❤️ Contributing
This is an open-source project. Contributions, issues, and feature requests are welcome! Feel free to check the issues page.

Licensed under the MIT License.
