# ansible_usecase

## Description
  To run the playbook to provision an EC2 instance(dbserver and webserver) of Ubuntu on the default AWS profile
```  
ansible-playbook -i hosts -e pem_file=~/.ssh/your.pem -e key_name=your_keyname site.yml
```
# Roles
  * ec2_dbserver
  * ec2_webserver
  * springboot
  * tomcat
  * mongodb  
  
# site.yml

  * provisioning 2 instances using ec2_webserver and ec2_dbserver roles
  * ## WebServer
    * Install Tomcat Server
    * deploy spring boot application by configuring the application name or source url in inventory file 
  * ## DB Server
    * Import the public key used by the package management system
    * Add MongoDB Repository 
    * Install MongoDb Server
    * Start Mongodb Server

### Example Playbook
Minimal playbook for deploying spring boot application
```
     - hosts: all
       vars:
         springboot_application_name: spring-boot-sample
         springboot_src: tests/spring-boot-sample.jar
       roles:
        - role: ansible-springboot
```        
In order to run this playbook, the path of the ssh private key file for the key_name has to be specified in the command line under the var name of pem_file. The correct name for the keypair should be specified for key_name. It is also assumed that ~/.aws/credentials is set up with the access_key and secret_key for either the default profile or a specific profile. Further more, it is also assuemd that the ssh key pair has been set up on the AWS region.
