---
layout: post
title:  "Why Value Averaging (Probably) Doesn't Work"
date:   2022-12-30
tag: technical
---

[Value averaging](https://en.wikipedia.org/wiki/Value_averaging) (VA) is a proposed 
improvement over 
[dollar cost averaging](https://en.wikipedia.org/wiki/Dollar_cost_averaging) (DCA).
Contrary to DCA, which accumulates a fixed *cost* each period, regardless of the 
underlying market price, VA attempts to accumulate a fixed *value* each period. In 
practice this means VA accumulates more shares when the market price is lower than some 
target and accumulates less, or even sells off, shares when the price is higher.

VA is both intuitively and theoretically, a very appealing investment strategy. It 
attempts to implement the old adage of "buy low, sell high" in a very passive and 
mechanical manner. Unfortunately, in order to outperform other passive investment 
strategies like DCA, it requires knowing how to set a portfolio target for each period.

Setting this target is exactly price forecasting. If we had a method to reliably 
forecast prices even $$50.1\%$$ of the time, we would become extremely wealthy without 
the need to resort to VA or DCA. Therefore in practice, this target will either be too 
high causing us to  waste money by purchasing overpriced shares, or too low causing us 
to miss out on potential upside. 

**Avoiding snake oil**: Many blogs and books which tout the dominance of VA over DCA set 
very conservative price targets, such as the total amount of capital invested. In such 
cases, VA will have a higher *rate* of return compared to DCA, but much lower *total* 
return, which is ultimately what we care about.
