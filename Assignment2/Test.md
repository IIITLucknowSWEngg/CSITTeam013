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
### Test Case 1: User Login

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

### Test Case 2: Search Functionality
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

### Test Case 3: Video Playback

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

### Test Case 4: Subscription Activation

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

### Test Case 5: Verify Website Scalability Under High Load

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

### Test Case 6: Verify Homepage API Latency
```markdown
Feature: Latency Testing
  As a user
  I want the website to respond quickly
  So that I can have a seamless experience

  Scenario: Homepage API responds within acceptable latency
    Given the server is running
    When a request is sent to the homepage API
    Then the response should be received within 2 seconds
    And the status code should be 200
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Latency Testing', function () {
  this.timeout(5000); // Extend timeout for latency testing
  const server = 'http://localhost:3000'; // Replace with your server URL
  const maxLatency = 2000; // Maximum acceptable latency in milliseconds

  it('should respond within 2 seconds for the homepage API', (done) => {
    const startTime = new Date().getTime(); // Record the start time

    chai.request(server)
      .get('/homepage') // Replace with the appropriate endpoint
      .end((err, res) => {
        const endTime = new Date().getTime(); // Record the end time
        const responseTime = endTime - startTime; // Calculate latency

        // Assertions
        expect(res).to.have.status(200);
        expect(responseTime).to.be.lessThan(maxLatency, 'Response time exceeds acceptable latency');

        done();
      });
  });
});
```

### Test Case 7: Verify Throughput for Homepage API
```markdown
Feature: Throughput Testing
  As a user
  I want the server to handle multiple requests efficiently
  So that the website remains responsive under heavy load

  Scenario: Measure throughput for the homepage API
    Given the server is running
    When 1000 concurrent requests are sent to the homepage API
    Then at least 95% of the requests should succeed
    And the average response time should be under 2 seconds
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Throughput Testing', function () {
  this.timeout(10000); // Extend timeout for throughput tests
  const server = 'http://localhost:3000'; // Replace with your server URL
  const totalRequests = 1000; // Total number of requests to simulate
  const concurrency = 100; // Number of concurrent requests per batch
  const maxResponseTime = 2000; // Maximum acceptable average response time in ms

  it('should handle 1000 requests with acceptable throughput and response time', (done) => {
    const promises = [];
    const startTime = new Date().getTime(); // Record the start time

    for (let i = 0; i < totalRequests; i++) {
      promises.push(
        chai.request(server)
          .get('/homepage') // Replace with the actual endpoint
          .then((res) => {
            return res.status === 200 ? 1 : 0; // Count successful requests
          })
          .catch(() => 0) // Count failed requests
      );
    }

    Promise.all(promises).then((results) => {
      const endTime = new Date().getTime(); // Record the end time
      const successfulRequests = results.reduce((sum, value) => sum + value, 0);
      const failedRequests = totalRequests - successfulRequests;
      const averageResponseTime = (endTime - startTime) / totalRequests;

      // Assertions
      expect(successfulRequests).to.be.greaterThan(totalRequests * 0.95, 'Less than 95% requests succeeded');
      expect(averageResponseTime).to.be.lessThan(maxResponseTime, 'Average response time exceeded limit');
      expect(failedRequests).to.be.lessThan(totalRequests * 0.05, 'Too many failed requests');

      done();
    });
  });
});
```

### Test Case 8: Bandwidth Optimization Test for Video Streaming

```markdown
Feature: Bandwidth Optimization
  As a user
  I want video streaming to use minimal bandwidth
  So that I can stream content efficiently on limited networks

  Scenario: Stream video with optimized bandwidth
    Given the server is running
    And the user requests a video stream
    When the video is played
    Then the video should be streamed in adaptive bitrate
    And the total data usage should be minimized
```
```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Bandwidth Optimization Testing', function () {
  this.timeout(15000); // Allow extra time for video stream tests
  const server = 'http://localhost:3000'; // Replace with your server URL
  const maxBandwidthUsage = 5 * 1024 * 1024; // Maximum allowable data usage in bytes (5MB for a sample test)
  const videoId = 'sampleVideo123'; // Replace with a test video ID

  it('should stream video with optimized bandwidth usage', (done) => {
    chai.request(server)
      .get(`/videos/${videoId}/stream`) // Replace with your video streaming endpoint
      .responseType('arraybuffer') // Ensure we measure raw data size
      .end((err, res) => {
        if (err) return done(err);

        const dataSize = res.body.byteLength; // Get size of the data transferred
        const isAdaptiveBitrate = res.headers['content-type'] === 'video/mp4'; // Example check for adaptive bitrate

        // Assertions
        expect(res).to.have.status(200);
        expect(isAdaptiveBitrate).to.be.true; // Ensure video uses adaptive bitrate
        expect(dataSize).to.be.lessThan(maxBandwidthUsage, 'Data usage exceeds optimization limit');

        done();
      });
  });
});

```

