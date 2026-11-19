# AWS-LOAD-BALANCER
# EX 5 AWS LOAD BALANCER
# REG NUMBER: 212225040478
# NAME:Vahini L
## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
### Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

### Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

### Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

### Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

### Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

### Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## OUTPUT

<img width="1920" height="1080" alt="Screenshot (490)" src="https://github.com/user-attachments/assets/7a90eba8-e035-4582-8224-36ee64746f5f" />
<img width="1920" height="1080" alt="Screenshot (491)" src="https://github.com/user-attachments/assets/345c213a-6bc7-4ede-89e3-a1bd30c2ced9" />
<img width="1920" height="1080" alt="Screenshot (492)" src="https://github.com/user-attachments/assets/98be75f8-5cae-4526-aa25-eb17beb4ea15" />
<img width="1920" height="1080" alt="Screenshot (493)" src="https://github.com/user-attachments/assets/4110215d-e1f5-415b-abe6-1318cb758cfc" />
<img width="1920" height="1080" alt="Screenshot (494)" src="https://github.com/user-attachments/assets/062e8610-6024-4dd5-9a10-e828d9f6bccf" />
<img width="1920" height="1080" alt="Screenshot (495)" src="https://github.com/user-attachments/assets/a50b79b8-2056-4683-9b95-331ddfbef126" />
<img width="1920" height="1080" alt="Screenshot (498)" src="https://github.com/user-attachments/assets/05d83e89-3cd7-4590-8406-4a2c08b57944" />
<img width="1920" height="1080" alt="Screenshot (500)" src="https://github.com/user-attachments/assets/be4dbb41-a39a-4711-8f70-eedc93727b4f" />
<img width="1920" height="1080" alt="Screenshot (501)" src="https://github.com/user-attachments/assets/dad2a013-340a-43f1-976c-1f1509792874" />
<img width="1920" height="1080" alt="Screenshot (502)" src="https://github.com/user-attachments/assets/593bb970-d021-4173-9de3-b75b5bc75529" />
<img width="1920" height="1080" alt="Screenshot (503)" src="https://github.com/user-attachments/assets/02a9bfd9-66d1-467d-8b78-61b534d5fec1" />
<img width="1920" height="1080" alt="Screenshot (504)" src="https://github.com/user-attachments/assets/c27d75fc-78e2-4807-96cc-db28b090104d" />



## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
