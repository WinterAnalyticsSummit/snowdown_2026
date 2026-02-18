# snowdown_2026

<h1>❄️ The Great Data SnowDown</h1>
<h2>Dataset Documentation – Winter Season 2024–2025</h2>

<hr />

<h2>1. Overview</h2>
<p>
  This dataset contains operational, transactional, and customer activity data from a ski resort during the
  <strong>2024–2025 winter season</strong>.
</p>

<p>The objective of this dataset is to analyze:</p>
<ul>
  <li>Customer behavior</li>
  <li>Membership value and profitability</li>
  <li>Discount campaign impact</li>
  <li>Lift utilization patterns</li>
  <li>Revenue performance across rentals, lift tickets, and cafés</li>
</ul>

<p>
  The dataset includes both <strong>financial transaction tables</strong> and a
  <strong>non-financial lift usage log</strong>.
</p>

<p>The resort operates seasonally from:</p>
<blockquote>
  <p><strong>October 1st through March 31st</strong></p>
</blockquote>

<p>All data in this competition falls within that operating window for the 2024–2025 winter season.</p>

<hr />

<h2>2. Membership Program</h2>
<p>Customers may purchase a <strong>Season Membership (Season Pass)</strong>.</p>

<h3>Membership Details</h3>
<ul>
  <li><strong>Cost:</strong> $2,000 per season</li>
  <li>
    <strong>Benefits:</strong>
    <ul>
      <li>Unlimited lift access (no per-ride charge)</li>
      <li>
        15% discount on:
        <ul>
          <li>Equipment rentals</li>
          <li>Café purchases</li>
        </ul>
      </li>
    </ul>
  </li>
</ul>

<h3>Important Rule</h3>
<ul>
  <li>A member's <code>member_id</code> is the same as their <code>customer_id.</code></li>
  <li>Customer IDs that begin with "M" are members.</li>
  <li>Customer IDs that begin with "C" are non-members.</li>
  <li>Only customers who purchased a season pass appear in the <code>members</code> table.</li>
</ul>

<hr />

<h2>3. Discount Campaigns</h2>
<p>The resort offers limited-time promotional discounts on lift tickets:</p>

<table>
  <thead>
    <tr>
      <th>Promotion Code</th>
      <th>Description</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>WELCOME50</code></td>
      <td>First week the resort is open</td>
      <td>50% off</td>
    </tr>
    <tr>
      <td><code>MLK30</code></td>
      <td>Martin Luther King Jr. Day</td>
      <td>30% off</td>
    </tr>
    <tr>
      <td><code>NYE20</code></td>
      <td>New Year’s Eve</td>
      <td>20% off</td>
    </tr>
    <tr>
      <td><code>PRESIDENT25</code></td>
      <td>Presidents Day</td>
      <td>25% off</td>
    </tr>
  </tbody>
</table>

<p>
  <strong>Important:</strong> All discounts are already reflected in <code>net_price</code> (i.e., the stored value
  represents the final amount paid after the discount is applied).
</p>

<hr />

<h2>4. Data Tables</h2>

<h3>4.1 Table: <code>members</code></h3>
<p>Contains customers who purchased a season pass.</p>

<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>member_id</code></td>
      <td>Unique member identifier (same as customer_id)</td>
    </tr>
    <tr>
      <td><code>customer_id</code></td>
      <td>Unique customer identifier</td>
    </tr>
    <tr>
      <td><code>first_name</code></td>
      <td>Customer first name</td>
    </tr>
    <tr>
      <td><code>last_name</code></td>
      <td>Customer last name</td>
    </tr>
    <tr>
      <td><code>member_since</code></td>
      <td>Date membership became active</td>
    </tr>
  </tbody>
</table>

<hr />

<h3>4.2 Table: <code>rental_transactions</code></h3>
<p>Contains ski equipment rental transactions.</p>

<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>transaction_id</code></td>
      <td>Unique transaction identifier</td>
    </tr>
    <tr>
      <td><code>item_id</code></td>
      <td>Rental item identifier</td>
    </tr>
    <tr>
      <td><code>customer_id</code></td>
      <td>Customer renting equipment</td>
    </tr>
    <tr>
      <td><code>rental_item</code></td>
      <td>Type of item rented (e.g., skis, snowboard, helmet)</td>
    </tr>
    <tr>
      <td><code>net_price</code></td>
      <td>Final price paid after discount</td>
    </tr>
    <tr>
      <td><code>date_time_out</code></td>
      <td>Date and time rental began</td>
    </tr>
	<tr>
      <td><code>date_time_in</code></td>
      <td>Date and time rental ended</td>
    </tr>
  </tbody>
</table>

<h4>Business Rules</h4>
<ul>
  <li>Members receive <strong>15% off rentals</strong>.</li>
  <li>Non-members pay full price.</li>
  <li><code>net_price</code> reflects the final amount paid after discounts.</li>
  <li>Rentals occur only during the seasonal window (Oct 1 – Mar 31).</li>
</ul>

<hr />

<h3>4.3 Table: <code>lift_ticket_transactions</code></h3>
<p>Contains lift ticket purchase transactions.</p>

