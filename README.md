
# DemoProject

## Overview
**DemoProject** is a Katalon Studio-based automation testing project designed to simulate and verify core e-commerce flows such as user registration, login, product browsing, cart interaction, checkout, and product search.

This project covers scenarios for both guest and registered users and includes functional verifications across different parts of the application.

---

## Project Structure

```
DemoProject/
├── Test Cases/
│   ├── Scenario 1 - Register New User
│   ├── Scenario 2 - Add Jacket to Cart
│   ├── Scenario 3 - Checkout Cart
│   └── Scenario 4 - Search Product (Nike)
│
├── Object Repository/
│   ├── Header/
│   │   ├── icon_Cart
│   │   └── link_ViewCart
│   ├── Scenario 3/
│   │   └── Pages/
│   │       └── Cart Page/
│   │           └── btn_ProcerssToCheckout
│   └── Cart/
│       └── item_InCart
│
├── Keywords/
│   └── CustomActions/
│       └── fillShippingFormAndPlaceOrder
│
├── Profiles/
│   └── default
└── Test Listeners/
```

---

## Scenarios

### ✅ Scenario 1 [P1] - Register New Account

**Objective**:  
As a guest user, register a new account to the application, then verify successful registration and login.

**Steps**:
1. Navigate to the registration page.
2. Fill in registration details (email, password, name, etc.).
3. Submit the form.
4. Verify account creation success message.
5. Attempt login using the new credentials.
6. Verify successful login by asserting presence of user-specific UI (e.g., welcome message, account menu).

---

### ✅ Scenario 2 [P1] - Add Jacket to Cart

**Objective**:  
Login to the application, navigate to Men’s > Jackets category, choose the second product, and add it to the cart.

**Steps**:
1. Login using valid credentials.
2. Navigate to “Men's” category.
3. Select “Jackets” subcategory.
4. Scroll to the second product in the list.
5. Click on the product.
6. Add the product to the cart.
7. Assert that the product appears in the cart.

---

### ✅ Scenario 3 [P2] - Checkout from Cart

**Objective**:  
Navigate to the cart, and if it's not empty, proceed to checkout with payment details.

**Steps**:
1. Check if cart has items:
   ```groovy
   if (WebUI.verifyElementPresent(findTestObject('Object Repository/Cart/item_InCart'), 5, FailureHandling.OPTIONAL)) {
       WebUI.click(findTestObject('Object Repository/Header/icon_Cart'))
       WebUI.click(findTestObject('Object Repository/Header/link_ViewCart'))
       WebUI.click(findTestObject('Object Repository/Scenario 3/Pages/Cart Page/btn_ProcerssToCheckout'))
       CustomActions.fillShippingFormAndPlaceOrder(shippingData)
   } else {
       println "You have no items in your shopping cart."
   }
   ```
2. Fill in shipping and payment details via custom keyword: `fillShippingFormAndPlaceOrder()`.
3. Submit order.
4. Verify order confirmation.

---

### ✅ Scenario 4 [P3] - Search for Product "Nike"

**Objective**:  
Login to the application, search for the keyword "Nike", and assert that results are returned.

**Steps**:
1. Login using valid credentials.
2. Use the search bar to enter "Nike".
3. Click search or press Enter.
4. Verify at least one result contains "Nike" in the title or description.
5. Assert the result page is not empty.

---

## Custom Keywords

### `CustomActions.fillShippingFormAndPlaceOrder(Map shippingData)`

Handles form-filling for checkout and placing orders. Accepts a map with keys like:
- `firstName`
- `lastName`
- `address`
- `email`
- `paymentMethod`, etc.

---

## Execution

To execute each scenario:

1. Open Katalon Studio.
2. Select the test case under `Test Cases`.
3. Click on **Run** to execute individually, or group them in a test suite for batch execution.

---

## Notes

- Project uses **Katalon Studio** with **Groovy**.
- Followed Page Object Model using **Object Repository**.
- Uses **FailureHandling.OPTIONAL** for safe checking elements.
- Follows priority-based test planning: P1 (Critical), P2 (High), P3 (Medium).

---

## Author

**DemoProject Team**  
Created for automating an end-to-end user flow of a demo e-commerce site.
