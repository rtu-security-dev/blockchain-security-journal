06.07.2026

- Contract Reviewed: OpenZeppelin ERC20 contract

-Source: GitHub 

- Reference link: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol 
- Observations:
    
    1. Assumption: _balances mapping prevents double-spend
    
    The program first maps the _balances to the 'account'.
    In the _update private function, the code uses '_balances' mapping to check whether the senders account balance is more than the value and the value to be sent is immediately reduced from the senders balance. 
    Due to the update, a second attempt to transfer the same value will fail. 
    Afterwards the balance is updated in the receiver account.  

    2. Question: What happens if someone sends tokens to the contract address itself?
    
    The tokens will likely be stuck unless the contracts adds a function to transfer them out. 

    3.  Could a malicious token override the _update
    
    The function is 'virtual' so a child contract can inherit it. This contract is able to skip the balance check, call external contracts, transfer to another address. 
    If a contract accepts any token, we can not assume all will follow the normal ERC20 rules. 
