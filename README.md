
# Project Title

A brief description of what this project does and who it's for

Sales Dashboard — 
This README is a learning guide for Sales(Data Modeling Concepts).pbix. It explains what each report page is useful for, why the chart type fits the question, and the Power BI concepts to practise: cardinality, star schema, filters, slicers, and visual interactions.
How to use this guide: Open the PBIX in Power BI Desktop, visit each page named below, select a visual, and inspect its fields in the Visualizations pane. The field names below are based on the report visuals. Exact totals depend on the underlying data and current filters.

# 1. Overview — explore the main business questions

Quick guide: match the visual to the analytical question.
A. How do discounts vary by promotion?
- Visual: Bar chart
- Fields: Promotion Name on the category axis; Discount Value as the value (summed).
- Why this chart: Bars make it easy to compare categories, especially when promotion names are long.
- Learn: Sort by Discount Value, turn on data labels, and compare the highest and lowest promotions.
- Ask: Which promotion has the largest total discount? Are discounts concentrated in a few promotions?
B. How many orders are there?
- Visual: Card
- Field: Number of orders
- Why this chart: A card highlights one important KPI without the detail of a chart.
- Learn: A measure is often better than a raw column for KPIs. Confirm whether the measure counts rows, distinct order IDs, or something else; those definitions can produce different results.
- Ask: Does the order count change when a date, product, or customer filter is applied?
C. Is profit related to net sales?
- Visual: Scatter chart
- Fields: Profit on X; Net Sales on Y.
- Why this chart: Each point represents an observation and helps reveal relationships, clusters, and outliers between two numeric values.
- Learn: Look for an upward or downward pattern, investigate unusual points, and consider adding a meaningful category to Details or Legend if the model supports it.
- Ask: Are high-sales observations also high-profit? Are there high-sales observations with low or negative profit?
D. How do net sales change over time?
- Visual: Line chart
- Fields: Date on the category axis; Net Sales as the value (summed).
- Why this chart: A line chart is suited to ordered time series and makes trends, peaks, and dips visible.
- Learn: Use a real Date column and a continuous/chronological axis where appropriate. Check whether the visual uses the raw date or a date hierarchy.
- Ask: When are sales highest? Is there a trend, seasonality, or a sudden change?
E. Which cities contribute the most sales?
- Visual: Map
- Fields: City as the geographic category; Net Sales for bubble size.
- Why this chart: A map adds geographic context, while larger markers represent greater sales.
- Learn: Set the City data category correctly and add Country/State when city names may be ambiguous. Validate geocoding before drawing business conclusions.
- Ask: Which locations have the largest sales bubbles? Are sales concentrated in certain areas?
# 2. Top/Bottom 5 Analysis — rank products
The page contains bar charts comparing product names with Net Sales, Profit, and Units Sold, including top/bottom views.
Questions to practise
1. Which five products have the highest net sales?
2. Which five products have the lowest net sales?
3. Which five products have the highest profit?
4. Which five products have the lowest profit?
5. Which five products have the highest units sold?
6. Which five products have the lowest units sold?
Why bar charts?
Products are discrete categories, and bars make ranked comparisons easy to read. Horizontal bars are especially useful when product names are long.
How to build a Top N / Bottom N visual
1. Select the product bar chart.
2. In the Filters pane, locate Product Name under Filters on this visual.
3. Change the filter type to Top N.
4. Enter 5, choose Top or Bottom, and drag the measure used by the chart into By value.
5. Select Apply filter.
6. Sort the chart by that same measure.
7. Repeat for each measure and ranking direction.
Important: Top N is evaluated in the current filter context. Selecting a date or promotion can change which products qualify. Use the same measure for the ranking and the displayed value unless you intentionally want a different ranking rule.
Interpretation tip
High sales do not automatically mean high profit. Compare Net Sales, Profit, and Units Sold together before making a recommendation.
# 3. Comparison Sales/Profit/Quantity — compare measures
This page compares paired measures in clustered column charts and includes date slicers.
Concepts to learn
- Net Sales vs. Sales: confirm how each measure is defined before assuming they mean the same thing.
- Profit comparison: use the chart to identify which measure is higher under the current context.
- Quantity comparison: compare the two quantity measures and investigate differences in their definitions.
- Date slicers: select one or more dates/periods and observe whether the comparison charts update.
Why clustered columns?
Clustered columns place measures side by side for the same category, making direct comparisons easier than reading two separate charts. If the chart has no category axis and only measure values, check the visual configuration and labels so viewers can tell which measure is which.
Practice
1. Record the values with no slicer selection.
2. Select a date or date range.
3. Note which visuals change.
4. Clear the slicer and verify that the original view returns.
5. Compare the results with a table or card to validate the interpretation.
# 4. Edit Interactions — control how visuals filter one another

Edit interactions controls whether a source visual filters, highlights, or leaves another visual unchanged.

