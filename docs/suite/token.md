# Security Token

# Token Constructor

The constructor initiates the token contract  
`msg.sender` is set automatically as the owner of the smart contract  
parameter 1 : `_identityRegistry` the address of the Identity registry linked to the token  
parameter 2 : `_compliance` the address of the compliance contract linked to the token  
parameter 3 : `_name` the name of the token  
parameter 4 : `_symbol` the symbol of the token  
parameter 5 : `_decimals` the decimals of the token  
parameter 6 : `_onchainID` the address of the onchainID of the token  
emits an `UpdatedTokenInformation` event  
emits an `IdentityRegistryAdded` event  
emits a `ComplianceAdded` event

```javascript Solidity
constructor(
        address _identityRegistry,
        address _compliance,
        string memory _name,
        string memory _symbol,
        uint8 _decimals,
        address _onchainID
        ) public;
```

# Token events

## Transfer

ERC20 Event : Emitted when `value` tokens are moved from one account (`from`) to another (`to`).  
Note that `value` may be zero.

```javascript Solidity
event Transfer(
  address indexed from, 
  address indexed to, 
  uint256 value
);
```

## Approval

ERC20 Event : Emitted when the allowance of a `spender` for an `owner` is set by a call to `approve()`. `value` is the new allowance.

```javascript Solidity
event Approval(
  address indexed owner, 
  address indexed spender, 
  uint256 value
);
```

## UpdatedTokenInformation

This event is emitted when the token is created, and is emitted only by the Token constructor.  
`_newName` is the name of the token  
`_newSymbol` is the symbol of the token  
`_newDecimals` is the decimals of the token  
`_newVersion` is the version of the token, current version is 3.0  
`_newOnchainID` is the address of the onchainID of the token

```javascript Solidity
event UpdatedTokenInformation(
  string _newName, 
  string _newSymbol, 
  uint8 _newDecimals, 
  string _newVersion, 
  address _newOnchainID
);
```

## IdentityRegistryAdded

This event is emitted when the IdentityRegistry has been set for the token  
the event is emitted by the token constructor and by the setIdentityRegistry function  
`_identityRegistry` is the address of the Identity Registry of the token

```javascript Solidity
event IdentityRegistryAdded(
  address indexed _identityRegistry
);
```

## ComplianceAdded

This event is emitted when the Compliance has been set for the token  
the event is emitted by the token constructor and by the setCompliance function  
`_compliance` is the address of the Compliance contract of the token

```javascript Solidity
event ComplianceAdded(
  address indexed _compliance
);
```

## RecoverySuccess

This event is emitted when an investor successfully recovers his tokens  
the event is emitted by the recoveryAddress function  
`_lostWallet` is the address of the wallet that the investor lost access to  
`_newWallet` is the address of the wallet that the investor provided for the recovery  
`_investorOnchainID` is the address of the onchainID of the investor who asked for a recovery

```javascript Solidity
event RecoverySuccess(
  address _lostWallet, 
  address _newWallet, 
  address _investorOnchainID
);
```

## AddressFrozen

This event is emitted when the wallet of an investor is frozen or unfrozen  
the event is emitted by setAddressFrozen and batchSetAddressFrozen functions  
`_userAddress` is the wallet of the investor that is concerned by the freezing status  
`_isFrozen` is the freezing status of the wallet  
if `_isFrozen` equals `true` the wallet is frozen after emission of the event  
if `_isFrozen` equals `false` the wallet is unfrozen after emission of the event  
`_owner` is the address of the agent who called the function to freeze the wallet

```javascript Solidity
event AddressFrozen(
  address indexed _userAddress, 
  bool indexed _isFrozen, 
  address indexed _owner
);
```

## TokensFrozen

This event is emitted when a certain amount of tokens is frozen on a wallet  
the event is emitted by freezePartialTokens and batchFreezePartialTokens functions  
`_userAddress` is the wallet of the investor that is concerned by the freezing status  
`_amount` is the amount of tokens that are frozen

