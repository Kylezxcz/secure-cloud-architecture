# Secure Cloud Architecture Plan

## CDN
The CDN stores cached copies of static content (like your HTML and CSS files) closer to users' geographic locations. This reduces latency, improves the overall loading speed of the web application, and decreases the direct traffic hitting your main infrastructure.

## Load Balancer
The load balancer distributes incoming internet requests evenly across multiple application servers. This ensures high availability, prevents any single server from crashing under heavy traffic, and acts as the secure entry point for the application.

## Application Servers
Application servers handle the core logic of the Student Management System and process dynamic requests from users. To maintain security, these servers should be placed in a private subnet, meaning they only accept traffic routed internally through the load balancer.

## Database
The database securely stores sensitive student records. To protect against unauthorized external access and potential data breaches, the database must remain strictly private and should never be directly accessible from the public Internet.


# Public and Private Resources

| Resource | Public or Private? | Explanation |
| :--- | :--- | :--- |
| CDN | Public | Must be accessible to users over the internet to deliver static content globally. |
| Load Balancer | Public | Acts as the entry point for internet traffic, directing it to the private application servers. |
| Application Server | Private | Should only accept internal traffic routed through the load balancer, protecting it from direct internet exposure. |
| Database | Private | Contains sensitive student data and must only be accessible by the internal application servers. |


# Security Controls

## IAM
Identity and Access Management (IAM) restricts cloud environment access to authorized personnel only. Only designated administrators and developers should have specific permissions to manage or modify these cloud resources.

## MFA
Multi-Factor Authentication (MFA) must be enabled for all administrator and developer accounts. This provides a critical second layer of security in case account passwords are stolen or compromised.

## Firewall / Security Group
Network traffic must be strictly controlled to prevent unauthorized access to backend systems.
* Internet -> Load Balancer = Allowed
* Load Balancer -> Application Server = Allowed
* Application Server -> Database = Allowed
* Internet -> Database = Blocked

## Encryption
Student information must be encrypted both at rest (in the database) and in transit (over the network) to protect sensitive personal data. This ensures that even if data is intercepted or storage is breached, the information remains completely unreadable to attackers.

## Logging
All system activities, including login attempts, infrastructure configuration changes, and database queries, must be recorded. This audit trail is essential for investigating security incidents and tracking who made specific changes.

## Monitoring
The system should be actively monitored for suspicious activities, such as unusual traffic spikes or repeated failed logins. Early detection allows administrators to respond to potential threats like DDoS attacks before they cause application downtime.

## Backup
The database must have automated, regular backups stored securely. This guarantees that student data can be fully restored in the event of hardware failure, accidental deletion, or ransomware attacks.


# Principle of Least Privilege

| User | Allowed Access |
| :--- | :--- |
| Administrator | Full access to configure and manage cloud resources, networking, and security groups. |
| Instructor | Read-only access to view all student records through the web application interface. |
| Student | Read-only access to view only their own personal records. |
| Developer | Access to manage application code and servers, with no access to production student data. |


# Shared Responsibility Model

| Responsibility | Cloud Provider or Customer? |
| :--- | :--- |
| Physical data center | Cloud Provider |
| Physical servers | Cloud Provider |
| User accounts | Customer |
| Student data | Customer |
| IAM permissions | Customer |
| Application security | Customer |
| Database access rules | Customer |
| Backups | Customer |

1. **What does Security OF the Cloud mean?**
Security of the cloud means the cloud provider is responsible for protecting the underlying infrastructure that runs all the services offered in the cloud, including hardware, software, networking, and physical facilities. 

2. **What does Security IN the Cloud mean?**
Security in the cloud means the customer is responsible for securing their own data, applications, identity management, and operating system configurations within the cloud environment.

3. **Which resource should be directly accessible from the Internet?**
The CDN and the Load Balancer should be directly accessible from the Internet. 

4. **Why should the database remain private?**
The database contains sensitive student records that must be protected from external threats. Keeping it private prevents unauthorized access and data breaches.

5. **Why should users not connect directly to the database?**
Direct connections expose the database to the internet, creating a massive security vulnerability. Users should only interact with the application server, which acts as a secure middleman.

6. **What is the purpose of a load balancer?**
A load balancer distributes incoming user traffic evenly across multiple application servers. This ensures high availability and prevents any single server from crashing under heavy load.

7. **What happens if one application server fails?**
The load balancer detects the failure and automatically redirects traffic to the remaining healthy application servers. This keeps the application online without interruption.

8. **What is the purpose of a CDN?**
A CDN caches static files on servers geographically closer to the user to improve loading speeds. It also reduces the strain on the main application servers by handling static content delivery.

9. **Why should administrator accounts use MFA?**
Administrator accounts have total control over the cloud environment, making them high-value targets for attackers. MFA requires a second form of verification, blocking unauthorized access even if a password is stolen.

10. **Why should administrator access not be given to every employee?**
Following the principle of least privilege minimizes the risk of accidental deletions, misconfigurations, or internal security breaches. Only personnel who absolutely require administrative access to perform their duties should be granted it.

11. **Why are logging and monitoring important?**
Logging and monitoring provide critical visibility into the system to detect suspicious behavior and audit access. They allow security teams to troubleshoot performance issues and respond to threats quickly.

12. **Why are backups important?**
Backups ensure that crucial student data can be quickly recovered in an emergency. They protect the system against data loss from accidental deletion, hardware failure, or ransomware attacks.

