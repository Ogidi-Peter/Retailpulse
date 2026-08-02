1. **Null** Values are found in unit_price and customer age

2. There are 270 duplicate values

3. There are two columns named card and also a column of the same name one written in **Capital** case and the other in **smaller**  case

4. The messiest part of this code was when I was converting values in unit_price to floating values some of the values had a **'₦'** symbol I had to take note of this when I was writing the function **is_str**

5. My take: since customer_age isn't central to a sales-performance analysis (unlike unit_price, which is core to revenue), I'd lean toward Option B — don't throw away 3,000 real transactions over a demographic field you may not even use heavily yet. But defend whichever you pick in your report.