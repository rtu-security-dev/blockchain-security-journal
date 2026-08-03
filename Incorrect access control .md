##03.08.2026

Finding: Incorrect access control 

Source: Solodit

Reference Link: https://solodit.cyfrin.io/issues/deliveryplacesettleasktaker-has-incorrect-access-control-codehawks-tadle-git 

Severity: High


Summary: 
  In the settleAskTaker a stock owner can transfer points to the buyer, thus completing the transaction. 
  As per the rule, only the stock owner can call this function. 
  However in the implementation, it checks whether the caller is the offer authority instead of the stock owner to call the function. 
  This causes the stock owner to not finalise the transaction and the offer owner might mistakenly call the function and lose points instead of acquiring it.

Severity Justification: 
  Interruption to the flow of operations and loss of integrity among the offer and stock authority

Takeaway:  
  Add proper check points to the correct authority

