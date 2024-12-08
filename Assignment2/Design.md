# Nova Digital System Design Document  
---
# Table of Contents

1. [Introduction](#1-introduction)
   - [1.1 Purpose](#11-purpose)
   - [1.2 Scope](#12-scope)
   - [1.3 Document Conventions](#13-document-conventions)
   
2. [System Overview](#2-system-overview)
   - [2.1 System Context](#21-system-context)
   - [2.2 Key Components](#22-key-components)

3. [Architectural Design](#3-architectural-design)
   - [3.1 Architectural Overview](#31-architectural-overview)
   - [3.2 Design Principles](#32-design-principles)

4. [Detailed Design](#4-detailed-design)
   - [4.1 User Management](#41-user-management)
   - [4.2 Content Management](#42-content-management)
   - [4.3 Recommendation Engine](#43-recommendation-engine)
   - [4.4 Streaming Infrastructure](#44-streaming-infrastructure)
   - [4.5 Billing and Subscription](#45-billing-and-subscription)
   - [4.6 Analytics and Insights](#46-analytics-and-insights)
   - [4.7 Design Decisions and Trade-offs](#47-design-decisions-and-trade-offs)

5. [Deployment Architecture](#5-deployment-architecture)
   - [5.1 Overview](#51-overview)
   - [5.2 Client Devices](#52-client-devices)
   - [5.3 Content Delivery Networks (CDNs)](#53-content-delivery-networks-cdns)
   - [5.4 Backend Services](#54-backend-services)

6. [Data Design](#6-data-design)
   - [6.1 Database](#61-database)
   - [6.2 Data Processing](#62-data-processing)
   - [6.3 Video Recommendation System](#63-video-recommendation-system)

7. [User Interface Design](#7-user-interface-design)
   - [7.1 User Interface Wireframes](#71-user-interface-wireframes)
   - [7.2 User Interaction Patterns](#72-user-interaction-patterns)

8. [Security Design](#8-security-design)
   - [8.1 Authentication and Authorization](#81-authentication-and-authorization)
   - [8.2 Data Protection](#82-data-protection)
   - [8.3 Secure Communication](#83-secure-communication)

9. [Error Handling](#9-error-handling)
   - [9.1 Exception Handling](#91-exception-handling)
   - [9.2 Logging and Monitoring](#92-logging-and-monitoring)

10. [Conclusion](#10-conclusion)
---

## 1. Introduction  

### 1.1 Purpose  
The purpose of this NOVA DIGITAL design document is to provide a comprehensive overview of the design principles and architecture for the Hotstar software system. It serves as a guide for the development team in creating a robust, scalable, and maintainable system. The document outlines the high-level design of the system, key components, and design principles to ensure clarity and consistency during the development process.  

### 1.2 Scope  
The Hotstar design document covers the following aspects of the software system:  
- **High-Level Architectural Overview**: Describing the overall structure and components of the system.  
- **Design Principles**: Identifying and applying relevant design principles for scalability and performance.  
- **Key Modules and Components**: Providing an overview of the major functional components of the system.  
- **Deployment Architecture**: Explaining how the system is deployed, including client devices, CDNs, backend services, and databases.  
- **Data Design**: Describing the database schema, data flow, and interactions between modules and databases.  
- **User Interface Design**: Presenting wireframes or mockups illustrating the user interface design.  
- **Security Design**: Outlining the mechanisms and protocols used for user authentication, data protection, and secure communication.  
- **Performance Optimization**: Detailing caching strategies, CDNs, and data indexing techniques used to enhance system performance.  
- **Error Handling and Logging**: Describing the approach to handling exceptions, errors, and system logging.  

### 1.3 Document Conventions  
The Nova Digital design document follows these conventions:  
- **UML Notation**: Using UML diagrams, such as class diagrams and deployment diagrams, to visualize the system design.  
- **Code Snippets**: Providing relevant code snippets for illustration purposes, especially in sections discussing specific modules or components.  
- **Visual Aids**: Including wireframes, mockups, and diagrams to enhance the understanding of the system design.  
- **Structured Sections**: Organizing the document into sections, such as introduction, architectural design, detailed design, and conclusion, for better readability and clarity.  

---

## 2. System Overview  

### 2.1 System Context  
Nova Digital is an online video streaming platform offering a vast library of TV shows, movies, live sports, and regional programming. The system consists of a backend infrastructure, client applications, and content delivery networks (CDNs) to ensure reliable and efficient streaming.  

The system context includes:  
- **User Devices**: Smartphones, tablets, smart TVs, and web browsers through which users access the platform.  
- **Content Providers**: Third-party providers and original productions contributing content to the platform.  
- **Payment Gateways**: External service providers managing subscription payments and transactions.  
- **CDNs**: Nova Digital's proprietary and third-party networks ensuring low-latency streaming.  
- **Social Media Platforms**: Integration enabling users to share their viewing activities and recommendations.  

### 2.2 Key Components  
1. **User Management**: Handles user authentication, registration, and profile management.  
2. **Content Management**: Manages ingestion, categorization, and search functionalities.  
3. **Recommendation Engine**: Provides personalized recommendations using machine learning.  
4. **Streaming Infrastructure**: Supports adaptive bitrate streaming and caching for smooth playback.  
5. **Billing and Subscription**: Manages secure payment processing and subscription plans.  
6. **Analytics and Insights**: Collects user data and system metrics for optimization.  

---

## 3. Architectural Design  

### 3.1 Architectural Overview  
Nova employs a **microservices architecture**, enabling scalability and modularity. The platform relies on:  
- **AWS and Nova Digital CDN**: Collaboratively handling backend services and video streaming.  
- **ReactJS Frontend**: Ensures modularity, performance, and startup speed.  

#### Core Components:  
1. **Client**: Devices like smartphones, TVs, and laptops used to browse and stream content.  
2. **Nova Digital CDN**: Distributes video content efficiently by delivering streams from geographically proximate servers.  
3. **Backend Services**: Responsible for user authentication, content recommendations, and subscription handling.  

### Onboarding a Movie  
- Nova Digital performs **video transcoding** to support multiple resolutions and formats.  
- Transcoded files are distributed to CDN servers globally.  
- AWS manages login, billing, and recommendation tasks, ensuring seamless playback.  

#### Design Highlights:  
- **Elastic Load Balancer (ELB)**: Balances traffic across multiple zones and instances.  
- **Zuul Gateway**: Handles dynamic routing, monitoring, and security.  
- **Hystrix**: Ensures fault tolerance in case of service failures.  
- **EV Cache**: A custom caching layer for frequently accessed data.  

---

## 4. Detailed Design  

### User Management  
- **Purpose**: Handles user registration, login, and profile customization.  
- **Interfaces**: OAuth for authentication, database for user data storage.  

### Content Management  
- **Purpose**: Manages content ingestion, categorization, and metadata.  
- **Interfaces**: Collaborates with content providers and recommendation engines.  

### Recommendation Engine  
- **Purpose**: Provides personalized content suggestions.  
- **Technology**: Machine learning models analyzing user data.  

### Streaming Infrastructure  
- **Purpose**: Ensures efficient video delivery.  
- **Features**: Adaptive bitrate streaming, caching, and network optimization.  

### Billing and Subscription  
- **Purpose**: Manages subscriptions and payment transactions.  
- **Interfaces**: Integrates with external payment gateways.  

### Analytics and Insights  
- **Purpose**: Collects data for user behavior analysis and system optimization.  
- **Interfaces**: Integrates with various modules for data collection.  

---

### Design Principles and Trade-offs  
- **Scalability**: Utilizes cloud-based infrastructure and CDN optimization.  
- **Performance vs. Storage**: Balances video quality and storage efficiency.  
- **Data Privacy**: Secures user data with encryption and authentication protocols.  

---

## **5. Deployment Architecture**

### **5.1 Overview**

The deployment architecture of Nova Digital involves a distributed system setup that encompasses various components and infrastructure to ensure efficient content delivery and availability. Here are the key elements of the deployment architecture:

- **Client Devices:**
  - Client devices include smartphones, tablets, smart TVs, web browsers, and other devices through which users access the Nova Digital platform.
  - Nova Digital supports a wide range of devices, each with different resolutions, screen sizes, and capabilities.

- **Content Delivery Networks (CDNs):**
  - CDNs play a crucial role in the deployment architecture by distributing content geographically closer to the end-users, reducing latency and improving streaming performance.
  - Nova Digital has built its own CDN called Open Connect, consisting of numerous caching servers deployed in data centers worldwide.
  - These servers store and deliver the most popular and frequently accessed content, reducing the load on the backend infrastructure.

- **Backend Services:**
  - The backend services form the core of Nova Digital's deployment architecture, handling various functionalities such as:
    - User management
    - Content management
    - Recommendation engines
    - Streaming infrastructure
    - Billing and analytics
  - These services are typically deployed on cloud platforms such as Amazon Web Services (AWS) or other cloud providers.
  - Designed to be scalable and resilient, capable of handling a large number of concurrent users and high traffic volumes.

- **Microservices Architecture:**
  - Nova Digital adopts a microservices architecture, breaking down the system into small, loosely coupled services that can be developed, deployed, and scaled independently.
  - Each microservice focuses on a specific business capability and communicates with others through well-defined APIs and protocols.
  - This architecture promotes flexibility, scalability, and fault isolation, allowing Nova Digital to evolve and update its system components without affecting the entire system.

- **Load Balancing and Auto Scaling:**
  - Load balancing techniques are employed to distribute incoming requests across multiple backend servers, ensuring efficient resource utilization and high availability.
  - Auto scaling mechanisms automatically adjust the number of server instances based on the current demand, scaling up or down to accommodate traffic fluctuations.

- **Data Storage and Databases:**
  - Nova Digital utilizes various types of databases and data storage systems to manage user profiles, content metadata, viewing history, and other data.
  - Relational databases (e.g., MySQL, PostgreSQL) and NoSQL databases (e.g., Cassandra, Amazon DynamoDB) are used based on specific data requirements.
  - Data is often replicated across multiple data centers to ensure data availability, resilience, and disaster recovery.

- **Monitoring and Logging:**
  - Nova Digital incorporates robust monitoring and logging systems to track system performance, detect issues, and troubleshoot problems.
  - Various monitoring tools and services are employed to collect metrics, log events, and generate alerts for timely response and system optimization.

The deployment architecture of Nova Digital is designed to provide a seamless streaming experience, ensuring content availability, scalability, and performance across a diverse range of client devices. It leverages CDNs, microservices, load balancing, auto scaling, and cloud infrastructure to deliver content efficiently and handle high user demands.

---

## **6. Data Design**

### **6.1 Database**

Nova Digital uses two different databases:

1. **MySQL (RDBMS):**
   - Nova Digital saves data like billing information, user information, and transaction information in MySQL because it needs ACID compliance.
   - **EC2 Deployed MySQL:**
     - Nova Digital has a master-master setup for MySQL, deployed on Amazon’s large EC2 instances using InnoDB.
     - Follows a **“Synchronous replication protocol”**:
       - Writes to the primary master node are replicated to a secondary master node.
       - Acknowledgment is sent only after both nodes confirm the write.
     - Ensures high availability with a read replica for every node (local and cross-region).
     - If the primary master fails, the secondary master takes over, and DNS (Route53) entries are updated.

2. **Cassandra (NoSQL):**
   - Handles large volumes of data, such as user viewing history.
   - **Key Features:**
     - Over 50 Cassandra clusters with 500+ nodes.
     - Processes over 30TB of daily backups and 250K writes/second.
   - **Data Segmentation:**
     - **Live Viewing History (LiveVH):** Recent and frequently updated data.
     - **Compressed Viewing History (CompressedVH):** Older, rarely accessed data stored in compressed form.

---

### **Data Processing in Nova Digital**

- **Tools Used:**
  - **Kafka:** For real-time data ingestion.
  - **Apache Chukwa:** For log collection and batch data processing.
  - **ElasticSearch:** For visualization and troubleshooting.

- **Workflow:**
  1. Data ingestion begins with Kafka and Chukwa.
  2. Data is stored in Hadoop-based systems for batch processing.
  3. Kafka routes data to sinks like S3, Elasticsearch, and secondary Kafka clusters.

---

### **Recommendation System**

Nova Digital's recommendation system predicts user interests based on:

- User interaction with the platform (viewing history, ratings).
- Metadata of watched content (genres, actors, etc.).
- User behavior patterns (device, active time).

#### **Algorithms Used:**
1. **Collaborative Filtering:** Matches users with similar preferences.
2. **Content-Based Filtering:** Recommends content based on metadata.

--- 

## **6.2 Data Flow**

The data flow within **Nova Digital** is critical for ensuring high performance, low latency, and seamless content delivery across multiple devices. The system involves several key components and stages of data transmission:

1. **Client Device to CDN:**
   - User requests are first sent from their device to a Content Delivery Network (CDN) to ensure low-latency access to video content.
   - The CDN caches content geographically to reduce the load on the central servers and minimize access time for users.

2. **Backend Services and APIs:**
   - User actions like logins, content searches, and playback requests are handled by microservices, which manage various business logic components, such as user authentication, recommendation algorithms, and content delivery strategies.
   - APIs aggregate data from different services, including user profiles, content metadata, and playback history.

3. **Database Interaction:**
   - All data, including user profiles, watch history, preferences, and settings, is stored in a distributed database system to ensure scalability and fault tolerance.
   - A NoSQL database (e.g., MongoDB) is used for user-generated content, while relational databases (e.g., MySQL) store structured data.

4. **Data Streaming:**
   - Real-time analytics data, such as user interactions, viewing patterns, and device health, is transmitted to the backend for processing and analytics.

This flow ensures that **Nova Digital** operates efficiently, providing users with a seamless experience while maintaining backend stability.

---

## **7. User Interface Design**

### **7.1 User Interface Wireframes**

#### **Lo-Fi Wireframes**

The wireframes are designed to map the overall UI layout and show all essential screen components needed for **Nova Digital**. These screens represent user journeys such as logging in, content discovery, and video playback:

1. **Input Controls:**
   - **Dropdowns, text fields, and radio buttons** allow users to filter content, input text, or select preferences.
   - Example: Content search bar with auto-complete options, genre selection dropdown.

2. **Navigational Components:**
   - **Breadcrumbs** allow users to track their location within the app, enabling easy back-and-forth navigation between pages.
   - **Slider and carousel** elements are used for content browsing (e.g., featured shows, trending movies).
   - **Icons** and **tags** (e.g., New, Popular) help users quickly identify content categories.

3. **Informational Components:**
   - **Notifications** alert users about new content, updates, or issues (e.g., connectivity problems, streaming quality alerts).
   - **Progress bars** are used to show video load times and buffering, offering a visual cue to the user.

4. **Containers:**
   - **Accordion-style containers** hold related content together, such as show episodes or movie details, keeping the UI clean and easily scannable.

---

### **7.2 User Interaction Patterns**

#### **Task Implementation:**
- **Tasks** are individual units of work in **Nova Digital**'s system, like content recommendations, video streaming, and subscription management. These tasks are implemented as separate microservices or Lambda functions to improve scalability and fault tolerance.
- Workers running outside of the Conductor server handle heavy processing tasks, like transcoding videos or generating user recommendations.

#### **Operators:**
- **Operators** allow for sophisticated control over the flow of tasks in a user’s session. For example:
  - **Switch:** Directs to different workflows based on user preferences.
  - **Loop:** Repeats a task (like fetching more content if the user scrolls down).
  - **Fork/Join:** Executes multiple tasks concurrently (e.g., fetching metadata for multiple pieces of content).
  - **Sub-workflows** are used for encapsulating complex tasks, such as video encoding, which can run as independent sub-processes.

**Nova Digital** integrates these operators to form flexible and adaptable workflows, ensuring scalability and resiliency in high-demand environments.

---

## **8. Security Design**

### **8.1 Authentication and Authorization**

- **Kerberos Protocol:** 
  - A robust authentication system that ensures users and servers can securely communicate without exposing sensitive credentials.
  - When a user logs in, the system generates a secure authentication ticket, validating their identity.
  - **Nova Digital** uses Kerberos to verify both user and server identities, ensuring that all connections are authenticated and secure.

#### **Advantages of Kerberos for Nova Digital:**
- Cross-platform support ensures compatibility with various devices (smartphones, desktops, smart TVs).
- Efficient key sharing improves system performance while maintaining a high security standard.
- Reduces the risk of man-in-the-middle attacks by encrypting authentication data.

---

### **8.2 Data Protection**

- **Digital Rights Management (DRM):**
  - **Nova Digital** implements advanced DRM technologies to secure video content. This includes encryption of streaming media, which prevents unauthorized copying or distribution of content.
  - The DRM ensures that **Nova Digital** content can only be viewed by authorized users, protecting intellectual property rights and preventing piracy.

- **Screenshot Protection:**
  - The system blocks screenshots of copyrighted content, ensuring that visual content cannot be captured and distributed without permission.

---

### **8.3 Secure Communication**

#### **Challenges with HTTPS:**
- HTTPS is susceptible to **PKI infrastructure issues**, where errors in certificate renewal or revocation can cause service interruptions.
- To mitigate these problems, **Nova Digital** has developed a custom security protocol, **Nova Secure Layer (NSL)**, to provide higher flexibility and security.

#### **NSL High-Level Goals:**
- **Cross-language support** ensures compatibility with a wide range of devices and platforms, including JavaScript-based web applications and native apps on Android and iOS.
- **Automatic error recovery** ensures that any device or service failure is recovered automatically, providing seamless user experiences without requiring manual intervention.
- **Performance Optimization** focuses on minimizing the performance overhead introduced by security protocols, especially in network-heavy operations like video streaming.
- **Flexibility and Extensibility** allow **Nova Digital** to adopt future security technologies without disrupting existing infrastructure.

#### **NSL Security Properties:**
1. **Integrity Protection:** Ensures data is not tampered with during transit.
2. **Encryption:** Protects message content from unauthorized inspection.
3. **Authentication:** Verifies the sender’s identity, ensuring trust between devices and services.
4. **Non-Replayable:** Ensures that data, especially payment transactions, cannot be replayed maliciously.

#### **NSL Deployment Models:**
- **Trusted Services Network:** A client device authenticates against multiple servers that share common cryptographic secrets. This network type is used in situations where a single client needs to interact with multiple backend services, all of which must trust each other.
- **Peer-to-Peer:** Both devices mutually authenticate, ensuring data integrity during direct communication between devices.

---

## **9. Error Handling and Logging**

### **9.1 Exception Handling**

In **Nova Digital**, all handled exceptions are captured as `NovaException`. Errors originating in middleware or custom service filters are captured to ensure they do not propagate further into the system, ensuring stable operation even in case of failures.

- **Customizing NovaExceptions:**
  - Custom exceptions are created for specific failure points such as failed content retrieval, network issues, or security breaches.
  - Each exception is tied to a specific workflow or service to ensure accurate error detection and logging.

---

### **9.2 Logging and Monitoring**

- As **Nova Digital** scales globally, data is continuously collected and analyzed to improve user experience and service performance. Real-time monitoring is performed to track:
  - **User interactions:** Data on how users interact with the content, such as what genres they prefer or which devices they use.
  - **Performance metrics:** Metrics like load times, buffering times, and server response times are closely monitored to identify and resolve bottlenecks.
  - **Device health:** Data from devices helps identify issues such as connectivity problems or system crashes, which are then used to trigger error recovery protocols.

---

## **10. Conclusion**

This **Software Design Document** for **Nova Digital** provides a comprehensive view of the system architecture, including security, user interface, error handling, and data flow. By adhering to best practices in software design and leveraging cutting-edge technologies, **Nova Digital** aims to deliver a highly reliable, secure, and scalable streaming platform that meets the needs of millions of users globally.

--- 
