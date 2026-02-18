# snowdown_2026

The Great Data SnowDown
Dataset Documentation – Winter Season 2024–2025

1. Overview
This dataset contains operational, transactional, and customer activity data from a ski resort for the 2024–2025 winter season.
The objective of this dataset is to analyze:
Customer behavior
Membership value and profitability
Discount campaign impact
Lift utilization patterns
Revenue performance across rentals, lift tickets, and cafés
The dataset includes both financial transaction tables and a non-financial lift usage log.
The resort operates seasonally from:
October 1st through March 31st
All data in this competition falls within that operating window for the 2024–2025 winter season.

2. Membership Program
Customers may purchase a Season Membership (Season Pass).
Membership Details
Cost: $2,000 per season
Benefits:
Unlimited lift access (no per-ride charge)
15% discount on:
Equipment rentals
Café purchases
Important Rule
member_id = customer_id
Every member is a customer.
Only customers who purchased a season pass appear in the members table.

4. Discount Campaigns
The resort offers limited-time promotional discounts on lift tickets:
Promotion Code
Description
Discount
WELCOME50
First week the resort is open
50% off
MLK30
Martin Luther King Jr. Day
30% off
NYE20
New Year’s Eve
20% off
PRESIDENT25
Presidents Day
25% off

All discounts are reflected in net_price (i.e., price after discount is applied).

5. Data Tables

5.1 Table: members
Contains customers who purchased a season pass.
Column Name
Description
member_id
Unique member identifier (same as customer_id)
customer_id
Unique customer identifier
first_name
Customer first name
last_name
Customer last name
member_since
Date membership became active







5.2 Table: rental_transactions
Contains ski equipment rental transactions.
Column Name
Description
transaction_id
Unique transaction identifier
item_id
Rental item identifier (Primary Key)
customer_id
Customer renting equipment
rental_item
Type of item rented (e.g., skis, snowboard, helmet)
net_price
Final price paid after discount
date_time_out
Date and time rental began

Business Rules
Members receive 15% off rentals.
Non-members pay full price.
net_price reflects the final amount paid after discounts.
The ski lift operates only during the seasonal window (Oct 1 – Mar 31).



5.3 Table: lift_ticket_transactions
Contains lift ticket purchase transactions.
Column Name
Description
transactions_id
Unique lift ticket transaction ID
item_id
Lift ticket identifier
customer_id
Customer purchasing lift access

Business Rules
Members pay $0 per lift ride (included in membership).
Non-members pay per lift ticket.
Promotional discount codes may apply.
net_price (if stored) reflects the discounted final price.
Resort operates October 1st – March 31st.






5.4 Table: cafe_transactions
Contains food and beverage purchase transactions.
Column Name
Description
cafe_location
Café location identifier
transaction_id
Unique café transaction ID
date_time
Transaction timestamp
customer_id
Customer making purchase
item
Product purchased
item_quantity
Quantity purchased
net_price
Final price after discount

Café Locations
There are 3 café locations:
Icee
Slushie
Slurpie
Business Rules
Members receive 15% off café purchases.
Non-members pay full price.
net_price reflects final payment after discount.
















\5.5 Table: lift_usage
This is NOT a transaction table.
It records actual lift usage events (occurrences).
Column Name
Description
lift_usage_id
Primary key
customer_id
Customer using lift
ticket_type
Type of lift access (e.g., day pass, member)
usage_datetime
Date and time of lift scan
lift_zone
Lift or zone accessed

Important Distinction
This table does not represent revenue.
It tracks operational activity (how often lifts are used).
Members may have high lift usage but generate no per-ride revenue.

6. Table Relationships
members.customer_id joins with:
rental_transactions.customer_id
lift_ticket_transactions.customer_id
cafe_transactions.customer_id
lift_usage.customer_id
A customer is considered a member if they exist in the members table.

7. Revenue Model Summary
Members
Revenue sources:
$2,000 fixed membership fee
15% of rental spending
15% of café spending
No lift ticket revenue
Non-Members
Revenue sources:
Full-price lift tickets (less promotional discounts)
Full-price rentals
Full-price café purchases
No membership fee

8. Analytical Opportunities
Participants may explore:
Member vs non-member profitability
Break-even analysis for membership
Impact of promotional campaigns
Lift utilization patterns by zone
Peak usage timing analysis
Café performance by location
Customer segmentation
Revenue forecasting
Operational load modeling using lift_usage

9. Key Considerations
Lift usage does not equal lift revenue.
Discounts are already reflected in net_price.
Membership creates upfront revenue but reduces per-transaction revenue.
Promotional campaigns may significantly impact short-term lift revenue.
All analysis must fall within the October 1 – March 31 operating season.

If you would like, I can now:
Create an ER diagram explanation
Add sample SQL joins and analytical queries
Create a competition-ready PDF version
Or simplify this into a 1-page executive summary