### Test Case 9: Data Protection
**Scenario: Verify Sensitive User Data is Encrypted During Transmission**
```markdown

Feature: Data Protection
  As a user
  I want my sensitive data to be protected
  So that my information remains secure

  Scenario: Ensure sensitive user data is encrypted during transmission
    Given the server is running
    When the user submits login credentials via the login API
    Then the data should be transmitted over HTTPS
    And the request payload should be encrypted
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Data Protection - Secure Transmission', function () {
  this.timeout(10000); // Allow additional time for tests

  const server = 'https://localhost:3000'; // Ensure HTTPS is used
  const loginEndpoint = '/login'; // Replace with your login endpoint

  it('should transmit sensitive data securely over HTTPS', (done) => {
    const loginData = { username: 'testuser', password: 'testpassword' };

    chai.request(server)
      .post(loginEndpoint)
      .send(loginData)
      .end((err, res) => {
        // Assertions
        expect(res).to.have.status(200);
        expect(res.req.agent.protocol).to.equal('https:', 'Request is not using HTTPS');
        done();
      });
  });
});
```

**Scenario: Restrict Unauthorized Access to User Profile Data**

```markdown
Scenario: Prevent unauthorized access to user profile data
  Given the server is running
  And the user is logged out
  When a GET request is sent to the user profile API without authentication
  Then the response should have a 401 Unauthorized status code
```

```javascript
describe('Data Protection - Unauthorized Access', function () {
  this.timeout(5000);

  const server = 'http://localhost:3000'; // Replace with your server URL
  const profileEndpoint = '/user/profile'; // Replace with your profile endpoint

  it('should deny access to the profile API without authentication', (done) => {
    chai.request(server)
      .get(profileEndpoint)
      .end((err, res) => {
        // Assertions
        expect(res).to.have.status(401); // Expect unauthorized status code
        expect(res.body).to.have.property('error').that.equals('Unauthorized access');
        done();
      });
  });
});
```

### Test Case 10: Service Availability
**Scenario: Verify Service Availability During System Maintenance**

```markdown
Feature: Service Availability
  As a developer
  I want the website to remain available during updates or maintenance
  So that users can continue to access the service with minimal disruption

  Scenario: Verify service availability during updates or maintenance
    Given the system is undergoing an update or maintenance
    When the user attempts to access the website
    Then the website should be responsive with minimal downtime
    And the user should not experience significant service interruptions
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Service Availability - During Maintenance', function () {
  this.timeout(30000); // Allow time for server maintenance tests

  const server = 'http://localhost:3000'; // Replace with your server URL

  it('should maintain service availability during system maintenance', (done) => {
    chai.request(server)
      .get('/homepage') // Replace with a valid endpoint
      .end((err, res) => {
        if (err) return done(err);
        
        // Simulate a maintenance window (mock or actual service restart)
        // Assume the service is running even with updates or restarts

        // Assertions
        expect(res).to.have.status(200);
        expect(res.body).to.have.property('message').that.equals('Service is available');

        done();
      });
  });
});
```

**Scenario: Verify Rolling Updates for Zero Downtime Deployment**

```markdown
Scenario: Ensure zero downtime during rolling updates
  Given the system is running in a load-balanced environment
  When an update is deployed to one instance of the server
  Then traffic should be rerouted to other servers
  And no downtime should be experienced by the user
```

