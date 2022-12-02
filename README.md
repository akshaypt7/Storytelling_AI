# Storytelling_AI Deployment

## Create a service account for deployment

-Go to GCP Console, search for "Service accounts" from the top search box. or go to: "IAM & Admins" > "Service accounts" from the top-left menu and create a new service account called "deployment"

-Give the following roles:

-For deployment:

-Compute Admin

-Compute OS Login

-Container Registry Service Agent

-Kubernetes Engine Admin

-Service Account User

-Storage Admin

-Then click done.

-This will create a service account

-On the right "Actions" column click the vertical ... and select "Create key". A prompt for Create private key for "deployment" will appear select "JSON" and click create. This will download a Private key json file to your computer. Copy this json file into the secrets folder.

-Rename the json key file to deployment.json

-Follow the same process Create another service account called gcp-service

-For gcp-service give the following roles:

-Storage Object Viewer

-Then click done.

-This will create a service account

-On the right "Actions" column click the vertical ... and select "Create key". A prompt for Create private key for "gcp-service" will appear select "JSON" and click create. This will download a Private key json file to your computer. Copy this json file into the secrets folder.

-Rename the json key file to gcp-service.json

### SSH Setup

Configuring OS Login for service account

gcloud compute project-info add-metadata --project <YOUR GCP_PROJECT> --metadata enable-oslogin=TRUE
  
  
### Create SSH key for service account

cd /secrets
ssh-keygen -f ssh-key-deployment
cd /app
  
  
### Providing public SSH keys to instances
  gcloud compute os-login ssh-keys add --key-file=/secrets/ssh-key-deployment.pub
