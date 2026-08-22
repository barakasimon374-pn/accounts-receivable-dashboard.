# Rebuild the Accounts Receivable & Collections dashboard

This guide recreates the one-page layout shown in the project preview. It assumes two tables: `invoices` and `payments`.

## 1. Load and relate the data

1. Import `invoices` and `payments` into Power BI Desktop.
2. Set `InvoiceID` to **Text** in both tables.
3. Set invoice, due, and payment dates to **Date**.
4. Set money fields to **Fixed decimal number**.
5. Create a one-to-many relationship from `invoices[InvoiceID]` to `payments[InvoiceID]`, with single-direction filtering from invoices to payments.

## 2. Create calculated columns

In the `invoices` table, create these columns. The `TODAY()` reference gives a live aging position; for a static portfolio demonstration, replace it with a chosen report date.

```DAX
Days Past Due =
MAX ( 0, DATEDIFF ( invoices[DueDate], TODAY (), DAY ) )

Aging Bucket =
SWITCH (
    TRUE (),
    invoices[Days Past Due] = 0, "Current",
    invoices[Days Past Due] <= 30, "1-30 Days",
    invoices[Days Past Due] <= 60, "31-60 Days",
    invoices[Days Past Due] <= 90, "61-90 Days",
    "90+ Days"
)

Aging Bucket Sort =
SWITCH (
    invoices[Aging Bucket],
    "Current", 1,
    "1-30 Days", 2,
    "31-60 Days", 3,
    "61-90 Days", 4,
    "90+ Days", 5
)
```

Select `Aging Bucket`, then use **Sort by column** → `Aging Bucket Sort`.

## 3. Create measures

```DAX
Total Invoiced = SUM ( invoices[InvoiceAmount] )

Total Payments Received = SUM ( payments[PaymentAmount] )

Outstanding Receivables =
SUM ( invoices[OutstandingBalance] )

Collection Rate =
DIVIDE ( [Total Payments Received], [Total Invoiced], 0 )
```

Format the first three as currency with display units **Millions**, and `Collection Rate` as a percentage with two decimal places.

## 4. Build the report canvas

Create a 16:9 page titled **Accounts Receivable & Collections**. Use a clean white background and a single blue accent colour to match the preview.

| Position | Visual | Fields | Configuration |
| --- | --- | --- | --- |
| Top left | Slicer | `CustomerName` | List with checkboxes. |
| Top middle | Slicer | `InvoiceDate` | List or date selector. |
| Top right | Slicer | `PaymentMethod` | List with checkboxes. |
| Row 2 | Card × 4 | Four measures above | Titles: Total Invoiced, Total Payments Received, Outstanding Receivables, Collection Rate. |
| Middle left | Line chart | Axis: `InvoiceDate`; Values: `[Total Invoiced]` | Title: Invoice Trend. |
| Middle right | Clustered bar chart | Y-axis: `CustomerName`; X-axis: `[Outstanding Receivables]` | Sort descending; title: Outstanding Receivables by Customer. |
| Bottom left | Donut chart | Legend: `PaymentMethod`; Values: `[Total Payments Received]` | Title: Payments by Method; show total in the centre. |
| Bottom right | Clustered column chart | X-axis: `Aging Bucket`; Y-axis: `[Outstanding Receivables]` | Title: Outstanding Receivables by Aging. |

## 5. Finish and validate

1. Turn on visual titles and use sentence case exactly as shown in the table.
2. For the customer chart, apply a Top N 10 filter by `[Outstanding Receivables]` if more than ten customers exist.
3. Confirm slicers affect every KPI and chart: **Format → Edit interactions**.
4. Check that total invoiced minus total payments agrees with outstanding receivables, according to your dataset's payment timing rules.
5. Save as a `.pbip` in the project root and follow [dashboard-setup.md](dashboard-setup.md).
