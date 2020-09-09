# LAB: GCP Fundamentals: Getting Started with Compute Engine

## Objectives
In this lab, you will learn how to perform the following tasks:

    1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
    2. Create a Compute Engine virtual machine using the gcloud command-line interface.
    3. Connect between the two instances.

## Steps:
1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
     - Create Instance

            cloud compute instances create "my-vm-1" --machine-type "n1-standard-1" --image-project "debian-cloud"  --image "debian-9-stretch-v20190213"  --subnet "default" --tags http
     - Create Firewall Rules
     
            gcloud compute firewall-rules create allow-http --action=ALLOW --destination=INGRESS --rules=http:80 --target-tags=http

2. Create a Compute Engine virtual machine using the gcloud command-line interface.

    - Display a list of all the zones in the region and Choose a zone
    
            cloud compute zones list | grep us-central1
        
    -  Set your default zone to the one you just chose
    
            gcloud config set compute/zone us-central1-b
            
    - Create Instance

            gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud"  --image "debian-9-stretch-v20190213"  --subnet "default" --tags http

3. Connect between the two instances.

    _Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network_

    - Connect to my-vm-2:
    
            gcloud compute ssh my-vm-2
        
    - Ping my-vm-1:
    
            ping -c 10 my-vm-1
        
    - Use the ssh command to open a command prompt on my-vm-1:
    
            ssh my-vm-1 -y
        
    - At the command prompt on my-vm-1, install the Nginx web server:
    
            sudo apt-get install nginx-light -y
            
    - Use the nano text editor to add a custom message to the home page of the web server:
    
            sudo nano /var/www/html/index.nginx-debian.html
            
    - Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
    
             Hi from YOUR_NAME
             
    Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.
    
    - Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
    
            curl http://localhost/
            
    RESPONSE will be the HTML source of the web server's home page, including your line of custom text.
    
    - To exit the command prompt on my-vm-1, execute this command:
    
               exit
               
    - To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
    
            curl http://my-vm-1/
            
    RESPONSE will again be the HTML source of the web server's home page, including your line of custom text.

    _Get External IP of my-vm-1_
    
            gcloud compute instances list --zone us-central1-a

    _Paste it into the address bar of a new browser tab._
    
    RESPONSE You will see your web server's home page, including your custom text.
