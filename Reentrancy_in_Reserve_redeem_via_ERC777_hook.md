#Daily Readings 

##11.05.2026

-**Finding:** [M-07] Attacker can steal RToken holders' funds by performing reentrancy attack during `redeem()` function token transfers
Reserve (Reserve, Code4rena, 2023)
-**Source:** Solodit
-**Reference link:** https://solodit.cyfrin.io/issues/m-07-attacker-can-steal-rtoken-holders-funds-by-performing-reentrancy-attack-during-redeem-function-token-transfers-code4rena-reserve-reserve-git
-**Summary:** 
The user holds an RToken in the Reserve protocol. When the redeem(amount) is called, the token is burnt and the share of all backing assets are returned. During the transfers, the function is in an inconsistent state because the transfers are happening before the function ends. Tokens like ERC777 or tokens with hooks/callbacks can execute code during transfers so once the token is sent the attackers code call back the function before it ends, thus confusing it. This is called reentrancy. The attacker can withdraw more than their fair share or steal funds through "excess collateral". This can be fixed by adding a reentrancy guard (avoids entering the function again back to back) and update states before sending transfers. 

-**Takeaway:**

Add reentrancy guards and make sure functions update all states before an external call.    