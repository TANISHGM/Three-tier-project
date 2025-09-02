# Three-Tier Architecture Project

## Project Overview
This project demonstrates a **Three-Tier Architecture** deployed on AWS using EC2 instances, RDS, and Load Balancers.  
It follows the standard design pattern for scalable, secure, and highly available web applications.

The architecture consists of:
1. **Presentation Layer (Frontend)** – Internet-facing Load Balancer (ALB) serving web requests.
2. **Application Layer (Backend)** – Application servers (EC2) behind an internal Load Balancer.
3. **Database Layer** – Amazon RDS instance for data storage.

---

## Security Groups Configuration
Five Security Groups are configured to control traffic flow:

1. **Internet-Facing Load Balancer (ALB) SG**
   - Allows HTTP/HTTPS traffic from the internet.
   - Restricted access to frontend EC2 instances only.

2. **Web Server EC2 SG**
   - Allows traffic only from Internet-Facing Load Balancer SG.
   - Outbound access as needed for backend communication.

3. **Internal Load Balancer SG**
   - Accepts traffic from web server EC2 SG.
   - Forwards requests to application server EC2 SG.

4. **Application Server EC2 SG**
   - Allows traffic only from Internal Load Balancer SG.
   - Connects to RDS SG for database operations.

5. **RDS SG**
   - Allows database connections only from Application Server EC2 SG.
   - No direct internet access.

---

## Architecture Workflow
1. **User request** comes from the Internet → reaches the **Internet-Facing Load Balancer**.  
2. Load Balancer routes the request to **Web Server EC2 instances**.  
3. Web Servers forward requests to **Internal Load Balancer**.  
4. Internal Load Balancer routes requests to **Application Server EC2 instances**.  
5. Application Servers communicate with **RDS database** for data storage and retrieval.  
6. Response travels back to the user through the same path.

---

## AWS Components Used
- **VPC** with public and private subnets  
- **Internet Gateway** for public access  
- **Elastic Load Balancers** (ALB)  
- **EC2 instances** for Web and App layers  
- **RDS instance** for database  
- **Security Groups** for network traffic control  

---

## How to Deploy
1. Create a VPC with public and private subnets.  
2. Launch EC2 instances for Web and App layers in appropriate subnets.  
3. Configure Security Groups as described above.  
4. Set up Internet-Facing and Internal Load Balancers.  
5. Launch RDS instance in private subnet.  
6. Test the workflow from Internet → Web → App → RDS.

---


