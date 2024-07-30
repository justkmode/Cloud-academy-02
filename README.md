# Cloud-academy-02
Week 3 - System Design Applications - 🚀 Project - Design Scalable Architecture

## Part 1: Traditional Server Scaling Design

### Web Application Idea: Social Media Platform

### Core Functionalities:

1. **User Registration and Authentication:** Signup, login, profile management.
2. **User Feed:** Display posts from friends and public profiles.
3. **Post Creation and Management:** Users can create, edit, delete posts.
4. **Likes and Comments:** Interaction features for user posts.
5. **Messaging:** Private messaging between users.
6. **Search:** Search for users, posts, and hashtags.

### High-Level Architecture Diagram

```
           +------------------+
           |   Load Balancer  |
           +--------+---------+
                    |
    +---------------+---------------+
    |                               |
+---+---+                       +---+---+
|  Web  |                       |  Web  |
| Server|                       | Server|
+---+---+                       +---+---+
    |                               |
+---+---+                       +---+---+
|  App  |                       |  App  |
| Server|                       | Server|
+---+---+                       +---+---+
    |                               |
    +---------------+---------------+
                    |
           +--------+---------+
           |    Database      |
           +------------------+

```

### Vertical and Horizontal Scaling

### Vertical Scaling for Database Layer

- **Vertical Scaling Strategy:** Increase the capacity of the database server by upgrading to a more powerful instance with more CPU, RAM, and storage.
- **Benefits:**
    - Simplicity: Easy to implement and manage.
    - No application changes required.
- **Limitations:**
    - Limited by the maximum capacity of a single server.
    - Downtime may be required for scaling.

### Horizontal Scaling with Auto Scaling Group

- **Horizontal Scaling Strategy:** Use an Auto Scaling Group for web and application servers.
- **Components:**
    - **Auto Scaling Group:** Automatically adjusts the number of web and application servers based on traffic.
    - **Load Balancer:** Distributes incoming traffic evenly across servers.
- **Benefits:**
    - High availability: Can handle more traffic by adding more instances.
    - Fault tolerance: Instances can be replaced automatically if they fail.
- **Limitations:**
    - More complex to manage and configure.
    - Requires careful load balancing and session management.

### Traditional Server Scaling Design Benefits and Limitations

- **Benefits:**
    - Control over server configuration and performance.
    - Can use existing tools and practices for monitoring and management.
- **Limitations:**
    - Higher operational overhead.
    - Scaling can be slower and more complex.
    - Higher fixed costs due to underutilized resources.

---

## Part 2: Serverless Architecture Design

### Serverless Components

- **AWS Lambda:** Backend processing for user registration, post creation, etc.
- **Amazon API Gateway:** API endpoints for interacting with Lambda functions.
- **Amazon DynamoDB:** NoSQL database for user data, posts, likes, and comments.
- **Amazon S3:** Storage for user-uploaded images and videos.
- **Amazon Cognito:** User authentication and authorization.
- **Amazon SNS/SQS:** Messaging and notifications.

### Serverless Architecture Diagram

```
           +-------------------+
           |    API Gateway    |
           +---------+---------+
                     |
    +----------------+----------------+
    |                |                |
+---+---+        +---+---+        +---+---+
| Lambda |        | Lambda |        | Lambda |
|  Auth  |        |  Post  |        | Search |
+---+---+        +---+---+        +---+---+
    |                |                |
+---+---+        +---+---+        +---+---+
|Cognito|        | DynamoDB |     |DynamoDB|
+---+---+        +---+---+        +---+---+
    |                |                |
+---+---+        +---+---+        +---+---+
|  S3   |        |  SNS   |        |  SQS  |
+-------+        +-------+        +-------+

```

### Serverless Architecture Scaling and Management

- **Scaling:**
    - **Automatic Scaling:** Lambda functions automatically scale with incoming requests.
    - **API Gateway:** Scales automatically with traffic.
    - **DynamoDB:** Scales based on demand.
- **Management:**
    - Simplified operations: AWS manages scaling, patching, and infrastructure.
    - Cost management: Pay only for actual usage, reducing costs during low traffic periods.
