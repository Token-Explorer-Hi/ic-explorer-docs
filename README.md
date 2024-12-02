# IC Explorer API Documentation

## About
This repository contains the official API documentation for IC Explorer, a comprehensive blockchain explorer for the Internet Computer (IC) ecosystem. The documentation provides detailed information about endpoints, request/response formats, and examples for integrating with IC Explorer's services.

## Purpose
- Provide clear and comprehensive API documentation for developers
- Enable seamless integration with IC Explorer's blockchain data services
- Support developers building applications on the Internet Computer platform

## API Documentation Index

### Transaction History
- Transaction List Query (`POST /api/tx/list`)
  - Paginated transaction history
  - Filtering by time range, category, and token
  - Detailed transaction information for transfers and swaps

### Token Information
- Token Holder Query (`POST /api/holder/token`)
  - Token holder lists with balances
  - USD value information
  - Holder account details

### User Holdings
- User Token List Query (`POST /api/holder/user`)
  - User token balance queries
  - Support for principal, accountId, and accountTextual lookups
  - Token holdings with USD valuations

## Getting Started
For detailed API specifications and examples, please refer to the [API Documentation](api.md).

## Support
If you have any questions or need assistance, please open an issue in this repository.