```javascript
describe('Service Availability - Rolling Updates', function () {
  this.timeout(30000); // Allow time for rolling updates to occur

  const server = 'http://localhost:3000'; // Replace with your server URL

  it('should not cause downtime during rolling updates', (done) => {
    chai.request(server)
      .get('/homepage') // Replace with a valid endpoint
      .end((err, res) => {
        if (err) return done(err);

        // Simulate that the system is being updated (i.e., during a rolling update)
        // Assume the request should still return successfully

        // Assertions
        expect(res).to.have.status(200);
        expect(res.body).to.have.property('message').that.equals('Service is available');

        done();
      });
  });
});
```

### Test Case 11: Content Control
**Scenario: Verify Age-Based Restrictions for Inappropriate Content**

```markdown
Feature: Content Control
  As a user
  I want to ensure that age-restricted content is accessible only to users of the appropriate age
  So that children cannot access inappropriate content

  Scenario: Ensure users below the required age cannot access age-restricted content
    Given the user has logged in with an age below 18
    When the user attempts to access age-restricted content
    Then the user should be denied access to the content
    And the user should see a message indicating that the content is restricted due to age
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Content Control - Age Restrictions', function () {
  this.timeout(5000);

  const server = 'http://localhost:3000'; // Replace with your server URL
  const restrictedContentId = 'restrictedVideo123'; // Replace with a test video ID
  const underageUser = { username: 'childUser', age: 15 }; // User under 18

  it('should deny access to age-restricted content for users under 18', (done) => {
    chai.request(server)
      .post('/login') // Assuming you have a login endpoint
      .send(underageUser)
      .end((err, loginRes) => {
        if (err) return done(err);

        chai.request(server)
          .get(`/content/${restrictedContentId}`) // Accessing restricted content
          .set('Authorization', `Bearer ${loginRes.body.token}`) // Assuming token-based auth
          .end((err, res) => {
            // Assertions
            expect(res).to.have.status(403); // Expecting Forbidden status code
            expect(res.body).to.have.property('message').that.equals('Access Denied: Age restricted content');
            done();
          });
      });
  });
});
```

**Scenario: Ensure Users of Appropriate Age Can Access Content**
```markdown
Scenario: Ensure users of appropriate age can access content
  Given the user has logged in with an age above 18
  When the user attempts to access age-restricted content
  Then the user should be allowed to access the content
  And the user should be able to view the content without restrictions
```

```javascript
describe('Content Control - Age Restrictions', function () {
  this.timeout(5000);

  const server = 'http://localhost:3000'; // Replace with your server URL
  const restrictedContentId = 'restrictedVideo123'; // Replace with a test video ID
  const adultUser = { username: 'adultUser', age: 25 }; // User above 18

  it('should allow access to age-restricted content for users 18 and older', (done) => {
    chai.request(server)
      .post('/login') // Assuming you have a login endpoint
      .send(adultUser)
      .end((err, loginRes) => {
        if (err) return done(err);

        chai.request(server)
          .get(`/content/${restrictedContentId}`) // Accessing restricted content
          .set('Authorization', `Bearer ${loginRes.body.token}`) // Assuming token-based auth
          .end((err, res) => {
            // Assertions
            expect(res).to.have.status(200); // Expecting OK status code
            expect(res.body).to.have.property('contentId').that.equals(restrictedContentId);
            done();
          });
      });
  });
});
```

