## Paper II: Detecting Bias

## Case Study: Chicago's Strategic Subject List  

## DS 680: Data, Society and AI Ethics

## Question

Chicago police used the Strategic Subject List (SSL) from 2012 to 2019 to give people a
0 to 500 risk score for being involved in a shooting. The score did not use race. I wanted
to check whether it still ended up affecting racial groups differently, and if so, where
that difference came from.

## Data

- Strategic Subject List, Chicago Data Portal: https://data.cityofchicago.org/d/4aki-r3np
- American Community Survey 2012-2016 5-year estimates, U.S. Census Bureau API (tract level)
- Community area boundaries: https://data.cityofchicago.org/d/igwz-8jzy
- Census tract boundaries 2010: https://data.cityofchicago.org/d/74p9-q2aq
- Crimes 2001 to present (arrest and homicide counts, 2012-2016): https://data.cityofchicago.org/d/ijzp-q8t2

The raw data is not in this repo because the files are large. The notebook downloads
everything itself.

## How to run

1. Open `final_code.ipynb` in Google Colab.
2. Get a free Census API key at https://api.census.gov/data/key_signup.html
3. In Colab, open Secrets (key icon on the left), add `CENSUS_API_KEY` with your key,
   and turn on notebook access.
4. Runtime > Run all. It takes about 5 to 8 minutes.

The notebook saves data to Google Drive under `ds680_ssl/`, so it only downloads once.

## Main findings

- 52% of people on the list were Black, compared to about 33% of Chicago. That is about
  1.6 times their share of the city.
- About 1 in 6 Black Chicagoans was flagged (score 250+), compared to about 1 in 15 White
  Chicagoans, a ratio of 2.57.
- The formula itself was close to race-blind. People with identical records got scores
  within about 1 point of each other regardless of race.
- About 95% of the city-wide gap comes from who ends up on the list in the first place.
  Changing the formula (removing police-based inputs, or equalizing flag rates with
  fairlearn) only moved the ratio to between 2.43 and 2.54.
- About 85% of flagged people had no violent arrest and had never been a victim of violence.
  Everyone under 30 on the list was flagged.

## Figures

- `fig1_representation.png`: racial makeup of the list vs Chicago
- `fig2_shap_gap.png`: which inputs add to the racial score gap (SHAP)
- `fig3_map.png`: neighborhood racial makeup and people flagged per 1,000, by community area
- `fig4_policing.png`: flagging vs homicide rates and drug arrest rates by area
- `table3_fixes.csv`: results of the five fixes I tested
  
## Limitations

There is no data on who was actually involved in a shooting later, so accuracy could not
be checked. Community area is missing for 44% of records, and more often for White
individuals. The Census and SSL race categories do not match exactly.
