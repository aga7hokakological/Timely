# Lines of code

https://github.com/code-423n4/2022-12-forgeries/blob/main/src/VRFNFTRandomDrawFactory.sol#L24


# Vulnerability details

risk = 2 (Med Risk)

## Impact
Due to a requirement of the proxy-based upgradeability system, no constructors can be used in upgradeable contracts.
Also the `implementation` variable is used inside constructor. While upgrading it might be upgraded to `newImplementation` but as `implementation` is already there both will be accessible.

## Tools Used
Manual Analysis

## Recommended Mitigation Steps
Please remove the constructor from the contract and move the `implementation` variable from constructor to `initialize()` function as `initialize()` function does similar work as constructor.