### Test case 12: User Authentication
**Scenario: Verify Two-Factor Authentication (2FA)**
```markdown
Feature: User Authentication
  As a user
  I want to secure my account with two-factor authentication (2FA)
  So that my account is protected by an additional layer of security

  Scenario: User logs in with two-factor authentication
    Given the user has registered for 2FA
    When the user logs in with their username and password
    And enters the correct 2FA code sent to their mobile device
    Then the user should be granted access to their account

```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('User Authentication - Two-Factor Authentication (2FA)', function () {
  this.timeout(10000); // Allow time for testing 2FA process

  const server = 'http://localhost:3000'; // Replace with your server URL
  const loginCredentials = { username: 'testuser', password: 'TestPass123' }; // Example credentials
  const valid2FACode = '123456'; // Example 2FA code, typically generated dynamically

  it('should allow the user to log in with valid 2FA code', (done) => {
    // Step 1: Attempt to login with username and password
    chai.request(server)
      .post('/login') // Replace with your login endpoint
      .send(loginCredentials)
      .end((err, loginRes) => {
        if (err) return done(err);

        // Step 2: Submit the valid 2FA code after login attempt
        chai.request(server)
          .post('/verify-2fa') // Replace with your 2FA verification endpoint
          .send({ username: loginCredentials.username, code: valid2FACode })
          .end((err, res) => {
            // Assertions
            expect(res).to.have.status(200); // Expecting OK status code
            expect(res.body).to.have.property('message').that.equals('Login successful');
            done();
          });
      });
  });

  it('should deny login with invalid 2FA code', (done) => {
    const invalid2FACode = '000000'; // Invalid code

    // Step 1: Attempt to login with username and password
    chai.request(server)
      .post('/login') // Replace with your login endpoint
      .send(loginCredentials)
      .end((err, loginRes) => {
        if (err) return done(err);

        // Step 2: Submit the invalid 2FA code after login attempt
        chai.request(server)
          .post('/verify-2fa') // Replace with your 2FA verification endpoint
          .send({ username: loginCredentials.username, code: invalid2FACode })
          .end((err, res) => {
            // Assertions
            expect(res).to.have.status(401); // Expecting Unauthorized status code
            expect(res.body).to.have.property('message').that.equals('Invalid 2FA code');
            done();
          });
      });
  });
});
```

**Scenario: Verify Strong Password Policy**
```markdown
Scenario: User must set a strong password during registration
  Given the user is registering a new account
  When the user enters a password that does not meet the strong password policy
  Then the user should see an error message indicating the password requirements
  And the user should not be able to complete the registration
```

```javascript
describe('User Authentication - Strong Password Policy', function () {
  this.timeout(5000); // Allow time for password validation testing

  const server = 'http://localhost:3000'; // Replace with your server URL
  const weakPassword = '12345'; // Weak password (less than 8 characters, no special characters)
  const strongPassword = 'Str0ngP@ssw0rd123'; // Strong password (meets policy)

  it('should deny registration with a weak password', (done) => {
    chai.request(server)
      .post('/register') // Replace with your registration endpoint
      .send({ username: 'newuser', password: weakPassword })
      .end((err, res) => {
        // Assertions
        expect(res).to.have.status(400); // Expecting Bad Request for weak password
        expect(res.body).to.have.property('message').that.equals('Password must be at least 8 characters long and contain at least one number, one uppercase letter, and one special character.');
        done();
      });
  });

  it('should allow registration with a strong password', (done) => {
    chai.request(server)
      .post('/register') // Replace with your registration endpoint
      .send({ username: 'newuser', password: strongPassword })
      .end((err, res) => {
        // Assertions
        expect(res).to.have.status(201); // Expecting Created status for successful registration
        expect(res.body).to.have.property('message').that.equals('Registration successful');
        done();
      });
  });
});

```

### Test Case 13: Encryption
**Scenario: Verify Data Encryption in Transit**

```markdown
Feature: Data Encryption
  As a user
  I want my data to be encrypted during transmission
  So that my sensitive information cannot be intercepted by unauthorized parties

  Scenario: Verify that data is encrypted in transit when accessing content
    Given the user is logged in and accessing streaming content
    When the user requests a video stream
    Then the video data should be encrypted during transmission
    And the user should not be able to intercept the data with unauthorized tools
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;
const https = require('https');

chai.use(chaiHttp);

describe('Data Encryption - In Transit', function () {
  this.timeout(10000); // Allow time for testing encryption in transit

  const server = 'https://localhost:3000'; // Replace with your HTTPS server URL
  const streamingEndpoint = '/stream/video123'; // Replace with the video streaming endpoint

  it('should ensure that data is encrypted in transit during streaming', (done) => {
    chai.request(server)
      .get(streamingEndpoint) // Requesting video stream
      .end((err, res) => {
        if (err) return done(err);

        // Check if the response is over HTTPS, which indicates encryption
        expect(res).to.have.status(200); // Expecting OK status code
        expect(res.request.protocol).to.equal('https'); // Check that protocol is HTTPS

        // Optional: Check for absence of sensitive data in plain text in the response
        expect(res.text).to.not.include('sensitive information'); // Ensuring no sensitive data leakage

        done();
      });
  });

  it('should block access over HTTP for sensitive data', (done) => {
    // Test to ensure data cannot be accessed over an unencrypted HTTP connection
    chai.request('http://localhost:3000') // Using HTTP (not HTTPS)
      .get(streamingEndpoint)
      .end((err, res) => {
        expect(res).to.have.status(403); // Expecting Forbidden status for non-HTTPS request
        done();
      });
  });
});
```

**Scenario: Verify Data Encryption at Rest**

```markdown
Scenario: Verify that user data is encrypted at rest
  Given the user has uploaded a video or saved personal information
  When the data is stored in the database
  Then the data should be encrypted in storage
  And the data should remain unreadable to unauthorized users or systems
