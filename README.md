## Deploying a Multi-Tier Website Using AWS EC2 and RDS

In this tutorial, we'll cover the step-by-step process of deploying a multi-tier website on AWS using Amazon EC2 for hosting the website and Amazon RDS for the MySQL database. We'll also set up auto-scaling for high availability and create a load balancer to distribute traffic across multiple instances.

### Prerequisites

Before you begin, ensure you have:

- An AWS account with appropriate permissions.
- Basic knowledge of AWS services like EC2, RDS, and load balancers.

### Step 1: Launching an EC2 Instance

1. **Launch an EC2 Instance**
   - Log in to your AWS Management Console.
   - Navigate to EC2 and click on "Launch Instance."
   - Choose Ubuntu Server as the AMI.
   - Select `t2.micro` as the instance type.
   - Create a new key pair (e.g., `my-keypair`) for SSH access and download the private key.
   - Configure security group (`website-deploy-security-group`) to allow all traffic (0.0.0.0/0).

### Step 2: Setting Up Apache and PHP

2. **Install Apache and PHP**
   ```bash
   sudo apt-get update
   sudo apt-get install apache2 -y
   cd /var/www/html
   sudo rm index.html
   sudo nano index.php
   ```
   Add your PHP code in `index.php` to display a basic webpage.

### Step 3: Setting Up RDS Database

3. **Create an RDS Instance**
   - Navigate to RDS in the AWS Management Console.
   - Click on "Create database" and choose MySQL as the engine.
   - Configure database details (e.g., `multi-tier-website-DB`).
   - Set master username and password.
   - Connect the RDS instance to the EC2 instance's security group.

### Step 4: Configuring Website to Use RDS

4. **Configure PHP to Connect to RDS**
   ```bash
   sudo apt-get install mysql-server -y
   sudo mysql -h multi-tier-website-db.cvwwkjmmcvgi.us-east-1.rds.amazonaws.com -u admin -padmin123
   ```
   Execute the following SQL commands:
   ```sql
   show databases;
   use intel;
   create table data(firstname varchar(20), email varchar(20));
   insert into data values('AWS', 'aws@support.com');
   select * from data;
   ```

### Step 5: Enabling Auto Scaling and Load Balancing

5. **Create Load Balancer and Auto Scaling Group**
   - Create an AMI from the EC2 instance.
   - Navigate to EC2 > Instances, select your instance, and click "Actions" > "Image and templates" > "Create image."
   - Set up an Application Load Balancer (ALB) in the AWS Management Console.
   - Create a target group for instances.
   - Configure auto-scaling group with the created AMI and ALB.

### Step 6: Testing and Verification

6. **Testing the Setup**
   - Access the website through the load balancer's DNS.
   - Add data to the website and verify database entries.

### Conclusion

Congratulations! You've successfully deployed a multi-tier website on AWS using EC2 for web hosting, RDS for database management, and auto-scaling for high availability. Feel free to customize and expand upon this setup based on your project requirements.

### Additional References

For more information and detailed documentation, refer to the following links:

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [AWS RDS Documentation](https://docs.aws.amazon.com/rds/)
- [AWS Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/)
- [AWS Elastic Load Balancing Documentation](https://docs.aws.amazon.com/elasticloadbalancing/)


