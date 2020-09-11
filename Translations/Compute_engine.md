#LAB:Getting Started with Compute Engine

##Objectives:
In this lab, you will learn how to perform the following tasks:

    - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
    
    - Create a Compute Engine virtual machine using the gcloud command-line interface.
    
    - Connect between the two instances.
##Steps:

1. Create a virtual machine using the GCP Console

       $ gcloud compute instances create "my-vm-1" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default" --tags http
       
       $ gcloud compute firewall-rules create allow-http --action=AKKOW --destination=INGRESS --rules=http:80 --target-tags=http

2. Create a virtual machine using the gcloud command line

       $ gcloud compute zones list | grep us-central1
        
       $ gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

3. Connect between the two VM instances
    
    1- Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network: 
    
        - Connect to my-vm-2:
        
               $ gcloud compute ssh my-vm-2
               
        - Ping my-vm-1 from my-vm-2:
        
               $ ping my-vm-1
               
        - Use the ssh command to open a command prompt on my-vm-1:
        
               $ ssh my-vm-1
               
        - At the command prompt on my-vm-1, install the Nginx web server:
               
               $ sudo apt-get install nginx-light -y
        
        - Use the nano text editor to add a custom message to the home page of the web server:
               
               $ sudo nano /var/www/html/index.nginx-debian.html
        
        - Add text like this, and replace YOUR_NAME with your name:
              
               $ Hi from YOUR_NAME
        
        - Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
               
               $ curl http://localhost/
               
               - result: The response will be the HTML source of the web server's home page, including your line of custom text. 
                                              
        - To exit the command prompt on my-vm-1, execute this command:
        
               $ exit   
                              
    2- Get the external IP of the my-vm-1 instance from this command:
    
        $ gcloud compute instances list --zone us-central1-a          