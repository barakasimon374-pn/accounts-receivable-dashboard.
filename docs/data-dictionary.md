# Data Dictionary

Update this page so it matches the final semantic model. Do not include confidential source-system details.

## Fact table: Invoices

| Field | Description | Example |
| --- | --- | --- |
| Invoice ID | Anonymised invoice identifier. | INV-10001 |
| CustomerID | Anonymised customer key. | CUST-001 |
| CustomerName | Anonymised customer display name. | ABC Traders Ltd |
| Invoice Date | Date the invoice was raised. | 2026-01-15 |
| Due Date | Contractual payment due date. | 2026-02-14 |
| Paid Date | Date payment was received, if paid. | 2026-02-10 |
| OutstandingBalance | Remaining unpaid invoice amount. | 4,250.00 |
| InvoiceAmount | Original invoice amount. | 8,500.00 |
| Days Past Due | Days elapsed after due date, not below zero. | 17 |
| Aging Bucket | Current or overdue aging band. | 1-30 Days |

## Dimensions

| Table | Purpose |
| --- | --- |
| Date | Enables month, quarter, year, and trend analysis. |
| Customer | Describes customer, segment, region, and account owner. |
| Collector | Identifies the collections owner, if applicable. |

## Fact table: payments

| Field | Description | Example |
| --- | --- | --- |
| PaymentID | Anonymised payment identifier. | PAY-10001 |
| InvoiceID | Related invoice identifier. | INV-10001 |
| PaymentDate | Date payment was received. | 2026-02-10 |
| PaymentAmount | Amount received. | 4,250.00 |
| PaymentMethod | Payment channel. | Bank Transfer |

## Aging-bucket logic

| Bucket | Days past due |
| --- | --- |
| Current | 0 or fewer days |
| 1–30 | 1 to 30 days |
| 31–60 | 31 to 60 days |
| 61–90 | 61 to 90 days |
| 90+ | More than 90 days |
