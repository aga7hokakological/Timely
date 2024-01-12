# Lines of code

https://github.com/code-423n4/2022-12-forgeries/blob/main/src/VRFNFTRandomDraw.sol#L33


# Vulnerability details

risk = 2 (Med Risk)

## Impact
Current month value is more than the real value in seconds for month which can cause wrong calculation in recovery time.

## Proof of Concept
[Here](https://github.com/code-423n4/2022-12-forgeries/blob/main/src/VRFNFTRandomDraw.sol#L93-L98) if you see `MONTH_IN_SECONDS * 12` which is `217728000` instead of regular value: `31556926`

## Tools Used
Manual Analysis

## Recommended Mitigation Steps
Add year variable setting it to seconds: `31556926` and change month variable value: `3600*24*30`


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