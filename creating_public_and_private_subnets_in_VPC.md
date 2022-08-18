## Create public and private subnet & Configuring Layered Security in an AWS VPC

**This can be very helpful when you want to create a private database.**


VPC Architecture Diagram
![This is an image](https://play.whizlabs.com/frontend/web/media/task_id_66/lab_57_understanding_and_configuring_layered_security_in_an_aws_vpc.png)


     
 **Task Details**:grinning: 
1. Sign into the AWS Management Console.
2. Create a VPC.
3. create 2 public and 2 private subnets PUBLIC-A, PUBLIC-B, PRIVATE-A, PRIVATE-B.
4. create route tables and associate subnets.
5. create an Internet Gateway and attach IG to VPC.
6. create a Security Group and add 2 public subnets/servers to get internet access. Add ssh, HTTP, HTTPS inbound rules to Anywhere 0.0.0.0/0 s SSH Anywhere 0.0.0.0/0.
7. create NACL Inbound rules For Private subnets and add 2 private servers or subnets, the private subnet doesn't need internet access, so you add ssh and 
   All ICMP-ipv4 inbound rules only, to anywhere 0.0.0.0/0
8. create NACL Outbound rules For 2 Private subnets and add 2 private servers or subnets, the private subnet doesn't need internet access, so you add 100-ssh,
   200-ICMP-ipv4, 300-Custom TCP(1024-65535). Outbound rules
9. Launch 4 instances Individually, and create a key pair. In Network settings, Attach VPC, Attach Security Group, Auto Assign Public-IP: Enable, PUBLIC-A, PUBLIC-B,
   PRIVATE-A, PRIVATE-B and add user data, use putty-gen to create a private key and putty to ssh into the servers.
   User data:
   
   :hugs:
   * #!/bin/bash
   - sudo su
   - yum update -y
   - yum install httpd -y
   - systemctl start httpd
   - systemctl enable httpd
   - echo "Response coming from PUBLIC-A" > /var/www/html/index.html




2.1*****creating VPC architecture*****:white_check_mark:
![](https://64.media.tumblr.com/e2bef5807bb782a926b7db8c29310581/c9c813a074581f33-02/s2048x3072/5670355100d5821688b7b54ed228358af03aad0c.pnj)
:white_check_mark:
![](https://64.media.tumblr.com/c848dc0dcc1474691c7af1911a56d0cd/c9c813a074581f33-69/s1280x1920/9849baec877e1ab0d1e3e2a1396cde2658b63a15.pnj)


6.1*****ADD SECURITY GROUPS INBOUND RULES*****:white_check_mark:
![](https://64.media.tumblr.com/14420f042b8e61dfa25bcd02d1125caf/c9c813a074581f33-42/s2048x3072/d6e8790fac3900a3bfd29c96926f10de37f88e06.pnj)


7.1*****ADD NACL INBOUND RULES*****:white_check_mark:
![](https://64.media.tumblr.com/8e6621e308e07f8d47a27631fe595f60/c9c813a074581f33-51/s2048x3072/ea028f45968b63f9b5851567bdc441bb4c3e10c0.pnj)

8.1*****ADD NACL GROUPS OUTBOUND RULES*****:white_check_mark:
![](https://64.media.tumblr.com/b7f91e19cfeb9e0f29a7651d615c68f4/c9c813a074581f33-f9/s2048x3072/dee72678269aa24552d4ea486bc781b357b65350.pnj)

9.1*****LAUNCHED 4 INSTANCES*****:white_check_mark:
![](https://64.media.tumblr.com/1f82a61677407e0fbf49391829b3344a/c9c813a074581f33-1b/s2048x3072/45076da8e13ff0c09fbf5b71890aa624bcbd5227.pnj)



**********RESPONCE OF PUBLIC SERVERS**********
PUBLIC SERVER-A:hugs::white_check_mark:
![](https://64.media.tumblr.com/0b28ba2b4c3f2f8a84c1efefaf177a1a/c9c813a074581f33-55/s2048x3072/70232d341d9d3ed588cb8c4020f1e34c0f972000.pnj)

PUBLIC SERVER-B:hugs::white_check_mark:
![](https://64.media.tumblr.com/271672865e0ab61714a9e2bf76ddf77e/c9c813a074581f33-c6/s2048x3072/4637e5738b9047b0a419d41335aa2d15da296ace.pnj)


*****CLOUDWATCH METRICS OF SERVERS*****:white_check_mark:
![](https://64.media.tumblr.com/4b854d9078d359b906663b1a58b5c556/c9c813a074581f33-5b/s2048x3072/236d3364ab4b586891f8bda7928a252f71f9bfe3.pnj)

Thanks, @AWS @Whizlabs

---------Any Queries or Doubts, please contact me in LinkedIn-------------