This page is designed to practise changing visual interactions.
Filter, highlight, or none?
When you select a data point in one visual, Power BI can affect other visuals in different ways:
- Filter: the target visual shows only data matching the selection.
- Highlight: the target keeps the full context but emphasizes the selected portion, where supported.
- None: the target visual is not affected by that source visual.
Change an interaction
1. Select the source visual (the one you will click to make a selection).
2. On the ribbon, choose Format → Edit interactions (the wording/location can vary by Power BI Desktop version).
3. Icons appear on the other visuals.
4. On each target visual, choose Filter, Highlight, or None, as available.
5. Turn off Edit interactions and test by selecting a bar or slicer value.
6. Repeat for other source visuals as needed.
The report has explicit NoFilter interactions configured for some source/target pairs. Test the report to see which visual selections intentionally do not affect other charts.
Good design practice
Not every visual needs to control every other visual. For example, a chart used to compare independent KPIs may be easier to interpret if clicking one KPI does not unexpectedly filter the others.
# 5. Table Visuals — inspect detail behind the summaries
The table includes fields such as Customer ID, Order ID, Product ID, Promotion ID, Date, Discount Value, Discount Percentage, Net Sales, Price Per Unit, Profit, Total Sales, and Units Sold. Product, customer, date, and promotion slicers are also present.
Why use a table?
Charts reveal patterns; tables let you inspect individual records and verify the values behind a chart.
Practice
- Filter to one product and inspect its records.
- Filter to one customer and check the associated orders.
- Select a date range and verify that the rows are restricted as expected.
- Compare totals in the table with the corresponding chart or KPI.
- Be careful with totals: adding a column is not always equivalent to calculating a business metric. Use measures when the business definition requires distinct counts, ratios, or custom logic.
# 6. Data modelling — fact tables, dimensions, and star schema


Illustrative model: verify the actual table and relationship names in your PBIX.

A star schema separates measurable business events from the descriptive attributes used to analyse them.
- Fact table: stores events/transactions and numeric values, for example units sold, sales, discounts, and profit. It usually contains foreign keys to dimensions.
- Dimension tables: describe the event, for example Product, Customer, Date, Promotion, and Geography/Location.
- Measures: calculations used in visuals, such as total net sales, total profit, units sold, or order count.
A typical sales model may look like this (adapt the names to the actual model in the PBIX):
                 DimDate
                    |
DimProduct — FactSales — DimCustomer
                    |
               DimPromotion
                    |
                DimLocation
Why a star schema?
- Clear separation between numeric transactions and descriptive labels.
- Simpler relationships and more predictable filtering.
- Easier-to-understand DAX measures and report visuals.
- Often better performance than a highly snowflaked model.
Model inspection checklist
1. Open Model view in Power BI Desktop.
2. Identify the fact table and each dimension table.
3. Check that dimension keys are unique on the “one” side of relationships.
4. Check that fact-table foreign keys match dimension keys.
5. Confirm that the Date dimension has one row per date and is marked as a date table when appropriate.
6. Prefer dimension fields (such as DimProduct[Product Name]) for slicers and chart categories, and fact-table numeric columns/measures for values.
7. Check for orphan keys, blank dimension members, and duplicate dimension keys.
Note: The diagram above is a teaching example, not a claim that every table is present under those exact names in this file. Verify the actual model in Model view.
# 7. Relationship cardinality

Use one-to-many for the usual dimension-to-fact relationship when dimension keys are unique.

Cardinality describes how many rows on one side of a relationship can match rows on the other side.
Cardinality	Meaning	Typical sales-model example	Common use
One-to-many (1:*)	One dimension row can match many fact rows	One product → many sales rows	Preferred pattern for dimension-to-fact relationships
Many-to-one (*:1)	The same relationship viewed from the fact side	Many sales rows → one product	Equivalent to 1:* in the opposite direction
One-to-one (1:1)	Each side has at most one matching row	Two tables with unique keys on both sides	Use only when the data genuinely has this structure
Many-to-many (:)	Multiple rows on both sides can match	Shared/non-unique keys on both tables	Use carefully; ambiguity and unexpected totals can occur


# How to check cardinality
1. Open Model view.
2. Select a relationship line or open Manage relationships.
3. Inspect Cardinality, Cross-filter direction, and whether the relationship is active.
4. For a normal star schema, dimension key is usually unique and the relationship is One-to-many, with the dimension on the 1 side and the fact on the * side.
Common pitfalls
- A dimension key is not unique, so Power BI cannot use it as the “one” side.
- Many-to-many is used to work around duplicate keys instead of fixing the model.
- Relationships connect columns with different meanings or data types.
- Several active filter paths create ambiguity.
- Bidirectional filtering is enabled without a clear reason.
# 8. Filter types in Power BI

Filter scope determines which visuals and pages are affected.

