#download the database
import requests
import zipfile
import io
import pandas as pd
import os

def download_and_add_to_csv(start_date, csv_path):
    # Construct the URL for the bhavcopy file
    url = f"https://www1.nseindia.com/content/historical/EQUITIES/{start_date.strftime('%Y')}/{start_date.strftime('%b').upper()}/cm{start_date.strftime('%d%b%Y').upper()}bhav.csv.zip"

    # Set the request headers
    headers = {'User-Agent': 'Mozilla/5.0'}

    # Send the GET request
    response = requests.get(url, headers=headers)

    # Check if the response is successful
    if response.status_code == 200:
        # Extract the zip file
        with zipfile.ZipFile(io.BytesIO(response.content)) as zf:
            filename = zf.namelist()[0]
            data = pd.read_csv(zf.open(filename))

        # Append the data to the CSV file
        if os.path.exists(csv_path):
            data.to_csv(csv_path, mode='a', header=False, index=False)
        else:
            data.to_csv(csv_path, index=False)

        print(f"Bhavcopy for {start_date} added to {csv_path}")

    else:
        print(f"Failed to download bhavcopy for {start_date}")
