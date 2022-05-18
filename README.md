# Hop Protocol Sybil Report Repository

Contains reports for every address considered sybil attacking hop protocol airdrop distribution



## Chains

The analisys conducted on Ethereum, Arbitrum, Optimism and Polygon.  
Each folder will contain all of its respective groups.  
In everyy group folder there's an Address.json file which contains all the addresses considered attacking.  

  
Ethereum Mainnet:   
https://github.com/eldief/HopProcol-Sybil-Report/tree/main/ETH


Arbitrum Mainnet:   
https://github.com/eldief/HopProcol-Sybil-Report/tree/main/ARB


Optimism Mainnet:   
 https://github.com/eldief/HopProcol-Sybil-Report/tree/main/OPT


Polygon Mainnet:    
https://github.com/eldief/HopProcol-Sybil-Report/tree/main/POLY

  

## Metodology

For each address from https://github.com/hop-protocol/hop-airdrop/blob/master/src/data/eligibleAddresses.txt are checked all ERC20 transactions up to a depth of 20 to verify if there's a match with another eligible address.


Transactions are considered valid only if placed before snapshot (1/04/2022):  


Ethereum Mainnet: 
```
fromBlock: 12650032
toBlock: 14497035
```


Arbitrum Mainnet: 
```
fromBlock: 440046
toBlock: 9002316
```


OptimismMainnet: 
```
fromTransactionIndex: 1
toTransactionIndex: 5156630
```


Polygon Mainnet: 
```
fromBlock: 15810014
toBlock: 26595905
```  


Criteria:  
- All addresses with more than 10000 ERC20 transactions are considered smartcontracts and not attackers.
- All addresses with more than 30 transactions are considered valid and not attackers.
- All addresses with less than 10 matches are considerd valid and not attackers.  
- Manual review of each dump to exclude non obvious attackers using the following rule:  
  - Addresses that sent an equal or an almost equal amount of the same token to a chain of valid addresses in a short period of time



## Output

For each address considered an attacker is created a JSON file containing the transactions tree linking the subject to another eligible address.  
The file output is in the following format:  


```
{
  "IsMatch": true,
  "Address": "0x...",
  "Transactions": [
    {
      "Quantity": 10000,
      "Currency": "USDC",
      "ERC20Address": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
      "BlockNumber": 14480759,
      "TransactionHash": "0x...",
      "Address": {
        "IsMatch": false,
        "Address": "0x...",
        "Transactions": [
          {
            "Quantity": 10000,
            "Currency": "USDC",
            "ERC20Address": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
            "BlockNumber": 13905874,
            "TransactionHash": "0x...",
            "Address": {
              "IsMatch": true,
              "Address": "0x...",
              "Transactions": []
            }
          },
          ...
        ]
      }
    },
    ...
  ]
}
```
