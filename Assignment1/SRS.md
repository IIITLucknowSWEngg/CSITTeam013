5. Non-functional Requirements
5.1 Performance Requirements:
• 
Scalability: The platform should handle millions of concurrent users without service degradation, including streaming at multiple resolutions (e.g., 1080p, 4K).
• Use Case: During the final match of a popular cricket tournament, millions of users log in to stream the event live in 4K. The system automatically scales its resources, ensuring all users experience smooth streaming without buffering or quality degradation.
• 
Latency: Content should load within 2-3 seconds, with minimal buffering, even in high-traffic conditions.
• Use Case: A user browsing the platform clicks on a movie, and the movie starts playing within 2 seconds, even though it’s peak hours with many users online.
• 
Throughput: The system should support multiple streams per user for different devices without affecting performance.
• Use Case: A user starts streaming a show on their TV while another family member streams a different show on their tablet. The platform efficiently handles multiple streams without buffering or reducing quality on either device.
• 
Bandwidth Optimization: Efficient use of bandwidth to ensure streaming quality on both high and low-speed networks.
• Use Case: A user on a slower mobile network streams content in 720p, while a user on high-speed broadband watches the same show in 4K. Both users experience smooth playback due to adaptive streaming based on available bandwidth.

5.2 Safety Requirements:
• 
Data Protection: Regular backups and disaster recovery plans should be in place to protect user data from loss or corruption.
• Use Case: A critical server crash occurs, but user data (e.g., watch history, preferences) is quickly restored from the most recent backup, minimizing any disruption to the service.
• 
Service Availability: Mechanisms to avoid system crashes during updates or maintenance, ensuring minimal downtime.
• Use Case: During a routine system update, users continue to access the platform without noticing any interruptions, thanks to rolling updates and redundancy.
• 
Content Control: Appropriate age-based restrictions to ensure children cannot access inappropriate content.
• Use Case: A child attempts to access a TV-MA rated show, but the platform prompts for the parent’s password due to the parental controls enabled on the account.
5.3 Security Requirements:
• 
User Authentication: Two-factor authentication (2FA) and strong password policies to protect user accounts.
• Use Case: A user logs in from a new device, and the platform requests a verification code sent to their email before allowing access to the account, adding an extra layer of security.
• 
Encryption: End-to-end encryption for data in transit and at rest, ensuring secure streaming and storage of user data.
• Use Case: While streaming a sensitive documentary, both the stream and personal data (e.g., billing information) are encrypted, protecting the user from eavesdropping or data breaches.
• 
Access Control: Strict role-based access control (RBAC) for managing administrative and user privileges.
• Use Case: Only authorized administrators can access the platform’s backend to update content, while customer service representatives can only access user support tickets and account-related queries.
• 
Fraud Detection: Systems to detect and mitigate fraudulent access or piracy attempts.
• Use Case: The platform detects a user attempting to bypass geo-restrictions using a VPN and immediately restricts access to the content, notifying the user of the violation.
5.4 Software Quality Attributes:
• 
Usability: The interface should be intuitive and accessible (e.g., screen reader support).
• Use Case: A visually impaired user navigates the platform easily using a screen reader to select shows and movies, with all menu items properly labeled for accessibility.
• 
Responsiveness: Instant interaction responses, such as play/pause, should be smooth and without delay.
• Use Case: A user clicks the "pause" button while watching a movie, and the playback immediately stops without any delay or stuttering.
• 
Localization: Support for multiple languages, including subtitles and audio in regional languages.
• Use Case: A user in Spain accesses a Bollywood movie and has the option to switch between Spanish, Hindi, and English subtitles, as well as dubbed audio tracks.
5.5 Maintainability Requirements:
• 
Modular Architecture: Code should be modular to facilitate easier updates and new feature additions without impacting existing functionality.
• Use Case: The development team adds a new "Watch Party" feature to the platform, and thanks to the modular system, they deploy it without affecting the core streaming functionality.
• 
Automated Testing: Continuous integration and automated testing practices should ensure quick identification and resolution of bugs.
• Use Case: A new recommendation algorithm is added, and automated tests are run immediately to verify that it does not break any other features before it is pushed to production.
• 
Version Control: A robust version control system to track changes and revert to stable versions if necessary.
• Use Case: After deploying a new update that causes minor interface bugs, the team quickly reverts to the previous stable version while they fix the issue.
5.6 Reliability Requirements:
• 
Fault Tolerance: The system should have mechanisms to recover from hardware or software failures without impacting user experience.
• Use Case: While a user is streaming a show, one server experiences an issue. The system automatically switches the user’s session to a backup server, allowing the stream to continue without interruption.
• 
High Availability: Ensure 99.99% uptime, with redundant servers and automatic failover.
• Use Case: Even during scheduled maintenance, the platform remains accessible due to server redundancy, ensuring that users don’t experience downtime.
• 
Content Delivery Network (CDN): Use of global CDNs to ensure reliable and quick content delivery, regardless of geographic location.
• Use Case: A user in a remote part of the world streams content without any noticeable delays because the CDN distributes the content from a server close to their location.
5.7 Interoperability Requirements:
• 
Cross-Platform Compatibility: The platform should work seamlessly across various devices (smart TVs, smartphones, tablets).
• Use Case: A user starts watching a series on their phone, pauses it, and resumes watching on their smart TV without any issues or loss of progress.
• 
Third-Party Integrations: Ability to integrate with external services like payment gateways and social media.
• Use Case: A user connects their Netflix account to their social media, sharing what they’re watching on their profile and using an integrated payment gateway to renew their subscription.
• 
APIs: Open and well-documented APIs for third-party apps and plugins.
• Use Case: A third-party app developer creates a recommendation tool that integrates seamlessly with the platform’s API to suggest content based on user preferences.
