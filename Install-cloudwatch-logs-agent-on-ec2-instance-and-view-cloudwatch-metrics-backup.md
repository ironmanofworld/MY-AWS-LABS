## Install CloudWatch Logs Agent on EC2 Instance and View CloudWatch Metrics

**This can be very helpful when testing your application.**


Architecture Diagram
![This is an image](https://play.whizlabs.com/frontend/web/media/task_id_124/task_id_124__install_cloudwatch_logs_agent_on_ec2_instance_and_view_cloudwatch_metrics.png)


     
 **Task Details**:grinning: 
1. Sign into the AWS Management Console.
2. Create an EC2 instance.
3. SSH into EC2 Instance.
4. Download and Install the Cloudwatch agent on EC2.
5. Configure and Start the Agent.
6. View the metric in the Cloudwatch Metrics.
7. Launching Lab Environment, To launch the lab environment, Click on the  button.

Please wait until the cloud environment is provisioned. It will take less than a minute to provision.


**Launching an EC2 Instance**
1. Choose an Amazon Machine Image (AMI): Select Amazon Linux 2 AMI in the drop-down, Choose architecture as 64-bit(x86),Choose an Instance Type: Select t2.micro.
2. For Key pair: Select Create a new key pair Button, create keypair and **do ssh using puttygen and later putty when your instance started**
3. create security group, ssh, http, https---Anywhere. create an instance role
4. Add user data 
#!/bin/bash
sudo su
yum update -y
yum install httpd -y
cd/var/www/html
echo "Hi from server" >/var/www/html/index.html
systemctl start httpd
systenctl enable httpd
systemctl status httpd

5. SSH into the EC2 Instance
6. Download and Install the Cloudwatch Agent 
- wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
![Download and Install the Cloudwatch Agent](https://play.whizlabs.com/frontend/web/media/task_id_124/image31.png)

8. Install the Cloudwatch Agent
- sudo rpm -U ./amazon-cloudwatch-agent.rpm
![](https://play.whizlabs.com/frontend/web/media/task_id_124/image30.png)

9. Configure and Start the Cloudwatch Agent, Open the setup wizard
- sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard

![](https://play.whizlabs.com/frontend/web/media/task_id_124/image24.png)

10. **Enter these values asked during setup:**

On which OS are you planning to use the agent? : Enter 1

Are you using EC2 or On-Premises? : Enter 1

Which user are you planning to run the agent? : Enter 1

Do you want to turn on the StatsD daemon? : Enter 2

Do you want to monitor metrics from CollectD? : Enter 2

Do you want to monitor any host metrics? Enter 1

Do you want to monitor CPU metrics per core? Enter 1

Do you want to add ec2 dimensions into all of your metrics if the info is available? : Enter 1

Would you like to collect your metrics at high resolution? : Enter 1 (1s)

Which default metrics config do you want?: Enter 2

Are you satisfied with the above config? Enter 1

Do you have any existing CloudWatch log Agent configuration file to import for migration? : Enter 2

Do you want to monitor any log files? : Enter 2

Do you want to store the config in the SSM parameter store? : Enter 2

Note: if you make any mistakes in the above configuration, you can run the configuration setup again whenever you want. The configurations that you make is saved in a JSON File.


11. Start the Agent:

- sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s

12. Check Agent Status

- systemctl status amazon-cloudwatch-agent
![](https://play.whizlabs.com/frontend/web/media/task_id_124/image7.png)

13. View the CloudWatch Metrics
Navigate to CloudWatch by clicking on the  menu available under the Management and Governance section.
Make sure you are in the N.Virginia Region.
Click on Metrics in the Left Panel.
You should be able to see CWAgent under All Metrics (Custom Namespaces). 
Note: If you are not able to see CWAgent, please wait for at least 2 minutes and then refresh the browser page.

![](https://play.whizlabs.com/frontend/web/media/task_id_124/image36.png)

14. Click on the CloudWatch Agent and you will be able to see visuals for that metric

![](https://play.whizlabs.com/frontend/web/media/task_id_124/image17.png)

15. Click on any Metric and you will be able to see the metrics on the above graph refreshed every 1 sec

![](https://play.whizlabs.com/frontend/web/media/task_id_124/image35.png)







