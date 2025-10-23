
# Compliant Private Tokens Workshop - Token Template

This is the Leo project scaffolding for the Aleo compliant private tokens workshop.  For more information, head over to the [main repository](https://github.com/alex-aleo/private-token-workshop).

## Project Overview

This project implements a compliant private token system on the Aleo blockchain with OFAC (Office of Foreign Assets Control) compliance checks. The token program supports both public and private transactions while maintaining regulatory compliance.

### Program Information
- **Program Name**: `basscee_workshop_token.aleo`
- **Version**: 0.1.0
- **License**: MIT
- **Network**: Testnet (configured in `.env`)
- **Endpoint**: https://api.explorer.provable.com/v1

## Features

The token program implements the following core functionalities:

### 1. Public Minting (`mint_public`)
- Mints new tokens by updating the public mapping
- Includes OFAC compliance check for recipients
- Updates recipient balance in the public `balances` mapping

### 2. Private Minting (`mint_private`)
- Mints new tokens as private records
- Includes OFAC compliance check for recipients  
- Returns a `Token` record with specified amount

### 3. Public Transfers (`transfer_public`)
- Transfers tokens between addresses using public mappings
- Includes OFAC compliance check for recipients
- Deducts from sender's balance and adds to recipient's balance

### 4. Private Transfers (`transfer_private`)
- Transfers tokens using private records
- Includes OFAC compliance check for recipients
- Consumes sender's record and creates new records for both parties

## Token Structure

```leo
record Token {
    owner: address,  // The token owner
    amount: u64,     // The token amount
}

mapping balances: address => u64;  // Public token balances
```

## Dependencies

- `workshop_ofac.aleo` - Provides OFAC compliance checking functionality

## Project Structure

```
├── src/
│   └── main.leo              # Main token program implementation
├── tests/
│   └── test_token.leo        # Test suite
├── build/
│   ├── main.aleo            # Compiled program
│   ├── program.json         # Build configuration
│   └── imports/
│       └── workshop_ofac.aleo
├── outputs/                  # Build outputs directory
├── program.json             # Project configuration
├── .env                     # Environment configuration
└── README.md               # This file
```

## Deployment Information

### Deployment ID
*at1rcwywuewnmpm3adl20aqpww9p0jldnuvy4wfq5urdxn226j7vcpqql62g5*

### Transaction IDs
*Transaction IDs will be populated here after program interactions:*

#### Deployment Transaction
- **Transaction ID**: *DEPLOYED*

#### Function Calls
- **mint_public**: *at14lc3wprj79vln3f0v39aj2qlrravpzshgrxtr7ufse5nen3p55xsmlslgh*

- **mint_private**: 
  - *at1kerppd9uqz3usn4a7w8sy88n7k99sesknpnu5xr5w8fjk7myys8qrz50pn*
  - *at1qxpr9zywzggd64evsjzm5s9xqhtwpapefl8xyt79kuqpqc9stu9su3d443* (Minted 200 tokens for private transfer)

- **transfer_public**: *at1xpdfyqvdr62ra8uk2xw36w5rysv6v8yg43x7zhaktcke2kz6ec8q3lef8q* 
  - Transferred 100 tokens to `aleo1k9qmksvt0wcgj6tamj75r2xfjfcua5hafu3w35ypjrlzg53fqs8qyrk823`
- **transfer_private**: *Pending - Network connectivity issues with state path fetching*
  - Token record available from mint_private transaction: `at1qxpr9zywzggd64evsjzm5s9xqhtwpapefl8xyt79kuqpqc9stu9su3d443`

## Setup and Development

1. **Environment Setup**: The project is configured for testnet deployment with environment variables in `.env`

2. **Building**: Compile the Leo program to generate Aleo bytecode in the `build/` directory

3. **Testing**: Run tests using the test suite in `tests/test_token.leo`

4. **Deployment**: Deploy to Aleo testnet using the configured private key and endpoint

## Compliance Features

This token implementation includes mandatory OFAC compliance checks for all recipient addresses through integration with `workshop_ofac.aleo`. All minting and transfer operations verify that recipient addresses are not on sanctioned lists before executing transactions.

## Future Enhancements (Bonus Tasks)

Potential additional features to implement:
- `transfer_private_to_public()` - Convert private tokens to public
- `transfer_public_to_private()` - Convert public tokens to private  
- `approve_public()` - Public allowance system
- `approve_private()` - Private allowance system
- `transfer_from()` - Delegated transfers
- `burn_public()` - Destroy public tokens
- `burn_private()` - Destroy private tokens

