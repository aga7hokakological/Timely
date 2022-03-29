C4 finding submitted: (risk = 1 (Low Risk))

# Handle

aga7hokakological


# Vulnerability details

## Impact
No return values for ERC20 functions. An approve function should return bool if approved correctly

## Proof of Concept
In the following function
```
interface ApproveLike {
  function approve(address, uint256) external;
}
```
There is no return value to check if approved correctly or not.

## Tools Used
Manual Analysis

## Recommended Mitigation Steps
Consider:
```
interface ApproveLike {
  function approve(address, uint256) external returns(bool success) ;
}
```