- **Benefits:**
    - Simplifies scaling and reduces operational overhead.
    - Cost-effective, especially for variable or unpredictable traffic patterns.
- **Challenges:**
    - Cold starts can introduce latency.
    - Debugging and monitoring can be more complex.
    - Potential vendor lock-in with AWS services.

---

## Part 3: Comparison and Analysis

### Performance and Cost

- **Performance:**
    - **Traditional:** Performance is predictable, but scaling can be slow and complex.
    - **Serverless:** Scales quickly and seamlessly, but may experience latency from cold starts.
- **Cost:**
    - **Traditional:** Higher fixed costs due to always-on servers.
    - **Serverless:** Pay-per-use model reduces costs during low traffic periods.

### Development, Deployment, and Maintenance

- **Traditional:**
    - **Development:** Familiar development and debugging environment.
    - **Deployment:** More complex due to managing server infrastructure.
    - **Maintenance:** Requires regular maintenance and patching.
- **Serverless:**
    - **Development:** Can be more complex due to event-driven nature.
    - **Deployment:** Simplified deployment process using AWS services.
    - **Maintenance:** Minimal maintenance as AWS handles infrastructure.

### Use Cases

- **Traditional Server Scaling:**
    - **Suitable for:** Applications with predictable, high traffic. Teams with existing expertise in server management.
- **Serverless Architecture:**
    - **Suitable for:** Applications with variable or unpredictable traffic. Startups and small teams looking to reduce operational overhead and costs.

---

## Deliverables

### Architecture Diagrams

1. **Traditional Server Scaling:**
    - Diagram illustrating the use of load balancers, web servers, application servers, and databases with vertical and horizontal scaling strategies.
2. **Serverless Architecture:**
    - Diagram showing the interaction of AWS Lambda functions, API Gateway, DynamoDB, and other serverless components.

### Design Document

1. **Components Explanation:**
    - Detailed explanation of each component in both traditional and serverless designs.
2. **Scaling Strategies:**
    - Explanation of vertical and horizontal scaling for traditional design, and automatic scaling in serverless design.
3. **Rationale:**
    - Justification for architectural decisions based on scalability, cost, and operational needs.

### Comparative Analysis

1. **Scalability:**
    - Traditional: Slower, more complex scaling with higher fixed costs.
    - Serverless: Fast, seamless scaling with pay-per-use cost model.
2. **Cost:**
    - Traditional: Higher fixed costs, even during low traffic.
    - Serverless: Cost-efficient with variable traffic, lower operational overhead.
3. **Operational Complexity:**
    - Traditional: Higher due to server management.
    - Serverless: Lower as AWS handles most infrastructure tasks.
4. **Suitability:**
    - Traditional: Best for predictable, high-traffic applications.
    - Serverless: Best for variable traffic, startups, and small teams.

---

This project aims to provide a comprehensive understanding of different architectural styles, their benefits, and their trade-offs. Through this exercise, you will gain practical insights into designing scalable web applications using both traditional and serverless approaches.

## Architecture Diagrams

### Traditional Server Scaling

### High-Level Architecture Diagram

```
           +---------------------+
           |    Load Balancer    |
           +----------+----------+
                      |
        +-------------+-------------+
        |                           |
    +---+---+                   +---+---+
    | Web    |                   | Web    |
    | Server |                   | Server |
    +---+---+                   +---+---+
        |                           |
    +---+---+                   +---+---+
    | App    |                   | App    |
    | Server |                   | Server |
    +---+---+                   +---+---+
        |                           |
    +---+---+                   +---+---+
    | DB     |                   | DB     |
    | Server |                   | Server |
    +---+---+                   +---+---+
        |                           |
        +-------------+-------------+
                      |
           +----------+----------+
           |    Database Cluster   |
           +----------------------+

```

### Vertical and Horizontal Scaling

1. **Vertical Scaling:**
    - **Database Layer:** Increase the capacity of the database server by upgrading to a more powerful instance.
    - **Diagram Update:** The DB Server box will be upgraded to a larger instance type (e.g., from `db.m5.large` to `db.m5.2xlarge`).
