Azure Scalable Nginx Web Application


Project Overview -
This project demonstrates the deployment of a highly available and auto-scaling static web application on Microsoft Azure. The solution leverages core Azure infrastructure services to ensure the web application is resilient, performant, and can automatically adapt to varying user loads, showcasing best practices for cloud deployments.

Key Features -
High Availability: Implemented using an Azure Load Balancer to distribute incoming traffic across multiple backend instances, ensuring continuous service.
Automatic Scaling: The application automatically scales its compute resources (VM instances) based on CPU utilization, ensuring optimal performance during peak loads and cost efficiency during low usage.
Network Security: A Network Security Group (NSG) is configured to control inbound and outbound network traffic, specifically allowing secure HTTP access to the web application.
Automated Deployment: Web server (Nginx) and custom web page deployment are automated on VM instances using a custom bash script, promoting consistency and efficiency.
Public Accessibility: The web application is accessible from the internet via a dedicated Public IP address.

Architecture -

Okay, here's a sorted and concise README file in English, designed to be clear and effective for an interviewer. It highlights the key technical aspects and achievements of your project.

Azure Scalable Nginx Web Application
Project Overview
This project demonstrates the deployment of a highly available and auto-scaling static web application on Microsoft Azure. The solution leverages core Azure infrastructure services to ensure the web application is resilient, performant, and can automatically adapt to varying user loads, showcasing best practices for cloud deployments.

Key Features-

High Availability: Implemented using an Azure Load Balancer to distribute incoming traffic across multiple backend instances, ensuring continuous service.
Automatic Scaling: The application automatically scales its compute resources (VM instances) based on CPU utilization, ensuring optimal performance during peak loads and cost efficiency during low usage.
Network Security: A Network Security Group (NSG) is configured to control inbound and outbound network traffic, specifically allowing secure HTTP access to the web application.
Automated Deployment: Web server (Nginx) and custom web page deployment are automated on VM instances using a custom bash script, promoting consistency and efficiency.
Public Accessibility: The web application is accessible from the internet via a dedicated Public IP address.

Architecture -

The project's architecture is built on the following Azure components:

Azure Resource Group (myWebAppRG): A logical container for all related resources.
Azure Virtual Network (myVNet): Provides a secure and isolated network environment for the application.
Azure Public IP (myPublicIP): The internet-facing IP address, associated with the Load Balancer.
Azure Load Balancer (myLoadBalancer): Distributes incoming HTTP traffic (Port 80) across healthy backend instances, utilizing:
Frontend IP Configuration: The public endpoint for the application.
Backend Pools: Groups the Virtual Machine Scale Set instances.
Health Probes: Monitors the health of backend instances to ensure traffic is only routed to operational servers.
Azure Network Security Group (myNSG): Applies inbound rules, notably allowing HTTP (Port 80) traffic from any source.
Azure Virtual Machine Scale Set (VMSS) (myWebAppScaleSet): Hosts the Nginx web servers. It is configured for auto-scaling:
Initial instance count: 2.
Scale-out: When average CPU usage exceeds 70%.
Scale-in: When average CPU usage drops below 30%.

Deployment & Setup-

The deployment process involves configuring the Azure infrastructure and automating the web server setup on the VMSS instances.

Azure Resource Creation: Set up the Resource Group, Virtual Network, Public IP, Load Balancer (with Frontend IP, Backend Pools, Health Probes, and Load Balancing Rules), and Network Security Group within the Azure portal.
VMSS Configuration: Deploy the Virtual Machine Scale Set, associating it with the VNet subnet and the Load Balancer's backend pool.
Automated Web Server Setup: A custom bash script is executed on each VMSS instance during provisioning to install Nginx and deploy the custom HTML content.

Web Server Configuration -

The #!/bin/bash (1).txt script automates the web server setup on each VMSS instance:

It updates package lists.
Installs the Nginx web server.
Removes the default Nginx index.html.
Creates a new index.html file with the content:
HTML

<!DOCTYPE html>
<html>
<head>
    <title>Mera Pehla Web Page</title>
</head>
<body>
    <h1>Swagat Hai!</h1>
    <p>Yeh mera pehla web page hai jo Azure par chal raha hai.</p>
</body>
</html>
Starts and enables the Nginx service.

Usage-

Once deployed, the web application can be accessed via the Public IP address configured for the Load Balancer.
