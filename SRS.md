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
