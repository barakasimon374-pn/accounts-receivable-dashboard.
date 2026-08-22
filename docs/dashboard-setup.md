# Build and publish this Power BI project

## 1. Prepare a portfolio-safe copy

1. In Power BI Desktop, duplicate the report used for the Accounts Receivable dashboard.
2. Replace confidential fields with anonymised values. For example, use `Customer A`, `Customer B`, and masked invoice IDs.
3. Remove embedded credentials and confirm that no production-only query or connection string remains.
4. Refresh the report and verify that the visuals still tell a coherent story.

## 2. Save as a Power BI Project

1. Open the cleaned report in Power BI Desktop.
2. Select **File → Save As**.
3. Choose **Power BI Project Files (`.pbip`)** as the file type.
4. Save it in this repository root with the name `Accounts-Receivable-Dashboard`.

Power BI creates these source-controlled assets:

```text
Accounts-Receivable-Dashboard.pbip
Accounts-Receivable-Dashboard.Report/
Accounts-Receivable-Dashboard.SemanticModel/
```

Do not commit `.pbix` files unless you deliberately want a binary backup; they are difficult to review in Git.

## 3. Document the report

1. Complete `docs/data-dictionary.md` with your final field names and definitions.
2. Export one anonymised image of each key report page.
3. Put them in `docs/images/` and update the Preview table in the README.
4. Ensure the README's dashboard pages match the pages in your report.

## 4. Create the GitHub repository

1. On GitHub, create a new public repository called `accounts-receivable-dashboard`.
2. Do not initialise it with a README, licence, or `.gitignore`; these are already included here.
3. In the project folder, initialise Git, create the first commit, and push to GitHub.

```powershell
git init
git add .
git commit -m "Initial Accounts Receivable Power BI portfolio project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/accounts-receivable-dashboard.git
git push -u origin main
```

## 5. Portfolio-quality checks before publishing

- Open the `.pbip` from a freshly cloned copy and confirm it loads.
- Verify that the report refreshes from a safe demo source or clearly documents the required parameters.
- Check every screenshot for customer data, internal names, and values that should not be public.
- Confirm that `.pbi/`, raw files, exported extracts, credentials, and `.pbix` backups are ignored.
- Add a concise GitHub repository description: `Power BI Accounts Receivable dashboard for aging, overdue exposure, and collection performance.`

## Suggested GitHub topics

`power-bi`, `powerbi`, `business-intelligence`, `data-analytics`, `finance`, `accounts-receivable`, `dax`, `portfolio`
