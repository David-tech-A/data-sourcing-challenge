# NASA CME and GST Data Processing

## Description

This project aims to request Coronal Mass Ejection (CME) and Geomagnetic Storm (GST) data from the NASA API, clean and merge the data, and export it for future use. The project is divided into three parts:

1. Request CME data from the NASA API.
2. Request GST data from the NASA API.
3. Merge and clean the data for export.

## Instructions

### Part 1: Request CME Data from the NASA API

1. Set up the base URL and search variables.
2. Make a GET request to obtain the CME data and store it in a variable `cme_response`.
3. Convert the response to JSON format and store it in a variable `cme_json`.
4. Convert `cme_json` to a Pandas DataFrame and keep only the columns `activityID`, `startTime`, and `linkedEvents`.
5. Remove rows with missing values in `linkedEvents`.
6. Expand rows in `linkedEvents` that contain multiple events into individual rows.
7. Create a function `extract_activityID_from_dict` to extract `activityID` from the dictionaries in `linkedEvents`.
8. Apply this function to each row in the `linkedEvents` column and create a new column `GST_ActivityID`.
9. Remove rows with missing values in `GST_ActivityID`.
10. Convert `GST_ActivityID` to string format and `startTime` to datetime format.
11. Rename `startTime` to `startTime_CME` and `activityID` to `cmeID`.
12. Keep only rows where `GST_ActivityID` contains 'GST'.

### Part 2: Request GST Data from the NASA API

1. Set up the base URL and search variables.
2. Make a GET request to obtain the GST data and store it in a variable `gst_response`.
3. Convert the response to JSON format and store it in a variable `gst_json`.
4. Convert `gst_json` to a Pandas DataFrame and keep only the columns `activityID`, `startTime`, and `linkedEvents`.
5. Remove rows with missing values in `linkedEvents`.
6. Expand rows in `linkedEvents` that contain multiple events into individual rows.
7. Apply the `extract_activityID_from_dict` function to each row in the `linkedEvents` column and create a new column `CME_ActivityID`.
8. Remove rows with missing values in `CME_ActivityID`.
9. Convert `gstID` to string format and `startTime` to datetime format.
10. Rename `startTime` to `startTime_GST`.
11. Keep only rows where `CME_ActivityID` contains 'CME'.

### Part 3: Merge and Clean the Data for Export

1. Merge both DataFrames using `gstID` and `CME_ActivityID` for GST, and `GST_ActivityID` and `cmeID` for CME.
2. Verify that the new DataFrame has the same number of rows as the `cme` and `gst` DataFrames.
3. Calculate the time difference between `startTime_GST` and `startTime_CME` by creating a new column `timeDiff`.
4. Use `describe()` to compute the mean and median time.
5. Export the data to a CSV file without the DataFrame's index.

## Requirements

- Python 3.x
- Pandas
- Requests
- JSON

## Usage

1. Ensure your NASA API key is in a `.env` file.
2. Run the script to obtain, clean, and merge the data.
3. The merged data will be exported to a CSV file for future use.
