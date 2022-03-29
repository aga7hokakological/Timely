C4 finding submitted: (risk = 2 (Med Risk))

# Lines of code

https://github.com/code-423n4/2022-03-prepo/blob/main/contracts/core/Collateral.sol#L155


# Vulnerability details

## Impact
Wrong calculation in this specific code block can lead to transaction reversal which might affect total withdrawal calculation use for collatoral.

## Proof of Concept

The code block which is wrong: 
```
uint256 _balanceBefore = _Token.balanceOf(address(this));
withdraw(address(this), _owed);
uint256 _balanceAfter = _Token.balanceOf(address(this));

uint256 _amountWithdrawn = _balanceAfter - _balanceBefore;
```

## Tools Used
Manual analysis

## Recommended Mitigation Steps

Here `uint256 _amountWithdrawn = _balanceAfter - _balanceBefore; `

should be `uint256 _amountWithdrawn = _balanceBefore - _balanceAfter;`