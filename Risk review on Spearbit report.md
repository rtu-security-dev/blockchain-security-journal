##10.07.2026

Finding: 5.1.1 Incorrect next scaled variable debt update in liquidations leads to wrong interest rates

Source: Spearbit - Aave Aptos V3.1-3.3 Core Upgrades Security Review

Reference Link: https://github.com/spearbit/portfolio/blob/master/pdfs/Avara-Aptos-V3.1-V3.3-Core-Spearbit-Security-Review.pdf 

Severity: High


Summary:
The program should update the debt token total supply by making it the next scaled variable “next_scaled_variable_debt variable” after liquitating or when “liquidation_logic::burn_debt_tokens” is called. 
But the debt token total supply is updated to “next_scaled_variable_ debt “ instead. 
The correct borrow index is in RAY (1e27) while the wrong index used is in debt token units ( 6-8 token decimals). 
This causes the interest rates in the proceeding functions to update incorrectly. 
Until there's a new interest update, the borrowers pay less interest causing the suppliers to earn less. 

Note: 
RAY - a number that uses 27 decimal places (1 x 10 to the power 27), used in precise calculations.
Debt token - numbers that use 6-8 decimal places (1 x 10 the power 6 to 1 x 10 to the power 8).

Severity Justification: The risk is high because it affects the borrowers who buy with low interest and the supplier earns less. 

Takeaway: The order for liquidation updates must be correct or else a small error in one variable causes the rest of the functions to update incorrectly. 

