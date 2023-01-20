# GA_race_prediction
Chris Iyer
Updated 1/18/2023

GOAL: Testing various race prediction methods on Georgia voter lists to select the best method for predicting race of Texas voters. Our ultimate goal is to estimate various voting behaviors of AAPI voters in Texas, but Texas (unlike Georgia) does not report race information with their voter list.

Here, I tested 3 libraries and several different methods for race prediction: the main libraries were:
- Predictrace: https://cran.r-project.org/web/packages/predictrace/vignettes/Predict-race-of-surname.html
- WRU: https://github.com/kosukeimai/wru
- Ethnicolr: https://github.com/appeler/ethnicolr

Link to google drive folder: https://drive.google.com/drive/folders/1kqZ6-R5Ji2_3zUtfTnhmExwDiRl_AGXf?usp=share_link
  This folder also contains
    1. The raw predictions of each method, to use in further assessments (GA_predictions.csv)
    2. The raw data — merged GA voter list between 2020 and 2022 raw voter list files, excluding entries with unknown race (GAlist_merged_nonan.csv)

Results:
Tl;dr WRU with geocoding reaches pretty solid and balanced performance for AAPIs as well as other racial groups. Predictrace full-name averaging comes in second. These options, as well as numerous different combination schemes of different predictions, can be titrated to minimize false positives vs. false negatives. But, as a first pass, I recommend using WRU with geocoding if you have access to county-, tract-, or block-level information, and using predictrace with an averaging scheme like the one I use in the absence of geographic data.


Top Scorers:
- WRU (surname + geocoding)
    AP: sens = 67%, PPV = 86%
    Slightly better on other races
- Predictrace (firstname + surname average)
    AP: sens = 64%, PPV = 89%
- Combination of (1) and (2): wru_geo OR pr_avg 
    AP: sens = 71%, PPV = 83%
- Combination of (1) and (2): wru_geo AND pr_avg
    AP: sens = 60%, PPV = 93%
Choose various different combinations to maximize sensitivity or PPV
- Max PPV: something like wru_geo AND pr_avg AND et_fl
    Sens = 50% PPV = 95%
- Max sens: something like wru_geo OR pr_avg OR et_fl_other
    Sens = 98%, PPV = 60%


More detailed results are discussed in results.pdf
