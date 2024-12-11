# Green Energy Trading Platform Smart Contract

## About
The Green Energy Trading Platform is a Clarity smart contract that facilitates the trading of green energy credits between producers and consumers. It provides a secure, transparent, and efficient marketplace for renewable energy certificate trading with built-in verification mechanisms.

## Features
- Producer and consumer registration
- Producer verification system
- Energy credit trading
- Transaction recording
- Authorization controls
- Platform commission management
- Energy production tracking
- Dynamic pricing system

## Contract Structure

### Data Maps
1. `energy-producers`: Stores information about energy producers
   - cumulative-energy-produced
   - producer-verification-status
   - producer-registration-timestamp
   - energy-unit-price

2. `energy-consumers`: Tracks energy consumers
   - cumulative-energy-purchased
   - available-energy-credits
   - consumer-registration-timestamp

3. `energy-trading-records`: Records all trading transactions
   - energy-seller
   - energy-buyer
   - energy-amount
   - transaction-price
   - transaction-timestamp
   - trade-status

### Error Codes
```clarity
ERR-UNAUTHORIZED-ACCESS (u100)
ERR-INVALID-ENERGY-AMOUNT (u101)
ERR-INSUFFICIENT-ENERGY-BALANCE (u102)
ERR-ENERGY-PRODUCER-NOT-FOUND (u103)
ERR-ENERGY-CONSUMER-NOT-FOUND (u104)
ERR-PARTICIPANT-ALREADY-REGISTERED (u105)
ERR-INVALID-TRADE-STATUS (u106)
```

## Public Functions

### Producer Functions
1. `register-energy-producer (initial-energy-price uint)`
   - Registers a new energy producer
   - Sets initial energy price
   - Returns: (ok bool) or (err uint)

2. `record-green-energy-production (production-amount uint)`
   - Records new energy production
   - Requires verified producer status
   - Returns: (ok bool) or (err uint)

### Consumer Functions
1. `register-energy-consumer ()`
   - Registers a new energy consumer
   - Initializes consumer account
   - Returns: (ok bool) or (err uint)

2. `create-energy-trade (producer-address principal) (energy-amount uint)`
   - Initiates energy credit purchase
   - Validates trade parameters
   - Returns: (ok bool) or (err uint)

### Administrative Functions
1. `verify-energy-producer (producer-address principal)`
   - Verifies producer credentials
   - Admin-only function
   - Returns: (ok bool) or (err uint)

2. `update-platform-commission-rate (new-commission-rate uint)`
   - Updates platform commission
   - Admin-only function
   - Returns: (ok bool) or (err uint)

3. `update-minimum-tradeable-energy (new-minimum-amount uint)`
   - Updates minimum trade amount
   - Admin-only function
   - Returns: (ok bool) or (err uint)

## Read-Only Functions
1. `get-energy-producer-details (producer-address principal)`
2. `get-energy-consumer-details (consumer-address principal)`
3. `get-energy-trade-details (trade-identifier uint)`
4. `get-platform-commission-rate ()`

## Usage Examples

### Registering as a Producer
```clarity
(contract-call? .green-energy-trading register-energy-producer u100)
```

### Registering as a Consumer
```clarity
(contract-call? .green-energy-trading register-energy-consumer)
```

### Creating a Trade
```clarity
(contract-call? .green-energy-trading create-energy-trade 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM u500)
```

## Security Considerations
1. Producer verification required before trading
2. Admin-only access for critical functions
3. Balance checks before transfers
4. Input validation for all parameters
5. Transaction atomicity

## Contract Variables
- `energy-trade-sequence`: Tracks trade IDs
- `platform-administrator`: Contract administrator
- `minimum-tradeable-energy`: Minimum trade amount
- `platform-commission-rate`: Platform fee percentage

## Best Practices
1. Always verify producer status before trading
2. Monitor energy balance before transactions
3. Keep track of trade IDs for reference
4. Maintain sufficient energy credits for trading
5. Review transaction details before confirmation

## Contributing
1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push to branch
5. Create Pull Request

**Note**: This contract is designed for the Stacks blockchain and requires appropriate testing before production deployment.