# -TW-Assignment

# Problem Statement
A development team has created a Java web application that is ready for a limited release (with reduced availability and reliability requirements - till we get to production). If the limited release is successful, the app will be rolled out for worldwide use. Once fully public, the application needs to be available 24/7 and must provide sub-second response times and continuity through single server failures - targeting 4-9’s availability.

<img alt="ALT test" src="UAT.png">

# Solution Overview

Prerequisites – Ansible 2.4 or above installed in a linux machine.

This solution uses Ansible to create the requisite infrastructure on AWS. Tomcat will be used for serving the dynamic content whereas Nginx will work as a proxy server as well as serve the static content.

Before creating the Infrastructure on your AWS account, you need to replace the values of <aws_access_key> and <aws_secret_key> in a file named ‘all’ located inside group_vars directory.Once it is done, you can just run the Ansible playbook Test.yml by running the following command from your Ansible server ->

Ansible-playbook Test.yml

Before creating any EC2 instances, script will create VPC, subnets, route tables, security groups. Security groups will be attached to respective servers based on what kind of access is required for the servers. At the end of the this operation, we will have two servers(web and proxy) with us. The script will proceed forward to install tomcat server and the given web application(comapnyNews.war) on the Web Server instance. Once that is done, it will install and configure Nginx on proxy server so that it serves the static content from within and redirects all other requests to Web Server on port 8080.

Self-signed certificates are used to ensure that the connection to Nginx server is encrypted. Those certificates can be found at ConfigureStaticAppOnProxyServer/files folder in the provided solution.

Once the script execution is complete(approx. 6-8 mins), we will be able to access the companyNews blog at https://<proxy_server_public_ip>.

![alt text](images/Prod.png "Production Solution")
