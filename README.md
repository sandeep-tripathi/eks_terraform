*Deploy in EKS Cluster with Terraform*
##### AWS Cloud Shell######
ssh cloud_user@<PUBLIC_IP_ADDRESS>

#Configure the AWS CLI
$ aws configure


$ cd eks_terraform/    # Terraform manifest is stored here
# Deploy the EKS Cluster using Terraform
Initialize the working directory:
$ terraform init

$ terraform plan
$terraform apply

# Configure kubectl to interact with the cluster (Context selection):
$ aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)
Confirm that kubectl was configured properly and that the cluster was successfully deployed:

$ kubectl get cs   # The all the components should be up and running with a status of Healthy.

#Deploy the NGINX Pods#
$ wget https://raw.githubusercontent.com/ACloudGuru-Resources/content-terraform-2021/main/nginx.tf
$ terraform plan
$ terraform apply

$ kubectl get deployments  # The two long-live-the-bat pods should both be up and running.

#Destroy Your Cluster

$ terraform state list    #Before you destroy the infrastructure, view the resources Terraform is managing:

#Destroy all of the resources you just created:
$ terraform destroy



