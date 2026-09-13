Crime Data Cleaning and Classification

A data cleaning and exploratory modeling project built on a deliberately messy, synthetic crime incidents dataset. The focus is on realistic data cleaning decisions , handling inconsistent categories, ambiguous formats, and missing values , followed by an attempt at classification to test whether the cleaned features carry predictive signal.

Dataset

crime_incidents_messy.csv contains 5,250 synthetic crime records with 33 columns, including incident details, suspect and victim demographics, weapon type, case status, and resolution outcomes. The dataset was intentionally corrupted with inconsistent casing, typos, mixed date formats, sign errors, and missing values to simulate real-world data quality issues.


Cleaning Process
Each column was cleaned individually, with decisions based on what the missingness or inconsistency actually meant, rather than applying a single blanket strategy:

1. Categorical inconsistencies (crime type, gender, race, weapon, resolution, case status): standardized casing and typos, merged duplicate categories written in different forms.

2. Numeric fields (age, property loss, arrest counts) : invalid values (negative ages, sign-flipped losses) were corrected or removed; missing values were either dropped or filled based on what each null value represented, not a default imputation rule.

3 Missing value strategy :before dropping or filling any column, missingness was checked against case_status to confirm it wasn't concentrated in a specific case outcome (which would have introduced bias). Categorical unknowns were filled with "unknown" rather than a guessed real category, to avoid fabricating information.

4. Date parsing incident timestamps were in day-first format (DD/MM/YYYY), which is ambiguous for pandas' default date parser. Format was explicitly specified to prevent silent day/month swaps.

5. Encoding  ordinal encoding was used for genuinely ordered categories (severity), one-hot encoding for unordered categories (gender, race, weapon, resolution), and label encoding for the classification target.
Modeling

5. Several classifiers (Logistic Regression, Gaussian Naive Bayes, Decision Tree, SVM) were trained to predict case severity and case status from the cleaned features.

Accuracy stayed close to the random-guessing baseline for a five-class problem (roughly 20%), and feature importance analysis showed no single feature carrying strong predictive weight (highest importance around 9%). This indicates the available features do not have a meaningful relationship with the target in this dataset, a reasonable outcome given the data was generated for cleaning practice, not to encode a genuine predictive pattern.

What This Project Demonstrates:

Cleaning decisions grounded in reasoning about what missing or malformed data actually represents, rather than default fill rules
Checking for bias before dropping data (correlating missingness against case outcome)
Correct handling of ambiguous date formats
Choosing encoding strategy based on whether a category has a natural order
Recognizing and diagnosing weak model performance through class balance and feature importance, rather than reporting results at face value

Tools:
Python, pandas, NumPy, scikit-learn, seaborn, matplotlib

License:
MIT