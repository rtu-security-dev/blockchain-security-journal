##11.07.2026

Finding: Storage collision between proxy and implementation 

Source: Solodit

Reference Link: https://solodit.cyfrin.io/issues/p1-c02-storage-collision-on-policed-contract-openzeppelin-eco-contracts-audit-markdown 

Severity: High


Summary: 
  If the policy contract is the manager it can command the policed contracts to act according to their instructions inside the policed contracts state and storage space. 
  The policyCommand function in the policed contract is used by the managing policy only (done by onlyPolicy modifier) for instructions. 
  The policyCommand function is proxy and makes use of a simple implementation of delegatecall, due to this an attacker can overwrite critical state variables. 
  Mitigation can be found in “ OpenZeppelin SDK documentation on unstructured storage”.

Note: 

  1. Proxy means upgradable. 

  2. Delegatecall means run another contract as their own (with their own storage and state).

Severity Justification: 

  An attacker can overwrite the policed contract to follow the malicious contracts instructions instead of the policy as intended. 
  The system is compromised. 

Takeaway: 

  1. Never use delegatecall on functions that can not be controlled. 

  2. The storage layout of the logic code (inside policy) must not collide with the proxy (inside policied). 
