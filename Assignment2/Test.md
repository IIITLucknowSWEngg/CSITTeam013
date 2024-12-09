# Software Testing Document for Nova Digital:

## Test Plan
### Test Plan Identifier
**TP-NovaDigital-001**
This identifier is unique to the Nova Digital website project for tracking purposes. 

### Introduction
**Purpose**
The purpose of this test plan is to validate the functionality, usability, and performance of the Nova Digital website. The tests will ensure that all core features—like video playback, user authentication, search functionality, and subscription management—perform as expected.

**Scope**
The scope includes testing both functional and non-functional requirements of the website, such as:

- Video streaming quality
- Search accuracy
- Subscription flow integration
- Compatibility across browsers and devices

**Objectives**
- Ensure all user-facing features work seamlessly.
- Identify and address defects before production.
- Deliver a high-quality, bug-free website of Nova Digital.

### Test Items
- Authentication System: Login, Registration, Logout
- Search Functionality: Predictive search, keyword matching
- Video Playback: Play, Pause, Resume, Quality Adjustments
- Subscriptions: Plan selection, payment gateway, confirmation
- User Interface: Responsiveness, Layout consistency

### Features to Be Tested
- **Authentication:** Login, logout, and registration.
- **Search Functionality:** Predictive search, keyword matching, and results display.
- **Video Playback:** Play, pause, resume, adjust quality, and full-screen mode.
- **Subscription Activation:** Plan selection, payment integration, and subscription activation.


### Features Not to Be Tested
- Administrative dashboard (if present but not included in user testing scope)
- Future updates or experimental features

### Approach
- **Manual Testing:** Validate basic features like navigation, forms, and responsiveness.
- **Automated Testing:** Use Chai assertions for back-end validation and BDD for feature-level testing.
- **Regression Testing:** Ensure new changes don’t break existing features.
- **Compatibility Testing:** Test on major browsers and devices.

### Pass/Fail Criteria
- A test passes if the expected output matches the actual output.
- A test fails if functionality deviates from expected results or produces errors.

### Suspension and Resumption Criteria
- **Suspension:** Testing will halt if critical defects (e.g., site crashes, broken authentication) are encountered.
- **Resumption:** Testing will resume once critical defects are resolved and verified.

### Testing Tasks
- Prepare test environment and data.
- Write and execute BDD-based test cases.
- Automate key workflows using Chai and Mocha.


### Environmental Needs
- **Hardware:** Desktop, Laptop, Mobile Devices (iOS and Android)
- **Software:** Node.js, Cucumber, Chai, Mocha, BrowserStack for compatibility testing
- **Tools:** Bug tracking software (e.g., Jira), IDE (e.g., VS Code)

### Responsibilities
- **QA Engineers:** Write and execute test cases, log defects.
- **Developers:** Resolve defects and support testing.
- **Test Manager:** Ensure test coverage and report status.

### Staffing and Training Needs
- Team of 2-3 QA engineers familiar with BDD and automated testing.
- Training sessions on using Chai assertions and BDD with Cucumber.

### Risks and Contingencies
- **Risk:** Insufficient time to execute all test cases.
  **Mitigation:** Prioritize critical features.

- **Risk:** Test environment setup delays.
**Mitigation:** Use cloud-based environments if required.

- **Risk:** Browser-specific defects.
**Mitigation:** Use BrowserStack for cross-browser testing.

## Test Cases 
### **Test Case 1: User Login**

```markdown
Feature: User Login
  Scenario: Successful login with valid credentials
    Given the user is on the login page
    When the user enters "user@example.com" in the email field
    And the user enters "Password123" in the password field
    And the user clicks the "Login" button
    Then the user should be redirected to the homepage
    And the username should appear in the header
```

**Chai Test Code:**
```javascript
const { expect } = require('chai');
const { browser, element, by } = require('protractor');

describe('User Login', function () {
    it('should login successfully with valid credentials', async function () {
        await browser.get('https://Nova-Digital.com/login');
        const emailField = element(by.id('email'));
        const passwordField = element(by.id('password'));
        const loginButton = element(by.css('.login-button'));

        await emailField.sendKeys('user@example.com');
        await passwordField.sendKeys('Password123');
        await loginButton.click();

        const usernameHeader = element(by.css('.username'));
        const currentUrl = await browser.getCurrentUrl();
        const usernameText = await usernameHeader.getText();

        expect(currentUrl).to.equal('https://Nova-Digital.com/home');
        expect(usernameText).to.equal('Welcome, User');
    });
}); 
```

