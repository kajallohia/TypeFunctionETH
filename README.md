Deployment on Local Hardhat Test Network using Remix Connect Localhost
To deploy the RUK token contract to the local Hardhat test network using Remix Connect Localhost, follow these steps:

install its dependencies:
npm install
Install the @remix-project/remixd dependency to connect Remix IDE:
npm install -g @remix-project/remixd
Run the following command in the terminal to connect Remix IDE to the Hardhat local host:
remixd -s ./ --remix-ide https://remix.ethereum.org
Open a new terminal and start Hardhat's testing network:
npx hardhat node
Open the Remix online IDE in your browser.

In the file explorer in the workspace, select "localhost" to connect to the local Hardhat network.

Rewrite the Token.sol file in the contracts directory with your RUK token contract code.

Compile the contract in the Remix IDE.

In the deploy section of Remix, select the environment as "Dev-Hardhat Provider".

Deploy your contract on the local Hardhat network using the deploy button in Remix.

Confirm the deployment transaction in Remix.

Wait for the deployment transaction to be confirmed on the local Hardhat network.

Once the contract is deployed, you will see the contract address in the Remix console. Make note of this address for future interactions.

Interacting with the Contract using Remix with Hardhat Provider
After deploying the RUK token contract to the local Hardhat test network, you can interact with the contract using Remix with Hardhat provider. Here are the steps to get started:

Open the Remix online IDE in your browser.

In the "File Explorer" section, locate the Token.sol file and open it.

In the "Deployed Contracts" section, click on the contract named Token.

In the "At Address" input field, enter the contract address obtained during deployment.

Click the "At Address" button to load the contract instance.

You can now interact with the RUK token contract through the provided functions.

Use the balanceOf function to check the token balance of a specific address.
Use the transfer function to send RUK tokens from your address to another address.
Use the mint function (accessible only to the contract owner) to mint
new RUK tokens.

Use the burn function to burn a specific amount of your RUK tokens.
Set the required parameters for each function and click the corresponding button to execute the transaction.

Confirm the transaction details and sign the transaction in Remix.

Wait for the transaction to be confirmed on the local Hardhat network.

You can view the transaction status and emitted events in the Remix console.


// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Token {
    string public name;
    string public symbol;
    uint8 public decimals;
    uint256 public totalSupply;

    mapping(address => uint256) private balances;
    mapping(address => mapping(address => uint256)) private allowances;

    address public owner;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Mint(address indexed to, uint256 value);
    event Burn(address indexed from, uint256 value);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can call this function.");
        _;
    }

    constructor() {
        name = "Token";
        symbol = "TKN";
        decimals = 18;
        totalSupply = 0;
        owner = msg.sender;
    }

    function balanceOf(address account) external view returns (uint256) {
        return balances[account];
    }

    function transfer(address recipient, uint256 amount) external returns (bool) {
        require(amount <= balances[msg.sender], "Insufficient balance.");

        balances[msg.sender] -= amount;
        balances[recipient] += amount;

        emit Transfer(msg.sender, recipient, amount);
        return true;
    }


    function mint(address to, uint256 amount) external onlyOwner {
        totalSupply += amount;
        balances[to] += amount;

        emit Mint(to, amount);
        emit Transfer(address(0), to, amount);
    }

    function burn(uint256 amount) external {
        require(amount <= balances[msg.sender], "Insufficient balance.");

        balances[msg.sender] -= amount;
        totalSupply -= amount;

        emit Burn(msg.sender, amount);
        emit Transfer(msg.sender, address(0), amount);
    }
}

Author 
kajal lohia

https://www.linkedin.com/in/kajal-lohia-38b184230/
