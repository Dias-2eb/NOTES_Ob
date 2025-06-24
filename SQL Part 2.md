## OLTP vs OLAP
![[Pasted image 20250623133104.png]]
![[Pasted image 20250623134330.png]]
![[Pasted image 20250623134343.png]]
![[Pasted image 20250623134401.png]]
## OLTP
OLTP systems are designed to allow transactions to be processed in real time and make it possible to manage and process operational data related to day-to-day business activities. They prioritize data integrity, concurrency control, and high-speed transaction execution. OLTP systems typically use a highly normalized data structure to optimize transactional operations, ensuring efficient data storage and retrieval for individual transactions.

Example: An e-commerce website uses OLTP to handle online orders, inventory management, and customer transactions. When a customer places an order, the system performs real-time validation, updates inventory levels, processes payment, and generates order confirmations. The focus is on rapid response and accurate data updates for each individual transaction.
## OLAP
OLAP is designed for complex data analysis and reporting. It focuses on providing fast and flexible access to large volumes of historical data for decision-making purposes. OLAP systems typically use a denormalized data structure, such as multidimensional cubes or star schemas, which allows for efficient data retrieval and analysis. OLAP tools enable users to perform advanced analytics, including aggregations, drill-downs, slicing and dicing, and data visualization.

Example: A retail company uses OLAP to analyze sales data over time, identify trends, perform market segmentation, and generate reports for sales forecasting and inventory management. Analysts can slice the data by product, region, and time period to gain insights into sales performance and make informed decisions.


## Data Warehouses
The data warehouse (DWH) plays a crucial role in connecting OLAP and OLTP systems. A DWH serves as a central repository that integrates data from various OLTP systems and other sources, transforming it into a structured and consistent format suitable for OLAP analysis.
A **DWH** is a subject-oriented, integrated, time-variant, and non-volatile collection of data that helps management make informed decisions.
![[Pasted image 20250623145925.png]]
![[Pasted image 20250623150124.png]]
**Subject-Oriented** - A DWH can be used to analyze a particular subject area—for example, "sales."
**Integrated** - A DWH integrates data from multiple data sources. For example, source A and source B may have different ways of identifying a product, but in a DWH, there will be only one way to identify a product.
**Time-Variant** - Historical data is kept in a DWH. For example, one can retrieve data from three months ago, six months ago, or even more than 12 months ago from a DWH. This contrasts with a transactions system, where often only the most recent data is kept. For example, a transaction system might hold a customer's most recent address, while a DWH might hold all addresses associated with a customer.
**Non-Volatile** - Once data is in a DWH, it will not change, so historical data in a DWH should never be altered.
![[Pasted image 20250623150138.png]]
![[Pasted image 20250623150150.png]]
![[Pasted image 20250623150711.png]]
## Normalized vs. Dimensional Data Storage
The **dimensional** approach—whose supporters are referred to as "Kimballites" and ascribe to Ralph Kimball's approach—states that a DWH should be modeled using a dimensional model/star schema.

According to the dimensional approach, transaction data is partitioned into either "facts," which are generally numeric transaction data, or "dimensions," the reference information that gives context to the facts. For example, a sales transaction can be broken up into facts, such as the number of products ordered and the price paid for the products, and into dimensions, such as order date, customer name, product number, order ship-to and bill-to locations, and the salesperson responsible for receiving the order.

