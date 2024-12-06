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
- Feature: Search Functionality
  - Scenario: Search returns relevant results
    - Given the user is on the homepage
    - When the user enters "Marvel" in the search bar
    - And the user clicks the "Search" button
    - Then the search results should display items related to "Marvel"
  
**Chai Test Code:**
```javascript
describe('Search Functionality', function () {
    it('should return relevant results for a search term', async function () {
        await browser.get('https://hotstar-clone.com');
        const searchBar = element(by.id('search'));
        const searchButton = element(by.css('.search-button'));
  
        await searchBar.sendKeys('Marvel');
        await searchButton.click();
  
        const results = element.all(by.css('.search-results .result-item'));
        const firstResultText = await results.first().getText();
  
        expect(results.count()).to.be.greaterThan(0);
        expect(firstResultText).to.include('Marvel');
    });
});
```
  
**Test Case 3: Video Playback**
  
- Feature: Video Playback
  - Scenario: Successful video playback
    - Given the user is on a video detail page
    - When the user clicks the "Play" button
    - Then the video should start playing
    - And the play button should change to a pause button
  
  
**Chai Test Code:**
```javascript
describe('Video Playback', function () {
    it('should start playing the video when play button is clicked', async function () {
        await browser.get('https://hotstar-clone.com/video/123');
        const playButton = element(by.css('.play-button'));
        const videoPlayer = element(by.tagName('video'));
  
        await playButton.click();
        const isPlaying = await videoPlayer.getAttribute('paused');
  
        expect(isPlaying).to.equal('false');
    });
});
  
```
  
**Test Case 4: Subscription Activation**
- Feature: Subscription Activation
 -  Scenario: Successful subscription activation
  -  Given the user is logged in
   - When the user selects the "Premium Plan"
   - And the user completes the payment
   - Then the subscription status should be updated to "Active"
   - And the user should gain access to premium content
  
  
**Chai Test Code:**
```javascript
describe('Subscription Activation', function () {
    it('should activate subscription upon successful payment', async function () {
        await browser.get('https://hotstar-clone.com/subscribe');
        const premiumPlanButton = element(by.css('.premium-plan'));
        const paymentButton = element(by.css('.pay-button'));
        const subscriptionStatus = element(by.css('.subscription-status'));
  
        await premiumPlanButton.click();
        await paymentButton.click();
  
        const statusText = await subscriptionStatus.getText();
        expect(statusText).to.equal('Active');
    });
});
```
## 7.1 References
The following references were used during the development and testing of the Hotstar clone project:
  
IEEE-829-2008 Standard for Software Test Documentation:
  
Link to IEEE Standard
Used as a guideline for creating the software testing document.
Behavior-Driven Development (BDD):
  
Cucumber Documentation on BDD
Cucumber eBooks
Referenced for writing Gherkin-based test cases to ensure test clarity and alignment with user stories.
Chai Assertion Library:
  
Chai.js Documentation
Used for implementing assertions in automated testing scripts.
  
```javascript
```
  
  
  
# Hotstar Clone - Test Cases in BDD Format
  
## 1. User Login
  
### Feature: User Login
#### Scenario: Successful login with valid credentials
- **Given** the user is on the login page
- **When** the user enters "user@example.com" in the email field
- **And** the user enters "Password123" in the password field
- **And** the user clicks the "Login" button
- **Then** the user should be redirected to the homepage
- **And** the username should appear in the header
  
---
  
## 2. Search Functionality
  
### Feature: Search Functionality
#### Scenario: Search returns relevant results
- **Given** the user is on the homepage
- **When** the user enters "Marvel" in the search bar
- **And** the user clicks the "Search" button
- **Then** the search results should display items related to "Marvel"
  
---
  
## 3. Video Playback
  
### Feature: Video Playback
#### Scenario: Successful video playback
- **Given** the user is on a video detail page
- **When** the user clicks the "Play" button
- **Then** the video should start playing
- **And** the play button should change to a pause button
  
---
  
## 4. Subscription Activation
  
### Feature: Subscription Activation
#### Scenario: Successful subscription activation
- **Given** the user is logged in
- **When** the user selects the "Premium Plan"
- **And** the user completes the payment
- **Then** the subscription status should be updated to "Active"
- **And** the user should gain access to premium content
  
---
  
## 5. UI Responsiveness
  
### Feature: UI Responsiveness
#### Scenario: Website adapts to different screen sizes
- **Given** the user is on a mobile device
- **When** the user opens the Hotstar clone website
- **Then** the layout should adjust to fit the screen size
- **And** navigation should remain functional
  