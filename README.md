###XXXXXXXXXX
```py
import requests
from bs4 import BeautifulSoup

# Provide the URL of the webpage you want to scrape
url = "https://www.rekhta.org/ghazals/sitaaron-se-aage-jahaan-aur-bhii-hain-allama-iqbal-ghazals-1?lang=ur"

# Send a GET request to the URL
response = requests.get(url)

# Check if the request was successful (status code 200)
if response.status_code == 200:
    # Parse the HTML content of the webpage
    soup = BeautifulSoup(response.content, 'html.parser')
    
    # Select the elements you want to extract using CSS selectors
    # For example, select all paragraph elements
    paragraphs = soup.select('.c p')
    
    # Iterate over the selected paragraphs and print their text
    for paragraph in paragraphs:
        print(paragraph.get_text(strip=True))
else:
    print("Failed to retrieve the webpage. Status code:", response.status_code)

```
### File to JSON
```py
import os
import json

# Path to the folder containing the text files
folder_path = 'urdu'

# List to store category dictionaries
categories = []

# Iterate over each file in the folder
for file_name in os.listdir(folder_path):
    file_path = os.path.join(folder_path, file_name)
    # Check if the path is a file (not a directory)
    if os.path.isfile(file_path):
        # Read the content of the file
        with open(file_path, 'r', encoding='utf-8') as file:
            lines = file.readlines()
            # Extract category name from the first line
            category_name = lines[1].strip()
            # Remove category name from the lines
            content_lines = lines[1:]
            poetry_lines = []
            # Group content lines into pairs (line1, line2)
            for i in range(0, len(content_lines), 2):
                line1 = content_lines[i].strip()
                line2 = content_lines[i + 1].strip() if i + 1 < len(content_lines) else ''
                poetry_lines.append({"line1": line1, "line2": line2})
            # Create category dictionary
            category_dict = {
                "category_name": category_name,
                "poetry_lines": poetry_lines
            }
            categories.append(category_dict)

# Path to the output JSON file
output_file = 'output.json'

# Write categories to the output JSON file
with open(output_file, 'w', encoding='utf-8') as json_file:
    json.dump(categories, json_file, ensure_ascii=False, indent=4)

print("Data saved successfully to", output_file)

```
