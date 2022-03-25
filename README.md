# Rancher Proof of Concept

## Rancher Server

1. Start a Rancher server with: `docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged rancher/rancher:latest`
2. Login with 'localhost' in your browser
3. Get the admin password from the logs: `docker logs  container-id  2>&1 | grep "Bootstrap Password:"`
4. Update the server IP to your local IP (not localhost)

## Create and import a k3d dev cluster

1. Start k3d cluster with: `k3d cluster create --image=rancher/k3s:v1.21.11-rc1-k3s1 --agents 3 dev`
2. Import the k3d cluster in Rancher: Import Existing (home page) -> Generic -> name: 'dev'
3. Run Rancher agent in cluster (follow instructions on registration page) by installing with unsecure method (option 2)
4. Wait for the 'dev' cluster to become ready in the UI

## Configure cluster services

1. Go to cluster tools and install monitoring, CIS benchmark, logging and OPA Gatekeeper with default settings
2. Create a user in the global settings
3. Create a project 'hello' in the imported dev cluster and add the above created user as a member
