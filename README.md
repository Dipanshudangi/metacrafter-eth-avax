MyToken Project:
This project implements an ERC-20 token named "Metacrafters" with the symbol "MTAC". 
The contract includes functionalities for minting, burning, and transferring tokens.
Additionally, the contract successfully uses require(), assert(), and revert() statements to ensure the correctness and security of the token operations.

Contract Functionalities:

Mint Function:
The 'mint' function allows the owner to create new tokens and assign them to a specified address.

function mint(address _address, uint _value) public onlyOwner {
    totalSupply += _value;
    balances[_address] += _value;
    
    // Assert to check if the total supply has been updated correctly
    assert(totalSupply >= _value && balances[_address] >= _value);
    
    emit Mint(_address, _value);
}

Burn Function:
The burn function allows the owner to destroy a specified amount of tokens from a specified address, reducing the total supply.

function burn(address _address, uint _value) public onlyOwner {
    if (balances[_address] < _value) {
        revert InsufficientBalance({balance: balances[_address], withdrawAmount: _value});
    } else {
        totalSupply -= _value;
        balances[_address] -= _value;
        emit Burn(_address, _value);
    }
}

Transfer Function:
The transfer function allows token holders to transfer tokens to another address, provided they have enough balance.

function transfer(address _receiver, uint _value) public {
    require(balances[msg.sender] >= _value, "Account balance must be greater than transferred value!");
    balances[msg.sender] -= _value;
    balances[_receiver] += _value;
    emit Transfer(msg.sender, _receiver, _value);
}

Contract Features:
Require Statement: Used in the transfer function to ensure the sender has enough balance before proceeding with the transfer.
Assert Statement: Used in the onlyOwner modifier to ensure the function caller is the owner, and in the mint function to verify the total supply and balance updates.
Revert Statement: Used in the burn function to revert the transaction if the address does not have enough balance to burn the specified amount.

Deployment and Testing:

1. Clone the repository:
git clone https://github.com/YOUR_USERNAME/MYTOKEN_PROJECT.git
cd MYTOKEN_PROJECT

2. Install dependencies:
npm install

3. Run tests:
npx hardhat test

4. Deploy the contract to Avalanche Fuji Testnet:

Configure hardhat.config.js with the network and deploy the contract.
Run the deployment script:
npx hardhat run scripts/deploy.js --network fuji

5. Verify the contract on Snowtrace:
npx hardhat verify --network fuji DEPLOYED_CONTRACT_ADDRESS

License:
This project is licensed under the MIT License.