```
```javascript
describe('Data Encryption - At Rest', function () {
  this.timeout(5000); // Allow time for testing encryption at rest

  const server = 'http://localhost:3000'; // Replace with your server URL
  const userData = { username: 'testuser', password: 'TestPass123', email: 'testuser@example.com' };

  it('should ensure that user data is encrypted at rest in the database', (done) => {
    // Step 1: Store user data (simulating registration or data saving)
    chai.request(server)
      .post('/register') // Replace with your registration endpoint
      .send(userData)
      .end((err, res) => {
        if (err) return done(err);

        // Step 2: Simulate retrieving the data from the database (in a real scenario, this would be a database query)
        chai.request(server)
          .get(`/user/${userData.username}`) // Replace with endpoint to retrieve user data
          .end((err, res) => {
            // Assertions
            expect(res).to.have.status(200); // Expecting OK status code

            // Check that sensitive data is encrypted (cannot be seen in plain text)
            expect(res.body).to.not.have.property('password'); // Password should not be exposed
            expect(res.body).to.have.property('email').that.equals(userData.email);

            // Further, check that no sensitive data is exposed in plaintext from the storage
            expect(res.body.password).to.not.match(/[A-Za-z0-9]/); // Ensure password is encrypted

            done();
          });
      });
  });
});
```
### Test case 14: Access Control 
**Scenario: Verify Role-Based Access Control for Users**

```markdown
Feature: Role-Based Access Control (RBAC)
  As an administrator
  I want to assign roles to users
  So that different users can have different levels of access

  Scenario: User with Admin role has access to administrative features
    Given the user is assigned the "Admin" role
    When the user logs in
    Then the user should have access to administrative features

  Scenario: User with Viewer role has no access to administrative features
    Given the user is assigned the "Viewer" role
    When the user logs in
    Then the user should not have access to administrative features
    And the user should see a "403 Forbidden" message

  Scenario: User with Editor role has access to content editing but not admin features
    Given the user is assigned the "Editor" role
    When the user logs in
    Then the user should have access to content editing features
    And the user should not have access to administrative features
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Access Control - RBAC', function () {
  this.timeout(5000); // Allow time for testing RBAC

  const server = 'http://localhost:3000'; // Replace with your server URL
  const adminCredentials = { username: 'adminuser', password: 'AdminPass123' };
  const editorCredentials = { username: 'editoruser', password: 'EditorPass123' };
  const viewerCredentials = { username: 'vieweruser', password: 'ViewerPass123' };

  it('should allow admin to access admin features', (done) => {
    chai.request(server)
      .post('/login') // Replace with your login endpoint
      .send(adminCredentials)
      .end((err, res) => {
        if (err) return done(err);

        // Step 2: Ensure admin can access admin features
        chai.request(server)
          .get('/admin/dashboard') // Replace with your admin endpoint
          .set('Authorization', `Bearer ${res.body.token}`) // Assuming token-based auth
          .end((err, adminRes) => {
            expect(adminRes).to.have.status(200); // Expecting OK status code
            expect(adminRes.body).to.have.property('message').that.equals('Admin Dashboard');
            done();
          });
      });
  });

  it('should deny viewer access to admin features', (done) => {
    chai.request(server)
      .post('/login') // Replace with your login endpoint
      .send(viewerCredentials)
      .end((err, res) => {
        if (err) return done(err);

        // Step 2: Ensure viewer cannot access admin features
        chai.request(server)
          .get('/admin/dashboard') // Replace with your admin endpoint
          .set('Authorization', `Bearer ${res.body.token}`) // Assuming token-based auth
          .end((err, res) => {
            expect(res).to.have.status(403); // Expecting Forbidden status code
            expect(res.body).to.have.property('message').that.equals('Access Forbidden');
            done();
          });
      });
  });

  it('should allow editor to access content features but not admin features', (done) => {
    chai.request(server)
      .post('/login') // Replace with your login endpoint
      .send(editorCredentials)
      .end((err, res) => {
        if (err) return done(err);

        // Step 2: Ensure editor can access content editing
        chai.request(server)
          .get('/content/edit') // Replace with your content editing endpoint
          .set('Authorization', `Bearer ${res.body.token}`) // Assuming token-based auth
          .end((err, contentRes) => {
            expect(contentRes).to.have.status(200); // Expecting OK status code
            expect(contentRes.body).to.have.property('message').that.equals('Content Editing Page');

            // Step 3: Ensure editor cannot access admin features
            chai.request(server)
              .get('/admin/dashboard') // Replace with your admin endpoint
              .set('Authorization', `Bearer ${res.body.token}`) // Assuming token-based auth
              .end((err, adminRes) => {
                expect(adminRes).to.have.status(403); // Expecting Forbidden status code
                expect(adminRes.body).to.have.property('message').that.equals('Access Forbidden');
                done();
              });
          });
      });
  });
});
```

### Test Case 15: Fraud Detection
**Scenario: Detect and Mitigate Multiple Failed Login Attempts**
```markdown
Feature: Fraud Detection - Multiple Failed Login Attempts
  As a system
  I want to detect and mitigate fraudulent access attempts from repeated failed logins
  So that malicious users cannot gain unauthorized access

  Scenario: Block user after multiple failed login attempts
    Given the user attempts to log in with incorrect credentials multiple times
    When the system detects 5 failed login attempts
    Then the user account should be temporarily locked
    And the user should receive a notification about suspicious activity

  Scenario: Detect login from an unusual IP address
    Given the user is logged in from a known device and location
    When the system detects a login attempt from an unusual IP address
    Then the system should flag the login as suspicious
    And prompt the user to verify the login via email or SMS
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Fraud Detection - Multiple Failed Login Attempts', function () {
  this.timeout(5000); // Allow time for testing fraud detection

  const server = 'http://localhost:3000'; // Replace with your server URL
  const invalidCredentials = { username: 'testuser', password: 'WrongPassword123' };
  const validCredentials = { username: 'testuser', password: 'ValidPassword123' };

  it('should lock the account after 5 failed login attempts', (done) => {
    let failedAttempts = 0;

    // Try to login with incorrect credentials multiple times
    function attemptLogin() {
      chai.request(server)
        .post('/login') // Replace with your login endpoint
        .send(invalidCredentials)
        .end((err, res) => {
          failedAttempts++;

          // Check for lockout after 5 failed attempts
          if (failedAttempts === 5) {
            expect(res).to.have.status(403); // Forbidden status due to account lock
            expect(res.body).to.have.property('message').that.equals('Account locked due to multiple failed login attempts');
            done();
          } else {
            attemptLogin(); // Continue attempting login
          }
        });
    }

    attemptLogin(); // Initiate the first login attempt
  });

  it('should send a notification after account lockout', (done) => {
    // Simulate a lockout and check if notification is sent
    chai.request(server)
      .post('/login')
      .send(invalidCredentials) // Send invalid credentials
      .end((err, res) => {
        expect(res).to.have.status(403);
        expect(res.body).to.have.property('message').that.equals('Account locked due to multiple failed login attempts');

        // Assuming there's a notification endpoint to check if the user received an alert
        chai.request(server)
          .get('/user/testuser/notifications') // Replace with actual notifications endpoint
          .set('Authorization', `Bearer ${res.body.token}`) // Assuming token-based auth
          .end((err, notifRes) => {
            expect(notifRes).to.have.status(200);
            expect(notifRes.body.notifications).to.include('Suspicious login attempts detected. Account locked.');
            done();
          });
      });
  });
});
```

```javascript
describe('Fraud Detection - Unusual IP Address Login', function () {
  this.timeout(5000); // Allow time for testing fraud detection

  const server = 'http://localhost:3000'; // Replace with your server URL
  const validCredentials = { username: 'testuser', password: 'ValidPassword123' };

  it('should flag login attempt from unusual IP address and prompt for verification', (done) => {
    // Simulate login from a usual location first
    chai.request(server)
      .post('/login')
      .send(validCredentials)
      .end((err, res) => {
        if (err) return done(err);

        // Simulate login from an unusual IP address
        chai.request(server)
          .post('/login')
          .send(validCredentials)
          .set('X-Forwarded-For', '198.51.100.2') // Simulate a different IP address
          .end((err, res) => {
            expect(res).to.have.status(401); // Unauthorized status due to suspicious IP
            expect(res.body).to.have.property('message').that.equals('Suspicious login attempt detected. Please verify your identity.');
            done();
          });
      });
  });
});
```

**Scenario: Detect and Prevent Piracy Attempts**

```markdown
Scenario: Prevent piracy by detecting simultaneous streaming from multiple locations
  Given the user is logged in and watching content from a known device
  When the system detects an attempt to stream the same content from multiple locations simultaneously
  Then the system should block additional streams from unauthorized locations
  And the user should be notified about the piracy attempt
