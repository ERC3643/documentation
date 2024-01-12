# Identity Registry Storage

# Events

## IdentityStored

This event is emitted when an Identity is registered into the storage contract.  
the event is emitted by the 'registerIdentity' function  
`investorAddress` is the address of the investor's wallet  
`identity` is the address of the Identity smart contract (onchainID)

```javascript Solidity
event IdentityStored(
  address indexed investorAddress, 
  IIdentity indexed identity
);
```

## IdentityUnstored

This event is emitted when an Identity is removed from the storage contract.  
the event is emitted by the 'deleteIdentity' function  
`investorAddress` is the address of the investor's wallet  
`identity` is the address of the Identity smart contract (onchainID)

```javascript Solidity
event IdentityUnstored(
  address indexed investorAddress, 
  IIdentity indexed identity
);
```

## IdentityModified

This event is emitted when an Identity has been updated  
the event is emitted by the 'updateIdentity' function  
`oldIdentity` is the old Identity contract's address to update  
`newIdentity` is the new Identity contract's

```javascript Solidity
event IdentityModified(
  IIdentity indexed oldIdentity, 
  IIdentity indexed newIdentity
);
```

## CountryModified

This event is emitted when an Identity's country has been updated  
the event is emitted by the 'updateCountry' function  
`investorAddress` is the address on which the country has been updated  
`country` is the numeric code (ISO 3166-1) of the new country

```javascript Solidity
event CountryModified(
  address indexed investorAddress, 
  uint16 indexed country
);
```

## IdentityRegistryBound

This event is emitted when an Identity Registry is bound to the storage contract  
the event is emitted by the 'addIdentityRegistry' function  
`identityRegistry` is the address of the identity registry added

```javascript Solidity
event IdentityRegistryBound(
  address indexed identityRegistry
);
```

## IdentityRegistryUnbound

This event is emitted when an Identity Registry is unbound from the storage contract  
the event is emitted by the 'removeIdentityRegistry' function  
`identityRegistry` is the address of the identity registry removed

```javascript Solidity
event IdentityRegistryUnbound(
  address indexed identityRegistry
);
```

# Functions

## linkedIdentityRegistries

Returns the identity registries linked to the storage contract

```javascript Solidity
function linkedIdentityRegistries() external view returns (address[] memory);
```

## storedIdentity

Returns the onchainID of an investor.  
parameter 1 : `_userAddress` The wallet of the investor

```javascript Solidity
function storedIdentity(
address _userAddress
) external view returns (IIdentity);
```

## storedInvestorCountry

Returns the country code of an investor.  
parameter 1 : `_userAddress` The wallet of the investor

```javascript Solidity
function storedInvestorCountry(
address _userAddress
) external view returns (uint16);
```

## addIdentityToStorage

adds an identity contract corresponding to a user address in the storage.  
Requires that the user doesn't have an identity contract already registered.  
This function can only be called by an address set as agent of the smart contract  
parameter 1 : `_userAddress` The address of the user  
parameter 2 : `_identity` The address of the user's identity contract  
parameter 3 : `_country` The country of the investor  
emits `IdentityStored` event

```javascript Solidity
function addIdentityToStorage(
address _userAddress, 
IIdentity _identity, 
uint16 _country
) external;
```

## removeIdentityFromStorage

Removes an user from the storage.  
Requires that the user have an identity contract already deployed that will be deleted.  
This function can only be called by an address set as agent of the smart contract  
parameter 1 : `_userAddress` The address of the user to be removed  
emits `IdentityUnstored` event

```javascript Solidity
function removeIdentityFromStorage(
address _userAddress
) external;
```

## modifyStoredInvestorCountry

Updates the country corresponding to a user address.  
Requires that the user should have an identity contract already deployed that will be replaced.  
This function can only be called by an address set as agent of the smart contract  
parameter 1 : `_userAddress` The address of the user  
parameter 2 : `_country` The new country of the user  
emits `CountryModified` event

```javascript Solidity
function modifyStoredInvestorCountry(
address _userAddress, 
uint16 _country
) external;
```

## modifyStoredIdentity

Updates an identity contract corresponding to a user address.  
Requires that the user address should be the owner of the identity contract.  
Requires that the user should have an identity contract already deployed that will be replaced.  
This function can only be called by an address set as agent of the smart contract  
parameter 1 : `_userAddress` The address of the user  
parameter 2 : `_identity` The address of the user's new identity contract  
emits `IdentityModified` event

```javascript Solidity
function modifyStoredIdentity(
address _userAddress, 
IIdentity _identity
) external;
```

## transferOwnershipOnIdentityRegistryStorage

Transfers the Ownership of the Identity Registry Storage to a new Owner.  
This function can only be called by the wallet set as owner of the smart contract  
parameter 1 : `_newOwner` The new owner of this contract.

```javascript Solidity
function transferOwnershipOnIdentityRegistryStorage(
address _newOwner
) external;
```

## bindIdentityRegistry

Adds an identity registry as agent of the Identity Registry Storage Contract.  
This function can only be called by the wallet set as owner of the smart contract  
This function adds the identity registry to the list of identityRegistries linked to the storage contract  
parameter 1 : `_identityRegistry` The identity registry address to add.

```javascript Solidity
function bindIdentityRegistry(
address _identityRegistry
) external;
```

## unbindIdentityRegistry

Removes an identity registry from being agent of the Identity Registry Storage Contract.  
This function can only be called by the wallet set as owner of the smart contract  
This function removes the identity registry from the list of identityRegistries linked to the storage contract  
parameter 1 : `_identityRegistry` The identity registry address to remove.

```javascript Solidity
function unbindIdentityRegistry(
address _identityRegistry
) external;
```