```javascript Solidity
event TokensFrozen(
  address indexed _userAddress, 
  uint256 _amount
);
```

## TokensUnfrozen

This event is emitted when a certain amount of tokens is unfrozen on a wallet  
the event is emitted by unfreezePartialTokens and batchUnfreezePartialTokens functions  
`_userAddress` is the wallet of the investor that is concerned by the freezing status  
`_amount` is the amount of tokens that are unfrozen

```javascript Solidity
event TokensUnfrozen(
  address indexed _userAddress, 
  uint256 _amount
);
```

## Paused

This event is emitted when the token is paused  
the event is emitted by the pause function  
`_userAddress` is the address of the wallet that called the pause function

```javascript Solidity
event Paused(
  address _userAddress
);
```

## Unpaused

This event is emitted when the token is unpaused  
the event is emitted by the unpause function  
`_userAddress` is the address of the wallet that called the unpause function

```javascript Solidity
event Unpaused(
  address _userAddress
);
```

# Functions

## totalSupply

ERC20 Function : Returns the amount of tokens in existence.

```javascript Solidity
function totalSupply() public view returns (uint256);
```

## balanceOf

ERC20 Function : Returns the amount of tokens owned by an investor  
parameter 1 : `_userAddress` the address of the investor's wallet

```javascript Solidity
function balanceOf(
address _userAddress
) public view returns (uint256);
```

## allowance

ERC20 Function : Returns the remaining number of tokens that `spender` will be allowed to spend on behalf of `owner` through `transferFrom()`. This is zero by default.  
This value changes when `approve()` or `transferFrom()` are called.

```javascript Solidity
function allowance(
address _owner, 
address _spender) 
public view virtual returns (uint256);
```

## approve

ERC20 Function : Sets `amount` as the allowance of `spender` over the caller's tokens.  
Returns a boolean value indicating whether the operation succeeded.  
IMPORTANT: Beware that changing an allowance with this method brings the risk that someone may use both the old and the new allowance by unfortunate transaction ordering. One possible solution to mitigate this race condition is to first reduce the spender's allowance to 0 and set the desired value afterwards: <https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729>  
Emits an `Approval` event.

```javascript Solidity
function approve(
address _spender, 
uint256 _amount
) public virtual returns (bool);
```

## increaseAllowance

ERC20 Function : Atomically increases the allowance granted to `spender` by the caller.  
This is an alternative to `approve()` that can be used as a mitigation for problems described in `approve()`  
Emits an `Approval` event indicating the updated allowance.  
Requirements:

- `spender` cannot be the zero address.

```javascript Solidity
function increaseAllowance(
address _spender, 
uint256 _addedValue
) public virtual returns (bool);
```

## decreaseAllowance

ERC20 Function : Atomically decreases the allowance granted to `spender` by the caller.  
This is an alternative to `approve()` that can be used as a mitigation for problems described in `approve()`  
Emits an `Approval` event indicating the updated allowance.  
Requirements:

- `spender` cannot be the zero address.
- `spender` must have allowance for the caller of at least `subtractedValue`.

```javascript Solidity
function decreaseAllowance(
address _spender, 
uint256 _subtractedValue
) public virtual returns (bool);
```

## decimals

Returns the number of decimals used to get its user representation.  
For example, if `decimals` equals `2`, a balance of `505` tokens should be displayed to a user as `5,05` (`505 / 1 ** 2`).  
Tokens usually opt for a value of 18, imitating the relationship between Ether and Wei.  
NOTE: This information is only used for _display_ purposes: it in no way affects any of the arithmetic of the contract, including `balanceOf()` and `transfer()`.

```javascript Solidity
function decimals() external view returns (uint8);
```

## name

Returns the name of the token.

```javascript Solidity
function name() external view returns (string memory);
```

## onchainID

