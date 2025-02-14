## **History of AWS**
- **2002**: AWS was launched internally at Amazon.com to externalize IT departments.
- **2004**: First public offering, **SQS (Simple Queue Service)**, was launched.
- **2006**: Expanded offerings with **SQS**, **S3 (Simple Storage Service)**, and **EC2 (Elastic Compute Cloud)**.
- AWS expanded globally, moving beyond the US to Europe and other regions.
- **Today**: AWS powers major applications like **Netflix**, **Dropbox**, **Airbnb**, and **NASA**.

---

## **AWS Today**
- **Market Position**: AWS is a leader in the **Gartner Magic Quadrant** for 13 consecutive years.
- **Revenue**: $90 billion in revenue as of 2023.
- **Market Share**: 31% of the cloud market in Q1 2024 (Microsoft is second with 25%).
- **Active Users**: Over 1 million active users.

---

## **What Can You Build on AWS?**
- **Sophisticated and Scalable Applications**: Applicable to diverse industries.
- **Use Cases**:
  - Enterprise IT transfer.
  - Backup and storage.
  - Big data analytics.
  - Hosting websites.
  - Backend for mobile and social applications.
  - Gaming servers.
- **Examples**: Netflix, McDonald's, 21st Century Fox, Activision.

---

## **AWS Global Infrastructure**
- **Regions**: Clusters of data centers around the world (e.g., US-east-1, EU-West-3).
  - Each region is a separate geographic area.
  - Services are region-scoped (using a service in one region is independent of another).
- **Availability Zones (AZs)**:
  - Each region has multiple AZs (minimum 3, maximum 6).
  - AZs are isolated from disasters (e.g., ap-southeast-2A, ap-southeast-2B).
  - Connected via high-bandwidth, low-latency networks.
- **Points of Presence (Edge Locations)**:
  - Over 400 edge locations in 90 cities across 40 countries.
  - Used for low-latency content delivery (e.g., via **CloudFront**).

---

## **Choosing an AWS Region**
Factors to consider when selecting a region:
1. **Compliance**: Data residency laws (e.g., data in France must stay in France).
2. **Latency**: Deploy close to users for reduced latency.
3. **Service Availability**: Not all regions have all services.
4. **Pricing**: Costs vary by region.

---

## **Key AWS Services**
- **Global Services**:
  - **IAM (Identity and Access Management)**. [[AWS Services - IAM (Identity and Access Management)]]
  - **Route 53** (DNS service).
  - **CloudFront** (Content Delivery Network).
  - **WAF (Web Application Firewall)**.
- **Region-Scoped Services**:
  - **EC2** (Elastic Compute Cloud).
  - **Elastic Beanstalk**.
  - **Lambda** (Serverless computing).
  - **Rekognition** (Image and video analysis).

---

## **Region Table**
- Check the **AWS Region Table** to see which services are available in specific regions.

---

## **Key Takeaways**
- AWS is a global leader in cloud computing with a vast infrastructure.
- Regions, Availability Zones, and Edge Locations form the backbone of AWS's global reach.
- Choosing the right region depends on compliance, latency, service availability, and pricing.
- AWS enables building scalable, sophisticated applications across industries.