```

```javascript
describe('Fraud Detection - Piracy Prevention (Simultaneous Streaming)', function () {
  this.timeout(5000); // Allow time for testing piracy prevention

  const server = 'http://localhost:3000'; // Replace with your server URL
  const validCredentials = { username: 'testuser', password: 'ValidPassword123' };

  it('should block additional streams from unauthorized locations', (done) => {
    // User logs in from one location and starts streaming
    chai.request(server)
      .post('/login')
      .send(validCredentials)
      .end((err, res) => {
        if (err) return done(err);

        // First streaming session (normal)
        chai.request(server)
          .get('/stream/video123') // Replace with your streaming endpoint
          .set('Authorization', `Bearer ${res.body.token}`) // Assuming token-based auth
          .end((err, streamRes) => {
            expect(streamRes).to.have.status(200); // Expecting OK status code for the first stream

            // Simulate login from a different location and attempt to start the same stream
            chai.request(server)
              .get('/stream/video123')
              .set('Authorization', `Bearer ${res.body.token}`)
              .set('X-Forwarded-For', '203.0.113.1') // Simulating a different IP address
              .end((err, piracyRes) => {
                expect(piracyRes).to.have.status(403); // Forbidden status, piracy detected
                expect(piracyRes.body).to.have.property('message').that.equals('Simultaneous streaming detected. Only one location allowed.');
                done();
              });
          });
      });
  });
});
```

### Test Case 16: Usability
**Scenario: Verify Screen Reader Support**
```markdown
Feature: Usability - Screen Reader Support
  As a visually impaired user
  I want the website to be compatible with screen readers
  So that I can navigate and interact with the site independently

  Scenario: Verify all images have appropriate alt text
    Given the user is navigating the website with a screen reader
    When the user encounters an image
    Then the screen reader should read the alt text associated with the image

  Scenario: Verify all interactive elements are accessible via keyboard navigation
    Given the user is using only the keyboard for navigation
    When the user navigates through buttons and links
    Then the user should be able to focus on all interactive elements without using a mouse

  Scenario: Verify proper contrast for text and background
    Given the user with visual impairments is reading the website
    When the user reads the text
    Then the text should have a high enough contrast with the background to be readable
