# Fieldwise: Crop Yield Prediction

A no-install, browser-based capstone prototype. Open `index.html` in a modern browser. Select one crop and enter the existing soil N/P/K, pH, average growing-season temperature, humidity, rainfall, and field-area inputs. The app returns an approximate yield in tonnes per hectare, an estimated total harvest, and a colored percentage marker.

## Your supplied data

Both supplied files are included next to the app for download:

- `provided-india-crop-yield.csv`: 98 India crop-season rows with area, production, and yield across 2021–22 through 2025–26. The app uses the 34 `Total` rows to calculate five-season reference averages. For supported crops with matching India reference data, generated demo yield values are scaled to that crop's five-season national average. Chickpea maps to Gram and Sorghum maps to Jowar. The displayed percentage is predicted yield divided by this five-season reference average. Red is below 70%, amber is 70–99%, and green is 100% or higher. These colors compare with the national historical reference; they are not crop-failure thresholds. Potato has no matching reference, so its percentage is shown as N/A.
- `provided-crop-composition.csv`: 737 crop-composition records with 161 columns, including nutrient and food-composition fields. This file is bundled and downloadable as requested, but is not used to train the yield model because composition and crop-unit-weight fields are not plot yields per hectare paired with weather/soil measurements.

The input requirements have not changed. The app still uses the entered growing-season averages and does not fetch live weather.

## Model and training data

For each supported crop, the app trains a ridge-regression model on 45 generated demonstration examples, calibrated to the relevant India reference where available. Soil/climate combinations in these generated examples are illustrative and are not observed measurements. The model can also learn from measured harvest records that you add or import. Imported CSV replaces the current training records; additions and imports are stored in the current browser.

Do not present demo-based output as validated predictions. For a meaningful capstone evaluation, gather local farm records with the same features and units, split evaluation data by year or location, report MAE/RMSE/R², compare with a baseline, and document data licensing and limitations.

## Training CSV format

Required header (column order may vary):

`crop,nitrogen,phosphorus,potassium,ph,rainfall,temperature,humidity,yield_t_ha`

Each row is one crop/plot/season. N/P/K are kg/ha; rainfall is mm across the growing season; temperature is °C; humidity is percent; yield is tonnes/ha. Supported model crops are Rice, Wheat, Maize, Chickpea, Cotton, Sugarcane, Potato, and Sorghum.
