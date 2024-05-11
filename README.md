# DSM_DE_Azure

import pandas as pd

# Sample file path
file_path = 'journal_entries.csv'

# Load the CSV file
data = pd.read_csv(file_path)

# Display the first few rows of the dataframe
print("Original Data:")
print(data.head())

# Data Cleaning Steps

# Convert the 'Date' column to datetime format
data['Date'] = pd.to_datetime(data['Date'], errors='coerce')

# Remove any rows where 'Date' could not be converted
data = data.dropna(subset=['Date'])

# Convert 'Amount' to a numeric format, coerce errors and fill NaNs with 0
data['Amount'] = pd.to_numeric(data['Amount'], errors='coerce').fillna(0)

# Strip any leading/trailing whitespace from 'Description'
data['Description'] = data['Description'].str.strip()

# Replace invalid account numbers with NaN and then handle NaNs if needed
# Assume valid account numbers are purely numeric
data['Account Number'] = pd.to_numeric(data['Account Number'], errors='coerce')
data['Account Number'] = data['Account Number'].fillna(0).astype(int)

# Optionally, remove duplicates if necessary
data = data.drop_duplicates()

# Output cleaned data
print("Cleaned Data:")
print(data.head())

# Save the cleaned data back to a CSV if required
data.to_csv('cleaned_journal_entries.csv', index=False)