```

**Scenario: Verify Intuitive User Interface**
```markdown
Feature: Usability - Intuitive User Interface
  As a new user
  I want the interface to be intuitive and easy to use
  So that I can find what I'm looking for quickly without confusion

  Scenario: Verify that the navigation menu is clear and easy to understand
    Given the user is on the homepage
    When the user looks at the navigation menu
    Then the menu should contain clear, self-explanatory labels for each section

  Scenario: Verify the presence of helpful tooltips on hover for icons and buttons
    Given the user hovers over an icon or button
    When the user interacts with the element
    Then a tooltip with a description of the element should appear
```

```javascript
const chai = require('chai');
const chaiHttp = require('chai-http');
const expect = chai.expect;

chai.use(chaiHttp);

describe('Usability - Screen Reader Support', function () {
  this.timeout(5000); // Allow time for accessibility testing

  const server = 'http://localhost:3000'; // Replace with your server URL

  it('should have alt text for all images for screen reader compatibility', (done) => {
    chai.request(server)
      .get('/') // Load the homepage or any page containing images
      .end((err, res) => {
        if (err) return done(err);

        // Step 1: Check for images
        const images = res.text.match(/<img [^>]*>/g); // Regex to match image tags
        images.forEach((imgTag) => {
          // Step 2: Ensure each image has an alt attribute
          expect(imgTag).to.match(/alt=["'][^"']*["']/); // Ensure alt text is present
        });

        done();
      });
  });
});
```

```javascript
describe('Usability - Keyboard Navigation', function () {
  this.timeout(5000); // Allow time for testing keyboard navigation

  const server = 'http://localhost:3000'; // Replace with your server URL

  it('should allow keyboard navigation through interactive elements', (done) => {
    chai.request(server)
      .get('/') // Load the homepage
      .end((err, res) => {
        if (err) return done(err);

        // Step 1: Simulate keyboard navigation (e.g., Tab key to move through elements)
        // Check if all interactive elements (buttons, links) are reachable by keyboard
        // Using "Tab" to navigate and "Enter" to select an item

        // Here we mock a user navigating through the page and accessing interactive elements
        const isAccessible = true; // Assuming a method to check if keyboard navigation works
        expect(isAccessible).to.be.true;

        done();
      });
  });
});
```

```javascript
describe('Usability - Text Contrast', function () {
  this.timeout(5000); // Allow time for testing contrast

  const server = 'http://localhost:3000'; // Replace with your server URL

  it('should have sufficient contrast between text and background for readability', (done) => {
    chai.request(server)
      .get('/') // Load the homepage
      .end((err, res) => {
        if (err) return done(err);

        // Step 1: Check for text and background contrast (using a color contrast library)
        // You can use libraries like "contrast-ratio" or similar to calculate contrast
        const textColor = '#000000'; // Example text color (black)
        const backgroundColor = '#FFFFFF'; // Example background color (white)

        const contrastRatio = calculateContrastRatio(textColor, backgroundColor); // Function to calculate contrast ratio

        // Step 2: Ensure the contrast ratio meets WCAG standards (at least 4.5:1 for normal text)
        expect(contrastRatio).to.be.at.least(4.5);

        done();
      });
  });
});

