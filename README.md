# Azure Scalable NGINX Web Application

## 📌 Project Overview
This project demonstrates the deployment of a highly available and auto-scaling static web application on Microsoft Azure.  
The solution leverages core Azure infrastructure services to ensure the web application is resilient, performant, and can automatically adapt to varying user loads — showcasing best practices for cloud deployments.

---

## 🚀 Key Features

- **High Availability**: Implemented using an Azure Load Balancer to distribute incoming traffic across multiple backend instances.
- **Automatic Scaling**: VM instances scale automatically based on CPU utilization.
- **Network Security**: NSG rules allow secure HTTP access and block unwanted traffic.
- **Automated Deployment**: NGINX + HTML page setup via custom Bash script.
- **Public Accessibility**: Application is accessible through a dedicated public IP.

---

## 🧱 Architecture

The project includes the following Azure components:

- **Resource Group** (`myWebAppRG`): Logical container for resources.
- **Virtual Network** (`myVNet`): Provides secure network environment.
- **Public IP** (`myPublicIP`): Exposes the app to the internet.
- **Load Balancer** (`myLoadBalancer`):
  - *Frontend IP Configuration*: Entry point for users.
  - *Backend Pools*: Contains VMSS instances.
  - *Health Probes*: Route traffic only to healthy VMs.
- **Network Security Group** (`myNSG`): Allows HTTP (port 80) traffic.
- **Virtual Machine Scale Set** (`myWebAppScaleSet`):
  - Initial instance count: 2
  - Scale-out: CPU > 70%
  - Scale-in: CPU < 30%

---

## ⚙️ Deployment & Setup

### 1. **Azure Resource Setup**:
- Create RG, VNet, Public IP, Load Balancer, NSG
- Attach Load Balancer backend pool to VMSS

### 2. **VMSS Configuration**:
- Associate with subnet & Load Balancer
- Use custom Bash script for provisioning

---

## 📝 Bash Script for VM Web Server Setup

```bash
#!/bin/bash
apt update
apt install nginx -y
rm /var/www/html/index.nginx-debian.html
echo "<!DOCTYPE html>
<html>
<head>
  <title>Mera Pehla Web Page</title>
</head>
<body>
  <h1>Swagat Hai!</h1>
  <p>Yeh mera pehla web page hai jo Azure par chal raha hai.</p>
</body>
</html>" > /var/www/html/index.html
systemctl start nginx
systemctl enable nginx