Power BI has several filter mechanisms. They affect different scopes.
Filter type	Scope	Example
Visual-level filter	One selected visual	Show only the top 5 products in one chart
Page-level filter	All visuals on one report page	Restrict the page to one year
Report-level filter	All pages in the report	Exclude test transactions throughout the report
Slicer	An interactive on-canvas control	Let users choose a date, product, customer, or promotion
Drillthrough filter	Passes selected context to a detail page	Right-click a product and open its detail page
Cross-filter / cross-highlight	Selection in one visual affects another	Click a product bar and update other visuals
Top N filter	Keeps the top/bottom N categories by a chosen value	Top 5 products by Net Sales
Basic filter	Select specific values from a list	Choose a particular promotion
Advanced filter	Apply conditions such as contains, greater than, or is not blank	Net Sales greater than a threshold
Relative date filter	Dynamic date window	Last 30 days
Relative time filter	Dynamic time window where supported	Recent hours/minutes for time-based data


Filter context
A measure is evaluated within its current filter context. A measure like total Net Sales can return a different result when the user changes a slicer, clicks a bar, or applies a page/report filter. This is expected behaviour, not necessarily a change to the underlying data.
Filter pane scopes
- Filters on this visual — affects the selected visual.
- Filters on this page — affects visuals on the current page.
- Filters on all pages — affects the report broadly.
Always check the scope before troubleshooting a chart that looks different from another page.
# 9. Changing filter behaviour for dimensions
Dimension tables should normally filter the fact table through relationships. For example, selecting a Product dimension value filters matching fact rows, and measures then recalculate for those rows.
A. Change which visuals a slicer affects
1. Select the slicer.
2. Choose Format → Edit interactions.
3. On each target visual, choose Filter, Highlight (where supported), or None.
4. Exit Edit interactions and test the slicer.
This changes report interaction behaviour; it does not change the underlying relationship.
B. Change relationship filter direction
1. Open Model view and select the relationship.
2. Edit Cross-filter direction.
3. Use Single for the typical dimension-to-fact filter path in a star schema.
4. Use Both only when there is a clear requirement and you understand the effect on other relationships and measures.
Best practice: Do not set all relationships to Both by default. Bidirectional filtering can create ambiguous paths, unexpected results, and performance issues. Consider a bridge table or a targeted DAX solution when the model requires more complex filtering.
C. Change which dimension field is used
Use the dimension's descriptive column for a slicer or axis, not a duplicate label in the fact table, whenever possible. This keeps category selection consistent and lets the relationship carry the filter to the fact table.
D. Make a measure ignore or modify a dimension filter (DAX)
Sometimes a measure should intentionally ignore a particular dimension filter. For example, if the model contains a DimProduct table:
Net Sales =
SUM ( FactSales[Net Sales] )

Net Sales All Products =
CALCULATE (
    [Net Sales],
    REMOVEFILTERS ( DimProduct )
)
Net Sales All Products removes filters from DimProduct while retaining other filter context, such as date or customer, unless those filters are affected by the model. Replace table/column names with the actual names in your model.

Other useful DAX filter functions:
- CALCULATE() — evaluates an expression in modified filter context.
- REMOVEFILTERS() — clears filters from specified tables or columns.
- ALL() — can remove filters and is also used in table expressions.
- KEEPFILTERS() — intersects a filter with existing filters rather than replacing them in the usual way.
- ALLSELECTED() — often useful for calculations that respect outer selections while changing the visual's internal context.
Use DAX only when changing slicer interactions or model relationships does not express the intended business rule.
# 10. A repeatable learning workflow
For every question in the report:
1. State the question in plain language.
2. Choose a visual that matches the analytical task: trend, comparison, ranking, relationship, geography, KPI, or detail.
3. Assign fields to the correct visual roles (axis/category, values, legend, size, or details).
4. Check aggregation — sum, average, count, or distinct count must match the question.
5. Check the model — use dimensions for grouping and fact data/measures for values.
6. Apply filters — test visual, page, report, and slicer behaviour separately.
7. Test interactions — click points/bars and confirm which other visuals change.
8. Validate — compare the result with a table or a second calculation.
9. Explain the insight — describe what the chart shows, not just its largest number.
10. Document assumptions — especially how order count, net sales, profit, and quantity are defined.
# 11. Quick glossary
- Dimension: descriptive entity used to group/filter facts.
- Fact: measurable business event or transaction.
- Measure: calculation evaluated in the current filter context.
- Cardinality: number of matching rows across a relationship.
- Cross-filter direction: direction in which relationship filters propagate.
- Filter context: filters active when a measure is evaluated.
- Slicer: interactive report control that filters data.
- Top N: filter that retains a chosen number of categories based on a value.
- Edit interactions: controls whether a visual filters, highlights, or does not affect another visual.
- Star schema: central fact table connected to descriptive dimensions.
