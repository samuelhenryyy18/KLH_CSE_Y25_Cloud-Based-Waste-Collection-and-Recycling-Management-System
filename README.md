-Cloud-Based Waste Collection and Recycling Management System

-Project Details

- Project Title: Cloud-Based Waste Collection and Recycling Management System
- Team Number: 1
- Section: 4
- Project Guide: Dr. V. Sireesha

- Team Members
 Vennela Eadala- 2520030288
  K. Sharanya -  2520030277 
 Jasmitha - 2520030557 



 # 1. Abstract

Municipal waste management teams often manage collection routes, vehicles, schedules, and recycling records using spreadsheets and manual communication. This project proposes a Cloud-Based Waste Collection and Recycling Management System that simplifies these operations through a centralized application.

The system provides two major modules:

1. Municipal Management: Administrators can register collection points, schedule waste pickups, assign vehicles and drivers, monitor collection status, manage cleaning operations, and maintain recycling statistics.

2. Citizen Participation: Citizens can report unclean areas by capturing and uploading geo-tagged photographs along with their geographical location. The waste management team can view these reports, identify the exact location, check whether the area's waste has been collected and cleaned, assign cleaning tasks, and update the cleaning status. Citizens can also track the progress of their submitted reports.

The application is designed to run using Docker containers on Amazon EC2 instances, supported by Elastic Load Balancing and EC2 Auto Scaling for availability and scalability.

A custom Amazon VPC provides secure networking through public, private application, and private data subnets across two Availability Zones. Amazon RDS stores operational data, Amazon ECR stores container images, Amazon S3 stores uploaded photographs, and Amazon CloudWatch monitors logs, metrics, resource utilization, and errors.


# 2. Problem Statement

Traditional waste management systems often depend on manual reporting, spreadsheets, and communication between municipal workers. This can result in delayed waste collection, missed pickups, inefficient vehicle assignments, and difficulty tracking cleaning operations.

The objective of this project is to develop a cloud-based waste management application that supports:

- Registering and managing waste collection points.
- Scheduling daily and weekly waste pickups.
- Assigning vehicles and drivers to collection routes.
- Tracking waste collection and cleaning status.
- Maintaining recycling statistics.
- Allowing citizens to report unclean areas through geo-tagged photographs.
- Enabling administrators to identify reported locations and monitor cleaning progress.
- Allowing citizens to track their submitted complaints.
- Deploying the application using Docker on AWS.
- Providing scalability, secure networking, and monitoring.


# 3. Motivation

- Cleaner Cities: Prevent missed and delayed waste collection.
- Efficient Operations: Improve scheduling and vehicle utilization.
- Better Recycling: Monitor recycling volumes and identify areas for improvement.
- Citizen Participation: Allow people to actively report waste accumulation in their neighbourhoods.
- Location-Based Reporting: Identify unclean areas using geo-tagged photographs.
- Accountability: Help municipal teams track and verify cleaning progress.
- Faster Response: Enable authorities to identify and respond to waste-related complaints efficiently.


# 4. Major Modules

The application is divided into two major modules.

- Module 1: Municipal Management

Administrators and municipal waste management teams manage the overall waste collection and cleaning operations.

Functionalities:

- Manage waste collection points and locations.
- Create daily or weekly pickup schedules.
- Assign vehicles and drivers to collection routes.
- Monitor collection status.
- Manage citizen waste reports.
- Assign cleaning tasks to municipal workers.
- Update cleaning progress.
- Maintain recycling statistics and reports.
- Monitor application activities.

- Module 2: Citizen Participation

Citizens can directly participate in maintaining cleanliness by reporting waste accumulation in their surroundings.

Functionalities:

- Capture photographs of waste-filled or unclean areas.
- Upload photographs with geographical coordinates.
- Automatically capture GPS location with user permission.
- Submit complaints with descriptions.
- View submitted reports.
- Track complaint and cleaning status.
- Check whether the reported area has been cleaned.
- Optionally view before-and-after cleaning photographs.


# 5. Functionalities

 1. Collection Point Management
Register and update waste bins and collection locations.

2. Pickup Scheduling
Create daily or weekly waste collection schedules.

 3. Vehicle Assignment
Assign vehicles and drivers to specific collection routes.

 4. Collection Status Tracking
Track pickup status using:
- Pending
- In Progress
- Done

 5. Recycling Statistics
Record and report recycled waste volumes by type.

 6. Citizen Waste Reporting and Geo-Tagging
Allow citizens to capture and upload photographs of waste-filled areas along with geographical coordinates. Administrators can identify the reported locations and take necessary cleaning actions.

 7. Complaint and Cleaning Status Tracking
Track citizen complaints using the following statuses:
- Pending
- Assigned
- In Progress
- Cleaned

 8. Monitoring
Monitor application logs, resource usage, system performance, and errors through dashboards and alarms.



# 6. Citizen Waste Reporting Workflow

