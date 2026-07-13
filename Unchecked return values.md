##13.07.2026

Finding: Unchecked return values

Source: Solodit

Reference Link: https://solodit.cyfrin.io/issues/h-5-anyone-can-steal-pool-shares-from-lender-group-if-no-revert-on-failure-tokens-are-used-sherlock-teller-finance-git 

Severity: High

Summary: 
  According to the README, the protocol assumes all tokens work with Uniswap V3 while supporting tokens from       previous audits. 
  The ZRX protocol inside LenderCommitmentGroup_Smart.sol fits all the conditions and can be used as principal token but it can be vulnerable to attacks since addPrincipleToCommitmentgroup() uses an outdated token transfer method. 
  The protocol ZRX returns false when the transfer fails but since the contract does not check the return value, the program acts as if the transfer is successful. 
  As a result, false internal accounts and minting pool shares are updated to attackers. 
  They can later use these fake shares for real tokens from other users. 

Note: 
  Principle token - main token used to transfer or deposit tokens. 

Severity Justification: 
  An attacker can get fake pool shares allowing them to withdraw funds affecting the integrity of the protocol. 

Takeaway: 
  1. There is no guarantee that ERC-20 token transfers will succeed.
  2. Check return values in functions. 
