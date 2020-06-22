# Force

Some contracts will simply not take your money ¯\\_(ツ)_/¯

The goal of this level is to make the balance of an **empty** contract greater
than zero.

The contract isn't just empty but does not have any _methods_ to either
**receive** or **transfer** ether.

So, it has to be _forced_ to receive it, because...well...that's the goal.

## The way out

There are **3 ways** to make a contract receive ether viz:

1. — _via payable functions_: The fallback function is to intentionally allow a
   contract to receive Ether from other contracts and external wallets. But if
   no such payable function exists, the contract still has 2 more indirect ways
   of receiving funds:

2. — _receiving mining reward_: contract addresses can be designated as the
   recipients of mining block rewards.

3. — _from a destroyed contract_: selfdestruct allows designation of a backup
   address to receive the remaining ethers from a contract that needs to be
   destroyed.

So, the approach is to make a contract that's designated to be destroyed:

```solidity
contract ReceiveByForce {
  address payable owner;

  function setOwner(address payable _owner) public{
    owner = _owner;
  }

  function destroy() public{
    selfdestruct(owner);
  }

  constructor() public payable {}

  function giveMeMoney() public payable {}
}

```

```RecerveByForce``` contract has a constructor that's _payable_. When the contract has been deployed with _some value_ (I used 1), it's ```setOwner()``` method is called with the _Force instance_ (the empty contract's instance).

The ```destroy()``` method is then called. It forces the **Force** contract to _receive_ the sent ether and _destroys_ the ```ReceiveByForce``` contract.

I checked the new balance, using ```await getBalance("0x2c0772289d991e06bcc74ebb8fd773c62b1ca8bc")```, on the ```Force``` contract and it's now: "0.000000000000000001".

Level completed!!!

On to the next one...Gracias 🐱‍🏍!