The proposed citizen reporting feature works as follows:

1. A citizen notices an unclean area or accumulated garbage.
2. The citizen captures a photograph using the application.
3. The application requests location permission and captures GPS coordinates.
4. The photograph, geographical location, and complaint description are uploaded.
5. The report is stored in the cloud.
6. Municipal administrators view the submitted photograph and location on their dashboard.
7. The administrator assigns the cleaning task to the appropriate municipal team.
8. The cleaning team visits the reported location and collects the waste.
9. The administrator updates the report status to Cleaned.
10. Citizens can track the progress of their submitted reports.



# 7. AWS Services Used

 Amazon EC2 - Hosts Docker containers and runs the application. 
 Amazon ECR - Stores Docker container images. 
 Elastic Load Balancer - Distributes incoming traffic across EC2 instances. 
 EC2 Auto Scaling - Automatically adjusts the number of instances based on demand. 
 Amazon VPC - Provides an isolated and secure cloud network. 
 Amazon RDS - Stores collection schedules, vehicles, complaints, GPS coordinates, and operational records. 
 Amazon S3- Stores citizen-uploaded waste photographs. 
 Amazon CloudWatch - Monitors logs, metrics, resource utilization, and alarms. 
 Security Groups - Control inbound and outbound network traffic. 
 IAM Roles - Provide controlled access to AWS resources. 



# 8. Architecture and VPC Design

The application is designed within a custom Amazon VPC with the CIDR block `10.0.0.0/16`, spanning two Availability Zones.

-VPC Subnet Configuration


 Public Subnets - `10.0.1.0/24`, `10.0.2.0/24` - Load balancer and NAT gateway 
 Private Application Subnets - `10.0.11.0/24`, `10.0.12.0/24` - EC2 instances running Docker in an Auto Scaling group 
 Private Data Subnets - `10.0.21.0/24`, `10.0.22.0/24`-  Amazon RDS database with no public access 

# Architecture Flow

1. Citizens and administrators access the application through the Elastic Load Balancer.
2. The load balancer distributes requests to EC2 instances in private application subnets.
3. Docker containers run the application on EC2 instances.
4. EC2 Auto Scaling adjusts instances based on application demand.
5. Amazon RDS stores application information, including schedules, vehicle details, complaints, GPS coordinates, and cleaning status.
6. Amazon S3 stores photographs uploaded by citizens.
7. The application retrieves photograph references and report information for the administrator dashboard.
8. Amazon CloudWatch monitors application logs, CPU and memory metrics, and errors.

- Citizen Reporting Architecture Flow

Citizen → Mobile/Web Application → Elastic Load Balancer → EC2 Docker Application → Amazon S3 (Photographs) + Amazon RDS (Report Details and GPS Coordinates) → Administrator Dashboard → Cleaning Team.



# 9. Security and Monitoring

- Application instances are hosted in private application subnets.
- The RDS database is placed in private data subnets without public access.
- Security Groups control network traffic.
- IAM roles support controlled access to AWS resources.
- Amazon S3 stores uploaded photographs securely.
- Location information is collected only with the citizen's permission.
- Amazon CloudWatch provides logs, metrics, dashboards, and alarms.
- The architecture uses multiple Availability Zones to improve availability.



# 10. Expected Outcomes

The proposed system aims to:

- Provide a centralized platform for municipal waste management.
- Reduce missed and delayed waste collection.
- Improve vehicle and route management.
- Encourage citizen participation in cleanliness activities.
- Help municipal teams identify unclean areas through geo-tagged photographs.
- Improve complaint tracking and cleaning accountability.
- Maintain digital recycling records and statistics.
- Provide a scalable and reliable cloud-based application.


# 11. Conclusion

The Cloud-Based Waste Collection and Recycling Management System provides a centralized and efficient approach to managing waste collection points, pickup schedules, vehicles, cleaning operations, recycling data, and citizen complaints.

The project combines two important modules: Municipal Management and Citizen Participation. 
While municipal administrators manage collection and cleaning operations, citizens can actively report unclean areas through geo-tagged photographs and track the progress of their complaints.

Its AWS-based architecture uses Docker on EC2, Elastic Load Balancing, and Auto Scaling to support scalability and availability. 
Amazon RDS and S3 manage operational records and uploaded photographs, while a secure VPC design and CloudWatch monitoring provide network security and operational visibility.

The proposed solution aims to encourage collaboration between citizens and municipal authorities, helping create cleaner communities through efficient waste management and cloud technology.



# 12. Future Enhancements

- Integrate Google Maps or another mapping service to visualize reported waste locations.
- Introduce notifications when complaint statuses change.
- Add image-based waste classification using Artificial Intelligence.
- Implement route optimization for waste collection vehicles.
- Provide analytics dashboards for waste generation and recycling trends.
- Add duplicate complaint detection for frequently reported locations.
- Introduce before-and-after photograph verification for completed cleaning tasks.