Returns the address of the onchainID of the token.  
The onchainID of the token gives all the information available about the token and is managed by the token issuer or his agent.

```javascript Solidity
function onchainID() external view returns (address);
```

## symbol

Returns the symbol of the token, usually a shorter version of the name.

```javascript Solidity
function symbol() external view returns (string memory);
```

## version

Returns the TREX version of the token.  
Current version is 3.0.0

```javascript Solidity
function version() external view returns (string memory);
```

## identityRegistry

Returns the Identity Registry linked to the token

```javascript Solidity
function identityRegistry() external view returns (IIdentityRegistry);
```

## compliance

Returns the Compliance contract linked to the token

```javascript Solidity
function compliance() external view returns (ICompliance);
```

## paused

Returns true if the contract is paused, and false otherwise.

```javascript Solidity
function paused() external view returns (bool);
```

## isFrozen

Returns the freezing status of a wallet  
if isFrozen returns `true` the wallet is frozen  
if isFrozen returns `false` the wallet is not frozen  
isFrozen returning `true` doesn't mean that the balance is free, tokens could be blocked by a partial freeze or the whole token could be blocked by pause  
parameter 1 : `_userAddress` the address of the wallet on which isFrozen is called

```javascript Solidity
function isFrozen(
address _userAddress
) external view returns (bool);
```

## getFrozenTokens

Returns the amount of tokens that are partially frozen on a wallet  
the amount of frozen tokens is always \<= to the total balance of the wallet  
parameter 1 : `_userAddress` the address of the wallet on which getFrozenTokens is called

```javascript Solidity
function getFrozenTokens(
address _userAddress
) external view returns (uint256);
```

## setName

Sets the token name  
parameter 1 : `_name` the name of token to set  
Only the owner of the token smart contract can call this function  
emits a `UpdatedTokenInformation` event

```javascript Solidity
function setName(
string calldata _name
) external;
```

## setSymbol

Sets the token symbol  
parameter 1 : `_symbol` the token symbol to set  
Only the owner of the token smart contract can call this function  
emits a `UpdatedTokenInformation` event

```javascript Solidity
function setSymbol(
string calldata _symbol
) external;
```

## setOnchainID

Sets the onchain ID of the token  
parameter 1 : `_onchainID` the address of the onchain ID to set  
Only the owner of the token smart contract can call this function  
emits a `UpdatedTokenInformation` event

```javascript Solidity
function setOnchainID(
address _onchainID
) external;
```

## pause

Pauses the token contract, when contract is paused investors cannot transfer tokens anymore  
This function can only be called by a wallet set as agent of the token  
emits a `Paused` event

```javascript Solidity
function pause() external;
```

## unpause

Unpauses the token contract, when contract is unpaused investors can transfer tokens  
if their wallet is not blocked & if the amount to transfer is \<= to the amount of free tokens  
This function can only be called by a wallet set as agent of the token  
emits an `Unpaused` event

```javascript Solidity
function unpause() external;
```

## setAddressFrozen

Sets an address frozen status for this token.  
parameter 1 : `_userAddress` The address for which to update frozen status  
parameter 2 : `_freeze` Frozen status of the address  
This function can only be called by a wallet set as agent of the token  
emits an `AddressFrozen` event

```javascript Solidity
function setAddressFrozen(
address _userAddress, 
bool _freeze
) external;
```

## freezePartialTokens

Freezes token amount specified for given address.  
parameter 1 : `_userAddress` The address for which to update frozen tokens  
parameter 2 : `_amount` Amount of Tokens to be frozen  
This function can only be called by a wallet set as agent of the token  
emits a `TokensFrozen` event

```javascript Solidity
function freezePartialTokens(
address _userAddress, 
uint256 _amount
) external;
```

## unfreezePartialTokens

