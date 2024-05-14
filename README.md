# Tweet Trend Application

This is a small application which contains main and test folders.  
Main contains application code.  
Test contains test cases.  
It also contains pom.xml which has all dependencies and artifact name and version.

## Technologies Used

This project leverages a robust set of tools and technologies to ensure efficient development, deployment, and monitoring:

- **Docker**: Containerization of applications.
- **Kubernetes**: Orchestration and management of containerized applications.
- **Ansible**: Automated configuration management and deployment.
- **Terraform**: Infrastructure as code for provisioning and managing cloud resources.
- **Maven**: Build automation and dependency management.
- **AWS**: Cloud computing services for scalable and reliable infrastructure.
- **Prometheus**: Monitoring and alerting toolkit.
- **Grafana**: Visualization and analytics for monitoring data.
- **Helm**: Package manager for Kubernetes.
- **JFrog Artifactory**: Universal artifact repository manager.

These technologies work together to create a seamless CI/CD pipeline, enabling efficient and reliable deployment and maintenance of the application.

## Deployment on AWS EC2

The entire Ttrend application has been deployed on an AWS EC2 instance to take advantage of the cloud's scalability and reliability. All project files, including the application code, test cases, and dependencies specified in the `pom.xml` file, are consolidated in a single repository. This setup ensures that everything required to build and run the application is readily available in one place.

### Steps to Deploy

1. **Setup AWS EC2 Instance**: 
   - Launch an EC2 instance with the desired configuration.
   - Configure security groups to allow necessary inbound and outbound traffic.

2. **Install Dependencies**:
   - Ensure Docker, Kubernetes, Ansible, Terraform, and Maven are installed on the EC2 instance.

3. **Clone Repository**:
   - Clone the repository containing all project files to the EC2 instance.
   - `git clone https://github.com/sakiphan/tweet-trend.git`

4. **Build and Deploy Application**:
   - Use Maven to build the application.
   - Dockerize the application and push the image to a Docker registry.
   - Use Kubernetes to orchestrate the deployment of the Dockerized application.
   - Use Helm for managing Kubernetes packages.
   - Use Ansible and Terraform for automating deployment and infrastructure provisioning.

5. **Monitoring and Logging**:
   - Set up Prometheus and Grafana for monitoring application performance.
   - Configure alerts and dashboards in Grafana to visualize metrics collected by Prometheus.

6. **Artifact Management**:
   - Use JFrog Artifactory to manage application artifacts and dependencies.

By consolidating all the necessary files and configuration in a single repository, the deployment process becomes streamlined, and maintaining the application becomes more manageable. This approach also facilitates continuous integration and continuous deployment (CI/CD) practices, ensuring that updates and changes can be efficiently tested and deployed.