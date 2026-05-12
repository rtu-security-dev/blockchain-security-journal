#Daily Readings 

##12.05.2026

-**Finding:** Gas refund logic edge case (Obront, 2023) 

-**Source:** Twitter (@zachobront)

-**Summary:** 

Users are refunded for the gas they spent on some protocols. 
The refund system is calculated by adding the gas spent with fixed extra amount.
The fixed amount covers transaction overheads.
The concern by Obront is what if someone makes many refundable actions in one single transaction, the protocol will add refunds for each action instead of once.
The protocol pays more refunds than it was intended. 

-**Takeaway:**

For a transaction, do not add a fixed overhead per-call refund without confirming it can only be claimed once
