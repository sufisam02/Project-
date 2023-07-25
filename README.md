# Project-
#Import the required libraries
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time


#Import the required libraries      

def create_whatsapp_group(group_name, participants):
    # Replace 'YOUR_CHROME_WEBDRIVER_PATH' with the path to your Chrome webdriver executable
    driver = webdriver.Chrome(executable_path='YOUR_CHROME_WEBDRIVER_PATH')
    driver.get('https://web.whatsapp.com/')
    time.sleep(15)  # Wait for the user to scan the QR code and log in

    # Locate and click the new chat button
    new_chat_btn = driver.find_element_by_css_selector('div._2UaNq')
    new_chat_btn.click()

    # Locate and click the new group button
    new_group_btn = driver.find_element_by_xpath('//div[text()="New group"]')
    new_group_btn.click()

    time.sleep(2)

    # Search and add participants to the group
    for participant in participants:
        search_box = driver.find_element_by_css_selector('div._3FRCZ')
        search_box.send_keys(participant)
        time.sleep(1)

        participant_elem = driver.find_element_by_xpath(f'//span[@title="{participant}"]')
        participant_elem.click()

    # Click the next button
    next_btn = driver.find_element_by_css_selector('button._3y5oW')
    next_btn.click()

    time.sleep(1)

    # Enter the group name
    group_name_input = driver.find_element_by_css_selector('div._2S1VP')
    group_name_input.send_keys(group_name)

    # Click the create button
    create_btn = driver.find_element_by_css_selector('button._3y5oW')
    create_btn.click()

    time.sleep(5)  # Wait for the group to be created
    driver.quit()
    
#Calling the function with the desired group name and participants:
    group_name = "Your Group Name"
participants = ["Participant 1", "Participant 2", "Participant 3"]

create_whatsapp_group(group_name, participants)

