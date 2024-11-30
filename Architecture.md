**1. System Context Diagram**
![System Context Diagram](assets/System_context_diagram.png)

```plantuml
@startuml
actor "User" as User
actor "Admin" as Admin
actor "Content Creator" as ContentCreator
actor "Payment Processor" as PaymentProcessor
actor "CDN Server" as CDN
actor "Recommendation Engine" as RecommendationEngine

package "Nova Digital System" {
    rectangle "User Authentication" as Authentication
    rectangle "Content Browsing & Streaming" as ContentSystem
    rectangle "Subscription Management" as SubscriptionSystem
    rectangle "Ratings & Feedback" as FeedbackSystem
    rectangle "Admin Dashboard" as AdminDashboard
}

User --> Authentication : Sign Up / Login
User --> ContentSystem : Browse / Watch Content
User --> SubscriptionSystem : Manage Subscription
User --> FeedbackSystem : Rate / Provide Feedback

Admin --> AdminDashboard : Manage Users / Content
Admin --> ContentSystem : Monitor Content

ContentCreator --> ContentSystem : Upload Content

Authentication --> ContentSystem : Provide Access
ContentSystem --> CDN : Stream Content
ContentSystem --> RecommendationEngine : Fetch Suggestions

SubscriptionSystem --> PaymentProcessor : Handle Payments
@enduml
```

**2. Container Diagram**
![Container Diagram](assets/Container_diagram.png)

```plantuml
@startuml
title Container Diagram - Nova Digital

rectangle "Web/Mobile App" as App <<User Interface>> #lightblue
rectangle "API Gateway" as APIGateway <<API Gateway>> #lightgreen
rectangle "Authentication Service" as AuthService <<Service>> #lightyellow
rectangle "Content Service" as ContentService <<Service>> #lightyellow
rectangle "Subscription Service" as SubscriptionService <<Service>> #lightyellow
rectangle "Feedback Service" as FeedbackService <<Service>> #lightyellow
rectangle "Recommendation Engine" as RecommendationEngine <<Service>> #lightyellow
rectangle "Admin Management Service" as AdminService <<Service>> #lightyellow

database "User Database" as UserDB <<Database>> #lightpink
database "Content Database" as ContentDB <<Database>> #lightpink
database "Subscription Database" as SubDB <<Database>> #lightpink

cloud "External Services" {
    rectangle "Payment Processor" as PaymentProcessor <<External Service>> #lightgray
    rectangle "CDN" as CDN <<External Service>> #lightgray
}

App --> APIGateway : API Calls
APIGateway --> AuthService : Authenticate Users
APIGateway --> ContentService : Fetch/Stream Content
APIGateway --> SubscriptionService : Manage Subscriptions
APIGateway --> FeedbackService : Submit Feedback
APIGateway --> RecommendationEngine : Fetch Recommendations
APIGateway --> AdminService : Manage Platform
APIGateway --> PaymentProcessor : Process Payments
APIGateway --> CDN : Stream Content

AuthService --> UserDB : Manage Users
ContentService --> ContentDB : Store/Fetch Content
SubscriptionService --> SubDB : Manage Subscriptions
FeedbackService --> ContentDB : Store Feedback
@enduml

```

