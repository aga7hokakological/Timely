C4 finding submitted: (risk = 2 (Med Risk))

 # Lines of code

https://github.com/code-423n4/2022-03-lifinance/blob/main/src/LiFiDiamond.sol#L42-L58


# Vulnerability details

## Impact
If the proxy delegates to an incorrect address, or implementation that has been destructed, the call to the implementation will return success even though no code was executed

## Proof of Concept
According to the blogpost of there is no contract existence check for `facet` contract which has been used
https://blog.trailofbits.com/2020/10/30/good-idea-bad-design-how-the-diamond-standard-falls-short/

```
assembly {
           // copy function selector and any arguments
           calldatacopy(0, 0, calldatasize())
           // execute function call using the facet
           let result := delegatecall(gas(), facet, 0, calldatasize(), 0, 0)
           // get any return value
           returndatacopy(0, 0, returndatasize())
           // return any return value or error back to the caller
           switch result
           case 0 {
               revert(0, returndatasize())
           }
           default {
               return(0, returndatasize())
           }
       }
```

## Tools Used
Manual analysis

## Recommended Mitigation Steps
Always check for contract existence when calling an arbitrary contract.