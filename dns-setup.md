# Handling Changing AWS EC2 IP for Jenkins

Since I’m using the AWS Free Tier, I can’t assign an Elastic IP without incurring costs.
To avoid charges, I stop the EC2 instance when it’s not in use.
However, this causes AWS to assign a new public IP each time the instance starts.

Normally, I’d have to update Jenkins’ IP configuration in:

/var/lib/jenkins/jenkins.model.JenkinsLocationConfiguration.xml

### Solution: Use a Domain with Cloudflare A Record
Create an A record in Cloudflare:

Name: jenkins

Domain: gamersunited.cy

Value: Current EC2 public IPv4

Proxy status: DNS only

<img width="1290" height="108" alt="image" src="https://github.com/user-attachments/assets/714e007b-4ef3-466c-bd0b-da679e8ae81e" />

In Jenkins, set the URL to the domain instead of the raw IP.
This way, I only need to update the Cloudflare A record when AWS changes the IP — no Jenkins config edits required.

### Example JenkinsLocationConfiguration.xml
```xml
<?xml version='1.1' encoding='UTF-8'?>
<jenkins.model.JenkinsLocationConfiguration>
  <jenkinsUrl>http://jenkins.gamersunited.cy:8080/</jenkinsUrl>
</jenkins.model.JenkinsLocationConfiguration>
```

This keeps Jenkins accessible via:
http://jenkins.gamersunited.cy:8080/


