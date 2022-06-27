# Access control missing for `initialize()` function

It is quite possible that while initializing contract it can be front-run and can be set by some malicious user which can cause trouble and loss of funds.

### POC:
```
function initialize(
      address _stakingToken,
      address _yieldyToken,
      address _tokeToken,
      address _tokePool,
      address _tokeManager,
      address _tokeReward,
      address _liquidityReserve,
      address _feeAddress,
      address _curvePool,
      uint256 _epochDuration,
      uint256 _firstEpochEndTime
  ) external initializer { }
```


### tools used:

manual analysis
