# ansible_usecase

## Description
  To run the playbook to provision an EC2 instance(dbserver and webserver) of Ubuntu on the default AWS profile
  
### cmd
     ansible-playbook -i hosts -e pem_file=~/.ssh/your.pem -e key_name=your_keyname site.yml
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
Minimal playbook:

     - hosts: all
       vars:
         springboot_application_name: spring-boot-sample
         springboot_src: tests/spring-boot-sample.jar
       roles:
        - role: ansible-springboot