2. **Horizontal Scaling:**
    - **Web and Application Servers:**
        - Use Auto Scaling Groups to automatically launch and terminate instances based on traffic.
        - A load balancer will distribute incoming traffic across multiple instances.

```
           +---------------------+
           |    Load Balancer    |
           +----------+----------+
                      |
        +-------------+-------------+
        |                           |
    +---+---+       +---+---+     +---+---+
    | Web    |       | Web    |     | Web    |
    | Server |       | Server |     | Server |
    +---+---+       +---+---+     +---+---+
        |               |             |
    +---+---+       +---+---+     +---+---+
    | App    |       | App    |     | App    |
    | Server |       | Server |     | Server |
    +---+---+       +---+---+     +---+---+
        |               |             |
    +---+---+       +---+---+     +---+---+
    | DB     |       | DB     |     | DB     |
    | Server |       | Server |     | Server |
    +---+---+       +---+---+     +---+---+
        |               |             |
        +-------+-------+-------------+
                |
           +----+----+
           | Database |
           +----------+

```

### Serverless Architecture

### High-Level Architecture Diagram

```
           +-------------------+
           |    API Gateway    |
           +---------+---------+
                     |
        +------------+------------+
        |            |            |
    +---+---+    +---+---+    +---+---+
    | Lambda |    | Lambda |    | Lambda |
    | Auth   |    | Post   |    | Search |
    +---+---+    +---+---+    +---+---+
        |            |            |
    +---+---+    +---+---+    +---+---+
    | Cognito|    | DynamoDB|    | DynamoDB|
    +---+---+    +---+---+    +---+---+
        |            |            |
    +---+---+    +---+---+    +---+---+
    |    S3  |    |   SNS  |    |   SQS |
    +-------+    +-------+    +-------+

```

1. **User Registration and Authentication:**
    - **AWS Lambda:** Handles user registration and authentication logic.
    - **Amazon Cognito:** Manages user identities and access.
2. **Post Creation and Management:**
    - **AWS Lambda:** Processes requests for creating, editing, and deleting posts.
    - **Amazon DynamoDB:** Stores post data.
3. **User Feed and Search:**
    - **AWS Lambda:** Handles fetching user feed and search queries.
    - **Amazon DynamoDB:** Stores user feed and search index data.
4. **Likes and Comments:**
    - **AWS Lambda:** Processes likes and comments.
    - **Amazon SNS:** Publishes notifications for likes and comments.
    - **Amazon SQS:** Queues messages for further processing.
5. **Messaging:**
    - **AWS Lambda:** Processes private messages between users.
    - **Amazon DynamoDB:** Stores messaging data.
6. **Storage:**
    - **Amazon S3:** Stores user-uploaded images and videos.

### Serverless Architecture Scaling

1. **API Gateway:**
    - Scales automatically with incoming traffic.
2. **AWS Lambda:**
    - Scales automatically with each request, handling scaling transparently.
3. **Amazon DynamoDB:**
    - Scales based on demand with provisioned or on-demand capacity modes.
4. **Amazon S3:**
    - Scales automatically with storage demand.

### Final Comparison

### Traditional Server Scaling vs. Serverless Architecture

- **Scalability:**
    - **Traditional:** Vertical scaling is limited by server capacity; horizontal scaling requires careful management.
    - **Serverless:** Automatically scales with demand; no manual intervention required.
- **Cost:**
    - **Traditional:** Higher fixed costs; underutilized resources incur costs.
    - **Serverless:** Pay-per-use model; cost-efficient for variable traffic.
- **Operational Complexity:**
    - **Traditional:** Higher due to server management, patching, and scaling.
    - **Serverless:** Lower as AWS manages infrastructure.
- **Suitability:**
    - **Traditional:** Best for predictable, high-traffic applications.
    - **Serverless:** Best for variable traffic, startups, and small teams.

These diagrams and explanations should help in understanding how each architecture handles scalability, cost, and operational complexity differently.
