# Nord-Mark-Supply-Chain
Interactive Power BI dashboard analyzing Nord Mark's supply chain: inventory stock outs, sales performance, and inventory movements.

An interactive **Power BI** dashboard that analyzes supply chain performance for Nord Mark, covering inventory health, sales, and stock movements. The report features a **custom landing page built with HTML** for a polished, app-like navigation experience.

## Project Objective
Help operations and commercial teams align inventory levels with demand, minimize stockouts and overstocking, and make data-driven replenishment decisions.
Key Views & Insights:Sales Analysis: Tracks 111K total units sold, 77.29 average inventory, overstock months and rates by product, and monthly sales-to-inventory comparisons.
Inventory Analysis: Monitors 219K inventory records and 3K stockout records (1.29% stockout rate), breaking down stockouts by location (Bergen, Trondheim, Oslo Sentrum, Online, Main DC) and month (with peaks in May and August), alongside sales and unit comparisons by product and location.
Inventory Movements: Covers 6K replenishment records, replenishment distribution by product and destination, and monthly breakdowns across movement types (ADJUSTMENT, REPLENISH, SALE).   

## 📊 Dashboard Pages
| Page | Description |
|------|-------------|
| **Home (Landing Page)** | Custom-designed landing page built using HTML, serving as the entry point and navigation hub of the report |
| **Inventory** | Stockout records by location and by month, with slicers and detailed breakdowns |
| **Sales** | Sales performance with KPI cards, pivot tables, and filters |
| **Inventory Movements** | Movement types across months, combined with sales and snapshot data |

## 🖼️ Screenshots
![Home](images/home.png)
![Inventory](images/inventory.png)
![Sales](images/sales.png)
![Inventory Movements](images/inventory-movements.png)

## 🛠️ Tools & Skills
- Power BI Desktop
- Data modeling (relationships, star schema)
- DAX measures
- Power Query (data cleaning and transformation)
- **HTML** (custom landing page via the HTML Content visual)
- Data visualization and dashboard design

## ✨ Highlights
- Custom HTML landing page that gives the report a web-style first impression

## 📁 Data Source

The data comes from a **SQL Server** database (`supply_chain`) organized using the **Medallion Architecture** (Bronze → Silver → Gold). The Power BI model connects to the **Gold layer**, which holds clean, analysis-ready fact tables.

### Data Layers
| Layer | Purpose | Tables |
|-------|---------|--------|
| **Bronze** | Raw ingested data | `bronze__inventory_movements__lite` |
| **Silver** | Cleaned and standardized data | `silver__sales_transactions__lite`, `silver__inventory_snapshots__lite`, `silver__inventory_movements__lite`, `silver__location_master__lite` |
| **Gold** | Business-ready fact tables used in the report | `gold__fact_sales__lite`, `gold__fact_inventory_snapshots__lite`, `gold__fact_inventory_movements__lite`, `gold__fact_inventory_exposure__lite` |

### Gold Layer Tables (used in Power BI)

| Table | Description | Key Columns |
|-------|-------------|-------------|
| `gold__fact_sales__lite` | Sales transactions | TransactionID, SalesDate, LocationID, ProductSKU, Quantity, UnitPrice, TotalRevenue |
| `gold__fact_inventory_snapshots__lite` | Daily on-hand stock levels per location and product | SnapshotDate, LocationID, ProductSKU, OnHandQuantity |
| `gold__fact_inventory_movements__lite` | Stock movements between locations | MovementID, MovementDate, MovementType, ProductSKU, FromLocationID, ToLocationID, Quantity |
| `gold__fact_inventory_exposure__lite` | Weekly aggregated view combining sales, stock, and movements | WeekStartDate, LocationID, ProductSKU, WeeklySalesQty, WeekEndOnHandQty, NetMovementQty |

### Notes
- Each fact table is joined through `LocationID` and `ProductSKU`.
- The raw sales data also includes a sales **channel** attribute in the Silver layer.
- The database backup (`supply_chain.bak`) can be restored using SQL Server Management Studio (SSMS).
