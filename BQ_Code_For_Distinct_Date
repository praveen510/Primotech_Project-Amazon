-- Step 1: Get distinct dates from Source Table A
WITH TableA_Dates AS (
  SELECT DISTINCT DATE(column_date_a) AS unified_date
  FROM `project.dataset.source_table_a`
),

-- Step 2: Get distinct dates from Source Table B
TableB_Dates AS (
  SELECT DISTINCT DATE(column_date_b) AS unified_date
  FROM `project.dataset.source_table_b`
),

-- Step 3: Combine and deduplicate all dates
Combined_Dates AS (
  SELECT * FROM TableA_Dates
  UNION DISTINCT
  SELECT * FROM TableB_Dates
),

-- Step 4: Format date into Month-Year and generate row number (optional)
Formatted_Dates AS (
  SELECT
    unified_date,
    FORMAT_DATE('%b-%Y', unified_date) AS month_year_label,
    ROW_NUMBER() OVER (
      PARTITION BY FORMAT_DATE('%b-%Y', unified_date)
      ORDER BY unified_date
    ) AS row_num
  FROM Combined_Dates
)

-- Step 5: Final Output
SELECT
  unified_date,
  month_year_label
FROM Formatted_Dates
ORDER BY unified_date;
