# Smart Contracts

### Tutorials followed: 
[Quicknode ](https://www.quicknode.com/guides/solidity/how-to-write-an-ethereum-smart-contract-using-solidity)


```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.4.0 <0.7.0;
contract SimpleStorage {
    uint storedData;
    function set(uint x) public {
        storedData = x;
    }
    function get() public view returns (uint) {
        return storedData;
    }
}
```
Here is a very basic smart contract that had two functions 
1. Get 
   1. This funtion just returns the value of `storedData`
2. Set
   1. This takes a unsigned int and stores it in the smart contract state. 
   

## Deploying 

We can use [Remix](https://remix.ethereum.org/) which is an ETH IDE. 


## ERC-721 

Uploading to IPFS 

```bash 
ipfs init

# separate win
ipfs daemon

ipfs add <imagefile>
```

If you copy the image file's hash you can just add it to the IPFS link “https://ipfs.io/ipfs/” 

1. Create a JSON file with the metadata




## Hardhat
ChainId for metamask: 31337