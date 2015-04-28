# Ansible playbook for Chaos Monkey

What is Chaos Monkey and Why we need to use it.

Chaos Monkey is a software tool that was developed by Netflix engineers to test the resiliency and recoverability of their Amazon Web Services (AWS). 

The software simulates failures of instances of services running within Auto Scaling Groups (ASG) by shutting down one or more of the virtual machines. According to the developers, Chaos Monkey was named for the way it wreaks havoc like a wild and armed monkey set loose in a data center.

Chaos Monkey works on the principle that the best way to avoid major failures is to fail constantly. However, unlike unexpected failures, which seem to occur at the worst possible times, the software is opt-out by default. It can also be configured for opt-in.

Chaos Monkey has a configurable schedule that allows simulated failures to occur at times when they can be closely monitored.  In this way, it’s possible to prepare for major unexpected errors rather than just waiting for catastrophe to strike and seeing how well you can manage.


Before running the playbook, you need to set the values for the below ones

```

Edit file:-  hosts.ini and give your hosts ipaddress

```

```
Edit file:-  awsconfig in the aws role

aws_access_key_id      --> your AWS Access Key
aws_secret_access_key  --> your AWS Secret Key
region                 --> your AWS Region

```

[For Refering Client-Settings!] (https://github.com/Netflix/SimianArmy/wiki/Client-Settings)

```
Edit file:-  client.properties in the chaos role 

simianarmy.client.aws.accountKey  --->  your AWS Access Key
simianarmy.client.aws.secretKey   --->  your AWS Secret Key
simianarmy.client.aws.region      --->  your AWS Region

```

[For Refering Chaos-Settings!] (https://github.com/Netflix/SimianArmy/wiki/Chaos-Settings)

```
Edit file:-  chaos.properties in the chaos role

I already have an Autoscaling group named "autoscale-1" and I am adding it in here.
Right now In this playbook, I dint add the feature to create its own Auto scaling group and launch configs. 
Will do it in the coming days.

So you need to add your Autoscaling group in here:

simianarmy.chaos.ASG.autoscale-1.enabled = true
simianarmy.chaos.ASG.autoscale-1.probability = 3.0

simianarmy.chaos.notification.sourceEmail --->  Set the source email that sends the termination notification
simianarmy.chaos.notification.global.receiverEmail ---> Set the destination email the termination notification is sent to for all instance groups

```
#you can run this playbook by the below command

```
$ ansible-playbook -i hosts.ini -s chaosmonkey.yml

```
If you are using AWS SES verified email address, then you will get notifications like below.

![](https://s3.amazonaws.com/uploads.hipchat.com/346676/2098603/vVrPGqQCDstueCz/chaos.png)

