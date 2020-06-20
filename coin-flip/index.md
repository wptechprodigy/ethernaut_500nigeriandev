# Coin Flip

This level is really challenging...

Well, I am the king endowed with IQ not it. So, I summoned the great community of ethereum hackers and with their backing there has been some progress.

I found out, by googling this [article](https://medium.com/@nicolezhu/ethernaut-lvl-3-walkthrough-how-to-abuse-psuedo-randomness-in-smart-contracts-4cc06bb82570) on medium that provided a way.

I had to use [Remix](remix.ethereum.org) online editor for this level. The first issue I got was that the math library can't be found.

Googling again, I found an issue [here](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/1824) on the SafeMath's github repo that helped me resolved this blocker. I also had to change the Solidity version I was using to version 0.6.0. Doing this, issue of naming the constructor function same as the contract name in earlier version of Solidity showed up.

I only needed to **read the error message** to resolve the issue. I changed the name simply to ```constructor()``` and that was it.

Then ```block.blockhash()``` has also deprecated and it now just ```blockhash()```.

My battery is almost out...I'll update my records later.
