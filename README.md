# **🚀TravelMemory Deployment on AWS**





### *📌**Overview**:*

### 

### This project demonstrates deployment of a MERN stack application on AWS EC2 with Nginx, Load Balancer, and Cloudflare integration.





### The objective is to host a scalable web application with proper routing, reverse proxy configuration, and global DNS optimization.

============================================================================



#### **Tech Stack**



* Frontend: React
* Backend: Node.js
* Database: MongoDB
* Web Server: Nginx
* Cloud: AWS EC2, AWS ALB, AWS Target Groups
* DNS \& Security: Cloudflare



============================================================================



##### **Deployment Architecture**



###### **Flow:**



* User → Cloudflare → Load Balancer → EC2 → Nginx → Backend → MongoDB



============================================================================



##### **1. GitHub Repository Setup**

##### 

* GitHub repository created for deployment documentation \& initial commit pushed to GitHub repository.
* Reference screenshot: Screenshots/github-repo.png \& github-push.png



============================================================================



##### **2. EC2 Instances Setup**



* Ubuntu EC2 instances (x2) launched
* Security groups configured (22, 80, 443, 3000, 3001)
* Reference screenshot: Screenshots/ec2.png, ec2-1.png, SSH.png \& ec2-multiple.png



============================================================================



##### **3. Environment Setup**



###### **Installed required dependencies on both EC2 instances:**



* Reference screenshot: Screenshots/Linux-setup.png



============================================================================



##### **4. Project Deployment on EC2 (x2)**



###### **Cloned repository and installed dependencies:**



* git clone https://github.com/UnpredictablePrashant/TravelMemory.git
* cd TravelMemory
* Reference screenshot: Screenshots/project-files.png



============================================================================



##### **5. Backend Deployment (x2 instances)**



* cd backend
* npm install
* pm2 start index.js
* Reference screenshot: Screenshots/backend-install.png, env.png, backend-running.png, backend-browser.png



============================================================================



##### **6. Frontend Build (x2 instances)**



* cd frontend
* npm install
* npm run build
* Reference screenshot: Screenshots/frontend-install.png, frontend-build.png





============================================================================



##### **7. API Route Fix (Critical) (x2 instances)**



###### **Issue:**



Frontend API calls were not working due to route mismatch.



* Frontend: /api/trip
* Backend: /trip



###### **Fix:**



app.use('/api/trip', tripRoutes)



* Reference screenshot: Screenshots/API-route-fix.png



============================================================================



##### **8. Nginx Configuration (x2 instances)**





###### **Configured reverse proxy:**



*server {*

&#x20;   *listen 80;*



&#x20;   *location / {*

&#x20;       *root /home/ubuntu/TravelMemory/frontend/build;*

&#x20;       *index index.html;*

&#x20;       *try\_files $uri /index.html;*

&#x20;   *}*



&#x20;   *location /api {*

&#x20;       *proxy\_pass http://localhost:3000;*

&#x20;   *}*

*}*



* sudo systemctl restart nginx
* Reference screenshot: Screenshots/nginx.png



============================================================================



##### **9. Checking if both the instances are working after the update of url.js file**



* src/url.ls
* Reference screenshot: Screenshots/frontend-url.png, final-app.png



============================================================================





##### **10. Target Group Configuration**



A target group was created to register EC2 instances and route traffic from the Load Balancer.



###### **Steps:**



* Navigated to Target Groups in Amazon Web Services Console
* Selected Target type: Instances
* Protocol: HTTP
* Port: 80



###### **Health Check Configuration:**



* Protocol: HTTP
* Path: /
* Ensures application availability before routing traffic



###### **Instance Registration:**



* Added EC2 instances to the target group
* Verified health status as healthy



* Reference screenshot: Screenshots/target-group.png



============================================================================



##### **11. Load Balancer Setup**



Configured an Application Load Balancer to distribute incoming traffic across multiple EC2 instances.



###### **Steps:**



* Created Application Load Balancer
* Attached the previously created Target Group
* Configured listener on port 80
* Enabled routing to healthy instances.
* Copied ABL's DNS and checked if ABL is working as expected.
* Reference screenshot: Screenshots/loadbalancer.png \& loadbalance-test.png



============================================================================



##### **12. Cloudflare Integration**



The domain makemyapp.site was configured using Cloudflare.



###### **Configuration Steps:**



* Domain added to Cloudflare
* Nameservers updated at registrar
* DNS record created pointing to Load Balancer
* Proxy enabled
* Reference screenshot: Screenshots/cloudflare.png



============================================================================



##### **13. Final Application**



The application is successfully deployed and accessible at:



***👉 https://makemyapp.site/***



* Reference screenshot: Screenshots/domain-working.png



###### **Key Validations:**



* Frontend loads via domain
* Backend APIs working correctly
* Load Balancer distributing traffic
* Nginx handling routing
* Cloudflare proxy active



============================================================================





























