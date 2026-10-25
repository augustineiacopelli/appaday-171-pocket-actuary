# Pocket Actuary

AppADay 171. See your own odds of reaching any age, straight from the official Social Security Administration 2023 period life table.

Live: https://augustineiacopelli.github.io/appaday-171-pocket-actuary/

## What it does

Pick a mortality table and enter a birthdate (month, day, and four digit year) (male or female) and the app draws your survival curve with a shaded band for future mortality improvement of 0 to 2 percent a year. It lists your chance of being alive at 65, 75, 85, 90, 95, 100, and any custom age, and the ages at which that chance falls to 90, 75, 50, 25, and 10 percent.

The Together tab adds a partner, whose mortality table is set automatically to the opposite sex of yours, and shows the chance both are alive, at least one is alive, and exactly one is alive, plus median years to the first and last death. The Factors tab holds illustrative hazard ratio sliders and the improvement selector. The Horizon tab shows your life in weeks, with markers at the median and 25th percentile ages, and a Social Security claiming panel with break even ages for 62 vs 67, 67 vs 70, and 62 vs 70.

## How the numbers work

Death rates for ages 0 to 119 are embedded from the SSA 2023 period life table used in the 2026 Trustees Report. Survivors start at 100,000 and shrink by each year's rate. Remaining life is the area under the survival curve. A hazard ratio changes each rate as q' = 1 minus (1 minus q) raised to the ratio. Improvement multiplies the rate k years ahead by (1 minus r) to the k. Fractional ages use straight line interpolation.

On load the app recomputes life expectancy at ages 0, 40, and 65 and warns in the console if any value differs from the SSA column by more than 0.1 years. With a hazard ratio of 1.0 and no improvement, it reproduces the SSA table.

Claiming factors for a full retirement age of 67 are 70, 75, 80, 86.67, 93.33, 100, 108, 116, and 124 percent for ages 62 through 70. Break even ages ignore taxes, inflation adjustments, interest, and spousal benefits.

## Estimating a hazard ratio

The Factors tab can estimate a hazard ratio for you or a partner from six groups of answers: smoking, height and weight, leisure time exercise, diabetes, marital status, and the lifespan of your parents. A hazard ratio multiplies the chance of dying in any given year compared with the average person in the SSA table. Insurers express the same idea as a percent of standard mortality, with each table rating step adding 25 percent.

Sources and figures used: Jha and colleagues (New England Journal of Medicine, 2013) for smoking, with mortality ratios of 2.8 for men and 3.0 for women and years gained by quitting; the Global BMI Mortality Collaboration (Lancet, 2016) for weight; Arem and colleagues (JAMA Internal Medicine, 2015) for activity; the Emerging Risk Factors Collaboration (2011) for diabetes at 1.80; and Li and colleagues (Circulation, 2018) as a check on the combined spread. CDC and NHANES figures give how common each factor is: 11.0 percent smoking (2023), 30.7 percent overweight, 42.4 percent obesity, and 9.2 percent severe obesity (2017 to 2018), 47.2 percent meeting the aerobic guideline (2024), and about 15 percent of adults with diabetes.

Two steps matter. First, each published ratio is divided by the average ratio across the population, because the SSA table already describes an average American and not a never smoker at a healthy weight. Second, the product of the separate ratios is shrunk to 65 percent in log terms, because factors overlap and plain multiplication overshoots the spread Li and colleagues found. The 65 percent, the "quit at 45 or later" interpolation, and the splits inside broad CDC groups are my assumptions, not published figures. The range shown is a rule of thumb of 20 percent below to 25 percent above the estimate.

The family history line uses a UK Biobank analysis of about 186,000 people aged 55 to 73, as reported in an American College of Cardiology release in 2016: all cause mortality was 16 percent lower per extra decade of a mother's life and 17 percent lower per decade of a father's life past age 69. The app uses 0.835 per decade for each parent, centered on age 79 (my assumption for a typical parental lifespan), counts deaths only between ages 69 and 95 because the evidence covers later ages, counts a living parent only from age 80, and ignores a parent who died of an accident. Two parents together count at 70 percent of their combined effect, which is my judgment because they share habits and a household. I read the release and not the paper itself, so this is the least verified line in the estimator. Twin studies put the inherited share of lifespan near 15 to 30 percent and a 2018 family tree study near 7 percent or less, so much of the signal overlaps with the lifestyle factors, which the overall shrink also addresses.

Marital status uses a 2020 meta-analysis of 20 studies and about 7.8 million people (Global Health Research and Policy): all cause mortality for unmarried versus married people was 1.46 for men and 1.22 for women, with never married at 1.67 and 1.46, divorced or separated at 1.59 and 1.27, and widowed at 1.30 and 1.14. I read a summary of the paper, not the paper. Because part of the gap is selection and overlap with other factors, the app divides each ratio by the population average (rough shares I assumed: 50 percent married, 32 never married, 12 divorced or separated, 6 widowed), shrinks it to half strength in log terms, and skips it under age 30. Those three steps are my judgment.

Grandparents are an optional input counted only when no parent line applies, for example while both parents are living and under 80. No study I could verify gives a hazard ratio for them, so the app applies half the parent effect in log terms (about 0.91 per decade, because a grandparent shares half as many genes), centered on 76 (my assumption) and limited to ages 65 through 95. It is a small, clearly labeled nudge and not a published figure.

The weight effect is scaled down after age 60, reaching 45 percent of its strength by 80, using the Global BMI Mortality Collaboration figures of 1.52 per 5 BMI units above 25 at ages 35 to 49 and 1.21 at ages 70 to 89. Starting the taper at 60 is my assumption. Other factors are not tapered because age specific ratios could not be verified.

Left out on purpose: existing conditions such as heart disease or cancer, alcohol, diet, blood pressure, the cause of death of a parent, family history of specific diseases, and friendships and other social ties, because a usable hazard ratio could not be verified or the effect overlaps with the factors above. A prior diagnosis can outweigh everything the estimator uses. Ratios describe groups, not individuals.

## Checks built into the app

The Factors tab shows what a hazard ratio does: average years left and median age at death against the table average, with a curve and a rule of thumb band. A Model check and limits panel recomputes life expectancy at ages 0, 40, and 65 from the embedded death rates and compares it with the SSA column, then runs a calibration: a healthy profile against an unhealthy one at age 50 gives about an 11 year gap in life expectancy for both sexes, compared with the 12.2 years for men and 14.0 for women that Li and colleagues found between five healthy habits and none (their habits also include diet and alcohol, so a somewhat smaller gap is expected). The Survival tab has a Copy summary button that puts inputs and key results on the clipboard, with a select and copy box if the browser blocks copying.

## Not medical or financial advice

This is an educational picture of population averages. It is not a forecast for any person and not medical or financial advice. Hazard ratios on the Factors tab are illustrative and not derived from the table. Both lives in the Together tab are treated as independent.

## Notes

Single file of vanilla HTML, CSS, and JavaScript with SVG charts and no dependencies. State is kept in the browser under appaday.171.state. No data leaves the device. The Claude API is not used.

Part of the [AppADay portfolio](https://augustineiacopelli.github.io/appaday/).
