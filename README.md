<h1>📊 Inventory Demand & Availability KPI Analysis (Power BI)</h1>

<p>
This repository contains an <b>end-to-end Power BI analytics project</b> focused on
analyzing inventory demand, availability, shortages, profit, and loss using
SQL Server and DAX measures.
</p>

<hr/>

<h2>🎯 Objectives</h2>

<p>The goal of this project is to analyze inventory performance using the following KPIs:</p>

<h3>KPI Page 1</h3>
<ul>
  <li>Average Demand per Day</li>
  <li>Average Availability per Day</li>
  <li>Total Supply Shortage</li>
</ul>

<h3>KPI Page 2</h3>
<ul>
  <li>Total Loss</li>
  <li>Total Profit</li>
  <li>Average Daily Loss</li>
</ul>

<h3>Filters Applied</h3>
<ul>
  <li>Date Filter</li>
  <li>Product Filter</li>
</ul>

<hr/>

<h2>📂 Repository Structure</h2>

<ul>
  <li><b>Power BI Reports</b>
    <ul>
      <li>Test Environment Report (.pdf)</li>
      <li>Production Environment Report (.pdf)</li>
    </ul>
  </li>

  <li><b>Datasets</b>
    <ul>
      <li>
        Test Environment
        <ul>
          <li>Inventory Dataset (99 rows)</li>
          <li>Products Dataset (10 rows)</li>
        </ul>
      </li>
      <li>
        Production Environment
        <ul>
          <li>Inventory Dataset (1043 rows)</li>
          <li>Products Dataset (22 rows)</li>
        </ul>
      </li>
    </ul>
  </li>

  <li><b>KPI Images</b>
    <ul>
      <li>KPI Page 1 – Test Environment</li>
      <li>KPI Page 2 – Test Environment</li>
      <li>KPI Page 1 – Production Environment</li>
      <li>KPI Page 2 – Production Environment</li>
    </ul>
  </li>
</ul>

<hr/>

<h2>🛠️ Data Processing & Cleaning (SQL Server)</h2>

<p>
The datasets were loaded into <b>SQL Server Management Studio (SSMS)</b>.
Data cleaning and integration were performed before connecting to Power BI.
</p>

<h3>Table Integration</h3>

<p>
Inventory and product datasets were combined into a single table using the following SQL query:
</p>

<pre>
SELECT * INTO new_table FROM
(
  SELECT
    a.product_id AS Product_ID,
    a.Order_Date_DD_MM_YYYY,
    a.demand AS Demand,
    a.availability AS Availability,
    b.product_name,
    b.unit_price
  FROM ProdEnvInventoryDataset AS a
  LEFT JOIN ProductsProd AS b
    ON a.product_id = b.product_id
) x;
</pre>

<p>
The same logic was applied for both <b>Test Environment</b> and <b>Production Environment</b> datasets.
</p>

<hr/>

<h2>🔍 Data Quality Fix</h2>

<p>
During data validation, inconsistencies were identified in the Production dataset:
</p>

<ul>
  <li><b>Product ID 21</b> mapped incorrectly → corrected to <b>7</b></li>
  <li><b>Product ID 22</b> mapped incorrectly → corrected to <b>11</b></li>
</ul>

<p>
These corrections were made directly in SSMS before refreshing Power BI reports.
</p>

<hr/>

<h2>📐 DAX Measures Created</h2>

<h4>Total Number of Days</h4>
<pre>
Total Number of Days =
DISTINCTCOUNT('Demand/Availability'[Order_Date_DD_MM_YYYY].[Date])
</pre>

<h4>Total Demand</h4>
<pre>
Total Demand =
SUM('Demand/Availability'[Demand])
</pre>

<h4>Total Availability</h4>
<pre>
Total Availability =
SUM('Demand/Availability'[Availability])
</pre>

<h4>Average Demand per Day</h4>
<pre>
Average Demand per Day =
DIVIDE([Total Demand], [Total Number of Days])
</pre>

<h4>Average Availability per Day</h4>
<pre>
Average Availability per Day =
DIVIDE([Total Availability], [Total Number of Days])
</pre>

<h4>Total Supply Shortage</h4>
<pre>
Total Supply Shortage =
[Total Demand] - [Total Availability]
</pre>

<h4>Total Profit</h4>
<pre>
Total Profit =
SUMX(
  FILTER(
    'Demand/Availability',
    'Demand/Availability'[Loss/Profit] > 0
  ),
  'Demand/Availability'[Loss/Profit] *
  'Demand/Availability'[unit_price]
)
</pre>

<h4>Average Loss per Day</h4>
<pre>
Average Loss per Day =
DIVIDE([Total Loss], [Total Number of Days])
</pre>

<hr/>

<h2>📸 KPI Dashboard Screenshots</h2>

<h3>Test Environment</h3>

<h4>KPI Page 1</h4>
<img width="1608" height="735" alt="KPI 1 test_env" src="https://github.com/user-attachments/assets/27070b55-8411-45a4-ab35-46c81ae34b5b" />


<h4>KPI Page 2</h4>
<img width="1584" height="709" alt="KPI 2 test_env" src="https://github.com/user-attachments/assets/74c7b887-322f-4e7e-b3a0-46f6f0cfccdc" />

<h3>Production Environment</h3>

<h4>KPI Page 1</h4>
<img width="1669" height="726" alt="KPI 1 Prod" src="https://github.com/user-attachments/assets/6c5f9ef0-85f9-4dec-bfeb-47259fc5e06f" />


<h4>KPI Page 2</h4>
<img width="1678" height="724" alt="KPI 2 Prod" src="https://github.com/user-attachments/assets/2d99104d-d4c3-4a21-a680-f754bfb9f0a0" />


<hr/>

<h2>🚀 Tools & Technologies Used</h2>

<ul>
  <li>Power BI</li>
  <li>SQL Server Management Studio (SSMS)</li>
  <li>DAX</li>
  <li>Data Modeling & KPI Analysis</li>
</ul>

<hr/>

<h2>📌 Conclusion</h2>

<p>
This project demonstrates a complete data analytics workflow:
from raw dataset ingestion and cleaning in SQL Server
to KPI-driven visualization and insights in Power BI,
across both Test and Production environments.
</p>

<p>
The dashboards provide actionable insights into demand trends,
availability gaps, supply shortages, and financial performance.
</p>
