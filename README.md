# DAY 3 HCL TASK
### ADVANCED SELENIUM AUTOMATION USING PYTHON
#### Alerts | Dropdowns | Waits | Mouse Actions | Web Elements | E-Commerce Automation
### AIM
To develop a Selenium automation program using Python to automate web application functionalities such as login, alerts, mouse actions, product search, checkout, order placement, and to use explicit waits for reliable test execution.
### ALGORITHM
1.	Start the program.
2.	Import the required Selenium modules and Python libraries.
3.	Open the Microsoft Edge browser using Selenium WebDriver.
4.	Maximize the browser window and create an explicit wait.
5.	Open the SauceDemo website and perform login using valid credentials.
6.	Verify that the inventory page is displayed successfully.
7.	Open the Selenium Alerts page and handle a simple alert using Accept.
8.	Handle a confirmation alert using Dismiss.
9.	Handle a prompt alert by entering text and accepting it.
10.	Open the mouse interaction page and perform Mouse Hover.
11.	Perform a Double Click and verify the result.
12.	Perform Drag and Drop from the source element to the target element.
13.	Open the Automation Exercise products page.
14.	Enter a product name in the search box and verify the searched products.
15.	Open SauceDemo again and log in.
16.	Add a product to the cart and proceed to checkout.
17.	Enter customer details and place the order.
18.	Verify the order confirmation message.
19.	Generate and handle an Order Confirmation Alert.
20.	Add a 3-second gap between each test case for clear execution.
21.	Close the browser after completing all test cases.
22.	Display the final execution status.
23.	Stop the program.

