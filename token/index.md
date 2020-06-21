# Token

This challenge is about transfering tokens to the player.

The player (obviously...that's me 👳‍♂️) has been given _20 tokens_ to start with,
and he's expected to add more tokens _as much as possible_.

Going through the `Token contract`, we have **two** methods:
`transfer(uint _initialSupply)` and `balanceOf(address_owner)`.

The _transfer_ method requires that the difference between the balance
`(initial supply)` and the value to be transfered **should be** _greater than_
or _equal to_ zero.

So, there's need for a way to be able to make this transfer to the player. Hence
the need for the creation of a custom contract to handle this interaction.

```solidity
contract MoreTokens {
  Token public token = Token(0x28bB54E783fCBA648ea14cfB16Ab94f639fABcec);

  function addMoreTokens(address _to, uint _value) public {
    token.transfer(_to, _value);
  }
}

```

## What's the initial supply

We need to know the _initialSupply_ to be able to know the value to be
transfered.

So, I ran `await contract.totalSupply()` to get the initial supply, which is
_21000000_.

## What then

I deployed `MoreTokens`.

It has a method `addMoreTokens(address _to, uint _value)` that requires **two** parameters:

- address to receive the tokens (player)

- value (amount) to be sent

After deploying, I made a transaction with the _player (my) address_ and _the
total token supply (21000000)_.

Then, I ran `await contract.balanceOf(player)` to check my balance and I got
this:

```object
{
  c: Array [ 21000020 ]
​
  e: 7
​
  s: 1
}

```

Implies, the player (I) just added _21000000_ tokens to my balance.

## Vulnerability

### Integer Overflow and Underflows

Like C and C++, Solidity is a lower level coding language that doesn’t have failsafes for handling storage limitations. That is memory has to be managed to avoid _memory leaks_ which are what **Garbage collectors** do.

This is different than what Ruby and Python developers might be used to.

Ethereum’s smart contract storage slot are each 256 bits, or 32 bytes. Solidity supports both signed integers, and unsigned integers uint of up to 256 bits.

This means arithmetic operations are prone to underflow and overflow errors, when numbers flow under or over the allocated bits of storage.

### What to do

It's better to use the ```SafeMath.sol``` library to handle mathematical operations.
