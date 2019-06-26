# Using VM-Series with AWS VPC Traffic Mirroring
This repository provides a sample firewall configuration that you can import into VM-Series. This sample configuration enables the VXLAN tunnel content inspection (TCI) feature to receive packets sent by the AWS VPC Traffic Mirroring service. This will allow you to get visibility, and detect and respond to attacks by sending copies of all packets sent/received by your AWS instances to VM-Series without putting the firewall inline. Putting the VM-Series inline with the traffic flow will allow you actually prevent attacks in real-time. You can also use this capability to run a security lifecycle report (SLR) on your public cloud deployment. 

## Prerequisites
1. Read details of [AWS VPC Traffic Mirroring](https://aws.amazon.com/blogs/aws/new-vpc-traffic-mirroring/)
1. Read an overview of use cases of how [VM-Series works with Traffic Mirroring](https://blog.paloaltonetworks.com/2019/06/cloud-see-unseen-aws-mirrored-traffic-vm-series/)
1. PAN-OS 9.0 or higher is required. Mirrored packets are sent by AWS in a VXLAN encapsulated tunnel. This can be handled using the [PAN-OS VXLAN TCI](https://docs.paloaltonetworks.com/pan-os/9-0/pan-os-new-features/networking-features/vxlan-tunnel-content-inspection.html) feature. 

## How To
Steps for setting up AWS VPC Traffic Mirroring
1. Deploy and configure VM-Series from [AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=0ed48363-5064-4d47-b41b-a53f7c937314). Use BYOL edition if you have a trial/evaluation/full license, or use the pre-licensed PAYG options. A 15-day free trial for VM-Series software is availale for first-time customers (normal compute/storage charges will still apply). After 15 days hourly charges will apply. Be sure to shutdown the trial if you're not using the instance to avoid unnecessary charges. See [AWS Marketplace documentation](https://docs.aws.amazon.com/marketplace/latest/buyerguide/buyer-free-trials.html) on free trials for more information. 
2. Follow [documentation](https://docs.paloaltonetworks.com/vm-series/7-1/vm-series-deployment/set-up-the-vm-series-firewall-in-aws/launch-the-vm-series-firewall-in-aws.html) to deploy a 3 ENI setup of VM-Series and do the basic setup to configure a password (up to Step 5 in documentation link). (A CFT of this is coming soon). 
3. Import the sample PAN-OS configuration file (aws-mirroring-sample.xml) from the repository into VM-Series. 
4. Load the imported configuration. IMPORTANT: Set the password immediately (Device > Setup > Operations > Import).
5. Commit the configuration. 
6. Follow AWS VPC Traffic Mirroring steps to send traffic from any of your instances to the Untrust ENI of VM-Series.
7. Check the Monitor tab in VM-Series to see the traffic sent.
8. Customize security policies to match your use case.
9. Enable [Log Filtering](https://docs.paloaltonetworks.com/pan-os/8-0/pan-os-new-features/management-features/selective-log-forwarding-based-on-log-attributes) to find high or critical level items, or specific attacks.
10. Enable a webhook also known as [Action-Oriented Log Forwarding using HTTP](https://docs.paloaltonetworks.com/pan-os/8-0/pan-os-new-features/management-features/action-oriented-log-forwarding-using-http) to trigger an action: create a service desk ticket, or launch an AWS Lambda function to quarrantine. 

For scaled out deployments and high availability: You can deploy 2 or more instances of VM-Series behind the the [NLB with UDP load balancing](https://aws.amazon.com/blogs/aws/new-udp-load-balancing-for-network-load-balancer/).
