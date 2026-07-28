## 💡 KEY BUSINESS INSIGHTS

1. The South generated the highest sales revenue of any region and also recorded the longest shipping times. This creates a risk: the company's most valuable market is also experiencing the worst logistics performance. If shipping delays worsen, customer satisfaction in the highest-revenue region is the first thing to deteriorate.

2. Electronics drives revenue, but the category mix tells a more complex story.
Electronics was the top revenue-generating category, with Tablet identified as the single highest-revenue product. However, Rice was the highest-selling product by quantity — which means the company's volume leader and its revenue leader are in completely different categories. Pricing strategy and investment decisions need to treat these two dimensions separately, not as the same signal.

3. Discounts are not clearly driving proportional profit recovery.
The analysis of discount percentage against profit showed a significant divergence between the two figures. While discounts are being applied broadly, there is no clear evidence that higher discounts are generating the kind of volume uplift needed to compensate for the margin reduction. The current discounting approach appears to be reducing profitability without a commensurate return in customer acquisition or retention.

4. Customer loyalty is concentrated in the West region.
The West had the highest concentration of repeat purchase customers. Combined with the fact that Meera Kumar received the highest cumulative discount of any single customer, this raises a segmentation question: are the company's most loyal customers being appropriately rewarded, or is discount allocation happening randomly across the customer base regardless of loyalty or lifetime value?

5. Product returns are not driven by shipping time.
Contrary to what management might assume, the data showed no meaningful relationship between longer shipping times and higher product return rates. With 623 returned orders in the dataset, the causes of returns appear to lie elsewhere — likely in product quality, incorrect fulfillment, or expectation mismatch — rather than in delivery speed. This is an important finding because it redirects where operational improvement effort should go.

6. Customer satisfaction is average and flat.
The average customer satisfaction score across all transactions was 3.02 out of 5 — exactly at the midpoint. Returned products did not show meaningfully lower satisfaction scores, which suggests customer dissatisfaction is spread across the base rather than concentrated in a specific problem area like returns or delayed shipping. This makes it harder to fix with a single operational change and suggests a more systemic experience improvement is needed.

7. 2023 was the company's peak revenue year.
Among all years in the dataset, 2023 recorded the highest total revenue. Understanding what drove that peak — whether a specific product launch, regional expansion, marketing campaign, or macroeconomic factor — and whether 2024 maintained or declined from that level, should be a priority analytical question for management planning.

🎯 BUSINESS RECOMMENDATIONS

1. Fix the data infrastructure before making any major strategic decision.
The single most important finding from this project is that the company's operational data cannot currently be trusted without validation. Conflicting figures, type errors, impossible values (age = 999), and inconsistent records across sales channels mean that any strategic decision based on raw reports is being made on shaky ground. The immediate priority should be implementing a centralised data pipeline with validation rules, mandatory field formats, and automated anomaly detection — so that data quality is enforced at the point of entry rather than cleaned manually after the fact.

2. Investigate and address logistics performance in the South region.
The South is the company's highest-revenue region and its worst-performing logistics region simultaneously. This is a ticking clock. Conduct a carrier-by-carrier analysis of shipping times and costs in the South, identify which fulfillment centres are responsible for the longest delays, and either renegotiate carrier contracts or establish an additional regional fulfillment point. Given that shipping time was not found to drive returns, the risk here is specifically to customer satisfaction and repeat purchase behaviour rather than returns — but those are equally valuable outcomes to protect.

3. Build a structured discount policy anchored to customer lifetime value.
The current discounting approach shows no clear strategic logic — the data does not support the conclusion that discounts are being used as a deliberate tool for customer acquisition or retention. A tiered discount framework tied to the customer segments identified in the analysis (Bronze, Silver, Gold, Platinum) would ensure that the company's highest-value customers receive meaningful rewards, while margin-diluting discounts to low-value customers are reduced or eliminated. Meera Kumar receiving the highest single-customer discount is not itself a problem — but it becomes one if that level of discounting is happening without a corresponding LTV justification.

4. Investigate the root cause of product returns rather than shipping operations.
Since longer shipping times do not correlate with higher return rates, the 623 returned orders represent a product quality or fulfillment accuracy problem rather than a logistics one. Segment return data by product category, specific SKU, and fulfillment centre to identify whether specific products are systematically being returned, whether certain warehouses are picking incorrectly, or whether product descriptions are creating expectation gaps that drive returns post-delivery. This analysis should be the next SQL project built on top of this dataset.

5. Develop a customer retention programme anchored to the West region.
The West has the company's highest concentration of loyal, repeat-purchase customers. This is the natural starting point for a formal loyalty programme — begin with the customer base that is already demonstrating loyalty behaviour, reward it explicitly with a structured programme, and use the learning from that cohort to design retention interventions for other regions. The Platinum-tier customers identified in the segmentation analysis (Question 50) are the first target audience.

6. Review the Electronics category pricing strategy.
Electronics is the highest-revenue category but the analysis did not confirm it as the highest-margin category. Before continuing to invest marketing and inventory resources into Electronics, conduct a detailed margin analysis at the SKU level to understand whether revenue leadership in this category is translating into profit leadership. If it is not — if Electronics is high-revenue but low-margin relative to other categories — the investment allocation needs to be rebalanced toward higher-margin categories.

7. Establish monthly performance reviews using the dashboard as the standard reporting tool.
The interactive Excel dashboard built as part of this project should replace the manual, inconsistent Excel reports that management currently relies on. Schedule a monthly business review cadence using the dashboard as the single source of truth, with a standing agenda item for investigating any metric that has moved more than 10% from the prior month. This creates accountability for data quality (because anomalies become visible immediately) and ensures that analytical work translates into regular strategic conversations rather than one-off reports.
