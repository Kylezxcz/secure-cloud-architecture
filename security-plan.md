# Secure Cloud Architecture Plan

## CDN
The CDN stores cached copies of static content (like your HTML and CSS files) closer to users' geographic locations. This reduces latency, improves the overall loading speed of the web application, and decreases the direct traffic hitting your main infrastructure.

## Load Balancer
The load balancer distributes incoming internet requests evenly across multiple application servers. This ensures high availability, prevents any single server from crashing under heavy traffic, and acts as the secure entry point for the application.

## Application Servers
Application servers handle the core logic of the Student Management System and process dynamic requests from users. To maintain security, these servers should be placed in a private subnet, meaning they only accept traffic routed internally through the load balancer.

## Database
The database securely stores sensitive student records. To protect against unauthorized external access and potential data breaches, the database must remain strictly private and should never be directly accessible from the public Internet.