Unfreezes token amount specified for given address  
parameter 1 : `_userAddress` The address for which to update frozen tokens  
parameter 2 : `_amount` Amount of Tokens to be unfrozen  
This function can only be called by a wallet set as agent of the token  
emits a `TokensUnfrozen` event

```javascript Solidity
function unfreezePartialTokens(
address _userAddress, 
uint256 _amount
) external;
```

## setIdentityRegistry

Sets the Identity Registry for the token  
parameter 1 : `_identityRegistry` the address of the Identity Registry to set  
Only the owner of the token smart contract can call this function  
emits an `IdentityRegistryAdded` event

```javascript Solidity
function setIdentityRegistry(
address _identityRegistry
) external;
```

## setCompliance

Sets the compliance contract of the token  
parameter 1 : `_compliance` the address of the compliance contract to set  
Only the owner of the token smart contract can call this function  
emits a `ComplianceAdded` event

```javascript Solidity
function setCompliance(
address _compliance
) external;
```

## transfer

ERC-20 overridden function that include logic to check for trade validity.  
Moves `_amount` tokens from the caller's account to the recipient `_to`.  
Require that the token is not paused  
Require that the `msg.sender` and `_to` addresses are not frozen.  
Require that the `_amount` should not exceed available balance .  
Require that the `_to` address is a verified address  
parameter 1 : `_to` The address of the receiver  
parameter 2 : `_amount` The number of tokens to transfer  
Returns  `true` if successful and revert if unsuccessful  
emits a `Transfer` event

```javascript Solidity
function transfer(
address _to, 
uint256 _amount
) public whenNotPaused returns (bool);
```

## transferFrom

ERC-20 overridden function that include logic to check for trade validity.  
Moves `_amount` tokens from sender `_from` to recipient `_to` using the allowance mechanism. `_amount` is then deducted from the caller's allowance.  
Require that the token is not paused  
Require that the from and to addresses are not frozen.  
Require that the value should not exceed available balance .  
Require that the to address is a verified address  
parameter 1 : `_from` The address of the sender  
parameter 2 : `_to` The address of the receiver  
parameter 3 : `_amount` The number of tokens to transfer  
Returns `true` if successful and revert if unsuccessful  
emits a `Transfer` event

```javascript Solidity
function transferFrom(
address _from, 
address _to, 
uint256 _amount
) public whenNotPaused returns (bool);
```

## forcedTransfer

Force a transfer of tokens between 2 whitelisted wallets  
In case the `from` address has not enough free tokens (unfrozen tokens) but has a total balance higher or equal to the `amount` the amount of frozen tokens is reduced in order to have enough free tokens to proceed the transfer, in such a case, the remaining balance on the `from` account is 100% composed of frozen tokens post-transfer.  
Require that the `to` address is a verified address,  
parameter 1 : `_from` The address of the sender  
parameter 2 : `_to` The address of the receiver  
parameter 3 : `_amount` The number of tokens to transfer  
Returns `true` if successful and revert if unsuccessful  
This function can only be called by a wallet set as agent of the token  
emits a `TokensUnfrozen` event if `_amount` is higher than the free balance of `_from`  
emits a `Transfer` event

```javascript Solidity
function forcedTransfer(
address _from, 
address _to, 
uint256 _amount
) external returns (bool);
```

## mint

Mint tokens on a wallet  
Improved version of default mint method. Tokens can be minted to an address if only it is a verified address as per the security token.  
parameter 1 : `_to` Address to mint the tokens to.  
parameter 2 : `_amount` Amount of tokens to mint.  
This function can only be called by a wallet set as agent of the token  
emits a `Transfer` event

```javascript Solidity
function mint(
address _to, 
uint256 _amount
) external;
```

## burn

