# Mini-project-11
!pip install requests beautifulsoup4
import requests
from bs4 import BeautifulSoup
import re

def scrape_emails(url):
    try:
        response = requests.get(url)
        if response.status_code != 200:
            print(f"Failed to retrieve {url}")
            return []

        # Parse HTML content
        soup = BeautifulSoup(response.text, 'html.parser')

        # Get visible text from page
        text = soup.get_text()

        # Regex pattern to find emails
        email_pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'

        # Find all matches
        emails = re.findall(email_pattern, text)

        # Remove duplicates
        emails = list(set(emails))

        return emails

    except Exception as e:
        print("Error:", e)
        return []

# Example usage
url = 'https://www.example.com'  # Replace with your target website
emails_found = scrape_emails(url)

print("Emails found:")
for email in emails_found:
    print(email)
