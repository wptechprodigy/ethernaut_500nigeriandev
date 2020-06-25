# Vault

This challenge is to _Unlock a vault_ with a password that's supposedly hidden (by making it private)!

It's important to always remember that, though by marking a variable _private only_ prevents other contracts from accessing it. However, state variables marked as private and local variables are still publicly accessible on the blockchain.

The blockchain is **append only**. So, once it's deployed it's accessible even though it might not be open to alterations.

To ensure that data is private, it needs to be encrypted before being put onto the blockchain.

## How to resolve this level

This level is resolved by accessing the storage location of the password which is at index 1.

The first step was to declare a variable to hold the content at the storage location we want to access - _password_.

Then use the ```web3``` library to access the storage.

The password is used as a parameter to the ```unlock()``` method in the ```Vault``` contract to unlock the vault.

```solidity
var password;

web3.eth.getStorageAt(instance, 1, (error, result) => (password = result));

await contract.unlock(password);

```

This resolves the vault challenge.