Burn tokens on a wallet  
In case the `account` address has not enough free tokens (unfrozen tokens) but has a total balance higher or equal to the `value` amount the amount of frozen tokens is reduced in order to have enough free tokens to proceed the burn, in such a case, the remaining balance on the `account` is 100% composed of frozen tokens post-transaction.  
parameter 1 : `_userAddress` Address to burn the tokens from.  
parameter 2 : `_amount Amount` of tokens to burn.  
This function can only be called by a wallet set as agent of the token  
emits a `TokensUnfrozen` event if `_amount` is higher than the free balance of `_userAddress`  
emits a `Transfer` event

```javascript Solidity
function burn(
address _userAddress, 
uint256 _amount
) external;
```

## recoveryAddress

Recovery function used to force transfer tokens from a lost wallet to a new wallet for an investor.  
parameter 1 : `_lostWallet` the wallet that the investor lost  
parameter 2 : `_newWallet` the newly provided wallet on which tokens have to be transferred  
parameter 3 : `_investorOnchainID` the onchainID of the investor asking for a recovery  
This function can only be called by a wallet set as agent of the token  
emits a `TokensUnfrozen` event if there is some frozen tokens on the lost wallet if the recovery process is successful  
emits a `Transfer` event if the recovery process is successful  
emits a `RecoverySuccess` event if the recovery process is successful

```javascript Solidity
function recoveryAddress(
address _lostWallet, 
address _newWallet, 
address _investorOnchainID
) external returns (bool);
```

## batchTransfer

Function allowing to issue transfers in batch  
Require that the `msg.sender` and `to` addresses are not frozen.  
Require that the total value should not exceed available balance.  
Require that the `to` addresses are all verified addresses,  
**IMPORTANT : THIS TRANSACTION COULD EXCEED GAS LIMIT IF `_toList.length` IS TOO HIGH, USE WITH CARE OR YOU COULD LOSE TX FEES WITH AN "OUT OF GAS" TRANSACTION**  
parameter 1 : `_toList` The addresses of the receivers  
parameter 2 : `_amounts` The number of tokens to transfer to the corresponding receiver  
emits \_toList.length `Transfer` events

```javascript Solidity
function batchTransfer(
address[] calldata _toList, 
uint256[] calldata _amounts
) external;
```

## batchForcedTransfer

Function allowing to issue forced transfers in batch  
Require that `_amounts[i]` should not exceed available balance of `_fromList[i]`.  
Require that the `_toList` addresses are all verified addresses  
**IMPORTANT : THIS TRANSACTION COULD EXCEED GAS LIMIT IF `_fromList.length` IS TOO HIGH, USE WITH CARE OR YOU COULD LOSE TX FEES WITH AN "OUT OF GAS" TRANSACTION**  
parameter 1 : `_fromList` The addresses of the senders  
parameter 2 : `_toList` The addresses of the receivers  
parameter 3 : `_amounts` The number of tokens to transfer to the corresponding receiver  
This function can only be called by a wallet set as agent of the token  
emits `TokensUnfrozen` events if `_amounts[i]` is higher than the free balance of `_fromList[i]`  
emits `_fromList.length` `Transfer` events

```javascript Solidity
function batchForcedTransfer(
address[] calldata _fromList, 
address[] calldata _toList, 
uint256[] calldata _amounts
) external;
```

## batchMint

Function allowing to mint tokens in batch  
Require that the `_toList` addresses are all verified addresses  
**IMPORTANT : THIS TRANSACTION COULD EXCEED GAS LIMIT IF `_toList.length` IS TOO HIGH, USE WITH CARE OR YOU COULD LOSE TX FEES WITH AN "OUT OF GAS" TRANSACTION**  
parameter 1 : `_toList` The addresses of the receivers  
parameter 2 : `_amounts` The number of tokens to mint to the corresponding receiver  
This function can only be called by a wallet set as agent of the token  
emits `_toList.length` `Transfer` events

```javascript Solidity
function batchMint(
address[] calldata _toList, 
uint256[] calldata _amounts
) external;
```

## batchBurn

