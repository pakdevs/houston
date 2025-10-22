# Methods and limitations

## Question

What is the main question? (e.g., Did wages in key occupations keep pace with rent since 2019 in the Houston MSA?)

## Scope

- Geography: [MSA/County/Tract]
- Time: [2019–2024], frequency: [annual/monthly]
- Population: [e.g., Occupations SOC codes …] (if applicable)

## Transformations

- Cleaning: [dedupe, column renames, type casts]
- Joins: [keys used; any mismatches and how handled]
- Inflation adjustment: [CPI-U series, base year, formula]
- Derived metrics: [YoY, index=100 in 2019, rankings]
- Suppression/MOE: [how small samples or MOE handled]

## Quality checks

- Row counts before/after merges
- Spot-checks against source totals
- Outliers flagged and reviewed
- NA handling rules

## Limitations

- Data lags / revision risk
- MOE or small-sample caveats
- Geographic boundary comparability
- Licensing/usage constraints
