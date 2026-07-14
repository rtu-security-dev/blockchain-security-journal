##14.07.2026

Finding: Infinite approvals

Source: Solodit

Reference Link: https://solodit.cyfrin.io/issues/h-5-attacker-can-drain-stoplimit-contract-funds-through-bracket-contract-because-it-gives-typeuint256max-allowance-to-bracket-contract-for-input-token-in-performupkeep-function-sherlock-okus-new-order-types-contract-contest-git

Severity: High


Summary: 

  The performUpkeep:StopLimit function allows unlimited input tokens for the Bracket contract. 
  Inside this contract, the fillStopLimitOrder function can transfer input tokens to itself. 
  The attacker first checks which tokens have unlimited approvals on the Bracket contract in order to transfer tokens from StopLimit contract. 
  Then they create an executable order in the Bracket contract, the order is executed by calling performUpkeep::Bracket function. 

Severity Justification: 

  Attackers are able to drain all contract funds on StopLimit contracts.

Takeaway: 

  1. Unless the spender is trustworthy, ‘type(uint256).max’ should never be approved