Function allowing to burn tokens in batch  
Require that the `_userAddresses` addresses are all verified addresses  
**IMPORTANT : THIS TRANSACTION COULD EXCEED GAS LIMIT IF `_userAddresses.length` IS TOO HIGH, USE WITH CARE OR YOU COULD LOSE TX FEES WITH AN "OUT OF GAS" TRANSACTION**  
parameter 1 : `_userAddresses` The addresses of the wallets concerned by the burn  
parameter 2 : `_amounts` The number of tokens to burn from the corresponding wallets  
This function can only be called by a wallet set as agent of the token  
emits `_userAddresses.length` `Transfer` events

```javascript Solidity
function batchBurn(
address[] calldata _userAddresses, 
uint256[] calldata _amounts
) external;
```

## batchSetAddressFrozen

Function allowing to set frozen addresses in batch  
**IMPORTANT : THIS TRANSACTION COULD EXCEED GAS LIMIT IF `_userAddresses.length` IS TOO HIGH, USE WITH CARE OR YOU COULD LOSE TX FEES WITH AN "OUT OF GAS" TRANSACTION**  
parameter 1 : `_userAddresses` The addresses for which to update frozen status  
parameter 2 : `_freeze` Frozen status of the corresponding address  
This function can only be called by a wallet set as agent of the token  
emits `_userAddresses.length` `AddressFrozen` events

```javascript Solidity
function batchSetAddressFrozen(
address[] calldata _userAddresses, 
bool[] calldata _freeze
) external;
```

## batchFreezePartialTokens

Function allowing to freeze tokens partially in batch  
**IMPORTANT : THIS TRANSACTION COULD EXCEED GAS LIMIT IF `_userAddresses.length` IS TOO HIGH, USE WITH CARE OR YOU COULD LOSE TX FEES WITH AN "OUT OF GAS" TRANSACTION**  
parameter 1 : `_userAddresses` The addresses on which tokens need to be frozen  
parameter 2 : `_amounts` the amount of tokens to freeze on the corresponding address  
This function can only be called by a wallet set as agent of the token  
emits `_userAddresses.length` `TokensFrozen` events

```javascript Solidity
function batchFreezePartialTokens(
address[] calldata _userAddresses, 
uint256[] calldata _amounts
) external;
```

## batchUnfreezePartialTokens

Function allowing to unfreeze tokens partially in batch  
**IMPORTANT : THIS TRANSACTION COULD EXCEED GAS LIMIT IF `_userAddresses.length` IS TOO HIGH, USE WITH CARE OR YOU COULD LOSE TX FEES WITH AN "OUT OF GAS" TRANSACTION**  
parameter 1 : `_userAddresses` The addresses on which tokens need to be unfrozen  
parameter 2 : `_amounts` the amount of tokens to unfreeze on the corresponding address  
This function can only be called by a wallet set as agent of the token  
emits `_userAddresses.length` `TokensUnfrozen` events

```javascript Solidity
function batchUnfreezePartialTokens(
address[] calldata _userAddresses, 
uint256[] calldata _amounts
) external;
```

## transferOwnershipOnTokenContract

Transfers the ownership of the token smart contract  
parameter 1 : `_newOwner` the address of the new token smart contract owner  
This function can only be called by the owner of the token  
emits an `OwnershipTransferred` event

```javascript Solidity
function transferOwnershipOnTokenContract(
address _newOwner
) external;
```

## addAgentOnTokenContract

Adds an agent to the token smart contract  
parameter 1 : `_agent` the address of the new agent of the token smart contract  
This function can only be called by the owner of the token  
emits an `AgentAdded` event

```javascript Solidity
function addAgentOnTokenContract(
address _agent
) external;
```

## removeAgentOnTokenContract

Remove an agent from the token smart contract  
parameter 1 : `_agent` the address of the agent to remove  
This function can only be called by the owner of the token  
emits an `AgentRemoved` event

```javascript Solidity
function removeAgentOnTokenContract(
address _agent
) external;
```