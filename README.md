```
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
