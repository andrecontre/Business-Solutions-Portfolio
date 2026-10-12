# Data Model - Halvorsen Industrial

Fictional B2B industrial manufacturer. This dashboard is based on a real-world project I delivered
for an industrial manufacturer. To protect confidentiality, **all data, names and branding are
fictional** and were generated with AI assistance for this project. No real company, customer or
figure is used. Currency: USD. Data cutoff: 2026-07-31.

## Tables (`/data`)

| Table | Grain | Key columns |
|---|---|---|
| DimSalesRep | 1 row per rep | SalesRepID, SalesRepName, Division, Region |
| DimCustomer | 1 row per customer | CustomerID, SalesRepID, CustomerType, Classification, PotentialClass, CVMStrategy |
| DimProduct | 1 row per material | ProductID, ProductGroup, BusinessUnit, MaterialCategory, UnitPrice |
| FactOrders | 1 row per order line | OrderID, OrderDate, CustomerID, ProductID, OrderAmount, DeliveredAmount, OpenAmount, ScheduledDeliveryDate, Status |
| FactSales | 1 row per shipment/invoice line | SaleID, SalesDate, CustomerID, ProductID, Quantity, SalesAmount |
| Plan | 1 row per rep per month | SalesRepID, Month (1st of month), TargetAmount |
| Visits | 1 row per customer contact | VisitID, VisitDate, CustomerID, VisitType |

The Calendar table is created in Power BI with DAX and marked as Date table.

Classification (VIP, A-F) ranks customers by trailing-12-month sales; PotentialClass is simulated.
CVMStrategy (Build, Maintain, Defend, Observe, Gain) is derived from classification vs. potential.

## Relationships (all many-to-one, single direction)

- FactSales / FactOrders / Visits -> DimCustomer (CustomerID)
- FactSales / FactOrders -> DimProduct (ProductID)
- DimCustomer -> DimSalesRep (SalesRepID)
- Plan -> DimSalesRep (SalesRepID)
- Calendar -> FactSales[SalesDate], FactOrders[OrderDate], Visits[VisitDate], Plan[Month]
  (inactive relationship + USERELATIONSHIP for FactOrders[ScheduledDeliveryDate])

Filter paths: `DimSalesRep -> DimCustomer -> facts` and `DimSalesRep -> Plan`.

**Design decision:** the sales rep is stored only on the customer (account owner), not repeated
in the fact tables. This keeps a single filter path and avoids ambiguous relationships. The
trade-off is that history is not preserved if a customer changes owner; in this dataset no
customer does.

All names are fictional and randomly generated; any resemblance to real companies is coincidental.
