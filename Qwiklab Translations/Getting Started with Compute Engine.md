## Lab:Getting Started with Compute Engine

## Objectives:

In this lab, you will learn how to perform the following tasks:

* Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

* Create a Compute Engine virtual machine using the gcloud command-line interface.

* Connect between the two instances.

## Task 1: Create a virtual machine using the GCP Console

## Steps:

1. Create a **compute engine** instance:


  `gcloud compute instances create my-vm-1 --machine-type "n1-standard-1" --image-project "debian-cloud" --image=debian-9-stretch-v20200902 --subnet "default" --tags=http-server`

  _for firewall rules_

  `gcloud compute firewall-rules create default-allow-http --direction=INGRESS --action=ALLOW --rules=tcp:80  --target-tags=http-server`

  > **Note**: The VM can take about two minutes to launch and be fully available for use.


  ## Task 2: Create a virtual machine using the gcloud command line


## Steps: 

1. To display a list of all the zones in the region to which Qwiklabs assigned you, enter this partial command **gcloud compute zones list | grep** followed by the region that Qwiklabs or your instructor assigned you to.

   Your completed command will look like this:

      `gcloud compute zones list | grep us-central1`

Choose a zone from that list other than the zone to which Qwiklabs assigned you. For example, if Qwiklabs assigned you to region **us-central1** and zone **us-central1-a** you might choose zone **us-central1-b**.  

2. To set your default zone to the one you just chose, enter this partial command **gcloud config set compute/zone** followed by the zone you chose.

   Your completed command will look like this:

      `gcloud config set compute/zone us-central1-b`


3. To create a VM instance called **my-vm-2** in that zone, execute this command:

    `gcloud compute instances create "my-vm-2" \
       --machine-type "n1-standard-1" \
       --image-project "debian-cloud" \
       --image "debian-9-stretch-v20190213" \
          --subnet "default"`

 > Note: The VM can take about two minutes to launch and be fully available for use.

4. To close the Cloud Shell, execute the following command:

       `exit`


## Task 4:


## Steps: Connect between VM instances

1. To open a command prompt on the **my-vm-2** instance:

      `gcloud compute ssh  my-vm-2`

2. Use the ping command to confirm that **my-vm-2** can reach **my-vm-1** over the network:

      `ping my-vm-1`

  > Notice that the output of the ping command reveals that the complete hostname of **my-vm-1** is **my-vm-1.c.PROJECT_ID.internal**, where **PROJECT_ID** is the name of your Google Cloud Platform project. GCP automatically supplies Domain Name Service (DNS) resolution for the internal IP addresses of VM instances.

3. Press **Ctrl+C** to abort the ping command.

4. Use the **ssh** command to open a command prompt on **my-vm-1**:

      `ssh my-vm-1`

  > If you are prompted about whether you want to continue connecting to a host with unknown authenticity, enter **yes** to confirm that you do. 

5. At the command prompt on **my-vm-1**, install the Nginx web server:

      `sudo apt-get install nginx-light -y`

6. Use the **nano** text editor to add a custom message to the home page of the web server:

      `sudo nano /var/www/html/index.nginx-debian.html`

7. Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace **YOUR_NAME** with your name:

       `Hi from YOUR_NAME`

8. Press **Ctrl+O** and then press **Enter** to save your edited file, and then press **Ctrl+X** to exit the **nano** text editor.

9. Confirm that the web server is serving your new page. At the command prompt on **my-vm-1**, execute this command:

    `curl http://localhost/`

  > The response will be the HTML source of the web server's home page, including your line of custom text.   

10. Copy the **External IP** address for **my-vm-1** and paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text. 


  > If you forgot to click **Allow HTTP traffic** when you created the **my-vm-1** VM instance, your attempt to reach your web server's home page will fail. You can add a firewall rule to allow inbound traffic to your instances, although this topic is out of scope for this course.

### Congratulations!

 In this lab, you created virtual machine (VM) instances in two different zones and connected to them using ping, ssh, and HTTP.
