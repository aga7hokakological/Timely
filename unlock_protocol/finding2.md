C4 finding submitted:

# Handle

aga7hokakological


# Vulnerability details

## Impact
The functions should be ordered according to their visibility and order and solidity style guide:
constructor > fallback function (if exists) > external > public > internal > private and view/pure functions at last.


## Proof of Concept
abstract contract ERC20PermitUpgradeable is Initializable, ERC20Upgradeable, IERC20PermitUpgradeable, EIP712Upgradeable {
function __ERC20Permit_init_unchained(string memory name) internal initializer {
      _PERMIT_TYPEHASH = keccak256("Permit(address owner,address spender,uint256 value,uint256 nonce,uint256 deadline)");
  }

  function __ERC20Permit_init_unsafe(string memory name) internal {
      _PERMIT_TYPEHASH = keccak256("Permit(address owner,address spender,uint256 value,uint256 nonce,uint256 deadline)");
  }

  /**
   * @dev See {IERC20Permit-permit}.
   */
  function permit(
      address owner,
      address spender,
      uint256 value,
      uint256 deadline,
      uint8 v,
      bytes32 r,
      bytes32 s
  ) public virtual override {
      require(block.timestamp <= deadline, "ERC20Permit: expired deadline");

      bytes32 structHash = keccak256(abi.encode(_PERMIT_TYPEHASH, owner, spender, value, _useNonce(owner), deadline));

      bytes32 hash = _hashTypedDataV4(structHash);

      address signer = ECDSAUpgradeable.recover(hash, v, r, s);
      require(signer == owner, "ERC20Permit: invalid signature");

      _approve(owner, spender, value);
  }

## Tools Used
Manual analysis