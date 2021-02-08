# GCP_lb_tf

cd ~/terraform-google-lb-http/examples/multi-backend-multi-mig-bucket-https-lb

sed -i 's/1.0.0/5.1.0/g' mig.tf

terraform init

terraform plan -out=tfplan -var 'project=<PROJECT_ID>'

terraform apply tfplan

Run the following to get the external URL:

EXTERNAL_IP=$(terraform output | grep load-balancer-ip | cut -d = -f2 | xargs echo -n)
echo https://${EXTERNAL_IP}

to test:
https://EXTERNAL_IP/group1
https://EXTERNAL_IP/group2
https://EXTERNAL_IP/group3
