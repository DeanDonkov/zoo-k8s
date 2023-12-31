# zoo-k8s

The project showcases how typically micro-service architectures are deployed.

In the first part I have created a [NodeJS backend](https://github.com/DeanDonkov/zoo-backend) that writes to both MongoDB and SQL databases. The connections to both databases are specified through environmental variables. We have a workflow on it that triggers based on the current branch we are on, and we have credentials to docker hub. 

Those credentials need to be entered through a secret in kubernetes(in the form of personal access token from dockerhub for example) and then the deployment image needs to be specified and we will have a fully working CI/CD.

Now, the CI/CD is one part. Then we have an ingress through nginx (i'm more familiar with nginx instead of HAproxy or traefik and prefer it to others) that routes to our service. As in the exercise it is stated that we do not want to expose databases.

The ingress can be further configured to support TLS through domain. It can also further be configured to even do a SSL passthrough to mongo & mysql services.

I have deployed a grafana dashboard to keep track of deployments, services, namespaces. Based on the data from grafana we can make a measured decision when deploying to a cloud such as AWS, GCP or DigitalOcean, based on performance metrics from it.

I have chosen not to create a frontend as it follows the same principles to fetch/edit/remove data from the backend through HTTP/S requests to our backend url, configured with kubernetes internal DNS, passed through an environment variable. 

If we want to host N number of web servers we will just deploy the container to the cluster and expose it through the nginx ingress, then on a raspberry pi for example that is connected to the internet just load the url ideally through HTTPS if there is javascript involved.

