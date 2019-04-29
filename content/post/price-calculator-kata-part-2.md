---
title: "Price Calculator Kata (Part 2)"
date: 2019-04-28T17:40:24-04:00
draft: false
tags:  ["programming", "kata"]
---

I scroll down and read the next requirement to implement...Discount. Hmm, I think I can do this easily. Let's see.

![Knock on Wood](/images/knock-on-wood.png)

## Jinx, no take backs
Let's do the easy part first. I modfied my PriceResult class to take a DiscountRatePercent and then to calculate the discount in the total. Add a test to verify and boom, done. Easy peasy. I added another test to check that discount and tax were working together just to make sure.

## Interfaces
Adding the new interfaces was a challenge. First, I realized I had a small mistake from the last part. After calling ForProduct(x) you should be able to see the WithTaxRate, WithDiscountRate, and GetResult because I think you should be able to call GetResult immediatly if you want. But my ITaxRate interface did not allow that. After [looking at this tutorial](https://scottlilly.com/how-to-create-a-fluent-interface-in-c/) I finally just bit the bullet and took his advice and made a grammar matrix like he did.

![My Grammar Matrix](/images/price-calculator-grammar-matrix.jpg)

With that I realized my IProductResult didn't really make sense and I really needed to modify my existing interfaces to include a GetResult method and a new ITaxOrDiscountRate to include all options. The amazing thing was, after I changed all the interfaces and updated my price calculator, my existing console app still worked! This makes me think I should add tests for the api structure but I'm concerned about those tests being brittle right now as I'm still desiging it.

So overall, not too bad. My commit was a little messier than it had to be due to me remapping the interfaces. But it's very readable and the [Roslyn Code Metrics extension](https://github.com/elishalom/netcodemetrics) I'm using is still only reporting a max cyclomatic complexity of 2. So overall, I'm feeling pretty good.

I thought I had my head wrapped around it but after looking at a different tutoria

You can see the code at this point on [my Github.](https://github.com/clintdavis77/price-calculator-kata/tree/78668751196394887f056a71bc7fe691f713fe09)