### PROGRAM CODE 
```PYTHON
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Edge()
driver.maximize_window()

wait = WebDriverWait(driver, 10)


##### TC01 - LOGIN

driver.get("https://www.saucedemo.com/")

print("TC01 - Shopping website opened successfully")

wait.until(
    EC.visibility_of_element_located((By.ID, "user-name"))
).send_keys("standard_user")

driver.find_element(
    By.ID, "password"
).send_keys("secret_sauce")

driver.find_element(
    By.ID, "login-button"
).click()

wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "inventory_list")
    )
)

print("TC01 - Login successful")

time.sleep(3)


# TC02 - SIMPLE ALERT

driver.get(
    "https://www.selenium.dev/selenium/web/alerts.html"
)

driver.find_element(
    By.ID, "alert"
).click()

alert = wait.until(
    EC.alert_is_present()
)

print("\nTC02 - Alert:")
print(alert.text)

alert.accept()

print("TC02 - Alert accepted successfully")

time.sleep(3)


# TC03 - CONFIRMATION ALERT

driver.get(
    "https://www.selenium.dev/selenium/web/alerts.html"
)

driver.find_element(
    By.ID, "confirm"
).click()

alert = wait.until(
    EC.alert_is_present()
)

print("\nTC03 - Confirmation Alert:")
print(alert.text)

alert.dismiss()

print("TC03 - Confirmation alert dismissed successfully")

time.sleep(3)


# TC04 - PROMPT ALERT

driver.get(
    "https://www.selenium.dev/selenium/web/alerts.html"
)

driver.find_element(
    By.ID, "prompt"
).click()

alert = wait.until(
    EC.alert_is_present()
)

print("\nTC04 - Prompt Alert:")
print(alert.text)

alert.send_keys("Aditya")
alert.accept()

print("TC04 - Prompt alert handled successfully")

time.sleep(3)


# TC05 - MOUSE HOVER

driver.get(
    "https://www.selenium.dev/selenium/web/mouse_interaction.html"
)

hover_element = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "hover")
    )
)

ActionChains(driver).move_to_element(
    hover_element
).perform()

move_status = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "move-status")
    )
)

print("\nTC05 - Mouse Hover performed successfully")
print("Result:", move_status.text)

time.sleep(3)


# TC06 - DOUBLE CLICK

driver.get(
    "https://www.selenium.dev/selenium/web/mouse_interaction.html"
)

double_click_element = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "clickable")
    )
)

ActionChains(driver).double_click(
    double_click_element
).perform()

click_status = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "click-status")
    )
)

print("\nTC06 - Double Click performed successfully")
print("Result:", click_status.text)

time.sleep(3)


# TC07 - DRAG AND DROP

driver.get(
    "https://www.selenium.dev/selenium/web/mouse_interaction.html"
)

source = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "draggable")
    )
)

target = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "droppable")
    )
)

ActionChains(driver).drag_and_drop(
    source,
    target
).perform()

drop_status = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "drop-status")
    )
)

print("\nTC07 - Drag and Drop performed successfully")
print("Result:", drop_status.text)

time.sleep(3)


# TC08 - PRODUCT SEARCH

driver.get(
    "https://www.automationexercise.com/products"
)

search_box = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "search_product")
    )
)

search_box.clear()
search_box.send_keys("Top")

search_button = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "submit_search")
    )
)

search_button.click()

searched_products = wait.until(
    EC.visibility_of_element_located(
        (
            By.XPATH,
            "//h2[contains(translate(normalize-space(.), "
            "'abcdefghijklmnopqrstuvwxyz', "
            "'ABCDEFGHIJKLMNOPQRSTUVWXYZ'), "
            "'SEARCHED PRODUCTS')]"
        )
    )
)

products = wait.until(
    EC.presence_of_all_elements_located(
        (
            By.XPATH,
            "//div[contains(@class,'productinfo')]"
        )
    )
)

print("\nTC08 - Product search completed successfully")
print("Result:", searched_products.text)
print("Number of products found:", len(products))

time.sleep(3)


# TC09 - PLACE ORDER

driver.get(
    "https://www.saucedemo.com/"
)

wait.until(
    EC.visibility_of_element_located(
        (By.ID, "user-name")
    )
).send_keys("standard_user")

driver.find_element(
    By.ID, "password"
).send_keys("secret_sauce")

driver.find_element(
    By.ID, "login-button"
).click()

wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "inventory_list")
    )
)

driver.find_element(
    By.ID,
    "add-to-cart-sauce-labs-backpack"
).click()

driver.find_element(
    By.CLASS_NAME,
    "shopping_cart_link"
).click()

wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "cart_item")
    )
)

driver.find_element(
    By.ID,
    "checkout"
).click()

wait.until(
    EC.visibility_of_element_located(
        (By.ID, "first-name")
    )
).send_keys("Aditya")

driver.find_element(
    By.ID,
    "last-name"
).send_keys("S")

driver.find_element(
    By.ID,
    "postal-code"
).send_keys("600001")

driver.find_element(
    By.ID,
    "continue"
).click()

finish_button = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "finish")
    )
)

print("\nTC09 - Place Order button is clickable")

finish_button.click()

confirmation = wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "complete-header")
    )
)

print("TC09 - Order submitted successfully")
print("Result:", confirmation.text)

time.sleep(3)


# TC10 - ORDER CONFIRMATION ALERT

driver.get(
    "https://www.saucedemo.com/"
)

wait.until(
    EC.visibility_of_element_located(
        (By.ID, "user-name")
    )
).send_keys("standard_user")

driver.find_element(
    By.ID, "password"
).send_keys("secret_sauce")

driver.find_element(
    By.ID, "login-button"
).click()

wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "inventory_list")
    )
)

driver.find_element(
    By.ID,
    "add-to-cart-sauce-labs-backpack"
).click()

driver.find_element(
    By.CLASS_NAME,
    "shopping_cart_link"
).click()

wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "cart_item")
    )
)

driver.find_element(
    By.ID,
    "checkout"
).click()

wait.until(
    EC.visibility_of_element_located(
        (By.ID, "first-name")
    )
).send_keys("Aditya")

driver.find_element(
    By.ID,
    "last-name"
).send_keys("S")

driver.find_element(
    By.ID,
    "postal-code"
).send_keys("600001")

driver.find_element(
    By.ID,
    "continue"
).click()

finish_button = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "finish")
    )
)

finish_button.click()

wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "complete-header")
    )
)

driver.execute_script(
    "setTimeout(function(){"
    "alert('Order confirmation successful')"
    "}, 500)"
)

alert = wait.until(
    EC.alert_is_present()
)

print("\nTC10 - Order Confirmation Alert:")
print(alert.text)

alert.accept()

print("TC10 - Confirmation alert handled successfully")

time.sleep(3)


# END

driver.quit()

print("\nAll test cases completed successfully")

``` 
### OUTPUT
<img width="1600" height="998" alt="image" src="https://github.com/user-attachments/assets/c2fb5f91-eb44-4f24-a0e4-317f61918971" />
<img width="1327" height="612" alt="image" src="https://github.com/user-attachments/assets/78aaf1b1-eb7c-486e-b7f9-2934ded7620c" />

