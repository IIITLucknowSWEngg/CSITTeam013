# Software Testing Document for Nova Digital:

## 1.Test Plan
### 1.1 Test Plan Identifier
**TP-HotstarClone-001**
This identifier is unique to the Hotstar website clone project for tracking purposes. 

### 1.2 Introduction
**Purpose**
The purpose of this test plan is to validate the functionality, usability, and performance of the Hotstar clone website. The tests will ensure that all core features—like video playback, user authentication, search functionality, and subscription management—perform as expected.

**Scope**
The scope includes testing both functional and non-functional requirements of the website, such as:

- Video streaming quality
- Search accuracy
- Subscription flow integration
- Compatibility across browsers and devices

**Objectives**
- Ensure all user-facing features work seamlessly.
- Identify and address defects before production.
- Deliver a high-quality, bug-free website clone of Hotstar.

### 1.3 Test Items
- Authentication System: Login, Registration, Logout
- Search Functionality: Predictive search, keyword matching
- Video Playback: Play, Pause, Resume, Quality Adjustments
- Subscriptions: Plan selection, payment gateway, confirmation
- User Interface: Responsiveness, Layout consistency

### 1.4 Features to Be Tested
- Video streaming and playback controls
- User profile and preferences management
- Dynamic search and suggestion display
- Payment gateway integration for subscriptions
- Multi-device compatibility

Authentication: Login, logout, and registration.
Search Functionality: Predictive search, keyword matching, and results display.
Video Playback: Play, pause, resume, adjust quality, and full-screen mode.
Subscription Flow: Plan selection, payment integration, and subscription activation.
User Profile Management: Update profile information, view subscriptions, and logout.
UI Responsiveness: Consistent layout on various devices and browsers.


### 1.5 Features Not to Be Tested
- Administrative dashboard (if present but not included in user testing scope)
- Future updates or experimental features

### 1.6 Approach
- **Manual Testing:** Validate basic features like navigation, forms, and responsiveness.
- **Automated Testing:** Use Chai assertions for back-end validation and BDD for feature-level testing.
- **Regression Testing:** Ensure new changes don’t break existing features.
- **Compatibility Testing:** Test on major browsers and devices.

### 1.7 Pass/Fail Criteria
- A test passes if the expected output matches the actual output.
- A test fails if functionality deviates from expected results or produces errors.

### 1.8 Suspension and Resumption Criteria
- **Suspension:** Testing will halt if critical defects (e.g., site crashes, broken authentication) are encountered.
- **Resumption:** Testing will resume once critical defects are resolved and verified.

### 1.9 Test Deliverables
- Test Cases Document (BDD-based)
- Test Execution Report
- Defect Log Report
- Test Summary Report

### 1.10 Testing Tasks
- Prepare test environment and data.
- Write and execute BDD-based test cases.
- Automate key workflows using Chai and Mocha.
- Log and track defects in a bug tracking system.

### 1.11 Environmental Needs
- **Hardware:** Desktop, Laptop, Mobile Devices (iOS and Android)
- **Software:** Node.js, Cucumber, Chai, Mocha, BrowserStack for compatibility testing
- **Tools:** Bug tracking software (e.g., Jira), IDE (e.g., VS Code)

### 1.12 Responsibilities
- **QA Engineers:** Write and execute test cases, log defects.
- **Developers:** Resolve defects and support testing.
- **Test Manager:** Ensure test coverage and report status.

### 1.13 Staffing and Training Needs
- Team of 2-3 QA engineers familiar with BDD and automated testing.
- Training sessions on using Chai assertions and BDD with Cucumber.

### 1.15 Risks and Contingencies
- **Risk:** Insufficient time to execute all test cases.
  **Mitigation:** Prioritize critical features.

- **Risk:** Test environment setup delays.
**Mitigation:** Use cloud-based environments if required.
- **Risk:** Browser-specific defects.
**Mitigation:** Use BrowserStack for cross-browser testing.


## 2. Test Design Specification
## 2.1 Test Design Identifier
TD-HotstarClone-001
This identifier represents the test design for the Hotstar clone project, encompassing functional and non-functional requirements.

## 2.4 Test Cases 
**Test Case 1: User Login**

* Feature: User Login
* Scenario: Successful login with valid credentials
    * Given the user is on the login page
    * When the user enters "user@example.com" in the email field
    * And the user enters "Password123" in the password field
    * And the user clicks the "Login" button
    * Then the user should be redirected to the homepage
    * And the username should appear in the header

**Chai Test Code:**
```javascript
const { expect } = require('chai');
const { browser, element, by } = require('protractor');

describe('User Login', function () {
    it('should login successfully with valid credentials', async function () {
        await browser.get('https://hotstar-clone.com/login');
        const emailField = element(by.id('email'));
        const passwordField = element(by.id('password'));
        const loginButton = element(by.css('.login-button'));

        await emailField.sendKeys('user@example.com');
        await passwordField.sendKeys('Password123');
        await loginButton.click();

        const usernameHeader = element(by.css('.username'));
        const currentUrl = await browser.getCurrentUrl();
        const usernameText = await usernameHeader.getText();

        expect(currentUrl).to.equal('https://hotstar-clone.com/home');
        expect(usernameText).to.equal('Welcome, User');
    });
}); 
```

**Test Case 2: Search Functionality**
Feature: Search Functionality
  Scenario: Search returns relevant results
    Given the user is on the homepage
    When the user enters "Marvel" in the search bar
    And the user clicks the "Search" button
    Then the search results should display items related to "Marvel"





```javascript
```