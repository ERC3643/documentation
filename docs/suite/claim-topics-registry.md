# Claim Topics Registry

# Events

## ClaimTopicAdded

This event is emitted when a claim topic has been added to the ClaimTopicsRegistry  
the event is emitted by the 'addClaimTopic' function  
`claimTopic` is the required claim added to the Claim Topics Registry

```javascript Solidity
event ClaimTopicAdded(
  uint256 indexed claimTopic
);
```

## ClaimTopicRemoved

This event is emitted when a claim topic has been removed from the ClaimTopicsRegistry  
the event is emitted by the 'removeClaimTopic' function  
`claimTopic` is the required claim removed from the Claim Topics Registry

```javascript Solidity
event ClaimTopicRemoved(
  uint256 indexed claimTopic
);
```

# Functions

## addClaimTopic

Add a trusted claim topic (For example: KYC=1, AML=2).  
Only the owner of the smart contract can call this function  
emits `ClaimTopicAdded` event  
parameter 1 : `_claimTopic` The claim topic index

```javascript Solidity
function addClaimTopic(
int256 _claimTopic
) external;
```

## removeClaimTopic

Remove a trusted claim topic (For example: KYC=1, AML=2).  
Only the owner of the smart contract can call this function  
emits `ClaimTopicRemoved` event  
parameter 1 : `_claimTopic` The claim topic index

```javascript Solidity
function removeClaimTopic(
uint256 _claimTopic
) external;
```

## getClaimTopics

Get the trusted claim topics for the security token  
Returns the array of trusted claim topics

```javascript Solidity
function getClaimTopics() external view returns (uint256[] memory);
```

## transferOwnershipOnClaimTopicsRegistryContract

Transfers the Ownership of ClaimTopics to a new Owner.  
Only the owner of the smart contract can call this function  
parameter 1 : `_newOwner` The new owner of this contract.

```javascript Solidity
function transferOwnershipOnClaimTopicsRegistryContract(
address _newOwner
) external;
```