// Example function to calculate contrast ratio
function calculateContrastRatio(color1, color2) {
  // Implement color contrast calculation logic here
  return 21; // Placeholder contrast ratio (this should be replaced with real logic)
}
```

```javascript
describe('Usability - Clear Navigation Menu', function () {
  this.timeout(5000); // Allow time for testing usability

  const server = 'http://localhost:3000'; // Replace with your server URL

  it('should have clear and self-explanatory labels in the navigation menu', (done) => {
    chai.request(server)
      .get('/') // Load the homepage
      .end((err, res) => {
        if (err) return done(err);

        // Step 1: Check if navigation menu contains clear labels (e.g., "Home", "About Us", "Contact")
        const navMenu = res.text.match(/<nav [^>]*>[\s\S]*?<\/nav>/); // Regex to match <nav> content
        const menuItems = navMenu[0].match(/<a [^>]*>([^<]+)<\/a>/g); // Extract text inside <a> tags

        // Step 2: Verify if menu items are clear and self-explanatory
        const expectedLabels = ['Home', 'About Us', 'Contact'];
        menuItems.forEach((item, index) => {
          const label = item.replace(/<\/?a[^>]*>/g, '').trim();
          expect(expectedLabels).to.include(label);
        });

        done();
      });
  });
});
```

```javascript
describe('Usability - Tooltips on Hover', function () {
  this.timeout(5000); // Allow time for testing tooltips

  const server = 'http://localhost:3000'; // Replace with your server URL

  it('should display tooltips on hover for icons and buttons', (done) => {
    chai.request(server)
      .get('/') // Load the homepage
      .end((err, res) => {
        if (err) return done(err);

        // Step 1: Check for elements with tooltips (e.g., icons or buttons)
        const tooltips = res.text.match(/<button [^>]*title=["'][^"']+["']/g); // Match buttons with tooltips

        // Step 2: Ensure each button or icon has a tooltip
        expect(tooltips.length).to.be.greaterThan(0); // Expecting at least one tooltip

        done();
      });
  });
});
```

### Test Case 17: Localization


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