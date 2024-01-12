# Roles and permissions

The TREX protocol, in its basic form distinguishes 2 different roles at the smart contract level, the owner of the smart contract and (on Token and Identity Registry) the agent(s). The owner of the contract is granted the rights to initialize the setup of the token, e.g. setting the links between contracts, setting the rules of transfers and restrictions applicable to transfers while the agents are meant to administrate the token on a day-to-day basis, by calling admin functions when necessary, such as minting/burning functions, recovery function, etc.

# Owner Role

The Owner Role is responsible for the core management of contracts, it is an administrator role with the capacity to modify the contracts settings as well as the rules of compliance, the Owner is also responsible to delegate permissions to Agent wallets by assigning the Agent Role to them.  
Hereunder, the list of functions under Owner Role's responsibility :

| Type of function             | functions                                                                                                                                                                                                                                                                                                                                        |
| :--------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Token Information Management | setName, setSymbol, setOnchainID                                                                                                                                                                                                                                                                                                                 |
| Registries Settings          | setClaimTopicsRegistry, setTrustedIssuersRegistry, setIdentityRegistry, setIdentityRegistryStorage                                                                                                                                                                                                                                               |
| Compliance Settings          | setCompliance                                                                                                                                                                                                                                                                                                                                    |
| Compliance Management        | Custom compliance functions depending on the compliance features, e.g. setDailyLimit, setMonthlyLimit, setAuthorizedCountry, etc.                                                                                                                                                                                                                |
| Claim Registry Management    | addClaimTopic, removeClaimTopic                                                                                                                                                                                                                                                                                                                  |
| Issuers Registry Management  | addTrustedIssuer, removeTrustedIssuer, updateIssuerClaimTopics                                                                                                                                                                                                                                                                                   |
| Roles Management             | transferOwnershipOnTokenContract, transferOwnershipOnIdentityRegistryContract, transferOwnershipOnComplianceContract, transferOwnershipOnClaimTopicsRegistryContract, transferOwnershipOnIssuersRegistryContract, addAgentOnTokenContract, removeAgentOnTokenContract, addAgentOnIdentityRegistryContract, removeAgentOnIdentityRegistryContract |

# Agent Role

The Agent Role is responsible for the operational management of contracts, Agents are able to perform all operational tasks such as minting tokens, burning tokens, whitelisting investors, etc.  
Hereunder, the list of functions under Agent Role's responsibility :

| Type of Function      | functions                                                                                                                                                 |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Supply modification   | Mint, burn, batchMint, batchBurn                                                                                                                          |
| Transfer restrictions | Pause, unPause, setAddressFrozen, batchSetAddressFrozen, freezePartialTokens, unfreezePartialTokens, batchFreezePartialTokens, batchUnfreezePartialTokens |
| Transaction           | forcedTransfer, batchForcedtransfer                                                                                                                       |
| Token recovery        | recoveryAddress                                                                                                                                           |
| Whitelisting          | registerIdentity, updateIdentity, updateCountry, deleteIdentity                                                                                           |