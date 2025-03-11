# gulbakelvan1
import pytest
import requests
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

def setup_browser():
    service = Service(ChromeDriverManager().install())
    driver = webdriver.Chrome(service=service)
    return driver

def test_selenium_and_api():
    driver = setup_browser()
    driver.get("https://example.com")  # Test edilecek siteyi girin
    
    # Web sayfasından veri alma
    element = driver.find_element(By.TAG_NAME, "h1")
    page_text = element.text
    
    # API çağrısı yapma
    response = requests.get("https://jsonplaceholder.typicode.com/posts/1")
    data = response.json()
    
    # Doğrulamalar
    assert response.status_code == 200
    assert "userId" in data
    assert page_text is not None
    
    driver.quit()
    
if __name__ == "__main__":
    pytest.main()
