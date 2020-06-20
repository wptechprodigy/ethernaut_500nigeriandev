# Telephone

This task helps understand the fine difference between ```tx.origin``` and ```msg.owner```.

It's another claim a contract adventure.

With help from this [article](https://medium.com/@nicolezhu/ethernaut-lvl-4-walkthrough-how-to-abuse-tx-origin-msg-sender-ef37d6751c8)...I understood the following about ```tx.origin```:

- It's the _original user wallet that initiated a transaction_
- It's the origin address of potentially _an entire chain_ of transactions and calls
- It can _only_ be user wallet
- It can never be a contract address

While ```msg.sender```:

- Is the _immediate sender_
 of the _specific_ transactions and calls
- **Both user wallets and smart contracts can be the** ```msg.sender```

With these perceptions and understood concepts, it means with the help of the ```changeOwner()``` method in the ```Telephone``` contract, we can easily change the owner of this contract and claim it. Do we really own these contracts we are claiming? Well, let's keep claiming them...😍.

So, I created another contract ```Telephony``` with an instance of the ```Telephone``` contract and created ```changeOwnerAddress(address _owner)``` public method that employs the ```changeOwner()``` method to, well..., claim the contract as mine.

Confirmed the owner of the contract using ```await contract.owner()``` and BOOM 🎇...it's mine.

On to the next challenge **Token**...let's meet again.

## Vulnerabilities

[X] Never use tx.origin as an authorization check on who’s calling your contracts

## Better to do

[✔] Use msg.sender if you need to authorize the immediate sender

Thanks and _Gracias_.