![](https://elearn.epam.com/assets/courseware/v1/beedd850dfcbb2601397aaf66d3dbf69/asset-v1:RD_CIS+DE+ENG+type@asset+block/Databases_Topic8_006_3x.png)
![[Pasted image 20250623151017.png]]
In the normalized approach, data in a DWH is stored—to a certain degree—according to normalization rules. Tables are grouped together by subject areas that correspond to general categories of data (e.g., data on customers, products, finance, etc.). The normalized structure divides data into entities, creating several tables in a relational database. When applied in large enterprises, the result is dozens of tables that are linked together by a web of joins. Furthermore, each of the created entities is converted into separate physical tables when the database is implemented (Kimball, Ralph 2008).

![](https://elearn.epam.com/assets/courseware/v1/bb3ffda3d35741ddf5665c6b408ba596/asset-v1:RD_CIS+DE+ENG+type@asset+block/Databases_Topic8_007_3x.png)
![[Pasted image 20250623151107.png]]
![[Pasted image 20250623151201.png]]
## Window Fuctions
![[Pasted image 20250624152405.png]]
In the context of SQL, a **window function** is a powerful analytical tool that operates on a set of rows within a specified window or group. It allows calculations or aggregations to be performed over a specific subset of data and defined by a window frame while retaining the individual row-level details. Window functions make it possible to perform advanced analysis tasks such as ranking, calculating running totals, finding percentiles, identifying gaps or peaks, and much more.
![[Pasted image 20250624152511.png]]
The ROW_NUMBER function assigns a unique sequential number to each row in the result set. The numbers start from 1 and increment by 1 for each subsequent row. There are no gaps or ties in the sequence.
The RANK function assigns a unique rank to each row in the result set based on the values in a specific column. If two or more rows have the same values, they receive the same rank, and the **subsequent rank is skipped**. The ranks are not consecutive, and gaps may exist.
Similar to the RANK function, the DENSE_RANK function assigns a unique rank to each row in the result set. However, **it does not skip ranks for ties**. If two or more rows have the same values, they receive the same rank, and the subsequent rank continues without gaps.
![[Pasted image 20250624152554.png]]
![[Pasted image 20250624152607.png]]
##  Window Frames

![[Pasted image 20250624153433.png]]

ROWS frames are defined based on the number of rows within the window. They specify a fixed number of preceding or following rows relative to the current row. For example, you can define a ROWS frame as "3 PRECEDING" to include the three rows before the current row. ROWS frames are particularly useful when you want to include a fixed number of rows for calculations or comparisons.
RANGE frames are defined based on the values of the column(s) in the ORDER BY clause. They include rows whose values fall within a specified range relative to the value of the current row.  
The range can be defined using logical offsets such as "UNBOUNDED PRECEDING" or "CURRENT ROW. "For example, you can define a RANGE frame as "BETWEEN 10 PRECEDING AND 5 FOLLOWING" to include rows within a range of 10 rows before the current row and five rows after it based on the ORDER BY column. RANGE frames are commonly used when you want to perform calculations based on the values of column(s) rather than a fixed number of rows.

The **offset value** specifies the number of lines or groups to include before or after the current line, depending on the frame mode. In rows mode, the offset determines the fixed size of the frame, while in groups mode, it shifts the frame based on the related rows.
![[Pasted image 20250624154824.png]]
![[Pasted image 20250624154937.png]]
![[Pasted image 20250624155929.png]]

### 1. **ROWS mode**

Operates on the physical number of rows.

`SUM(salary) OVER (ORDER BY department ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)`

➡️ Includes exactly one row before and one row after the current row based on ordering.

---

### 2. **RANGE mode**

Operates on **value-based logical ranges**, **not row counts**. All rows with equal `ORDER BY` values are included.

`SUM(salary) OVER (ORDER BY department RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)`

➡️ Includes all rows with the same department value and all greater values (according to the `ORDER BY`).

- In `RANGE`, **ties (equal values)** are treated as a group.
    
- Cannot be used with multiple `ORDER BY` columns unless all are numeric or date types and support numeric distance.
    

---

### 3. **GROUPS mode** (PostgreSQL 11+, SQL:2011+)

Works like `RANGE`, but on **logical peer groups** (rows with same `ORDER BY` values), but instead of specifying value ranges, you specify group counts.
`SUM(salary) OVER (ORDER BY department GROUPS BETWEEN 1 PRECEDING AND 1 FOLLOWING)`

➡️ Includes the group before and after the current group of `department`.
![[Pasted image 20250624161423.png]]
![[Pasted image 20250624161823.png]]
![[Pasted image 20250624161950.png]]
![[Pasted image 20250624162032.png]]
![[Pasted image 20250624162118.png]]
![[Pasted image 20250624162904.png]]
![[Pasted image 20250624163300.png]]
![[Pasted image 20250624163350.png]]
NOTE: Last value faction returns only first value if window frame is not specified
