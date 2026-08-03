##03.08.2026

Finding: Rounding errors cause unfair cost distributions

Source: Solodit

Reference Link: https://solodit.cyfrin.io/issues/rounding-error-accumulation-in-partial-order-fills-leads-to-unfair-cost-distribution-cyfrin-none-deriverse-dex-markdown 

Severity: Medium


Summary:
  When the order is filled multiple times partially, the “sum” field is affected due to the rounding errors in trade_sum(). 
  Due to the vulnerability the last trader ends up paying more than the traded amount. 
  During order creation, the total currency is calculated in trade_sum() where a floating point multiplication with rounded division factor (rdf) is performed (rounded to i64) and stored in order.sum.

  The root causes of the vulnerability:

  When “let rdf = 1f64 / df;” where df are powers of 10 the resulting rdf will be much smaller.
  If rdf was a decimal fraction, multiplying with it causes a fraction which can not be stored (i64). 
  So instead of storing a fraction, it stores only the whole number.  

  During a partial fill, the implementation recalculates the value using trade_sum but due to the vulnerability it stores only the whole number ( if its 19.9 → 19 ). 
  When the order is finally full, the order.sum value and the trade_sum() value (decimal value) are not equal, it contains all the rounding errors from the previous fills. 
  
Note:
  Floating point multiplication - multiplication between decimals.
  i64 - stores 64-bit signed integers, only stores whole numbers 


Severity Justification: 
  Rounding errors are present when orders are filled multiple times partially only. 
  But the final trader receives a value more than intended due to the rounding errors causing unfair cost distributions. 

Takeaway:  
  Avoid using floating-point calculation for financial purposes as it may cause rounding errors. 
