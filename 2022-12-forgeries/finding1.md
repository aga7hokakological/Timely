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