<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>date</code></td>
      <td>Date of transaction</td>
    </tr>
    <tr>
      <td><code>customer_id</code></td>
      <td>Customer purchasing lift access</td>
    </tr>
	<tr>
      <td><code>ticket_price</code></td>
      <td>Price of ticket before day pass lift ticket discounts are applied</td>
    </tr>
	<tr>
      <td><code>discount_code</code></td>
      <td>Promotional code</td>
    </tr>
	<tr>
      <td><code>discount_pct</code></td>
      <td>Percent of discount</td>
    </tr>
    <tr>
      <td><code>net_price</code></td>
      <td>Final price paid after discount (if stored)</td>
    </tr>
  </tbody>
</table>

<h4>Business Rules</h4>
<ul>
  <li>Members pay <strong>$0 per lift ride</strong> (included in membership).</li>
  <li>Non-members pay per lift ticket.</li>
  <li>Promotional discount codes may apply.</li>
  <li><code>net_price</code> reflects the final discounted price.</li>
  <li>Resort operates October 1st – March 31st.</li>
</ul>

<hr />

<h3>4.4 Table: <code>cafe_transactions</code></h3>
<p>Contains food and beverage purchase transactions.</p>

<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>cafe_location</code></td>
      <td>Café location</td>
    </tr>
    <tr>
      <td><code>transaction_id</code></td>
      <td>Unique café transaction ID</td>
    </tr>
    <tr>
      <td><code>date_time</code></td>
      <td>Transaction timestamp</td>
    </tr>
    <tr>
      <td><code>customer_id</code></td>
      <td>Customer making purchase</td>
    </tr>
    <tr>
      <td><code>item</code></td>
      <td>Product purchased</td>
    </tr>
    <tr>
      <td><code>item_quantity</code></td>
      <td>Quantity purchased</td>
    </tr>
    <tr>
      <td><code>net_price</code></td>
      <td>Final price after discount</td>
    </tr>
  </tbody>
</table>

<h4>Café Locations</h4>
<ul>
  <li>Icee</li>
  <li>Slushie</li>
  <li>Slurpie</li>
</ul>

<h4>Business Rules</h4>
<ul>
  <li>Members receive <strong>15% off café purchases</strong>.</li>
  <li>Non-members pay full price.</li>
  <li><code>net_price</code> reflects final payment after discount.</li>
</ul>

<hr />

<h3>4.5 Table: <code>lift_usage</code></h3>
<p><strong>⚠️ This is NOT a transaction table.</strong></p>
<p>It records actual lift usage events (operational activity).</p>

<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>lift_usage_id</code></td>
      <td>Unique lift usage identifier</td>
    </tr>
    <tr>
      <td><code>customer_id</code></td>
      <td>Customer using lift</td>
    </tr>
    <tr>
      <td><code>ticket_type</code></td>
      <td>Type of lift access (e.g., day pass, member)</td>
    </tr>
    <tr>
      <td><code>usage_datetime</code></td>
      <td>Date and time of lift scan</td>
    </tr>
    <tr>
      <td><code>lift_zone</code></td>
      <td>Lift or zone accessed</td>
    </tr>
  </tbody>
</table>

<h4>Important Distinction</h4>
<ul>
  <li>This table does <strong>not</strong> represent revenue.</li>
  <li>It tracks operational activity (how often lifts are used).</li>
  <li>Members may have high lift usage but generate no per-ride revenue.</li>
</ul>

<hr />

<h2>5. Table Relationships</h2>
<p><code>members.customer_id</code> joins with:</p>
<ul>
  <li><code>rental_transactions.customer_id</code></li>
  <li><code>lift_ticket_transactions.customer_id</code></li>
  <li><code>cafe_transactions.customer_id</code></li>
  <li><code>lift_usage.customer_id</code></li>
</ul>
<p>A customer is considered a <strong>member</strong> if they exist in the <code>members</code> table.</p>

<hr />

<h2>6. Revenue Model Summary</h2>

<h3>Members</h3>
<p><strong>Revenue Sources:</strong></p>
<ul>
  <li>$2,000 fixed membership fee</li>
  <li>Discounted rental spending (15% off retail price)</li>
  <li>Discounted café spending (15% off retail price)</li>
  <li>No lift ticket revenue</li>
</ul>

<h3>Non-Members</h3>
<p><strong>Revenue Sources:</strong></p>
<ul>
  <li>Full-price lift tickets (less promotional discounts)</li>
  <li>Full-price rentals</li>
  <li>Full-price café purchases</li>
  <li>No membership fee</li>
</ul>

<hr />

<h2>7. Key Considerations</h2>
<ul>
  <li>Lift usage does <strong>not</strong> equal lift revenue.</li>
  <li>Discounts are already reflected in <code>net_price</code>.</li>
  <li>Membership creates upfront revenue but reduces per-transaction revenue.</li>
  <li>Promotional campaigns may significantly impact short-term lift revenue.</li>
  <li>All analysis must fall within the October 1 – March 31 operating season.</li>
</ul>

<hr />

<p><strong>End of Documentation</strong><br />
The Great Data SnowDown – Winter Season 2024–2025</p>
