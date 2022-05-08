# Hop Protocol Sybil Report Repository

Contains reports for every address considered sybil attacking hop protocol airdrop distribution

## Metodology

For each address from https://github.com/hop-protocol/hop-airdrop/blob/master/src/data/eligibleAddresses.txt are checked all ERC20 transactions up to a depth of 5 to verify if there's a match with another eligible address.  


All addresses with more than 10000 ERC20 transactions are considered smartcontracts and not attackers.  
All addresses with more than 30 transactions are considered valid and not attackers.  
All addresses with less than 2 matches are considerd valid and not attackers.  
Finally all dumps are manually reviewed looking for patterns and excluding not obvious attacks

The repository will be updated over time.

## Chains

The analisys is conducted on Ethereum, Arbitrum, Optimism and Polygon.  
Each folder will contain all of its respective dumps.

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