### **Test Case 2: Search Functionality**
```markdown
Feature: Search Functionality
  Scenario: Search returns relevant results
    Given the user is on the homepage
    When the user enters "Marvel" in the search bar
    And the user clicks the "Search" button
    Then the search results should display items related to "Marvel"
```

**Chai Test Code:**
```javascript
describe('Search Functionality', function () {
    it('should return relevant results for a search term', async function () {
        await browser.get('https://Nova-Digital.com');
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

### **Test Case 3: Video Playback**

```markdown
Feature: Video Playback
  Scenario: Successful video playback
    Given the user is on a video detail page
    When the user clicks the "Play" button
    Then the video should start playing
    And the play button should change to a pause button
```


**Chai Test Code:**
```javascript
describe('Video Playback', function () {
    it('should start playing the video when play button is clicked', async function () {
        await browser.get('https://Nova-Digital.com/video/123');
        const playButton = element(by.css('.play-button'));
        const videoPlayer = element(by.tagName('video'));

        await playButton.click();
        const isPlaying = await videoPlayer.getAttribute('paused');

        expect(isPlaying).to.equal('false');
    });
});

```

### **Test Case 4: Subscription Activation**

```markdown
Feature: Subscription Activation
  Scenario: Successful subscription activation
    Given the user is logged in
    When the user selects the "Premium Plan"
    And the user completes the payment
    Then the subscription status should be updated to "Active"
    And the user should gain access to premium content
```


```javascript
describe('Subscription Activation', function () {
    it('should activate subscription upon successful payment', async function () {
        await browser.get('https://Nova-Digital.com/subscribe');
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

### **Test Case 5: Scalability- Verify Website Scalability Under High Load**

```markdown
Feature: Scalability Testing
  As a developer
  I want the website to handle increased user load
  So that it performs efficiently under stress

  Scenario: Simulate 1000 concurrent users accessing the homepage API
    Given the server is running
    When 1000 concurrent requests are sent to the homepage API
    Then the server should respond to 95% of the requests successfully
    And the average response time should remain under 2 seconds
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Scalability Testing', function () {
  this.timeout(20000); // Extend timeout for scalability tests
  const server = 'http://localhost:3000'; // Replace with your server URL
  const totalRequests = 1000; // Total number of requests
  const maxResponseTime = 2000; // Maximum acceptable average response time in ms
  const successThreshold = 0.95; // Minimum success rate

  it('should handle 1000 concurrent requests within performance limits', (done) => {
    const promises = [];
    const startTime = new Date().getTime(); // Record the start time

    for (let i = 0; i < totalRequests; i++) {
      promises.push(
        chai.request(server)
          .get('/homepage') // Replace with your homepage endpoint
          .then((res) => res.status === 200 ? 1 : 0) // Count successful requests
          .catch(() => 0) // Count failed requests
      );
    }

    Promise.all(promises).then((results) => {
      const endTime = new Date().getTime(); // Record the end time
      const successfulRequests = results.reduce((sum, value) => sum + value, 0);
      const failedRequests = totalRequests - successfulRequests;
      const averageResponseTime = (endTime - startTime) / totalRequests;

      // Assertions
      expect(successfulRequests / totalRequests).to.be.greaterThan(successThreshold, 'Success rate is below 95%');
      expect(failedRequests).to.be.lessThan(totalRequests * 0.05, 'Failed requests exceed 5%');
      expect(averageResponseTime).to.be.lessThan(maxResponseTime, 'Average response time exceeds 2 seconds');

      done();
    });
  });
});
```





## References
The following references were used during the development and testing of the Nova Digital project:

**IEEE-829-2008 Standard for Software Test Documentation:**
- Used as a guideline for creating the software testing document.

**Behavior-Driven Development (BDD):**
- Cucumber Documentation on BDD
- Cucumber eBooks

**Chai Assertion Library:**
- Chai.js Documentation
- Used for implementing assertions in automated testing scripts.

**ChatGPT by OpenAI:**
- Assistance in creating the outline for the software testing document along with codes.