**3. Component Diagram**
*3.1 Component Diagram for users*
![Component Diagram](assets/Component_diagram(for_users).png)
```plantuml
@startuml
title Component Diagram - User Interactions in Nova Digital

component "Web/Mobile App" as App #lightblue
component "API Gateway" as APIGateway #lightgreen
component "Authentication Service" as AuthService #lightyellow
component "Content Service" as ContentService #lightyellow
component "Subscription Service" as SubscriptionService #lightyellow
component "Feedback Service" as FeedbackService #lightyellow
component "Recommendation Engine" as RecommendationEngine #lightyellow

database "User Database" as UserDB #lightpink
database "Content Database" as ContentDB #lightpink
database "Subscription Database" as SubDB #lightpink

cloud "External Services" {
    component "CDN" as CDN #lightgray
    component "Payment Processor" as PaymentService #lightgray
}

App --> APIGateway : API Requests
APIGateway --> AuthService : Authenticate User
AuthService --> UserDB : User Data

APIGateway --> ContentService : Fetch Content
ContentService --> ContentDB : Media Metadata
ContentService --> CDN : Stream Media

APIGateway --> SubscriptionService : Manage Subscription
SubscriptionService --> SubDB : Subscription Data
SubscriptionService --> PaymentService : Process Payments

APIGateway --> FeedbackService : Submit Feedback
FeedbackService --> ContentDB : Store Feedback

APIGateway --> RecommendationEngine : Get Recommendations
RecommendationEngine --> ContentDB : Analyze User Preferences

@enduml
```

*3.2 Component Diagram for Admins*
![Component Diagram](assets/Component_diagram(for_admins).png)

```plantuml
@startuml
title Component Diagram - Admin Interactions in Nova Digital

component "Admin Dashboard" as AdminDashboard #lightblue
component "API Gateway" as APIGateway #lightgreen
component "Authentication Service" as AuthService #lightyellow
component "User Management Service" as UserService #lightyellow
component "Content Management Service" as ContentService #lightyellow
component "Subscription Management Service" as SubscriptionService #lightyellow
component "Reporting Service" as ReportingService #lightyellow

database "User Database" as UserDB #lightpink
database "Content Database" as ContentDB #lightpink
database "Subscription Database" as SubDB #lightpink

cloud "External Services" {
    component "Payment Processor" as PaymentService #lightgray
}

AdminDashboard --> APIGateway : Admin Requests
APIGateway --> AuthService : Authenticate Admin
AuthService --> UserDB : Verify Admin Credentials

APIGateway --> UserService : Manage Users
UserService --> UserDB : Create/Update/Delete Users

APIGateway --> ContentService : Manage Content
ContentService --> ContentDB : Add/Update/Delete Content

APIGateway --> SubscriptionService : Manage Subscriptions
SubscriptionService --> SubDB : Create/Update/Delete Subscriptions
SubscriptionService --> PaymentService : Process Payments

APIGateway --> ReportingService : Generate Reports
ReportingService --> UserDB : Fetch User Data
ReportingService --> ContentDB : Fetch Content Data
ReportingService --> SubDB : Fetch Subscription Data
@enduml

```

**4. Deployment Diagram**
![Deployment Diagram](assets/deployment_diagram.png)

```plantuml
@startuml
title Deployment Diagram - Nova Digital

node "Web/Mobile Client" as Client {
    artifact "Web App" as WebApp
    artifact "Mobile App" as MobileApp
}

node "API Server" as APIServer {
    artifact "API Gateway" as APIGateway
    artifact "Auth Service" as AuthService
    artifact "Content Service" as ContentService
    artifact "Subscription Service" as SubscriptionService
    artifact "Recommendation Engine" as RecommendationEngine
}

node "Database Server" as DBServer {
    artifact "User Database" as UserDB
    artifact "Content Database" as ContentDB
    artifact "Subscription Database" as SubDB
}

node "External Services" as ExternalServices {
    artifact "CDN" as CDN
    artifact "Payment Processor" as PaymentProcessor
}

Client --> APIServer : API Requests (Web/Mobile App)
APIServer --> AuthService : Authentication Requests
APIServer --> ContentService : Fetch Content
APIServer --> SubscriptionService : Manage Subscriptions
APIServer --> RecommendationEngine : Get Recommendations
APIServer --> CDN : Stream Content
APIServer --> PaymentProcessor : Process Payments

AuthService --> UserDB : Store/Retrieve User Data
ContentService --> ContentDB : Store/Retrieve Content Data
SubscriptionService --> SubDB : Store/Retrieve Subscription Data

CDN --> ContentDB : Retrieve Media for Streaming
PaymentProcessor --> SubDB : Process Payments
@enduml
```