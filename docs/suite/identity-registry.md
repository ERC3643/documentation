# Identity Registry

The Identity Registry smart contract is a registry of identities. It is used by the Asset smart contract to verify that
a recipient is associated with a compliant identity.

Each recipient address (that could be a wallet, a smart contract, or even an ONCHAINID) is associated with an ONCHAINID
in the Identity Registry (it maintains a mapping of `address -> ONCHAINID`).

Multiple assets can share the same identity registry and thus the same rules for identities (same configuration of
required claims and trusted issuers). If assets have different rules, they must use different identity registries.

## Methods

### registerIdentity

Register a mapping between an asset owner address and an ONCHAINID. Requires that the user doesn't have an identity
contract already registered. The method also expects a country integer code. This function can only be called by a
wallet set as agent of the smart contract.

```solidity
function registerIdentity(
    address userAddress,
    address identity,
    uint16 country
);
```

### deleteIdentity

Removes a pairing between an asset owner address and an ONCHAINID. This function can only be called by a wallet set as
agent of the smart contract.

```solidity
function deleteIdentity(address userAddress);
```

### updateCountry

Update the country integer code stored for an asset owner address. This function can only be called by a wallet set as
agent of the smart contract.

```solidity
function updateCountry(address userAddress, uint16 country);
```

### updateIdentity

Update the ONCHAINID address stored for an asset owner address. This function can only be called by a wallet set as
agent of the smart contract.

```solidity
function updateIdentity(address userAddress, address identity);
```

### isVerified

A read only method that returns true if a given asset owner address is associated with an ONCHAINID that satisfies the
requirements for claims topics and trusted issuers.

The method first retrieve the paired ONCHAINID address for the asset holder address, and then verified that there is at
least one valid claim (correct signature and not revoked) issuer by a trusted issuer for each required claim topic on
the ONCHAINID contract.

```solidity
function isVerified(address userAddress) public view returns (bool);
```

## Configuration methods

The owner of the Identity Registry can set the trusted issuer registry, the identity registry storage, and the required
claim topics registry.

### setIdentityRegistryStorage

```solidity
function setIdentityRegistryStorage(address identityRegistryStorage);
```

### setClaimTopicsRegistry

```solidity
function setClaimTopicsRegistry(address claimTopicsRegistry);
```

### setTrustedIssuersRegistry

```solidity
function setTrustedIssuersRegistry(address trustedIssuersRegistry);
```
