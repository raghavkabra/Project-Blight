# BlightFight

## Task

Work with real data collected in Detroit to help urban planners predict **blight** (the deterioration and decay of buildings and older areas of large cities, due to neglect, crime, or lack of economic support).

## Approach

### Step 1: Establish a list of all the buildings with their space extents.

0. Filter NAs and invalid coordinates (outside the bounds of Detroit)
1. Extract latitutude/longitude pair and address (in raw text) from 4 files
2. Concatenate them into one data frame
3. Clean up the address field (extract numbers, drop symbols, normalize spelling, expand abbreviations, etc)
4. Cluster geolocations by fuzzy matching on address field and incident proximities (`eps = 0.000075`).
5. Represent each building with a rectangle centered at average coordinates.


### Step 2: Generate a balanced data set for training and testing

0. Map demolition permits to buildings, derive positive labels.
1. Random sample a same amount of buildings with negative labels.
2. Concatenate them into a "training" set.


### Step 3: Develop a naive model and evalute its performance.

### Step 4: Feature engineering.

0. Derive features from `violations.csv`, `calls.csv` and `crimes.csv`. Bascially counts of one-hot-encoded categorical variables.
1. Examine feature importance using random forest. Got a ~0.83 AUC score on OOB data.

Counts of violations and crimes are the simplist yet most important features.

### Step 5: Develop a more advanced model.

0. Trained a Xgboost model, got a ~0.85 AUC score on OOB data
1. Simplify the model and still got a~0.849 AUC score.

