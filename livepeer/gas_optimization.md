C4 finding submitted: (risk = G (Gas Optimization))

# Handle

aga7hokakological


# Vulnerability details

## Impact
Revert strings that are longer than 32 bytes require at least one additional mstore, along with additional overhead for computing memory offset, etc.

## Proof of Concept
https://github.com/livepeer/arbitrum-lpt-bridge/blob/main/contracts/L2/gateway/L2Migrator.sol#L184
https://github.com/livepeer/arbitrum-lpt-bridge/blob/main/contracts/L2/gateway/L2Migrator.sol#L136
https://github.com/livepeer/arbitrum-lpt-bridge/blob/main/contracts/L2/gateway/L2Migrator.sol#L201
https://github.com/livepeer/arbitrum-lpt-bridge/blob/main/contracts/L2/gateway/L2Migrator.sol#L221
https://github.com/livepeer/arbitrum-lpt-bridge/blob/main/contracts/L1/gateway/L1Migrator.sol#L508

## Tools Used
Manual Review, Visual Studio Code

## Recommended Mitigation Steps
Shortening revert strings to fit in 32 bytes will decrease deployment time gas and will decrease runtime gas when the revert condition has been met.
